# Numerics and determinism

16 types in this area.

!!! abstract "On this page"
    [B3CreationDiagnostic](#b3creationdiagnostic) &middot; [B3CreationResult](#b3creationresult) &middot; [B3CreationStage](#b3creationstage) &middot; [CanonicalBattleSerializer](#canonicalbattleserializer) &middot; [CanonicalReadException](#canonicalreadexception) &middot; [CanonicalReader](#canonicalreader) &middot; [CanonicalWriter](#canonicalwriter) &middot; [Chance64](#chance64) &middot; [DeterministicRng](#deterministicrng) &middot; [Diagnostic](#diagnostic) &middot; [DiagnosticIds](#diagnosticids) &middot; [Fixed64](#fixed64) &middot; [FrozenList](#frozenlist) &middot; [RngState](#rngstate) &middot; [Sha256Digest](#sha256digest) &middot; [StableId](#stableid)

## B3CreationDiagnostic

```csharp
public sealed class B3CreationDiagnostic : IEquatable<B3CreationDiagnostic>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Common/B3Creation.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int? AuthoredOrdinal`

:   &mdash;

`public Diagnostic Diagnostic`

:   &mdash;

`public StableId? OwnerId`

:   &mdash;

`public StableId? RelatedId`

:   &mdash;

`public B3CreationStage Stage`

:   &mdash;

**Methods**

`public bool Equals(B3CreationDiagnostic other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

`public override string ToString()`

:   &mdash;

---

## B3CreationResult

```csharp
public sealed class B3CreationResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Common/B3Creation.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<B3CreationDiagnostic> Diagnostics`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public T Value`

:   &mdash;

---

## B3CreationStage

```csharp
public enum B3CreationStage : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Common/B3Creation.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Definition` | &mdash; |
| `Reference` | &mdash; |
| `Registry` | &mdash; |
| `ReactionGraph` | &mdash; |
| `Start` | &mdash; |
| `Canonical` | &mdash; |

---

## CanonicalBattleSerializer

```csharp
public static partial class CanonicalBattleSerializer
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Canonical/CanonicalBattleSerializer.B3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public static Sha256Digest EmptyEventChain`

:   &mdash;

**Methods**

`public static Sha256Digest AdvanceEventChain(Sha256Digest previous, BattleEvent battleEvent)`

:   &mdash;

`public static BattleSnapshot DecodeBattleState(byte[] bytes)`

:   &mdash;

`public static BattleSnapshot DecodeBattleState()`

:   &mdash;

`public static CompiledBattleContent DecodeCompiledSnapshot(byte[] bytes)`

:   &mdash;

`public static CompiledBattleContent DecodeCompiledSnapshot()`

:   &mdash;

`public static BattleStartRequest DecodeStartRequest(byte[] bytes)`

:   &mdash;

`public static byte[] EncodeBattleState(BattleSnapshot snapshot)`

:   &mdash;

`public static byte[] EncodeBattleState()`

:   &mdash;

`public static byte[] EncodeCommand(BattleCommand command)`

:   &mdash;

`public static byte[] EncodeCompiledSnapshot(CompiledBattleContent content)`

:   &mdash;

`public static byte[] EncodeEvent(BattleEvent battleEvent)`

:   &mdash;

`public static byte[] EncodeFormulaAttribution(FormulaAttribution attribution)`

:   &mdash;

`public static byte[] EncodeStartRequest(BattleStartRequest start)`

:   &mdash;

`public static Sha256Digest HashBattleState(BattleSnapshot snapshot)`

:   &mdash;

`public static Sha256Digest HashBattleState()`

:   &mdash;

`public static Sha256Digest HashCommand(BattleCommand command)`

:   &mdash;

`public static Sha256Digest HashCompiledSnapshot(CompiledBattleContent content)`

:   &mdash;

`public static Sha256Digest HashContentManifest(CompiledBattleContent content)`

:   &mdash;

`public static Sha256Digest HashEvent(BattleEvent battleEvent)`

:   &mdash;

`public static Sha256Digest HashFormulaAttribution(FormulaAttribution attribution)`

:   &mdash;

`public static Sha256Digest HashPropertySet(PropertySet properties)`

:   &mdash;

`public static Sha256Digest HashReplayCheckpoint(ReplayCheckpoint checkpoint)`

:   &mdash;

`public static Sha256Digest HashStartRequest(BattleStartRequest start)`

:   &mdash;

---

## CanonicalReadException

```csharp
public sealed class CanonicalReadException : Exception
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Canonical/CanonicalReader.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CanonicalReadException(string diagnosticId, string message)`

:   &mdash;

**Properties**

`public StableId DiagnosticId`

:   &mdash;

---

## CanonicalReader

```csharp
public sealed class CanonicalReader
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Canonical/CanonicalReader.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CanonicalReader(byte[] bytes, int totalByteLimit)`

:   &mdash;

**Properties**

`public int Remaining`

:   &mdash;

**Methods**

`public void EnsureComplete()`

:   &mdash;

`public bool ReadBool()`

:   &mdash;

`public byte ReadByte()`

:   &mdash;

`public byte[] ReadByteSequence(int maximumBytes)`

:   &mdash;

`public Fixed64 ReadFixed64()`

:   &mdash;

`public int ReadInt32()`

:   &mdash;

`public long ReadInt64()`

:   &mdash;

`public bool ReadPresence()`

:   &mdash;

`public StableId ReadStableId()`

:   &mdash;

`public string ReadString(int maximumUtf8Bytes)`

:   &mdash;

`public uint ReadUInt32()`

:   &mdash;

`public ulong ReadUInt64()`

:   &mdash;

---

## CanonicalWriter

```csharp
public sealed class CanonicalWriter
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Canonical/CanonicalWriter.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CanonicalWriter(int maximumLength = int.MaxValue)`

:   &mdash;

**Properties**

`public int Length`

:   &mdash;

**Methods**

`public Sha256Digest ComputeHash()`

:   &mdash;

`public byte[] ToArray()`

:   &mdash;

`public void WriteBool(bool value)`

:   &mdash;

`public void WriteByte(byte value)`

:   &mdash;

`public void WriteByteSequence(byte[] value)`

:   &mdash;

`public void WriteChance64(Chance64 value)`

:   &mdash;

`public void WriteFixed64(Fixed64 value)`

:   &mdash;

`public void WriteInt32(int value)`

:   &mdash;

`public void WriteInt64(long value)`

:   &mdash;

`public void WriteRawBytes(byte[] value)`

:   &mdash;

`public void WriteStableId(StableId value)`

:   &mdash;

`public void WriteString(string value)`

:   &mdash;

`public void WriteUInt32(uint value)`

:   &mdash;

`public void WriteUInt64(ulong value)`

:   &mdash;

---

## Chance64

```csharp
public readonly struct Chance64 : IEquatable<Chance64>, IComparable<Chance64>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Numerics/Chance64.cs</small>

A deterministic probability value where 1,000,000 raw units equal 100%.
This type is deliberately distinct from Fixed64.

**Constructors**

`public Chance64(long raw)`

:   &mdash;

**Properties**

`public bool IsGuaranteed`

:   &mdash;

`public bool IsImpossible`

:   &mdash;

`public long Raw`

:   &mdash;

**Methods**

`public static Chance64 ApplyResistance(Chance64 baseChance, Chance64 resistance)`

:   &mdash;

`public static Chance64 Clamp(long raw)`

:   &mdash;

`public int CompareTo(Chance64 other)`

:   &mdash;

`public bool Equals(Chance64 other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

`public static Chance64 Multiply(Chance64 left, Chance64 right)`

:   &mdash;

`public override string ToString()`

:   &mdash;

---

## DeterministicRng

```csharp
public readonly struct DeterministicRng : IEquatable<DeterministicRng>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Numerics/DeterministicRng.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public RngState State`

:   &mdash;

**Methods**

`public bool Equals(DeterministicRng other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public static DeterministicRng FromSeed(uint seed)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

`public DeterministicRng NextBelow(uint exclusiveUpperBound, out uint value)`

:   &mdash;

`public DeterministicRng NextBelow(ulong exclusiveUpperBound, out ulong value)`

:   &mdash;

`public DeterministicRng NextUInt32(out uint value)`

:   &mdash;

`public DeterministicRng SamplePercent(Fixed64 percent, out bool succeeded)`

:   &mdash;

`public static bool TryRestore(RngState restored, out DeterministicRng rng, out Diagnostic diagnostic)`

:   &mdash;

---

## Diagnostic

```csharp
public readonly struct Diagnostic : IEquatable<Diagnostic>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Common/Diagnostic.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public Diagnostic(StableId id, string detail = null)`

:   &mdash;

**Properties**

`public string Detail`

:   &mdash;

`public StableId Id`

:   &mdash;

**Methods**

`public bool Equals(Diagnostic other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

`public override string ToString()`

:   &mdash;

---

## DiagnosticIds

```csharp
public static class DiagnosticIds
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Common/Diagnostic.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## Fixed64

```csharp
public readonly struct Fixed64 : IEquatable<Fixed64>, IComparable<Fixed64>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Numerics/Fixed64.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public Fixed64(long raw)`

:   &mdash;

**Properties**

`public long Raw`

:   &mdash;

**Methods**

`public static Fixed64 Abs(Fixed64 value)`

:   &mdash;

`public static Fixed64 Add(Fixed64 left, Fixed64 right)`

:   &mdash;

`public int CompareTo(Fixed64 other)`

:   &mdash;

`public static Fixed64 Divide(Fixed64 left, Fixed64 right)`

:   &mdash;

`public bool Equals(Fixed64 other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public static Fixed64 FromInt32(int value)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

`public static Fixed64 Multiply(Fixed64 left, Fixed64 right)`

:   &mdash;

`public static Fixed64 Negate(Fixed64 value)`

:   &mdash;

`public static Fixed64 ParseInvariant(string text)`

:   &mdash;

`public static Fixed64 Subtract(Fixed64 left, Fixed64 right)`

:   &mdash;

`public int ToInt32Clamped(int minimum, int maximum)`

:   &mdash;

`public long ToInt64Rounded()`

:   &mdash;

`public override string ToString()`

:   &mdash;

`public static bool TryParseInvariant(string text, out Fixed64 result)`

:   &mdash;

---

## FrozenList

```csharp
public sealed class FrozenList
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Common/FrozenList.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FrozenList(IEnumerable<T> source)`

:   &mdash;

`public FrozenList(params T[] source)`

:   &mdash;

**Properties**

`public int Count`

:   &mdash;

`public static FrozenList<T> Empty`

:   &mdash;

**Methods**

`public IEnumerator<T> GetEnumerator()`

:   &mdash;

`public T[] ToArray()`

:   &mdash;

---

## RngState

```csharp
public readonly struct RngState : IEquatable<RngState>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Numerics/DeterministicRng.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public RngState(uint s0, uint s1, uint s2, uint s3)`

:   &mdash;

**Properties**

`public bool IsZero`

:   &mdash;

`public uint S0`

:   &mdash;

`public uint S1`

:   &mdash;

`public uint S2`

:   &mdash;

`public uint S3`

:   &mdash;

**Methods**

`public bool Equals(RngState other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## Sha256Digest

```csharp
public readonly struct Sha256Digest : IEquatable<Sha256Digest>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Canonical/Sha256Digest.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public bool IsValid`

:   &mdash;

**Methods**

`public static Sha256Digest Compute(byte[] data)`

:   &mdash;

`public bool Equals(Sha256Digest other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public static Sha256Digest FromBytes(byte[] source)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

`public byte[] ToByteArray()`

:   &mdash;

`public override string ToString()`

:   &mdash;

`public static bool TryParse(string text, out Sha256Digest digest)`

:   &mdash;

---

## StableId

```csharp
public readonly struct StableId : IEquatable<StableId>, IComparable<StableId>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Common/StableId.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StableId(string value)`

:   &mdash;

**Properties**

`public bool IsValid`

:   &mdash;

`public string Value`

:   &mdash;

**Methods**

`public int CompareTo(StableId other)`

:   &mdash;

`public bool Equals(StableId other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

`public static bool IsValidText(string text)`

:   &mdash;

`public override string ToString()`

:   &mdash;

`public static bool TryParse(string text, out StableId id)`

:   &mdash;

---

