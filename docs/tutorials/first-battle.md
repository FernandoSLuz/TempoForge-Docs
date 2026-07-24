# 1. Getting started

Goal: a battle running on screen, then the same battle reproduced exactly, then your own
combatant in it. About twenty minutes.

---

## Install

1. Import the TempoForge package into a Unity **2022.3 LTS or newer** project.
2. That is all. No dependencies, no packages, no render-pipeline setup.

Everything ships under `Assets/TempoForge/`. Nothing is written outside it.

## Five-minute first success

Open `Assets/TempoForge/Samples/RuntimeDemo/TempoForgeDemo.unity` and press Play.

You should see the stage with combatant tokens, nameplates carrying health and shield
bars, a turn-order strip along the top, a rolling battle log, and scenario and playback
controls in the corner.

Try these:

- **`<` / `>`** step through the eight shipped encounters.
- **Seed** -- type a number and press **Start**.
- **Pause / Speed / Skip** -- visuals only. More on that below.

If the interface renders as flat rectangles with no shading, see
[Troubleshooting > the interface looks flat](../how-to/troubleshooting.md#the-interface-looks-flat).

## Prove determinism

This is the property everything else rests on, so see it directly:

1. Note the seed. Run the encounter to completion and watch the log.
2. Press **Start** again with the *same* seed. The same events resolve in the same order
   with the same numbers.
3. Change the seed by one. The battle diverges.

The same `(encounter, scheduler, formation, seed)` tuple always produces identical state
hashes and an identical replay.

**Pause, speed, and skip scale the visual clock only.** They never touch a simulation
value, so a battle watched at 4x and a battle watched paused-and-stepped produce the same
result. That separation is what makes a replay trustworthy.

## Start a battle from your own code

The **driver owns the engine**. The presenter and interface only receive values. Minimum
real loop:

```csharp
using TempoForge.Authoring;
using TempoForge.Simulation;
using UnityEngine;

public sealed class MyBattleDriver : MonoBehaviour
{
    [SerializeField] private BattleContentCatalog catalog;

    private const float TicksPerSecond = 30f;

    private BattleEngine engine;
    private CompiledAuthoringCatalog compiled;
    private float accumulator;

    private void Start()
    {
        // Compile the authored catalog once, with the built-in registries.
        var result = new BattleContentCompiler().Compile(
            AuthoringCompileRequest.WithBuiltIns(catalog));

        if (!result.Succeeded)
        {
            // Diagnostics name the exact asset and field that failed.
            for (var i = 0; i < result.Diagnostics.Count; i++)
                Debug.LogError(result.Diagnostics[i].Message);
            return;
        }

        compiled = result.CatalogSnapshot;

        var encounter = compiled.Encounters[0].Value;
        engine = BattleEngine.Create(
            compiled.BattleContent,
            encounter.StartRequest,
            seed: 12345u,
            compiled.SchedulerRegistry,
            compiled.MechanicsRegistry);
    }

    private void Update()
    {
        if (engine == null) return;

        // Convert elapsed presentation time into an integer tick count.
        // Accumulated time is never authoritative and is never replayed.
        accumulator += Time.deltaTime * TicksPerSecond;
        var ticks = (int)accumulator;
        if (ticks <= 0) return;
        accumulator -= ticks;

        var step = engine.AdvanceTicks(ticks);

        if (step.Outcome == AdvanceTicksOutcome.Terminal)
            Debug.Log("Result: " + step.Snapshot.Result.ResultId.Value);
    }
}
```

Compile once, run many battles. Compilation freezes the assets; creating an engine is the
cheap part.

## Add presentation

To get the stage and interface, hand the presenter a binding and forward your visual
delta:

```csharp
var presenter = presenterHost.AddComponent<BattlePresenter>();
var log  = new PresentationLog();
var pool = new BuiltInPoolAdapter(presenterHost.transform, log);

presenter.Bind(new PresenterBinding(
    compiled,
    encounter.FormationLayout,
    recipeSet,                            // PresentationRecipeSet asset
    new BuiltInAnimationAdapter(log),
    new BuiltInVfxAdapter(pool, log),
    new BuiltInAudioAdapter(audioSource, log),
    pool,
    labels,                               // DisplayStringTable
    uiRoot));                             // BattleUiRoot, optional

// Each frame, after advancing the engine:
presenter.EnqueueEvents(step.Events);
presenter.AdoptSnapshot(step.Snapshot);
presenter.Tick(Time.deltaTime);           // beats, bars, plates, numbers
```

Add **TempoForge > Battle Stage Frame** next to the presenter to control where the stage
sits and how much screen you reserve for your own interface.

## Author your own combatant

1. **Assets > Create > TempoForge > Combatant**.
2. Give it a **Stable Id** such as `combatant.my-hero`. This is a compatibility contract:
   renaming the *asset* is safe, changing the *id* is not.
3. Set stats, resources, and granted skills. The starter definitions in
   `Assets/TempoForge/Samples/StarterContent/` are worked examples of every asset type.
4. Add it to your `BattleContentCatalog`.
5. **Tools > TempoForge > Content Validator** and fix anything it reports.
6. Reference it from a team in an encounter, then run it.

Detail in [guide 3](../how-to/author-content.md).

## Two things that catch everyone

### Displaying numbers

`Fixed64` and `Chance64` hold raw scaled integers, so `ToString()` gives `50000`, not
`5`. That is intentional -- their string form feeds canonical encoding and must never
drift. Use `BattleNumberFormat` for anything a player reads:

```csharp
BattleNumberFormat.Amount(value);           // "5.25"
BattleNumberFormat.AmountRange(min, max);   // "10-14"
BattleNumberFormat.Percent(chance);         // "87.5%"
BattleNumberFormat.WholeAmount(value);      // "5"
```

### The interface submits nothing

`BattleUiRoot` raises `CommandChosen` with the player's intent. **Your driver** builds and
submits the command:

```csharp
ui.CommandChosen += choice =>
{
    var snapshot = engine.GetSnapshot();

    var command = choice.IsConcede
        ? BattleCommand.Concede(snapshot.NextCommandSequence, snapshot.Tick, choice.ActorId)
        : new BattleCommand(
            snapshot.NextCommandSequence, snapshot.Tick, BattleIds.UseSkillCommand,
            choice.ActorId, choice.SkillId, choice.Targets, PropertySet.Empty);

    engine.Submit(command);
};
```

That separation is what makes the interface incapable of desynchronising a battle.

## Next

- **[Core concepts](../explanation/architecture.md)** -- read before writing much code.
- **[Skins and presets](../tutorials/skinning-your-battle.md)** -- make it look like your game.
