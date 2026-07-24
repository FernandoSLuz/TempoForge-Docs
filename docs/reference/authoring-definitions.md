# Authoring definitions

69 types in this area.

!!! abstract "On this page"
    [AiConditionDefinition](#aiconditiondefinition) &middot; [AiConditionKind](#aiconditionkind) &middot; [AiPolicyDefinition](#aipolicydefinition) &middot; [AiRuleDefinition](#airuledefinition) &middot; [AuthoringValueTag](#authoringvaluetag) &middot; [BattleContentCatalog](#battlecontentcatalog) &middot; [BattleResultPolicyKind](#battleresultpolicykind) &middot; [BattleRulesDefinition](#battlerulesdefinition) &middot; [CombatantDefinition](#combatantdefinition) &middot; [CombatantResourceEntryDefinition](#combatantresourceentrydefinition) &middot; [CombatantStatEntryDefinition](#combatantstatentrydefinition) &middot; [CompiledAiCondition](#compiledaicondition) &middot; [CompiledAiPolicyDefinition](#compiledaipolicydefinition) &middot; [CompiledAiRule](#compiledairule) &middot; [CompiledBattleContent](#compiledbattlecontent) &middot; [CompiledBattleRulesV3](#compiledbattlerulesv3) &middot; [CompiledCombatantDefinition](#compiledcombatantdefinition) &middot; [CompiledEffectEntry](#compiledeffectentry) &middot; [CompiledMechanicsBinding](#compiledmechanicsbinding) &middot; [CompiledReactionDefinition](#compiledreactiondefinition) &middot; [CompiledResourceDefault](#compiledresourcedefault) &middot; [CompiledResourceDefinition](#compiledresourcedefinition) &middot; [CompiledSkillDefinition](#compiledskilldefinition) &middot; [CompiledStatDefinition](#compiledstatdefinition) &middot; [CompiledStatModifier](#compiledstatmodifier) &middot; [CompiledStatValue](#compiledstatvalue) &middot; [CompiledStatusDefinition](#compiledstatusdefinition) &middot; [CompiledStatusDuration](#compiledstatusduration) &middot; [CompiledStatusPeriodicPolicy](#compiledstatusperiodicpolicy) &middot; [CompiledStatusResistance](#compiledstatusresistance) &middot; [EffectDefinition](#effectdefinition) &middot; [EffectUseDefinition](#effectusedefinition) &middot; [EncounterDefinition](#encounterdefinition) &middot; [EncounterTeamDefinition](#encounterteamdefinition) &middot; [FormationAssignmentDefinition](#formationassignmentdefinition) &middot; [InitialStatusApplicationDefinition](#initialstatusapplicationdefinition) &middot; [InvalidTargetPolicy](#invalidtargetpolicy) &middot; [MechanicsImplementationReference](#mechanicsimplementationreference) &middot; [MechanicsImplementationReferenceDefinition](#mechanicsimplementationreferencedefinition) &middot; [ModifierStage](#modifierstage) &middot; [PropertyEntryDefinition](#propertyentrydefinition) &middot; [PropertyEntrySnapshot](#propertyentrysnapshot) &middot; [PropertySetDefinition](#propertysetdefinition) &middot; [ReactionDefinition](#reactiondefinition) &middot; [ReactionTriggerPhase](#reactiontriggerphase) &middot; [ResistanceMatchKind](#resistancematchkind) &middot; [ResourceDefinition](#resourcedefinition) &middot; [SchedulerDefinition](#schedulerdefinition) &middot; [SkillCostDefinition](#skillcostdefinition) &middot; [SkillDefinition](#skilldefinition) &middot; [StableIdDefinition](#stableiddefinition) &middot; [StartCombatantV3](#startcombatantv3) &middot; [StartResourceV3](#startresourcev3) &middot; [StartStatusApplicationV3](#startstatusapplicationv3) &middot; [StartTeamV3](#startteamv3) &middot; [StartingHealthMode](#startinghealthmode) &middot; [StatDefinition](#statdefinition) &middot; [StatusDefinition](#statusdefinition) &middot; [StatusDurationClock](#statusdurationclock) &middot; [StatusModifierDefinition](#statusmodifierdefinition) &middot; [StatusPeriodicPhase](#statusperiodicphase) &middot; [StatusPolarity](#statuspolarity) &middot; [StatusResistanceDefinition](#statusresistancedefinition) &middot; [StatusStackPolicy](#statusstackpolicy) &middot; [TargetDefinition](#targetdefinition) &middot; [TargetLockPolicy](#targetlockpolicy) &middot; [TeamDefinition](#teamdefinition) &middot; [TeamMemberDefinition](#teammemberdefinition) &middot; [TeamMemberResourceOverrideDefinition](#teammemberresourceoverridedefinition)

## AiConditionDefinition

```csharp
public sealed class AiConditionDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## AiConditionKind

```csharp
public enum AiConditionKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `ActorHealthAtMost` | &mdash; |
| `ActorResourceAtLeast` | &mdash; |
| `ActorHasStatus` | &mdash; |
| `AllyCountAtMost` | &mdash; |
| `EnemyCountAtLeast` | &mdash; |
| `SkillReady` | &mdash; |
| `TargetAvailable` | &mdash; |

---

## AiPolicyDefinition

```csharp
public sealed class AiPolicyDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/AiPolicyDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## AiRuleDefinition

```csharp
public sealed class AiRuleDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## AuthoringValueTag

```csharp
public enum AuthoringValueTag : byte
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/PropertyDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Boolean` | &mdash; |
| `Int32` | &mdash; |
| `Int64` | &mdash; |
| `UInt64` | &mdash; |
| `Fixed64` | &mdash; |
| `Chance64` | &mdash; |
| `StableId` | &mdash; |
| `String` | &mdash; |
| `BooleanArray` | &mdash; |
| `Int32Array` | &mdash; |
| `Int64Array` | &mdash; |
| `UInt64Array` | &mdash; |
| `Fixed64Array` | &mdash; |
| `Chance64Array` | &mdash; |
| `StableIdArray` | &mdash; |
| `StringArray` | &mdash; |

---

## BattleContentCatalog

```csharp
public sealed class BattleContentCatalog : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/BattleContentCatalog.cs</small>

The sole root of a closed authoring graph. Compilation never searches the
project, Resources, Addressables, folders, or loaded assemblies.

---

## BattleResultPolicyKind

```csharp
public enum BattleResultPolicyKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `LastLivingTeam` | &mdash; |

---

## BattleRulesDefinition

```csharp
public sealed class BattleRulesDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/BattleRulesDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## CombatantDefinition

```csharp
public sealed class CombatantDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/CombatantDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## CombatantResourceEntryDefinition

```csharp
public sealed class CombatantResourceEntryDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## CombatantStatEntryDefinition

```csharp
public sealed class CombatantStatEntryDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## CompiledAiCondition

```csharp
public sealed class CompiledAiCondition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledAiCondition(AiConditionKind kind, StableId id, long threshold)`

:   &mdash;

**Properties**

`public StableId Id`

:   &mdash;

`public AiConditionKind Kind`

:   &mdash;

`public long Threshold`

:   &mdash;

---

## CompiledAiPolicyDefinition

```csharp
public sealed class CompiledAiPolicyDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledAiPolicyDefinition()`

:   &mdash;

**Properties**

`public MechanicsImplementationReference Implementation`

:   &mdash;

`public StableId PolicyId`

:   &mdash;

`public PropertySet Properties`

:   &mdash;

`public FrozenList<CompiledAiRule> Rules`

:   &mdash;

---

## CompiledAiRule

```csharp
public sealed class CompiledAiRule
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledAiRule()`

:   &mdash;

**Properties**

`public FrozenList<CompiledAiCondition> Conditions`

:   &mdash;

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

## CompiledBattleContent

```csharp
public sealed partial class CompiledBattleContent
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/CompiledBattleContent.B3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledBattleContent(StableId rulesId, IEnumerable<StableId> registeredCommandTypeIds)`

:   &mdash;

**Properties**

`public FrozenList<CompiledAiPolicyDefinition> AiPolicyDefinitionsV3`

:   &mdash;

`public FrozenList<CompiledAutomaticDecisionPolicy> AutomaticDecisionPolicies`

:   &mdash;

`public FrozenList<CompiledCombatantDefinition> CombatantDefinitionsV3`

:   &mdash;

`public int EngineVersion`

:   &mdash;

`public SimulationContractProfile Profile`

:   &mdash;

`public FrozenList<ReactionCycleDiagnostic> ReactionCycleDiagnostics`

:   &mdash;

`public FrozenList<CompiledReactionDefinition> ReactionDefinitionsV3`

:   &mdash;

`public FrozenList<StableId> RegisteredCommandTypeIds`

:   &mdash;

`public FrozenList<CompiledMechanicsBinding> RequiredMechanicsBindings`

:   &mdash;

`public FrozenList<CompiledResourceDefinition> ResourceDefinitionsV3`

:   &mdash;

`public StableId RulesId`

:   &mdash;

`public CompiledBattleRulesV3 RulesV3`

:   &mdash;

`public FrozenList<CompiledSchedulerDefinition> SchedulerDefinitions`

:   &mdash;

`public int SchemaVersion`

:   &mdash;

`public FrozenList<CompiledSkillDefinition> SkillDefinitionsV3`

:   &mdash;

`public FrozenList<CompiledSkillTiming> SkillTimings`

:   &mdash;

`public FrozenList<CompiledStatDefinition> StatDefinitionsV3`

:   &mdash;

`public FrozenList<CompiledStatusDefinition> StatusDefinitionsV3`

:   &mdash;

**Methods**

`public static CompiledBattleContent CreateB1Default()`

:   &mdash;

`public static CompiledBattleContent CreateB2()`

:   &mdash;

`public static CompiledBattleContent CreateB3()`

:   &mdash;

`public static CompiledBattleContent CreateB3()`

:   &mdash;

`public CompiledAiPolicyDefinition FindAiPolicyDefinitionV3(StableId id)`

:   &mdash;

`public CompiledAutomaticDecisionPolicy FindAutomaticDecisionPolicy(StableId policyId)`

:   &mdash;

`public CompiledCombatantDefinition FindCombatantDefinitionV3(StableId id)`

:   &mdash;

`public CompiledReactionDefinition FindReactionDefinitionV3(StableId id)`

:   &mdash;

`public CompiledResourceDefinition FindResourceDefinitionV3(StableId id)`

:   &mdash;

`public CompiledSchedulerDefinition FindSchedulerDefinition(StableId schedulerId)`

:   &mdash;

`public CompiledSkillDefinition FindSkillDefinitionV3(StableId id)`

:   &mdash;

`public CompiledSkillTiming FindSkillTiming(StableId skillId)`

:   &mdash;

`public CompiledStatDefinition FindStatDefinitionV3(StableId id)`

:   &mdash;

`public CompiledStatusDefinition FindStatusDefinitionV3(StableId id)`

:   &mdash;

`public bool RegistersCommand(StableId commandType)`

:   &mdash;

`public static B3CreationResult<CompiledBattleContent> TryCreateB3()`

:   &mdash;

`public static B3CreationResult<CompiledBattleContent> TryCreateB3()`

:   &mdash;

---

## CompiledBattleRulesV3

```csharp
public sealed class CompiledBattleRulesV3
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3BattleRules.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledBattleRulesV3()`

:   &mdash;

**Properties**

`public StableId CriticalChanceStatId`

:   &mdash;

`public MechanicsImplementationReference CriticalFormula`

:   &mdash;

`public Fixed64 CriticalMultiplier`

:   &mdash;

`public MechanicsImplementationReference DamageFormula`

:   &mdash;

`public MechanicsImplementationReference DefenseFormula`

:   &mdash;

`public StableId DefenseStatId`

:   &mdash;

`public Fixed64 FormulaMaximum`

:   &mdash;

`public Fixed64 FormulaMinimum`

:   &mdash;

`public MechanicsImplementationReference HealingFormula`

:   &mdash;

`public StableId MagicStatId`

:   &mdash;

`public long MaximumBattleTicks`

:   &mdash;

`public StableId MaximumHealthStatId`

:   &mdash;

`public int MaximumReactionCount`

:   &mdash;

`public int MaximumReactionDepth`

:   &mdash;

`public ulong MaximumRootActions`

:   &mdash;

`public StableId PowerStatId`

:   &mdash;

`public BattleResultPolicyKind ResultPolicy`

:   &mdash;

`public StableId RulesId`

:   &mdash;

`public StableId SpeedStatId`

:   &mdash;

`public StableId SpiritStatId`

:   &mdash;

`public MechanicsImplementationReference StatusChanceFormula`

:   &mdash;

`public Fixed64 VarianceMaximum`

:   &mdash;

`public Fixed64 VarianceMinimum`

:   &mdash;

---

## CompiledCombatantDefinition

```csharp
public sealed class CompiledCombatantDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3BattleRules.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledCombatantDefinition()`

:   &mdash;

**Properties**

`public FrozenList<CompiledStatValue> BaseStats`

:   &mdash;

`public StableId? DefaultAiPolicyId`

:   &mdash;

`public StableId DefinitionId`

:   &mdash;

`public FrozenList<StableId> GrantedSkillIds`

:   &mdash;

`public FrozenList<StableId> ImmuneStatusIds`

:   &mdash;

`public FrozenList<StableId> ImmuneStatusTags`

:   &mdash;

`public FrozenList<StableId> IntrinsicReactionDefinitionIds`

:   &mdash;

`public FrozenList<CompiledStatusResistance> Resistances`

:   &mdash;

`public FrozenList<CompiledResourceDefault> ResourceDefaults`

:   &mdash;

`public FrozenList<StableId> Tags`

:   &mdash;

---

## CompiledEffectEntry

```csharp
public sealed class CompiledEffectEntry
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledEffectEntry()`

:   &mdash;

**Properties**

`public FrozenList<StableId> EffectTags`

:   &mdash;

`public StableId EntryId`

:   &mdash;

`public PropertySet Properties`

:   &mdash;

`public MechanicsImplementationReference Resolver`

:   &mdash;

---

## CompiledMechanicsBinding

```csharp
public sealed class CompiledMechanicsBinding
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/CompiledBattleContent.B3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledMechanicsBinding()`

:   &mdash;

**Properties**

`public MechanicsRegistryBinding Binding`

:   &mdash;

`public Sha256Digest ValidatedPropertyHash`

:   &mdash;

---

## CompiledReactionDefinition

```csharp
public sealed class CompiledReactionDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledReactionDefinition()`

:   &mdash;

**Properties**

`public bool ConsumeRequiredStatusOnEnqueue`

:   &mdash;

`public FrozenList<CompiledEffectEntry> Effects`

:   &mdash;

`public MechanicsImplementationReference Implementation`

:   &mdash;

`public bool OncePerRoot`

:   &mdash;

`public int Priority`

:   &mdash;

`public PropertySet Properties`

:   &mdash;

`public StableId? RequiredStatusDefinitionId`

:   &mdash;

`public StableId RuleId`

:   &mdash;

`public ReactionTriggerPhase TriggerPhase`

:   &mdash;

---

## CompiledResourceDefault

```csharp
public readonly struct CompiledResourceDefault
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledResourceDefault(StableId resourceId, int value)`

:   &mdash;

**Properties**

`public StableId ResourceId`

:   &mdash;

`public int Value`

:   &mdash;

---

## CompiledResourceDefinition

```csharp
public sealed class CompiledResourceDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledResourceDefinition(StableId resourceId, int minimum, int maximum, bool mayCrossZero)`

:   &mdash;

**Properties**

`public int Maximum`

:   &mdash;

`public bool MayCrossZero`

:   &mdash;

`public int Minimum`

:   &mdash;

`public StableId ResourceId`

:   &mdash;

---

## CompiledSkillDefinition

```csharp
public sealed class CompiledSkillDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledSkillDefinition()`

:   &mdash;

**Properties**

`public FrozenList<CompiledEffectEntry> Effects`

:   &mdash;

`public InvalidTargetPolicy InvalidTargetPolicy`

:   &mdash;

`public StableId SkillId`

:   &mdash;

`public FrozenList<StableId> Tags`

:   &mdash;

`public TargetLockPolicy TargetLockPolicy`

:   &mdash;

`public PropertySet TargetProperties`

:   &mdash;

`public MechanicsImplementationReference TargetResolver`

:   &mdash;

`public CompiledSkillTiming Timing`

:   &mdash;

---

## CompiledStatDefinition

```csharp
public sealed class CompiledStatDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledStatDefinition()`

:   &mdash;

**Properties**

`public Fixed64 Maximum`

:   &mdash;

`public Fixed64 Minimum`

:   &mdash;

`public FrozenList<StableId> SemanticTags`

:   &mdash;

`public StableId StatId`

:   &mdash;

---

## CompiledStatModifier

```csharp
public sealed class CompiledStatModifier
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledStatModifier()`

:   &mdash;

**Properties**

`public int Priority`

:   &mdash;

`public ModifierStage Stage`

:   &mdash;

`public StableId StatId`

:   &mdash;

`public Fixed64 Value`

:   &mdash;

---

## CompiledStatValue

```csharp
public readonly struct CompiledStatValue
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledStatValue(StableId statId, Fixed64 value)`

:   &mdash;

**Properties**

`public StableId StatId`

:   &mdash;

`public Fixed64 Value`

:   &mdash;

---

## CompiledStatusDefinition

```csharp
public sealed class CompiledStatusDefinition
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3Definitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledStatusDefinition()`

:   &mdash;

**Properties**

`public bool Dispellable`

:   &mdash;

`public CompiledStatusDuration Duration`

:   &mdash;

`public StableId? ExclusiveGroupId`

:   &mdash;

`public int MaximumStacks`

:   &mdash;

`public FrozenList<CompiledStatModifier> Modifiers`

:   &mdash;

`public CompiledStatusPeriodicPolicy Periodic`

:   &mdash;

`public FrozenList<CompiledEffectEntry> PeriodicEffects`

:   &mdash;

`public bool PersistOnDeath`

:   &mdash;

`public StatusPolarity Polarity`

:   &mdash;

`public bool PreventNextOpportunity`

:   &mdash;

`public FrozenList<StableId> ReactionDefinitionIds`

:   &mdash;

`public bool RefreshKeepHigherMetadata`

:   &mdash;

`public FrozenList<StableId> RestrictedSkillTags`

:   &mdash;

`public StatusStackPolicy StackPolicy`

:   &mdash;

`public StableId StatusId`

:   &mdash;

`public Fixed64 Strength`

:   &mdash;

`public FrozenList<StableId> Tags`

:   &mdash;

`public bool TauntHostileSingleTarget`

:   &mdash;

---

## CompiledStatusDuration

```csharp
public sealed class CompiledStatusDuration
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledStatusDuration(StatusDurationClock clock, int amount)`

:   &mdash;

**Properties**

`public int Amount`

:   &mdash;

`public StatusDurationClock Clock`

:   &mdash;

---

## CompiledStatusPeriodicPolicy

```csharp
public sealed class CompiledStatusPeriodicPolicy
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledStatusPeriodicPolicy(StatusPeriodicPhase phase, int interval)`

:   &mdash;

**Properties**

`public int Interval`

:   &mdash;

`public StatusPeriodicPhase Phase`

:   &mdash;

---

## CompiledStatusResistance

```csharp
public readonly struct CompiledStatusResistance
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public CompiledStatusResistance(ResistanceMatchKind kind, StableId id, Chance64 resistance)`

:   &mdash;

**Properties**

`public StableId Id`

:   &mdash;

`public ResistanceMatchKind Kind`

:   &mdash;

`public Chance64 Resistance`

:   &mdash;

---

## EffectDefinition

```csharp
public sealed class EffectDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/EffectDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## EffectUseDefinition

```csharp
public sealed class EffectUseDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## EncounterDefinition

```csharp
public sealed class EncounterDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/EncounterDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## EncounterTeamDefinition

```csharp
public sealed class EncounterTeamDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## FormationAssignmentDefinition

```csharp
public sealed class FormationAssignmentDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## InitialStatusApplicationDefinition

```csharp
public sealed class InitialStatusApplicationDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## InvalidTargetPolicy

```csharp
public enum InvalidTargetPolicy : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `SkipInvalid` | &mdash; |
| `CancelAction` | &mdash; |
| `RetargetStable` | &mdash; |

---

## MechanicsImplementationReference

```csharp
public readonly struct MechanicsImplementationReference : IEquatable<MechanicsImplementationReference>
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public MechanicsImplementationReference(StableId implementationId, int contractVersion)`

:   &mdash;

**Properties**

`public int ContractVersion`

:   &mdash;

`public StableId ImplementationId`

:   &mdash;

**Methods**

`public bool Equals(MechanicsImplementationReference other)`

:   &mdash;

`public override bool Equals(object obj)`

:   &mdash;

`public override int GetHashCode()`

:   &mdash;

---

## MechanicsImplementationReferenceDefinition

```csharp
public sealed class MechanicsImplementationReferenceDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ModifierStage

```csharp
public enum ModifierStage : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `FlatStat` | &mdash; |
| `MultiplicativeStat` | &mdash; |
| `Outgoing` | &mdash; |
| `Incoming` | &mdash; |
| `CriticalChance` | &mdash; |
| `CriticalMultiplier` | &mdash; |

---

## PropertyEntryDefinition

```csharp
public sealed class PropertyEntryDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/PropertyDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public string KeyRaw`

:   &mdash;

`public AuthoringValueTag Tag`

:   &mdash;

**Methods**

`public PropertyEntrySnapshot CreateSnapshot()`

:   &mdash;

`public static PropertyEntryDefinition FromBoolean(string key, bool value)`

:   &mdash;

`public static PropertyEntryDefinition FromBooleans(string key, params bool[] values)`

:   &mdash;

`public static PropertyEntryDefinition FromChance64Raw(string key, long value)`

:   &mdash;

`public static PropertyEntryDefinition FromChance64Raws(string key, params long[] values)`

:   &mdash;

`public static PropertyEntryDefinition FromFixed64Raw(string key, long value)`

:   &mdash;

`public static PropertyEntryDefinition FromFixed64Raws(string key, params long[] values)`

:   &mdash;

`public static PropertyEntryDefinition FromInt32(string key, int value)`

:   &mdash;

`public static PropertyEntryDefinition FromInt32s(string key, params int[] values)`

:   &mdash;

`public static PropertyEntryDefinition FromInt64(string key, long value)`

:   &mdash;

`public static PropertyEntryDefinition FromInt64s(string key, params long[] values)`

:   &mdash;

`public static PropertyEntryDefinition FromStableId(string key, string value)`

:   &mdash;

`public static PropertyEntryDefinition FromStableIds(string key, params string[] values)`

:   &mdash;

`public static PropertyEntryDefinition FromString(string key, string value)`

:   &mdash;

`public static PropertyEntryDefinition FromStrings(string key, params string[] values)`

:   &mdash;

`public static PropertyEntryDefinition FromUInt64(string key, ulong value)`

:   &mdash;

`public static PropertyEntryDefinition FromUInt64s(string key, params ulong[] values)`

:   &mdash;

---

## PropertyEntrySnapshot

```csharp
public sealed class PropertyEntrySnapshot
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/PropertyDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Properties**

`public bool[] BooleanArray`

:   &mdash;

`public bool BooleanValue`

:   &mdash;

`public long Chance64Raw`

:   &mdash;

`public long[] Chance64RawArray`

:   &mdash;

`public int DeclaredValueCount`

:   &mdash;

`public long Fixed64Raw`

:   &mdash;

`public long[] Fixed64RawArray`

:   &mdash;

`public int[] Int32Array`

:   &mdash;

`public int Int32Value`

:   &mdash;

`public long[] Int64Array`

:   &mdash;

`public long Int64Value`

:   &mdash;

`public string KeyRaw`

:   &mdash;

`public string StableIdRaw`

:   &mdash;

`public string[] StableIdRawArray`

:   &mdash;

`public string[] StringArray`

:   &mdash;

`public string StringValue`

:   &mdash;

`public AuthoringValueTag Tag`

:   &mdash;

`public ulong[] UInt64Array`

:   &mdash;

`public ulong UInt64Value`

:   &mdash;

`public bool ValueLimitExceeded`

:   &mdash;

---

## PropertySetDefinition

```csharp
public sealed class PropertySetDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/PropertyDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public PropertySetDefinition()`

:   &mdash;

`public PropertySetDefinition(params PropertyEntryDefinition[] entries)`

:   &mdash;

**Properties**

`public PropertyEntryDefinition[] Entries`

:   &mdash;

**Methods**

`public int Compare()`

:   &mdash;

---

## ReactionDefinition

```csharp
public sealed class ReactionDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/ReactionDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## ReactionTriggerPhase

```csharp
public enum ReactionTriggerPhase : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `BeforeEffect` | &mdash; |
| `AfterEffect` | &mdash; |

---

## ResistanceMatchKind

```csharp
public enum ResistanceMatchKind : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `StatusDefinition` | &mdash; |
| `StatusTag` | &mdash; |

---

## ResourceDefinition

```csharp
public sealed class ResourceDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/ResourceDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## SchedulerDefinition

```csharp
public sealed class SchedulerDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/SchedulerDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## SkillCostDefinition

```csharp
public sealed class SkillCostDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## SkillDefinition

```csharp
public sealed class SkillDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/SkillDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## StableIdDefinition

```csharp
public abstract class StableIdDefinition : ScriptableObject
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/StableIdDefinition.cs</small>

Base class for authoring assets whose identity survives file, folder, label,
and localization changes. Identity is never generated or repaired at runtime.

**Properties**

`public int AuthoringSchemaVersion`

:   &mdash;

`public string DisplayLabel`

:   &mdash;

`public string LocalizationKey`

:   &mdash;

`public string StableIdRaw`

:   &mdash;

---

## StartCombatantV3

```csharp
public sealed class StartCombatantV3
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/BattleStartV3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StartCombatantV3()`

:   &mdash;

**Properties**

`public StableId? AiPolicyOverrideId`

:   &mdash;

`public StableId CombatantDefinitionId`

:   &mdash;

`public StableId CombatantId`

:   &mdash;

`public DecisionControlKind ControlKind`

:   &mdash;

`public int CurrentHealth`

:   &mdash;

`public StableId FormationRowId`

:   &mdash;

`public StableId FormationSideId`

:   &mdash;

`public StableId FormationSlotId`

:   &mdash;

`public int InitialAtbGaugeUnits`

:   &mdash;

`public FrozenList<StartStatusApplicationV3> InitialStatuses`

:   &mdash;

`public int MaximumHealth`

:   &mdash;

`public FrozenList<StartResourceV3> Resources`

:   &mdash;

`public bool Targetable`

:   &mdash;

---

## StartResourceV3

```csharp
public readonly struct StartResourceV3
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/BattleStartV3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StartResourceV3(StableId resourceId, int current)`

:   &mdash;

**Properties**

`public int Current`

:   &mdash;

`public StableId ResourceId`

:   &mdash;

---

## StartStatusApplicationV3

```csharp
public sealed class StartStatusApplicationV3
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/BattleStartV3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StartStatusApplicationV3(StableId statusDefinitionId, StableId? sourceCombatantId, int stackCount)`

:   &mdash;

**Properties**

`public StableId? SourceCombatantId`

:   &mdash;

`public int StackCount`

:   &mdash;

`public StableId StatusDefinitionId`

:   &mdash;

---

## StartTeamV3

```csharp
public sealed class StartTeamV3
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/BattleStartV3.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

**Constructors**

`public StartTeamV3(StableId teamId, IEnumerable<StartCombatantV3> combatants)`

:   &mdash;

**Properties**

`public FrozenList<StartCombatantV3> Combatants`

:   &mdash;

`public StableId TeamId`

:   &mdash;

---

## StartingHealthMode

```csharp
public enum StartingHealthMode : byte
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `FullHealth` | &mdash; |
| `ExplicitCurrentHealth` | &mdash; |

---

## StatDefinition

```csharp
public sealed class StatDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/StatDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## StatusDefinition

```csharp
public sealed class StatusDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/StatusDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## StatusDurationClock

```csharp
public enum StatusDurationClock : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `OwnerActionStart` | &mdash; |
| `OwnerActionEnd` | &mdash; |
| `OwnerOpportunity` | &mdash; |
| `ElapsedTicks` | &mdash; |

---

## StatusModifierDefinition

```csharp
public sealed class StatusModifierDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## StatusPeriodicPhase

```csharp
public enum StatusPeriodicPhase : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `None` | &mdash; |
| `OwnerActionStart` | &mdash; |
| `OwnerActionEnd` | &mdash; |
| `ElapsedBoundary` | &mdash; |

---

## StatusPolarity

```csharp
public enum StatusPolarity : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Neutral` | &mdash; |
| `Buff` | &mdash; |
| `Debuff` | &mdash; |

---

## StatusResistanceDefinition

```csharp
public sealed class StatusResistanceDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## StatusStackPolicy

```csharp
public enum StatusStackPolicy : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `Refresh` | &mdash; |
| `AddStacksRefreshAll` | &mdash; |
| `Independent` | &mdash; |
| `Replace` | &mdash; |
| `KeepHigher` | &mdash; |

---

## TargetDefinition

```csharp
public sealed class TargetDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TargetDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## TargetLockPolicy

```csharp
public enum TargetLockPolicy : byte
```

`TempoForge.Simulation` &middot; <small>Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

| Value | Meaning |
| --- | --- |
| `LockAtAcceptance` | &mdash; |

---

## TeamDefinition

```csharp
public sealed class TeamDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TeamDefinition.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## TeamMemberDefinition

```csharp
public sealed class TeamMemberDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

## TeamMemberResourceOverrideDefinition

```csharp
public sealed class TeamMemberResourceOverrideDefinition
```

`TempoForge.Authoring` &middot; <small>Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

!!! warning "Not yet documented"
    This type has no summary comment in the source. Its name and signature are accurate; the description is missing.

---

