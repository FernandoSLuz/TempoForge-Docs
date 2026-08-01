# Other

18 types in this area.

!!! abstract "On this page"
    [AudioArtBinding](#audioartbinding) &middot; [BattleUiCommandTranslationResult](#battleuicommandtranslationresult) &middot; [BattleUiCommandTranslator](#battleuicommandtranslator) &middot; [CharacterArtImporter](#characterartimporter) &middot; [DisplayStringTableAsset](#displaystringtableasset) &middot; [Entry](#entry) &middot; [ForecastRequest](#forecastrequest) &middot; [ForecastResult](#forecastresult) &middot; [ForecastStopReason](#forecaststopreason) &middot; [ParticleArtBinding](#particleartbinding) &middot; [PresentationContentGenerator](#presentationcontentgenerator) &middot; [SessionEndState](#sessionendstate) &middot; [StarterContentGenerator](#startercontentgenerator) &middot; [TargetCandidateQuery](#targetcandidatequery) &middot; [TempoForgeDemoBootstrap](#tempoforgedemobootstrap) &middot; [TempoForgeDependencyReporter](#tempoforgedependencyreporter) &middot; [TempoForgePackageExporter](#tempoforgepackageexporter) &middot; [TokenArtBinding](#tokenartbinding)

## AudioArtBinding

```csharp
public sealed class AudioArtBinding
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Binds a recipe audio key (an sfx-* clip name) to art.

---

## BattleUiCommandTranslationResult

```csharp
public sealed class BattleUiCommandTranslationResult
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Runtime/BattleUiCommandTranslator.cs</small>

Typed result of translating a presentation choice into a command.

**Properties**

`public BattleCommand Command`

:   The translated command on success; null on failure.

`public string Message`

:   Actionable failure detail, or an empty string on success.

`public bool Succeeded`

:   True when a complete command was produced.

---

## BattleUiCommandTranslator

```csharp
public static class BattleUiCommandTranslator
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Runtime/BattleUiCommandTranslator.cs</small>

Turns a UI choice into the exact command shape the engine expects. When
the caller supplies no explicit targets for a resolver that requires
them, this asks that skill's registered `ITargetResolver` who is
eligible and takes the lowest stable IDs from the answer, so a project
whose resolver narrows further than its declared contract gets an
auto-pick its own resolver accepts. Explicit target lists are preserved
verbatim, checked against the same resolver, and remain subject to
authoritative engine validation.

**Methods**

`public static BattleUiCommandTranslationResult Translate()`

:   Translates a presentation choice against the current authoritative snapshot and compiled command shapes. It returns a failed result for null context, a stale actor, an unavailable skill, or an unsatisfied target contract; normal validation failures do not throw.
    - `choice` &mdash; Player intent to translate.
    - `snapshot` &mdash; Current authoritative state.
    - `catalog` &mdash; Compiled content used by the battle.
    - **Returns** &mdash; A complete command on success or actionable failure detail.

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

**Fields**

`public const float CharacterPixelsPerUnit`

:   Pixels per unit for the drawn characters. The generated role tokens are 128 px at 100 PPU, so they stand 1.28 world units tall. These drawings are around 900-984 px, so 750 PPU puts them at roughly the same height on the stage while preserving the real height differences between them - the Brawler stays shorter than the Knight rather than every character being normalised to one size.

**Methods**

`public static void ApplyCharacterImportSettings()`

:   &mdash;

`public static void WireCharacterArt()`

:   Command-line entry point: applies the import settings and then rewrites the demo's serialized art bindings so the characters actually reach the stage. Fails loudly, because a batch run that half-succeeds is worse than one that stops.

---

## DisplayStringTableAsset

```csharp
public sealed class DisplayStringTableAsset : DisplayStringTableProvider
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/DisplayStringTableAsset.cs</small>

The shipped serialized string-table asset the demo driver supplies to the
presenter (specification section 3: display text comes from an explicit
table, never from compiled snapshots, which exclude labels from every
hash). Entries map a stable id to a human display name; the asset is
authored by the Internal presentation-content generator and consumed by
`TempoForgeDemoBootstrap` through `Build`. It is
non-authoritative data and never enters any battle hash.

**Properties**

`public IReadOnlyList<Entry> Entries`

:   The authored entries in serialized order.

**Methods**

`public override DisplayStringTable Build()`

:   Builds the runtime `DisplayStringTable`. Invalid ids and null labels are skipped defensively; lookups for skipped ids fall back to the raw id text inside the table itself.

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

`public PresentationVfxAnchorKind AnchorKind`

:   &mdash;

`public string Animation`

:   &mdash;

`public string Audio`

:   &mdash;

`public long Duration`

:   &mdash;

`public bool Shake`

:   &mdash;

`public FloatingNumberStyle Style`

:   &mdash;

`public string Vfx`

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

## TargetCandidateQuery

```csharp
public static class TargetCandidateQuery
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Runtime/TargetCandidateQuery.cs</small>

Asks a skill's registered target resolver who it may legally hit right
now, and whether one particular pick would be accepted.

It is the single place the interface and the command translator both go
for that answer, which is what keeps the two from disagreeing: a project
that registers a resolver narrower than its declared contract - front row
only, lowest health only, line of fire - narrows the picker and the
auto-pick together, because both ask the same object the engine will ask.

Everything here is a read. The snapshot is projected into the read-only
view the resolver contract already takes, no command is submitted, and no
RNG is drawn, so consulting it can never change a battle.

**Methods**

`public static FrozenList<StableId> GetCandidates()`

:   Lists every combatant the skill's resolver currently considers a legal pick for `actorId`.
    - `snapshot` &mdash; Current authoritative state; read, never advanced.
    - `catalog` &mdash; Compiled content and the registry the resolver is looked up in.
    - `actorId` &mdash; The combatant that would use the skill.
    - `skillId` &mdash; The skill whose resolver is consulted.
    - **Returns** &mdash; Candidate ids, ascending and without duplicates. Empty for a missing argument, an unknown skill, an unregistered resolver, or a resolver that threw; an empty result therefore means "offer no picks" rather than "every combatant is legal".

`public static bool ValidateRequest()`

:   Puts a proposed pick through the same resolver check the engine runs before it accepts a command.
    - `snapshot` &mdash; Current authoritative state; read, never advanced.
    - `catalog` &mdash; Compiled content and the registry the resolver is looked up in.
    - `actorId` &mdash; The combatant that would use the skill.
    - `skillId` &mdash; The skill whose resolver is consulted.
    - `requested` &mdash; Exactly the ids the command would carry, in pick order. An empty list asks for automatic selection.
    - `message` &mdash; Why the pick would be refused, or an empty string when it would be accepted. It is developer-facing detail, not player-facing text.
    - **Returns** &mdash; True when the resolver accepts the request. A resolver this method cannot reach at all also returns true: the engine remains the authority, and refusing a command the UI merely failed to preview would be worse than letting the engine answer.

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

**Properties**

`public int AtbCompileErrorCount`

:   Error diagnostic count from the ATB load-time compile.

`public bool AtbCompileSucceeded`

:   True when the assigned ATB showcase catalog compiled.

`public int CompileErrorCount`

:   Error diagnostic count from the primary load-time compile.

`public bool CompileSucceeded`

:   True when the primary catalog compiled with zero errors.

`public IReadOnlyList<StableId> EncounterIds`

:   The authored encounter variants offered by the picker.

`public SessionEndState EndState`

:   The typed end-of-session state of the current battle.

`public bool IsBattleRunning`

:   True when a battle exists and has not reached an end state.

`public bool Paused`

:   Presentation-only pause; halts presentation-time accumulation (and therefore tick pumping) without touching state.

`public StableId? SelectedEncounterId`

:   The picker's currently selected encounter variant.

`public float SpeedMultiplier`

:   The active presentation speed step.

`public StableId? TerminalResultId`

:   The terminal result id when `EndState` is `SessionEndState.TerminalResult` (battle.stalled marks a stall surfaced as a clean terminal result).

**Fields**

`public const float BaseTicksPerSecond`

:   Simulation ticks represented by one presentation second at 1x speed.

`public static readonly float[] SpeedSteps`

:   The specification section 9 presentation speed steps.

**Methods**

`public void CompileCatalog()`

:   Explicitly compiles both starter catalogs with built-in registries (specification section 9: compile at load through the same public entry point the Workbench and tests use). The picker then spans the primary catalog's Action Order variants plus the dedicated ATB catalog's variant; each variant remembers its owning compiled catalog because the engine binds scheduler-adjustment support per catalog at creation (specification section 6).

`public void CycleSpeed()`

:   Cycles the presentation speed through 0.5x/1x/2x/4x.

`public void SelectNextEncounter()`

:   Moves the scenario picker forward through the authored variants.

`public void SelectPreviousEncounter()`

:   Moves the scenario picker backward through the authored variants.

`public void SkipAll()`

:   Finishes every queued presentation beat now (visuals only).

`public bool StartBattle(StableId encounterId, uint seedValue)`

:   Creates the engine for one authored encounter variant from the variant's OWNING compiled catalog (primary or ATB) and binds a fresh presenter to its compiled formation layout.

`public bool StartSelectedBattle()`

:   Starts (or restarts) the picker-selected encounter variant with the current seed value. The variant is an authored, already-compiled start; nothing is re-authored or swapped at runtime.

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

