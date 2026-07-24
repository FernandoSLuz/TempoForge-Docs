# Analysis and balancing

13 types in this area.

!!! abstract "On this page"
    [AnalysisDiagnosticIds](#analysisdiagnosticids) &middot; [AnalysisLimits](#analysislimits) &middot; [BatchExport](#batchexport) &middot; [BatchOutcomeKind](#batchoutcomekind) &middot; [BatchSeedPlan](#batchseedplan) &middot; [BattleBatchAggregate](#battlebatchaggregate) &middot; [BattleBatchLimits](#battlebatchlimits) &middot; [BattleBatchRequest](#battlebatchrequest) &middot; [BattleBatchResult](#battlebatchresult) &middot; [BattleBatchRunner](#battlebatchrunner) &middot; [BattleOutcomeRecord](#battleoutcomerecord) &middot; [SingleBattleReproduction](#singlebattlereproduction) &middot; [TeamWinCount](#teamwincount)

## AnalysisDiagnosticIds

```csharp
public static class AnalysisDiagnosticIds
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/AnalysisDiagnostics.cs</small>

Permanent diagnostic identifiers for analysis batch contract 1. These
IDs never change once shipped; new failure modes receive new IDs.

---

## AnalysisLimits

```csharp
public static class AnalysisLimits
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

Structural limits for analysis batch contract 1. Caps are checked with
checked arithmetic before any dependent allocation.

---

## BatchExport

```csharp
public static class BatchExport
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchExport.cs</small>

Deterministic CSV and JSON text generation for batch results. Export is
text only; no file dialog, path choice, or I/O lives in this assembly.
Both encoders use invariant culture, `\n` line endings, and ASCII
output, so equal results export byte-identically across cultures,
platforms, and worker counts.

**Methods**

`public static string WriteCsv(BattleBatchResult result)`

:   &mdash;

`public static string WriteJson(BattleBatchResult result)`

:   &mdash;

---

## BatchOutcomeKind

```csharp
public enum BatchOutcomeKind
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

The recorded stop reason of one batch battle.

| Value | Meaning |
| --- | --- |
| `Terminal` | &mdash; |
| `RootActionLimit` | &mdash; |
| `TickLimit` | &mdash; |
| `CommandLimit` | &mdash; |
| `NoScheduledWork` | &mdash; |
| `FatalInvariant` | &mdash; |

---

## BatchSeedPlan

```csharp
public sealed class BatchSeedPlan
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

An immutable deduplicated ascending seed list. Construction failures
(negative counts, ranges that would wrap past UInt32.MaxValue, and the
65,536-seed cap) are retained on the plan and surfaced as the typed
`analysis.request.invalid` failure through the batch request gate
instead of throwing.

**Properties**

`public FrozenList<uint> Seeds`

:   &mdash;

**Methods**

`public static BatchSeedPlan FromRange(uint firstSeed, int count)`

:   &mdash;

`public static BatchSeedPlan FromSeeds(IEnumerable<uint> seeds)`

:   &mdash;

---

## BattleBatchAggregate

```csharp
public sealed class BattleBatchAggregate
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

The deterministic single-threaded ordered reduction over the sorted
records of one completed batch.

**Properties**

`public int BattleCount`

:   &mdash;

`public int CommandLimitCount`

:   &mdash;

`public int ConcessionCount`

:   &mdash;

`public int DrawCount`

:   &mdash;

`public int FatalInvariantCount`

:   &mdash;

`public long MaximumFinalTick`

:   &mdash;

`public long MinimumFinalTick`

:   &mdash;

`public int NoScheduledWorkCount`

:   &mdash;

`public Sha256Digest RecordSetHash`

:   &mdash;

`public int RootActionLimitCount`

:   &mdash;

`public int StalledCount`

:   &mdash;

`public FrozenList<TeamWinCount> TeamWins`

:   &mdash;

`public int TickLimitCount`

:   &mdash;

`public long TotalDamageDealt`

:   &mdash;

`public long TotalFinalTicks`

:   &mdash;

`public long TotalHealingDone`

:   &mdash;

`public ulong TotalRootActions`

:   &mdash;

---

## BattleBatchLimits

```csharp
public sealed class BattleBatchLimits
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

Per-battle stopping bounds. Out-of-range values are retained and
surfaced as the typed request-gate failure instead of throwing.

**Constructors**

`public BattleBatchLimits()`

:   &mdash;

`public BattleBatchLimits()`

:   &mdash;

**Properties**

`public int CancellationPollRootActionInterval`

:   &mdash;

`public int MaximumRootActionsPerBattle`

:   &mdash;

`public long MaximumTicksPerBattle`

:   &mdash;

---

## BattleBatchRequest

```csharp
public sealed class BattleBatchRequest
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

The complete immutable input of one Monte Carlo batch. Null members are
accepted here and rejected by the request gate with the permanent
`analysis.request.invalid` diagnostic before any battle or thread
starts.

**Constructors**

`public BattleBatchRequest()`

:   &mdash;

**Properties**

`public CancellationToken CancellationToken`

:   &mdash;

`public CompiledBattleContent Content`

:   &mdash;

`public BattleBatchLimits Limits`

:   &mdash;

`public BattleMechanicsRegistry MechanicsRegistry`

:   &mdash;

`public BattleSchedulerRegistry SchedulerRegistry`

:   &mdash;

`public BatchSeedPlan SeedPlan`

:   &mdash;

`public BattleStartRequest StartRequest`

:   &mdash;

---

## BattleBatchResult

```csharp
public sealed class BattleBatchResult
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

The complete immutable result of one batch execution. Request-level
failures carry a diagnostic and nothing else; cancelled batches keep
every fully completed record and no aggregate.

**Properties**

`public BattleBatchAggregate Aggregate`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public FrozenList<BattleOutcomeRecord> Records`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public bool WasCancelled`

:   &mdash;

---

## BattleBatchRunner

```csharp
public sealed class BattleBatchRunner
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BattleBatchRunner.cs</small>

The deterministic scripted AI-versus-AI Monte Carlo runner. Instances
hold no state; `un` and `unParallel` are pure
functions of the request, and for the same request both produce
byte-identical records, aggregate, record-set hash, CSV, and JSON
regardless of worker count, scheduling, or processor count.

**Methods**

`public BattleBatchResult Run(BattleBatchRequest request)`

:   Runs every planned seed synchronously on the caller thread.

`public BattleBatchResult RunParallel(BattleBatchRequest request, int workerCount)`

:   Runs the planned seeds on worker threads owned by this call. Workers execute whole battles only, share no mutable state, and deliver completed immutable records that are merged and sorted by seed before the single-threaded ordered aggregation.

`public SingleBattleReproduction RunSingleForReproduction(BattleBatchRequest request, uint seed)`

:   Reruns one seed through the identical per-battle algorithm the batch loop uses and additionally captures the strict replay envelope bytes from the same engine. Invalid requests throw the request-gate diagnostic as an `rgumentException`; cancellation throws `perationCanceledException`.

---

## BattleOutcomeRecord

```csharp
public sealed class BattleOutcomeRecord : IEquatable<BattleOutcomeRecord>
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

The immutable outcome of one batch battle. Records reference no engine,
snapshot, event list, or trace. The optional `iagnostic`
exists only on `atchOutcomeKind.FatalInvariant` records and
is excluded from CSV, JSON, and `RecordSetHash`.

**Constructors**

`public BattleOutcomeRecord()`

:   &mdash;

**Properties**

`public ulong CompletedRootActions`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public int EventCount`

:   &mdash;

`public Sha256Digest FinalEventChainHash`

:   &mdash;

`public Sha256Digest FinalStateHash`

:   &mdash;

`public long FinalTick`

:   &mdash;

`public BatchOutcomeKind Kind`

:   &mdash;

`public StableId? LosingTeamId`

:   &mdash;

`public StableId? ResultId`

:   &mdash;

`public uint Seed`

:   &mdash;

`public int SurvivingCombatants`

:   &mdash;

`public long TotalDamageDealt`

:   &mdash;

`public long TotalHealingDone`

:   &mdash;

`public StableId? WinningTeamId`

:   &mdash;

**Methods**

`public bool Equals(BattleOutcomeRecord other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## SingleBattleReproduction

```csharp
public sealed class SingleBattleReproduction
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

A single-seed rerun derived by the exact batch per-battle algorithm plus
the strict replay bytes captured from the same engine.

**Properties**

`public BattleOutcomeRecord Record`

:   &mdash;

`public byte[] ReplayBytes`

:   &mdash;

---

## TeamWinCount

```csharp
public sealed class TeamWinCount
```

`TempoForge.Analysis` &middot; <small>Runtime/Analysis/BatchContracts.cs</small>

One winning team and how many batch records it won.

**Properties**

`public StableId TeamId`

:   &mdash;

`public int Wins`

:   &mdash;

---

