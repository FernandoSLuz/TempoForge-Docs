# Scheduling and tempo

52 types in this area.

!!! abstract "On this page"
    [ActionCostPaymentPolicy](#actioncostpaymentpolicy) &middot; [ActionOrderScheduler](#actionorderscheduler) &middot; [ActionOrderSchedulerAdjustmentAdapter](#actionorderscheduleradjustmentadapter) &middot; [ActionOrderSchedulerStateCodec](#actionorderschedulerstatecodec) &middot; [ActionOrderState](#actionorderstate) &middot; [AtbScheduler](#atbscheduler) &middot; [AtbSchedulerAdjustmentAdapter](#atbscheduleradjustmentadapter) &middot; [AtbSchedulerStateCodec](#atbschedulerstatecodec) &middot; [AtbState](#atbstate) &middot; [AutomaticTargetMode](#automatictargetmode) &middot; [BattleClock](#battleclock) &middot; [BattleForecast](#battleforecast) &middot; [BattleSchedulerRegistry](#battleschedulerregistry) &middot; [BattleSchedulerResolveResult](#battleschedulerresolveresult) &middot; [CompiledActionCost](#compiledactioncost) &middot; [CompiledAutomaticDecisionPolicy](#compiledautomaticdecisionpolicy) &middot; [CompiledSchedulerDefinition](#compiledschedulerdefinition) &middot; [CompiledSkillTiming](#compiledskilltiming) &middot; [CooldownClockKind](#cooldownclockkind) &middot; [CooldownStartPolicy](#cooldownstartpolicy) &middot; [GaugeEntry](#gaugeentry) &middot; [IBattleScheduler](#ibattlescheduler) &middot; [ISchedulerAdjustmentAdapter](#ischeduleradjustmentadapter) &middot; [ISchedulerAdjustmentAdapterProvider](#ischeduleradjustmentadapterprovider) &middot; [ISchedulerStateCodec](#ischedulerstatecodec) &middot; [ISchedulerStateCodecProvider](#ischedulerstatecodecprovider) &middot; [InputPausePolicy](#inputpausepolicy) &middot; [InterruptRefundPolicy](#interruptrefundpolicy) &middot; [ReadyTickEntry](#readytickentry) &middot; [RoundState](#roundstate) &middot; [SchedulerAdjustmentContext](#scheduleradjustmentcontext) &middot; [SchedulerAdjustmentResult](#scheduleradjustmentresult) &middot; [SchedulerAdvanceContext](#scheduleradvancecontext) &middot; [SchedulerAdvanceResult](#scheduleradvanceresult) &middot; [SchedulerAdvanceStopReason](#scheduleradvancestopreason) &middot; [SchedulerCombatantTimingView](#schedulercombatanttimingview) &middot; [SchedulerCreateContext](#schedulercreatecontext) &middot; [SchedulerCreateResult](#schedulercreateresult) &middot; [SchedulerDiagnosticIds](#schedulerdiagnosticids) &middot; [SchedulerDueTimer](#schedulerduetimer) &middot; [SchedulerDueTimerKind](#schedulerduetimerkind) &middot; [SchedulerIds](#schedulerids) &middot; [SchedulerOpportunityContext](#scheduleropportunitycontext) &middot; [SchedulerOpportunityOutcome](#scheduleropportunityoutcome) &middot; [SchedulerOpportunityResult](#scheduleropportunityresult) &middot; [SchedulerState](#schedulerstate) &middot; [SchedulerStateDecodeResult](#schedulerstatedecoderesult) &middot; [SchedulerStateTag](#schedulerstatetag) &middot; [SchedulerTransitionResult](#schedulertransitionresult) &middot; [SchedulerWork](#schedulerwork) &middot; [SchedulerWorkTag](#schedulerworktag) &middot; [TimingResolutionKind](#timingresolutionkind)

## ActionCostPaymentPolicy

```csharp
public enum ActionCostPaymentPolicy : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Acceptance` | &mdash; |

---

## ActionOrderScheduler

```csharp
public sealed class ActionOrderScheduler : IBattleScheduler, ISchedulerStateCodecProvider
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/ActionOrderScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public bool IsSchedulerReadiness`

:   &mdash;

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public ISchedulerStateCodec StateCodec`

:   &mdash;

`public SchedulerAdvanceStopReason StopReason`

:   &mdash;

`public long Tick`

:   &mdash;

**Methods**

`public SchedulerAdvanceResult Advance()`

:   &mdash;

`public SchedulerCreateResult Create(SchedulerCreateContext context)`

:   &mdash;

`public SchedulerTransitionResult OnOpportunityAccepted()`

:   &mdash;

`public SchedulerTransitionResult OnOpportunityFinished()`

:   &mdash;

---

## ActionOrderSchedulerAdjustmentAdapter

```csharp
public sealed class ActionOrderSchedulerAdjustmentAdapter : ISchedulerAdjustmentAdapter
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerAdjustment.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

**Methods**

`public SchedulerAdjustmentResult Apply()`

:   &mdash;

`public bool Supports(SchedulerAdjustmentKind kind)`

:   &mdash;

---

## ActionOrderSchedulerStateCodec

```csharp
public sealed class ActionOrderSchedulerStateCodec : ISchedulerStateCodec
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/BattleSchedulerRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public SchedulerStateTag StateTag`

:   &mdash;

**Methods**

`public bool CanHandle(SchedulerState state)`

:   &mdash;

`public SchedulerStateDecodeResult DecodePayload(byte[] payload)`

:   &mdash;

`public byte[] EncodePayload(SchedulerState state)`

:   &mdash;

---

## ActionOrderState

```csharp
public sealed class ActionOrderState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ActionOrderState()`

:   &mdash;

**Properties**

`public FrozenList<ReadyTickEntry> ReadyTicks`

:   &mdash;

`public RoundState Round`

:   &mdash;

`public ulong RoundIndex`

:   &mdash;

**Methods**

`public ReadyTickEntry FindReadyTick(StableId actorId)`

:   &mdash;

---

## AtbScheduler

```csharp
public sealed class AtbScheduler : IBattleScheduler, ISchedulerStateCodecProvider
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/AtbScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public StableId ActorId`

:   &mdash;

`public long GaugeUnits`

:   &mdash;

`public long RecoveryLockUntilTick`

:   &mdash;

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public ISchedulerStateCodec StateCodec`

:   &mdash;

**Methods**

`public SchedulerAdvanceResult Advance()`

:   &mdash;

`public SchedulerCreateResult Create(SchedulerCreateContext context)`

:   &mdash;

`public SchedulerTransitionResult OnOpportunityAccepted()`

:   &mdash;

`public SchedulerTransitionResult OnOpportunityFinished()`

:   &mdash;

---

## AtbSchedulerAdjustmentAdapter

```csharp
public sealed class AtbSchedulerAdjustmentAdapter : ISchedulerAdjustmentAdapter
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerAdjustment.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

**Methods**

`public SchedulerAdjustmentResult Apply()`

:   &mdash;

`public bool Supports(SchedulerAdjustmentKind kind)`

:   &mdash;

---

## AtbSchedulerStateCodec

```csharp
public sealed class AtbSchedulerStateCodec : ISchedulerStateCodec
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/BattleSchedulerRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public SchedulerStateTag StateTag`

:   &mdash;

**Methods**

`public bool CanHandle(SchedulerState state)`

:   &mdash;

`public SchedulerStateDecodeResult DecodePayload(byte[] payload)`

:   &mdash;

`public byte[] EncodePayload(SchedulerState state)`

:   &mdash;

---

## AtbState

```csharp
public sealed class AtbState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AtbState()`

:   &mdash;

**Properties**

`public FrozenList<GaugeEntry> GaugeEntries`

:   &mdash;

`public int GaugeThresholdUnits`

:   &mdash;

`public InputPausePolicy InputPausePolicy`

:   &mdash;

**Methods**

`public GaugeEntry FindGauge(StableId actorId)`

:   &mdash;

---

## AutomaticTargetMode

```csharp
public enum AutomaticTargetMode : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `None` | &mdash; |
| `Self` | &mdash; |
| `FirstLivingOpponent` | &mdash; |

---

## BattleClock

```csharp
public static class BattleClock
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Numerics/BattleClock.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Methods**

`public static long CalculateTargetTick(long currentTick, int count)`

:   &mdash;

---

## BattleForecast

```csharp
public static class BattleForecast
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Forecast/BattleForecast.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Methods**

`public static ForecastResult Run(BattleEngine source, ForecastRequest request)`

:   &mdash;

---

## BattleSchedulerRegistry

```csharp
public sealed class BattleSchedulerRegistry
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/BattleSchedulerRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public ISchedulerAdjustmentAdapter AdjustmentAdapter`

:   &mdash;

`public IBattleScheduler Scheduler`

:   &mdash;

`public ISchedulerStateCodec StateCodec`

:   &mdash;

**Methods**

`public static BattleSchedulerRegistry CreateWithBuiltIns()`

:   &mdash;

`public BattleSchedulerRegistry Register(IBattleScheduler scheduler)`

:   &mdash;

`public BattleSchedulerRegistry Register()`

:   &mdash;

`public BattleSchedulerRegistry Register()`

:   &mdash;

`public BattleSchedulerResolveResult Resolve()`

:   &mdash;

---

## BattleSchedulerResolveResult

```csharp
public sealed class BattleSchedulerResolveResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/BattleSchedulerRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public ISchedulerAdjustmentAdapter AdjustmentAdapter`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public IBattleScheduler Scheduler`

:   &mdash;

`public ISchedulerStateCodec StateCodec`

:   &mdash;

`public bool Succeeded`

:   &mdash;

---

## CompiledActionCost

```csharp
public sealed class CompiledActionCost
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledActionCost(StableId resourceId, int amount)`

:   &mdash;

**Properties**

`public int Amount`

:   &mdash;

`public ActionCostPaymentPolicy PaymentPolicy`

:   &mdash;

`public StableId ResourceId`

:   &mdash;

---

## CompiledAutomaticDecisionPolicy

```csharp
public sealed class CompiledAutomaticDecisionPolicy
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledAutomaticDecisionPolicy()`

:   &mdash;

**Properties**

`public StableId PolicyId`

:   &mdash;

`public FrozenList<StableId> SkillIds`

:   &mdash;

`public AutomaticTargetMode TargetMode`

:   &mdash;

---

## CompiledSchedulerDefinition

```csharp
public sealed class CompiledSchedulerDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public int GaugeThresholdUnits`

:   &mdash;

`public InputPausePolicy InputPausePolicy`

:   &mdash;

`public int NoActionRecoveryTicks`

:   &mdash;

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public SchedulerStateTag StateTag`

:   &mdash;

**Methods**

`public static CompiledSchedulerDefinition ActionOrder(int noActionRecoveryTicks)`

:   &mdash;

`public static CompiledSchedulerDefinition Atb()`

:   &mdash;

`public static CompiledSchedulerDefinition CreateActionOrder()`

:   &mdash;

`public static CompiledSchedulerDefinition CreateAtb()`

:   &mdash;

---

## CompiledSkillTiming

```csharp
public sealed class CompiledSkillTiming
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledSkillTiming()`

:   &mdash;

**Properties**

`public int CastTicks`

:   &mdash;

`public int CooldownAmount`

:   &mdash;

`public CooldownClockKind CooldownClockKind`

:   &mdash;

`public CooldownStartPolicy CooldownStartPolicy`

:   &mdash;

`public FrozenList<CompiledActionCost> Costs`

:   &mdash;

`public InterruptRefundPolicy InterruptRefundPolicy`

:   &mdash;

`public bool Interruptible`

:   &mdash;

`public int MaximumRequestedTargets`

:   &mdash;

`public int MinimumRequestedTargets`

:   &mdash;

`public int RecoveryTicks`

:   &mdash;

`public StableId SkillId`

:   &mdash;

`public TimingResolutionKind TimingResolutionKind`

:   &mdash;

---

## CooldownClockKind

```csharp
public enum CooldownClockKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `ElapsedTicks` | &mdash; |
| `OwnerOpportunities` | &mdash; |

---

## CooldownStartPolicy

```csharp
public enum CooldownStartPolicy : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Queue` | &mdash; |
| `Resolve` | &mdash; |

---

## GaugeEntry

```csharp
public sealed class GaugeEntry
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public GaugeEntry(StableId actorId, int gaugeUnits, long recoveryLockUntilTick)`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public int GaugeUnits`

:   &mdash;

`public long RecoveryLockUntilTick`

:   &mdash;

---

## IBattleScheduler

```csharp
public interface IBattleScheduler
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ISchedulerAdjustmentAdapter

```csharp
public interface ISchedulerAdjustmentAdapter
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerAdjustment.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ISchedulerAdjustmentAdapterProvider

```csharp
public interface ISchedulerAdjustmentAdapterProvider
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerAdjustment.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ISchedulerStateCodec

```csharp
public interface ISchedulerStateCodec
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/BattleSchedulerRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ISchedulerStateCodecProvider

```csharp
public interface ISchedulerStateCodecProvider
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/BattleSchedulerRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## InputPausePolicy

```csharp
public enum InputPausePolicy : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Active` | &mdash; |
| `WaitForInput` | &mdash; |
| `PauseOnInput` | &mdash; |

---

## InterruptRefundPolicy

```csharp
public enum InterruptRefundPolicy : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `None` | &mdash; |
| `Full` | &mdash; |

---

## ReadyTickEntry

```csharp
public sealed class ReadyTickEntry
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReadyTickEntry(StableId actorId, long readyTick)`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public long ReadyTick`

:   &mdash;

---

## RoundState

```csharp
public sealed class RoundState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public RoundState()`

:   &mdash;

**Properties**

`public FrozenList<StableId> ParticipantIds`

:   &mdash;

`public FrozenList<StableId> ResolvedParticipantIds`

:   &mdash;

`public long StartedTick`

:   &mdash;

**Methods**

`public bool ContainsParticipant(StableId actorId)`

:   &mdash;

`public bool IsResolved(StableId actorId)`

:   &mdash;

---

## SchedulerAdjustmentContext

```csharp
public sealed class SchedulerAdjustmentContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerAdjustment.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public SchedulerAdjustmentContext()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public FrozenList<SchedulerCombatantTimingView> Combatants`

:   &mdash;

`public long CurrentTick`

:   &mdash;

`public long Delta`

:   &mdash;

`public SchedulerAdjustmentKind Kind`

:   &mdash;

`public ulong NextOpportunitySequence`

:   &mdash;

---

## SchedulerAdjustmentResult

```csharp
public sealed class SchedulerAdjustmentResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerAdjustment.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public long ActualDelta`

:   &mdash;

`public Diagnostic? Diagnostic`

:   &mdash;

`public SchedulerState State`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public FrozenList<SchedulerWork> Work`

:   &mdash;

**Methods**

`public static SchedulerAdjustmentResult Failure()`

:   &mdash;

`public static SchedulerAdjustmentResult Success()`

:   &mdash;

---

## SchedulerAdvanceContext

```csharp
public sealed class SchedulerAdvanceContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public SchedulerAdvanceContext()`

:   &mdash;

**Properties**

`public FrozenList<SchedulerCombatantTimingView> Combatants`

:   &mdash;

`public long CurrentTick`

:   &mdash;

`public FrozenList<SchedulerDueTimer> DueTimers`

:   &mdash;

`public SchedulerDueTimer EarliestDueTimer`

:   &mdash;

`public long? ExternalDueTick`

:   &mdash;

`public ulong NextOpportunitySequence`

:   &mdash;

`public long? TickCeiling`

:   &mdash;

---

## SchedulerAdvanceResult

```csharp
public sealed class SchedulerAdvanceResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Diagnostic? Diagnostic`

:   &mdash;

`public SchedulerState State`

:   &mdash;

`public SchedulerAdvanceStopReason StopReason`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public FrozenList<SchedulerWork> Work`

:   &mdash;

**Methods**

`public static SchedulerAdvanceResult Failure(Diagnostic diagnostic)`

:   &mdash;

`public static SchedulerAdvanceResult Success()`

:   &mdash;

---

## SchedulerAdvanceStopReason

```csharp
public enum SchedulerAdvanceStopReason : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `WorkProduced` | &mdash; |
| `ReachedTickCeiling` | &mdash; |
| `ExternalBoundary` | &mdash; |
| `AwaitingCommand` | &mdash; |
| `NoScheduledWork` | &mdash; |

---

## SchedulerCombatantTimingView

```csharp
public sealed class SchedulerCombatantTimingView
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public SchedulerCombatantTimingView()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public DecisionControlKind ControlKind`

:   &mdash;

`public int EffectiveSpeedRaw`

:   &mdash;

`public int InitialAtbGaugeUnits`

:   &mdash;

`public bool IsBusy`

:   &mdash;

`public bool IsEligible`

:   &mdash;

---

## SchedulerCreateContext

```csharp
public sealed class SchedulerCreateContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public SchedulerCreateContext()`

:   &mdash;

**Properties**

`public FrozenList<SchedulerCombatantTimingView> Combatants`

:   &mdash;

`public long CurrentTick`

:   &mdash;

`public CompiledSchedulerDefinition Definition`

:   &mdash;

---

## SchedulerCreateResult

```csharp
public sealed class SchedulerCreateResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Diagnostic? Diagnostic`

:   &mdash;

`public SchedulerState State`

:   &mdash;

`public bool Succeeded`

:   &mdash;

**Methods**

`public static SchedulerCreateResult Failure(Diagnostic diagnostic)`

:   &mdash;

`public static SchedulerCreateResult Success(SchedulerState state)`

:   &mdash;

---

## SchedulerDiagnosticIds

```csharp
public static class SchedulerDiagnosticIds
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## SchedulerDueTimer

```csharp
public sealed class SchedulerDueTimer
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public SchedulerDueTimer()`

:   &mdash;

**Properties**

`public ulong ApplicationSequence`

:   &mdash;

`public long DueTick`

:   &mdash;

`public SchedulerDueTimerKind Kind`

:   &mdash;

`public StableId OwnerId`

:   &mdash;

`public StableId TimerId`

:   &mdash;

---

## SchedulerDueTimerKind

```csharp
public enum SchedulerDueTimerKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `CastCompletion` | &mdash; |
| `ElapsedCooldownExpiry` | &mdash; |
| `ElapsedStatusBoundary` | &mdash; |

---

## SchedulerIds

```csharp
public static class SchedulerIds
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## SchedulerOpportunityContext

```csharp
public sealed class SchedulerOpportunityContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public SchedulerOpportunityContext()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public FrozenList<SchedulerCombatantTimingView> Combatants`

:   &mdash;

`public long CurrentTick`

:   &mdash;

`public ulong OpportunitySequence`

:   &mdash;

---

## SchedulerOpportunityOutcome

```csharp
public enum SchedulerOpportunityOutcome : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Completed` | &mdash; |
| `Interrupted` | &mdash; |
| `Skipped` | &mdash; |

---

## SchedulerOpportunityResult

```csharp
public sealed class SchedulerOpportunityResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public SchedulerOpportunityResult()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public FrozenList<SchedulerCombatantTimingView> Combatants`

:   &mdash;

`public long CurrentTick`

:   &mdash;

`public ulong OpportunitySequence`

:   &mdash;

`public SchedulerOpportunityOutcome Outcome`

:   &mdash;

`public int RecoveryTicks`

:   &mdash;

---

## SchedulerState

```csharp
public sealed class SchedulerState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public ActionOrderState ActionOrder`

:   &mdash;

`public AtbState Atb`

:   &mdash;

`public FrozenList<DecisionEntry> DecisionEntries`

:   &mdash;

`public DecisionEntry HeadDecision`

:   &mdash;

`public long LastAdvancedTick`

:   &mdash;

`public int SchedulerContractVersion`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public SchedulerStateTag StateTag`

:   &mdash;

**Methods**

`public SchedulerState ClearDecisions()`

:   &mdash;

`public static SchedulerState CreateActionOrder()`

:   &mdash;

`public static SchedulerState CreateAtb()`

:   &mdash;

`public SchedulerState RemoveHeadDecision(ulong opportunitySequence, StableId actorId)`

:   &mdash;

`public bool TryFindDecision(StableId actorId, out DecisionEntry decision)`

:   &mdash;

---

## SchedulerStateDecodeResult

```csharp
public sealed class SchedulerStateDecodeResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerStateCodec.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Diagnostic? Diagnostic`

:   &mdash;

`public SchedulerState State`

:   &mdash;

`public bool Succeeded`

:   &mdash;

**Methods**

`public static SchedulerStateDecodeResult Failure()`

:   &mdash;

`public static SchedulerStateDecodeResult Success(SchedulerState state)`

:   &mdash;

---

## SchedulerStateTag

```csharp
public enum SchedulerStateTag : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `ActionOrder` | &mdash; |
| `Atb` | &mdash; |

---

## SchedulerTransitionResult

```csharp
public sealed class SchedulerTransitionResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Diagnostic? Diagnostic`

:   &mdash;

`public SchedulerState State`

:   &mdash;

`public bool Succeeded`

:   &mdash;

`public FrozenList<SchedulerWork> Work`

:   &mdash;

**Methods**

`public static SchedulerTransitionResult Failure(Diagnostic diagnostic)`

:   &mdash;

`public static SchedulerTransitionResult Success()`

:   &mdash;

---

## SchedulerWork

```csharp
public sealed class SchedulerWork
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public DecisionEntry Decision`

:   &mdash;

`public long FromTick`

:   &mdash;

`public SchedulerAdvanceStopReason NoWorkReason`

:   &mdash;

`public RoundState Round`

:   &mdash;

`public ulong RoundIndex`

:   &mdash;

`public SchedulerWorkTag Tag`

:   &mdash;

`public long ToTick`

:   &mdash;

**Methods**

`public static SchedulerWork AdvanceTimers(long fromTick, long toTick)`

:   &mdash;

`public static SchedulerWork CompleteRound(ulong roundIndex, RoundState round)`

:   &mdash;

`public static SchedulerWork NoWork(SchedulerAdvanceStopReason reason)`

:   &mdash;

`public static SchedulerWork ReadyOpportunity(DecisionEntry decision)`

:   &mdash;

`public static SchedulerWork StartRound(ulong roundIndex, RoundState round)`

:   &mdash;

---

## SchedulerWorkTag

```csharp
public enum SchedulerWorkTag : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/IBattleScheduler.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `StartRound` | &mdash; |
| `CompleteRound` | &mdash; |
| `ReadyOpportunity` | &mdash; |
| `AdvanceTimers` | &mdash; |
| `NoWork` | &mdash; |

---

## TimingResolutionKind

```csharp
public enum TimingResolutionKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `None` | &mdash; |
| `InterruptFirstLockedCast` | &mdash; |

---

