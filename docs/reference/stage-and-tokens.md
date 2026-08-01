# Stage and tokens

11 types in this area.

!!! abstract "On this page"
    [BattlePresenter](#battlepresenter) &middot; [BattleStage2D](#battlestage2d) &middot; [BattleStageBackdrop](#battlestagebackdrop) &middot; [BattleStageBloom](#battlestagebloom) &middot; [BattleStageFrame](#battlestageframe) &middot; [BeatDeriver](#beatderiver) &middot; [CombatantTokenView](#combatanttokenview) &middot; [PresentationBeat](#presentationbeat) &middot; [PresentationBeatContext](#presentationbeatcontext) &middot; [PresenterBinding](#presenterbinding) &middot; [StageFrameMode](#stageframemode)

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

:   Floating numbers currently on the stage, including ones still playing out their rise. Each returns to the pool as it finishes, and the oldest is retired early rather than exceeding `MaximumFloatingNumbers`.

`public Action CameraShakeCallback`

:   Optional camera-shake sink; visual only, never authoritative.

`public int CameraShakeRequestCount`

:   Camera shakes requested since `Bind`. Counted whether or not `CameraShakeCallback` is set.

`public int ForcedInstantBeatCount`

:   Beats that were finished instantly because the queue had already reached `MaximumQueuedBeats`. A non-zero count means visuals were compressed to keep up, never that the battle changed. Cleared by `Bind`.

`public bool IsIdle`

:   True when no beat is playing and none are queued, so the visuals have caught up with every event handed in so far.

`public IList<IPerformBeatModule> PerformModules`

:   The perform modules driving the moment a skill lands, run in list order as each phase begins. This is the seam the shipped effects are built on and the one a project extends: add a module, drop one, reorder them, or replace the set entirely. The presenter contains anything a module throws, so a project's own module cannot stop a battle from playing. The list starts empty and, unless the built-in perform feel is switched off in the inspector, the shipped set is installed on the first tick. Registering your own modules before then keeps them, and their order, exactly as you built them: only a kind that is missing is added.

`public StableId PlayerTeamId`

:   The team treated as the player's for ally/enemy tinting. Presentation only. Left unset, the first team in the compiled layout is used, which matches how the shipped encounters order their teams.

`public int QueuedBeatCount`

:   Beats waiting behind the one currently playing. It never passes `MaximumQueuedBeats`, because reaching that cap completes the oldest beat instantly to make room, so a count that sits near the cap means the visuals are trailing the engine rather than that events are being lost.

`public float Speed`

:   Presentation-only playback speed multiplier (visual). A negative value clamps to zero, which freezes the visuals rather than reversing them.

`public BattleStage2D Stage`

:   The stage this presenter created and owns, or null until `Bind` has run.

`public Rect StageWorldRect`

:   Where the stage lands in world space, in units, for the current viewport and scale. Tokens are placed in world space directly rather than under this transform, so a camera framed on this rectangle sees the whole formation wherever the presenter object itself sits. The setup wizard frames the scene camera from this value, so the framing is authored here rather than copied by hand into a scene.

`public float UnitsPerPixel`

:   World units per stage pixel, falling back to `DefaultUnitsPerPixel` when the serialized value is zero or negative, which is the coercion `BattleStage2D.Build` applies anyway.

`public FormationViewport Viewport`

:   The pixel rectangle the formation is projected into, read straight from the serialized stage fields. `SetViewport` writes those fields, so a `BattleStageFrame` that reframes the stage at runtime shows up in the inspector instead of hiding behind it.

**Fields**

`public const float DefaultUnitsPerPixel`

:   World units one stage pixel is worth when the serialized scale is left at zero or below. It repeats `BattleStage2D.Build`'s own fallback so a presenter nobody has touched frames exactly as before.

`public const int MaximumFloatingNumbers`

:   Section 10 cap: floating numbers concurrently visible.

`public const int MaximumQueuedBeats`

:   Section 10 cap: queued beats per presenter.

**Methods**

`public void AdoptSnapshot(BattleSnapshot snapshot)`

:   Adopts an authoritative snapshot for resync/skip and display.
    - `snapshot` &mdash; State to mirror onto the stage and HUD. It is read, never advanced or mutated; a null snapshot is accepted and updates nothing.

`public void Bind(PresenterBinding presenterBinding)`

:   Binds the presenter and builds its stage. Explicit; no scan.
    - `presenterBinding` &mdash; Catalog, formation layout, recipes, adapters, labels, and optional UI the presenter draws from. Required, and retained for the lifetime of the binding. Binding again clears the beat queue and the counters and rebuilds the stage from the new layout.

`public void EnqueueEvents(IReadOnlyList<BattleEvent> events)`

:   Derives and enqueues one beat per event (host step result).
    - `events` &mdash; Events from one engine step, in the order the engine produced them. A null list, and any null entry, is skipped. Once the queue reaches `MaximumQueuedBeats` the oldest beat is completed instantly to make room instead of being dropped, which increments `ForcedInstantBeatCount`.

`public int InstallBuiltInPerformModules()`

:   Registers the shipped perform moment in one call: the skill title announcement, the focus pull, the body shake, and - when a camera is supplied - the camera shake and push-in, plus the bloom, vignette, and backdrop blur for whichever of those optional components the camera carries. This is the wiring the demo scene does by hand, offered as one line so a battle assembled from the shipped facade does not read flatter than the demo a buyer watched before purchasing. It adds only modules of a kind that is not registered yet, so calling it twice, or calling it after adding a module of your own, cannot double an effect. The first tick calls it for you with the serialized feel, camera, and no card, so calling it explicitly is only needed to pass a different preset, a different camera, or a card of your own. `PerformModules` stays open afterwards: drop one, reorder them, or add your own alongside.
    - `feel` &mdash; How hard the moment hits. Null uses the shipped defaults rather than zeroes, so the effects are visible without an asset being authored.
    - `camera` &mdash; The camera the shake and the push-in drive. Null registers the modules that need no camera and skips the rest.
    - `titleView` &mdash; The card the skill name is announced on. Null builds one over the bound interface, and skips the announcement when there is no interface to build it on.
    - **Returns** &mdash; How many modules were added.

`public void ResetPerformModules()`

:   Puts every module's effect back. Called on teardown and whenever playback is skipped, because a module that has dimmed the stage or moved the camera would otherwise leave it that way.

`public void SetViewport(FormationViewport value)`

:   Sets the stage viewport; rebuilds the stage when bound.
    - `value` &mdash; Pixel rectangle the formation is projected into. Written to the serialized stage fields even when the presenter is not bound yet, so the next `Bind` uses it and the inspector shows it.

`public void SkipAll()`

:   Finishes every queued beat immediately (visuals only).

`public void Teardown()`

:   Releases pooled instances and clears playback state.

`public void Tick(float presentationDeltaSeconds)`

:   Advances beats and adapters by presentation delta seconds.
    - `presentationDeltaSeconds` &mdash; Elapsed seconds, unscaled: `Speed` is applied on top, so a host passes its frame delta straight in. Zero or less does nothing, which is how a host implements pause.

---

## BattleStage2D

```csharp
public sealed class BattleStage2D : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BattleStage2D.cs</small>

A neutral 2D battle stage. It maps normalized formation space to stage
space with the documented aspect-fit rule by reusing
`FormationLayoutCompiler.Project`, spawns one
`CombatantTokenView` per compiled occupancy through the pool
adapter, and resolves slot/approach/anchor positions for beats. No
transform ever feeds back into anything authoritative.

**Properties**

`public Camera PickCamera`

:   The camera clicks are unprojected through. Left unset, the stage uses `Camera.main`, which is what the shipped setups have.

`public IReadOnlyDictionary<StableId, StageTokenPlacement> Placements`

:   Every token the last `Build` produced, keyed by combatant. Each entry carries the projected slot and approach points along with the slot's facing and sorting data, so a caller can read where a combatant stands without going through its transform.

`public int TokenCount`

:   How many tokens are currently spawned. It can be lower than the layout's occupancy count without that being an error: a team whose formation fails to project is skipped with a warning, while an occupancy whose slot is missing from the preset or whose pool returns nothing is skipped silently.

`public float TokenPickRadiusPixels`

:   How near a click has to land, in formation pixels, before it counts as hitting a combatant. It is measured against the token's slot point, so it is a radius around where the combatant stands rather than the bounds of whatever art is on top of it.

`public bool TokenPickingEnabled`

:   Whether the stage watches for clicks on its tokens at all. Turn it off for a project that reads its own input; with no listener attached the watch already costs nothing.

`public IReadOnlyDictionary<StableId, CombatantTokenView> Tokens`

:   Every spawned token by combatant id, for a caller that has to walk the whole field rather than look one combatant up. Read only, and the instances belong to the pool: reposition or tint one and you must put it back, because the stage will not recompute it.

`public FormationViewport Viewport`

:   The viewport the current layout was projected against, as handed to `Build`. Nothing re-projects on its own, so a change of screen size means building again.

**Fields**

`public const string TokenPoolKey`

:   Pool key used for spawned combatant tokens when no per-combatant prototype has been registered. One prototype under this key serves every combatant.

**Events**

`public event Action<StableId> TokenClicked`

:   Raised when the player clicks a combatant on the stage. It is a report, not a command: the stage never decides what a click means, which is what lets the same click pick a target, open an inspector, or do nothing at all depending on who is listening.

**Methods**

`public void Build()`

:   Projects the layout at `viewport` and spawns the token set. Explicit; the stage never scans the scene.
    - `layout` &mdash; The layout value used by this operation.
    - `log` &mdash; The log value used by this operation.
    - `pool` &mdash; The pool value used by this operation.
    - `unitsPerPixel` &mdash; The units per pixel value used by this operation.
    - `viewport` &mdash; The viewport value used by this operation.

`public void Clear()`

:   Releases every token back to the pool and clears state.

`public void SetPresentation()`

:   Supplies the skin and label table used to dress spawned tokens with nameplates, bars, and status pips. Call before `Build`. Optional: without it tokens still mirror state onto their properties, which is what the headless tests assert against.
    - `allyTeamId` &mdash; The ally team id value used by this operation.
    - `battleSkin` &mdash; The battle skin value used by this operation.
    - `labelTable` &mdash; The label table value used by this operation.

`public void Tick(float presentationDeltaSeconds)`

:   Advances token plate animation by a visual delta.
    - `presentationDeltaSeconds` &mdash; The presentation delta seconds value used by this operation.

`public static string TokenPoolKeyFor(StableId combatantId)`

:   The pool key that gives one combatant its own body: `presentation.token.`. Register a prototype under this key and that combatant spawns from it; register nothing and it falls back to `TokenPoolKey`, so a project can give art to some combatants and not others. The stage only looks for the specific key when the pool can be asked whether it holds one, because `IPoolAdapter.Acquire` is allowed to fabricate an empty instance for an unknown key rather than returning null, and a fallback built on null would silently spawn blank tokens instead.
    - `combatantId` &mdash; The combatant whose prototype is wanted.
    - **Returns** &mdash; The validated result of the operation.

`public bool TryGetAnchorWorld()`

:   Resolves a beat anchor to stage space for a combatant.
    - `anchorId` &mdash; The anchor id value used by this operation.
    - `combatantId` &mdash; The combatant id value used by this operation.
    - `kind` &mdash; The kind value used by this operation.
    - `world` &mdash; The world value used by this operation.
    - **Returns** &mdash; True when the operation succeeds; otherwise false.

`public bool TryGetToken(StableId combatantId, out CombatantTokenView token)`

:   Returns the spawned token for a combatant, if present.
    - `combatantId` &mdash; The combatant id value used by this operation.
    - `token` &mdash; The token value used by this operation.
    - **Returns** &mdash; True when the operation succeeds; otherwise false.

`public bool TryPickTokenAtWorld(Vector3 worldPoint, out StableId combatantId)`

:   Finds the combatant standing nearest a point on the stage.
    - `worldPoint` &mdash; The point to test, in world space, and only its x and y are read. Tokens are placed at world positions rather than under this transform, so this is measured against those positions directly.
    - `combatantId` &mdash; The combatant found, or the default id when none is near enough.
    - **Returns** &mdash; True when a combatant stands within `TokenPickRadiusPixels` of the point. Ties resolve to the lowest id so the same click always picks the same combatant.

`public void UpdateFromSnapshot(BattleSnapshot snapshot)`

:   Mirrors current snapshot state onto every token.
    - `snapshot` &mdash; The snapshot value used by this operation.

---

## BattleStageBackdrop

```csharp
public sealed class BattleStageBackdrop : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/BattleStageBackdrop.cs</small>

Optional background blur for the perform moment. **Off by default and never required.**

While a skill performs, everything behind the battle stage softens so the eye stays on
the participants. The shipped `FocusPerformModule` does the same job by
tinting non-participants, which costs nothing and works everywhere; this is the richer
alternative for a project that wants the background itself to go out of focus.

**Works in every render pipeline.** This is not an image effect. It renders the scene
a second time, without TempoForge's own content, into a half-resolution RenderTexture,
softens that through a chain of bilinear blits, and shows the result on a quad behind
the stage. A camera, a RenderTexture and `Graphics.Blit(Texture,RenderTexture)`
behave the same under Built-in, URP and HDRP -- unlike `OnRenderImage`, which is why
`BattleStageBloom` has to disable itself outside Built-in and this does not.

**Only the background is blurred.** The capture hides the stage tokens and the battle
interface for the duration of its own render, so the participants are never in the
blurred image and never ghost behind their sharp selves.

The blur is live rather than a snapshot: it is re-rendered each frame while
`Strength` is above zero, so anything still moving behind the wash stays
readable. At zero it releases everything it allocated and costs nothing at all.

To enable: add it to the battle camera. Drive `Strength` yourself, or
register a `BackdropBlurPerformModule` to have it ride the perform beat.

**Properties**

`public bool IsActive`

:   True once the capture camera and its buffers exist.

`public float Strength`

:   How far out of focus the background is, 0 to 1. Zero tears the whole effect down. Writable so a perform module can pull focus on impact and ease it back. Values outside the range clamp rather than doing something surprising.

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

`public float Intensity`

:   Bloom strength added over the stage. Zero skips the bloom pass entirely and blits the frame through unchanged. Writable so a perform module can pulse it on impact and ease it back to the authored resting value. Negative values clamp to zero rather than inverting the effect.

`public bool IsSupportedPipeline`

:   True when this effect can run in the active pipeline.

`public float VignetteStrength`

:   Corner darkening strength, 0 to 1. Zero skips the vignette. Writable for the same reason `Intensity` is: a perform module can close the frame in on impact and ease it back to the authored resting value. Independent of the bloom -- a vignette with `Intensity` at zero draws the vignette and no bloom.

**Fields**

`public const string ShaderName`

:   Name of the optional bloom shader.

`public const string ShaderResourcePath`

:   Resources path of the optional bloom shader.

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

Attach next to a `BattlePresenter`; it re-applies the viewport
whenever the screen, safe area, or any field changes.

**Properties**

`public FormationViewport AppliedViewport`

:   The viewport most recently pushed to the presenter.

**Methods**

`public void ApplyNow()`

:   Recomputes and applies the stage viewport. Cheap to call repeatedly: when the result matches the viewport already applied, the presenter is not touched at all. Screen and safe-area changes trigger this automatically, so an explicit call is only needed to force a re-frame.

`public FormationViewport Resolve(int screenWidth, int screenHeight, Rect safeAreaPixels)`

:   Computes the stage viewport for a screen. Public and parameterised so EditMode tests can verify every mode and margin without a device. Pure: it reads the serialized fields but applies nothing to the presenter.
    - `screenWidth` &mdash; Screen width in pixels. Outside Explicit mode, a non-positive value falls back to a 1x1 viewport rather than throwing.
    - `screenHeight` &mdash; Screen height in pixels, treated as `screenWidth` is.
    - `safeAreaPixels` &mdash; The device safe area in pixels. Ignored unless the safe-area option is on, and ignored when its width or height is not positive, so passing a default Rect is a valid way to ask for the full screen.
    - **Returns** &mdash; The stage rectangle in pixels with a bottom-left origin, never smaller than 1x1. In Explicit mode the screen arguments are ignored entirely.

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
    - `battleEvent` &mdash; The event to read; only its typed properties are inspected.
    - **Returns** &mdash; The extracted context, or the default context when the event is null. Source falls back to the actor id, and amount to the actual delta when present, otherwise the plain amount; both are absent when untyped. The critical, shielded, and killing-blow flags read false unless the event says otherwise.

`public static PresentationBeat Derive()`

:   Derives the single beat for one event (never null).
    - `battleEvent` &mdash; The gameplay event to map; null yields a default context.
    - `recipes` &mdash; The candidate recipe set searched for a match.
    - `catalog` &mdash; Compiled content supplying the skill/status tag tables that tag selectors match against.
    - **Returns** &mdash; A beat pairing the event's context with the winning recipe, or with a null recipe (an instant no-visual beat) when no recipe matches.

---

## CombatantTokenView

```csharp
public sealed class CombatantTokenView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/CombatantTokenView.cs</small>

A neutral 2D token view for one combatant. It mirrors compiled slot data
(facing, sorting) and snapshot/event state (health, shield, status pips,
death) onto an optional `SpriteRenderer` and, when a skin is
supplied, onto a `SkinnedTokenPlate` that draws those values.

It reads values only; it never computes or mutates anything authoritative.

**Properties**

`public ProjectedFormationPoint ApproachProjected`

:   The projected point a step-in should travel toward, in reference pixels. It is recorded but never used here; the token stays at `SlotProjected` unless the host animates it.

`public StableId CombatantId`

:   The combatant this token stands for, as given to `Configure`. It is the default id until the token has been configured, which matters for tokens taken from a pool.

`public FormationFacing Facing`

:   The facing recorded from the compiled slot. `FormationFacing.Left` is what flips the sprite renderer horizontally, so one sprite serves both sides of the field.

`public int Health`

:   Health from the last mirrored snapshot state. A null combatant passed to `ApplyState` leaves the previous value standing.

`public float HealthFraction`

:   Normalized health in [0,1] for a bar; 0 when max is unset.

`public bool IsDead`

:   Whether the mirrored state has stopped counting the combatant as living. This is what desaturates and fades the sprite; the token is never hidden or destroyed on death.

`public int MaximumHealth`

:   The health ceiling from the last mirrored snapshot state, used by `HealthFraction`.

`public SkinnedTokenPlate Plate`

:   The plate drawing this token's values, or null when unskinned.

`public int ShieldAmount`

:   The shield total the plate draws. A negative amount handed to `ApplyState` is stored as zero, so the bar can never invert.

`public ProjectedFormationPoint SlotProjected`

:   The projected rest position in reference pixels, which `Configure` converts to world units and moves the token to.

`public StableId SortingLayerKey`

:   The sorting layer the caller asked for. It is recorded only: `Configure` never assigns a layer to the renderer, so a host that cares about layers has to apply this itself.

`public int SortingOrder`

:   Draw order within the sorting layer. Unlike `SortingLayerKey`, this is written straight onto the sprite renderer.

`public int StatusPipCount`

:   How many status pips to draw, clamped at zero the same way `ShieldAmount` is.

**Fields**

`public const float PlateOffsetPixels`

:   Plate offset above the token, in reference pixels.

**Methods**

`public void ApplySkin(CompiledBattleSkin battleSkin, float unitsPerPixel)`

:   Attaches the skinned plate that renders this token's values. Optional: a token with no skin still mirrors state onto its properties, which is what the headless tests assert against.
    - `battleSkin` &mdash; The compiled skin to draw with; null leaves the token unskinned and adds no plate.
    - `unitsPerPixel` &mdash; World units per reference pixel, used to size and offset the plate.

`public void ApplyState()`

:   Mirrors snapshot/event state onto the token and its plate.
    - `combatant` &mdash; Snapshot state to mirror; null leaves health, maximum, and death as they were.
    - `shieldAmount` &mdash; Shield amount to display; negative values clamp to zero.
    - `statusPipCount` &mdash; How many status pips to show; negative values clamp to zero.

`public void Configure()`

:   Places the token from its compiled slot projection.
    - `facing` &mdash; Compiled slot facing; Left flips the sprite horizontally.
    - `sortingLayerKey` &mdash; Recorded for the caller to apply; only `sortingOrder` reaches the sprite renderer.
    - `slotProjected` &mdash; Projected rest position, in reference pixels, that the token is moved to.
    - `approachProjected` &mdash; Projected approach point, recorded for callers that animate a step-in; Configure does not move the token to it.
    - `unitsPerPixel` &mdash; World units per reference pixel, applied to the projected position.
    - `combatantId` &mdash; The combatant id value used by this operation.
    - `sortingOrder` &mdash; The sorting order value used by this operation.

`public void Pulse()`

:   Starts a visual pulse that always returns to rest. Replaces the older behaviour of assigning a scale that was never restored.

`public void SetCastProgress(float fraction, bool visible)`

:   Shows cast progress on the plate, or hides the cast bar.
    - `fraction` &mdash; Cast progress in [0,1]; read only when `visible` is true.
    - `visible` &mdash; False hides the cast bar. Does nothing when the token is unskinned.

`public void SetGauge(float fraction, bool visible)`

:   Shows the scheduler gauge on the plate, or hides it.
    - `fraction` &mdash; Gauge fill in [0,1]; a full gauge is drawn with the ready accent.
    - `visible` &mdash; False hides the gauge. Does nothing when the token is unskinned.

`public void SetPlateIdentity(string label, Color teamTint)`

:   Updates set plate identity on presentation state only. The call cannot submit a command, advance a tick, or change an authoritative hash.
    - `label` &mdash; The resolved display string; ignored when the token is unskinned.
    - `teamTint` &mdash; Tint that distinguishes ally from enemy, replacing the skin default.

`public void Tick(float deltaSeconds)`

:   Advances plate and pulse animation by a visual delta.
    - `deltaSeconds` &mdash; Wall-clock seconds since the last call. Non-positive values are ignored, and this is presentation time only: it never advances the battle.

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

:   Pairs an event's beat context with the recipe resolved for it.
    - `context` &mdash; The data extracted from the source event.
    - `recipe` &mdash; The resolved recipe, or null to make this an instant no-visual beat.

**Properties**

`public PresentationBeatContext Context`

:   Everything the beat knows about the event it came from: participants, tick, and any amount. It is captured once when the beat is built, so a beat that plays several frames later still draws the situation as it stood at the event rather than as the battle stands now.

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

:   Creates a beat context. Normally produced by `BeatDeriver.BuildContext` from an event's property set; construct one directly only to drive a beat without a live battle.
    - `eventTypeId` &mdash; The source event's type, one of the `BattleIds` event identifiers.
    - `tick` &mdash; The tick the source event was emitted on.
    - `eventSequence` &mdash; The source event's battle-wide sequence, which identifies this beat's origin uniquely.
    - `sourceId` &mdash; The acting combatant, or null when the event names none.
    - `targetId` &mdash; The affected combatant, or null when the event names none.
    - `skillId` &mdash; The skill involved, or null.
    - `statusId` &mdash; The status involved, or null.
    - `reactionId` &mdash; The reaction rule involved, or null.
    - `amount` &mdash; The event's numeric amount, for a floating number. Null when the event carries none, which is the common case for non-numeric events such as a cast starting.

`public PresentationBeatContext()`

:   Creates a beat context that also carries the outcome flags a hit can have. Same as the shorter form in every other respect; the flags default to false there, which is what an event that does not report them reads as.
    - `eventTypeId` &mdash; The source event's type, one of the `BattleIds` event identifiers.
    - `tick` &mdash; The tick the source event was emitted on.
    - `eventSequence` &mdash; The source event's battle-wide sequence, which identifies this beat's origin uniquely.
    - `sourceId` &mdash; The acting combatant, or null when the event names none.
    - `targetId` &mdash; The affected combatant, or null when the event names none.
    - `skillId` &mdash; The skill involved, or null.
    - `statusId` &mdash; The status involved, or null.
    - `reactionId` &mdash; The reaction rule involved, or null.
    - `amount` &mdash; The event's numeric amount, for a floating number. Null when the event carries none.
    - `isCritical` &mdash; Whether the event reported the hit as critical.
    - `blockedByShield` &mdash; Whether a shield absorbed some or all of the amount.
    - `isKillingBlow` &mdash; Whether the amount took its target out of the battle.

**Properties**

`public int? Amount`

:   The amount to show as a floating number, or null when the source event carries no numeric amount.

`public bool BlockedByShield`

:   Whether a shield absorbed some or all of the amount. Offered so a project can play a block rather than a hit; nothing in the shipped beats reads it yet.

`public ulong EventSequence`

:   The source event's battle-wide sequence. It identifies this beat's origin uniquely, so it is what to key on when suppressing a beat already played.

`public StableId EventTypeId`

:   Which kind of gameplay event the beat came from. Recipe resolution matches on it before anything else, so a recipe declaring another event type is never considered however specific its selector is.

`public bool IsCritical`

:   Whether the source event reported the hit as critical. False when the event says nothing about it, so a beat built from an emitter that does not report criticals reads exactly as it always did.

`public bool IsKillingBlow`

:   Whether this amount is what took the target out of the battle. The authoritative death is still its own event; this only lets a visual react on the blow instead of one event later.

`public StableId? ReactionId`

:   The reaction rule that produced the event, or null. Only a recipe selecting by reaction ID reads it, which is how a counter-attack can be given its own look without touching the ordinary attack recipe.

`public StableId? SkillId`

:   The skill involved, or null. A recipe that selects by skill ID or skill tag can only match while this is present; without it the candidates are the event-default recipes plus any status or reaction selector the event still satisfies.

`public StableId? SourceId`

:   The acting combatant, or null when the event names none. Animations play on this combatant's token, and a visual effect anchors here when the event carries no target.

`public StableId? StatusId`

:   The status involved, or null. It is what recipes selecting by status ID or status tag match against.

`public StableId? TargetId`

:   The affected combatant, or null when the event names none. Visual effects prefer this anchor over `SourceId`, so a hit lands on the receiver rather than on whoever swung.

`public long Tick`

:   The tick the source event was emitted on. It is battle time, not the moment the beat is drawn - a queue of beats can still be playing out several ticks behind the simulation.

---

## PresenterBinding

:material-star: **Start here**

```csharp
public sealed class PresenterBinding
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Stage/PresenterBinding.cs</small>

The explicit dependency bundle a driver hands to a
`BattlePresenter`. It carries compiled content, the
non-authoritative formation layout, the recipe set, the four visual
adapters, the display-string table, and an optional uGUI root. The
binding contains no engine and no authoritative mutator.

**Constructors**

`public PresenterBinding()`

:   Bundles everything a presenter needs into one value. Every argument through `labels` is required and throws `ArgumentNullException` when null, so a binding that constructs is always complete: the presenter never has to null-check its own dependencies.
    - `layout` &mdash; The non-authoritative formation layout, used for placement only.
    - `recipes` &mdash; The recipe set beats are resolved against.
    - `labels` &mdash; The display-string table names are resolved through.
    - `ui` &mdash; Optional uGUI root; null runs the presenter headless.
    - `log` &mdash; Optional shared log-once ledger; a fresh one is created when null.
    - `animation` &mdash; The animation value used by this operation.
    - `audio` &mdash; The audio value used by this operation.
    - `catalog` &mdash; The catalog value used by this operation.
    - `pool` &mdash; The pool value used by this operation.
    - `vfx` &mdash; The vfx value used by this operation.

**Properties**

`public IAnimationAdapter Animation`

:   Plays the animation keys named by a beat's phases.

`public IAudioAdapter Audio`

:   Plays the one-shot sound keys named by a beat's phases.

`public CompiledAuthoringCatalog Catalog`

:   The compiled catalog battle events are interpreted against, used to derive beats and the shape of a pending decision. It is read only, so the presenter can share the same catalog instance as the engine.

`public DisplayStringTable Labels`

:   Display text for the IDs shown to players. Compiled content carries no labels, so an ID this table does not hold falls back to its raw ID text instead of rendering blank.

`public CompiledEncounterFormationLayout Layout`

:   Where each combatant sits on the stage. It is non-authoritative, so swapping it moves the art and nothing else.

`public PresentationLog Log`

:   Shared log-once ledger for missing-key degradation.

`public IPoolAdapter Pool`

:   Lends out the instances behind token views, floating numbers, and pooled effects. The presenter and the stage return what they borrowed on teardown rather than destroying it, so the same pool survives repeated battles.

`public PresentationRecipeSet Recipes`

:   The ordered recipe list every battle event is matched against. Candidate recipes come only from this set and nothing else in the project is scanned, though tag selectors are matched against the catalog's compiled skill and status tables. An event that matches no recipe here still becomes a beat, just one with no visuals.

`public BattleUiRoot Ui`

:   Optional uGUI root; null runs the presenter headless.

`public IVfxAdapter Vfx`

:   Plays the one-shot effect keys named by a beat's phases.

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

