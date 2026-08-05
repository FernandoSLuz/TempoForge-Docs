# Skinning and appearance

17 types in this area.

!!! abstract "On this page"
    [BattleSkinDefaults](#battleskindefaults) &middot; [BattleSkinPreset](#battleskinpreset) &middot; [CompiledBattleSkin](#compiledbattleskin) &middot; [SkinAnchor](#skinanchor) &middot; [SkinBarTokens](#skinbartokens) &middot; [SkinEasing](#skineasing) &middot; [SkinFillMode](#skinfillmode) &middot; [SkinFloatingNumberTokens](#skinfloatingnumbertokens) &middot; [SkinMaterialPool](#skinmaterialpool) &middot; [SkinMotionTokens](#skinmotiontokens) &middot; [SkinPaletteTokens](#skinpalettetokens) &middot; [SkinRegionTokens](#skinregiontokens) &middot; [SkinShape](#skinshape) &middot; [SkinStatusPipTokens](#skinstatuspiptokens) &middot; [SkinSurfaceGraphic](#skinsurfacegraphic) &middot; [SkinSurfaceTokens](#skinsurfacetokens) &middot; [SkinTypographyTokens](#skintypographytokens)

## BattleSkinDefaults

```csharp
public static class BattleSkinDefaults
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinDefaults.cs</small>

The shipped skins, defined in code rather than as serialized assets.

Two reasons. First, the interface always has a complete, valid look even
when a scene assigns no skin asset, so the package never renders as
unstyled boxes. Second, no texture, font, or material is redistributed,
which keeps the provenance audit clean; every look is drawn procedurally
from these numbers.

The Skin Browser materializes any of these into an editable
`BattleSkinPreset` asset via "Duplicate and Edit".

**Fields**

`public float CornerRadius`

:   Corner radius every surface in the look starts from, in reference pixels. Bars clamp it to half their own height, so a generous value rounds a thin bar into a capsule instead of distorting it.

`public const string DefaultSkinId`

:   Identity of the skin loaded when a scene assigns none.

`public SkinFillMode FillMode`

:   Fill treatment for the look's surfaces. The stage backdrop ignores it and always uses a radial gradient, since it is the one surface that has to sit behind everything else.

`public float GlowIntensity`

:   Base glow intensity, scaled by the same fraction as `GlowRadius`. Values above 1 read as bloom without a post-processing stack.

`public float GlowRadius`

:   Base outer glow radius. Each recipe scales it - raised panels, pips, and bar fills take a fraction of it - so a single zero here turns the glow off across the whole look.

`public float GradientSpread`

:   How far the second gradient stop is darkened away from the fill colour. Zero leaves the two stops identical, which makes even a gradient fill read as flat.

`public SkinShape PipShape`

:   Silhouette of the status pips, the one shape that changes from look to look. It also decides whether a pip is given a corner radius at all, since only a rounded rectangle reads one.

`public float ShadowRadius`

:   Base drop-shadow softness. A surface that ends up with a radius of zero is also given a fully transparent shadow colour, so it draws no shadow rather than a hard edge.

`public float StrokeWidth`

:   Border thickness the look's surfaces are stroked with. The stage backdrop is the exception and drops it to zero, since it draws no border behind the rest of the interface.

**Methods**

`public static IReadOnlyList<CompiledBattleSkin> All()`

:   Every shipped skin, in browser order.
    - **Returns** &mdash; The validated result of the operation.

`public static CompiledBattleSkin Default()`

:   The skin used when a scene assigns none.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinFloatingNumberTokens DefaultFloatingNumbers()`

:   Floating-number timing shared by every shipped skin.
    - **Returns** &mdash; The validated result of the operation.

`public static CompiledSkinLayout DefaultLayout()`

:   The region placement shared by every shipped skin.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinMotionTokens DefaultMotion()`

:   Transition timings shared by every shipped skin.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinTypographyTokens DefaultTypography()`

:   Type sizing shared by every shipped skin.
    - **Returns** &mdash; The validated result of the operation.

`public static CompiledBattleSkin MinimalMono()`

:   Light, flat, glowless; the neutral base to customize from.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinPaletteTokens MinimalMonoPalette()`

:   Light, flat, glowless. The neutral base to customize from.
    - **Returns** &mdash; The validated result of the operation.

`public static CompiledBattleSkin NeonCircuit()`

:   Deep indigo with saturated neon rims and heavy halos.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinPaletteTokens NeonCircuitPalette()`

:   Deep indigo with saturated neon rims. The loudest look.
    - **Returns** &mdash; The validated result of the operation.

`public static CompiledBattleSkin ParchmentAtlas()`

:   Warm paper and ink, no glow.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinPaletteTokens ParchmentAtlasPalette()`

:   Warm paper and ink. Suits adventure and campaign framing.
    - **Returns** &mdash; The validated result of the operation.

`public static CompiledBattleSkin Resolve(BattleSkinPreset preset)`

:   Resolves the skin a component should draw with: the assigned asset when present, otherwise the shipped default. Never returns null, so callers need no null branch.
    - `preset` &mdash; The preset value used by this operation.
    - **Returns** &mdash; The validated result of the operation.

`public static CompiledBattleSkin SlateNocturne()`

:   Dark slate with cyan and amber accents.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinSurfaceTokens SlateNocturneBackdrop()`

:   Default-look stage backdrop drawn behind the combatants.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinSurfaceTokens SlateNocturneButton()`

:   Default-look button surface: skill tray, timeline, and transport buttons.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinSurfaceTokens SlateNocturneButtonDisabled()`

:   Default-look button surface for a skill the actor cannot currently use.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinSurfaceTokens SlateNocturneButtonSelected()`

:   Default-look button surface for the selected or hovered entry.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinBarTokens SlateNocturneCastBar()`

:   Default-look cast bar. It carries no delta ghost, since progress only rises.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinBarTokens SlateNocturneGauge()`

:   Default-look scheduler gauge for the combatant plate; no delta ghost either.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinBarTokens SlateNocturneHealthBar()`

:   Default-look health bar for nameplates and roster rows.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinPaletteTokens SlateNocturnePalette()`

:   Dark slate with cyan and amber accents. The default look.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinSurfaceTokens SlateNocturnePanel()`

:   Default-look base panel: status roster, feedback log, timeline backing.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinSurfaceTokens SlateNocturnePanelRaised()`

:   Default-look raised surface: roster rows and the next timeline entry.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinStatusPipTokens SlateNocturnePips()`

:   Default-look status pip strip drawn above each combatant.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinBarTokens SlateNocturneResourceBar()`

:   Default-look resource bar for the actor's spendable pools.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinBarTokens SlateNocturneShieldBar()`

:   Default-look shield bar, drawn thinner than the health bar.
    - **Returns** &mdash; The validated result of the operation.

`public static SkinSurfaceTokens SlateNocturneTooltip()`

:   Default-look tooltip and result banner backing.
    - **Returns** &mdash; The validated result of the operation.

`public static bool TryFind(string stableId, out CompiledBattleSkin skin)`

:   Finds a shipped skin by its stable id.
    - `stableId` &mdash; Id to match exactly; a skin asset's own id is never found here, since only the shipped looks are searched.
    - `skin` &mdash; The matching skin, or null when nothing matches.
    - **Returns** &mdash; True when a shipped skin carries that id.

---

## BattleSkinPreset

:material-star: **Start here**

```csharp
public sealed class BattleSkinPreset : ScriptableObject
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinPreset.cs</small>

Every value the battle interface draws itself with, in one asset.
Duplicate a shipped skin, edit it in the inspector, and the whole HUD
restyles with no prefab surgery and no code changes.

A skin is presentation-only. It never enters a snapshot, a replay, a
state hash, or a compiled catalog, so swapping skins can never change a
battle outcome.

**Properties**

`public string Description`

:   Description shown in the Skin Browser.

`public string DisplayName`

:   Name shown in the Skin Browser.

`public string StableIdText`

:   Persistent skin identity.

**Methods**

`public CompiledBattleSkin Compile()`

:   Resolves this asset into the immutable value set the HUD consumes. Out-of-range authored values are clamped rather than rejected, so a half-edited skin still renders instead of throwing at runtime.
    - **Returns** &mdash; A complete skin, never null. Every token group is copied by value, so editing this asset afterwards does not alter an already-compiled skin.

`public void CopyFrom(CompiledBattleSkin source, string newStableId, string newDisplayName)`

:   Overwrites every field from `source`. Used by "Duplicate and Edit" in the Skin Browser and by the editor tests; it is the only supported way to author a skin from code.
    - `source` &mdash; Values to write in. Required; a null source throws.
    - `newStableId` &mdash; Replacement identity, or null or empty to keep the source's id.
    - `newDisplayName` &mdash; Replacement Skin Browser name, or null or empty to keep the source's name.

---

## CompiledBattleSkin

```csharp
public sealed class CompiledBattleSkin
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinPreset.cs</small>

The immutable skin the HUD reads. Built either from a
`BattleSkinPreset` asset or from `BattleSkinDefaults`
so the interface always has a complete, valid look even when no asset is
assigned.

**Constructors**

`public CompiledBattleSkin()`

:   Assembles a skin from finished token groups. Values are stored exactly as given; clamping is `BattleSkinPreset.Compile`'s job, not this constructor's. A null surface, bar, or layout group throws, because the interface has nothing to fall back to for those.
    - `bars` &mdash; The bars value used by this operation.
    - `description` &mdash; The description value used by this operation.
    - `displayName` &mdash; The display name value used by this operation.
    - `floatingNumbers` &mdash; The floating numbers value used by this operation.
    - `layout` &mdash; The layout value used by this operation.
    - `motion` &mdash; The motion value used by this operation.
    - `palette` &mdash; The palette value used by this operation.
    - `stableIdText` &mdash; The stable id text value used by this operation.
    - `statusPips` &mdash; The status pips value used by this operation.
    - `surfaces` &mdash; The surfaces value used by this operation.
    - `typography` &mdash; The typography value used by this operation.

**Properties**

`public CompiledSkinBars Bars`

:   Styling for the health, shield, resource, cast and scheduler bars. Never null.

`public string Description`

:   The short prose describing the look, shown under the name in the Skin Browser. Empty, never null, when the source supplied none.

`public string DisplayName`

:   The name to list this skin under in a picker. Empty, never null, when the source supplied none.

`public SkinFloatingNumberTokens FloatingNumbers`

:   Size, rise distance and easing for the damage, healing and shield numbers. Their colours come from `FloatingNumberColor` instead, so that damage and healing stay tied to the palette.

`public CompiledSkinLayout Layout`

:   Reference resolution, canvas match, safe-area handling and the position of every HUD region. Never null.

`public SkinMotionTokens Motion`

:   Transition timings for the whole interface. Widgets scale their durations through `SkinMotionTokens.Scale`, which is how a single reduce-motion flag snaps every animation at once instead of each widget deciding for itself.

`public SkinPaletteTokens Palette`

:   The semantic colour roles every widget draws from. Because widgets ask for a role rather than a literal colour, recolouring the whole interface is a change here and nowhere else.

`public string StableIdText`

:   The skin's persistent identity, carried over from the asset it was compiled from. Renaming the asset does not change it, so this is what to record when saving a player's chosen look. Empty, never null, when the source supplied none.

`public SkinStatusPipTokens StatusPips`

:   Size, spacing and stack-count settings for the status pip strip drawn above each combatant.

`public CompiledSkinSurfaces Surfaces`

:   Fills, strokes, glows and shadows for the panels, buttons, tooltip and stage backdrop. Never null.

`public SkinTypographyTokens Typography`

:   Type sizes and treatment. Read the font through `ResolveFont` rather than from here, since an unset font falls back to Unity's built-in one.

**Methods**

`public Color FloatingNumberColor(FloatingNumberStyle style)`

:   The colour a floating number of `style` uses.
    - `style` &mdash; The style value used by this operation.
    - **Returns** &mdash; The validated result of the operation.

`public Font ResolveFont()`

:   The font the skin draws text with, falling back to Unity's built-in runtime font so no third-party font ships with the package.
    - **Returns** &mdash; The validated result of the operation.

---

## SkinAnchor

```csharp
public enum SkinAnchor
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Where a HUD region attaches inside the safe area.

| Value | Meaning |
| --- | --- |
| `TopLeft` | Chooses the top left variant of skin anchor in serialized or canonical state. |
| `TopCenter` | Chooses the top center variant of skin anchor in serialized or canonical state. |
| `TopRight` | Chooses the top right variant of skin anchor in serialized or canonical state. |
| `MiddleLeft` | Chooses the middle left variant of skin anchor in serialized or canonical state. |
| `MiddleCenter` | Chooses the middle center variant of skin anchor in serialized or canonical state. |
| `MiddleRight` | Chooses the middle right variant of skin anchor in serialized or canonical state. |
| `BottomLeft` | Chooses the bottom left variant of skin anchor in serialized or canonical state. |
| `BottomCenter` | Chooses the bottom center variant of skin anchor in serialized or canonical state. |
| `BottomRight` | Chooses the bottom right variant of skin anchor in serialized or canonical state. |

---

## SkinBarTokens

```csharp
public struct SkinBarTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

A value bar: health, shield, resource, cast, or gauge.

**Fields**

`public float CornerRadius`

:   The bar's intended corner radius in reference pixels. What is actually drawn is the radius on `Track` and `Fill`, since those are the surfaces that reach the shader; the shipped bars set all three to the same value, so change them together when reshaping a bar.

`public float DeltaCatchUpSeconds`

:   Seconds the ghost holds at the previous value before catching up. The ghost only appears when the value falls, and this duration passes through `SkinMotionTokens.Scale`, so zero here, a zero `SkinMotionTokens.MotionScale`, or `SkinMotionTokens.ReduceMotion` each suppress it.

`public Color DeltaColor`

:   Colour of the trailing ghost that marks the value just lost.

`public SkinSurfaceTokens Fill`

:   The surface masked to the current value. The trailing ghost is built from it too, recoloured to `DeltaColor` and stripped of its glow. Only the fill colour is cut by the value; a stroke on this surface still traces the whole bar, so use `Track` for the outline and leave the fill's stroke transparent unless that is the look you want.

`public float Height`

:   Bar height in reference pixels. It is also the layout height the bar requests, so the rows around it move when this changes.

`public Color SegmentColor`

:   Colour the tick marks are blended toward. Its alpha controls how strongly they cut in, and a fully transparent colour draws none at all whatever `SegmentCount` says. The ticks go onto both `Track` and `Fill`, so they stay aligned as the value moves.

`public int SegmentCount`

:   Tick marks drawn across the bar. Zero draws one continuous bar.

`public SkinSurfaceTokens Track`

:   The surface drawn across the bar's full width, showing what the value is measured against. It sits behind both the ghost and the fill, so its own glow is largely hidden and its stroke is what gives the bar its outline.

**Methods**

`public SkinBarTokens Sanitized()`

:   Clamps every token into its supported range.
    - **Returns** &mdash; A clamped copy, with `Track` and `Fill` sanitized in turn; this instance is unchanged.

---

## SkinEasing

```csharp
public enum SkinEasing
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

The easing curve applied to a skinned transition.

| Value | Meaning |
| --- | --- |
| `Linear` | Constant rate; no easing. |
| `EaseIn` | Accelerates from rest. |
| `EaseOut` | Decelerates into rest. |
| `EaseInOut` | Accelerates then decelerates. |
| `BackOut` | Overshoots slightly then settles. |

---

## SkinFillMode

```csharp
public enum SkinFillMode
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

How a skinned surface fills its rectangle.

| Value | Meaning |
| --- | --- |
| `Flat` | A single flat colour. |
| `LinearGradient` | A two-stop linear gradient along `SkinSurfaceTokens.GradientAngleDegrees`. |
| `RadialGradient` | A two-stop radial gradient from the surface centre. |

---

## SkinFloatingNumberTokens

```csharp
public struct SkinFloatingNumberTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Rise-and-fade numbers for damage, healing, and shields.

**Fields**

`public float CriticalScale`

:   Multiplies `FontSize` for `FloatingNumberStyle.Critical` only; every other style draws at the base size.

`public int FontSize`

:   Size every number is drawn at before `CriticalScale` is applied. Numbers are drawn on their own world-space canvas over the stage, not in the HUD, so this is independent of `SkinTypographyTokens` and needs to be much larger than body text to read at the same distance.

`public float HorizontalScatter`

:   Horizontal spread in reference pixels so stacked hits stay readable. The offset is derived from the spawn position rather than a random draw, so it never touches RNG the simulation could observe. Zero stacks the numbers.

`public float LifetimeSeconds`

:   Seconds a number stays visible. `SkinMotionTokens.ReduceMotion` caps it at a quarter second rather than removing the number, so a hit is never silent.

`public float RiseDistance`

:   How far a number travels upward from where it was spawned, in reference pixels, over the whole of `LifetimeSeconds`. The number fades out over the second half of that time regardless, so a long rise reads as slower rather than as lingering longer.

`public SkinEasing RiseEasing`

:   Shapes the rise over the number's lifetime. It moves the position only; the fade always runs on the same schedule, so easing changes where the number is when it starts disappearing. `SkinEasing.BackOut` carries the number past `RiseDistance` before settling back, which is worth knowing if the rise is tuned to clear a nameplate exactly.

**Methods**

`public SkinFloatingNumberTokens Sanitized()`

:   Clamps every token into its supported range.
    - **Returns** &mdash; A clamped copy; this instance is unchanged. `RiseEasing` is left as authored.

---

## SkinMaterialPool

```csharp
public sealed class SkinMaterialPool : MonoBehaviour
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/SkinSurfaceGraphic.cs</small>

Reference-counted material pool for skinned surfaces, owned by a component
rather than by static state.

The Presentation assembly forbids static fields that can retain a
`UnityEngine.Object`, because such a cache survives a domain
reload and a scene unload and then hands out destroyed materials. Anchoring
the pool to the canvas root gives every material a real owner: when the
interface goes away, so do its materials.

The shader is loaded from Resources rather than found by name so it
survives build shader stripping without the buyer editing Always Included
Shaders. If it cannot load, callers fall back to the default UI material,
which draws a plain quad instead of a magenta error surface.

**Properties**

`public int CachedMaterialCount`

:   Live cached material count; useful in tests and profiling.

`public bool IsShaderAvailable`

:   True when the skinned-surface shader is available.

**Fields**

`public const string ShaderName`

:   Shader name, used as a secondary lookup.

`public const string ShaderResourcePath`

:   Resources path of the skinned-surface shader.

**Methods**

`public Material Acquire(SkinMaterialRequest request)`

:   Returns a material for `request`, sharing an existing one when the parameters match exactly.
    - `request` &mdash; The immutable request to validate and execute.
    - **Returns** &mdash; The validated result of the operation.

`public void Clear()`

:   Destroys every pooled material. Safe to call repeatedly.

`public static SkinMaterialPool EnsureFor(Component owner)`

:   Finds the pool owning `owner`, creating one on the nearest canvas root when absent. Returns null only when the owner is not in a scene.
    - `owner` &mdash; The owner value used by this operation.
    - **Returns** &mdash; The validated result of the operation.

`public void Release(Material material)`

:   Drops one reference to a pooled material.
    - `material` &mdash; The material value used by this operation.

---

## SkinMotionTokens

```csharp
public struct SkinMotionTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Transition timings. Every duration scales by `MotionScale`.

**Fields**

`public SkinEasing BarEasing`

:   Shapes that travel. It applies to the fill only; the ghost behind it always catches up at a constant rate, which is what keeps the gap between the two readable.

`public float BarTransitionSeconds`

:   How long a bar takes to travel to a new value, before scaling. Once `Scale` reduces it to zero the bar snaps instead, and the trailing ghost is skipped with it, so a reduced-motion player sees the new value but not the amount just lost.

`public float MotionScale`

:   Multiplies every duration handed out by `Scale`. Zero snaps every change instantly.

`public float PanelFadeSeconds`

:   How long a panel takes to fade in, before scaling. The result banner uses it; at zero the banner appears at full opacity on the frame it is shown rather than never appearing.

`public float PipPopSeconds`

:   How long a status pip takes to pop in, before scaling. Offered for hosts that animate their own pip strip; the shipped combatant plate adds and removes pips outright and does not read it.

`public float PulseScale`

:   Scale a combatant token reaches at the peak of a pulse. The pulse rises and falls within `PulseSeconds`, so this is a peak rather than a resting size and a token is never left enlarged. Values close to 1 still register: the shipped Minimal Mono skin pulses at 1.04.

`public float PulseSeconds`

:   How long a whole pulse takes, out and back, before scaling. Once `Scale` reduces it to zero the token is returned to its rest scale immediately, so a pulse requested under reduced motion cannot leave a token stuck at `PulseScale`.

`public bool ReduceMotion`

:   Skip decorative motion. `Scale` then returns zero for every duration, so values snap instead of animating, while floating numbers stay briefly visible so nothing is missed. Drive this from a player accessibility setting.

`public float TimelineShiftSeconds`

:   How long the timeline takes to settle after the running order changes, before scaling. Offered for hosts that animate their own timeline; the shipped strip repaints in place and does not read it.

**Methods**

`public static float Ease(SkinEasing easing, float t)`

:   Maps a normalized 0..1 progress value through the selected easing curve. Input and output are clamped for presentation use only.
    - `t` &mdash; Progress from 0 to 1; anything outside that range is clamped first.
    - `easing` &mdash; The easing value used by this operation.
    - **Returns** &mdash; Eased progress. Every curve stays within 0..1 except `SkinEasing.BackOut`, which rises above 1 near the end and is what gives it its overshoot, so a caller that lerps with this result must tolerate values past the target.

`public SkinMotionTokens Sanitized()`

:   Clamps every token into its supported range.
    - **Returns** &mdash; A clamped copy; this instance is unchanged. `ReduceMotion` and `BarEasing` are left as authored.

`public float Scale(float seconds)`

:   The effective duration for `seconds` under this skin.
    - `seconds` &mdash; The unscaled duration the animation would like.
    - **Returns** &mdash; `seconds` multiplied by `MotionScale`, never negative, and zero whenever `ReduceMotion` is set. Treat a zero result as an instruction to snap rather than animate.

---

## SkinPaletteTokens

```csharp
public struct SkinPaletteTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

The semantic colour roles a skin assigns once and reuses everywhere.

**Fields**

`public Color Accent`

:   The colour the interface uses to point at something: the selected skill button and its glow, the next timeline entry, status pips, and the scheduler gauge while it fills. It appears more often than any other accent, so it is the single value that most changes a skin's character.

`public Color AccentAlt`

:   Secondary accent. The cast bar, the resource bar, and resource floating numbers use it.

`public Color AllyTeam`

:   Tints the name plate of a combatant on the player's team. The stage decides which team that is by matching each team against the player team id it was given, so with no player team set every combatant is tinted `EnemyTeam` instead.

`public Color Background`

:   The colour behind everything else. The shipped skins build the stage backdrop as a radial gradient from it to a darker shade of itself, and reuse it for the empty part of a bar track and for segment ticks, so it sets how deep the HUD reads overall rather than only the scene edges.

`public Color Border`

:   The stroke colour panels and bars fall back to when nothing more specific applies. A selected or focused widget swaps it for `Accent`, which is what makes selection read at a glance.

`public Color EnemyTeam`

:   Tints the name plate of every combatant not on the player's team. Only the plate label takes the tint; bars keep the colours the skin gave them, so health still reads the same on both sides of the field.

`public Color Negative`

:   Reads as bad news: damage numbers and the defeat banner.

`public Color Positive`

:   Reads as good news: healing numbers, the health bar, and the victory banner.

`public Color Shield`

:   Shield and barrier amounts: the shield bar, shield numbers, and a roster row that is holding shield.

`public Color Surface`

:   The resting colour of a HUD panel. Its alpha is carried through to the panel surface, so a translucent value lets the stage read through the interface; the tooltip surface forces the same colour opaque so text over a busy stage stays legible.

`public Color SurfaceRaised`

:   The colour that lifts something out of a panel: a roster row, a skill button, the next timeline entry, and the +N overflow status pip all use it, so it needs enough contrast against `Surface` to be read as a state change rather than as decoration.

`public Color TextMuted`

:   The recessive text colour: a dead combatant's name, the target caption under a skill button, the tooltip's target row, and the order number of timeline entries that are not next. It still has to be read, so keep it clearly distinguishable from `TextSecondary`.

`public Color TextPrimary`

:   The colour of anything the player is meant to read first: combatant names, headline text, bar readouts, and floating numbers that carry no semantic colour of their own.

`public Color TextSecondary`

:   The colour of text that supports a primary label rather than competing with it: log lines, the tooltip's chance and timing rows, and roster detail. The tooltip's cost row is drawn in `AccentAlt` instead, so a price still reads as its own thing.

`public Color Warning`

:   Reads as caution: critical-hit numbers and the concession banner.

---

## SkinRegionTokens

```csharp
public struct SkinRegionTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Where one HUD region sits. Every region is independently placeable so a
customer can move the whole interface without editing a prefab.

**Fields**

`public SkinAnchor Anchor`

:   The point of the safe area the region hangs from. It becomes the region's anchor and its pivot at once, so the region grows away from that corner and stays put on screens of any aspect. `Offset` is then measured inward from it.

`public Vector2 Offset`

:   Distance from the anchor in reference pixels, always measured inward, so the same numbers keep their meaning when the region is re-anchored to another corner. See `InwardOffset` for the signed form a RectTransform wants.

`public float Scale`

:   Extra scale for this region alone. Zero or negative is read as 1, so an unset value never scales a region out of sight.

`public Vector2 Size`

:   Region size in reference pixels. Zero on an axis leaves that axis alone, so the region sizes to its content.

`public bool Visible`

:   Whether the interface builds this region. A hidden region is never created rather than created and disabled, so switching it off costs nothing at runtime and its view is simply skipped when the interface repaints. This is how a host drops a block of the HUD it does not want without editing a prefab.

**Methods**

`public static Vector2 AnchorPoint(SkinAnchor anchor)`

:   The normalized anchor point for `anchor`.
    - `anchor` &mdash; The anchor value used by this operation.
    - **Returns** &mdash; The matching point with (0,0) at the bottom left and (1,1) at the top right, ready to use as a RectTransform anchor and pivot. A value outside the enum falls back to the bottom right.

`public static SkinRegionTokens At(SkinAnchor anchor, Vector2 offset, Vector2 size)`

:   A visible region anchored at `anchor`.
    - `offset` &mdash; Inward distance from the anchor in reference pixels.
    - `size` &mdash; Size in reference pixels; zero on an axis sizes to content.
    - `anchor` &mdash; The anchor value used by this operation.
    - **Returns** &mdash; A visible region at scale 1.

`public Vector2 InwardOffset()`

:   Converts `Offset` into a signed anchored position so positive values always move a region inward from its anchor.
    - **Returns** &mdash; `Offset` with its sign flipped on each axis whose anchor sits at the far edge. A centred axis keeps the raw value, where positive still means right and up.

`public SkinRegionTokens Sanitized()`

:   Clamps every token into its supported range.
    - **Returns** &mdash; A clamped copy; this instance is unchanged. A zero or negative `Scale` becomes 1, and a negative `Size` axis becomes zero.

---

## SkinShape

```csharp
public enum SkinShape
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

The silhouette a skinned surface draws.

| Value | Meaning |
| --- | --- |
| `RoundedRect` | A rounded rectangle honouring the corner radius. |
| `Circle` | A circle inscribed in the shorter rectangle axis. |
| `Capsule` | A capsule: fully rounded on the shorter axis. |
| `Hexagon` | A hexagon inscribed in the rectangle. |
| `Diamond` | A diamond inscribed in the rectangle. |

---

## SkinStatusPipTokens

```csharp
public struct SkinStatusPipTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

The status pip strip drawn above a combatant.

**Fields**

`public int MaximumVisible`

:   Pips drawn before the strip overflows. Past this many statuses the last visible pip becomes a +N pip counting the ones not shown, so the strip never grows wider than this.

`public bool ShowStackCounts`

:   Allows a count to be drawn inside a pip. On the shipped combatant plate only the overflow pip carries one, reading +N for every status the strip has no pip of its own for. The overflow pip takes the place of the last visible one, so N runs one higher than the count past `MaximumVisible`. Turning this off leaves that pip blank, so the strip still shows that something is hidden but not how much.

`public float Size`

:   Edge length of one pip in reference pixels. It also fixes the height of the strip and the size of the stack-count digits, which are derived from it, so a small pip stays legible rather than carrying unreadable text.

`public float Spacing`

:   Gap between neighbouring pips in reference pixels. It widens the strip without widening the pips, so together with `Size` and `MaximumVisible` it decides how much room the strip takes above a combatant.

`public SkinSurfaceTokens Surface`

:   Pip surface. Its shape, stroke, and glow are drawn as authored, but the fill is replaced when the pip is drawn: `SkinPaletteTokens.Accent` for a status pip, `SkinPaletteTokens.SurfaceRaised` for the overflow pip.

**Methods**

`public SkinStatusPipTokens Sanitized()`

:   Clamps every token into its supported range.
    - **Returns** &mdash; A clamped copy, with `Surface` sanitized in turn; this instance is unchanged.

---

## SkinSurfaceGraphic

```csharp
public sealed class SkinSurfaceGraphic : MaskableGraphic
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/SkinSurfaceGraphic.cs</small>

Draws one `SkinSurfaceTokens` as a uGUI graphic through the
TurnGauge skinned-surface shader. Every panel, button, bar, gauge, and
status pip in the HUD is one of these, so restyling the interface means
changing token values rather than swapping prefabs or textures.

The mesh is padded beyond the layout rect so glow and shadow can bleed
outside the shape without being clipped. Padding is excluded from layout,
so a glowing widget still occupies exactly its `RectTransform`.

**Properties**

`public float FillAmount`

:   Filled fraction in [0,1]. Bars and gauges animate this; other surfaces leave it at 1.

`public bool FillVertical`

:   True when `FillAmount` runs bottom-to-top.

`public float Padding`

:   Padding in reference pixels added around the rect so glow and shadow are not clipped by the quad.

`public SkinSurfaceTokens Surface`

:   The surface tokens this graphic draws.

**Methods**

`public void Apply(SkinSurfaceTokens value)`

:   Updates apply on presentation state only. The call cannot submit a command, advance a tick, or change an authoritative hash.
    - `value` &mdash; The value to validate and apply.

`public void ApplySegments(int count, Color color)`

:   Applies segment ticks, used by segmented bars.
    - `color` &mdash; The color value used by this operation.
    - `count` &mdash; The number of values or operations requested.

`public void SetFillColors(Color primary, Color secondary)`

:   Replaces only the fill colours, keeping shape and glow.
    - `primary` &mdash; The primary value used by this operation.
    - `secondary` &mdash; The secondary value used by this operation.

`public void SetGlow(Color color, float radius, float intensity)`

:   Replaces only the glow, keeping shape and fill.
    - `color` &mdash; The color value used by this operation.
    - `intensity` &mdash; The intensity value used by this operation.
    - `radius` &mdash; The radius value used by this operation.

---

## SkinSurfaceTokens

```csharp
public struct SkinSurfaceTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Fill, stroke, and glow for one skinned surface. Every skinned widget
resolves to one of these, so a customer restyles the whole HUD by editing
a handful of surfaces rather than hunting individual prefabs.

**Fields**

`public float CornerRadius`

:   Corner radius in reference pixels. Only `SkinShape.RoundedRect` reads it, and the shader clamps it to half the shorter axis, so an over-large value settles into a capsule instead of distorting the shape.

`public Color FillColor`

:   The near gradient stop, and the entire fill under `SkinFillMode.Flat`. A linear gradient starts from it at the leading edge and a radial gradient starts from it at the centre, so this is the colour a surface reads as whichever fill mode is chosen.

`public Color FillColorSecondary`

:   The far gradient stop. `SkinFillMode.Flat` ignores it and draws `FillColor` alone.

`public SkinFillMode FillMode`

:   Carries fill mode for SkinSurfaceTokens with explicit ownership and deterministic validation semantics. It does not discover project or scene state.

`public Color GlowColor`

:   Halo colour. Its alpha is one of the three switches on the glow, so a fully transparent colour suppresses the halo however generous `GlowRadius` and `GlowIntensity` are. The halo falls off outside the silhouette only, so it never washes out the fill.

`public float GlowIntensity`

:   Multiplies the glow mask. A glow needs a non-zero `GlowRadius`, a non-zero intensity, and a `GlowColor` carrying alpha before anything is drawn at all; values above 1 widen the solid core of the halo, which reads as bloom without a post-processing stack.

`public float GlowRadius`

:   How far the halo reaches beyond the silhouette, in reference pixels. The mesh is padded by this distance so the halo is not clipped by the quad, and the padding is excluded from layout, so a widget that glows still occupies exactly its RectTransform and does not push its neighbours around.

`public float GradientAngleDegrees`

:   Direction of a `SkinFillMode.LinearGradient` fill, in degrees anticlockwise from screen right: 0 runs `FillColor` to `FillColorSecondary` left to right, 90 runs bottom to top. The flat and radial modes ignore it.

`public Color ShadowColor`

:   Drop-shadow colour. Its alpha both gates and scales the shadow: a fully transparent colour draws nothing whatever `ShadowRadius` and `ShadowOffset` say, and it is also what stops a shadowless surface from paying for shadow padding.

`public Vector2 ShadowOffset`

:   Displacement of the shadow from the surface in reference pixels, with positive x to the right and positive y upward. The offset is added to `ShadowRadius` when the mesh is padded, so a far-thrown shadow is drawn in full rather than cut off at the quad edge.

`public float ShadowRadius`

:   Drop-shadow softness in reference pixels. Zero, or a fully transparent `ShadowColor`, draws no shadow.

`public SkinShape Shape`

:   The silhouette every part of the surface is measured against: fill, stroke, glow, and shadow all follow it. The shape is cut from a signed distance field inside the shader rather than built from geometry, so switching shapes costs no extra vertices and needs no sprite or mask.

`public Color StrokeColor`

:   Border colour. It is drawn over the fill as a band hugging the inside of the silhouette, and it is not masked by a partial fill, so a bar built on a stroked surface keeps a complete outline however low its value runs.

`public float StrokeWidth`

:   Border thickness in reference pixels, drawn inside the silhouette so it never enlarges the surface. Zero, or a fully transparent `StrokeColor`, draws no border.

**Methods**

`public static SkinSurfaceTokens Flat(Color fill, float cornerRadius = 0f)`

:   A flat, strokeless, glowless surface in `fill`.
    - `cornerRadius` &mdash; Corner radius in reference pixels; zero gives square corners.
    - `fill` &mdash; The fill value used by this operation.
    - **Returns** &mdash; A rounded-rect surface with no stroke, glow, or shadow, ready to be built on.

`public SkinSurfaceTokens Sanitized()`

:   Clamps every token into its supported range.
    - **Returns** &mdash; A clamped copy; this instance is unchanged. `GradientAngleDegrees` wraps into 0..360 rather than clamping, and the colours are left exactly as authored.

`public SkinSurfaceTokens WithFill(Color fill)`

:   Returns this surface with its fill replaced by `fill`.
    - `fill` &mdash; The fill value used by this operation.
    - **Returns** &mdash; A copy with both gradient stops set to `fill`, so a gradient surface reads as flat until a second stop is set again.

`public SkinSurfaceTokens WithGlow(Color color, float radius, float intensity)`

:   Returns this surface with its glow replaced.
    - `radius` &mdash; Glow radius in reference pixels, measured outward from the silhouette.
    - `intensity` &mdash; Glow strength; above 1 the halo reads as bloom.
    - `color` &mdash; The color value used by this operation.
    - **Returns** &mdash; A copy carrying the new glow. The values are stored as given, so call `Sanitized` if they came from outside the supported ranges.

---

## SkinTypographyTokens

```csharp
public struct SkinTypographyTokens
```

`TurnGauge.Presentation` &middot; <small>TurnGauge/Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Type sizing and treatment. Fonts stay optional so no font is redistributed.

**Fields**

`public int BodySize`

:   Size of the interface's ordinary text: roster names, skill names, and the tooltip's damage preview.

`public int CaptionSize`

:   Size of small supporting text, and the busiest of the three sizes: it covers combatant plates, bar readouts, log lines, timeline entries, and tooltip cost and timing rows. Several regions derive their row heights from it, so raising it grows those rows rather than overflowing them.

`public Font Font`

:   Optional font. Left empty, the skin falls back to Unity's built-in runtime font, so a skin never depends on a font asset the package would have to redistribute.

`public int HeadingSize`

:   Size of titles. The result banner scales it up further for its headline, so a large value here grows the end-of-battle text faster than it grows a tooltip title.

`public float LineSpacing`

:   Multiplies the gap between lines of a wrapped label. Most HUD text is a single line, so this mainly affects the feedback log and tooltip body.

`public Color OutlineColor`

:   Colour of that outline. It is read only while `UseOutline` is set, and it should oppose the text colour rather than match the panel behind it: the shipped dark skins outline in black, the neon skin in its own near-black backdrop colour.

`public bool UseOutline`

:   Adds a one-pixel contrast outline to every label the skin builds, which is what keeps text readable where it sits directly over the stage. The outline is attached when a label is created, so a skin swapped at runtime applies it on the rebuild rather than to labels already on screen. The two light shipped skins leave it off; their text is already dark against pale panels.

**Methods**

`public SkinTypographyTokens Sanitized()`

:   Clamps every token into its supported range.
    - **Returns** &mdash; A clamped copy; this instance is unchanged. `Font`, `UseOutline`, and `OutlineColor` are left as authored.

---

