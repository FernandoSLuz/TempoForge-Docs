# Other

10 types in this area.

!!! abstract "On this page"
    [AudioArtBinding](#audioartbinding) &middot; [DisplayStringTableAsset](#displaystringtableasset) &middot; [Entry](#entry) &middot; [ForecastRequest](#forecastrequest) &middot; [ForecastResult](#forecastresult) &middot; [ForecastStopReason](#forecaststopreason) &middot; [ParticleArtBinding](#particleartbinding) &middot; [SessionEndState](#sessionendstate) &middot; [TempoForgeDemoBootstrap](#tempoforgedemobootstrap) &middot; [TokenArtBinding](#tokenartbinding)

## AudioArtBinding

```csharp
public sealed class AudioArtBinding
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Binds a recipe audio key (an sfx-* clip name) to art.

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
`empoForgeDemoBootstrap` through `uild`. It is
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

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ForecastRequest(int maximumTickDelta, int maximumActions, int maximumEvents)`

:   &mdash;

**Properties**

`public int MaximumActions`

:   &mdash;

`public int MaximumEvents`

:   &mdash;

`public int MaximumTickDelta`

:   &mdash;

---

## ForecastResult

```csharp
public sealed class ForecastResult
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Forecast/BattleForecast.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AiDecisionTrace> AiDecisionTraces`

:   &mdash;

`public int CompletedActions`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public FrozenList<BattleEvent> Events`

:   &mdash;

`public FrozenList<FormulaAttributionTrace> FormulaAttributionTraces`

:   &mdash;

`public FormulaAttributionTraceBatch FormulaAttributions`

:   &mdash;

`public long OmittedFormulaAttributionTraceCount`

:   &mdash;

`public long RequestedHorizonTick`

:   &mdash;

`public BattleSnapshot Snapshot`

:   &mdash;

`public ForecastStopReason StopReason`

:   &mdash;

---

## ForecastStopReason

```csharp
public enum ForecastStopReason : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Forecast/BattleForecast.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `HorizonReached` | &mdash; |
| `UnknownHumanDecision` | &mdash; |
| `Terminal` | &mdash; |
| `NoScheduledWork` | &mdash; |
| `ActionLimit` | &mdash; |
| `EventLimit` | &mdash; |
| `FatalInvariant` | &mdash; |

---

## ParticleArtBinding

```csharp
public sealed class ParticleArtBinding
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Binds a recipe VFX key (a particle-* sprite name) to art.

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
field, owns the `attleEngine`, and runs the continuous
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

## TokenArtBinding

```csharp
public sealed class TokenArtBinding
```

`TempoForge.Presentation.Demo` &middot; <small>TempoForge/Samples/RuntimeDemo/TempoForgeDemoBootstrap.cs</small>

Binds a starter combatant definition id to its generated
token sprite (the token-* art keys from the art manifest).

---

