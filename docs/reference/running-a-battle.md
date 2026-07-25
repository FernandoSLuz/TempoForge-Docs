# Running a battle

11 types in this area.

!!! abstract "On this page"
    [AdvanceTicksOutcome](#advanceticksoutcome) &middot; [AdvanceTicksResult](#advanceticksresult) &middot; [BattleEngine](#battleengine) &middot; [BattleResultState](#battleresultstate) &middot; [BattleStartRequest](#battlestartrequest) &middot; [CommandDisposition](#commanddisposition) &middot; [CommandResult](#commandresult) &middot; [StepActionOutcome](#stepactionoutcome) &middot; [StepActionResult](#stepactionresult) &middot; [StepEventOutcome](#stepeventoutcome) &middot; [StepEventResult](#stepeventresult)

## AdvanceTicksOutcome

:material-star: **Start here**

```csharp
public enum AdvanceTicksOutcome
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `ReachedTarget` | &mdash; |
| `AwaitingCommand` | &mdash; |
| `Terminal` | &mdash; |
| `NoScheduledWork` | &mdash; |
| `FatalInvariant` | &mdash; |

---

## AdvanceTicksResult

:material-star: **Start here**

```csharp
public sealed class AdvanceTicksResult
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AiDecisionTrace> AiDecisionTraces`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public FrozenList<BattleEvent> Events`

:   &mdash;

`public FrozenList<FormulaAttributionTrace> FormulaAttributionTraces`

:   &mdash;

`public FormulaAttributionTraceBatch FormulaAttributions`

:   &mdash;

`public long OmittedFormulaAttributionTraceCount`

:   &mdash;

`public AdvanceTicksOutcome Outcome`

:   &mdash;

`public BattleSnapshot Snapshot`

:   &mdash;

`public long TargetTick`

:   &mdash;

---

## BattleEngine

:material-star: **Start here**

```csharp
public sealed partial class BattleEngine
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.B2.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public BattleCommand Command`

:   &mdash;

`public CompiledBattleContent Content`

:   &mdash;

`public int DrawCount`

:   &mdash;

`public BattleMechanicsRegistry MechanicsRegistry`

:   &mdash;

`public SimulationContractProfile Profile`

:   &mdash;

`public int RecordedCommandCount`

:   &mdash;

`public DeterministicRng RngAfterSelection`

:   &mdash;

`public uint Seed`

:   &mdash;

`public BattleStartRequest StartRequest`

:   &mdash;

`public AiDecisionTrace Trace`

:   &mdash;

**Fields**

`public List<ActiveActionState> ActiveActions`

:   &mdash;

`public StableId? B1PendingDecisionActorId`

:   &mdash;

`public List<CombatantState> Combatants`

:   &mdash;

`public ulong CompletedRootActionCount`

:   &mdash;

`public Sha256Digest ContentManifestHash`

:   &mdash;

`public List<CooldownState> Cooldowns`

:   &mdash;

`public Sha256Digest EventChainHash`

:   &mdash;

`public List<ExecutionFrame> Frames`

:   &mdash;

`public ulong NextActionSequence`

:   &mdash;

`public ulong NextApplicationSequence`

:   &mdash;

`public ulong NextCommandSequence`

:   &mdash;

`public ulong NextEventSequence`

:   &mdash;

`public ulong NextOpportunitySequence`

:   &mdash;

`public ulong NextReactionSequence`

:   &mdash;

`public SimulationContractProfile Profile`

:   &mdash;

`public List<ReactionRootBudgetState> ReactionRoots`

:   &mdash;

`public Sha256Digest RegistryBindingHash`

:   &mdash;

`public List<ResourceState> Resources`

:   &mdash;

`public BattleResultState Result`

:   &mdash;

`public DeterministicRng Rng`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public SchedulerState SchedulerState`

:   &mdash;

`public List<ShieldState> Shields`

:   &mdash;

`public List<CombatantStatState> Stats`

:   &mdash;

`public List<StatusInstanceState> Statuses`

:   &mdash;

`public List<SystemStatusActionState> SystemStatusActions`

:   &mdash;

`public List<TeamState> Teams`

:   &mdash;

`public long Tick`

:   &mdash;

**Methods**

`public void AddPeriodicCheckpoint(ReplayCheckpoint checkpoint)`

:   &mdash;

`public void AddRecordedCommand(RecordedCommand command)`

:   &mdash;

`public AdvanceTicksResult AdvanceTicks(int count)`

:   &mdash;

`public BattleSnapshot Build()`

:   &mdash;

`public BattleEngine Clone()`

:   &mdash;

`public static BattleEngine Create()`

:   &mdash;

`public static BattleEngine Create()`

:   &mdash;

`public static BattleEngine Create()`

:   &mdash;

`public FrozenList<AiDecisionTrace> DrainAiDecisionTraces()`

:   &mdash;

`public FormulaAttributionTraceBatch DrainFormulaAttributionTraces()`

:   &mdash;

`public BattleSnapshot GetSnapshot()`

:   &mdash;

`public uint NextBelow(uint exclusiveUpperBound)`

:   &mdash;

`public static BattleEngine Restore()`

:   &mdash;

`public static BattleEngine Restore()`

:   &mdash;

`public static BattleEngine Restore()`

:   &mdash;

`public FrozenList<BattleEvent> RunUntilBoundary()`

:   &mdash;

`public StepActionResult StepAction()`

:   &mdash;

`public StepEventResult StepEvent()`

:   &mdash;

`public CommandResult Submit(BattleCommand command)`

:   &mdash;

---

## BattleResultState

:material-star: **Start here**

```csharp
public sealed class BattleResultState
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public BattleResultState(bool terminal, StableId resultId, StableId winningTeamId, StableId losingTeamId)`

:   &mdash;

**Properties**

`public bool IsTerminal`

:   &mdash;

`public StableId? LosingTeamId`

:   &mdash;

`public StableId? ResultId`

:   &mdash;

`public StableId? WinningTeamId`

:   &mdash;

**Methods**

`public static BattleResultState Concession()`

:   &mdash;

`public static BattleResultState Defeat()`

:   &mdash;

`public static BattleResultState Draw()`

:   &mdash;

`public static BattleResultState Stalled()`

:   &mdash;

`public static BattleResultState Victory()`

:   &mdash;

---

## BattleStartRequest

:material-star: **Start here**

```csharp
public sealed partial class BattleStartRequest
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/BattleStartV3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public BattleStartRequest(StableId schedulerId, IEnumerable<StartTeam> teams)`

:   &mdash;

**Properties**

`public int CompiledSchemaVersion`

:   &mdash;

`public int EngineVersion`

:   &mdash;

`public StableId? PerspectiveTeamId`

:   &mdash;

`public SimulationContractProfile Profile`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public FrozenList<StartTeam> Teams`

:   &mdash;

`public FrozenList<StartTeamV3> TeamsV3`

:   &mdash;

**Methods**

`public static BattleStartRequest CreateB2()`

:   &mdash;

`public static BattleStartRequest CreateB3()`

:   &mdash;

`public static BattleStartRequest CreateB3()`

:   &mdash;

`public static B3CreationResult<BattleStartRequest> TryCreateB3()`

:   &mdash;

`public static B3CreationResult<BattleStartRequest> TryCreateB3()`

:   &mdash;

---

## CommandDisposition

```csharp
public enum CommandDisposition
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `TransportRejected` | &mdash; |
| `Accepted` | &mdash; |
| `Rejected` | &mdash; |
| `FatalInvariant` | &mdash; |

---

## CommandResult

```csharp
public sealed class CommandResult
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AiDecisionTrace> AiDecisionTraces`

:   &mdash;

`public BattleEvent CommandEvent`

:   &mdash;

`public Sha256Digest? CommandEventHash`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public CommandDisposition Disposition`

:   &mdash;

`public FrozenList<FormulaAttributionTrace> FormulaAttributionTraces`

:   &mdash;

`public FormulaAttributionTraceBatch FormulaAttributions`

:   &mdash;

`public long OmittedFormulaAttributionTraceCount`

:   &mdash;

`public StableId? ReasonId`

:   &mdash;

`public BattleSnapshot Snapshot`

:   &mdash;

---

## StepActionOutcome

```csharp
public enum StepActionOutcome
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `ActionCompleted` | &mdash; |
| `AwaitingCommand` | &mdash; |
| `RejectedCommand` | &mdash; |
| `Terminal` | &mdash; |
| `NoScheduledWork` | &mdash; |
| `FatalInvariant` | &mdash; |

---

## StepActionResult

```csharp
public sealed class StepActionResult
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AiDecisionTrace> AiDecisionTraces`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public FrozenList<BattleEvent> Events`

:   &mdash;

`public FrozenList<FormulaAttributionTrace> FormulaAttributionTraces`

:   &mdash;

`public FormulaAttributionTraceBatch FormulaAttributions`

:   &mdash;

`public long OmittedFormulaAttributionTraceCount`

:   &mdash;

`public StepActionOutcome Outcome`

:   &mdash;

`public BattleSnapshot Snapshot`

:   &mdash;

---

## StepEventOutcome

```csharp
public enum StepEventOutcome
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `EventEmitted` | &mdash; |
| `AwaitingCommand` | &mdash; |
| `Terminal` | &mdash; |
| `NoScheduledWork` | &mdash; |
| `FatalInvariant` | &mdash; |

---

## StepEventResult

```csharp
public sealed class StepEventResult
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Engine/BattleEngine.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<AiDecisionTrace> AiDecisionTraces`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public BattleEvent Event`

:   &mdash;

`public FrozenList<FormulaAttributionTrace> FormulaAttributionTraces`

:   &mdash;

`public FormulaAttributionTraceBatch FormulaAttributions`

:   &mdash;

`public long OmittedFormulaAttributionTraceCount`

:   &mdash;

`public StepEventOutcome Outcome`

:   &mdash;

`public BattleSnapshot Snapshot`

:   &mdash;

---

