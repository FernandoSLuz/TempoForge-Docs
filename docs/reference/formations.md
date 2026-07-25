# Formations

14 types in this area.

!!! abstract "On this page"
    [AspectRatio](#aspectratio) &middot; [CompiledEncounterFormationLayout](#compiledencounterformationlayout) &middot; [CompiledEncounterFormationTeam](#compiledencounterformationteam) &middot; [CompiledFormationAnchor](#compiledformationanchor) &middot; [CompiledFormationPreset](#compiledformationpreset) &middot; [CompiledFormationSlot](#compiledformationslot) &middot; [FormationFacing](#formationfacing) &middot; [FormationOccupancy](#formationoccupancy) &middot; [FormationPoint](#formationpoint) &middot; [FormationPresetDefinition](#formationpresetdefinition) &middot; [FormationSlotDefinition](#formationslotdefinition) &middot; [FormationVfxAnchorDefinition](#formationvfxanchordefinition) &middot; [FormationViewport](#formationviewport) &middot; [ProjectedFormationPoint](#projectedformationpoint)

## AspectRatio

```csharp
public readonly struct AspectRatio : IEquatable<AspectRatio>
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

## FormationFacing

```csharp
public enum FormationFacing : byte
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Left` | &mdash; |
| `Right` | &mdash; |

---

## FormationOccupancy

```csharp
public readonly struct FormationOccupancy
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

## FormationPresetDefinition

:material-star: **Start here**

```csharp
public sealed class FormationPresetDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationPresetDefinition.cs</small>

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

## FormationSlotDefinition

```csharp
public sealed class FormationSlotDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationDefinitions.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationDefinitions.cs</small>

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

## ProjectedFormationPoint

```csharp
public readonly struct ProjectedFormationPoint : IEquatable<ProjectedFormationPoint>
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Formation/FormationModels.cs</small>

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

