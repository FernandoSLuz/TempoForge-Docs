# Interface and widgets

23 types in this area.

!!! abstract "On this page"
    [BattleNumberFormat](#battlenumberformat) &middot; [BattleUiCommandChoice](#battleuicommandchoice) &middot; [BattleUiRoot](#battleuiroot) &middot; [DecisionOptions](#decisionoptions) &middot; [DecisionShapeCompiler](#decisionshapecompiler) &middot; [DisplayStringTable](#displaystringtable) &middot; [FeedbackLogView](#feedbacklogview) &middot; [FloatingNumberLabel](#floatingnumberlabel) &middot; [PointerFocusRelay](#pointerfocusrelay) &middot; [ResultBannerView](#resultbannerview) &middot; [SafeAreaFitter](#safeareafitter) &middot; [SkillCommandShape](#skillcommandshape) &middot; [SkillTrayView](#skilltrayview) &middot; [SkinnedTokenPlate](#skinnedtokenplate) &middot; [SkinnedValueBar](#skinnedvaluebar) &middot; [SkinnedWidgetFactory](#skinnedwidgetfactory) &middot; [StatusRosterView](#statusrosterview) &middot; [TargetShape](#targetshape) &middot; [TimelineStripView](#timelinestripview) &middot; [TooltipData](#tooltipdata) &middot; [TooltipPanelView](#tooltippanelview) &middot; [TransportBarView](#transportbarview) &middot; [UiStatusEntry](#uistatusentry)

## BattleNumberFormat

```csharp
public static class BattleNumberFormat
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/BattleNumberFormat.cs</small>

Turns the simulation's fixed-point types into player-facing text.

`ixed64` and `hance64` deliberately expose only
raw scaled integers, because their `ToString` feeds canonical
encoding and must never drift. A tooltip that printed those directly would
show "50000" instead of "5" and "875000" instead of "87.5%", so display
formatting belongs here in the presentation layer.

Every conversion is integer arithmetic. No float ever touches a value that
could be mistaken for an authoritative number.

**Methods**

`public static string Amount(Fixed64 value)`

:   Formats a fixed-point amount, trimming trailing zeros: 5, 5.5, 5.25.

`public static string AmountRange(Fixed64 minimum, Fixed64 maximum)`

:   Formats a range as "12" when both ends match, otherwise "10-14".

`public static string Percent(Chance64 value)`

:   Formats a chance as a percentage, trimming trailing zeros: 100%, 87.5%, 0.05%.

`public static string Ticks(int ticks)`

:   Formats a tick count as a short duration, "12t".

`public static string WholeAmount(Fixed64 value)`

:   Formats a fixed-point amount rounded to a whole number, which is what damage and healing readouts usually want.

---

## BattleUiCommandChoice

```csharp
public readonly struct BattleUiCommandChoice
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/BattleUiRoot.cs</small>

A player-chosen command the driver (not the UI) will submit.

**Constructors**

`public BattleUiCommandChoice()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public bool IsConcede`

:   &mdash;

`public StableId? SkillId`

:   &mdash;

`public FrozenList<StableId> Targets`

:   &mdash;

---

## BattleUiRoot

```csharp
public sealed class BattleUiRoot : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/BattleUiRoot.cs</small>

The battle interface. It offers the pending actor's legal command shapes,
surfaces the timeline, roster, feedback log, tooltips, and terminal
results verbatim from snapshots and events, and raises a plain C# event
with the chosen command for the DRIVER to submit.

It submits nothing, resolves no targets exactly, and invokes no simulation
or preview API; tooltips are supplied to it as computed
`ooltipData` values.

Every colour, size, font, animation timing, and region position comes from
a `attleSkinPreset`, so the whole interface restyles from one
asset with no prefab editing. With no preset assigned it falls back to the
shipped default skin rather than rendering unstyled boxes.

**Properties**

`public DecisionOptions CurrentDecision`

:   &mdash;

`public IReadOnlyList<string> FeedbackLines`

:   &mdash;

`public string InputUnavailableMessage`

:   &mdash;

`public string InputUnavailableMessage`

:   &mdash;

`public bool IsResultShown`

:   &mdash;

`public BattleUiCommandChoice? LastCommandChoice`

:   &mdash;

`public bool LegacyInputAvailable`

:   Classic input is available; the demo polls it here.

`public bool LegacyInputAvailable`

:   The legacy input manager is disabled. The tray remains fully clickable through the graphic raycaster, so only the number-key shortcuts are unavailable; nothing throws.

`public IReadOnlyList<SkillCommandShape> OfferedSkills`

:   &mdash;

`public bool OffersConcede`

:   &mdash;

`public StableId? ResultId`

:   &mdash;

`public string ResultText`

:   &mdash;

`public CompiledBattleSkin Skin`

:   The resolved skin this interface draws with.

`public IReadOnlyList<UiStatusEntry> StatusEntries`

:   &mdash;

`public IReadOnlyList<StableId> TimelineActors`

:   &mdash;

`public RectTransform TransportMount`

:   A mount point for host-supplied controls such as the sample's scenario picker, placed by the skin's transport region.

**Events**

`public event Action<BattleUiCommandChoice> CommandChosen`

:   Raised when the player chooses a command; never submitted here.

**Methods**

`public void AppendFeedback(BattleEvent battleEvent, DisplayStringTable labels)`

:   Appends one feedback line from an event (bounded log).

`public void ApplySkin(BattleSkinPreset preset)`

:   Replaces the skin and rebuilds the interface. Safe to call at runtime, which is what lets the Skin Browser preview a look live.

`public void ChooseConcede()`

:   Raises a concession command for the driver.

`public void ChooseSkill(StableId skillId, IReadOnlyList<StableId> targets)`

:   Raises the chosen-skill command for the driver. The UI submits nothing; it only surfaces the player's intent.

`public void ClearDecision()`

:   Clears any offered decision.

`public void Initialize()`

:   Builds the uGUI tree. Explicit so EditMode tests can call it.

`public void SetTooltip(TooltipData tooltip)`

:   Stores driver-computed tooltip data for a skill, verbatim.

`public void ShowDecision(DecisionOptions options)`

:   Offers exactly the legal command shapes the snapshot exposes.

`public void ShowResult(BattleResultState result, DisplayStringTable labels)`

:   Surfaces a terminal result verbatim (all five kinds).

`public void Tick(float presentationDeltaSeconds)`

:   Advances interface animation by a visual delta. The driver forwards its presentation delta here so pause and speed apply to the HUD exactly as they do to the stage.

`public bool TryGetTooltip(StableId skillId, out TooltipData tooltip)`

:   Returns the tooltip previously supplied for a skill.

`public void UpdateStatus(BattleSnapshot snapshot, DisplayStringTable labels)`

:   Rebuilds the status panel from the snapshot.

`public void UpdateTimeline(FrozenList<DecisionEntry> decisions)`

:   Mirrors the currently-ready decision entries as the timeline.

---

## DecisionOptions

```csharp
public sealed class DecisionOptions
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/DecisionShape.cs</small>

The complete set of legal command shapes for one pending decision:
filtered granted skills plus whether concession is offered. This is a
display projection, never a submission.

**Constructors**

`public DecisionOptions()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public bool CanConcede`

:   &mdash;

`public bool HasActor`

:   &mdash;

`public static DecisionOptions None`

:   &mdash;

`public IReadOnlyList<SkillCommandShape> Skills`

:   &mdash;

---

## DecisionShapeCompiler

```csharp
public static class DecisionShapeCompiler
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/DecisionShape.cs</small>

Pure compiler of legal command shapes from a snapshot and compiled
catalog. It offers a granted skill only when the snapshot-visible
cooldowns, resource costs, and restriction tags allow it, and it reads
the target shape from the compiled target contract. It performs no exact
re-resolution and calls no engine mutator or preview API.

**Methods**

`public static DecisionOptions Compile()`

:   &mdash;

---

## DisplayStringTable

```csharp
public sealed class DisplayStringTable
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/DisplayStringTable.cs</small>

A non-authoritative map from stable id to display text. Compiled
snapshots carry no labels (they are excluded from B3 compilation and
hashes), so the driver supplies this table from authoring
`DisplayLabel` metadata or a shipped serialized string table. The
table never enters any hash and never affects a simulation output.

**Constructors**

`public DisplayStringTable(IEnumerable<KeyValuePair<StableId, string>> pairs = null)`

:   &mdash;

**Properties**

`public int Count`

:   &mdash;

`public static DisplayStringTable Empty`

:   An empty table; every lookup falls back to the raw id.

**Methods**

`public string GetOrId(StableId id)`

:   Returns the label for an id, or the raw id text as a fallback.

`public bool TryGet(StableId id, out string text)`

:   &mdash;

---

## FeedbackLogView

```csharp
public sealed class FeedbackLogView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/FeedbackLogView.cs</small>

The rolling battle log. It shows the most recent lines newest-last and
fades older entries so the newest line reads first.

The owning `attleUiRoot` keeps the authoritative bounded line
list; this view only draws a window onto its tail, so the 512-line cap is
enforced in exactly one place.

**Methods**

`public void Apply(IReadOnlyList<string> allLines)`

:   Draws the tail of `allLines`. The newest line is fully opaque and older ones fade toward the muted role.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the panel. Explicit so EditMode tests can drive it.

---

## FloatingNumberLabel

```csharp
public sealed class FloatingNumberLabel : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Widgets/FloatingNumberLabel.cs</small>

One rise-and-fade combat number.

It draws on a small world-space canvas so it tracks the stage position it
was spawned at with no per-frame screen projection. Colour, size, rise
distance, lifetime, and easing all come from the skin, and criticals scale
up so a big hit reads without a separate art asset.

The value shown is formatted from the amount the beat carried. It is
display only and never re-derived from simulation state.

**Properties**

`public string DisplayText`

:   The text currently displayed.

`public bool IsFinished`

:   True once the number has finished its lifetime.

**Methods**

`public static FloatingNumberLabel Attach(GameObject host, CompiledBattleSkin skin)`

:   Attaches the label hierarchy to a pooled instance. Separate from `lay` so a host that registers its own prototype can build the visuals once instead of per spawn.

`public void Play(CompiledBattleSkin skin, FloatingNumberStyle style, int amount)`

:   Starts one rise-and-fade for `amount`.

`public void Tick(float deltaSeconds)`

:   Advances the rise and fade by a visual delta.

---

## PointerFocusRelay

```csharp
public sealed class PointerFocusRelay : MonoBehaviour, IPointerEnterHandler, IPointerExitHandler
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/SkillTrayView.cs</small>

Forwards pointer enter and exit as plain C# events. Used for tooltip
focus without pulling in an EventTrigger asset or a serialized callback
list, both of which would be awkward to build procedurally.

**Events**

`public event Action Entered`

:   Raised when the pointer enters this element.

`public event Action Exited`

:   Raised when the pointer leaves this element.

**Methods**

`public void OnPointerEnter(PointerEventData eventData)`

:   &mdash;

`public void OnPointerExit(PointerEventData eventData)`

:   &mdash;

---

## ResultBannerView

```csharp
public sealed class ResultBannerView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/ResultBannerView.cs</small>

The terminal result banner. It surfaces all five terminal kinds (victory,
defeat, draw, concession, and the stalled result) and tints itself by
outcome so the end state reads instantly.

It displays the result it is handed and decides nothing about the outcome.

**Properties**

`public bool IsShown`

:   True while the banner is displayed.

**Methods**

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the banner. Explicit so EditMode tests can drive it.

`public void Hide()`

:   Hides the banner.

`public void Show(StableId resultId, string headlineText, string detailText)`

:   Shows a terminal result. `headlineText` and `detailText` are already-localized display strings.

`public void Tick(float deltaSeconds)`

:   Advances the fade-in by a visual delta.

---

## SafeAreaFitter

```csharp
public sealed class SafeAreaFitter : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/SafeAreaFitter.cs</small>

Insets a `ectTransform` to the device safe area so HUD
regions never land under a notch, a punch-hole camera, or a home
indicator. It re-applies only when the screen or safe area actually
changes, so it costs nothing on desktop.

The whole HUD sits inside one of these, which means every skin region is
automatically safe-area correct without the buyer positioning anything
twice.

**Properties**

`public Rect AppliedNormalizedArea`

:   The normalized safe area currently applied.

**Methods**

`public bool Apply(int screenWidth, int screenHeight, Rect safeAreaPixels)`

:   Applies a safe area explicitly. Public and parameterised so EditMode tests can verify inset maths without a device.

---

## SkillCommandShape

```csharp
public sealed class SkillCommandShape
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/DecisionShape.cs</small>

One legal skill command shape offered to the pending actor.

**Constructors**

`public SkillCommandShape(StableId skillId, TargetShape target)`

:   &mdash;

**Properties**

`public StableId SkillId`

:   &mdash;

`public TargetShape Target`

:   &mdash;

---

## SkillTrayView

```csharp
public sealed class SkillTrayView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/SkillTrayView.cs</small>

The command tray offered to a pending human actor: one button per legal
skill shape plus concede.

It raises plain C# events carrying the player's choice and submits
nothing. Target resolution, legality, and submission all stay with the
driver and the engine, which is what keeps the presenter-purity contract
intact while still giving the player something clickable.

**Properties**

`public int VisibleButtonCount`

:   Buttons currently visible.

**Fields**

`public SkinSurfaceGraphic Background`

:   &mdash;

`public Button Button`

:   &mdash;

`public Text Caption`

:   &mdash;

`public GameObject Host`

:   &mdash;

`public Text Name`

:   &mdash;

`public StableId SkillId`

:   &mdash;

**Events**

`public event Action ConcedeChosen`

:   Raised when the player concedes. Never submitted here.

`public event Action<StableId> SkillChosen`

:   Raised when the player picks a skill. Never submitted here.

`public event Action SkillFocusCleared`

:   Raised when the pointer leaves every skill button.

`public event Action<StableId> SkillFocused`

:   Raised when the pointer enters a skill button.

**Methods**

`public void Apply(DecisionOptions options, DisplayStringTable labels)`

:   Offers exactly the shapes in `options`. An empty or non-human decision hides the tray entirely.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the tray. Explicit so EditMode tests can drive it.

`public void ClearSelection()`

:   Clears every button highlight.

`public void SetSelected(StableId skillId)`

:   Highlights the button for `skillId`.

---

## SkinnedTokenPlate

```csharp
public sealed class SkinnedTokenPlate : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Widgets/SkinnedTokenPlate.cs</small>

The floating plate above one combatant: name, health, shield, cast
progress, scheduler gauge, and status pips.

It lives on a world-space canvas parented to the token, so it tracks the
token with no per-frame screen projection and works with any camera setup
the buyer already has. Everything it draws comes from values handed to it;
it reads no simulation state and computes nothing authoritative.

**Properties**

`public bool IsBuilt`

:   True once `uild` has run.

`public int VisiblePipCount`

:   Status pips currently visible.

**Methods**

`public void ApplyState()`

:   Mirrors health, shield, and status counts onto the plate.

`public void Build(CompiledBattleSkin battleSkin, float unitsPerPixel, float verticalOffsetPixels)`

:   Builds the plate. Explicit so EditMode tests can construct one with no scene and no camera.

`public void Pulse(Transform target)`

:   Starts a scale pulse that always returns to rest. The previous implementation set a scale and never restored it, so tokens grew permanently every time they acted.

`public void SetCast(float fraction, bool visible)`

:   Shows cast progress in [0,1], or hides the bar.

`public void SetGauge(float fraction, bool visible)`

:   Shows the scheduler gauge in [0,1], or hides it.

`public void SetLabel(string text)`

:   Sets the displayed combatant name.

`public void SetTeamTint(Color tint)`

:   Tints the plate for a team. Keeps ally and enemy readable at a glance without requiring per-combatant art.

`public void Tick(float deltaSeconds)`

:   Advances plate animation. Driven by the presenter's visual clock so pause and speed apply, and so tests can step it deterministically.

---

## SkinnedValueBar

```csharp
public sealed class SkinnedValueBar : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Widgets/SkinnedValueBar.cs</small>

A skinned value bar: track, an optional trailing ghost showing the value
just lost, the live fill, and an optional numeric readout.

The bar animates toward its target rather than snapping, which is what
makes a hit legible at a glance. All motion is presentation-only and
derives from the skin, so `Reduce Motion` or a zero
`Motion Scale` makes every change instant without touching this code.

**Properties**

`public float DisplayedFraction`

:   The fraction currently drawn, in [0,1].

`public bool IsAnimating`

:   True while the fill is still moving toward its target.

`public Text Readout`

:   The numeric readout, or null when the bar was built without one.

`public float TargetFraction`

:   The fraction the bar is animating toward, in [0,1].

**Methods**

`public void Build(CompiledBattleSkin skin, SkinBarTokens barTokens, bool withReadout)`

:   Builds the bar's children. Explicit rather than done in Awake so EditMode tests can construct and drive a bar with no scene.

`public void SetFillColor(Color primary)`

:   Replaces the fill colour, keeping shape, glow, and geometry.

`public void SetFraction(float fraction)`

:   Animates toward `fraction`. A decrease leaves a ghost at the previous value that catches up shortly after, so the player can see how much was just taken.

`public void SetFractionImmediate(float fraction)`

:   Snaps to `fraction` with no animation.

`public void SetReadout(string text)`

:   Sets the numeric readout text, if the bar has one.

`public void Tick(float deltaSeconds)`

:   Advances the bar's animation. Driven by the presenter's visual clock rather than `Update` so pause and speed apply consistently and so tests can step it deterministically.

---

## SkinnedWidgetFactory

```csharp
public static class SkinnedWidgetFactory
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Widgets/SkinnedWidgetFactory.cs</small>

Builds the skinned uGUI primitives the HUD is assembled from. Centralising
construction here is what lets the whole interface restyle from a
`ompiledBattleSkin`: no widget hardcodes a colour, a size, or
a font, and nothing depends on a shipped prefab.

**Methods**

`public static HorizontalLayoutGroup AddHorizontalLayout()`

:   Adds a horizontal layout group with skin-consistent spacing.

`public static ContentSizeFitter AddVerticalFitter(RectTransform rect)`

:   Adds a content-size fitter so a region can size to content.

`public static VerticalLayoutGroup AddVerticalLayout()`

:   Adds a vertical layout group with skin-consistent spacing.

`public static void ApplyRegion(RectTransform rect, SkinRegionTokens region)`

:   Anchors a rect inside its parent according to a skin region, so a customer can move any HUD block by editing the preset alone.

`public static Text CreateLabel()`

:   Creates a label using the skin's typography.

`public static RectTransform CreateRect(string name, Transform parent)`

:   Creates a child object with a `ectTransform`.

`public static SkinSurfaceGraphic CreateSurface()`

:   Creates a skinned surface filling its parent unless resized.

`public static void Fill(RectTransform rect, float inset = 0f)`

:   Stretches a rect to fill its parent with an optional uniform inset.

---

## StatusRosterView

```csharp
public sealed class StatusRosterView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/StatusRosterView.cs</small>

The combatant roster: one row per combatant with name, health bar, shield
readout, and status count. Rows are pooled and reused, so a long battle
allocates nothing per update.

It mirrors supplied `iStatusEntry` values verbatim and reads
no simulation state.

**Properties**

`public int VisibleRowCount`

:   Rows currently visible.

**Fields**

`public SkinSurfaceGraphic Background`

:   &mdash;

`public Text Detail`

:   &mdash;

`public SkinnedValueBar Health`

:   &mdash;

`public GameObject Host`

:   &mdash;

`public Text Name`

:   &mdash;

**Methods**

`public void Apply(IReadOnlyList<UiStatusEntry> entries, DisplayStringTable labels)`

:   Rebuilds the roster from supplied entries.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the panel. Explicit so EditMode tests can drive it.

`public void Tick(float deltaSeconds)`

:   Advances row bar animation by a visual delta.

---

## TargetShape

```csharp
public readonly struct TargetShape
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/DecisionShape.cs</small>

The display-only shape of a skill's target request, taken from the
compiled target contract. It describes what the player may pick; it is
never the engine's exact target resolution.

**Constructors**

`public TargetShape()`

:   &mdash;

**Properties**

`public bool ActorMayAppear`

:   &mdash;

`public bool AutomaticSelection`

:   &mdash;

`public TargetLifeState LifeState`

:   &mdash;

`public int MaximumResolvedTargets`

:   &mdash;

`public int MaximumTargets`

:   &mdash;

`public int MinimumTargets`

:   &mdash;

`public TargetTeamRelation Relation`

:   &mdash;

---

## TimelineStripView

```csharp
public sealed class TimelineStripView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/TimelineStripView.cs</small>

The turn-order strip: one chip per upcoming actor, left to right, with the
actor about to act raised and accented.

Knowing who acts next is the single most important readout in a
tempo-driven battle, which is why this is a first-class HUD region rather
than a line of text. It mirrors the supplied decision order verbatim.

**Properties**

`public int VisibleChipCount`

:   Chips currently visible.

**Fields**

`public SkinSurfaceGraphic Background`

:   &mdash;

`public GameObject Host`

:   &mdash;

`public Text Label`

:   &mdash;

`public Text Order`

:   &mdash;

**Methods**

`public void Apply(IReadOnlyList<StableId> actors, DisplayStringTable labels)`

:   Rebuilds the strip from the supplied actor order.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the strip. Explicit so EditMode tests can drive it.

---

## TooltipData

```csharp
public readonly struct TooltipData
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/TooltipData.cs</small>

A passive tooltip value computed by the DRIVER through the public preview
surface (`BattleFormulaService.Preview` /
`PreviewStatusApplication`, `FormulaPreview`, and
`IEffectResolver.Plan`) and handed to the UI verbatim. The UI stores
and displays it; it never invokes a simulation or preview API itself.

**Constructors**

`public TooltipData()`

:   &mdash;

**Properties**

`public string CostText`

:   &mdash;

`public Chance64 CriticalChance`

:   &mdash;

`public bool HasPreview`

:   &mdash;

`public Chance64 HitChance`

:   &mdash;

`public Fixed64 PreviewMaximum`

:   &mdash;

`public Fixed64 PreviewMinimum`

:   &mdash;

`public StableId SkillId`

:   &mdash;

`public Chance64 StatusChance`

:   &mdash;

`public string TargetShapeText`

:   &mdash;

`public string TimingText`

:   &mdash;

**Methods**

`public static TooltipData TextOnly()`

:   Builds tooltip text with no numeric preview figures.

---

## TooltipPanelView

```csharp
public sealed class TooltipPanelView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/TooltipPanelView.cs</small>

The skill tooltip: cost, timing, target shape, and the driver-computed
preview figures.

It renders a `ooltipData` value verbatim and calls no preview
or simulation API itself, which is what keeps the UI on the passive side
of the presenter contract.

**Properties**

`public bool IsShown`

:   True while a tooltip is displayed.

**Methods**

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the panel. Explicit so EditMode tests can drive it.

`public void Hide()`

:   Hides the tooltip.

`public void Show(string title, TooltipData tooltip)`

:   Shows `tooltip` under `title`.

---

## TransportBarView

```csharp
public sealed class TransportBarView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/Regions/TransportBarView.cs</small>

Scenario picker, seed field, and playback controls, drawn with the skin.

This replaces an `OnGUI`/`GUI.skin.box` overlay. Immediate-mode
chrome is fine for an internal harness but it is the first thing a buyer
sees, it cannot be skinned, it ignores the canvas scaler, and it does not
exist on a touch device. Everything here is real uGUI and therefore
scales, skins, and works on mobile.

Pause, speed, and skip are presentation-only. They scale or halt the
visual clock and never a simulation value, so the same
(scenario, scheduler, formation, seed) tuple still reproduces identical
hashes.

**Events**

`public event Action NextRequested`

:   Raised when the player selects the next scenario.

`public event Action PauseToggled`

:   Raised when the player toggles pause.

`public event Action PreviousRequested`

:   Raised when the player selects the previous scenario.

`public event Action SkipRequested`

:   Raised when the player skips queued visuals.

`public event Action SpeedCycled`

:   Raised when the player cycles playback speed.

`public event Action<string> StartRequested`

:   Raised with the seed text when the player starts a battle.

**Methods**

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the bar. Explicit so EditMode tests can drive it.

`public void SetPaused(bool paused)`

:   Reflects the current pause state on the toggle.

`public void SetScenario(string text)`

:   Sets the displayed scenario name.

`public void SetSeedText(string text)`

:   Sets the seed field text without raising events.

`public void SetSpeed(float multiplier)`

:   Reflects the current playback speed.

`public void SetStatus(string text)`

:   Sets the status line shown under the controls.

---

## UiStatusEntry

```csharp
public readonly struct UiStatusEntry
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/UI/BattleUiRoot.cs</small>

One combatant's surfaced status-panel row.

**Constructors**

`public UiStatusEntry()`

:   &mdash;

**Properties**

`public StableId CombatantId`

:   &mdash;

`public int Health`

:   &mdash;

`public bool IsDead`

:   &mdash;

`public int MaximumHealth`

:   &mdash;

`public int Shield`

:   &mdash;

`public int StatusCount`

:   &mdash;

---

