# Numerics and determinism

7 types in this area.

!!! abstract "On this page"
    [Chance64](#chance64) &middot; [DeterministicRng](#deterministicrng) &middot; [Diagnostic](#diagnostic) &middot; [Fixed64](#fixed64) &middot; [FrozenList](#frozenlist) &middot; [Sha256Digest](#sha256digest) &middot; [StableId](#stableid)

## Chance64

:material-star: **Start here**

```csharp
public readonly struct Chance64 : IEquatable<Chance64>, IComparable<Chance64>
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Numerics/Chance64.cs</small>

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

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Numerics/DeterministicRng.cs</small>

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

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Common/Diagnostic.cs</small>

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

## Fixed64

:material-star: **Start here**

```csharp
public readonly struct Fixed64 : IEquatable<Fixed64>, IComparable<Fixed64>
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Numerics/Fixed64.cs</small>

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

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Common/FrozenList.cs</small>

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

## Sha256Digest

```csharp
public readonly struct Sha256Digest : IEquatable<Sha256Digest>
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Canonical/Sha256Digest.cs</small>

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

:material-star: **Start here**

```csharp
public readonly struct StableId : IEquatable<StableId>, IComparable<StableId>
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Common/StableId.cs</small>

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

