# Effects and mechanics

41 types in this area.

!!! abstract "On this page"
    [AiValidationContext](#aivalidationcontext) &middot; [BattleFormulaService](#battleformulaservice) &middot; [BattleMechanicsRegistry](#battlemechanicsregistry) &middot; [BattleStateView](#battlestateview) &middot; [EffectPlan](#effectplan) &middot; [EffectPlanningContext](#effectplanningcontext) &middot; [EffectPrimitive](#effectprimitive) &middot; [EffectPrimitiveTag](#effectprimitivetag) &middot; [EffectValidationContext](#effectvalidationcontext) &middot; [FormulaAttribution](#formulaattribution) &middot; [FormulaAttributionTrace](#formulaattributiontrace) &middot; [FormulaAttributionTraceBatch](#formulaattributiontracebatch) &middot; [FormulaContext](#formulacontext) &middot; [FormulaContribution](#formulacontribution) &middot; [FormulaContributionKind](#formulacontributionkind) &middot; [FormulaEvaluationRequest](#formulaevaluationrequest) &middot; [FormulaModifierInput](#formulamodifierinput) &middot; [FormulaPreview](#formulapreview) &middot; [FormulaPreviewContext](#formulapreviewcontext) &middot; [FormulaRandomBoundKind](#formularandomboundkind) &middot; [FormulaRandomInputDescriptor](#formularandominputdescriptor) &middot; [FormulaRandomSample](#formularandomsample) &middot; [FormulaResult](#formularesult) &middot; [FormulaValidationContext](#formulavalidationcontext) &middot; [IAiPolicy](#iaipolicy) &middot; [IEffectResolver](#ieffectresolver) &middot; [IFormula](#iformula) &middot; [IMechanicsImplementation](#imechanicsimplementation) &middot; [IMechanicsRandomSource](#imechanicsrandomsource) &middot; [IReactionRule](#ireactionrule) &middot; [ITargetResolver](#itargetresolver) &middot; [MechanicsCategoryTag](#mechanicscategorytag) &middot; [MechanicsDiagnosticIds](#mechanicsdiagnosticids) &middot; [MechanicsIds](#mechanicsids) &middot; [MechanicsRegistryBinding](#mechanicsregistrybinding) &middot; [MechanicsResolveResult](#mechanicsresolveresult) &middot; [ReactionValidationContext](#reactionvalidationcontext) &middot; [SchedulerAdjustmentKind](#scheduleradjustmentkind) &middot; [StatusApplicationPreview](#statusapplicationpreview) &middot; [TargetValidationContext](#targetvalidationcontext) &middot; [ValidationReport](#validationreport)

## AiValidationContext

```csharp
public sealed class AiValidationContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public AiValidationContext(CompiledBattleContent content)`

:   &mdash;

**Properties**

`public CompiledBattleContent Content`

:   &mdash;

---

## BattleFormulaService

```csharp
public static class BattleFormulaService
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Formulas/BattleFormulaService.cs</small>

Pure formula input and evaluation boundary shared by runtime, forecast,
replay, Workbench, tooltips, and range previews.

**Methods**

`public static FormulaContext BuildContext()`

:   &mdash;

`public static FormulaResult Evaluate()`

:   &mdash;

`public static FormulaPreview Preview()`

:   &mdash;

`public static StatusApplicationPreview PreviewStatusApplication()`

:   &mdash;

---

## BattleMechanicsRegistry

```csharp
public sealed class BattleMechanicsRegistry
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/BattleMechanicsRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public FrozenList<MechanicsRegistryBinding> Bindings`

:   &mdash;

`public static BattleMechanicsRegistry Empty`

:   &mdash;

**Methods**

`public static BattleMechanicsRegistry CreateWithBuiltIns()`

:   &mdash;

`public BattleMechanicsRegistry Register(IFormula implementation)`

:   &mdash;

`public BattleMechanicsRegistry Register(IEffectResolver implementation)`

:   &mdash;

`public BattleMechanicsRegistry Register(ITargetResolver implementation)`

:   &mdash;

`public BattleMechanicsRegistry Register(IAiPolicy implementation)`

:   &mdash;

`public BattleMechanicsRegistry Register(IReactionRule implementation)`

:   &mdash;

`public MechanicsResolveResult<IAiPolicy> ResolveAi(StableId id, int version)`

:   &mdash;

`public MechanicsResolveResult<IEffectResolver> ResolveEffect(StableId id, int version)`

:   &mdash;

`public MechanicsResolveResult<IFormula> ResolveFormula(StableId id, int version)`

:   &mdash;

`public MechanicsResolveResult<IReactionRule> ResolveReaction(StableId id, int version)`

:   &mdash;

`public MechanicsResolveResult<ITargetResolver> ResolveTarget(StableId id, int version)`

:   &mdash;

---

## BattleStateView

```csharp
public sealed class BattleStateView
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/BattleStateView.cs</small>

Immutable, RNG-free projection supplied to non-formula mechanics extensions.
The authoritative snapshot deliberately is not reachable from this type.

**Properties**

`public FrozenList<ActiveActionState> ActiveActions`

:   &mdash;

`public FrozenList<CombatantState> Combatants`

:   &mdash;

`public FrozenList<CooldownState> Cooldowns`

:   &mdash;

`public SimulationContractProfile Profile`

:   &mdash;

`public FrozenList<ResourceState> Resources`

:   &mdash;

`public BattleResultState Result`

:   &mdash;

`public StableId SchedulerId`

:   &mdash;

`public SchedulerState SchedulerState`

:   &mdash;

`public FrozenList<ShieldState> Shields`

:   &mdash;

`public FrozenList<CombatantStatState> Stats`

:   &mdash;

`public FrozenList<StatusInstanceState> Statuses`

:   &mdash;

`public FrozenList<TeamState> Teams`

:   &mdash;

`public long Tick`

:   &mdash;

**Methods**

`public CombatantState FindCombatant(StableId id)`

:   &mdash;

`public ResourceState FindResource(StableId ownerId, StableId resourceId)`

:   &mdash;

`public TeamState FindTeam(StableId id)`

:   &mdash;

---

## EffectPlan

```csharp
public sealed class EffectPlan
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Effects/EffectPlan.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public EffectPlan(IEnumerable<EffectPrimitive> primitives, IEnumerable<Diagnostic> diagnostics)`

:   &mdash;

**Properties**

`public FrozenList<Diagnostic> Diagnostics`

:   &mdash;

`public bool IsValid`

:   &mdash;

`public FrozenList<EffectPrimitive> Primitives`

:   &mdash;

---

## EffectPlanningContext

```csharp
public sealed class EffectPlanningContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Effects/EffectPlan.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public EffectPlanningContext(CompiledBattleContent content, BattleSnapshot snapshot, StableId sourceId, StableId targetId, StableId effectEntryId)`

:   &mdash;

**Properties**

`public CompiledBattleContent Content`

:   &mdash;

`public StableId EffectEntryId`

:   &mdash;

`public BattleStateView Snapshot`

:   &mdash;

`public StableId SourceId`

:   &mdash;

`public StableId TargetId`

:   &mdash;

---

## EffectPrimitive

```csharp
public sealed class EffectPrimitive
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Effects/EffectPlan.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public bool BypassDefense`

:   &mdash;

`public bool BypassIncomingModifiers`

:   &mdash;

`public bool BypassShield`

:   &mdash;

`public Chance64 Chance`

:   &mdash;

`public Fixed64 FixedAmount`

:   &mdash;

`public MechanicsImplementationReference Formula`

:   &mdash;

`public PropertySet FormulaProperties`

:   &mdash;

`public StableId Id`

:   &mdash;

`public StableId? LinkedStatusDefinitionId`

:   &mdash;

`public StatusPolarity Polarity`

:   &mdash;

`public int Priority`

:   &mdash;

`public long SignedAmount`

:   &mdash;

`public EffectPrimitiveTag Tag`

:   &mdash;

`public FrozenList<StableId> Tags`

:   &mdash;

**Methods**

`public static EffectPrimitive AdjustScheduler(SchedulerAdjustmentKind kind, long delta)`

:   &mdash;

`public static EffectPrimitive ApplyShield()`

:   &mdash;

`public static EffectPrimitive ApplyStatus(StableId statusDefinitionId, Chance64 baseChance)`

:   &mdash;

`public static EffectPrimitive ChangeResource(StableId resourceId, long delta)`

:   &mdash;

`public static EffectPrimitive Damage()`

:   &mdash;

`public static EffectPrimitive Dispel(StatusPolarity polarity, IEnumerable<StableId> tags, int maximumCount)`

:   &mdash;

`public static EffectPrimitive Heal(MechanicsImplementationReference formula, PropertySet formulaProperties)`

:   &mdash;

`public static EffectPrimitive InterruptCast(StableId reasonId)`

:   &mdash;

`public static EffectPrimitive RemoveStatus(StableId statusDefinitionId)`

:   &mdash;

---

## EffectPrimitiveTag

```csharp
public enum EffectPrimitiveTag : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Effects/EffectPlan.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `CalculateAndDamage` | &mdash; |
| `CalculateAndHeal` | &mdash; |
| `ChangeResource` | &mdash; |
| `ApplyShield` | &mdash; |
| `ApplyStatus` | &mdash; |
| `RemoveStatus` | &mdash; |
| `Dispel` | &mdash; |
| `AdjustScheduler` | &mdash; |
| `InterruptCast` | &mdash; |

---

## EffectValidationContext

```csharp
public sealed class EffectValidationContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public EffectValidationContext(CompiledBattleContent content)`

:   &mdash;

**Properties**

`public CompiledBattleContent Content`

:   &mdash;

---

## FormulaAttribution

```csharp
public sealed class FormulaAttribution
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Trace/FormulaTrace.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaAttribution()`

:   &mdash;

**Properties**

`public Fixed64 ClampContribution`

:   &mdash;

`public FrozenList<FormulaContribution> Contributions`

:   &mdash;

`public StableId EffectEntryId`

:   &mdash;

`public Fixed64 FinalResult`

:   &mdash;

`public MechanicsImplementationReference Formula`

:   &mdash;

`public PropertySet Inputs`

:   &mdash;

`public int PrimitiveIndex`

:   &mdash;

`public FrozenList<FormulaRandomSample> RandomSamples`

:   &mdash;

`public Fixed64 RoundedResult`

:   &mdash;

`public StableId SourceId`

:   &mdash;

`public StableId TargetId`

:   &mdash;

`public Fixed64 UnclampedResult`

:   &mdash;

---

## FormulaAttributionTrace

```csharp
public sealed class FormulaAttributionTrace
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Trace/FormulaTrace.cs</small>

Consumer-owned evidence linking full formula attribution bytes to the
gameplay event that references their hash. This record is deliberately
excluded from authoritative battle state and its canonical hash.

**Constructors**

`public FormulaAttributionTrace()`

:   &mdash;

**Properties**

`public FormulaAttribution Attribution`

:   &mdash;

`public Sha256Digest AttributionHash`

:   &mdash;

`public StableId EffectEntryId`

:   &mdash;

`public StableId EventTypeId`

:   &mdash;

`public int PrimitiveIndex`

:   &mdash;

`public ulong RootActionSequence`

:   &mdash;

`public long Tick`

:   &mdash;

---

## FormulaAttributionTraceBatch

```csharp
public sealed class FormulaAttributionTraceBatch
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Trace/FormulaTrace.cs</small>

Bounded immutable formula evidence returned to one consumer call.
OmittedCount is nonzero only when a long aggregate operation produced
more traces than the documented result-memory bound.

**Properties**

`public static FormulaAttributionTraceBatch Empty`

:   &mdash;

`public bool IsTruncated`

:   &mdash;

`public long OmittedCount`

:   &mdash;

`public FrozenList<FormulaAttributionTrace> Traces`

:   &mdash;

---

## FormulaContext

```csharp
public sealed class FormulaContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaContext()`

:   &mdash;

**Properties**

`public Fixed64 BaseStat`

:   &mdash;

`public Chance64 CriticalChance`

:   &mdash;

`public Fixed64 CriticalMultiplier`

:   &mdash;

`public Fixed64 Defense`

:   &mdash;

`public StableId EffectEntryId`

:   &mdash;

`public Fixed64 EndpointMaximum`

:   &mdash;

`public Fixed64 EndpointMinimum`

:   &mdash;

`public Chance64 HitChance`

:   &mdash;

`public FrozenList<FormulaModifierInput> Modifiers`

:   &mdash;

`public Fixed64 Potency`

:   &mdash;

`public int PrimitiveIndex`

:   &mdash;

`public StableId SourceId`

:   &mdash;

`public StableId TargetId`

:   &mdash;

`public Fixed64 VarianceMaximum`

:   &mdash;

`public Fixed64 VarianceMinimum`

:   &mdash;

---

## FormulaContribution

```csharp
public readonly struct FormulaContribution
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Trace/FormulaTrace.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaContribution()`

:   &mdash;

**Properties**

`public Fixed64 Input`

:   &mdash;

`public FormulaContributionKind Kind`

:   &mdash;

`public Fixed64 Output`

:   &mdash;

`public int Priority`

:   &mdash;

`public StableId SourceId`

:   &mdash;

---

## FormulaContributionKind

```csharp
public enum FormulaContributionKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Trace/FormulaTrace.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `BaseStat` | &mdash; |
| `FlatModifier` | &mdash; |
| `MultiplicativeModifier` | &mdash; |
| `Potency` | &mdash; |
| `OutgoingModifier` | &mdash; |
| `CriticalMultiplier` | &mdash; |
| `Defense` | &mdash; |
| `IncomingModifier` | &mdash; |
| `Variance` | &mdash; |
| `Rounding` | &mdash; |
| `Clamp` | &mdash; |

---

## FormulaEvaluationRequest

```csharp
public sealed class FormulaEvaluationRequest
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Formulas/BattleFormulaService.cs</small>

Immutable coordinates for one formula primitive. The same request can be
evaluated by the live reducer or previewed without consuming RNG.

**Constructors**

`public FormulaEvaluationRequest()`

:   &mdash;

**Properties**

`public StableId EffectEntryId`

:   &mdash;

`public EffectPrimitive Primitive`

:   &mdash;

`public int PrimitiveIndex`

:   &mdash;

`public StableId SourceId`

:   &mdash;

`public StableId TargetId`

:   &mdash;

---

## FormulaModifierInput

```csharp
public readonly struct FormulaModifierInput
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaModifierInput()`

:   &mdash;

**Properties**

`public ulong ApplicationSequence`

:   &mdash;

`public FormulaContributionKind Kind`

:   &mdash;

`public int ModifierIndex`

:   &mdash;

`public int Priority`

:   &mdash;

`public StableId StatusDefinitionId`

:   &mdash;

`public Fixed64 Value`

:   &mdash;

---

## FormulaPreview

```csharp
public sealed class FormulaPreview
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Trace/FormulaTrace.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaPreview()`

:   &mdash;

**Properties**

`public Chance64 CriticalChance`

:   &mdash;

`public Chance64 HitChance`

:   &mdash;

`public bool IsExact`

:   &mdash;

`public Fixed64 Maximum`

:   &mdash;

`public Fixed64 Minimum`

:   &mdash;

`public Chance64 StatusChance`

:   &mdash;

---

## FormulaPreviewContext

```csharp
public sealed class FormulaPreviewContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaPreviewContext(FormulaContext context)`

:   &mdash;

**Properties**

`public FormulaContext Context`

:   &mdash;

---

## FormulaRandomBoundKind

```csharp
public enum FormulaRandomBoundKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Fixed` | &mdash; |
| `VarianceWidth` | &mdash; |

---

## FormulaRandomInputDescriptor

```csharp
public readonly struct FormulaRandomInputDescriptor
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaRandomInputDescriptor(StableId inputId, uint exclusiveUpperBound, bool conditional)`

:   &mdash;

**Properties**

`public FormulaRandomBoundKind BoundKind`

:   &mdash;

`public bool Conditional`

:   &mdash;

`public uint ExclusiveUpperBound`

:   &mdash;

`public StableId InputId`

:   &mdash;

**Methods**

`public static FormulaRandomInputDescriptor ForVarianceWidth(StableId inputId, bool conditional)`

:   &mdash;

`public uint ResolveExclusiveUpperBound(FormulaContext context)`

:   &mdash;

---

## FormulaRandomSample

```csharp
public readonly struct FormulaRandomSample
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Trace/FormulaTrace.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaRandomSample(StableId inputId, uint exclusiveUpperBound, uint sample)`

:   &mdash;

**Properties**

`public uint ExclusiveUpperBound`

:   &mdash;

`public StableId InputId`

:   &mdash;

`public uint Sample`

:   &mdash;

---

## FormulaResult

```csharp
public sealed class FormulaResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaResult(bool hit, bool critical, Fixed64 value, FormulaAttribution attribution)`

:   &mdash;

**Properties**

`public FormulaAttribution Attribution`

:   &mdash;

`public bool Critical`

:   &mdash;

`public bool Hit`

:   &mdash;

`public Fixed64 Value`

:   &mdash;

---

## FormulaValidationContext

```csharp
public sealed class FormulaValidationContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public FormulaValidationContext(CompiledBattleContent content)`

:   &mdash;

**Properties**

`public CompiledBattleContent Content`

:   &mdash;

---

## IAiPolicy

```csharp
public interface IAiPolicy : IMechanicsImplementation
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## IEffectResolver

```csharp
public interface IEffectResolver : IMechanicsImplementation
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## IFormula

```csharp
public interface IFormula : IMechanicsImplementation
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## IMechanicsImplementation

```csharp
public interface IMechanicsImplementation
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## IMechanicsRandomSource

```csharp
public interface IMechanicsRandomSource
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## IReactionRule

```csharp
public interface IReactionRule : IMechanicsImplementation
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ITargetResolver

```csharp
public interface ITargetResolver : IMechanicsImplementation
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## MechanicsCategoryTag

```csharp
public enum MechanicsCategoryTag : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/BattleMechanicsRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Formula` | &mdash; |
| `Effect` | &mdash; |
| `Target` | &mdash; |
| `Ai` | &mdash; |
| `Reaction` | &mdash; |

---

## MechanicsDiagnosticIds

```csharp
public static class MechanicsDiagnosticIds
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsDiagnostics.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## MechanicsIds

```csharp
public static class MechanicsIds
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsIds.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## MechanicsRegistryBinding

```csharp
public readonly struct MechanicsRegistryBinding : IEquatable<MechanicsRegistryBinding>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/BattleMechanicsRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public MechanicsRegistryBinding(MechanicsCategoryTag category, StableId implementationId, int contractVersion)`

:   &mdash;

**Properties**

`public MechanicsCategoryTag Category`

:   &mdash;

`public int ContractVersion`

:   &mdash;

`public StableId ImplementationId`

:   &mdash;

**Methods**

`public bool Equals(MechanicsRegistryBinding other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## MechanicsResolveResult

```csharp
public sealed class MechanicsResolveResult
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/BattleMechanicsRegistry.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public Diagnostic Diagnostic`

:   &mdash;

`public T Implementation`

:   &mdash;

`public bool IsSuccess`

:   &mdash;

---

## ReactionValidationContext

```csharp
public sealed class ReactionValidationContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ReactionValidationContext(CompiledBattleContent content)`

:   &mdash;

**Properties**

`public CompiledBattleContent Content`

:   &mdash;

---

## SchedulerAdjustmentKind

```csharp
public enum SchedulerAdjustmentKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Effects/EffectPlan.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `ReadyTickDelta` | &mdash; |
| `GaugeDelta` | &mdash; |

---

## StatusApplicationPreview

```csharp
public sealed class StatusApplicationPreview
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Formulas/BattleFormulaService.cs</small>

RNG-free status application calculation used by runtime and tooltips.

**Properties**

`public Chance64 BaseChance`

:   &mdash;

`public Chance64 FinalChance`

:   &mdash;

`public bool Immune`

:   &mdash;

`public Chance64 Resistance`

:   &mdash;

`public StableId StatusId`

:   &mdash;

`public StableId TargetId`

:   &mdash;

---

## TargetValidationContext

```csharp
public sealed class TargetValidationContext
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/MechanicsContracts.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public TargetValidationContext(CompiledBattleContent content)`

:   &mdash;

**Properties**

`public CompiledBattleContent Content`

:   &mdash;

---

## ValidationReport

```csharp
public sealed class ValidationReport
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Mechanics/ValidationReport.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public ValidationReport()`

:   &mdash;

**Properties**

`public FrozenList<Diagnostic> Errors`

:   &mdash;

`public bool IsValid`

:   &mdash;

`public static ValidationReport Valid`

:   &mdash;

`public FrozenList<Diagnostic> Warnings`

:   &mdash;

**Methods**

`public static ValidationReport Error(StableId id, string detail = null)`

:   &mdash;

`public static ValidationReport Warning(StableId id, string detail = null)`

:   &mdash;

---

