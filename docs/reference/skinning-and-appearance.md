# Skinning and appearance

21 types in this area.

!!! abstract "On this page"
    [BattleSkinDefaults](#battleskindefaults) &middot; [BattleSkinPreset](#battleskinpreset) &middot; [CompiledBattleSkin](#compiledbattleskin) &middot; [CompiledSkinBars](#compiledskinbars) &middot; [CompiledSkinLayout](#compiledskinlayout) &middot; [CompiledSkinSurfaces](#compiledskinsurfaces) &middot; [SkinAnchor](#skinanchor) &middot; [SkinBarTokens](#skinbartokens) &middot; [SkinEasing](#skineasing) &middot; [SkinFillMode](#skinfillmode) &middot; [SkinFloatingNumberTokens](#skinfloatingnumbertokens) &middot; [SkinMaterialPool](#skinmaterialpool) &middot; [SkinMaterialRequest](#skinmaterialrequest) &middot; [SkinMotionTokens](#skinmotiontokens) &middot; [SkinPaletteTokens](#skinpalettetokens) &middot; [SkinRegionTokens](#skinregiontokens) &middot; [SkinShape](#skinshape) &middot; [SkinStatusPipTokens](#skinstatuspiptokens) &middot; [SkinSurfaceGraphic](#skinsurfacegraphic) &middot; [SkinSurfaceTokens](#skinsurfacetokens) &middot; [SkinTypographyTokens](#skintypographytokens)

## BattleSkinDefaults

```csharp
public static class BattleSkinDefaults
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinDefaults.cs</small>

The shipped skins, defined in code rather than as serialized assets.

Two reasons. First, the interface always has a complete, valid look even
when a scene assigns no skin asset, so the package never renders as
unstyled boxes. Second, no texture, font, or material is redistributed,
which keeps the provenance audit clean; every look is drawn procedurally
from these numbers.

The Skin Browser materializes any of these into an editable
`attleSkinPreset` asset via "Duplicate and Edit".

**Fields**

`public float CornerRadius`

:   &mdash;

`public SkinFillMode FillMode`

:   &mdash;

`public float GlowIntensity`

:   &mdash;

`public float GlowRadius`

:   &mdash;

`public float GradientSpread`

:   &mdash;

`public SkinShape PipShape`

:   &mdash;

`public float ShadowRadius`

:   &mdash;

`public float StrokeWidth`

:   &mdash;

**Methods**

`public static IReadOnlyList<CompiledBattleSkin> All()`

:   Every shipped skin, in browser order.

`public static CompiledBattleSkin Default()`

:   The skin used when a scene assigns none.

`public static SkinFloatingNumberTokens DefaultFloatingNumbers()`

:   Floating-number timing shared by every shipped skin.

`public static CompiledSkinLayout DefaultLayout()`

:   The region placement shared by every shipped skin.

`public static SkinMotionTokens DefaultMotion()`

:   Transition timings shared by every shipped skin.

`public static SkinTypographyTokens DefaultTypography()`

:   Type sizing shared by every shipped skin.

`public static CompiledBattleSkin MinimalMono()`

:   Light, flat, glowless; the neutral base to customize from.

`public static SkinPaletteTokens MinimalMonoPalette()`

:   Light, flat, glowless. The neutral base to customize from.

`public static CompiledBattleSkin NeonCircuit()`

:   Deep indigo with saturated neon rims and heavy halos.

`public static SkinPaletteTokens NeonCircuitPalette()`

:   Deep indigo with saturated neon rims. The loudest look.

`public static CompiledBattleSkin ParchmentAtlas()`

:   Warm paper and ink, no glow.

`public static SkinPaletteTokens ParchmentAtlasPalette()`

:   Warm paper and ink. Suits adventure and campaign framing.

`public static CompiledBattleSkin Resolve(BattleSkinPreset preset)`

:   Resolves the skin a component should draw with: the assigned asset when present, otherwise the shipped default. Never returns null, so callers need no null branch.

`public static CompiledBattleSkin SlateNocturne()`

:   Dark slate with cyan and amber accents.

`public static SkinSurfaceTokens SlateNocturneBackdrop()`

:   &mdash;

`public static SkinSurfaceTokens SlateNocturneButton()`

:   &mdash;

`public static SkinSurfaceTokens SlateNocturneButtonDisabled()`

:   &mdash;

`public static SkinSurfaceTokens SlateNocturneButtonSelected()`

:   &mdash;

`public static SkinBarTokens SlateNocturneCastBar()`

:   &mdash;

`public static SkinBarTokens SlateNocturneGauge()`

:   &mdash;

`public static SkinBarTokens SlateNocturneHealthBar()`

:   &mdash;

`public static SkinPaletteTokens SlateNocturnePalette()`

:   Dark slate with cyan and amber accents. The default look.

`public static SkinSurfaceTokens SlateNocturnePanel()`

:   &mdash;

`public static SkinSurfaceTokens SlateNocturnePanelRaised()`

:   &mdash;

`public static SkinStatusPipTokens SlateNocturnePips()`

:   &mdash;

`public static SkinBarTokens SlateNocturneResourceBar()`

:   &mdash;

`public static SkinBarTokens SlateNocturneShieldBar()`

:   &mdash;

`public static SkinSurfaceTokens SlateNocturneTooltip()`

:   &mdash;

`public static bool TryFind(string stableId, out CompiledBattleSkin skin)`

:   Finds a shipped skin by its stable id.

---

## BattleSkinPreset

```csharp
public sealed class BattleSkinPreset : ScriptableObject
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinPreset.cs</small>

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

`public void CopyFrom(CompiledBattleSkin source, string newStableId, string newDisplayName)`

:   Overwrites every field from `source`. Used by "Duplicate and Edit" in the Skin Browser and by the editor tests; it is the only supported way to author a skin from code.

---

## CompiledBattleSkin

```csharp
public sealed class CompiledBattleSkin
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinPreset.cs</small>

The immutable skin the HUD reads. Built either from a
`attleSkinPreset` asset or from `attleSkinDefaults`
so the interface always has a complete, valid look even when no asset is
assigned.

**Constructors**

`public CompiledBattleSkin()`

:   &mdash;

**Properties**

`public CompiledSkinBars Bars`

:   &mdash;

`public string Description`

:   &mdash;

`public string DisplayName`

:   &mdash;

`public SkinFloatingNumberTokens FloatingNumbers`

:   &mdash;

`public CompiledSkinLayout Layout`

:   &mdash;

`public SkinMotionTokens Motion`

:   &mdash;

`public SkinPaletteTokens Palette`

:   &mdash;

`public string StableIdText`

:   &mdash;

`public SkinStatusPipTokens StatusPips`

:   &mdash;

`public CompiledSkinSurfaces Surfaces`

:   &mdash;

`public SkinTypographyTokens Typography`

:   &mdash;

**Methods**

`public Color FloatingNumberColor(FloatingNumberStyle style)`

:   The colour a floating number of `style` uses.

`public Font ResolveFont()`

:   The font the skin draws text with, falling back to Unity's built-in runtime font so no third-party font ships with the package.

---

## CompiledSkinBars

```csharp
public sealed class CompiledSkinBars
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinPreset.cs</small>

The resolved bar set for one skin.

**Constructors**

`public CompiledSkinBars()`

:   &mdash;

**Properties**

`public SkinBarTokens Cast`

:   &mdash;

`public SkinBarTokens Health`

:   &mdash;

`public SkinBarTokens Resource`

:   &mdash;

`public SkinBarTokens SchedulerGauge`

:   &mdash;

`public SkinBarTokens Shield`

:   &mdash;

---

## CompiledSkinLayout

```csharp
public sealed class CompiledSkinLayout
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinPreset.cs</small>

The resolved layout and region set for one skin.

**Constructors**

`public CompiledSkinLayout()`

:   &mdash;

**Properties**

`public SkinRegionTokens Feedback`

:   &mdash;

`public float MatchWidthOrHeight`

:   &mdash;

`public Vector2 ReferenceResolution`

:   &mdash;

`public SkinRegionTokens Result`

:   &mdash;

`public SkinRegionTokens SkillTray`

:   &mdash;

`public SkinRegionTokens Status`

:   &mdash;

`public SkinRegionTokens Timeline`

:   &mdash;

`public SkinRegionTokens Tooltip`

:   &mdash;

`public SkinRegionTokens Transport`

:   &mdash;

`public bool UseSafeArea`

:   &mdash;

---

## CompiledSkinSurfaces

```csharp
public sealed class CompiledSkinSurfaces
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinPreset.cs</small>

The resolved surface set for one skin.

**Constructors**

`public CompiledSkinSurfaces()`

:   &mdash;

**Properties**

`public SkinSurfaceTokens Button`

:   &mdash;

`public SkinSurfaceTokens ButtonDisabled`

:   &mdash;

`public SkinSurfaceTokens ButtonSelected`

:   &mdash;

`public SkinSurfaceTokens Panel`

:   &mdash;

`public SkinSurfaceTokens PanelRaised`

:   &mdash;

`public SkinSurfaceTokens StageBackdrop`

:   &mdash;

`public SkinSurfaceTokens Tooltip`

:   &mdash;

---

## SkinAnchor

```csharp
public enum SkinAnchor
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Where a HUD region attaches inside the safe area.

| Value | Meaning |
| --- | --- |
| `TopLeft` | &mdash; |
| `TopCenter` | &mdash; |
| `TopRight` | &mdash; |
| `MiddleLeft` | &mdash; |
| `MiddleCenter` | &mdash; |
| `MiddleRight` | &mdash; |
| `BottomLeft` | &mdash; |
| `BottomCenter` | &mdash; |
| `BottomRight` | &mdash; |

---

## SkinBarTokens

```csharp
public struct SkinBarTokens
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

A value bar: health, shield, resource, cast, or gauge.

**Fields**

`public float CornerRadius`

:   &mdash;

`public float DeltaCatchUpSeconds`

:   &mdash;

`public Color DeltaColor`

:   &mdash;

`public SkinSurfaceTokens Fill`

:   &mdash;

`public float Height`

:   &mdash;

`public Color SegmentColor`

:   &mdash;

`public int SegmentCount`

:   &mdash;

`public SkinSurfaceTokens Track`

:   &mdash;

**Methods**

`public SkinBarTokens Sanitized()`

:   Clamps every token into its supported range.

---

## SkinEasing

```csharp
public enum SkinEasing
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

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

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

How a skinned surface fills its rectangle.

| Value | Meaning |
| --- | --- |
| `Flat` | A single flat colour. |
| `LinearGradient` | A two-stop linear gradient along `kinSurfaceTokens.GradientAngleDegrees`. |
| `RadialGradient` | A two-stop radial gradient from the surface centre. |

---

## SkinFloatingNumberTokens

```csharp
public struct SkinFloatingNumberTokens
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Rise-and-fade numbers for damage, healing, and shields.

**Fields**

`public float CriticalScale`

:   &mdash;

`public int FontSize`

:   &mdash;

`public float HorizontalScatter`

:   &mdash;

`public float LifetimeSeconds`

:   &mdash;

`public float RiseDistance`

:   &mdash;

`public SkinEasing RiseEasing`

:   &mdash;

**Methods**

`public SkinFloatingNumberTokens Sanitized()`

:   Clamps every token into its supported range.

---

## SkinMaterialPool

```csharp
public sealed class SkinMaterialPool : MonoBehaviour
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/SkinSurfaceGraphic.cs</small>

Reference-counted material pool for skinned surfaces, owned by a component
rather than by static state.

The Presentation assembly forbids static fields that can retain a
`nityEngine.Object`, because such a cache survives a domain
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

**Methods**

`public Material Acquire(SkinMaterialRequest request)`

:   Returns a material for `request`, sharing an existing one when the parameters match exactly.

`public void Clear()`

:   Destroys every pooled material. Safe to call repeatedly.

`public static SkinMaterialPool EnsureFor(Component owner)`

:   Finds the pool owning `owner`, creating one on the nearest canvas root when absent. Returns null only when the owner is not in a scene.

`public void Release(Material material)`

:   Drops one reference to a pooled material.

---

## SkinMaterialRequest

```csharp
public readonly struct SkinMaterialRequest
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/SkinSurfaceGraphic.cs</small>

The full parameter set for one skinned-surface material. Two widgets with
identical parameters share a material and therefore batch together, which
keeps a HUD of repeated pips and bars cheap.

**Constructors**

`public SkinMaterialRequest()`

:   &mdash;

**Properties**

`public Vector2 Extent`

:   &mdash;

`public float FillAmount`

:   &mdash;

`public bool FillVertical`

:   &mdash;

`public Color SegmentColor`

:   &mdash;

`public int SegmentCount`

:   &mdash;

`public Vector2 Size`

:   &mdash;

`public SkinSurfaceTokens Surface`

:   &mdash;

**Methods**

`public void ApplyTo(Material material)`

:   Writes every request value onto a material.

`public string Key()`

:   A stable key over every value that reaches the material. Sizes are quantized to whole pixels and fill to 1/256 so a bar animating smoothly does not allocate a new material every frame.

---

## SkinMotionTokens

```csharp
public struct SkinMotionTokens
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Transition timings. Every duration scales by `otionScale`.

**Fields**

`public SkinEasing BarEasing`

:   &mdash;

`public float BarTransitionSeconds`

:   &mdash;

`public float MotionScale`

:   &mdash;

`public float PanelFadeSeconds`

:   &mdash;

`public float PipPopSeconds`

:   &mdash;

`public float PulseScale`

:   &mdash;

`public float PulseSeconds`

:   &mdash;

`public bool ReduceMotion`

:   &mdash;

`public float TimelineShiftSeconds`

:   &mdash;

**Methods**

`public static float Ease(SkinEasing easing, float t)`

:   Evaluates `easing` at normalized time `t`.

`public SkinMotionTokens Sanitized()`

:   Clamps every token into its supported range.

`public float Scale(float seconds)`

:   The effective duration for `seconds` under this skin.

---

## SkinPaletteTokens

```csharp
public struct SkinPaletteTokens
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

The semantic colour roles a skin assigns once and reuses everywhere.

**Fields**

`public Color Accent`

:   &mdash;

`public Color AccentAlt`

:   &mdash;

`public Color AllyTeam`

:   &mdash;

`public Color Background`

:   &mdash;

`public Color Border`

:   &mdash;

`public Color EnemyTeam`

:   &mdash;

`public Color Negative`

:   &mdash;

`public Color Positive`

:   &mdash;

`public Color Shield`

:   &mdash;

`public Color Surface`

:   &mdash;

`public Color SurfaceRaised`

:   &mdash;

`public Color TextMuted`

:   &mdash;

`public Color TextPrimary`

:   &mdash;

`public Color TextSecondary`

:   &mdash;

`public Color Warning`

:   &mdash;

---

## SkinRegionTokens

```csharp
public struct SkinRegionTokens
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Where one HUD region sits. Every region is independently placeable so a
customer can move the whole interface without editing a prefab.

**Fields**

`public SkinAnchor Anchor`

:   &mdash;

`public Vector2 Offset`

:   &mdash;

`public float Scale`

:   &mdash;

`public Vector2 Size`

:   &mdash;

`public bool Visible`

:   &mdash;

**Methods**

`public static Vector2 AnchorPoint(SkinAnchor anchor)`

:   The normalized anchor point for `anchor`.

`public static SkinRegionTokens At(SkinAnchor anchor, Vector2 offset, Vector2 size)`

:   A visible region anchored at `anchor`.

`public Vector2 InwardOffset()`

:   Converts `ffset` into a signed anchored position so positive values always move a region inward from its anchor.

`public SkinRegionTokens Sanitized()`

:   Clamps every token into its supported range.

---

## SkinShape

```csharp
public enum SkinShape
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

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

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

The status pip strip drawn above a combatant.

**Fields**

`public int MaximumVisible`

:   &mdash;

`public bool ShowStackCounts`

:   &mdash;

`public float Size`

:   &mdash;

`public float Spacing`

:   &mdash;

`public SkinSurfaceTokens Surface`

:   &mdash;

**Methods**

`public SkinStatusPipTokens Sanitized()`

:   Clamps every token into its supported range.

---

## SkinSurfaceGraphic

```csharp
public sealed class SkinSurfaceGraphic : MaskableGraphic
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/SkinSurfaceGraphic.cs</small>

Draws one `kinSurfaceTokens` as a uGUI graphic through the
TempoForge skinned-surface shader. Every panel, button, bar, gauge, and
status pip in the HUD is one of these, so restyling the interface means
changing token values rather than swapping prefabs or textures.

The mesh is padded beyond the layout rect so glow and shadow can bleed
outside the shape without being clipped. Padding is excluded from layout,
so a glowing widget still occupies exactly its `ectTransform`.

**Properties**

`public float FillAmount`

:   Filled fraction in [0,1]. Bars and gauges animate this; other surfaces leave it at 1.

`public bool FillVertical`

:   True when `illAmount` runs bottom-to-top.

`public float Padding`

:   Padding in reference pixels added around the rect so glow and shadow are not clipped by the quad.

`public SkinSurfaceTokens Surface`

:   The surface tokens this graphic draws.

**Methods**

`public void Apply(SkinSurfaceTokens value)`

:   Applies a surface and rebuilds the material and mesh.

`public void ApplySegments(int count, Color color)`

:   Applies segment ticks, used by segmented bars.

`public void SetFillColors(Color primary, Color secondary)`

:   Replaces only the fill colours, keeping shape and glow.

`public void SetGlow(Color color, float radius, float intensity)`

:   Replaces only the glow, keeping shape and fill.

---

## SkinSurfaceTokens

```csharp
public struct SkinSurfaceTokens
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Fill, stroke, and glow for one skinned surface. Every skinned widget
resolves to one of these, so a customer restyles the whole HUD by editing
a handful of surfaces rather than hunting individual prefabs.

**Fields**

`public float CornerRadius`

:   &mdash;

`public Color FillColor`

:   &mdash;

`public Color FillColorSecondary`

:   &mdash;

`public SkinFillMode FillMode`

:   &mdash;

`public Color GlowColor`

:   &mdash;

`public float GlowIntensity`

:   &mdash;

`public float GlowRadius`

:   &mdash;

`public float GradientAngleDegrees`

:   &mdash;

`public Color ShadowColor`

:   &mdash;

`public Vector2 ShadowOffset`

:   &mdash;

`public float ShadowRadius`

:   &mdash;

`public SkinShape Shape`

:   &mdash;

`public Color StrokeColor`

:   &mdash;

`public float StrokeWidth`

:   &mdash;

**Methods**

`public static SkinSurfaceTokens Flat(Color fill, float cornerRadius = 0f)`

:   A flat, strokeless, glowless surface in `fill`.

`public SkinSurfaceTokens Sanitized()`

:   Clamps every token into its supported range.

`public SkinSurfaceTokens WithFill(Color fill)`

:   Returns this surface with its fill replaced by `fill`.

`public SkinSurfaceTokens WithGlow(Color color, float radius, float intensity)`

:   Returns this surface with its glow replaced.

---

## SkinTypographyTokens

```csharp
public struct SkinTypographyTokens
```

`TempoForge.Presentation` &middot; <small>Runtime/Presentation/Skin/BattleSkinTokens.cs</small>

Type sizing and treatment. Fonts stay optional so no font is redistributed.

**Fields**

`public int BodySize`

:   &mdash;

`public int CaptionSize`

:   &mdash;

`public Font Font`

:   &mdash;

`public int HeadingSize`

:   &mdash;

`public float LineSpacing`

:   &mdash;

`public Color OutlineColor`

:   &mdash;

`public bool UseOutline`

:   &mdash;

**Methods**

`public SkinTypographyTokens Sanitized()`

:   Clamps every token into its supported range.

---

