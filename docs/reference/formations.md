# Formations

32 types in this area.

!!! abstract "On this page"
    [AspectRatio](#aspectratio) &middot; [CompiledEncounterFormationLayout](#compiledencounterformationlayout) &middot; [CompiledEncounterFormationTeam](#compiledencounterformationteam) &middot; [CompiledFormationAnchor](#compiledformationanchor) &middot; [CompiledFormationPreset](#compiledformationpreset) &middot; [CompiledFormationSlot](#compiledformationslot) &middot; [EncounterFormationCompileRequest](#encounterformationcompilerequest) &middot; [EncounterFormationCompileResult](#encounterformationcompileresult) &middot; [EncounterFormationTeamRequest](#encounterformationteamrequest) &middot; [FormationAssignment](#formationassignment) &middot; [FormationDelta](#formationdelta) &middot; [FormationDragPoint](#formationdragpoint) &middot; [FormationFacing](#formationfacing) &middot; [FormationFieldTokens](#formationfieldtokens) &middot; [FormationHandleKey](#formationhandlekey) &middot; [FormationHandleKind](#formationhandlekind) &middot; [FormationInverseDragRequest](#formationinversedragrequest) &middot; [FormationInverseDragResult](#formationinversedragresult) &middot; [FormationLayoutCompiler](#formationlayoutcompiler) &middot; [FormationOccupancy](#formationoccupancy) &middot; [FormationPoint](#formationpoint) &middot; [FormationPresetCompileRequest](#formationpresetcompilerequest) &middot; [FormationPresetCompileResult](#formationpresetcompileresult) &middot; [FormationPresetDefinition](#formationpresetdefinition) &middot; [FormationProjectionEntry](#formationprojectionentry) &middot; [FormationProjectionRequest](#formationprojectionrequest) &middot; [FormationProjectionResult](#formationprojectionresult) &middot; [FormationSlotDefinition](#formationslotdefinition) &middot; [FormationVfxAnchorDefinition](#formationvfxanchordefinition) &middot; [FormationViewport](#formationviewport) &middot; [MovedFormationPoint](#movedformationpoint) &middot; [ProjectedFormationPoint](#projectedformationpoint)

## AspectRatio

```csharp
public readonly struct AspectRatio : IEquatable<AspectRatio>
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AspectRatio(int numerator, int denominator)`

:   &mdash;

**Properties**

`public int Denominator`

:   &mdash;

`public int Numerator`

:   &mdash;

**Methods**

`public bool Equals(AspectRatio other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## CompiledEncounterFormationLayout

```csharp
public sealed class CompiledEncounterFormationLayout
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public StableId EncounterId`

:   &mdash;

`public FrozenList<FormationOccupancy> Occupancy`

:   &mdash;

`public FrozenSortedIndex<StableId, FormationOccupancy> OccupancyByCombatant`

:   &mdash;

`public FrozenSortedIndex<StableId, StableId> OccupancyBySlot`

:   &mdash;

`public FrozenList<CompiledEncounterFormationTeam> Teams`

:   &mdash;

---

## CompiledEncounterFormationTeam

```csharp
public sealed class CompiledEncounterFormationTeam
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<FormationOccupancy> Occupancy`

:   &mdash;

`public CompiledFormationPreset Preset`

:   &mdash;

`public StableId ResolvedSideId`

:   &mdash;

`public StableId TeamId`

:   &mdash;

---

## CompiledFormationAnchor

```csharp
public readonly struct CompiledFormationAnchor
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public StableId AnchorId`

:   &mdash;

`public FormationPoint Position`

:   &mdash;

---

## CompiledFormationPreset

```csharp
public sealed class CompiledFormationPreset
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public AspectRatio DesignAspect`

:   &mdash;

`public StableId PresetId`

:   &mdash;

`public FrozenList<CompiledFormationSlot> Slots`

:   &mdash;

**Methods**

`public bool TryGetSlot(StableId slotId, out CompiledFormationSlot slot)`

:   &mdash;

---

## CompiledFormationSlot

```csharp
public sealed class CompiledFormationSlot
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<CompiledFormationAnchor> Anchors`

:   &mdash;

`public FormationPoint ApproachPoint`

:   &mdash;

`public FormationFacing Facing`

:   &mdash;

`public FormationPoint Position`

:   &mdash;

`public StableId RowId`

:   &mdash;

`public StableId SideId`

:   &mdash;

`public StableId SlotId`

:   &mdash;

`public StableId SortingLayerKey`

:   &mdash;

`public int SortingOrder`

:   &mdash;

---

## EncounterFormationCompileRequest

```csharp
public sealed class EncounterFormationCompileRequest
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public EncounterFormationCompileRequest()`

:   &mdash;

**Properties**

`public StableId EncounterId`

:   &mdash;

`public AuthoringCompileOptions Options`

:   &mdash;

`public FrozenList<EncounterFormationTeamRequest> Teams`

:   &mdash;

---

## EncounterFormationCompileResult

```csharp
public sealed class EncounterFormationCompileResult
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public CompiledEncounterFormationLayout Layout`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public bool WasCancelled`

:   &mdash;

---

## EncounterFormationTeamRequest

```csharp
public sealed class EncounterFormationTeamRequest
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public EncounterFormationTeamRequest()`

:   &mdash;

**Properties**

`public FrozenList<FormationAssignment> Assignments`

:   &mdash;

`public FrozenList<StableId> MemberIds`

:   &mdash;

`public CompiledFormationPreset Preset`

:   &mdash;

`public StableId TeamId`

:   &mdash;

---

## FormationAssignment

```csharp
public readonly struct FormationAssignment
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationAssignment(StableId combatantId, StableId slotId)`

:   &mdash;

**Properties**

`public StableId CombatantId`

:   &mdash;

`public StableId SlotId`

:   &mdash;

---

## FormationDelta

```csharp
public readonly struct FormationDelta : IEquatable<FormationDelta>
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationDelta(int x, int y)`

:   &mdash;

**Properties**

`public int X`

:   &mdash;

`public int Y`

:   &mdash;

**Methods**

`public bool Equals(FormationDelta other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## FormationDragPoint

```csharp
public readonly struct FormationDragPoint
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationDragPoint(FormationHandleKey key, FormationPoint original)`

:   &mdash;

**Properties**

`public FormationHandleKey Key`

:   &mdash;

`public FormationPoint Original`

:   &mdash;

---

## FormationFacing

```csharp
public enum FormationFacing : byte
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Left` | &mdash; |
| `Right` | &mdash; |

---

## FormationFieldTokens

```csharp
public static class FormationFieldTokens
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationLayoutCompiler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## FormationHandleKey

```csharp
public readonly struct FormationHandleKey
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationHandleKey()`

:   &mdash;

**Properties**

`public StableId? AnchorId`

:   &mdash;

`public FormationHandleKind Kind`

:   &mdash;

`public StableId SlotId`

:   &mdash;

**Methods**

`public int CompareTo(FormationHandleKey other)`

:   &mdash;

`public bool Equals(FormationHandleKey other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## FormationHandleKind

```csharp
public enum FormationHandleKind : byte
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Slot` | &mdash; |
| `Approach` | &mdash; |
| `Anchor` | &mdash; |

---

## FormationInverseDragRequest

```csharp
public sealed class FormationInverseDragRequest
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationInverseDragRequest()`

:   &mdash;

**Properties**

`public ProjectedFormationPoint CurrentPointer`

:   &mdash;

`public int GridStep`

:   &mdash;

`public FormationProjectionResult Projection`

:   &mdash;

`public FrozenList<FormationDragPoint> SelectedPoints`

:   &mdash;

`public ProjectedFormationPoint StartPointer`

:   &mdash;

---

## FormationInverseDragResult

```csharp
public sealed class FormationInverseDragResult
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FormationDelta Delta`

:   &mdash;

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public FrozenList<MovedFormationPoint> MovedPoints`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public bool WasClamped`

:   &mdash;

---

## FormationLayoutCompiler

```csharp
public sealed partial class FormationLayoutCompiler
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationLayoutCompiler.CopiedSnapshot.cs</small>

Pure deterministic formation compiler and integer projection service.
It retains no Unity object and performs no editor or gameplay mutation.

**Methods**

`public EncounterFormationCompileResult CompileEncounter()`

:   &mdash;

`public FormationPresetCompileResult CompilePreset()`

:   &mdash;

`public FormationInverseDragResult InverseDrag()`

:   &mdash;

`public FormationProjectionResult Project(FormationProjectionRequest request)`

:   &mdash;

---

## FormationOccupancy

```csharp
public readonly struct FormationOccupancy
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public StableId CombatantId`

:   &mdash;

`public StableId PresetId`

:   &mdash;

`public StableId RowId`

:   &mdash;

`public StableId SideId`

:   &mdash;

`public StableId SlotId`

:   &mdash;

`public StableId TeamId`

:   &mdash;

---

## FormationPoint

```csharp
public readonly struct FormationPoint : IEquatable<FormationPoint>
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationPoint(int x, int y)`

:   &mdash;

**Properties**

`public int X`

:   &mdash;

`public int Y`

:   &mdash;

**Methods**

`public bool Equals(FormationPoint other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## FormationPresetCompileRequest

```csharp
public sealed class FormationPresetCompileRequest
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationPresetCompileRequest()`

:   &mdash;

**Properties**

`public AuthoringCompileOptions Options`

:   &mdash;

`public FormationPresetDefinition Preset`

:   &mdash;

---

## FormationPresetCompileResult

```csharp
public sealed class FormationPresetCompileResult
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public CompiledFormationPreset Preset`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public bool WasCancelled`

:   &mdash;

---

## FormationPresetDefinition

```csharp
public sealed class FormationPresetDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationPresetDefinition.cs</small>

Mutable Unity authoring data. Compilation snapshots every value and returns
engine-independent immutable records; this object is never retained.

**Properties**

`public int DesignAspectDenominator`

:   &mdash;

`public int DesignAspectNumerator`

:   &mdash;

`public IReadOnlyList<FormationSlotDefinition> Slots`

:   &mdash;

**Methods**

`public static FormationPresetDefinition CreateTransient()`

:   Explicit in-memory construction hook for tests and customer tooling. It creates no asset, GUID, or implicit persistent mutation.

---

## FormationProjectionEntry

```csharp
public readonly struct FormationProjectionEntry
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FormationHandleKey Key`

:   &mdash;

`public ProjectedFormationPoint Projected`

:   &mdash;

`public FormationPoint Source`

:   &mdash;

---

## FormationProjectionRequest

```csharp
public sealed class FormationProjectionRequest
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationProjectionRequest()`

:   &mdash;

**Properties**

`public AspectRatio Aspect`

:   &mdash;

`public CompiledFormationPreset Preset`

:   &mdash;

`public FormationViewport Viewport`

:   &mdash;

---

## FormationProjectionResult

```csharp
public sealed class FormationProjectionResult
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public AspectRatio Aspect`

:   &mdash;

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public FrozenList<FormationProjectionEntry> Entries`

:   &mdash;

`public FormationViewport FittedViewport`

:   &mdash;

`public CompiledFormationPreset Preset`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public FormationViewport Viewport`

:   &mdash;

**Methods**

`public bool TryGetEntry()`

:   &mdash;

---

## FormationSlotDefinition

```csharp
public sealed class FormationSlotDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationSlotDefinition()`

:   &mdash;

`public FormationSlotDefinition()`

:   &mdash;

**Properties**

`public IReadOnlyList<FormationVfxAnchorDefinition> Anchors`

:   &mdash;

`public int ApproachX`

:   &mdash;

`public int ApproachY`

:   &mdash;

`public FormationFacing Facing`

:   &mdash;

`public int PositionX`

:   &mdash;

`public int PositionY`

:   &mdash;

`public string RowIdRaw`

:   &mdash;

`public string SideIdRaw`

:   &mdash;

`public string SlotIdRaw`

:   &mdash;

`public string SortingLayerKeyRaw`

:   &mdash;

`public int SortingOrder`

:   &mdash;

---

## FormationVfxAnchorDefinition

```csharp
public sealed class FormationVfxAnchorDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationVfxAnchorDefinition()`

:   &mdash;

`public FormationVfxAnchorDefinition()`

:   &mdash;

**Properties**

`public string AnchorIdRaw`

:   &mdash;

`public int PositionX`

:   &mdash;

`public int PositionY`

:   &mdash;

---

## FormationViewport

```csharp
public readonly struct FormationViewport : IEquatable<FormationViewport>
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormationViewport(int left, int bottom, int width, int height)`

:   &mdash;

**Properties**

`public int Bottom`

:   &mdash;

`public int Height`

:   &mdash;

`public int Left`

:   &mdash;

`public int Width`

:   &mdash;

**Methods**

`public bool Equals(FormationViewport other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## MovedFormationPoint

```csharp
public readonly struct MovedFormationPoint
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FormationHandleKey Key`

:   &mdash;

`public FormationPoint Position`

:   &mdash;

---

## ProjectedFormationPoint

```csharp
public readonly struct ProjectedFormationPoint : IEquatable<ProjectedFormationPoint>
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Formation/FormationModels.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ProjectedFormationPoint(int x, int y)`

:   &mdash;

**Properties**

`public int X`

:   &mdash;

`public int Y`

:   &mdash;

**Methods**

`public bool Equals(ProjectedFormationPoint other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

