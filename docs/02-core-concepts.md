# 2. Core concepts

Three roles and one hard boundary. Almost every integration problem comes from blurring
the boundary, so it is worth being precise about it.

---

## The three roles

```
   YOUR DRIVER                 owns the engine
        |                      creates it, advances it, submits commands
        | events + snapshots
        v
   BattlePresenter             receives values, drives visuals
        |                      never calls Submit, AdvanceTicks, a forecast, or RNG
        v
   BattleUiRoot                offers legal choices, raises intent
                               submits nothing
```

**The driver is the single engine owner.** The presenter holds no `BattleEngine` and
cannot obtain one. The interface raises a plain C# event carrying what the player picked;
the driver turns that into a command and submits it.

This is enforced by a presenter-purity audit in the test suite, not by convention.

## Why the boundary matters

Because it is what makes a replay trustworthy. If presentation could reach into the
engine -- even to peek at RNG -- then frame timing, animation speed, or a dropped frame
could change an outcome. With the boundary intact:

- Pause, speed, and skip scale the visual clock only.
- The same `(encounter, scheduler, formation, seed)` tuple always yields the same hashes.
- A battle recorded on a phone replays identically on a desktop.

## Determinism is structural

`TempoForge.Simulation` is compiled with `noEngineReferences: true`. It has no access to
`UnityEngine` at all -- not `Random`, not `Time`, not `GameObject`.

Numbers are fixed-point:

| Type | Scale | Represents |
| --- | --- | --- |
| `Fixed64` | 10,000 | Amounts: damage, healing, stat values |
| `Chance64` | 1,000,000 | Probabilities |

Both are integer-backed, so there is no platform-dependent floating-point drift. RNG is
`DeterministicRng`, seeded explicitly and advanced in a defined order.

**Never show `Fixed64.ToString()` to a player.** It returns the raw scaled integer because
that string feeds canonical encoding. Use `BattleNumberFormat`.

## The content pipeline

```
Definition assets              stats, skills, effects, statuses, reactions,
      |                        AI policies, formations, teams, encounters
      v
BattleContentCatalog           the collection you hand to the compiler
      |
      v
BattleContentCompiler          validates and freezes
      |
      v
CompiledAuthoringCatalog       immutable; carries a content manifest hash
      |
      v
BattleEngine.Create(...)       + encounter start + seed
```

Compilation is where authoring mistakes surface. `Compile` returns diagnostics naming the
exact asset and field; `Validate` does the same without producing content.

The compiled catalog carries a **content manifest hash**, and snapshots carry it too. If a
replay was recorded against different content, you can detect it rather than silently
mis-playing it.

## Stepping the engine

The driver converts elapsed presentation time into an integer tick count:

```csharp
var step = engine.AdvanceTicks(ticks);
step.Outcome     // ReachedTarget, Terminal, NoScheduledWork, FatalInvariant
step.Events      // what happened, in order
step.Snapshot    // authoritative state afterwards
```

Accumulated real time is **never** authoritative and never replayed -- only the integer
tick count is. That is the whole trick to frame-rate independence here.

Four outcomes, all of them ordinary data:

| Outcome | Meaning |
| --- | --- |
| `ReachedTarget` | Advanced the requested ticks; battle continues |
| `Terminal` | A result was reached (victory, defeat, draw, concession, stalled) |
| `NoScheduledWork` | Nothing left to schedule |
| `FatalInvariant` | An invariant broke; stop pumping rather than looping on exceptions |

Note `stalled` is a *terminal result*, not a crash: a battle that cannot progress ends
cleanly instead of hanging.

## Schedulers set the tempo

A scheduler decides who acts and when. Two ship:

| Scheduler | Behaviour |
| --- | --- |
| **Action Order** | Classic queue. Actors take discrete turns in a computed order. |
| **ATB** | Each combatant charges a gauge; acting when it fills. |

The scheduler is part of encounter identity, not a runtime toggle. Picking a different
scheduler means picking a different authored encounter -- which is why the demo's scenario
picker spans already-compiled variants rather than swapping a preset on a live battle.

Register your own through the scheduler registry.

## Commands and events

**Commands** are intent going in: use a skill, concede. Each carries a sequence number and
the tick it was requested at, so ordering is explicit rather than arrival-dependent.

**Events** are facts coming out: damage resolved, status applied, cast started, combatant
died. The presenter derives one *beat* per event through a recipe, which is how visuals
stay decoupled from mechanics.

## Snapshots

A `BattleSnapshot` is the complete authoritative state at a tick: combatants, statuses,
shields, resources, cooldowns, scheduler state, decision entries, and the result. It is
immutable and safe to hold.

The interface renders snapshots verbatim. It does not recompute anything from them.

## Formations

Combatants occupy authored **slots** in a formation preset, defined in normalized space
and projected to whatever viewport you give it with a documented aspect-fit rule. Slots
carry facing, sorting, and anchor points that visual effects attach to.

Formation choice is part of encounter identity, like the scheduler.

## Presentation is skin-deep by design

A `BattleSkinPreset` holds the entire interface look and never enters a snapshot, a
replay, or a hash. Restyling cannot change an outcome. See
[guide 4](04-skins-and-presets.md).

## Replays

`ReplaySerializer` writes a versioned envelope; `ReplayMigration` upgrades older ones. A
replay plus its content manifest hash reproduces a battle exactly.

Replay format versions and stable IDs are **public compatibility contracts**. Changing a
stable ID breaks replays that reference it.

## Next

- **[Authoring content](03-authoring-content.md)**
- **[Workbench and balancing](05-workbench-and-balancing.md)**
