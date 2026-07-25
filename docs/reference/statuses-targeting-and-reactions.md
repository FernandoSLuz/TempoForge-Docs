# Statuses, targeting and reactions

11 types in this area.

!!! abstract "On this page"
    [CombatantStatState](#combatantstatstate) &middot; [ReactionContext](#reactioncontext) &middot; [ReactionEvaluation](#reactionevaluation) &middot; [ReactionSignature](#reactionsignature) &middot; [ShieldState](#shieldstate) &middot; [StatusInstanceState](#statusinstancestate) &middot; [TargetContext](#targetcontext) &middot; [TargetLifeState](#targetlifestate) &middot; [TargetRequestContract](#targetrequestcontract) &middot; [TargetRequestResult](#targetrequestresult) &middot; [TargetTeamRelation](#targetteamrelation)

## CombatantStatState

```csharp
public sealed class CombatantStatState
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Statuses/MechanicsState.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CombatantStatState(StableId ownerId, StableId statId, Fixed64 value)`

:   &mdash;

**Properties**

`public StableId OwnerId`

:   &mdash;

`public StableId StatId`

:   &mdash;

`public Fixed64 Value`

:   &mdash;

---

## ReactionContext

```csharp
public sealed class ReactionContext
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Reactions/ReactionContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReactionContext()`

:   &mdash;

**Properties**

`public CompiledBattleContent Content`

:   &mdash;

`public int ParentDepth`

:   &mdash;

`public ReactionTriggerPhase Phase`

:   &mdash;

`public ulong RootActionSequence`

:   &mdash;

`public BattleStateView Snapshot`

:   &mdash;

`public StableId SourceCombatantId`

:   &mdash;

`public StableId TargetCombatantId`

:   &mdash;

`public StableId TriggeringEffectTag`

:   &mdash;

---

## ReactionEvaluation

```csharp
public sealed class ReactionEvaluation
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Reactions/ReactionContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReactionEvaluation(bool eligible, StableId sourceCombatantId, StableId targetCombatantId, Diagnostic diagnostic)`

:   &mdash;

**Properties**

`public Diagnostic Diagnostic`

:   &mdash;

`public bool Eligible`

:   &mdash;

`public StableId SourceCombatantId`

:   &mdash;

`public StableId TargetCombatantId`

:   &mdash;

---

## ReactionSignature

```csharp
public sealed class ReactionSignature
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Reactions/ReactionContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReactionSignature()`

:   &mdash;

**Properties**

`public FrozenList<StableId> EmittedEffectTags`

:   &mdash;

`public bool FiniteByConstruction`

:   &mdash;

`public FrozenList<StableId> TriggerEffectTags`

:   &mdash;

---

## ShieldState

```csharp
public sealed class ShieldState
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Statuses/MechanicsState.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ShieldState()`

:   &mdash;

**Properties**

`public ulong ApplicationSequence`

:   &mdash;

`public ulong? LinkedStatusApplicationSequence`

:   &mdash;

`public int MaximumAuthoredAmount`

:   &mdash;

`public StableId OwnerId`

:   &mdash;

`public int Priority`

:   &mdash;

`public int RemainingAmount`

:   &mdash;

`public StableId ShieldId`

:   &mdash;

`public StableId SourceId`

:   &mdash;

`public ulong SourceRootActionSequence`

:   &mdash;

---

## StatusInstanceState

```csharp
public sealed class StatusInstanceState
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Statuses/MechanicsState.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StatusInstanceState()`

:   &mdash;

**Properties**

`public ulong ApplicationSequence`

:   &mdash;

`public StatusDurationClock DurationClock`

:   &mdash;

`public ulong ExcludedOriginatingRootActionSequence`

:   &mdash;

`public PropertySet InstanceConfiguration`

:   &mdash;

`public ulong? LinkedShieldApplicationSequence`

:   &mdash;

`public long NextPeriodicTick`

:   &mdash;

`public StableId OwnerId`

:   &mdash;

`public int RemainingDuration`

:   &mdash;

`public StableId SourceId`

:   &mdash;

`public ulong SourceRootActionSequence`

:   &mdash;

`public int StackCount`

:   &mdash;

`public StableId StatusDefinitionId`

:   &mdash;

---

## TargetContext

```csharp
public sealed class TargetContext
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Targeting/TargetContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public TargetContext(CompiledBattleContent content, BattleSnapshot snapshot, StableId actorId, CompiledSkillDefinition skill)`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public CompiledBattleContent Content`

:   &mdash;

`public CompiledSkillDefinition Skill`

:   &mdash;

`public BattleStateView Snapshot`

:   &mdash;

---

## TargetLifeState

```csharp
public enum TargetLifeState : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Targeting/TargetContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Living` | &mdash; |
| `Dead` | &mdash; |
| `Any` | &mdash; |

---

## TargetRequestContract

```csharp
public sealed class TargetRequestContract
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Targeting/TargetContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public TargetRequestContract()`

:   &mdash;

`public TargetRequestContract()`

:   &mdash;

**Properties**

`public bool ActorMayAppear`

:   &mdash;

`public TargetLifeState AllowedLifeState`

:   &mdash;

`public int MaximumRequestedIds`

:   &mdash;

`public int MaximumResolvedTargets`

:   &mdash;

`public int MinimumRequestedIds`

:   &mdash;

`public int RandomCount`

:   &mdash;

`public TargetTeamRelation TeamRelation`

:   &mdash;

`public bool ZeroRequestedInvokesAutomaticSelection`

:   &mdash;

---

## TargetRequestResult

```csharp
public sealed class TargetRequestResult
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Targeting/TargetContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public TargetRequestResult(bool accepted, IEnumerable<StableId> lockedTargets, Diagnostic diagnostic)`

:   &mdash;

**Properties**

`public bool Accepted`

:   &mdash;

`public Diagnostic Diagnostic`

:   &mdash;

`public FrozenList<StableId> LockedTargets`

:   &mdash;

**Methods**

`public static TargetRequestResult Accept(IEnumerable<StableId> lockedTargets)`

:   &mdash;

`public static TargetRequestResult Reject(StableId reasonId, string detail = null)`

:   &mdash;

---

## TargetTeamRelation

```csharp
public enum TargetTeamRelation : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Targeting/TargetContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Self` | &mdash; |
| `Ally` | &mdash; |
| `Enemy` | &mdash; |
| `Any` | &mdash; |

---

