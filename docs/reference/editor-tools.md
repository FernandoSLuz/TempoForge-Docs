# Editor tools

1 types in this area.

## BattleSkinBrowserWindow

```csharp
public sealed class BattleSkinBrowserWindow : EditorWindow
```

`TempoForge.Editor` &middot; <small>TempoForge/Editor/Skins/BattleSkinBrowserWindow.cs</small>

Browse the shipped skins, preview them with the real shader, and turn any
of them into an editable asset in one click.

This window exists because the package previously offered no way to
discover or create a look: a customer had to create a blank asset and fill
in fields with no preview. "Create editable copy" is the intended entry
point for authoring a custom skin.

**Fields**

`public BattleSkinPreset Asset`

:   &mdash;

`public bool IsShipped`

:   &mdash;

`public CompiledBattleSkin Skin`

:   &mdash;

**Methods**

`public static void Open()`

:   &mdash;

`public void Refresh()`

:   Rebuilds the list from shipped skins plus project assets.

---

