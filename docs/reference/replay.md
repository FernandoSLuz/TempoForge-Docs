# Replay

10 types in this area.

!!! abstract "On this page"
    [IReplayMigration](#ireplaymigration) &middot; [ReplayDivergenceHashKind](#replaydivergencehashkind) &middot; [ReplayEnvelope](#replayenvelope) &middot; [ReplayExecutionResult](#replayexecutionresult) &middot; [ReplayExecutor](#replayexecutor) &middot; [ReplayMigrationChain](#replaymigrationchain) &middot; [ReplayMigrationResult](#replaymigrationresult) &middot; [ReplayReadResult](#replayreadresult) &middot; [ReplaySerializer](#replayserializer) &middot; [ReplayWriteException](#replaywriteexception)

## IReplayMigration

```csharp
public interface IReplayMigration
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayMigration.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ReplayDivergenceHashKind

```csharp
public enum ReplayDivergenceHashKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayExecutor.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `None` | &mdash; |
| `CommandEvent` | &mdash; |
| `State` | &mdash; |
| `EventChain` | &mdash; |
| `PreCommandState` | &mdash; |

---

## ReplayEnvelope

```csharp
public sealed class ReplayEnvelope
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayEnvelope.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int? AiRegistryVersion`

:   &mdash;

`public int CanonicalVersion`

:   &mdash;

`public FrozenList<ReplayCheckpoint> Checkpoints`

:   &mdash;

`public int CommandVersion`

:   &mdash;

`public FrozenList<RecordedCommand> Commands`

:   &mdash;

`public int CompiledSchemaVersion`

:   &mdash;

`public byte[] CompiledSnapshot`

:   &mdash;

`public Sha256Digest CompiledSnapshotHash`

:   &mdash;

`public Sha256Digest ContentManifestHash`

:   &mdash;

`public CompiledBattleContent DecodedContent`

:   &mdash;

`public BattleStartRequest DecodedStartRequest`

:   &mdash;

`public int? EffectRegistryVersion`

:   &mdash;

`public int EngineVersion`

:   &mdash;

`public int EventVersion`

:   &mdash;

`public int ExecutionVersion`

:   &mdash;

`public ReplayCheckpoint FinalCheckpoint`

:   &mdash;

`public int FormatVersion`

:   &mdash;

`public int? FormulaRegistryVersion`

:   &mdash;

`public int NumericVersion`

:   &mdash;

`public SimulationContractProfile Profile`

:   &mdash;

`public int? ReactionRegistryVersion`

:   &mdash;

`public Sha256Digest RegistryBindingHash`

:   &mdash;

`public int RngVersion`

:   &mdash;

`public int? SchedulerVersion`

:   &mdash;

`public uint Seed`

:   &mdash;

`public byte[] StartRequest`

:   &mdash;

`public Sha256Digest StartRequestHash`

:   &mdash;

`public int? TargetRegistryVersion`

:   &mdash;

**Methods**

`public static ReplayEnvelope Capture(BattleEngine engine)`

:   &mdash;

`public static ReplayEnvelope Capture()`

:   &mdash;

---

## ReplayExecutionResult

```csharp
public sealed class ReplayExecutionResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayExecutor.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Sha256Digest? ActualHash`

:   &mdash;

`public FrozenList<AiDecisionTrace> AiDecisionTraces`

:   Consumer-owned decision evidence produced while replay execution revalidated automatic commands. It is intentionally outside the canonical battle state and replay hashes.

`public int CheckpointIndex`

:   &mdash;

`public int CommandIndex`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public Sha256Digest? ExpectedHash`

:   &mdash;

`public FrozenList<FormulaAttributionTrace> FormulaAttributionTraces`

:   &mdash;

`public FormulaAttributionTraceBatch FormulaAttributions`

:   &mdash;

`public ReplayDivergenceHashKind HashKind`

:   &mdash;

`public long OmittedFormulaAttributionTraceCount`

:   &mdash;

`public BattleSnapshot Snapshot`

:   &mdash;

`public bool Succeeded`

:   &mdash;

---

## ReplayExecutor

```csharp
public static class ReplayExecutor
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayExecutor.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Methods**

`public static ReplayExecutionResult Execute(ReplayEnvelope replay)`

:   &mdash;

`public static ReplayExecutionResult Execute()`

:   &mdash;

`public static ReplayExecutionResult Execute()`

:   &mdash;

---

## ReplayMigrationChain

```csharp
public sealed class ReplayMigrationChain
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayMigration.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReplayMigrationChain(IEnumerable<IReplayMigration> migrations)`

:   &mdash;

**Methods**

`public ReplayMigrationResult Migrate(byte[] immutableInput, int fromVersion, int targetVersion)`

:   &mdash;

---

## ReplayMigrationResult

```csharp
public sealed class ReplayMigrationResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayMigration.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public byte[] Bytes`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public bool Succeeded`

:   &mdash;

**Methods**

`public static ReplayMigrationResult Failure(Diagnostic diagnostic)`

:   &mdash;

`public static ReplayMigrationResult Success(byte[] bytes)`

:   &mdash;

---

## ReplayReadResult

```csharp
public sealed class ReplayReadResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplayEnvelope.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Diagnostic? Diagnostic`

:   &mdash;

`public ReplayEnvelope Replay`

:   &mdash;

`public bool Succeeded`

:   &mdash;

---

## ReplaySerializer

```csharp
public static class ReplaySerializer
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/ReplaySerializer.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Methods**

`public static ReplayReadResult Read(byte[] utf8)`

:   &mdash;

`public static ReplayReadResult Read()`

:   &mdash;

`public static byte[] Write(ReplayEnvelope replay)`

:   &mdash;

---

## ReplayWriteException

```csharp
public sealed class ReplayWriteException : InvalidOperationException
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Replay/StrictJson.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReplayWriteException(StableId diagnosticId, string message)`

:   &mdash;

**Properties**

`public Diagnostic Diagnostic`

:   &mdash;

---

