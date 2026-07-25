# Stage and tokens

10 types in this area.

!!! abstract "On this page"
    [BattlePresenter](#battlepresenter) &middot; [BattleStage2D](#battlestage2d) &middot; [BattleStageBloom](#battlestagebloom) &middot; [BattleStageFrame](#battlestageframe) &middot; [BeatDeriver](#beatderiver) &middot; [CombatantTokenView](#combatanttokenview) &middot; [PresentationBeat](#presentationbeat) &middot; [PresentationBeatContext](#presentationbeatcontext) &middot; [PresenterBinding](#presenterbinding) &middot; [StageFrameMode](#stageframemode)

## BattlePresenter

:material-star: **Start here**

```csharp
public sealed class BattlePresenter : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BattlePresenter.cs</small>

The pure presentation consumer. It owns a FIFO of presentation beats
derived deterministically from engine events and drives the visual
adapters, stage, and optional UI from supplied immutable values only. It
never calls `Submit`, `StepEvent`, `StepAction`,
`AdvanceTicks`, `RunUntilBoundary`, a forecast, or RNG, and it
holds no `BattleEngine`. Beat timing, speed, skipping, and pausing
affect visuals only, so presentation can never change a state hash, an
event chain, a replay, or a result.

**Properties**

`public int ActiveFloatingNumberCount`

:   &mdash;

`public Action CameraShakeCallback`

:   Optional camera-shake sink; visual only, never authoritative.

`public int CameraShakeRequestCount`

:   &mdash;

`public int ForcedInstantBeatCount`

:   &mdash;

`public bool IsIdle`

:   &mdash;

`public StableId PlayerTeamId`

:   The team treated as the player's for ally/enemy tinting. Presentation only. Left unset, the first team in the compiled layout is used, which matches how the shipped encounters order their teams.

`public int QueuedBeatCount`

:   &mdash;

`public float Speed`

:   Presentation-only playback speed multiplier (visual).

`public BattleStage2D Stage`

:   &mdash;

**Methods**

`public void AdoptSnapshot(BattleSnapshot snapshot)`

:   Adopts an authoritative snapshot for resync/skip and display.

`public void Bind(PresenterBinding presenterBinding)`

:   Binds the presenter and builds its stage. Explicit; no scan.

`public void EnqueueEvents(IReadOnlyList<BattleEvent> events)`

:   Derives and enqueues one beat per event (host step result).

`public void SetViewport(FormationViewport value)`

:   Sets the stage viewport; rebuilds the stage when bound.

`public void SkipAll()`

:   Finishes every queued beat immediately (visuals only).

`public void Teardown()`

:   Releases pooled instances and clears playback state.

`public void Tick(float presentationDeltaSeconds)`

:   Advances beats and adapters by presentation delta seconds.

---

## BattleStage2D

```csharp
public sealed class BattleStage2D : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BattleStage2D.cs</small>

A neutral 2D battle stage. It maps normalized formation space to stage
space with the documented aspect-fit rule by reusing
`ormationLayoutCompiler.Project`, spawns one
`ombatantTokenView` per compiled occupancy through the pool
adapter, and resolves slot/approach/anchor positions for beats. No
transform ever feeds back into anything authoritative.

**Properties**

`public IReadOnlyDictionary<StableId, StageTokenPlacement> Placements`

:   &mdash;

`public int TokenCount`

:   &mdash;

`public FormationViewport Viewport`

:   &mdash;

**Methods**

`public void Build()`

:   Projects the layout at `viewport` and spawns the token set. Explicit; the stage never scans the scene.

`public void Clear()`

:   Releases every token back to the pool and clears state.

`public void SetPresentation()`

:   Supplies the skin and label table used to dress spawned tokens with nameplates, bars, and status pips. Call before `uild`. Optional: without it tokens still mirror state onto their properties, which is what the headless tests assert against.

`public void Tick(float presentationDeltaSeconds)`

:   Advances token plate animation by a visual delta.

`public bool TryGetAnchorWorld()`

:   Resolves a beat anchor to stage space for a combatant.

`public bool TryGetToken(StableId combatantId, out CombatantTokenView token)`

:   Returns the spawned token for a combatant, if present.

`public void UpdateFromSnapshot(BattleSnapshot snapshot)`

:   Mirrors current snapshot state onto every token.

---

## BattleStageBloom

```csharp
public sealed class BattleStageBloom : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BattleStageBloom.cs</small>

Optional stage bloom and vignette. **Off by default and never required.**

The shipped look needs no post-processing: glow is drawn inside the
skinned-surface shader. That is why TempoForge depends on no
post-processing package at all, and why a buyer's existing volumes,
renderer features, and profiles cannot conflict with it.

This component exists only for buyers who want a softer bloom across the
whole stage and are not already running their own post stack. It is a
self-contained image effect with no package dependency.

Built-in render pipeline only. Under URP or HDRP, `OnRenderImage` is
never called, so rather than silently doing nothing this component detects
the active pipeline, logs one explanatory warning, and disables itself.
Use that pipeline's own Bloom volume override instead.

To enable: add it to the battle camera and tick `Enabled`. Nothing in
the package adds it for you.

**Properties**

`public bool IsSupportedPipeline`

:   True when this effect can run in the active pipeline.

---

## BattleStageFrame

```csharp
public sealed class BattleStageFrame : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BattleStageFrame.cs</small>

Controls where the battle stage sits on screen and how large it is.

Without this, the stage was pinned to a hardcoded 1920x1080 viewport, so on
any other resolution the formation was cropped or floated in dead space,
and a buyer had no supported way to reserve screen area for their own
interface. Every value here is presentation-only: moving or resizing the
stage cannot change a state hash, an event chain, or a result.

Attach next to a `attlePresenter`; it re-applies the viewport
whenever the screen, safe area, or any field changes.

**Properties**

`public FormationViewport AppliedViewport`

:   The viewport most recently pushed to the presenter.

**Methods**

`public void ApplyNow()`

:   Recomputes and applies the stage viewport.

`public FormationViewport Resolve(int screenWidth, int screenHeight, Rect safeAreaPixels)`

:   Computes the stage viewport for a screen. Public and parameterised so EditMode tests can verify every mode and margin without a device.

---

## BeatDeriver

```csharp
public static class BeatDeriver
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BeatDeriver.cs</small>

Pure event-to-beat derivation. Every gameplay event maps to exactly one
beat: the resolved recipe when one matches, otherwise an instant
no-visual beat. The deriver reads only the event's property set and the
supplied recipe set/catalog, performs no simulation math, and holds no
engine reference.

**Methods**

`public static PresentationBeatContext BuildContext(BattleEvent battleEvent)`

:   Extracts the beat context from an event's property set.

`public static PresentationBeat Derive()`

:   Derives the single beat for one event (never null).

---

## CombatantTokenView

```csharp
public sealed class CombatantTokenView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/CombatantTokenView.cs</small>

A neutral 2D token view for one combatant. It mirrors compiled slot data
(facing, sorting) and snapshot/event state (health, shield, status pips,
death) onto an optional `priteRenderer` and, when a skin is
supplied, onto a `kinnedTokenPlate` that draws those values.

It reads values only; it never computes or mutates anything authoritative.

**Properties**

`public ProjectedFormationPoint ApproachProjected`

:   &mdash;

`public StableId CombatantId`

:   &mdash;

`public FormationFacing Facing`

:   &mdash;

`public int Health`

:   &mdash;

`public float HealthFraction`

:   Normalized health in [0,1] for a bar; 0 when max is unset.

`public bool IsDead`

:   &mdash;

`public int MaximumHealth`

:   &mdash;

`public SkinnedTokenPlate Plate`

:   The plate drawing this token's values, or null when unskinned.

`public int ShieldAmount`

:   &mdash;

`public ProjectedFormationPoint SlotProjected`

:   &mdash;

`public StableId SortingLayerKey`

:   &mdash;

`public int SortingOrder`

:   &mdash;

`public int StatusPipCount`

:   &mdash;

**Methods**

`public void ApplySkin(CompiledBattleSkin battleSkin, float unitsPerPixel)`

:   Attaches the skinned plate that renders this token's values. Optional: a token with no skin still mirrors state onto its properties, which is what the headless tests assert against.

`public void ApplyState()`

:   Mirrors snapshot/event state onto the token and its plate.

`public void Configure()`

:   Places the token from its compiled slot projection.

`public void Pulse()`

:   Starts a visual pulse that always returns to rest. Replaces the older behaviour of assigning a scale that was never restored.

`public void SetCastProgress(float fraction, bool visible)`

:   Shows cast progress on the plate, or hides the cast bar.

`public void SetGauge(float fraction, bool visible)`

:   Shows the scheduler gauge on the plate, or hides it.

`public void SetPlateIdentity(string label, Color teamTint)`

:   Sets the display label and team tint on the plate.

`public void Tick(float deltaSeconds)`

:   Advances plate and pulse animation by a visual delta.

---

## PresentationBeat

```csharp
public sealed class PresentationBeat
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/PresentationBeat.cs</small>

One immutable presentation beat: the event context plus the resolved
recipe. A null recipe is an instant, no-visual beat (an unmapped event).
Beat timing is derived from the recipe only for visuals and never feeds
back into any authoritative hash.

**Constructors**

`public PresentationBeat()`

:   &mdash;

**Properties**

`public PresentationBeatContext Context`

:   &mdash;

`public bool IsNoVisual`

:   True when the source event mapped to no recipe.

`public int PhaseCount`

:   The number of visual phases (0 for a no-visual beat, else 3).

`public PresentationRecipeDefinition Recipe`

:   The resolved recipe, or null for a no-visual beat.

`public float TotalDurationSeconds`

:   Total clamped duration across the three phases, in seconds.

---

## PresentationBeatContext

```csharp
public readonly struct PresentationBeatContext
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/PresentationBeat.cs</small>

The non-authoritative, immutable data a beat needs, extracted entirely
from one gameplay event's property set. It carries participants and an
optional amount for floating numbers; it performs no simulation math.

**Constructors**

`public PresentationBeatContext()`

:   &mdash;

**Properties**

`public int? Amount`

:   &mdash;

`public ulong EventSequence`

:   &mdash;

`public StableId EventTypeId`

:   &mdash;

`public StableId? ReactionId`

:   &mdash;

`public StableId? SkillId`

:   &mdash;

`public StableId? SourceId`

:   &mdash;

`public StableId? StatusId`

:   &mdash;

`public StableId? TargetId`

:   &mdash;

`public long Tick`

:   &mdash;

---

## PresenterBinding

:material-star: **Start here**

```csharp
public sealed class PresenterBinding
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/PresenterBinding.cs</small>

The explicit dependency bundle a driver hands to a
`attlePresenter`. It carries compiled content, the
non-authoritative formation layout, the recipe set, the four visual
adapters, the display-string table, and an optional uGUI root. The
binding contains no engine and no authoritative mutator.

**Constructors**

`public PresenterBinding()`

:   &mdash;

**Properties**

`public IAnimationAdapter Animation`

:   &mdash;

`public IAudioAdapter Audio`

:   &mdash;

`public CompiledAuthoringCatalog Catalog`

:   &mdash;

`public DisplayStringTable Labels`

:   &mdash;

`public CompiledEncounterFormationLayout Layout`

:   &mdash;

`public PresentationLog Log`

:   Shared log-once ledger for missing-key degradation.

`public IPoolAdapter Pool`

:   &mdash;

`public PresentationRecipeSet Recipes`

:   &mdash;

`public BattleUiRoot Ui`

:   Optional uGUI root; null runs the presenter headless.

`public IVfxAdapter Vfx`

:   &mdash;

---

## StageFrameMode

```csharp
public enum StageFrameMode
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BattleStageFrame.cs</small>

How the stage rectangle is derived from the screen.

| Value | Meaning |
| --- | --- |
| `FullScreen` | Use the whole screen, inset by the configured margins. |
| `FixedAspect` | Keep a fixed aspect ratio inside the margins, letterboxing as needed. |
| `Explicit` | Use an explicit pixel rectangle, ignoring screen size. |

---

