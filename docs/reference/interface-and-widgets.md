# Interface and widgets

22 types in this area.

!!! abstract "On this page"
    [BattleNumberFormat](#battlenumberformat) &middot; [BattleUiCommandChoice](#battleuicommandchoice) &middot; [BattleUiRoot](#battleuiroot) &middot; [DecisionOptions](#decisionoptions) &middot; [DecisionShapeCompiler](#decisionshapecompiler) &middot; [DisplayStringTable](#displaystringtable) &middot; [FeedbackLogView](#feedbacklogview) &middot; [ResultBannerView](#resultbannerview) &middot; [SafeAreaFitter](#safeareafitter) &middot; [SkillCommandShape](#skillcommandshape) &middot; [SkillTitleView](#skilltitleview) &middot; [SkillTrayView](#skilltrayview) &middot; [SkinnedTokenPlate](#skinnedtokenplate) &middot; [SkinnedValueBar](#skinnedvaluebar) &middot; [SkinnedWidgetFactory](#skinnedwidgetfactory) &middot; [StatusRosterView](#statusrosterview) &middot; [TargetShape](#targetshape) &middot; [TimelineStripView](#timelinestripview) &middot; [TooltipData](#tooltipdata) &middot; [TooltipPanelView](#tooltippanelview) &middot; [TransportBarView](#transportbarview) &middot; [UiStatusEntry](#uistatusentry)

## BattleNumberFormat

:material-star: **Start here**

```csharp
public static class BattleNumberFormat
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/BattleNumberFormat.cs</small>

Turns the simulation's fixed-point types into player-facing text.

`Fixed64` and `Chance64` deliberately expose only
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

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/BattleUiRoot.cs</small>

A player-chosen command the driver (not the UI) will submit.

**Constructors**

`public BattleUiCommandChoice()`

:   Records one choice for the driver to act on.
    - `isConcede` &mdash; True for a concession, which carries no skill.
    - `targets` &mdash; Target ids the player picked. Null becomes empty, and empty leaves exact target resolution to the driver.

**Properties**

`public StableId ActorId`

:   The combatant the command is for. It is taken from the pending decision rather than from whoever clicked, so it always matches the actor the engine is waiting on.

`public bool IsConcede`

:   True when the player conceded instead of picking a skill. Such a choice carries no `SkillId` and no `Targets`.

`public StableId? SkillId`

:   The skill the player picked; null when the choice is a concession.

`public FrozenList<StableId> Targets`

:   The targets the player picked, never null. Empty means the driver still owns target resolution; the shipped tray always raises choices empty.

---

## BattleUiRoot

:material-star: **Start here**

```csharp
public sealed class BattleUiRoot : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/BattleUiRoot.cs</small>

The battle interface. It offers the pending actor's legal command shapes,
surfaces the timeline, roster, feedback log, tooltips, and terminal
results verbatim from snapshots and events, and raises a plain C# event
with the chosen command for the DRIVER to submit.

It submits nothing, resolves no targets exactly, and invokes no simulation
or preview API; tooltips are supplied to it as computed
`TooltipData` values.

Every colour, size, font, animation timing, and region position comes from
a `BattleSkinPreset`, so the whole interface restyles from one
asset with no prefab editing. With no preset assigned it falls back to the
shipped default skin rather than rendering unstyled boxes.

**Properties**

`public DecisionOptions CurrentDecision`

:   The decision currently on offer, or `DecisionOptions.None` when there is nothing to decide. Never null, so it can be read without a guard between battles.

`public IReadOnlyList<string> FeedbackLines`

:   The retained feedback log, oldest line first. A live view, capped at `MaximumFeedbackLines` by dropping the oldest lines.

`public string InputUnavailableMessage`

:   Empty, because shortcuts are available in this build.

`public string InputUnavailableMessage`

:   Display-ready explanation of why the keyboard shortcuts are missing and which project setting restores them. Empty in builds that have them.

`public bool IsResultShown`

:   Whether the result banner is currently up. A `ShowResult` call whose result is null, not yet terminal, or carries no result id clears this again, which is what makes the call safe to repeat every frame.

`public BattleUiCommandChoice? LastCommandChoice`

:   The most recent choice raised through `CommandChosen`. Null until the player has chosen once, and never cleared afterwards.

`public bool LegacyInputAvailable`

:   Classic input is available; the demo polls it here.

`public bool LegacyInputAvailable`

:   The legacy input manager is disabled. The tray remains fully clickable through the graphic raycaster, so only the number-key shortcuts are unavailable; nothing throws.

`public IReadOnlyList<SkillCommandShape> OfferedSkills`

:   The skill shapes the tray is offering, in the order the decision supplied them. Empty whenever no actor is pending.

`public bool OffersConcede`

:   Whether a concede button is offered. This is exactly the condition under which `ChooseConcede` raises anything, so a custom tray can use it to decide whether to draw the button at all.

`public StableId? ResultId`

:   The id of the surfaced result, or null while none is shown. This is the simulation's own result id, not a display string; use the label table to turn it into text.

`public string ResultText`

:   One-line text form of the surfaced result, with the winning team appended when there is one. Empty while no result is shown. The banner draws its own labels; this string is for logs and tests.

`public CompiledBattleSkin Skin`

:   The resolved skin this interface draws with.

`public IReadOnlyList<UiStatusEntry> StatusEntries`

:   The surfaced status rows, in snapshot order. A live view, rebuilt in place by every `UpdateStatus` call.

`public IReadOnlyList<StableId> TimelineActors`

:   The actors on the timeline strip, in the order they were supplied. This is a live view of the interface's own list, so copy it if you need it to survive the next update.

`public RectTransform TransportMount`

:   A mount point for host-supplied controls such as the sample's scenario picker, placed by the skin's transport region.

**Events**

`public event Action<BattleUiCommandChoice> CommandChosen`

:   Raised when the player chooses a command; never submitted here.

**Methods**

`public void AppendFeedback(BattleEvent battleEvent, DisplayStringTable labels)`

:   Appends one feedback line from an event (bounded log).
    - `battleEvent` &mdash; The event to describe; null appends nothing. Its type id, plus the actor id when the event carries one, become the line.
    - `labels` &mdash; Display names for those ids. Any id the table does not cover, and every id at all when this is null, is written as the raw id text.

`public void ApplySkin(BattleSkinPreset preset)`

:   Replaces the skin and rebuilds the interface. Safe to call at runtime, which is what lets the Skin Browser preview a look live.
    - `preset` &mdash; The look to adopt, or null to fall back to the shipped default skin.

`public void ChooseConcede()`

:   Raises a concession command for the driver. Silently does nothing unless the pending decision actually offers concession.

`public void ChooseSkill(StableId skillId, IReadOnlyList<StableId> targets)`

:   Raises the chosen-skill command for the driver. The UI submits nothing; it only surfaces the player's intent.
    - `skillId` &mdash; The skill the player picked. Nothing is raised while no actor is pending, and the id is not re-checked against the offer.
    - `targets` &mdash; Exact targets, copied into the choice. Null or empty hands target resolution to the driver, which is what the shipped tray does.

`public void ClearDecision()`

:   Clears any offered decision.

`public void Initialize()`

:   Builds the uGUI tree. Explicit so EditMode tests can call it. Awake already calls it, and a second call does nothing.

`public void SetTooltip(TooltipData tooltip)`

:   Stores driver-computed tooltip data for a skill, verbatim.
    - `tooltip` &mdash; Already-computed tooltip text. Ignored unless its skill id is valid, and it replaces any tooltip previously stored for that skill.

`public void ShowDecision(DecisionOptions options)`

:   Offers exactly the legal command shapes the snapshot exposes.
    - `options` &mdash; The shapes to offer; null withdraws the offer, as `ClearDecision` does.

`public void ShowResult(BattleResultState result, DisplayStringTable labels)`

:   Surfaces a terminal result verbatim (all five kinds).
    - `result` &mdash; The result to show. Null, not yet terminal, or carrying no result id all hide the banner instead, so this may be called every frame.
    - `labels` &mdash; Display names for the result and winning team ids. Uncovered ids, and all ids when this is null, are shown as raw id text.

`public void Tick(float presentationDeltaSeconds)`

:   Advances interface animation by a visual delta. The driver forwards its presentation delta here so pause and speed apply to the HUD exactly as they do to the stage.
    - `presentationDeltaSeconds` &mdash; Presentation seconds since the last call. Zero or negative is ignored, which is how a paused presentation freezes the HUD.

`public bool TryGetTooltip(StableId skillId, out TooltipData tooltip)`

:   Returns the tooltip previously supplied for a skill.
    - `tooltip` &mdash; The stored tooltip, or the default value when none was supplied.
    - **Returns** &mdash; True when `SetTooltip` has stored data for this skill.

`public void UpdateStatus(BattleSnapshot snapshot, DisplayStringTable labels)`

:   Rebuilds the status panel from the snapshot.
    - `snapshot` &mdash; Source of health, shields, and status counts; null empties the panel. It is only read, never advanced.
    - `labels` &mdash; Display names for the rows. Null keeps the table from an earlier call, so labels never have to be resupplied.

`public void UpdateTimeline(FrozenList<DecisionEntry> decisions)`

:   Mirrors the currently-ready decision entries as the timeline.
    - `decisions` &mdash; Ready entries to mirror, kept in the order supplied; null or empty clears the strip. Only each entry's actor is read.

---

## DecisionOptions

```csharp
public sealed class DecisionOptions
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/DecisionShape.cs</small>

The complete set of legal command shapes for one pending decision:
filtered granted skills plus whether concession is offered. This is a
display projection, never a submission.

**Constructors**

`public DecisionOptions()`

:   Creates an option set. A null skill list becomes an empty one, so a caller never has to null-check `Skills`.
    - `hasActor` &mdash; False for the "nothing to decide" set; see `None`.
    - `canConcede` &mdash; Whether a concede command may be offered alongside the skills.

**Properties**

`public StableId ActorId`

:   The combatant every entry in `Skills` belongs to, and the one whose command the engine will serve next.

`public bool CanConcede`

:   Whether a concede command may be offered alongside the skills. It reports only that the compiled content registers the concede command at all, so it does not vary from actor to actor within a battle.

`public bool HasActor`

:   Whether a decision is actually pending. It is the flag to test before reading `ActorId`, which carries the default ID in the empty set rather than any meaningful combatant.

`public static DecisionOptions None`

:   The empty set - no actor, no concession, no skills. Returned whenever there is nothing for a player to decide.

`public IReadOnlyList<SkillCommandShape> Skills`

:   The skills the actor may use at this moment, ordered by skill ID so a given decision always lays out the same way. Never null. A granted skill that is on cooldown, unaffordable, or restricted by a status is absent altogether rather than present and marked unusable, so a tray that draws greyed-out entries has to keep its own list of what the actor was granted.

---

## DecisionShapeCompiler

```csharp
public static class DecisionShapeCompiler
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/DecisionShape.cs</small>

Pure compiler of legal command shapes from a snapshot and compiled
catalog. It offers a granted skill only when the snapshot-visible
cooldowns, resource costs, and restriction tags allow it, and it reads
the target shape from the compiled target contract. It performs no exact
re-resolution and calls no engine mutator or preview API.

**Methods**

`public static DecisionOptions Compile()`

:   Builds the option set for the decision at the head of the snapshot's queue. Only that first entry is considered, and only when it is human-controlled, because it is the one the engine serves next. A granted skill is offered only when the snapshot shows no live cooldown for it, every resource cost is affordable from the actor's current pools, no status on the actor restricts one of the skill's tags, and its target resolver is registered. Concession is offered when the compiled content registers the concede command at all.
    - `snapshot` &mdash; State to read; nothing in it is mutated.
    - `catalog` &mdash; Compiled content the granted skills and target contracts are read from.
    - **Returns** &mdash; `DecisionOptions.None` for a null argument, an empty or non-human decision queue, a missing or dead actor, or a combatant definition the catalog does not contain; otherwise the legal shapes, ordered by skill id so the same decision always lays out the same way.

---

## DisplayStringTable

:material-star: **Start here**

```csharp
public sealed class DisplayStringTable
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/DisplayStringTable.cs</small>

A non-authoritative map from stable id to display text. Compiled
snapshots carry no labels (they are excluded from B3 compilation and
hashes), so the driver supplies this table from authoring
`DisplayLabel` metadata or a shipped serialized string table. The
table never enters any hash and never affects a simulation output.

**Constructors**

`public DisplayStringTable(IEnumerable<KeyValuePair<StableId, string>> pairs = null)`

:   Copies the supplied labels into a table. The pairs are read once here, so the table does not observe later changes to the source.
    - `pairs` &mdash; Id-to-label pairs; entries with an invalid id or a null label are dropped, and a repeated id keeps the last label. Null builds an empty table.

**Properties**

`public int Count`

:   How many ids carry a label. Pairs the constructor dropped as invalid, and repeats collapsed onto one id, are not counted, so a total below the number of pairs supplied is how those losses show up.

`public static DisplayStringTable Empty`

:   An empty table; every lookup falls back to the raw id.

**Methods**

`public string GetOrId(StableId id)`

:   Returns the label for an id, or the raw id text as a fallback.

`public bool TryGet(StableId id, out string text)`

:   Looks up the label for an id without falling back to it.
    - `text` &mdash; The label, or null when the id is invalid or unlabelled.
    - **Returns** &mdash; True when a label was found.

---

## FeedbackLogView

```csharp
public sealed class FeedbackLogView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/FeedbackLogView.cs</small>

The rolling battle log. It shows the most recent lines newest-last and
fades older entries so the newest line reads first.

The owning `BattleUiRoot` keeps the authoritative bounded line
list; this view only draws a window onto its tail, so the 512-line cap is
enforced in exactly one place.

**Methods**

`public void Apply(IReadOnlyList<string> allLines)`

:   Draws the tail of `allLines`. The newest line is fully opaque and older ones fade toward the muted role.
    - `allLines` &mdash; The whole log, oldest first; only the last `VisibleLines` entries are drawn. Null or empty clears every row.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the panel. Explicit so EditMode tests can drive it. A second call stores the new skin but does not restyle widgets already built.
    - `battleSkin` &mdash; Skin to draw with; null falls back to the shipped default.

---

## ResultBannerView

```csharp
public sealed class ResultBannerView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/ResultBannerView.cs</small>

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
    - `battleSkin` &mdash; Skin to draw with; null falls back to the shipped default.

`public void Hide()`

:   Hides the banner.

`public void Show(StableId resultId, string headlineText, string detailText)`

:   Shows a terminal result. `headlineText` and `detailText` are already-localized display strings.
    - `resultId` &mdash; Terminal result id. It only picks the tint; an id the package does not ship still displays, in the neutral accent.
    - `detailText` &mdash; Second line; when null or empty the line is hidden rather than left blank.

`public void Tick(float deltaSeconds)`

:   Advances the fade-in by a visual delta.

---

## SafeAreaFitter

```csharp
public sealed class SafeAreaFitter : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/SafeAreaFitter.cs</small>

Insets a `RectTransform` to the device safe area so HUD
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

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/DecisionShape.cs</small>

One legal skill command shape offered to the pending actor.

**Constructors**

`public SkillCommandShape(StableId skillId, TargetShape target)`

:   Pairs a skill with the target shape its resolver declares.

**Properties**

`public StableId SkillId`

:   The skill this shape stands for, and the ID to carry in the command once the player commits to it.

`public TargetShape Target`

:   What this skill's resolver will accept: how many target IDs the command may carry and which combatants qualify. Read it to decide how many picks to collect before the command is submittable.

---

## SkillTitleView

```csharp
public sealed class SkillTitleView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/SkillTitleView.cs</small>

The skill title card: the name of what is being performed, announced as it
happens and gone again a moment later.

It draws with the same surface and typography tokens as every other region,
so it inherits whichever skin is applied without any per-skin work. Like the
result banner, it displays what it is handed and decides nothing.

**Properties**

`public float Alpha`

:   Current alpha, which is what a test can assert the fade against.

`public string CurrentTitle`

:   The text currently displayed, empty when the card is resting.

`public bool IsShown`

:   True while the card is on screen, fading counted as shown.

**Methods**

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the card. Explicit so EditMode tests can drive it.
    - `battleSkin` &mdash; Skin to draw with; null falls back to the shipped default.

`public void Hide()`

:   Takes the card down immediately.

`public void Show(string displayName, float holdSeconds, float fadeInOutSeconds)`

:   Announces a skill. Calling it again while a card is up replaces it and restarts the hold, so a fast chain of skills reads as the latest one rather than queueing cards the player will never see.
    - `displayName` &mdash; Already-localized skill name; empty hides the card.
    - `holdSeconds` &mdash; Total seconds on screen, fades included. Zero or less hides the card.
    - `fadeInOutSeconds` &mdash; Fade time at each end, clamped to half the hold.

`public void Tick(float deltaSeconds)`

:   Advances the fade and the hold on the presentation clock, so pause and speed reach the card the same way they reach everything else.
    - `deltaSeconds` &mdash; Elapsed presentation seconds; zero or less does nothing.

---

## SkillTrayView

```csharp
public sealed class SkillTrayView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/SkillTrayView.cs</small>

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

:   The skinned surface behind the button. It is reskinned in place to show selection rather than swapped for another graphic.

`public Button Button`

:   The clickable component. Its listener is wired once when the entry is created and reads `SkillId` at click time, so rebinding the entry to another skill needs no rewiring.

`public Text Caption`

:   The short target description under the name, such as "one enemy".

`public GameObject Host`

:   The button's root object. Entries are pooled rather than destroyed, so this is deactivated when the tray offers fewer skills than it has already built.

`public Text Name`

:   The skill's display name, resolved through the display-string table and falling back to the raw ID text.

`public StableId SkillId`

:   The skill this entry currently stands for. It changes as the tray is reapplied, which is why the click and focus handlers read it rather than capturing it.

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

:   Offers exactly the shapes in `options`. An empty or non-human decision hides the tray entirely. Does nothing before `Build` has run, and never offers more than `MaximumButtons` skills however many are legal.
    - `labels` &mdash; Display names for the actor and skill ids; null, or an id the table does not carry, falls back to the raw id text.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the tray. Explicit so EditMode tests can drive it.
    - `battleSkin` &mdash; Skin every widget in the tray is drawn from; null falls back to `BattleSkinDefaults.Default`. Only the first call builds the widget tree - a later call stores the skin and returns.

`public void ClearSelection()`

:   Clears every button highlight.

`public void SetSelected(StableId skillId)`

:   Highlights the button for `skillId`.

---

## SkinnedTokenPlate

```csharp
public sealed class SkinnedTokenPlate : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Widgets/SkinnedTokenPlate.cs</small>

The floating plate above one combatant: name, health, shield, cast
progress, scheduler gauge, and status pips.

It lives on a world-space canvas parented to the token, so it tracks the
token with no per-frame screen projection and works with any camera setup
the buyer already has. Everything it draws comes from values handed to it;
it reads no simulation state and computes nothing authoritative.

**Properties**

`public bool IsBuilt`

:   True once `Build` has run.

`public int VisiblePipCount`

:   Status pips currently visible.

**Methods**

`public void ApplyState()`

:   Mirrors health, shield, and status counts onto the plate. Does nothing until `Build` has run.
    - `health` &mdash; Current health, used only to derive the bar's fraction.
    - `maximumHealth` &mdash; Denominator for both the health and shield bars. Zero or less empties the health bar and hides the shield, since neither has a scale to be drawn against.
    - `shieldAmount` &mdash; Absorb remaining, drawn as a share of `maximumHealth` and clamped there. Zero hides the shield bar.
    - `statusCount` &mdash; Total statuses on the combatant, not the number of pips to draw. Anything beyond the skin's visible limit collapses into a single overflow pip.
    - `isDead` &mdash; Draws the health bar empty and mutes the name regardless of `health`.

`public void Build(CompiledBattleSkin battleSkin, float unitsPerPixel, float verticalOffsetPixels)`

:   Builds the plate. Explicit so EditMode tests can construct one with no scene and no camera.
    - `battleSkin` &mdash; Skin the plate is dressed from; null falls back to the package default.
    - `unitsPerPixel` &mdash; World units one reference pixel is worth. It scales the whole plate, so `PlateWidth` only means 132 world units at a value of one.
    - `verticalOffsetPixels` &mdash; Height above the token in reference pixels. It is scaled by `unitsPerPixel` too, so the plate keeps its distance as the plate is resized.

`public void Pulse(Transform target)`

:   Starts a scale pulse that always returns to rest. The previous implementation set a scale and never restored it, so tokens grew permanently every time they acted.
    - `target` &mdash; Transform to scale, normally the token root; null pulses this plate's own transform. A zero motion scale in the skin restores rest scale at once instead of animating.

`public void SetCast(float fraction, bool visible)`

:   Shows cast progress in [0,1], or hides the bar.

`public void SetGauge(float fraction, bool visible)`

:   Shows the scheduler gauge in [0,1], or hides it.

`public void SetLabel(string text)`

:   Sets the displayed combatant name.

`public void SetTeamTint(Color tint)`

:   Tints the plate for a team. Keeps ally and enemy readable at a glance without requiring per-combatant art.
    - `tint` &mdash; Colour applied to the combatant's name label; the bars keep the colours the skin gave them.

`public void Tick(float deltaSeconds)`

:   Advances plate animation. Driven by the presenter's visual clock so pause and speed apply, and so tests can step it deterministically.

---

## SkinnedValueBar

```csharp
public sealed class SkinnedValueBar : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Widgets/SkinnedValueBar.cs</small>

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

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Widgets/SkinnedWidgetFactory.cs</small>

Builds the skinned uGUI primitives the HUD is assembled from. Centralising
construction here is what lets the whole interface restyle from a
`CompiledBattleSkin`: no widget hardcodes a colour, a size, or
a font, and nothing depends on a shipped prefab.

**Methods**

`public static HorizontalLayoutGroup AddHorizontalLayout()`

:   Adds a horizontal layout group with skin-consistent spacing.

`public static ContentSizeFitter AddVerticalFitter(RectTransform rect)`

:   Adds a content-size fitter so a region can size to content. A fitter measures `ILayoutElement` components on its OWN object, so `rect` must already carry the layout group whose content it should follow. On a rect with no layout group the preferred height resolves to zero and the region collapses.

`public static VerticalLayoutGroup AddVerticalLayout()`

:   Adds a vertical layout group with skin-consistent spacing.

`public static void ApplyRegion(RectTransform rect, SkinRegionTokens region)`

:   Anchors a rect inside its parent according to a skin region, so a customer can move any HUD block by editing the preset alone.

`public static Text CreateLabel()`

:   Creates a label using the skin's typography.

`public static RectTransform CreateRect(string name, Transform parent)`

:   Creates a child object with a `RectTransform`.

`public static SkinSurfaceGraphic CreateSurface()`

:   Creates a skinned surface filling its parent unless resized.

`public static void Fill(RectTransform rect, float inset = 0f)`

:   Stretches a rect to fill its parent with an optional uniform inset.

`public static LayoutElement IgnoreLayout(RectTransform rect)`

:   Excludes `rect` from its parent's layout group, keeping the anchors it was given. Used for panel backgrounds that must stretch across a region whose children are otherwise laid out in a row or column.

---

## StatusRosterView

```csharp
public sealed class StatusRosterView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/StatusRosterView.cs</small>

The combatant roster: one row per combatant with name, health bar, shield
readout, and status count. Rows are pooled and reused, so a long battle
allocates nothing per update.

It mirrors supplied `UiStatusEntry` values verbatim and reads
no simulation state.

**Properties**

`public int VisibleRowCount`

:   Rows currently visible.

**Fields**

`public SkinSurfaceGraphic Background`

:   The plate drawn behind the row. Hidden while the combatant is down, so a dead row reads as an empty slot rather than a live one.

`public Text Detail`

:   The caption line to the right of the name, carrying shield and status counts, or `Down` alone once the combatant is dead.

`public SkinnedValueBar Health`

:   The health bar. It eases towards its new fraction rather than snapping, so `Tick` has to be called for the movement to be seen.

`public GameObject Host`

:   The row object itself. It is deactivated rather than destroyed when the roster shrinks, which is how the pool avoids reallocating.

`public Text Name`

:   The combatant label. Falls back to the raw id when the display string table has no name, and is drawn muted once the combatant is down.

**Methods**

`public void Apply(IReadOnlyList<UiStatusEntry> entries, DisplayStringTable labels)`

:   Rebuilds the roster from supplied entries, one row per entry in the order given. Rows are added as the roster grows and hidden, not destroyed, as it shrinks.
    - `entries` &mdash; Rows to draw; null or empty hides every row.
    - `labels` &mdash; Name source; null falls back to `DisplayStringTable.Empty`, which shows raw ids.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the panel. Explicit so EditMode tests can drive it.
    - `battleSkin` &mdash; Skin to draw with; null falls back to the shipped default.

`public void Tick(float deltaSeconds)`

:   Advances row bar animation by a visual delta.

---

## TargetShape

```csharp
public readonly struct TargetShape
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/DecisionShape.cs</small>

The display-only shape of a skill's target request, taken from the
compiled target contract. It describes what the player may pick; it is
never the engine's exact target resolution.

**Constructors**

`public TargetShape()`

:   Creates a shape from an already-resolved target contract. It copies the declared limits as given and validates nothing.
    - `minimumTargets` &mdash; Fewest ids a command must carry.
    - `maximumTargets` &mdash; Most ids a command may carry.
    - `maximumResolvedTargets` &mdash; Most combatants the resolver may finally reach, which can exceed `maximumTargets` when one pick spreads.
    - `actorMayAppear` &mdash; Whether the acting combatant is itself a legal pick.
    - `automaticSelection` &mdash; Whether a command carrying no ids is legal, leaving the pick to the resolver.

**Properties**

`public bool ActorMayAppear`

:   Whether the acting combatant is itself a legal pick.

`public bool AutomaticSelection`

:   Whether a command carrying no ids is legal, leaving the pick to the resolver.

`public TargetLifeState LifeState`

:   Which life state a pick must be in. Copied from the compiled contract in the same way as `Relation`, and equally not re-derived here.

`public int MaximumResolvedTargets`

:   Most combatants the resolver may finally reach; can exceed `MaximumTargets` when one pick spreads.

`public int MaximumTargets`

:   Most ids a command may carry.

`public int MinimumTargets`

:   Fewest ids a command must carry.

`public TargetTeamRelation Relation`

:   Which combatants the skill may reach, relative to the acting combatant's team. It is the resolver's declared eligibility copied verbatim, so it is sound for shading legal picks but is not the check the engine performs when the command arrives.

---

## TimelineStripView

```csharp
public sealed class TimelineStripView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/TimelineStripView.cs</small>

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

:   The chip plate, re-dressed on every rebuild: the raised panel surface for the actor about to act and the button surface for the rest.

`public GameObject Host`

:   The chip object. Deactivated rather than destroyed when the order shortens, so the strip reuses its chips for the whole battle.

`public Text Label`

:   The actor's display name, falling back to the raw identifier when the supplied table has no entry for it.

`public Text Order`

:   The caption above the name: `NOW` on the leading chip, and the one-based position in the order on the rest.

**Methods**

`public void Apply(IReadOnlyList<StableId> actors, DisplayStringTable labels)`

:   Rebuilds the strip from the supplied actor order. Does nothing until `Build` has run.
    - `actors` &mdash; Decision order as the simulation reported it, soonest first: index 0 is the chip raised and marked NOW. Entries past `MaximumChips` are not drawn, and null is treated as an empty order.
    - `labels` &mdash; Display names for the actors. A missing entry falls back to the actor's identifier, and null is treated as an empty table.

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the strip. Explicit so EditMode tests can drive it.
    - `battleSkin` &mdash; Skin the chips are dressed from; null falls back to the package default.

---

## TooltipData

```csharp
public readonly struct TooltipData
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/TooltipData.cs</small>

A passive tooltip value computed by the DRIVER through the public preview
surface (`BattleFormulaService.Preview` /
`PreviewStatusApplication`, `FormulaPreview`, and
`IEffectResolver.Plan`) and handed to the UI verbatim. The UI stores
and displays it; it never invokes a simulation or preview API itself.

**Constructors**

`public TooltipData()`

:   Captures one already-computed tooltip. Null text arguments are stored as empty strings, so a consumer never needs a null check.
    - `hasPreview` &mdash; True when the driver ran a numeric preview. While it is false the shipped tooltip panel hides the amount range and the hit and critical figures, and shows only the status chance.

**Properties**

`public string CostText`

:   The cost line, worded and localised entirely by the driver. Nothing in the package parses it back, and an empty string hides the row rather than drawing a blank one.

`public Chance64 CriticalChance`

:   Odds of a critical on a use that lands. The shipped panel leaves the figure out altogether when it is impossible instead of printing zero, so a skill that cannot crit costs no tooltip space.

`public bool HasPreview`

:   True when the amount range and hit and critical figures are worth drawing.

`public Chance64 HitChance`

:   Odds that the use lands at all, meaningful only while `HasPreview` is true.

`public Fixed64 PreviewMaximum`

:   Highest amount a use that lands can produce. It equals `PreviewMinimum` when the formula has no spread, which is how a caller can decide to print one figure instead of a range.

`public Fixed64 PreviewMinimum`

:   Lowest amount a use that lands can produce. A miss is reported by `HitChance` rather than by this bound, and the value stands for nothing while `HasPreview` is false.

`public StableId SkillId`

:   The skill this value was computed for, so a tray entry can tell whether the tooltip it holds still belongs to the skill it draws.

`public Chance64 StatusChance`

:   Odds that the accompanying status applies. It comes from a separate preview call from the amount figures, so it can be worth drawing even while `HasPreview` is false - a pure status skill has odds but no amount range.

`public string TargetShapeText`

:   The line describing who the skill may be aimed at, worded by the driver. An empty string hides the row.

`public string TimingText`

:   The timing line, worded by the driver. An empty string hides the row.

**Methods**

`public static TooltipData TextOnly()`

:   Builds tooltip text with no numeric preview figures.

---

## TooltipPanelView

```csharp
public sealed class TooltipPanelView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/TooltipPanelView.cs</small>

The skill tooltip: cost, timing, target shape, and the driver-computed
preview figures.

It renders a `TooltipData` value verbatim and calls no preview
or simulation API itself, which is what keeps the UI on the passive side
of the presenter contract.

**Properties**

`public bool IsShown`

:   True while a tooltip is displayed.

**Methods**

`public void Build(CompiledBattleSkin battleSkin)`

:   Builds the panel. Explicit so EditMode tests can drive it.
    - `battleSkin` &mdash; Skin the panel is dressed from; null falls back to the package default. The panel is left hidden.

`public void Hide()`

:   Hides the tooltip.

`public void Show(string title, TooltipData tooltip)`

:   Shows `tooltip` under `title`. Does nothing until `Build` has run.
    - `title` &mdash; Heading text, normally the skill's display name; null shows an empty heading.
    - `tooltip` &mdash; Values the driver already computed. Rows whose text is empty are hidden, the amount range and hit chance appear only when the value carries a preview, and the critical and status chances are each left out while impossible.

---

## TransportBarView

```csharp
public sealed class TransportBarView : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/Regions/TransportBarView.cs</small>

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
    - `battleSkin` &mdash; Skin the bar is dressed from; null falls back to the package default.

`public void SetPaused(bool paused)`

:   Reflects the current pause state on the toggle.
    - `paused` &mdash; The state the host is now in, not the action to offer: true captions the button Resume.

`public void SetScenario(string text)`

:   Sets the displayed scenario name.
    - `text` &mdash; Name to show; null or empty shows a dash rather than a blank gap.

`public void SetSeedText(string text)`

:   Sets the seed field text without raising events.

`public void SetSpeed(float multiplier)`

:   Reflects the current playback speed.
    - `multiplier` &mdash; Visual speed multiplier, captioned as-is with an x suffix. Displaying it is all this does; the host owns the cycle order.

`public void SetStatus(string text)`

:   Sets the status line shown under the controls.

---

## UiStatusEntry

```csharp
public readonly struct UiStatusEntry
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/UI/BattleUiRoot.cs</small>

One combatant's surfaced status-panel row.

**Constructors**

`public UiStatusEntry()`

:   Records one row exactly as the snapshot reported it.

**Properties**

`public StableId CombatantId`

:   Which combatant the row was built from. Look the display name up from this id; the row itself carries no text.

`public int Health`

:   Health exactly as the snapshot reported it; the row itself never interpolates. The roster's health bar eases toward the fraction this implies, and snaps only when the skin scales bar motion to zero, so the drawn bar can trail this value until `BattleUiRoot.Tick` advances it.

`public bool IsDead`

:   True when the snapshot no longer counts the combatant as living. Dead combatants keep their row, so the panel does not reshuffle as a battle thins out.

`public int MaximumHealth`

:   The health ceiling from the same snapshot, for drawing `Health` as a fraction.

`public int Shield`

:   Remaining shield summed over every shield the combatant owns.

`public int StatusCount`

:   How many status entries the snapshot lists for this combatant.

---

