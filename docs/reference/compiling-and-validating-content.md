# Compiling and validating content

11 types in this area.

!!! abstract "On this page"
    [AuthoringCompileOptions](#authoringcompileoptions) &middot; [AuthoringCompileRequest](#authoringcompilerequest) &middot; [AuthoringCompileResult](#authoringcompileresult) &middot; [AuthoringDiagnostic](#authoringdiagnostic) &middot; [AuthoringDiagnosticSeverity](#authoringdiagnosticseverity) &middot; [AuthoringLimits](#authoringlimits) &middot; [AuthoringValidationReport](#authoringvalidationreport) &middot; [BattleContentCompiler](#battlecontentcompiler) &middot; [CompiledAuthoringCatalog](#compiledauthoringcatalog) &middot; [CompiledEncounterSnapshot](#compiledencountersnapshot) &middot; [FrozenSortedIndex](#frozensortedindex)

## AuthoringCompileOptions

```csharp
public sealed class AuthoringCompileOptions
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/AuthoringCompileOptions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AuthoringCompileOptions()`

:   &mdash;

**Properties**

`public CancellationToken CancellationToken`

:   &mdash;

`public static AuthoringCompileOptions Default`

:   &mdash;

`public bool IncludeWarnings`

:   &mdash;

---

## AuthoringCompileRequest

:material-star: **Start here**

```csharp
public sealed class AuthoringCompileRequest
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/AuthoringCompileContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AuthoringCompileRequest()`

:   &mdash;

**Properties**

`public BattleContentCatalog Catalog`

:   &mdash;

`public BattleMechanicsRegistry MechanicsRegistry`

:   &mdash;

`public AuthoringCompileOptions Options`

:   &mdash;

`public BattleSchedulerRegistry SchedulerRegistry`

:   &mdash;

**Methods**

`public static AuthoringCompileRequest WithBuiltIns()`

:   &mdash;

---

## AuthoringCompileResult

:material-star: **Start here**

```csharp
public sealed class AuthoringCompileResult
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/AuthoringCompileContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public CompiledAuthoringCatalog CatalogSnapshot`

:   &mdash;

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public bool WasCancelled`

:   &mdash;

---

## AuthoringDiagnostic

```csharp
public sealed class AuthoringDiagnostic : IEquatable<AuthoringDiagnostic>
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Validation/AuthoringDiagnostics.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AuthoringDiagnostic()`

:   &mdash;

**Properties**

`public StableId DiagnosticId`

:   &mdash;

`public string HumanDetail`

:   &mdash;

`public Diagnostic? NestedB3Diagnostic`

:   &mdash;

`public string OwnerStableIdRaw`

:   &mdash;

`public StableId? RelatedId`

:   &mdash;

`public AuthoringDiagnosticSeverity Severity`

:   &mdash;

`public PortableSourceCoordinate Source`

:   &mdash;

**Methods**

`public bool Equals(AuthoringDiagnostic other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## AuthoringDiagnosticSeverity

```csharp
public enum AuthoringDiagnosticSeverity : byte
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Validation/AuthoringDiagnostics.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Error` | &mdash; |
| `Warning` | &mdash; |

---

## AuthoringLimits

```csharp
public static class AuthoringLimits
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Validation/AuthoringLimits.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## AuthoringValidationReport

```csharp
public sealed class AuthoringValidationReport
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/AuthoringCompileContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AuthoringDiagnostic> Diagnostics`

:   &mdash;

`public bool IsValid`

:   &mdash;

`public bool WasCancelled`

:   &mdash;

---

## BattleContentCompiler

:material-star: **Start here**

```csharp
public sealed partial class BattleContentCompiler
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/BattleContentCompiler.B4ContentMapping.cs</small>

Deterministic, synchronous, fail-closed compiler. Unity data is touched
once by CatalogSourceSnapshot.Capture; every validation stage below reads
only immutable non-Unity DTOs.

**Methods**

`public AuthoringCompileResult Compile(AuthoringCompileRequest request)`

:   &mdash;

`public AuthoringValidationReport Validate(AuthoringCompileRequest request)`

:   &mdash;

---

## CompiledAuthoringCatalog

:material-star: **Start here**

```csharp
public sealed class CompiledAuthoringCatalog
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/AuthoringCompileContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledAuthoringCatalog()`

:   &mdash;

**Properties**

`public CompiledBattleContent BattleContent`

:   &mdash;

`public Sha256Digest CompiledSnapshotHash`

:   &mdash;

`public Sha256Digest ContentManifestHash`

:   &mdash;

`public FrozenSortedIndex<StableId, CompiledEncounterSnapshot> Encounters`

:   &mdash;

`public FrozenSortedIndex<StableId, CompiledFormationPreset> FormationPresets`

:   &mdash;

`public BattleMechanicsRegistry MechanicsRegistry`

:   &mdash;

`public BattleSchedulerRegistry SchedulerRegistry`

:   &mdash;

---

## CompiledEncounterSnapshot

```csharp
public sealed class CompiledEncounterSnapshot
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/AuthoringCompileContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledEncounterSnapshot()`

:   &mdash;

**Properties**

`public StableId EncounterId`

:   &mdash;

`public CompiledEncounterFormationLayout FormationLayout`

:   &mdash;

`public BattleStartRequest StartRequest`

:   &mdash;

`public Sha256Digest StartRequestHash`

:   &mdash;

---

## FrozenSortedIndex

```csharp
public sealed class FrozenSortedIndex
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Compilation/FrozenSortedIndex.cs</small>

A defensively copied, key-sorted immutable index.

**Constructors**

`public FrozenSortedIndex(IEnumerable<KeyValuePair<TKey, TValue>> source)`

:   &mdash;

**Properties**

`public int Count`

:   &mdash;

`public static FrozenSortedIndex<TKey, TValue> Empty`

:   &mdash;

**Methods**

`public IEnumerator<KeyValuePair<TKey, TValue>> GetEnumerator()`

:   &mdash;

`public bool TryGetValue(TKey key, out TValue value)`

:   &mdash;

---

