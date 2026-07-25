# Determinism

A battle is a function of four inputs: the compiled content, the encounter start request, the
seed, and the commands submitted into it. This page names the properties that guarantee that,
and the choices on your side that can still spoil it.

---

## No engine references

`TempoForge.Simulation` is compiled with `noEngineReferences: true` and references no other
assembly. It cannot see `UnityEngine` at all -- not `Random`, not `Time`, not `GameObject`.
`TempoForge.Analysis`, which runs Monte Carlo batches, is compiled the same way.

That is a compile-time guarantee rather than a coding rule. Simulation code cannot reach a
frame counter or a system clock, so nothing in a battle can depend on when or where it ran.

`TempoForge.Authoring` does reference Unity, because definitions are `ScriptableObject`
assets. Authoring runs before the battle: it produces compiled content and then steps out of
the way. [Architecture](architecture.md) covers how the layers sit.

## Fixed-point numbers

There is no `float` or `double` anywhere in the simulation or analysis assemblies. Every
quantity a battle reasons about is integer-backed, so there is no platform-dependent
floating-point drift between a phone and a desktop.

| Type | Scale | Represents |
| --- | --- | --- |
| `Fixed64` | 10,000 | Amounts: damage, healing, stat values, multipliers |
| `Chance64` | 1,000,000 | Probabilities, from `Chance64.Zero` to `Chance64.Guaranteed` |

The two are deliberately separate types. A `Chance64` is range-checked on construction, so a
probability cannot silently exceed 100%; use `Chance64.Clamp` when you want clamping rather
than an exception.

Arithmetic is `checked`. Division rounds to nearest with exact halves rounding away from
zero, and an overflow throws instead of wrapping into a different battle.

### Never print these types directly

`Fixed64.ToString()` and `Chance64.ToString()` return the raw scaled integer, because their
string form feeds canonical encoding and must never drift. A label that prints one shows
`50000` instead of `5`, and `875000` instead of `87.5%`.

Format through `BattleNumberFormat`, which lives in the presentation layer and is integer
arithmetic throughout:

```csharp
BattleNumberFormat.Amount(value);           // "5.25"
BattleNumberFormat.WholeAmount(value);      // "5"
BattleNumberFormat.AmountRange(min, max);   // "10-14"
BattleNumberFormat.Percent(chance);         // "87.5%"
BattleNumberFormat.Ticks(ticks);            // "12t"
```

## Seeded, ordered RNG

Randomness comes from `DeterministicRng`, built with `DeterministicRng.FromSeed(uint)`. The
engine takes that seed as a `uint` when you create it.

`DeterministicRng` is an immutable struct. Every draw returns a **new** generator alongside
its value:

```csharp
var advanced = rng.NextBelow(6u, out var roll);
```

There is no shared mutable generator and no global to draw from out of order. The state has
to be threaded through whatever consumed it, which puts the draw order in the code rather
than at the mercy of timing.

Because the state is plain data, a snapshot carries it. `snapshot.Rng` is the generator as of
that tick, and restoring it resumes the same sequence. `DeterministicRng.TryRestore` refuses
an all-zero state and hands back a diagnostic instead of a degenerate generator.

`BattleBatchRunner.Run` and `RunParallel` hold no state for the same reason, so a thousand
seeds spread across worker threads give the same per-seed results as running them one at a
time. The shipped audits assert that, and also assert identical results under the `en-US`,
`tr-TR` and `ar-SA` cultures.

## The visual clock is separate

Presentation runs on its own clock and cannot feed a value back into the battle.

`BattlePresenter.Tick(deltaSeconds)` scales its delta by `presenter.Speed` and spends it on
beats, bars, pips, plates and floating numbers. `presenter.SkipAll()` finishes every queued
beat immediately. Neither touches a simulation value. The presenter holds no `BattleEngine`
and cannot obtain one, and a presenter-purity audit in the test suite enforces that.

The skin behaves the same way. `MotionScale = 0` and `ReduceMotion = true` change how long
transitions take and nothing else; a skin never enters a snapshot, a replay, or a hash.

What *is* authoritative is the integer tick count your driver hands to `AdvanceTicks`.
Accumulated real time is never authoritative and is never replayed. See
[The engine loop](engine-loop.md).

## What can still break it

!!! warning "The engine cannot protect you from its own inputs"
    Vary the content, the start request, the seed, or the tick a command lands on, and you
    have a different battle. Everything below is one of those four.

| Your choice | What happens | What to do instead |
| --- | --- | --- |
| Seeding from `UnityEngine.Random`, `DateTime.Now`, or a frame count | A different battle every run | Choose the seed yourself, store it, and show it |
| Editing a definition asset between runs | The same seed gives a different result | Compare `snapshot.ContentManifestHash` |
| Submitting a command at a different tick | A different battle: `CommandSequence` and `RequestedTick` are part of the input | See below |
| Registering different mechanics implementations | `snapshot.RegistryBindingHash` differs and a replay is refused | Keep registry bindings stable, or re-record |
| Changing a stable ID | Replays that reference it break | Rename assets freely; never change their IDs |

A command whose `RequestedTick` is not the engine's current tick is rejected with the
`command.tick.mismatch` diagnostic rather than being quietly applied at another moment.

### Human decisions and presentation speed

The Action Order scheduler never advances while any decision is pending, so a human decision
always lands on the tick the decision was raised at, whatever the presentation is doing.

ATB has a choice, authored as `InputPausePolicy` on the scheduler definition. It is an
ATB-only field: leave it unset on an Action Order scheduler or compilation reports it.

| Policy | While a human decision is pending |
| --- | --- |
| `PauseOnInput` | The scheduler stops advancing until the command arrives |
| `WaitForInput` | Gauges keep charging but are held below the threshold, so no second decision arrives |
| `Active` | Everything keeps advancing and other combatants can become ready |

`PauseOnInput` is what makes a human-decision ATB battle reproducible. Under `Active`, a
player who answers while the presentation runs at 4x submits at a different tick from one at
1x. The shipped starter scenarios are all automatic, so this only arises once you author a
human-controlled combatant. See [Schedulers and tempo](schedulers.md).

## Next

- **[The engine loop](engine-loop.md)** -- what one `AdvanceTicks` call does with your ticks.
- **[Record and replay a battle](../how-to/record-and-replay.md)** -- what the hashes are for.
- **[Troubleshooting](../how-to/troubleshooting.md)** -- symptoms this page does not cover.
