# AI policies

6 types in this area.

!!! abstract "On this page"
    [AiCandidateDescription](#aicandidatedescription) &middot; [AiCandidatePlan](#aicandidateplan) &middot; [AiCandidateTrace](#aicandidatetrace) &middot; [AiConditionTrace](#aiconditiontrace) &middot; [AiContext](#aicontext) &middot; [AiDecisionTrace](#aidecisiontrace)

## AiCandidateDescription

```csharp
public sealed class AiCandidateDescription
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/AI/AiContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AiCandidateDescription()`

:   &mdash;

**Properties**

`public int Priority`

:   &mdash;

`public FrozenList<StableId> RequestedTargets`

:   &mdash;

`public StableId RuleId`

:   &mdash;

`public StableId SkillId`

:   &mdash;

`public uint Weight`

:   &mdash;

---

## AiCandidatePlan

```csharp
public sealed class AiCandidatePlan
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/AI/AiContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AiCandidatePlan(IEnumerable<AiCandidateDescription> candidates)`

:   &mdash;

**Properties**

`public FrozenList<AiCandidateDescription> Candidates`

:   &mdash;

---

## AiCandidateTrace

```csharp
public sealed class AiCandidateTrace
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/AI/AiContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AiCandidateTrace()`

:   &mdash;

**Properties**

`public FrozenList<AiConditionTrace> Conditions`

:   &mdash;

`public int Priority`

:   &mdash;

`public Diagnostic? Rejection`

:   &mdash;

`public StableId RuleId`

:   &mdash;

`public StableId SkillId`

:   &mdash;

`public uint Weight`

:   &mdash;

---

## AiConditionTrace

```csharp
public readonly struct AiConditionTrace
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/AI/AiContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AiConditionTrace(StableId ruleId, int conditionIndex, bool passed)`

:   &mdash;

**Properties**

`public int ConditionIndex`

:   &mdash;

`public bool Passed`

:   &mdash;

`public StableId RuleId`

:   &mdash;

---

## AiContext

```csharp
public sealed class AiContext
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/AI/AiContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AiContext()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public CompiledBattleContent Content`

:   &mdash;

`public CompiledAiPolicyDefinition Policy`

:   &mdash;

`public BattleStateView Snapshot`

:   &mdash;

---

## AiDecisionTrace

```csharp
public sealed class AiDecisionTrace
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/AI/AiContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AiDecisionTrace()`

:   &mdash;

**Properties**

`public StableId ActorId`

:   &mdash;

`public FrozenList<AiCandidateTrace> Candidates`

:   &mdash;

`public MechanicsImplementationReference Implementation`

:   &mdash;

`public bool NoLegalCommand`

:   &mdash;

`public ulong OpportunitySequence`

:   &mdash;

`public StableId PolicyId`

:   &mdash;

`public BattleCommand SelectedCommand`

:   &mdash;

`public ulong? SelectionBound`

:   &mdash;

`public ulong? SelectionSample`

:   &mdash;

`public FrozenList<StableId> TargetCandidates`

:   &mdash;

`public FrozenList<uint> TargetSamples`

:   &mdash;

`public long Tick`

:   &mdash;

---

