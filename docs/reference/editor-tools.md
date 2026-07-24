# Editor tools

23 types in this area.

!!! abstract "On this page"
    [AuthoringMigrationBatchOrchestrator](#authoringmigrationbatchorchestrator) &middot; [AuthoringMigrationRegistry](#authoringmigrationregistry) &middot; [BattleSkinBrowserWindow](#battleskinbrowserwindow) &middot; [BattleSkinPresetEditor](#battleskinpreseteditor) &middot; [CompilerBackedMigrationPrecommitValidator](#compilerbackedmigrationprecommitvalidator) &middot; [EditorDiagnosticNavigationIndex](#editordiagnosticnavigationindex) &middot; [EditorDiagnosticNavigationRecord](#editordiagnosticnavigationrecord) &middot; [IAuthoringAssetMigration](#iauthoringassetmigration) &middot; [IAuthoringMigrationCommitFaultInjector](#iauthoringmigrationcommitfaultinjector) &middot; [IAuthoringMigrationPrecommitValidator](#iauthoringmigrationprecommitvalidator) &middot; [IAuthoringStableIdChangingMigration](#iauthoringstableidchangingmigration) &middot; [MigrationAssetSnapshot](#migrationassetsnapshot) &middot; [MigrationBatchResult](#migrationbatchresult) &middot; [MigrationChange](#migrationchange) &middot; [MigrationCommitCheckpoint](#migrationcommitcheckpoint) &middot; [MigrationObjectReferenceToken](#migrationobjectreferencetoken) &middot; [MigrationPrecommitValidationResult](#migrationprecommitvalidationresult) &middot; [MigrationPreview](#migrationpreview) &middot; [MigrationSerializedField](#migrationserializedfield) &middot; [MigrationSerializedValue](#migrationserializedvalue) &middot; [MigrationSerializedValueKind](#migrationserializedvaluekind) &middot; [MigrationStepResult](#migrationstepresult) &middot; [SkinPreviewRenderer](#skinpreviewrenderer)

## AuthoringMigrationBatchOrchestrator

```csharp
public sealed class AuthoringMigrationBatchOrchestrator
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationBatchOrchestrator.cs</small>

Explicit, synchronous Editor migration transaction. It never discovers
assets, saves assets, or runs from import/deserialization callbacks.

**Constructors**

`public AuthoringMigrationBatchOrchestrator()`

:   &mdash;

`public AuthoringMigrationBatchOrchestrator()`

:   &mdash;

**Methods**

`public MigrationBatchResult MigrateAffectedClosure()`

:   &mdash;

---

## AuthoringMigrationRegistry

```csharp
public sealed class AuthoringMigrationRegistry
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AuthoringMigrationRegistry()`

:   &mdash;

**Properties**

`public FrozenList<IAuthoringAssetMigration> OrderedSteps`

:   &mdash;

`public static AuthoringMigrationRegistry Product`

:   &mdash;

---

## BattleSkinBrowserWindow

```csharp
public sealed class BattleSkinBrowserWindow : EditorWindow
```

`TempoForge.Editor` &middot; <small>Editor/Skins/BattleSkinBrowserWindow.cs</small>

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

## BattleSkinPresetEditor

```csharp
public sealed class BattleSkinPresetEditor : UnityEditor.Editor
```

`TempoForge.Editor` &middot; <small>Editor/Skins/BattleSkinPresetEditor.cs</small>

Inspector for `attleSkinPreset` with a live preview above the
fields.

Editing a colour or a corner radius and seeing the result immediately is
the difference between a customization surface a customer will actually
use and a wall of forty numbers they will not. The preview is drawn with
the shipped shader, so what is shown here is what ships.

**Methods**

`public override bool HasPreviewGUI()`

:   &mdash;

`public override void OnInspectorGUI()`

:   &mdash;

`public override void OnPreviewGUI(Rect rect, GUIStyle background)`

:   &mdash;

---

## CompilerBackedMigrationPrecommitValidator

```csharp
public sealed class CompilerBackedMigrationPrecommitValidator
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/CompilerBackedMigrationPrecommitValidator.cs</small>

Builds the exact, explicit authoring closure rooted at one catalog and
validates detached migration output through the production compiler.
No project, folder, or assembly discovery is performed.

**Constructors**

`public CompilerBackedMigrationPrecommitValidator()`

:   &mdash;

**Properties**

`public FrozenList<StableIdDefinition> AffectedAssets`

:   The unique source objects that must be passed to MigrateAffectedClosure. The root catalog is first; remaining objects follow the catalog's fixed category order and serialized set order.

**Methods**

`public bool Equals(T left, T right)`

:   &mdash;

`public int GetHashCode(T value)`

:   &mdash;

`public MigrationPrecommitValidationResult ValidateAffectedClosure()`

:   &mdash;

---

## EditorDiagnosticNavigationIndex

```csharp
public sealed class EditorDiagnosticNavigationIndex
```

`TempoForge.Editor` &middot; <small>Editor/Validation/EditorDiagnosticNavigationIndex.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int DiagnosticCount`

:   &mdash;

**Methods**

`public bool TryGetRecords()`

:   &mdash;

---

## EditorDiagnosticNavigationRecord

```csharp
public sealed class EditorDiagnosticNavigationRecord
```

`TempoForge.Editor` &middot; <small>Editor/Validation/EditorDiagnosticNavigationIndex.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public EditorDiagnosticNavigationRecord()`

:   &mdash;

**Properties**

`public int NestedSerializedIndex`

:   &mdash;

`public string SerializedPropertyPath`

:   &mdash;

`public UnityEngine.Object Source`

:   &mdash;

`public int TopLevelSerializedIndex`

:   &mdash;

---

## IAuthoringAssetMigration

```csharp
public interface IAuthoringAssetMigration
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## IAuthoringMigrationCommitFaultInjector

```csharp
public interface IAuthoringMigrationCommitFaultInjector
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## IAuthoringMigrationPrecommitValidator

```csharp
public interface IAuthoringMigrationPrecommitValidator
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

The product integration compiles and validates the complete affected
catalog closure from detached staged snapshots. A validator is mandatory;
the orchestrator has no permissive production fallback. Product catalog
migrations use CompilerBackedMigrationPrecommitValidator; lightweight
alternatives are intended only for isolated transaction tests.

---

## IAuthoringStableIdChangingMigration

```csharp
public interface IAuthoringStableIdChangingMigration
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

Optional, deliberately conspicuous escape hatch for a future documented
public migration that must change gameplay identity. Ordinary migrations
are rejected if they alter StableIdRaw.

---

## MigrationAssetSnapshot

```csharp
public sealed class MigrationAssetSnapshot
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Type AssetType`

:   &mdash;

`public int SchemaVersion`

:   &mdash;

`public FrozenList<MigrationSerializedField> SerializedFields`

:   &mdash;

`public string StableIdRaw`

:   &mdash;

`public bool WasDirty`

:   &mdash;

**Methods**

`public byte[] GetCanonicalSnapshotBytes()`

:   Returns a deterministic, bit-exact encoding of this detached snapshot. This is not a Unity asset-file serialization and must not be presented as disk bytes.

`public bool TryGetField()`

:   &mdash;

`public MigrationAssetSnapshot WithBoolean()`

:   &mdash;

`public MigrationAssetSnapshot WithInteger()`

:   &mdash;

`public MigrationAssetSnapshot WithObjectReference()`

:   &mdash;

`public MigrationAssetSnapshot WithSchemaVersion(int schemaVersion)`

:   &mdash;

`public MigrationAssetSnapshot WithString()`

:   &mdash;

`public MigrationAssetSnapshot WithUnsignedInteger()`

:   &mdash;

---

## MigrationBatchResult

```csharp
public sealed class MigrationBatchResult
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public FrozenList<UnityEngine.Object> MutatedAssets`

:   &mdash;

`public bool RestorationFailed`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public bool WasCancelled`

:   &mdash;

---

## MigrationChange

```csharp
public sealed class MigrationChange
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public MigrationChange()`

:   &mdash;

**Properties**

`public string AfterValue`

:   &mdash;

`public string BeforeValue`

:   &mdash;

`public string PropertyPath`

:   &mdash;

`public string Summary`

:   &mdash;

---

## MigrationCommitCheckpoint

```csharp
public enum MigrationCommitCheckpoint : byte
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `BeforeFirstApplication` | &mdash; |
| `BetweenApplications` | &mdash; |
| `AfterLastApplication` | &mdash; |

---

## MigrationObjectReferenceToken

```csharp
public sealed class MigrationObjectReferenceToken
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

Editor-only identity for a serialized Unity object reference. Persistent
references use GlobalObjectId; transient test objects use a direct identity
fallback that never leaves the migration operation.

**Properties**

`public string GlobalObjectIdText`

:   &mdash;

`public bool IsPersistent`

:   &mdash;

`public bool RepresentsNull`

:   &mdash;

**Methods**

`public bool Equals(MigrationObjectReferenceToken other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## MigrationPrecommitValidationResult

```csharp
public sealed class MigrationPrecommitValidationResult
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public MigrationPrecommitValidationResult()`

:   &mdash;

**Properties**

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public bool HasErrors`

:   &mdash;

---

## MigrationPreview

```csharp
public sealed class MigrationPreview
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public MigrationPreview()`

:   &mdash;

**Properties**

`public FrozenList<MigrationChange> Changes`

:   &mdash;

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public int FromVersion`

:   &mdash;

`public bool Supported`

:   &mdash;

`public int ToVersion`

:   &mdash;

---

## MigrationSerializedField

```csharp
public sealed class MigrationSerializedField
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public MigrationSerializedField()`

:   &mdash;

**Properties**

`public string PropertyPath`

:   &mdash;

`public MigrationSerializedValue Value`

:   &mdash;

**Methods**

`public bool Equals(MigrationSerializedField other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## MigrationSerializedValue

```csharp
public sealed class MigrationSerializedValue
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

Immutable scalar copied from a SerializedProperty. Containers are
represented by their array size plus flattened immutable child values.

**Properties**

`public bool BooleanValue`

:   &mdash;

`public double FloatingPointValue`

:   &mdash;

`public long IntegerValue`

:   &mdash;

`public MigrationSerializedValueKind Kind`

:   &mdash;

`public MigrationObjectReferenceToken ObjectReferenceValue`

:   &mdash;

`public string StringValue`

:   &mdash;

`public ulong UnsignedIntegerValue`

:   &mdash;

**Methods**

`public bool Equals(MigrationSerializedValue other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## MigrationSerializedValueKind

```csharp
public enum MigrationSerializedValueKind : byte
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `ArraySize` | &mdash; |
| `Integer` | &mdash; |
| `Boolean` | &mdash; |
| `FloatingPoint` | &mdash; |
| `String` | &mdash; |
| `Color` | &mdash; |
| `ObjectReference` | &mdash; |
| `LayerMask` | &mdash; |
| `Enum` | &mdash; |
| `Vector2` | &mdash; |
| `Vector3` | &mdash; |
| `Vector4` | &mdash; |
| `Rect` | &mdash; |
| `Character` | &mdash; |
| `Bounds` | &mdash; |
| `Quaternion` | &mdash; |
| `Vector2Int` | &mdash; |
| `Vector3Int` | &mdash; |
| `RectInt` | &mdash; |
| `BoundsInt` | &mdash; |
| `ExposedReference` | &mdash; |
| `SignedInteger8` | &mdash; |
| `SignedInteger16` | &mdash; |
| `SignedInteger32` | &mdash; |
| `SignedInteger64` | &mdash; |
| `UnsignedInteger8` | &mdash; |
| `UnsignedInteger16` | &mdash; |
| `UnsignedInteger32` | &mdash; |
| `UnsignedInteger64` | &mdash; |
| `Float32` | &mdash; |
| `Float64` | &mdash; |

---

## MigrationStepResult

```csharp
public sealed class MigrationStepResult
```

`TempoForge.Editor` &middot; <small>Editor/Validation/Migrations/AuthoringMigrationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public MigrationStepResult()`

:   &mdash;

**Properties**

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public MigrationAssetSnapshot Output`

:   &mdash;

`public bool Succeeded`

:   &mdash;

---

## SkinPreviewRenderer

```csharp
public sealed class SkinPreviewRenderer : IDisposable
```

`TempoForge.Editor` &middot; <small>Editor/Skins/SkinPreviewRenderer.cs</small>

Draws skin previews in editor windows and inspectors using the same
shader the runtime interface uses.

Reusing the real shader matters: a preview drawn with editor primitives
would drift from the shipped look, and a customer who picks a skin from a
lying thumbnail has been misled. Every surface here is rendered by
`TempoForge/Skinned Surface` with the same token values the runtime
would use, through the same material writer.

This is an instance type rather than a static helper because the editor
assembly forbids static fields that can retain a
`nityEngine.Object`: such a field survives a reload with
Domain Reload disabled and then hands out a destroyed material. Owners
create one in `OnEnable` and `ispose` it in
`OnDisable`.

**Properties**

`public bool CanRenderSurfaces`

:   True when the skinned-surface shader is available.

**Methods**

`public void Dispose()`

:   Releases the preview material.

`public void DrawBar(Rect rect, SkinBarTokens bar, float fraction)`

:   Draws a value bar preview at `fraction`.

`public void DrawHudPreview(Rect rect, CompiledBattleSkin skin)`

:   Draws a compact mock interface: backdrop, roster panel, bars, status pips, timeline chip, and a tray button. Enough for a customer to judge a skin without entering play mode.

`public void DrawPalette(Rect rect, SkinPaletteTokens palette)`

:   Draws the palette as a row of swatches.

`public void DrawSurface()`

:   Draws one skin surface into `rect`.

---

