# 4. Take a decision from the player

By the end of this page a click in the skill tray becomes a command your driver submits, a hover
fills the tooltip with previewed numbers, and every id on screen reads as a name.

## What the interface offers

A bound presenter compiles the legal command shapes on every adopted snapshot with
[`DecisionShapeCompiler`](../reference/interface-and-widgets.md#decisionshapecompiler) and hands them
to `BattleUiRoot.ShowDecision`, so the tray fills itself. A skill reaches it only when:

- The first decision entry is a **human** control kind and its actor is living. Otherwise the result
  is `DecisionOptions.None` and the tray hides entirely.
- The actor has no cooldown entry for that skill.
- Every cost in the skill's timing is payable from the actor's current resources.
- No status on the actor restricts one of the skill's tags.
- The skill's target resolver resolves in the mechanics registry.

Offered skills are sorted by skill id, so button order is stable between frames and between runs. The
concede button appears only when the compiled content registers the concede command, and the tray
draws at most twelve buttons.

### The target shape on each button

Each [`SkillCommandShape`](../reference/interface-and-widgets.md#skillcommandshape) carries a
[`TargetShape`](../reference/interface-and-widgets.md#targetshape) from the compiled target contract.
It is what the player may aim at, not the engine's resolution.

| Field | What it tells the player |
| --- | --- |
| `Relation` | `Self`, `Ally`, `Enemy` or `Any`. The tray caption says "one enemy", "3 ally", "auto self". |
| `LifeState` | Whether living, dead, or any combatants may be picked. |
| `MinimumTargets` / `MaximumTargets` | How many ids the command may carry. |
| `MaximumResolvedTargets` | How many combatants the effect can end up hitting. |
| `ActorMayAppear` | Whether the actor can be among its own targets. |
| `AutomaticSelection` | Sending no ids lets the resolver choose. The caption reads "auto". |

`DecisionOptions` is a display projection: compiling it reads a snapshot and a compiled catalog and
calls no engine mutator, so rebuilding it can never change a battle.

## Submit the command yourself

`BattleUiRoot` raises `CommandChosen` with the player's intent and stops there. Your driver turns
that intent into a [`BattleCommand`](../reference/commands-events-and-snapshots.md#battlecommand) and
submits it:

```csharp
ui.CommandChosen += choice =>
{
    var snapshot = engine.GetSnapshot();

    // Ignore a click that arrived after the pending actor changed.
    var pending = snapshot.PendingDecisionActorId;
    if (!pending.HasValue || pending.Value != choice.ActorId) return;
    var command = choice.IsConcede
        ? BattleCommand.Concede(snapshot.NextCommandSequence, snapshot.Tick, choice.ActorId)
        : new BattleCommand(
            snapshot.NextCommandSequence, snapshot.Tick, BattleIds.UseSkillCommand,
            choice.ActorId, choice.SkillId, choice.Targets, PropertySet.Empty);

    var result = engine.Submit(command);
    if (result.CommandEvent != null) presenter.EnqueueEvents(new[] { result.CommandEvent });
    presenter.AdoptSnapshot(engine.GetSnapshot());
};
```

The returned [`CommandResult`](../reference/running-a-battle.md#commandresult) reports `Accepted`,
`Rejected`, `TransportRejected` or `FatalInvariant`, with `ReasonId` naming a rejection, and a
rejected command leaves the battle exactly as it was. That separation is what makes the interface
incapable of desynchronising a simulation.

### Targets the player picked

The shipped tray raises a chosen skill with an **empty** target list, which suits shapes that select
automatically. For hand-picked targets, run your own selection step and call
`ui.ChooseSkill(skillId, pickedIds)`; `SkillTrayView.SetSelected` and `ClearSelection` highlight the
pending button while the player chooses.

!!! tip
    Number keys 1-9 and Escape drive the tray only when the legacy Input Manager is enabled
    (**Project Settings ▸ Player ▸ Active Input Handling**). Pointer input always works, and
    `BattleUiRoot.LegacyInputAvailable` reports which case you are in.

## Fill a tooltip with a forecast

The tooltip panel renders a [`TooltipData`](../reference/interface-and-widgets.md#tooltipdata) value
verbatim and calls no preview API of its own. Compute one per offered skill and store it with
`SetTooltip`; a hover shows the stored value, and a skill with none stored shows nothing.

```csharp
var options = DecisionShapeCompiler.Compile(snapshot, compiled);

foreach (var shape in options.Skills)
{
    // Text-only is enough to ship: cost, timing, target shape.
    ui.SetTooltip(TooltipData.TextOnly(
        shape.SkillId, "12 stamina", "Cast 6t, recover 4t", "one enemy"));
}
```

Recompute only when the pending actor or tick changes, not every frame.

### Where the numbers come from

Plan the skill's effect through `MechanicsRegistry.ResolveEffect(...).Plan(...)`, then price one
planned primitive with [`BattleFormulaService`](../reference/effects-and-mechanics.md#battleformulaservice).
`Preview` returns `Minimum`, `Maximum`, `HitChance` and `CriticalChance` for a damage or healing
primitive; `PreviewStatusApplication` returns the `FinalChance` of a status landing after resistance.
Pass those into the full `TooltipData` constructor. The panel formats the range and hides the crit and
status rows when those chances are impossible. `TempoForgeDemoBootstrap.BuildTooltip` in the runtime
demo is the worked example.

To answer "what happens if I do nothing", run
[`BattleForecast`](../reference/scheduling-and-tempo.md#battleforecast) with a
[`ForecastRequest`](../reference/other.md#forecastrequest) of tick, action and event budgets. It runs
a copy of the battle, so the live engine is untouched, and reports why it stopped: `HorizonReached`,
`Terminal`, `NoScheduledWork`, `ActionLimit`, `EventLimit`, or `UnknownHumanDecision`.

!!! warning
    A forecast is not a promise. It stops at the first human decision because it cannot know what the
    player will choose, and a request outside the structural budgets returns `FatalInvariant` with a
    diagnostic instead of a partial answer.

## Numbers and names players read

`Fixed64` and `Chance64` hold raw scaled integers, so `ToString()` gives `50000`, not `5`. Their
string form feeds canonical encoding and must never drift, so format anything a player reads with
[`BattleNumberFormat`](../reference/interface-and-widgets.md#battlenumberformat):

```csharp
BattleNumberFormat.Amount(value);           // "5.25"
BattleNumberFormat.WholeAmount(value);      // "5"
BattleNumberFormat.AmountRange(min, max);   // "10-14", or "12" when both ends match
BattleNumberFormat.Percent(chance);         // "87.5%"
BattleNumberFormat.Ticks(12);               // "12t"
```

Names work the same way. Compiled snapshots carry no labels, so the driver supplies a
[`DisplayStringTable`](../reference/interface-and-widgets.md#displaystringtable) through the presenter
binding. It maps stable ids to display text for the roster, timeline, tray, feedback log and result
banner, and an unmapped id falls back to its raw id text rather than to an empty label. The table
never enters a hash and never affects an outcome, which is why it can be swapped per language.

## Next

- **[5. Restyle the interface](skinning-your-battle.md)** — make the tray and tooltip look like your game.
- **[What each interface region draws](../how-to/interface-regions.md)** — what every region renders, and what it refuses to do.
- **[Step a battle in the Workbench](../how-to/balance-with-the-workbench.md)** — when a previewed number is not the number you expected.
