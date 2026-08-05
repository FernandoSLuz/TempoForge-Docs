# Architecture

TurnGauge splits a battle into three roles separated by one hard boundary. After this page
you will know which role owns the engine, which assembly each role lives in, why nothing on
the visual side may touch the engine, and where your authored assets enter.

---

## The three roles

```
   THE DRIVER           owns the BattleEngine
        |               creates it, advances it, submits commands, computes forecasts
        |               BattleRuntimeController, or a script of your own
        | events + snapshots
        v
   BattlePresenter      receives immutable values, plays beats, drives the stage
        |               holds no engine and cannot obtain one
        v
   BattleUiRoot         offers the legal choices, raises the player's intent
                        submits nothing
```

| Role | Who writes it | What it may call |
| --- | --- | --- |
| Driver | shipped (`BattleRuntimeController`) or you | `BattleEngine.Create`, `AdvanceTicks`, `Submit`, `GetSnapshot`, forecasts |
| `BattlePresenter` | shipped | `Bind`, `EnqueueEvents`, `AdoptSnapshot`, `Tick`, `SkipAll` |
| `BattleUiRoot` | shipped | nothing on the engine; it raises `CommandChosen` |

The driver is the single engine owner, and there is exactly one per battle. Drop a
`BattleRuntimeController` in the scene and it is the driver; write your own `MonoBehaviour`
and that is the driver instead. Either way `BattleUiRoot` raises a plain C# event carrying
what the player picked, and the driver turns that into a `BattleCommand` and calls `Submit`.
The `PresenterBinding` handed to the presenter carries compiled content, a formation layout,
a recipe set, four adapters and a label table - and deliberately no engine.

### How the boundary is enforced

Assembly references only point one way, so a skin, a prefab or a frame time cannot be
reached from inside the engine.

| Assembly | Sees `UnityEngine` | References |
| --- | --- | --- |
| `TurnGauge.Simulation` | no (`noEngineReferences: true`) | nothing |
| `TurnGauge.Analysis` | no (`noEngineReferences: true`) | Simulation |
| `TurnGauge.Authoring` | yes | Simulation |
| `TurnGauge.Presentation` | yes | Simulation, Authoring, `UnityEngine.UI` |
| `TurnGauge.Runtime` | yes | Simulation, Authoring, Presentation, `UnityEngine.UI` |

On top of that, an edit-mode test walks the IL of every method in
`TurnGauge.Presentation` and fails if any type holds a `BattleEngine` or `BattleForecast`
field, or if any call site reaches `Submit`, `StepEvent`, `StepAction`, `AdvanceTicks` or
`RunUntilBoundary`. The shipped demo's scripts join that assembly on purpose so the audit
covers them too; two demo driver types are exempted, and a companion test freezes that list.

### `TurnGauge.Runtime` is the driver assembly

`TurnGauge.Runtime` is the one shipped assembly that is *allowed* to own an engine, and
`BattleRuntimeController` is what lives there. It is the only assembly that references
Presentation, which is what lets it sit above the boundary and hold both sides: it compiles
the catalog, creates the engine, pumps ticks, and hands the presenter events and snapshots.
The presenter audit does not cover it, and does not need to - it is the driver, not the
visual side.

| It may | It may not |
| --- | --- |
| Own one `BattleEngine`, create it, advance it, restore it | Own two, or hand the engine to the presenter |
| Compile the assigned catalog and look up one explicit encounter | Search the project for content, or pick an encounter for you |
| Convert presentation time into an integer tick count and call `AdvanceTicks` | Let a frame time, a float or an animation length reach the engine as anything but that integer |
| Translate a `BattleUiCommandChoice` into a `BattleCommand` and submit it | Guess targets outside the compiled target contract, or turn a rejected command into a different one |
| Pause for an authored human decision | Change an authored `Automatic` member into a `Human` one |
| Capture checkpoints and replay bytes, and refuse a restore whose hashes disagree | Regenerate or substitute content after an incompatible save |
| Fail closed, publish a typed failure, and log it | Continue silently on a failure, or reroll a restore |

Because it references Presentation and not the other way round, nothing on the visual side
can reach the controller's engine either. And because the whole thing is one `MonoBehaviour`
in a scene, none of it is required: `BattleEngine`, the replay APIs and the presentation
adapters all stay public, and a driver you write yourself is a first-class option. See
[Run a battle from your own code](../tutorials/run-a-battle-from-code.md).

