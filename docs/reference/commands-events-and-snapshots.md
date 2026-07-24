# Commands, events and snapshots

24 types in this area.

!!! abstract "On this page"
    [ActionCostState](#actioncoststate) &middot; [ActiveActionState](#activeactionstate) &middot; [ActiveCastState](#activecaststate) &middot; [BattleCommand](#battlecommand) &middot; [BattleEvent](#battleevent) &middot; [BattleIds](#battleids) &middot; [BattleSnapshot](#battlesnapshot) &middot; [CombatantState](#combatantstate) &middot; [CommandSubmissionBoundary](#commandsubmissionboundary) &middot; [CooldownState](#cooldownstate) &middot; [DecisionControlKind](#decisioncontrolkind) &middot; [DecisionEntry](#decisionentry) &middot; [PropertyEntry](#propertyentry) &middot; [PropertySet](#propertyset) &middot; [RecordedCommand](#recordedcommand) &middot; [RecordedCommandDisposition](#recordedcommanddisposition) &middot; [ReplayCheckpoint](#replaycheckpoint) &middot; [ResourceState](#resourcestate) &middot; [StartCombatant](#startcombatant) &middot; [StartResource](#startresource) &middot; [StartTeam](#startteam) &middot; [TaggedValue](#taggedvalue) &middot; [TaggedValueTag](#taggedvaluetag) &middot; [TeamState](#teamstate)

## ActionCostState

```csharp
public sealed class ActionCostState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ActionCostState(StableId resourceId, int amount)`

:   &mdash;

**Properties**

`public int Amount`

:   &mdash;

`public StableId ResourceId`

:   &mdash;

---

## ActiveActionState

```csharp
public sealed class ActiveActionState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ActiveActionState()`

:   &mdash;

**Properties**

`public long AcceptedTick`

:   &mdash;

`public StableId ActorId`

:   &mdash;

`public ActiveCastState Cast`

:   &mdash;

`public InterruptRefundPolicy InterruptRefundPolicy`

:   &mdash;

`public FrozenList<StableId> LockedTargetIds`

:   &mdash;

`public ulong OpportunitySequence`

:   &mdash;

`public FrozenList<ActionCostState> PaidCosts`

:   &mdash;

`public bool QueueCooldownStarted`

:   &mdash;

`public FrozenList<ActionCostState> RefundedCosts`

:   &mdash;

`public ulong RootActionSequence`

:   &mdash;

`public StableId SkillId`

:   &mdash;

`public TimingResolutionKind TimingResolutionKind`

:   &mdash;

---

## ActiveCastState

```csharp
public sealed class ActiveCastState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ActiveCastState(long startTick, long endTick, bool interruptible)`

:   &mdash;

**Properties**

`public long EndTick`

:   &mdash;

`public bool Interruptible`

:   &mdash;

`public long StartTick`

:   &mdash;

---

## BattleCommand

```csharp
public sealed class BattleCommand
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleCommand.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public BattleCommand()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public ulong CommandSequence`

:   &mdash;

`public StableId CommandTypeId`

:   &mdash;

`public PropertySet Properties`

:   &mdash;

`public FrozenList<StableId> RequestedTargetIds`

:   &mdash;

`public long RequestedTick`

:   &mdash;

`public StableId? SkillId`

:   &mdash;

**Methods**

`public static BattleCommand Concede(ulong sequence, long tick, StableId actorId)`

:   &mdash;

---

## BattleEvent

```csharp
public sealed class BattleEvent
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleEvent.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public BattleEvent(long tick, ulong eventSequence, ulong rootActionSequence, StableId eventTypeId, PropertySet properties)`

:   &mdash;

**Properties**

`public ulong EventSequence`

:   &mdash;

`public StableId EventTypeId`

:   &mdash;

`public PropertySet Properties`

:   &mdash;

`public ulong RootActionSequence`

:   &mdash;

`public long Tick`

:   &mdash;

---

## BattleIds

```csharp
public static class BattleIds
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleEvent.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## BattleSnapshot

```csharp
public sealed class BattleSnapshot
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<ActiveActionState> ActiveActions`

:   &mdash;

`public FrozenList<CombatantState> Combatants`

:   &mdash;

`public ulong CompletedRootActionCount`

:   &mdash;

`public Sha256Digest ContentManifestHash`

:   &mdash;

`public FrozenList<CooldownState> Cooldowns`

:   &mdash;

`public FrozenList<DecisionEntry> DecisionEntries`

:   &mdash;

`public int EngineVersion`

:   &mdash;

`public Sha256Digest EventChainHash`

:   &mdash;

`public FrozenList<ExecutionFrame> Frames`

:   &mdash;

`public ulong LastEventSequence`

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

`public StableId? PendingDecisionActorId`

:   &mdash;

`public FrozenList<ReplayCheckpoint> PeriodicCheckpoints`

:   &mdash;

`public SimulationContractProfile Profile`

:   &mdash;

`public FrozenList<ReactionRootBudgetState> ReactionRoots`

:   &mdash;

`public FrozenList<RecordedCommand> RecordedCommands`

:   &mdash;

`public Sha256Digest RegistryBindingHash`

:   &mdash;

`public FrozenList<ResourceState> Resources`

:   &mdash;

`public BattleResultState Result`

:   &mdash;

`public DeterministicRng Rng`

:   &mdash;

`public SchedulerState Scheduler`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public SchedulerState SchedulerState`

:   &mdash;

`public FrozenList<ShieldState> Shields`

:   &mdash;

`public Sha256Digest StateHash`

:   &mdash;

`public FrozenList<CombatantStatState> Stats`

:   &mdash;

`public FrozenList<StatusInstanceState> Statuses`

:   &mdash;

`public FrozenList<SystemStatusActionState> SystemStatusActions`

:   &mdash;

`public FrozenList<TeamState> Teams`

:   &mdash;

`public long Tick`

:   &mdash;

**Methods**

`public ActiveActionState FindActiveAction(StableId actorId)`

:   &mdash;

`public CombatantState FindCombatant(StableId id)`

:   &mdash;

`public CooldownState FindCooldown(StableId ownerId, StableId skillId)`

:   &mdash;

`public ResourceState FindResource(StableId ownerId, StableId resourceId)`

:   &mdash;

`public TeamState FindTeam(StableId id)`

:   &mdash;

---

## CombatantState

```csharp
public sealed class CombatantState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CombatantState(StableId id, StableId teamId, int maximumHealth, int health, bool targetable)`

:   &mdash;

**Properties**

`public StableId? AiPolicyId`

:   &mdash;

`public DecisionControlKind ControlKind`

:   &mdash;

`public StableId DefinitionId`

:   &mdash;

`public StableId FormationRowId`

:   &mdash;

`public StableId FormationSideId`

:   &mdash;

`public StableId FormationSlotId`

:   &mdash;

`public int Health`

:   &mdash;

`public StableId Id`

:   &mdash;

`public bool IsLiving`

:   &mdash;

`public int MaximumHealth`

:   &mdash;

`public bool Targetable`

:   &mdash;

`public StableId TeamId`

:   &mdash;

---

## CommandSubmissionBoundary

```csharp
public readonly struct CommandSubmissionBoundary : IEquatable<CommandSubmissionBoundary>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CommandSubmissionBoundary(long tick, ulong eventSequence, Sha256Digest preCommandStateHash)`

:   &mdash;

**Properties**

`public ulong EventSequence`

:   &mdash;

`public Sha256Digest PreCommandStateHash`

:   &mdash;

`public long Tick`

:   &mdash;

**Methods**

`public bool Equals(CommandSubmissionBoundary other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## CooldownState

```csharp
public sealed class CooldownState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CooldownState()`

:   &mdash;

**Properties**

`public CooldownClockKind ClockKind`

:   &mdash;

`public StableId OwnerId`

:   &mdash;

`public int RemainingElapsedTicks`

:   &mdash;

`public int RemainingOwnerOpportunities`

:   &mdash;

`public StableId SkillId`

:   &mdash;

`public ulong StartedActionSequence`

:   &mdash;

---

## DecisionControlKind

```csharp
public enum DecisionControlKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Human` | &mdash; |
| `Automatic` | &mdash; |

---

## DecisionEntry

```csharp
public sealed class DecisionEntry
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Scheduling/SchedulerSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public DecisionEntry()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public DecisionControlKind ControlKind`

:   &mdash;

`public ulong OpportunitySequence`

:   &mdash;

`public long ReadyTick`

:   &mdash;

---

## PropertyEntry

```csharp
public readonly struct PropertyEntry
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/TaggedValue.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public PropertyEntry(StableId key, TaggedValue value)`

:   &mdash;

**Properties**

`public StableId Key`

:   &mdash;

`public TaggedValue Value`

:   &mdash;

---

## PropertySet

```csharp
public sealed class PropertySet : IReadOnlyList<PropertyEntry>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/TaggedValue.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public PropertySet(IEnumerable<PropertyEntry> entries)`

:   &mdash;

**Properties**

`public int Count`

:   &mdash;

`public static PropertySet Empty`

:   &mdash;

**Methods**

`public IEnumerator<PropertyEntry> GetEnumerator()`

:   &mdash;

`public TaggedValue Require(StableId key, TaggedValueTag expectedTag)`

:   &mdash;

`public bool TryGetValue(StableId key, out TaggedValue value)`

:   &mdash;

---

## RecordedCommand

```csharp
public sealed class RecordedCommand
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public RecordedCommand()`

:   &mdash;

**Properties**

`public BattleCommand Command`

:   &mdash;

`public Sha256Digest CommandEventHash`

:   &mdash;

`public RecordedCommandDisposition Disposition`

:   &mdash;

`public StableId? ReasonId`

:   &mdash;

`public CommandSubmissionBoundary? SubmissionBoundary`

:   &mdash;

**Methods**

`public static RecordedCommand CreateB2()`

:   &mdash;

---

## RecordedCommandDisposition

```csharp
public enum RecordedCommandDisposition : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Accepted` | &mdash; |
| `Rejected` | &mdash; |

---

## ReplayCheckpoint

```csharp
public sealed class ReplayCheckpoint
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReplayCheckpoint()`

:   &mdash;

**Properties**

`public Sha256Digest EventChainHash`

:   &mdash;

`public ulong EventSequence`

:   &mdash;

`public int RecordedCommandCount`

:   &mdash;

`public Sha256Digest StateHash`

:   &mdash;

`public long Tick`

:   &mdash;

---

## ResourceState

```csharp
public sealed class ResourceState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ResourceState(StableId ownerId, StableId resourceId, int maximum, int current)`

:   &mdash;

**Properties**

`public int Current`

:   &mdash;

`public int Maximum`

:   &mdash;

`public StableId OwnerId`

:   &mdash;

`public StableId ResourceId`

:   &mdash;

---

## StartCombatant

```csharp
public sealed class StartCombatant
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/CompiledBattleContent.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StartCombatant(StableId combatantId, int maximumHealth, int startingHealth, bool targetable)`

:   &mdash;

**Properties**

`public StableId? AutomaticPolicyId`

:   &mdash;

`public StableId CombatantId`

:   &mdash;

`public DecisionControlKind ControlKind`

:   &mdash;

`public int EffectiveSpeedRaw`

:   &mdash;

`public FrozenList<StableId> GrantedSkillIds`

:   &mdash;

`public int InitialAtbGaugeUnits`

:   &mdash;

`public int MaximumHealth`

:   &mdash;

`public FrozenList<StartResource> Resources`

:   &mdash;

`public int StartingHealth`

:   &mdash;

`public bool Targetable`

:   &mdash;

**Methods**

`public static StartCombatant CreateB2()`

:   &mdash;

---

## StartResource

```csharp
public sealed class StartResource
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/CompiledBattleContent.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StartResource(StableId resourceId, int maximum, int current)`

:   &mdash;

**Properties**

`public int Current`

:   &mdash;

`public int Maximum`

:   &mdash;

`public StableId ResourceId`

:   &mdash;

---

## StartTeam

```csharp
public sealed class StartTeam
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/CompiledBattleContent.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StartTeam(StableId teamId, IEnumerable<StartCombatant> combatants)`

:   &mdash;

**Properties**

`public FrozenList<StartCombatant> Combatants`

:   &mdash;

`public StableId TeamId`

:   &mdash;

**Methods**

`public static StartTeam CreateB2(StableId teamId, IEnumerable<StartCombatant> combatants)`

:   &mdash;

---

## TaggedValue

```csharp
public sealed class TaggedValue
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/TaggedValue.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<bool> BooleanArrayValue`

:   &mdash;

`public bool BooleanValue`

:   &mdash;

`public byte[] BytesValue`

:   &mdash;

`public FrozenList<Chance64> Chance64ArrayValue`

:   &mdash;

`public Chance64 Chance64Value`

:   &mdash;

`public FrozenList<Fixed64> Fixed64ArrayValue`

:   &mdash;

`public Fixed64 Fixed64Value`

:   &mdash;

`public FrozenList<int> Int32ArrayValue`

:   &mdash;

`public int Int32Value`

:   &mdash;

`public FrozenList<long> Int64ArrayValue`

:   &mdash;

`public long Int64Value`

:   &mdash;

`public FrozenList<StableId> StableIdArrayValue`

:   &mdash;

`public StableId StableIdValue`

:   &mdash;

`public FrozenList<string> StringArrayValue`

:   &mdash;

`public string StringValue`

:   &mdash;

`public TaggedValueTag Tag`

:   &mdash;

`public uint UInt32Value`

:   &mdash;

`public FrozenList<ulong> UInt64ArrayValue`

:   &mdash;

`public ulong UInt64Value`

:   &mdash;

**Methods**

`public static TaggedValue FromBoolean(bool value)`

:   &mdash;

`public static TaggedValue FromBooleans(IEnumerable<bool> values)`

:   &mdash;

`public static TaggedValue FromBytes(byte[] value)`

:   &mdash;

`public static TaggedValue FromChance64(Chance64 value)`

:   &mdash;

`public static TaggedValue FromChance64s(IEnumerable<Chance64> values)`

:   &mdash;

`public static TaggedValue FromFixed64(Fixed64 value)`

:   &mdash;

`public static TaggedValue FromFixed64s(IEnumerable<Fixed64> values)`

:   &mdash;

`public static TaggedValue FromInt32(int value)`

:   &mdash;

`public static TaggedValue FromInt32s(IEnumerable<int> values)`

:   &mdash;

`public static TaggedValue FromInt64(long value)`

:   &mdash;

`public static TaggedValue FromInt64s(IEnumerable<long> values)`

:   &mdash;

`public static TaggedValue FromStableId(StableId value)`

:   &mdash;

`public static TaggedValue FromStableIds(IEnumerable<StableId> values)`

:   &mdash;

`public static TaggedValue FromString(string value)`

:   &mdash;

`public static TaggedValue FromStrings(IEnumerable<string> values)`

:   &mdash;

`public static TaggedValue FromUInt32(uint value)`

:   &mdash;

`public static TaggedValue FromUInt64(ulong value)`

:   &mdash;

`public static TaggedValue FromUInt64s(IEnumerable<ulong> values)`

:   &mdash;

---

## TaggedValueTag

```csharp
public enum TaggedValueTag : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/TaggedValue.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Boolean` | &mdash; |
| `Int32` | &mdash; |
| `Int64` | &mdash; |
| `UInt32` | &mdash; |
| `UInt64` | &mdash; |
| `Fixed64` | &mdash; |
| `StableId` | &mdash; |
| `StableIdArray` | &mdash; |
| `Bytes` | &mdash; |
| `Chance64` | &mdash; |
| `String` | &mdash; |
| `BooleanArray` | &mdash; |
| `Int32Array` | &mdash; |
| `Int64Array` | &mdash; |
| `UInt64Array` | &mdash; |
| `Fixed64Array` | &mdash; |
| `Chance64Array` | &mdash; |
| `StringArray` | &mdash; |

---

## TeamState

```csharp
public sealed class TeamState
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Model/BattleSnapshot.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public TeamState(StableId id, bool conceded)`

:   &mdash;

**Properties**

`public bool Conceded`

:   &mdash;

`public StableId Id`

:   &mdash;

---

