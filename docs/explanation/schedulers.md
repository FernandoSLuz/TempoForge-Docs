# Schedulers and tempo

After this page you can choose between the two shipped schedulers, set every field on a
scheduler asset, and say why swapping one on a running battle is not offered.

---

## The scheduler asset

A scheduler is a ScriptableObject created from **Assets > Create > TempoForge > Scheduler**,
and every encounter references exactly one. Four fields carry all of its behaviour.

| Field | Applies to | What it sets |
| --- | --- | --- |
| `StateTag` | Both | `ActionOrder` or `Atb`. This field *is* the choice of scheduler |
| `NoActionRecoveryTicks` | Both | Recovery charged when an opportunity produces no action. 1 to 1,000,000 |
| `InputPausePolicy` | ATB only | What the clock does while a player decision is pending |
| `GaugeThresholdUnits` | ATB only | Gauge units a combatant must accumulate to act. 1 to 1,000,000 |

`NoActionRecoveryTicks` is spent whenever a combatant reaches the head of the queue and does
nothing: a stun or other preventing status blocked it, or its AI policy found no legal
command. Without it that combatant would be handed the same opportunity again on the same
tick, so the value must be at least one. The two shipped assets set it identically:

| Field | `scheduler.action-order.v1` | `scheduler.atb.v1` |
| --- | --- | --- |
| `NoActionRecoveryTicks` | 30 | 30 |
| `InputPausePolicy` | unset | `PauseOnInput` |
| `GaugeThresholdUnits` | 0 | 1,000,000 |

!!! warning
    An Action Order asset must carry no input policy and no gauge threshold, and the input
    policy field has to hold zero — which is not one of the policy's named values. Copy the
    shipped `scheduler.action-order.v1` asset rather than creating one from scratch. Every
    rejection is an `authoring.value.invalid` error naming the offending field, such as
    `scheduler.input-policy`, and the Content Validator selects that field for you.

## Action Order

Combatants take discrete turns in rounds. At the start of a round every eligible combatant
becomes a participant; the round ends when all of them have resolved, and a new one begins
immediately. A combatant that dies or whose team concedes mid-round counts as resolved
rather than stalling the round.

Order inside a round is by earliest ready tick, with ties broken by stable ID. After acting,
a combatant's next ready tick is its skill's recovery **divided by its effective speed**: at
speed 1.0 recovery is spent as authored, at speed 2.0 it is halved. Speed therefore shortens
the gap between your turns; it never buys extra turns within a round.

Only one decision is ever outstanding. The scheduler refuses to advance a single tick while
a decision waits, so `AdvanceTicks` returns `AwaitingCommand` and the timeline strip shows
exactly one chip.

## ATB and the gauge

Each combatant carries a gauge that gains its effective speed in units every tick. When the
gauge reaches `GaugeThresholdUnits` the combatant is handed a decision, and the threshold is
*subtracted* rather than the gauge being cleared, so overflow carries into the next fill.

At the shipped threshold of 1,000,000, a combatant at speed 1.0 acts every 100 ticks.
Effective speed may not exceed the threshold: a faster combatant is a
`scheduler.speed.invalid` failure rather than one acting twice in a tick.

After acting, a combatant's gauge stops filling until its recovery ticks have elapsed. Note
the asymmetry with Action Order — here recovery is spent as authored and speed is applied to
the fill instead.

Because several gauges can cross on the same tick, more than one decision can be outstanding
and the timeline strip can show several chips at once. A team member may start part-charged
through `InitialAtbGauge` on the team asset, which must be below the threshold, and must be
zero under Action Order.

## Waiting for a player decision

`InputPausePolicy` decides what the rest of the battle does while a player-controlled
combatant is being asked to choose. It applies to ATB only; Action Order always freezes.

| Policy | While a player decision is pending |
| --- | --- |
| `PauseOnInput` | Nothing moves. The tick stops until you submit |
| `WaitForInput` | Timers keep running, but every other gauge is held one unit below the threshold, so nobody else becomes ready |
| `Active` | Gauges keep filling and other combatants can become ready and queue behind the player |

!!! warning
    Only `PauseOnInput` gives a player a battle they can reproduce. Under the other two the
    tick a command lands on depends on how long the player took to click, so the same
    choices produce a different battle. Recording and replay still reproduce a run exactly,
    because the replay carries each command's requested tick.

An AI-controlled decision never waits on you, whatever the policy: the engine resolves it
from the combatant's AI policy inside the same call.

## Part of encounter identity

The scheduler is authored on the encounter, and the engine binds it once at
`BattleEngine.Create`. No API changes it afterwards, by design:

- A snapshot carries its scheduler state, and `Restore` refuses a snapshot whose scheduler
  ID, contract version, state tag, ATB threshold or input policy differs from the compiled
  content it is handed.
- The `adjust-scheduler` effect primitive is scheduler-specific. Action Order accepts only
  `ReadyTickDelta` adjustments, ATB only `GaugeDelta`. Every such effect in a catalog is
  checked against the resolved scheduler at `Create`, so one catalog cannot hold both a
  ready-tick haste effect and an ATB encounter.

To offer a choice of tempo, author two encounters — and two catalogs if either uses
scheduler-adjusting effects. That is why the shipped demo compiles a starter catalog and a
separate ATB catalog, and why its scenario picker spans already-compiled variants instead of
swapping a preset on a live battle.

## Registering your own

`BattleSchedulerRegistry` is immutable: `Register` returns a new registry, and one scheduler
ID plus contract version may appear only once. A custom scheduler implements
`IBattleScheduler` and must supply a canonical state codec, either by also implementing
`ISchedulerStateCodecProvider` or by passing an `ISchedulerStateCodec` to `Register`. The
codec's ID and contract version must match the scheduler's, and its state tag must still be
`ActionOrder` or `Atb` — there is no third state shape. Add an `ISchedulerAdjustmentAdapter`
if your content adjusts tempo.

```csharp
var schedulers = BattleSchedulerRegistry.CreateWithBuiltIns()
    .Register(new MyScheduler());

var compiled = new BattleContentCompiler().Compile(new AuthoringCompileRequest(
    catalog, schedulers, BattleMechanicsRegistry.CreateWithBuiltIns()));

var encounter = compiled.CatalogSnapshot.Encounters[0].Value;
var engine = BattleEngine.Create(
    compiled.CatalogSnapshot.BattleContent, encounter.StartRequest, seed,
    compiled.CatalogSnapshot.SchedulerRegistry,
    compiled.CatalogSnapshot.MechanicsRegistry);
```

Compile with the same registry you create the engine with. The authored asset's stable ID
must equal the registered `SchedulerId` and its `SchedulerContractVersion` must be `1`. An
unknown ID fails as `scheduler.registry.missing`, and a known ID at another version as
`scheduler.version.unsupported`. A catalog may hold up to 16 scheduler definitions.

## Next

- **[The engine loop](engine-loop.md)** — what `AdvanceTicks` does with scheduler work.
- **[Combatants, teams and encounters](../how-to/author-combatants-and-encounters.md)** —
  where the scheduler and the starting gauge are assigned.
- **[Determinism](determinism.md)** — the rest of what `PauseOnInput` protects.