## Why the boundary matters

Because it is what makes a replay worth keeping. If the visual side could reach the engine
- even to read RNG - then frame timing, animation length or a dropped frame could change an
outcome. With the boundary intact:

- Pause, speed and skip scale the visual clock only. `BattlePresenter.Speed` and `SkipAll`
  finish queued beats; neither advances a tick.
- Only the integer tick count you hand to `AdvanceTicks` is authoritative. The accumulated
  real time your driver converts into that count is never recorded and never replayed.
- The same content, encounter, scheduler and seed produce the same events and the same
  hashes on any platform.

### Values cross the boundary, not references

Nothing on the visual side computes a number a battle depends on.

| What the interface shows | Who produces it |
| --- | --- |
| The pending actor's legal skills and target shapes | `DecisionShapeCompiler.Compile(snapshot, catalog)`, called by the presenter |
| Tooltip damage, hit and status chances | your driver, passed in as a `TooltipData` value |
| One visual cue per event | `BeatDeriver`, resolved against your recipe set |

`DecisionShapeCompiler` reads cooldowns, costs and restriction tags out of the snapshot and
the compiled target contract. It does not re-resolve targets exactly; the engine does that
when the command arrives.

!!! warning "Snapshot values are not display strings"
    Amounts are `Fixed64` and chances are `Chance64`, and their `ToString()` returns the raw
    scaled integer because that string feeds canonical encoding. Format player-facing
    numbers with `BattleNumberFormat`. See [Determinism](determinism.md).

## From assets to a running battle

```
Definition assets            stats, resources, effects, statuses, targets, skills,
      |                      reactions, AI policies, combatants, formations,
      v                      teams, battle rules, schedulers, encounters
BattleContentCatalog         the one root you hand to the compiler
      |
      v
BattleContentCompiler        Compile() maps and freezes; Validate() only reports
      |
      v
CompiledAuthoringCatalog     immutable; carries ContentManifestHash,
      |                      CompiledSnapshotHash and the compiled encounters
      v
BattleEngine.Create(content, startRequest, seed, schedulers, mechanics)
```

Every layer is a ScriptableObject created from **Assets > Create > TurnGauge**. The catalog
is the sole root of a closed graph: compilation never searches the project, Resources,
Addressables, folders or loaded assemblies, so content the catalog does not reference does
not exist as far as the engine is concerned.

Compilation is where authoring mistakes surface. Each `AuthoringDiagnostic` carries a
`Source` naming the owning asset, the field, and where relevant the list element and its
authored ordinal, alongside a `HumanDetail` string. `Validate` returns the same diagnostics
without producing content. The compiled catalog carries a `ContentManifestHash`, and every
`BattleSnapshot` carries it too, so a replay recorded against different content can be
detected rather than silently mis-played.

!!! note "Slot identity is authoritative; slot position is not"
    A combatant's `FormationSlotId`, `FormationRowId` and `FormationSideId` are part of the
    start request the engine consumes. The screen coordinates the presenter draws them at
    are presentation data. See [Place combatants with the Formation Editor](../how-to/place-formations.md).

## What presentation may never do

A `BattleSkinPreset` holds the entire interface look - palette, surfaces, bars, indicators,
motion timings and region positions - and never enters a snapshot, a replay, a state hash or
a compiled catalog. Restyling cannot change an outcome, and that is structural rather than
promised: `TurnGauge.Simulation` cannot reference `TurnGauge.Presentation`.

| Presentation concern | Where it lives | Reaches a hash |
| --- | --- | --- |
| Palette, surfaces, bars, region layout | `BattleSkinPreset` | no |
| Speed, pause, skip | `BattlePresenter` | no |
| Animation, VFX, audio, pooling | your four adapters | no |
| Names and labels shown to a player | `DisplayStringTable` | no |
| Camera shake, floating numbers | `BattlePresenter` | no |

The only thing that ever crosses back into the engine is a `BattleCommand`, and only the
driver submits it - whether that driver is `BattleRuntimeController` or a script of yours.

## Next

- **[The engine loop](engine-loop.md)** - what one `AdvanceTicks` call returns.
- **[Determinism](determinism.md)** - and which of your own choices can break it.
- **[Run a battle from your own code](../tutorials/run-a-battle-from-code.md)** - a driver of
  your own, written out in full.
