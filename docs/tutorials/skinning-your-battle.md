# 4. Skins and presets

Everything the battle interface draws itself with lives in one asset: a
**Battle Skin Preset**. Colours, corner radii, glow, bar geometry, status pips,
typography, animation timings, and where each interface region sits on screen all
come from that asset.

Two consequences worth stating plainly:

- You never edit a prefab to restyle the interface, because the interface has no
  prefabs. It is built from the skin at runtime.
- A skin cannot change a battle outcome. Skins are presentation-only and never
  enter a snapshot, a replay, or a state hash.

---

## The five-minute version

1. **Tools ▸ TempoForge ▸ Skin Browser**.
2. Pick a shipped skin. The preview uses the real shader, so what you see ships.
3. **Create editable copy…** and save it into your own folder.
4. Select the new asset. Edit fields; the inspector preview updates live.
5. Assign it to your `BattleUiRoot` component's **Skin Preset** field, or press
   **Apply to interfaces in open scenes** in the browser.

That is the whole authoring loop. There is no step where you hand-position a
panel.

## Shipped skins

| Skin | Character |
| --- | --- |
| **Slate Nocturne** | Dark slate, cyan and amber accents, soft in-shader glow. The default. |
| **Parchment Atlas** | Warm paper, inked borders, sepia type, circular pips, no glow. |
| **Neon Circuit** | Deep indigo, saturated cyan and magenta rims, strong halos, hex pips. |
| **Minimal Mono** | Light neutral surfaces, hairline borders, no glow or gradients. |

These are defined in code (`BattleSkinDefaults`), not as assets. That is
deliberate:

- The interface always has a complete, valid look even when a scene assigns no
  skin, so the package never renders as unstyled boxes.
- No font, texture, or material is redistributed. Every look is drawn
  procedurally.

Use **Create editable copy…** to turn any of them into an asset you own.

---

## What you can change

### Palette

Semantic roles, assigned once and reused everywhere. Change `Accent` and the
selection highlight, ready gauge, focus rings, and status pips all follow.

`Background`, `Surface`, `SurfaceRaised`, `Border`, `TextPrimary`,
`TextSecondary`, `TextMuted`, `Accent`, `AccentAlt`, `Positive`, `Negative`,
`Warning`, `Shield`, `AllyTeam`, `EnemyTeam`.

### Surfaces

Each surface is a shape plus a fill, stroke, glow, and shadow:

| Surface | Used by |
| --- | --- |
| `Panel` | Roster, feedback log, timeline backing, transport bar |
| `PanelRaised` | Active timeline entry, roster rows |
| `Button` / `ButtonSelected` / `ButtonDisabled` | Skill tray, transport buttons |
| `Tooltip` | Tooltip panel and result banner |
| `StageBackdrop` | Behind the combatants |

Shapes: `RoundedRect`, `Circle`, `Capsule`, `Hexagon`, `Diamond`. Fills: flat,
linear gradient at any angle, or radial.

**Glow is drawn inside the shader.** It is not post-processing. This is why
TempoForge depends on no post-processing package and why enabling a glow cannot
conflict with your existing volumes or renderer features.

### Bars and gauges

`Health`, `Shield`, `Resource`, `Cast`, and `SchedulerGauge`, each with its own
height, corner radius, track surface, fill surface, and segment ticks.

`DeltaCatchUpSeconds` controls the trailing ghost that shows the value just lost
— set it to 0 to disable that feedback.

### Status pips

Size, spacing, shape, and how many show before collapsing into a `+N` overflow
pip. Capping matters: without it a heavily-stacked combatant would push its plate
wider than its token.

### Motion

Every duration passes through `MotionScale`. Two shortcuts:

- `MotionScale = 0` snaps every transition instantly.
- `ReduceMotion = true` does the same and skips decorative motion. Wire this to a
  player accessibility setting.

### Layout regions

Each interface region is independently placeable: `Status`, `Timeline`,
`SkillTray`, `Feedback`, `Result`, `Transport`, `Tooltip`. Every one has
`Visible`, `Anchor`, `Offset`, `Size`, and `Scale`.

- Positive `Offset` values always move a region **inward** from its anchor,
  whichever corner it is anchored to.
- Setting `Visible = false` means the region is never created at all, so hiding it
  costs nothing.
- `UseSafeArea` insets the whole interface into the device safe area, so no region
  lands under a notch or a home indicator.

**Shipping tip:** turn off the `Transport` region, or tick **Hide Transport
Controls** on `BattleUiRoot`. Those are development controls.

---

## Applying a skin from code

```csharp
[SerializeField] private BattleUiRoot ui;
[SerializeField] private BattleSkinPreset nightSkin;

void EnterNightMode()
{
    // Rebuilds the interface and repaints it from retained state.
    ui.ApplySkin(nightSkin);
}
```

`ApplySkin` is safe at runtime. It destroys the old region tree, rebuilds from the
new tokens, and redraws the roster, timeline, tray, log, and result from state the
interface already holds — no snapshot replay needed.

To read the resolved values without an asset:

```csharp
CompiledBattleSkin skin = ui.Skin;          // never null
Color accent = skin.Palette.Accent;
float barHeight = skin.Bars.Health.Height;
```

## Using skinned widgets in your own interface

The primitives are public, so you can build your own panels in the same style:

```csharp
var panel = SkinnedWidgetFactory.CreateSurface("MyPanel", parent, skin.Surfaces.Panel);
SkinnedWidgetFactory.Fill((RectTransform)panel.transform);

var label = SkinnedWidgetFactory.CreateLabel(
    "Title", parent, skin, skin.Typography.HeadingSize,
    skin.Palette.TextPrimary, TextAnchor.MiddleLeft);

var bar = barRect.gameObject.AddComponent<SkinnedValueBar>();
bar.Build(skin, skin.Bars.Health, withReadout: true);
bar.SetFraction(0.6f);   // animates
bar.Tick(deltaSeconds);  // drive from your visual clock
```

`SkinSurfaceGraphic` is a `MaskableGraphic`, so it behaves correctly inside `Mask`
and `RectMask2D` exactly like a built-in `Image`.

---

## Performance notes

Materials are pooled per unique parameter set by a `SkinMaterialPool` created on
the canvas root. Six identical status pips share one material and batch together;
a bar animating its fill quantizes to 1/256 so it does not allocate a new material
per frame.

The pool is owned by a component, not by static state, so its materials are
destroyed with the interface rather than surviving a scene unload.

## If previews or surfaces look flat

The shader lives at
`Assets/TempoForge/Runtime/Presentation/Resources/TempoForge/TempoForgeSkinnedSurface.shader`.

It is in a `Resources` folder on purpose: that guarantees it survives build shader
stripping without you adding it to **Always Included Shaders**. If it cannot be
loaded, the interface logs one warning and falls back to flat surfaces — never
magenta. Reimport that folder to restore it.

## Optional post-processing

The default look needs none. If you want a softer bloom across the whole stage
and are not already running your own post stack, add **TempoForge ▸ Battle Stage
Bloom (Optional)** to your battle camera.

It is off until you add it, needs no packages, and is Built-in-pipeline only.
Under URP or HDRP it logs one explanation and disables itself rather than silently
doing nothing — use that pipeline's own Bloom and Vignette volume overrides
instead.

## Next

- **[Workbench and balancing](../how-to/balance-with-the-workbench.md)**
- **[API reference](../reference/index.md)**
