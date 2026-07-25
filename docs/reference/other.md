# Other

15 types in this area.

!!! abstract "On this page"
    [AudioArtBinding](#audioartbinding) &middot; [CharacterArtImporter](#characterartimporter) &middot; [DisplayStringTableAsset](#displaystringtableasset) &middot; [Entry](#entry) &middot; [ForecastRequest](#forecastrequest) &middot; [ForecastResult](#forecastresult) &middot; [ForecastStopReason](#forecaststopreason) &middot; [ParticleArtBinding](#particleartbinding) &middot; [PresentationContentGenerator](#presentationcontentgenerator) &middot; [SessionEndState](#sessionendstate) &middot; [StarterContentGenerator](#startercontentgenerator) &middot; [TempoForgeDemoBootstrap](#tempoforgedemobootstrap) &middot; [TempoForgeDependencyReporter](#tempoforgedependencyreporter) &middot; [TempoForgePackageExporter](#tempoforgepackageexporter) &middot; [TokenArtBinding](#tokenartbinding)

## AudioArtBinding

```csharp
public sealed class AudioArtBinding
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Binds a recipe audio key (an sfx-* clip name) to art.

---

## CharacterArtImporter

```csharp
public static class CharacterArtImporter
```

`TempoForge.InternalTools.Editor` &middot; <small>TempoForge.InternalTools/Editor/CharacterArtImporter.cs</small>

Applies the shipped import settings to the drawn character sprites under
`Samples/Characters`, and is safe to re-run.

These are hand-authored, so unlike everything under `Samples/Art` they
are not produced by the Internal generator and carry no seed. Their import
settings therefore have to be set deliberately rather than emitted with the
asset, which is what this does.

Internal tooling: it lives outside the shipped root and is never exported.

**Methods**

`public static void ApplyCharacterImportSettings()`

:   &mdash;

`public static void WireCharacterArt()`

:   Command-line entry point: applies the import settings and then rewrites the demo's serialized art bindings so the characters actually reach the stage. Fails loudly, because a batch run that half-succeeds is worse than one that stops.

---

## DisplayStringTableAsset

```csharp
public sealed class DisplayStringTableAsset : ScriptableObject
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/DisplayStringTableAsset.cs</small>

The shipped serialized string-table asset the demo driver supplies to the
presenter (specification section 3: display text comes from an explicit
table, never from compiled snapshots, which exclude labels from every
hash). Entries map a stable id to a human display name; the asset is
authored by the Internal presentation-content generator and consumed by
`TempoForgeDemoBootstrap` through `Build`. It is
non-authoritative data and never enters any battle hash.

---

## Entry

```csharp
public sealed class Entry
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/DisplayStringTableAsset.cs</small>

One stable-id-to-display-name pair.

---

## ForecastRequest

```csharp
public sealed class ForecastRequest
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Forecast/BattleForecast.cs</small>

The three caps that bound one `BattleForecast.Run` call: how
far ahead it may look, and how much work and evidence it may collect
before stopping. The constructor accepts any values; out-of-range caps
are reported by `BattleForecast.Run` as
`ForecastStopReason.FatalInvariant` rather than thrown.

**Constructors**

`public ForecastRequest(int maximumTickDelta, int maximumActions, int maximumEvents)`

:   Creates a forecast bound. All three caps are checked at `BattleForecast.Run` time, not here.
    - `maximumTickDelta` &mdash; Ticks to look ahead of the source engine's current tick, not an absolute tick. Valid range is 0 to `SimulationLimits.ForecastTickDelta`.
    - `maximumActions` &mdash; The most action-terminal events the forecast may pass through. Valid range is 1 to `SimulationLimits.ForecastActions`.
    - `maximumEvents` &mdash; The most events the forecast may collect. Valid range is 1 to `SimulationLimits.ForecastEvents`.

**Properties**

`public int MaximumActions`

:   The cap on `ForecastResult.CompletedActions`: how many action-terminal events the forecast may pass through before it stops with `ForecastStopReason.ActionLimit`.

`public int MaximumEvents`

:   The cap on `ForecastResult.Events` before the forecast stops with `ForecastStopReason.EventLimit`.

`public int MaximumTickDelta`

:   Ticks ahead of the source engine's current tick, not an absolute tick. The forecast derives its absolute horizon by adding this to the source tick.

---

## ForecastResult

```csharp
public sealed class ForecastResult
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Forecast/BattleForecast.cs</small>

Immutable outcome of one `BattleForecast.Run` call: where the
lookahead stopped, the state and events of the throwaway clone it ran,
and the non-authoritative evidence it produced. Only
`BattleForecast` creates it, and holding it has no effect on
the engine it was forecast from.

**Properties**

`public FrozenList<AiDecisionTrace> AiDecisionTraces`

:   Non-authoritative AI decision evidence from the automatic decisions the clone took. It is outside canonical battle state and hashes.

`public int CompletedActions`

:   How many action-terminal events (action completed, interrupted, or skipped) appear in `Events`, which is the count compared against `ForecastRequest.MaximumActions`.

`public Diagnostic? Diagnostic`

:   The typed reason a cap or invariant ended the run. Set only for `ForecastStopReason.ActionLimit`, `ForecastStopReason.EventLimit`, and `ForecastStopReason.FatalInvariant`; null otherwise.

`public FrozenList<BattleEvent> Events`

:   The events the clone emitted, in emission order. They belong to the forecast alone and are not part of the source engine's event chain.

`public FrozenList<FormulaAttributionTrace> FormulaAttributionTraces`

:   Shorthand for `FormulaAttributions.Traces`.

`public FormulaAttributionTraceBatch FormulaAttributions`

:   Non-authoritative formula evidence produced by the clone, likewise outside canonical battle state and hashes.

`public long OmittedFormulaAttributionTraceCount`

:   Shorthand for `FormulaAttributions.OmittedCount`: how many formula traces were produced but dropped to stay inside the documented result-memory bound.

`public long RequestedHorizonTick`

:   The absolute tick the forecast was asked to reach: the source tick plus `ForecastRequest.MaximumTickDelta`. It records the request, not the outcome; only `ForecastStopReason.HorizonReached` means it was reached. When the request itself was rejected this is the source tick.

`public BattleSnapshot Snapshot`

:   State of the throwaway clone where the lookahead stopped. The source engine's own snapshot, hashes, RNG, and history are unchanged, so this is a prediction and never the authoritative battle state.

`public ForecastStopReason StopReason`

:   Why the lookahead stopped, and the first thing to branch on. Only `ForecastStopReason.HorizonReached` means the whole requested window was covered, and only `ForecastStopReason.Terminal` means the battle itself ended inside it; every other value leaves the rest of the window unknown rather than empty.

---

## ForecastStopReason

```csharp
public enum ForecastStopReason : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Forecast/BattleForecast.cs</small>

Why one `BattleForecast.Run` call stopped. Caps are
evaluated only at complete emitted boundaries, so a forecast never stops
part-way through an event.

| Value | Meaning |
| --- | --- |
| `HorizonReached` | The forecast reached `ForecastResult.RequestedHorizonTick` with no earlier stop. |
| `UnknownHumanDecision` | The next decision belongs to a human-controlled actor, so the forecast stopped instead of inventing a command. |
| `Terminal` | A terminal battle result was reached, or the source was already terminal. |
| `NoScheduledWork` | The forecast ran out of scheduled work before the horizon without reaching a terminal result. |
| `ActionLimit` | `ForecastRequest.MaximumActions` was reached. |
| `EventLimit` | `ForecastRequest.MaximumEvents` was reached. |
| `FatalInvariant` | The request was null or out of range, the horizon would overflow, or a step failed. |

---

## ParticleArtBinding

```csharp
public sealed class ParticleArtBinding
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Binds a recipe VFX key (a particle-* sprite name) to art.

---

## PresentationContentGenerator

```csharp
public static class PresentationContentGenerator
```

`TempoForge.InternalTools.Editor` &middot; <small>TempoForge.InternalTools/Editor/PresentationContentGenerator.cs</small>

Non-shipped internal generator for the B6 presentation content: the
starter recipe library (In/Impact/Out beats wired to the generated art
adapter keys), the explicit recipe set, the shipped display string
table, and the runtime demo scene. It is invoked head-lessly via
`-executeMethod TempoForge.InternalTools.Editor.PresentationContentGenerator.GeneratePresentationContent`
and always exits the editor explicitly so batch runs never hold the
project lock.

**Fields**

`public long Duration`

:   &mdash;

`public bool Shake`

:   &mdash;

**Methods**

`public static void GeneratePresentationContent()`

:   &mdash;

---

## SessionEndState

```csharp
public enum SessionEndState
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Typed end-of-session states surfaced by the driver.

| Value | Meaning |
| --- | --- |
| `None` | No battle, or the battle is still running. |
| `TerminalResult` | The engine reported a terminal result (victory, defeat, draw, concession, or the stalled result). |
| `NoScheduledWork` | The engine reported no scheduled work remains. |
| `FatalInvariant` | The engine reported a fatal invariant; the driver stops pumping instead of entering an exception loop. |

---

## StarterContentGenerator

```csharp
public static class StarterContentGenerator
```

`TempoForge.InternalTools.Editor` &middot; <small>TempoForge.InternalTools/Editor/StarterContentGenerator.cs</small>

Non-shipped internal generator that authors the complete B6 starter
content library as B4 `.asset` definitions under
`Assets/TempoForge/Samples/StarterContent` and compiles the result
through the real B4 authoring pipeline. It is invoked head-lessly via
`-executeMethod TempoForge.InternalTools.Editor.StarterContentGenerator.GenerateStarterContent`.
The generator writes shipped content but itself lives outside the shipped
product root, so it uses `UnityEditor` freely.

**Fields**

`public int Diagnostics`

:   &mdash;

`public int Errors`

:   &mdash;

`public bool Success`

:   &mdash;

**Methods**

`public static void GenerateStarterContent()`

:   &mdash;

---

## TempoForgeDemoBootstrap

```csharp
public sealed class TempoForgeDemoBootstrap : MonoBehaviour
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

The runtime demo driver (specification section 9). It compiles the
starter catalog with built-in registries explicitly at load, offers the
scenario picker over the AUTHORED encounter variants (scheduler and
formation choices are inputs to scenario identity, so picking one of the
eight already-compiled encounters IS the scheduler/formation choice; no
preset is ever swapped on a live start), exposes a user-visible seed
field, owns the `BattleEngine`, and runs the continuous
driver loop from ExecutionSteppingV1 section 7: accumulated presentation
time is converted into an integer requested tick count and handed to
`AdvanceTicks`, whose returned events feed the presenter and whose
snapshots are adopted verbatim.

The DRIVER is the single audited engine owner in the Presentation
assembly (specification section 3 rule 1: "The demo's driver object owns
the engine; the presenter only receives values"); the presenter-purity
audit carves out exactly this demo namespace and nothing else. Pause,
speed, and skip affect presentation only: they scale or halt the
presentation-time accumulator and the visual beat clock, never a
simulation value, so the same (scenario, scheduler, formation, seed)
tuple always reproduces the same hashes. Human-decision scenarios must
author the PauseOnInput scheduler policy so presentation speed cannot
shift submission ticks; the shipped starter scenarios are all-Automatic.
`FatalInvariant`, `NoScheduledWork`, and the stalled terminal
result surface as typed end-of-session states without an exception loop.

---

## TempoForgeDependencyReporter

```csharp
public static class TempoForgeDependencyReporter
```

`TempoForge.InternalTools.Editor` &middot; <small>TempoForge.InternalTools/Editor/TempoForgeDependencyReporter.cs</small>

Produces a deterministic, non-shipped dependency report from Unity's
AssetDatabase. The report is subsequently reviewed and hash-attested.

**Fields**

`public int approvedPackageDependencyCount`

:   &mdash;

`public string[] approvedPackageIds`

:   &mdash;

`public int builtInDependencyCount`

:   &mdash;

`public string classification`

:   &mdash;

`public DependencyEntry[] dependencies`

:   &mdash;

`public int dependencyCount`

:   &mdash;

`public string guid`

:   &mdash;

`public int internalDependencyCount`

:   &mdash;

`public string packageId`

:   &mdash;

`public string path`

:   &mdash;

`public string product`

:   &mdash;

`public string productRoot`

:   &mdash;

`public string[] requestedBy`

:   &mdash;

`public int schemaVersion`

:   &mdash;

`public string shippedAggregate`

:   &mdash;

`public long shippedBytes`

:   &mdash;

`public int shippedFileCount`

:   &mdash;

`public string unityVersion`

:   &mdash;

`public int unknownDependencyCount`

:   &mdash;

**Methods**

`public static void Run()`

:   &mdash;

---

## TempoForgePackageExporter

```csharp
public static class TempoForgePackageExporter
```

`TempoForge.InternalTools.Editor` &middot; <small>TempoForge.InternalTools/Editor/TempoForgePackageExporter.cs</small>

Batch-mode entry point. It intentionally accepts no asset-root argument:
the only exportable root is the constant Assets/TempoForge.

**Methods**

`public static void Run()`

:   &mdash;

---

## TokenArtBinding

```csharp
public sealed class TokenArtBinding
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Binds a starter combatant definition id to its generated
token sprite (the token-* art keys from the art manifest).

---

