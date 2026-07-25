# Authoring definitions

57 types in this area.

!!! abstract "On this page"
    [AiConditionDefinition](#aiconditiondefinition) &middot; [AiConditionKind](#aiconditionkind) &middot; [AiPolicyDefinition](#aipolicydefinition) &middot; [AiRuleDefinition](#airuledefinition) &middot; [AuthoringValueTag](#authoringvaluetag) &middot; [BattleContentCatalog](#battlecontentcatalog) &middot; [BattleResultPolicyKind](#battleresultpolicykind) &middot; [BattleRulesDefinition](#battlerulesdefinition) &middot; [CombatantDefinition](#combatantdefinition) &middot; [CombatantResourceEntryDefinition](#combatantresourceentrydefinition) &middot; [CombatantStatEntryDefinition](#combatantstatentrydefinition) &middot; [CompiledAiCondition](#compiledaicondition) &middot; [CompiledAiPolicyDefinition](#compiledaipolicydefinition) &middot; [CompiledAiRule](#compiledairule) &middot; [CompiledBattleContent](#compiledbattlecontent) &middot; [CompiledCombatantDefinition](#compiledcombatantdefinition) &middot; [CompiledEffectEntry](#compiledeffectentry) &middot; [CompiledSkillDefinition](#compiledskilldefinition) &middot; [CompiledStatusDefinition](#compiledstatusdefinition) &middot; [EffectDefinition](#effectdefinition) &middot; [EffectUseDefinition](#effectusedefinition) &middot; [EncounterDefinition](#encounterdefinition) &middot; [EncounterTeamDefinition](#encounterteamdefinition) &middot; [FormationAssignmentDefinition](#formationassignmentdefinition) &middot; [InitialStatusApplicationDefinition](#initialstatusapplicationdefinition) &middot; [InvalidTargetPolicy](#invalidtargetpolicy) &middot; [MechanicsImplementationReference](#mechanicsimplementationreference) &middot; [MechanicsImplementationReferenceDefinition](#mechanicsimplementationreferencedefinition) &middot; [ModifierStage](#modifierstage) &middot; [PropertyEntryDefinition](#propertyentrydefinition) &middot; [PropertySetDefinition](#propertysetdefinition) &middot; [ReactionDefinition](#reactiondefinition) &middot; [ReactionTriggerPhase](#reactiontriggerphase) &middot; [ResistanceMatchKind](#resistancematchkind) &middot; [ResourceDefinition](#resourcedefinition) &middot; [SchedulerDefinition](#schedulerdefinition) &middot; [SkillCostDefinition](#skillcostdefinition) &middot; [SkillDefinition](#skilldefinition) &middot; [StableIdDefinition](#stableiddefinition) &middot; [StartCombatantV3](#startcombatantv3) &middot; [StartResourceV3](#startresourcev3) &middot; [StartStatusApplicationV3](#startstatusapplicationv3) &middot; [StartTeamV3](#startteamv3) &middot; [StartingHealthMode](#startinghealthmode) &middot; [StatDefinition](#statdefinition) &middot; [StatusDefinition](#statusdefinition) &middot; [StatusDurationClock](#statusdurationclock) &middot; [StatusModifierDefinition](#statusmodifierdefinition) &middot; [StatusPeriodicPhase](#statusperiodicphase) &middot; [StatusPolarity](#statuspolarity) &middot; [StatusResistanceDefinition](#statusresistancedefinition) &middot; [StatusStackPolicy](#statusstackpolicy) &middot; [TargetDefinition](#targetdefinition) &middot; [TargetLockPolicy](#targetlockpolicy) &middot; [TeamDefinition](#teamdefinition) &middot; [TeamMemberDefinition](#teammemberdefinition) &middot; [TeamMemberResourceOverrideDefinition](#teammemberresourceoverridedefinition)

## AiConditionDefinition

```csharp
public sealed class AiConditionDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

One gate on an `AiRuleDefinition`. `Kind` selects which
single operand below is read and leaves the rest ignored, so only the operand the
kind asks for has to be filled in. Conditions are tested against the battle state
without changing it, and the first one that fails drops the rule from
consideration.

---

## AiConditionKind

```csharp
public enum AiConditionKind : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3Definitions.cs</small>

The tests an AI rule may gate itself on. Each kind reads only the operands it
needs from the condition: some take an id, some a threshold, and
`AiConditionKind.ActorResourceAtLeast` takes both.

| Value | Meaning |
| --- | --- |
| `ActorHealthAtMost` | Passes while the acting combatant's current health is at or below the threshold. |
| `ActorResourceAtLeast` | Passes while the actor holds at least the threshold of the resource named by the id. |
| `ActorHasStatus` | Passes while the actor carries the status named by the id. |
| `AllyCountAtMost` | Passes while the living combatants on the actor's own team, the actor included, number at most the threshold. |
| `EnemyCountAtLeast` | Passes while the living combatants not on the actor's team number at least the threshold. |
| `SkillReady` | Passes while the skill named by the id exists and is off cooldown for the actor. |
| `TargetAvailable` | Passes while the skill named by the id can resolve at least one legal target for the actor. |

---

## AiPolicyDefinition

```csharp
public sealed class AiPolicyDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/AiPolicyDefinition.cs</small>

One reusable answer to "what does this combatant do when it gets an
opportunity": the registered AI policy that decides, the authored configuration
handed to it, and the candidate rules it decides between. A
`CombatantDefinition` names one as its default and a
`TeamMemberDefinition` may override it for a single member, so one
policy asset can drive a whole roster.

Which ordering field on a rule matters is the policy's business rather than the
rule's: the built-in priority and conditional policies read
`AiRuleDefinition.Priority` and ignore
`AiRuleDefinition.Weight`, while the built-in weighted policy does
the reverse. The implementation is resolved in the mechanics registry by
implementation ID and contract version together, and it validates the authored
properties itself while content compiles, so a mistyped argument fails the
compile rather than the battle.

---

## AiRuleDefinition

```csharp
public sealed class AiRuleDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

One candidate action inside an `AiPolicyDefinition`: the skill to use,
the conditions that must all hold before it may be chosen, and the ordering data
the policy selects with. Which ordering field matters depends on the policy: the
built-in priority and conditional policies read `Priority` and ignore
`Weight`, while the built-in weighted policy does the reverse.

---

## AuthoringValueTag

```csharp
public enum AuthoringValueTag : byte
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/PropertyDefinitions.cs</small>

Which of a `PropertyEntryDefinition`'s value slots is the live one.
An entry carries exactly one value, and its tag names both that value's type and,
for the `*Array` tags, that it holds many values rather than one.

There is no zero member. A default-constructed entry therefore has no tag at all,
captures no value, and is reported as an invalid property tag when compiled.

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

:material-star: **Start here**

```csharp
public sealed class BattleContentCatalog : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/BattleContentCatalog.cs</small>

The sole root of a closed authoring graph. Compilation never searches the
project, Resources, Addressables, folders, or loaded assemblies.

---

## BattleResultPolicyKind

```csharp
public enum BattleResultPolicyKind : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

How a battle's terminal result is decided. This schema defines only the
last-living-team rule, and compiled battle rules reject any other value,
so victory, defeat, and draw always derive from the living non-conceded
teams.

| Value | Meaning |
| --- | --- |
| `LastLivingTeam` | &mdash; |

---

## BattleRulesDefinition

:material-star: **Start here**

```csharp
public sealed class BattleRulesDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/BattleRulesDefinition.cs</small>

The one set of rules every battle compiled from a catalog runs under: which stat
assets carry the meanings the engine needs, which registered formulas it calls
for damage, healing, defense, criticals, and status chance, and the ceilings that
keep a battle finite.

The stat fields are how meaning is attached to otherwise anonymous stat assets:
the engine has no built-in "health" or "speed", it reads whichever
`StatDefinition` is named here. All seven are required and must be
reachable from the same catalog, so renaming or replacing a stat asset changes
the rules rather than breaking the engine. The ceilings bound a run instead of
tuning it, but not in the same way: reaching the root-action or tick ceiling
ends the battle as a stall rather than a victory, while the reaction depth and
count ceilings only suppress the reaction that would have crossed them and
leave the battle running.

---

## CombatantDefinition

:material-star: **Start here**

```csharp
public sealed class CombatantDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/CombatantDefinition.cs</small>

One reusable template for a fighter: the stats and resources it carries in, the
skills it may use, the AI policy that drives it, and what it shrugs off. It is
not a participant in itself - a `TeamMemberDefinition` instantiates
it into an encounter and may override its starting health, resources, and AI
policy - so the same definition can appear several times in one battle and on
both sides of it.

Nothing here is inferred. A stat left out of `BaseStats` has no base
value at all, but only two of the stats `BattleRulesDefinition` gives
meaning to are checked here: the maximum-health and speed stats must be present
and positive or the catalog fails to compile, while the other five are not
required at compile time and instead fail the battle with a missing-content
diagnostic the moment something reads them. A resource left out of
`ResourceDefaults` cannot be overridden per member either. Every
asset referenced from here must be reachable from the same catalog.

---

## CombatantResourceEntryDefinition

```csharp
public sealed class CombatantResourceEntryDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

One entry in a `CombatantDefinition`'s resource default list: the resource, and how
much of it the combatant starts with unless an encounter's team member entry overrides that
resource. Amounts here are plain integer units, not the fixed-point raw values a base stat uses.

---

## CombatantStatEntryDefinition

```csharp
public sealed class CombatantStatEntryDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

One entry in a `CombatantDefinition`'s base stat list: the stat, and the value that
combatant carries into battle. A stat the list omits has no base value at all, so the stats a
battle needs semantically -- maximum health and speed -- have to be listed explicitly or
compilation fails with a missing reference.

---

## CompiledAiCondition

```csharp
public sealed class CompiledAiCondition
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3Definitions.cs</small>

One gate on an AI rule. Immutable, and evaluated against the battle state without
changing it, so a condition can never advance or mutate a battle.

**Constructors**

`public CompiledAiCondition(AiConditionKind kind, StableId id, long threshold)`

:   Validates and freezes one condition. The kinds that name a resource, status, or skill require a valid `id`; the count and health kinds do not use one.
    - `kind` &mdash; Which test to run, and therefore which operands are read.
    - `id` &mdash; The resource, status, or skill the test is about. Leave it default for the kinds that take no operand.
    - `threshold` &mdash; Comparison bound, in the units of the kind: health points, resource units, or a combatant count. Ignored by the kinds that only test presence.

**Properties**

`public StableId Id`

:   The resource, status, or skill the test is about, required by the kinds that name one. The health and combatant-count kinds name nothing and read only `Threshold`; compiled content leaves this default (invalid) for them, and an id handed to one of those kinds directly is stored unchecked and never read.

`public AiConditionKind Kind`

:   Which test this condition runs, and therefore which of `Id` and `Threshold` are read at all. The unused operand is still stored, but it has no effect on the outcome.

`public long Threshold`

:   Comparison bound interpreted by `Kind`. Kinds that only test presence never read it.

---

## CompiledAiPolicyDefinition

```csharp
public sealed class CompiledAiPolicyDefinition
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3Definitions.cs</small>

One AI policy after compilation: the policy implementation to run and the rules it
chooses between. Immutable; the engine hands it to the implementation each time an
automatic combatant needs a decision, and the implementation only proposes
candidates, which the engine then validates before any of them can act.

**Constructors**

`public CompiledAiPolicyDefinition()`

:   Validates and freezes one AI policy. Rule ids must be unique within the policy, because candidates are matched back to their rule by id.
    - `implementation` &mdash; The `IAiPolicy` implementation to run, plus the contract version it was authored against.
    - `properties` &mdash; Authored arguments handed to the implementation. The built-in policies accept none and report any property as an error.
    - `rules` &mdash; Candidate rules, capped by `SimulationLimits.AutomaticPolicyEntries`. Nothing here forces the implementation to use them all.

**Properties**

`public MechanicsImplementationReference Implementation`

:   The AI implementation this policy runs, and the contract version it expects.

`public StableId PolicyId`

:   Identity of this policy in the compiled catalog. A combatant definition names one as its default and a battle start entry may name another in its place; either way the engine resolves the policy by this value when the combatant needs a decision.

`public PropertySet Properties`

:   Authored arguments passed to the implementation when it builds candidates.

`public FrozenList<CompiledAiRule> Rules`

:   The rules this policy may choose between. Rule ids are unique within the policy.

---

## CompiledAiRule

```csharp
public sealed class CompiledAiRule
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3Definitions.cs</small>

One candidate action inside an AI policy: a skill to use, the conditions that must
all hold first, and the ordering data the policy selects with. Immutable.

**Constructors**

`public CompiledAiRule()`

:   Validates and freezes one AI rule. Both ids are required, and the engine later rejects any candidate whose skill id does not match the rule it names.
    - `priority` &mdash; Higher wins. The priority and conditional policies take the highest-priority legal rule and ignore weight; the weighted policy ignores priority.
    - `weight` &mdash; Relative share used by the weighted policy only. A weight of zero removes the rule from a weighted draw.
    - `conditions` &mdash; Gates that must all pass for the rule to be considered. Capped by `SimulationLimits.ConditionsPerAiRule`.
    - `requestedTargets` &mdash; Targets the rule asks for. Stored sorted and de-duplicated, so authored order carries no meaning.

**Properties**

`public FrozenList<CompiledAiCondition> Conditions`

:   Gates on this rule. Every one must pass, in list order, before the rule is treated as a legal candidate.

`public int Priority`

:   Selection order for the priority and conditional policies, highest first. The weighted policy ignores it.

`public FrozenList<StableId> RequestedTargets`

:   Targets this rule requests when it is selected, sorted and de-duplicated. They still go through the skill's target resolver and its validation.

`public StableId RuleId`

:   Identity of this rule inside its policy, unique among that policy's rules. Proposed candidates and AI decision traces both refer back to a rule by this value, so it is what makes a recorded decision readable against the authored policy.

`public StableId SkillId`

:   The skill this rule uses. A candidate that names this rule has to propose the same skill; the engine rejects one that does not.

`public uint Weight`

:   Relative share for the weighted policy, ignored by the others. Zero drops the rule out of a weighted draw entirely.

---

## CompiledBattleContent

:material-star: **Start here**

```csharp
public sealed partial class CompiledBattleContent
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/CompiledBattleContent.B3.cs</small>

The validated, read-only content a battle runs on: rules, stats, resources,
combatants, skills, statuses, reactions, AI policies, schedulers, and the
mechanics registry those definitions resolve through.

All checking happens once, while the instance is being built. Holding one
is the guarantee: every stat, resource, status, skill, reaction, and AI
policy the definitions below name exists, every formula, effect, target,
AI, and reaction implementation it names resolved from the registry under a
matching contract version and passed that implementation's own validation,
no reaction cycle in it is fatal, and no collection exceeds its structural
limit. The one reference construction does not resolve is the resource a
skill timing charges as a cost; that check belongs to the authoring
compiler.

Every definition collection is sorted by id with duplicates and nulls
rejected, so iteration order is identical on every machine and the Find
methods below binary-search instead of scanning. Nothing about the instance
changes after construction, so the same content can back many battles.

**Constructors**

`public CompiledBattleContent(StableId rulesId, IEnumerable<StableId> registeredCommandTypeIds)`

:   Builds the smallest usable content: a rules identity and the set of command types the engine will accept, with no schedulers, skill timings, or automatic policies. This is B1 content, which is enough for a battle whose only outcome is a concession. Content that has to run skills comes from CreateB2, and content for the current schema from the CreateB3 factories.
    - `rulesId` &mdash; Names the rule set this content belongs to. The default identifier is rejected, so content can never be built without one.
    - `registeredCommandTypeIds` &mdash; Command types the engine will accept. They are copied and sorted, so the order you pass them in does not matter, and the set must contain battle.concede and battle.use-skill.

**Properties**

`public FrozenList<CompiledAiPolicyDefinition> AiPolicyDefinitionsV3`

:   Every AI policy the content declares, in ascending policy-id order, each holding the ordered rules an automatic combatant picks its next skill from. Every skill a rule names is known to exist, because a policy that referenced a missing one would not have compiled.

`public FrozenList<CompiledAutomaticDecisionPolicy> AutomaticDecisionPolicies`

:   The B2 automatic decision policies, sorted by policy id. Every skill a policy names is present in `SkillTimings`, since a dangling reference fails construction. B1 content carries none, and schema 3 content leaves this empty because automatic combatants there are driven by `AiPolicyDefinitionsV3` instead.

`public FrozenList<CompiledCombatantDefinition> CombatantDefinitionsV3`

:   Every combatant archetype the content declares, in ascending definition-id order. A battle start names one of these per participant instead of repeating its stats, so one definition can back any number of combatants in the same battle.

`public int EngineVersion`

:   Engine version of the profile, which rises with each contract level, so comparing it is the cheapest way to tell B1, B2, and B3 content apart.

`public SimulationContractProfile Profile`

:   The contract level this content was built at, which fixes the schema, engine, and registry versions everything downstream is checked against. The factory you called decides it, and a battle start refuses content whose profile does not match the one it was created for.

`public FrozenList<ReactionCycleDiagnostic> ReactionCycleDiagnostics`

:   Cycles the reaction-graph validator found. A cycle it judges unsafe aborts construction, so every entry that survives here is a non-fatal one reported for authoring review.

`public FrozenList<CompiledReactionDefinition> ReactionDefinitionsV3`

:   Every reaction rule the content declares, in ascending rule-id order. Construction walks the graph these form, so by the time you hold the content the cycle question is already settled: an unsafe cycle aborted the build, and any remaining one is listed in `ReactionCycleDiagnostics`.

`public FrozenList<StableId> RegisteredCommandTypeIds`

:   The command types this content accepts, sorted by id with duplicates rejected. battle.concede and battle.use-skill are always present, because content that omitted either could not be built. Use `RegistersCommand` rather than scanning the list yourself.

`public FrozenList<CompiledMechanicsBinding> RequiredMechanicsBindings`

:   Every mechanics implementation this content depends on, deduplicated and in a stable order, each carrying the contract version and the hash of the properties it was validated against. The engine re-resolves this set against whichever registry it is handed, and the canonical codec writes it out and rejects a decode that does not present the same set.

`public FrozenList<CompiledResourceDefinition> ResourceDefinitionsV3`

:   Every resource the content declares, in ascending resource-id order. Resource effects and combatant resource defaults are resolved against this list while the content is built, and a default outside the definition's bounds fails construction. Skill-cost resource ids are not resolved here: they are matched against the actor's own pools while the battle runs, so a cost naming a resource this list does not declare never becomes payable.

`public StableId RulesId`

:   Names the rule set behind this content; for schema 3 content it is the id of `RulesV3`. Diagnostics raised while validating the rules themselves are attributed to it, so it is what identifies the offending content in an authoring report.

`public CompiledBattleRulesV3 RulesV3`

:   The rules the whole battle is measured against: which stat ids carry the engine's semantic roles, which formulas damage, healing, defence, criticals, and status chance resolve through, and the variance, clamp, and reaction ceilings no action may exceed. Every id it names is checked against the definitions below while the content is built.

`public FrozenList<CompiledSchedulerDefinition> SchedulerDefinitions`

:   The schedulers this content offers, sorted by scheduler id. A B2 or schema 3 start selects one of them by id, so a start naming a scheduler that is absent here cannot be created at all; a B1 start never consults the content and takes its scheduler id on trust. B1 content carries none; anything above it carries between one and 16.

`public int SchemaVersion`

:   Compiled-schema version of the profile: 1 for B1 content, 2 for B2, 3 for the current schema. Canonical snapshots and replay envelopes record this number, so it is what a stored battle is matched against when it is loaded back.

`public FrozenList<CompiledSkillDefinition> SkillDefinitionsV3`

:   Every skill the content declares, in ascending skill-id order, each carrying its timing, its target resolver, and the effects it applies. The timings are also projected into `SkillTimings`, which is what the engine reads while a battle runs.

`public FrozenList<CompiledSkillTiming> SkillTimings`

:   The timing, cooldown, cost, and target-count contract for each skill, sorted by skill id. This is the form the engine reads while a battle runs; schema 3 content fills it from the timing on each entry of `SkillDefinitionsV3`, so the two never disagree. B1 content carries none.

`public FrozenList<CompiledStatDefinition> StatDefinitionsV3`

:   Every stat the content declares, in ascending stat-id order. A combatant base stat, a status modifier, or a semantic role in the rules may only name a stat that appears here, and a base value outside the definition's own bounds fails construction rather than being clamped later.

`public FrozenList<CompiledStatusDefinition> StatusDefinitionsV3`

:   Every status the content declares, in ascending status-id order, with its stacking rule, duration, stat modifiers, periodic effects, and the reactions it brings with it.

**Methods**

`public static CompiledBattleContent CreateB1Default()`

:   Builds ready-made B1 content under the rules id rules.b1-concession that registers the two built-in command types and nothing else. It needs no authored assets, so it is the quickest way to stand an engine up in a test or a sample scene. The battle it backs can only end by concession, since no skill is defined.

`public static CompiledBattleContent CreateB2()`

:   Builds B2 content, which adds schedulers, skill timings, and automatic decision policies to the rules identity and command set B1 already had. Every collection is copied and sorted here, so the content is fixed and safe to share between battles from the moment it is returned.
    - `rulesId` &mdash; Names the rule set this content belongs to; the default identifier is rejected.
    - `registeredCommandTypeIds` &mdash; Command types the engine will accept; battle.concede and battle.use-skill must both be among them.
    - `schedulerDefinitions` &mdash; One to 16 schedulers a battle start may select from. Nulls and repeated scheduler ids are rejected.
    - `skillTimings` &mdash; Timing contracts for the skills this content knows. Nulls and repeated skill ids are rejected.
    - `automaticDecisionPolicies` &mdash; Policies for automatically controlled combatants. A policy that names a skill with no timing in `skillTimings` is rejected, so a policy can never pick a skill the engine cannot run.

`public static CompiledBattleContent CreateB3()`

:   Builds validated content resolved against the built-in mechanics alone. Use the overload that takes a registry if the content names an implementation you registered yourself.
    - **Returns** &mdash; Content that has passed every construction check. This never returns null: a broken rule throws the exception that described it, so reach for TryCreateB3 when you would rather read a diagnostic than catch.

`public static CompiledBattleContent CreateB3()`

:   Builds validated content resolved against a registry you supply, which is how custom formulas, effects, targets, AI, and reactions reach the simulation.
    - `mechanicsRegistry` &mdash; Registry every implementation the content names must resolve from, at the contract version the content asks for. Whatever registry you later hand the engine has to satisfy the same bindings, so pass the same one.
    - **Returns** &mdash; Content that has passed every construction check; never null. A broken rule throws rather than returning.

`public CompiledAiPolicyDefinition FindAiPolicyDefinitionV3(StableId id)`

:   The AI policy definition with this id, or null when the content has none.

`public CompiledAutomaticDecisionPolicy FindAutomaticDecisionPolicy(StableId policyId)`

:   The automatic decision policy with this id, or null when the content has none. Schema 3 content always answers null, because its automatic combatants are driven by AI policy definitions instead.
    - `policyId` &mdash; Id a combatant names when it is placed under automatic control.

`public CompiledCombatantDefinition FindCombatantDefinitionV3(StableId id)`

:   The combatant definition with this id, or null when the content has none.

`public CompiledReactionDefinition FindReactionDefinitionV3(StableId id)`

:   The reaction definition with this rule id, or null when the content has none.

`public CompiledResourceDefinition FindResourceDefinitionV3(StableId id)`

:   The resource definition with this id, or null when the content has none.

`public CompiledSchedulerDefinition FindSchedulerDefinition(StableId schedulerId)`

:   The scheduler definition with this id, or null when the content does not offer it. The lookup is a binary search over the sorted definitions.
    - `schedulerId` &mdash; Id a battle start uses to select its scheduler.

`public CompiledSkillDefinition FindSkillDefinitionV3(StableId id)`

:   The skill definition with this id, or null when the content has none.

`public CompiledSkillTiming FindSkillTiming(StableId skillId)`

:   The timing contract for this skill, or null when the content has none. A null answer is what tells you a skill is unknown to the content, which is how a combatant granted a missing skill is caught.
    - `skillId` &mdash; Id of the skill whose timing is wanted.

`public CompiledStatDefinition FindStatDefinitionV3(StableId id)`

:   The stat definition with this id, or null when the content has none.

`public CompiledStatusDefinition FindStatusDefinitionV3(StableId id)`

:   The status definition with this id, or null when the content has none.

`public bool RegistersCommand(StableId commandType)`

:   Reports whether a command type is one this content accepts. It binary searches the sorted ids and allocates nothing, so it is cheap enough to call while building a command rather than after submitting one.
    - `commandType` &mdash; Command type id to look for; an unknown or default id simply reports false.

`public static B3CreationResult<CompiledBattleContent> TryCreateB3()`

:   The reporting form of CreateB3, against the built-in mechanics alone: a broken construction rule comes back as a failed result instead of an exception. Prefer this when compiling authored content a user can edit, so a bad asset produces a message rather than a stack trace.
    - **Returns** &mdash; A successful result carrying the content, or a failed one whose diagnostics name the stage and the rule that broke. Only the construction rules this content model knows about are converted; an unexpected exception still propagates.

`public static B3CreationResult<CompiledBattleContent> TryCreateB3()`

:   The reporting form of CreateB3 against a registry you supply. This is the entry point an authoring pipeline wants: custom mechanics are honoured and every failure arrives as a diagnostic.
    - `mechanicsRegistry` &mdash; Registry every implementation the content names must resolve from, at the contract version the content asks for. The engine must later be handed a registry that satisfies the same bindings.
    - **Returns** &mdash; A successful result carrying the content, or a failed one whose diagnostics name the stage and the rule that broke. Only known construction failures are converted; an unexpected exception still propagates.

---

## CompiledCombatantDefinition

```csharp
public sealed class CompiledCombatantDefinition
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3BattleRules.cs</small>

The compiled, immutable archetype a combatant is spawned from: its base
stats, starting resources, granted skills, tags, status resistances,
status immunities and intrinsic reactions. A start request names one of
these per combatant and supplies only the per-battle overrides on top of
it.
Every collection is sorted into a canonical order and checked for
duplicates while the object is built, so two catalogues that authored the
same archetype in a different order compile to the same bytes and hash
alike. That is why the properties below come back sorted rather than in
the order they were authored: by identifier, except
`Resistances`, which sorts by match kind and then identifier.

**Constructors**

`public CompiledCombatantDefinition()`

:   Compiles one combatant archetype, sorting every collection into canonical order and rejecting duplicate keys. The sequences are copied, so the caller may keep using its own collections afterwards.
    - `definitionId` &mdash; Identity a start request names to spawn this archetype. Required.
    - `baseStats` &mdash; The value each stat starts at before any status modifier, at most one entry per stat.
    - `resourceDefaults` &mdash; The amount each resource starts at, at most one entry per resource.
    - `tags` &mdash; Classification identifiers carried by the archetype itself; valid and unique. These are combatant tags, not the status tags named by `immuneStatusTags`.
    - `grantedSkillIds` &mdash; The skills a combatant of this archetype may use.
    - `defaultAiPolicyId` &mdash; The AI policy used when a combatant of this archetype is automatically controlled and its start entry names no override. Null when the archetype supplies none, in which case the start entry has to.
    - `resistances` &mdash; Resistance chances keyed either by status definition or by status tag. The kind and identifier together form the key and must be unique, so the same status may be resisted once by ID and again by tag.
    - `immuneStatusIds` &mdash; Status definitions this archetype cannot receive at all. Immunity is absolute rather than a very high resistance: the resulting chance is zero whatever `resistances` says.
    - `immuneStatusTags` &mdash; Status tags this archetype cannot receive; a status carrying any of them is refused.
    - `intrinsicReactionDefinitionIds` &mdash; Reaction rules every combatant of this archetype carries from the start, without a status having to grant them.

**Properties**

`public FrozenList<CompiledStatValue> BaseStats`

:   The value each stat starts at, sorted by stat ID and unique per stat. These are the base figures before any status modifier, so they are not what a combatant's effective stats read mid-battle. Content validation rejects a value outside the bounds of its stat definition.

`public StableId? DefaultAiPolicyId`

:   The AI policy used when a combatant of this archetype is automatically controlled and its start entry names no override, or null when the archetype supplies none. An automatic combatant with neither has no policy to resolve and the battle will not start.

`public StableId DefinitionId`

:   Identity a start request names to spawn a combatant from this archetype, and the key content validation reports failures against.

`public FrozenList<StableId> GrantedSkillIds`

:   The skills a combatant of this archetype may use, sorted by skill ID. Content validation rejects the catalogue if any of them is unknown.

`public FrozenList<StableId> ImmuneStatusIds`

:   Status definitions this archetype cannot receive at all. Immunity is absolute rather than a very high resistance: the resulting chance is zero whatever `Resistances` says.

`public FrozenList<StableId> ImmuneStatusTags`

:   Status tags this archetype cannot receive; a status carrying any of them is refused the same way a named immunity refuses one.

`public FrozenList<StableId> IntrinsicReactionDefinitionIds`

:   Reaction rules every combatant of this archetype carries from battle start, sorted by reaction ID. They come from the archetype itself rather than from a status that grants them.

`public FrozenList<CompiledStatusResistance> Resistances`

:   Resistance chances keyed by status definition or by status tag, sorted by match kind and then by identifier. Every entry that matches an incoming status is summed and clamped into one chance, so a definition entry and a tag entry for the same status both count.

`public FrozenList<CompiledResourceDefault> ResourceDefaults`

:   The amount each resource starts at, sorted by resource ID and unique per resource. Content validation rejects a value outside the bounds of its resource definition.

`public FrozenList<StableId> Tags`

:   Classification identifiers carried by the archetype itself, sorted and free of duplicates. These describe the combatant; the status tags it cannot receive are in `ImmuneStatusTags`.

---

## CompiledEffectEntry

```csharp
public sealed class CompiledEffectEntry
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3Definitions.cs</small>

One authored effect slot on a skill, status, or reaction: which registered
effect resolver runs and with which authored arguments. Immutable, and planned
once per locked target rather than once per action, so a single entry on a
multi-target skill produces one plan per target.

**Constructors**

`public CompiledEffectEntry()`

:   Validates and freezes one effect entry. The resolver is only named here, not resolved: a reference to an implementation missing from the mechanics registry fails later, when the catalog is validated or the entry is planned.
    - `entryId` &mdash; Identity of this entry inside its owner. It appears in attribution traces, and owners require it to be unique among their entries.
    - `resolver` &mdash; The `IEffectResolver` implementation to run, plus the contract version it was authored against.
    - `properties` &mdash; Authored arguments handed to the resolver on every plan call.
    - `effectTags` &mdash; Tags this entry publishes. Reaction rules trigger by matching them. Stored sorted and de-duplicated, so authored order carries no meaning.

**Properties**

`public FrozenList<StableId> EffectTags`

:   Sorted, de-duplicated tags published by this entry. Reaction rules match their trigger tags against these, so tagging an entry is what makes it reactable.

`public StableId EntryId`

:   Identity of this entry inside its owning skill, status, or reaction, unique among that owner's entries. It is carried through to formula attribution, so it is what ties a recorded number back to the entry that produced it.

`public PropertySet Properties`

:   Authored arguments passed to the resolver every time this entry is planned.

`public MechanicsImplementationReference Resolver`

:   The effect-resolver implementation this entry runs, and the contract version it expects. Both must match a registration in the mechanics registry.

---

## CompiledSkillDefinition

```csharp
public sealed class CompiledSkillDefinition
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3Definitions.cs</small>

One usable skill after compilation: its timing, how it picks and keeps targets,
and the ordered effect entries it runs. Immutable, and looked up by id from the
compiled catalog each time the skill resolves, so a skill in flight cannot drift.

**Constructors**

`public CompiledSkillDefinition()`

:   Validates and freezes one skill definition. Timing must belong to the same skill id, and the two target policies must be values this contract version supports, so an incoherent skill cannot reach a battle.
    - `tags` &mdash; Skill tags. Stored sorted and de-duplicated.
    - `timing` &mdash; Cast, recovery, cooldown, cost, and requested-target bounds. Its `CompiledSkillTiming.SkillId` must equal `skillId`.
    - `targetResolver` &mdash; The `ITargetResolver` implementation that turns requested targets into locked targets.
    - `targetProperties` &mdash; Authored arguments handed to that target resolver.
    - `targetLockPolicy` &mdash; Must be `TargetLockPolicy.LockAtAcceptance`; no other value is accepted by this contract version.
    - `effects` &mdash; Effect entries in the order they run. Entry ids must be unique within the skill, and the count is capped by `SimulationLimits.EffectEntriesPerSkill`.

**Properties**

`public FrozenList<CompiledEffectEntry> Effects`

:   Effect entries in authored order. The engine walks them front to back and plans each one against every locked target before moving to the next, so reordering entries changes what a battle produces.

`public InvalidTargetPolicy InvalidTargetPolicy`

:   What happens when a locked target stops being valid mid-action: skip that target, cancel the whole action, or retarget to the first still-valid candidate that is not already locked.

`public StableId SkillId`

:   Identity of this skill in the compiled catalog. Commands, cooldowns, and the skill's own timing record all key on it, and it is what the catalog is searched by when an action resolves.

`public FrozenList<StableId> Tags`

:   Sorted, de-duplicated skill tags. Statuses forbid skills by these tags, and presentation recipes can select on them; the simulation attaches no other meaning to a tag.

`public TargetLockPolicy TargetLockPolicy`

:   When the skill captures the targets it will act on. This contract version defines only `TargetLockPolicy.LockAtAcceptance`, so targets are always frozen when the command is accepted and anything that goes wrong afterwards is handled by `InvalidTargetPolicy` instead.

`public PropertySet TargetProperties`

:   Authored arguments passed to the target resolver.

`public MechanicsImplementationReference TargetResolver`

:   The target-resolver implementation and contract version used to resolve this skill's targets.

`public CompiledSkillTiming Timing`

:   Cast and recovery ticks, cooldown, resource costs, and the bounds on how many targets a command for this skill may request. Its `CompiledSkillTiming.SkillId` always equals `SkillId`, so it can be passed around on its own without losing which skill it belongs to.

---

## CompiledStatusDefinition

```csharp
public sealed class CompiledStatusDefinition
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3Definitions.cs</small>

One status after compilation: how it stacks, how long it lasts, what it modifies
while resident, and what it costs its owner. Immutable, and re-read by id on every
application, clock boundary, and dispel, so a resident instance stores only its own
bookkeeping (stacks, remaining duration, next periodic tick) and never these rules.

**Constructors**

`public CompiledStatusDefinition()`

:   Validates and freezes one status definition. Stacking, duration, and periodic values are cross-checked against each other here, so an incoherent status cannot reach a battle.
    - `tags` &mdash; Status tags. Stored sorted and de-duplicated.
    - `exclusiveGroupId` &mdash; Optional exclusivity group. Pass null for none; a supplied id must be valid.
    - `maximumStacks` &mdash; Concurrent ceiling. It must be positive and no greater than `SimulationLimits.IndependentStatusStacks`, and exactly 1 when `stackPolicy` is `StatusStackPolicy.Refresh`.
    - `periodicEffects` &mdash; Effects run on the periodic phase. Supplying any while `periodic` declares `StatusPeriodicPhase.None` throws.
    - `reactionDefinitionIds` &mdash; Reaction rules this status contributes. Stored sorted and de-duplicated; each id must resolve inside the same compiled catalog.
    - `preventNextOpportunity` &mdash; Optional, defaults to false. When set, the status is spent skipping its owner's next opportunity.

**Properties**

`public bool Dispellable`

:   Whether a dispel effect may remove this status. When false it can still be removed by expiry, by death cleanup, or by an effect that removes it by id.

`public CompiledStatusDuration Duration`

:   How long an instance lasts, and which clock counts it down: elapsed battle ticks, or one of the owner's action or opportunity boundaries. Only the elapsed clock measures the authored amount in ticks - under the others the amount is a count of boundaries.

`public StableId? ExclusiveGroupId`

:   Optional exclusivity group. Under `StatusStackPolicy.KeepHigher` an incoming application also loses to a resident status that merely shares this group, not just to another instance of the same status.

`public int MaximumStacks`

:   Concurrent ceiling: stacks carried by one instance for the stacking policies, or the number of separate instances under `StatusStackPolicy.Independent`.

`public FrozenList<CompiledStatModifier> Modifiers`

:   Modifiers that apply while the status is resident, in authored order. Each one names the stat it touches and the pipeline stage it joins; within a stage the engine orders by priority, then status ID, then application sequence, then authored index, so authored order only settles the final tie.

`public CompiledStatusPeriodicPolicy Periodic`

:   When this status's periodic effects fire and, for an elapsed boundary, how many ticks apart. A phase of `StatusPeriodicPhase.None` means it has none, and authoring `PeriodicEffects` alongside that phase is rejected at construction.

`public FrozenList<CompiledEffectEntry> PeriodicEffects`

:   Effects planned on the owner at each periodic phase, sourced from whoever applied the status. Empty unless `Periodic` declares a phase.

`public bool PersistOnDeath`

:   Survives its owner's death. Instances without this are stripped during death cleanup.

`public StatusPolarity Polarity`

:   Buff, debuff, or neutral. A dispel effect only removes instances whose polarity matches the one it asks for.

`public bool PreventNextOpportunity`

:   The owner's next opportunity is skipped, and the instance is consumed doing so. With several such instances resident, the earliest-applied one is spent first.

`public FrozenList<StableId> ReactionDefinitionIds`

:   Reaction rules this status contributes while it is resident, on top of the owner's intrinsic rules. Sorted and de-duplicated.

`public bool RefreshKeepHigherMetadata`

:   When an application is absorbed by an equal or stronger resident instance, refresh that instance's remaining duration and periodic timer instead of leaving them untouched.

`public FrozenList<StableId> RestrictedSkillTags`

:   While this status is resident, its owner cannot use any skill carrying one of these tags. Sorted and de-duplicated.

`public StatusStackPolicy StackPolicy`

:   What a fresh application does when the target already carries this status: refresh the resident instance, add a stack to it, add a separate instance, replace what is there, or defer to whichever side is stronger. It also constrains `MaximumStacks`, which must be exactly 1 under `StatusStackPolicy.Refresh`.

`public StableId StatusId`

:   Identity of this status in the compiled catalog. Applications, combatant immunities, and dispels that name a status all key on it, and a resident instance stores this value rather than a reference to the definition itself.

`public Fixed64 Strength`

:   Ranking value read only under `StatusStackPolicy.KeepHigher`: a resident instance of the same status or exclusive group whose strength is at least this value absorbs the incoming application. It is not a magnitude and never enters a formula.

`public FrozenList<StableId> Tags`

:   Sorted, de-duplicated status tags. Combatant immunities, resistances, tag-filtered dispels, and presentation recipes all match on these.

`public bool TauntHostileSingleTarget`

:   Forces the owner's single-target enemy skills onto whoever applied this status, provided that source is still a living, targetable enemy among the resolver's candidates. Skills that resolve more than one target, or that do not target enemies, are unaffected.

---

## EffectDefinition

:material-star: **Start here**

```csharp
public sealed class EffectDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/EffectDefinition.cs</small>

One reusable thing that happens to a target: the registered effect resolver that
plans the work, the authored arguments handed to it, and the tags the effect
publishes while it resolves. Skills, statuses, and reactions all point at these
through an `EffectUseDefinition` rather than describing their own
behaviour, so one effect asset can serve many of them and editing it changes all
of them.

The resolver is planned once per locked target, not once per action, so a
multi-target skill runs this effect once for each target it resolved.
`EffectTags` is what makes an effect reactable: a reaction rule
triggers by matching its declared trigger tags against these, so an untagged
effect can never set a reaction off.

---

## EffectUseDefinition

```csharp
public sealed class EffectUseDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

One slot in an owner's effect list: the effect to run, plus an id that names the
slot inside that owner. `SkillDefinition`,
`StatusDefinition`, and `ReactionDefinition` all hold
lists of these, and the compiler keeps the authored order, so the order entries
appear in the inspector is the order the effects run in.

---

## EncounterDefinition

:material-star: **Start here**

```csharp
public sealed class EncounterDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/EncounterDefinition.cs</small>

One playable fight: the two sides that meet, the formation each stands in, and
the scheduler that decides who acts when. It is what compilation turns into a
battle start request, so it is the asset a game hands to the engine to begin a
battle.

Exactly two `EncounterTeamDefinition` entries are expected, naming
different teams. `PerspectiveTeam` is required and must be one of
those two: it is what turns "one team is left standing" into a victory or a
defeat, since the engine has no other notion of which side the player is on.

---

## EncounterTeamDefinition

```csharp
public sealed class EncounterTeamDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

One of the two sides of an `EncounterDefinition`: the roster that
fights, the formation it fights in, and where each of its members stands. An
encounter carries exactly two of these, and the two must reference different
teams.

---

## FormationAssignmentDefinition

```csharp
public sealed class FormationAssignmentDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

Places one team member in one formation slot. Placement is never inferred:
every member of the team needs exactly one assignment, and no two assignments
in the encounter may name the same slot, even across the two teams.

---

## InitialStatusApplicationDefinition

```csharp
public sealed class InitialStatusApplicationDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

One status already applied to a team member when the battle starts, before the
first tick is simulated. At most one entry per status definition per member:
the compiler rejects a repeated status rather than merging the two entries.

---

## InvalidTargetPolicy

```csharp
public enum InvalidTargetPolicy : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

What the engine does when a locked target is no longer valid at
resolution. SkipInvalid drops that target and continues with the rest,
CancelAction abandons the action's unresolved effects without refunding
paid costs, and RetargetStable substitutes the lowest-StableId candidate
that is not already locked. Revalidation never consumes a random draw.

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

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

An immutable pointer from compiled content to one registered mechanics
implementation: its stable ID plus the contract version the content was
authored against. Resolution demands an exact version match, so a
registry that offers only another version of the same ID makes the
content invalid instead of silently binding to it.

**Constructors**

`public MechanicsImplementationReference(StableId implementationId, int contractVersion)`

:   Creates a reference to a registered formula, effect, target, AI, or reaction implementation.
    - `implementationId` &mdash; The implementation's registered ID; must be valid.
    - `contractVersion` &mdash; The contract version the content targets; must be positive and is matched exactly at resolution.

**Properties**

`public int ContractVersion`

:   The contract version the content was authored against. Resolution matches it exactly, so raising an implementation's version invalidates the content still naming the old one rather than binding it to behaviour it was never authored for.

`public StableId ImplementationId`

:   The registered ID of the formula, effect, target, AI, or reaction implementation the content binds to. It names a registration in `BattleMechanicsRegistry`, not a C# type, so a game can swap the class behind an ID without recompiling content.

**Methods**

`public bool Equals(MechanicsImplementationReference other)`

:   Two references are equal only when both the implementation ID and the contract version match; the same ID at another version is a different reference.

`public override bool Equals(object obj)`

:   Value equality against any object; false for other types.

`public override int GetHashCode()`

:   A hash over the implementation ID and contract version.

---

## MechanicsImplementationReferenceDefinition

```csharp
public sealed class MechanicsImplementationReferenceDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

The inspector form of a pointer to one registered mechanics implementation. It appears wherever
authored content hands work to code -- the formulas on `BattleRulesDefinition`,
`EffectDefinition`, `TargetDefinition`,
`AiPolicyDefinition`, and `ReactionDefinition` -- and compiles to a
`MechanicsImplementationReference`. Both fields are required: an implementation is
found by ID and contract version together, never by ID alone.

---

## ModifierStage

```csharp
public enum ModifierStage : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

Which step of the deterministic stat and formula pipeline a status
modifier joins. FlatStat and MultiplicativeStat are the only stages that
change a combatant's effective stat value, and they apply only to the
stat the modifier names. Outgoing follows the source's potency, Incoming
applies on the target and can be bypassed by an effect, and the critical
stages adjust critical chance additively and the critical multiplier
multiplicatively. Within one stage, order is priority, status ID,
application sequence, then authored index.

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/PropertyDefinitions.cs</small>

One authored property: a key, a tag saying which value slot is live, and that value.
Every slot is serialized separately, so changing the tag in the inspector leaves the
other slots untouched - only the tagged one is ever read.

Build entries with the `From*` factories rather than by hand. The array factories
copy their input, and a null array becomes an empty one.

**Properties**

`public string KeyRaw`

:   The authored key text, verbatim and never null. It becomes a `StableId` at compile time, so text that is empty or not valid ID text is reported as a diagnostic then rather than rejected here.

`public AuthoringValueTag Tag`

:   Which of this entry's value slots is live.

**Methods**

`public PropertyEntrySnapshot CreateSnapshot()`

:   Copies this entry's key, tag, and live value into an immutable snapshot that later edits to this definition cannot reach. Arrays are copied element by element, so the snapshot shares no storage with the authored data.
    - **Returns** &mdash; Never null. An array longer than its tag allows is not an exception here: the snapshot then carries the key, the tag, and the declared value count, but no value.

`public static PropertyEntryDefinition FromBoolean(string key, bool value)`

:   Creates an entry holding a boolean.

`public static PropertyEntryDefinition FromBooleans(string key, params bool[] values)`

:   Creates an entry holding a copy of a boolean array.

`public static PropertyEntryDefinition FromChance64Raw(string key, long value)`

:   Creates an entry holding a chance as its raw scaled integer: certainty is `Chance64.Scale`, so 87.5% is authored as 875000. The range is not checked here - a raw value outside 0..`Chance64.Scale` is reported as an invalid property value when compiled.

`public static PropertyEntryDefinition FromChance64Raws(string key, params long[] values)`

:   Creates an entry holding a copy of an array of chances, each as its raw scaled integer in `Chance64.Scale` units and range-checked only at compile time.

`public static PropertyEntryDefinition FromFixed64Raw(string key, long value)`

:   Creates an entry holding a fixed-point amount as its raw scaled integer: one whole unit is `Fixed64.Scale`, so 5 is authored as 50000.

`public static PropertyEntryDefinition FromFixed64Raws(string key, params long[] values)`

:   Creates an entry holding a copy of an array of fixed-point amounts, each as its raw scaled integer in `Fixed64.Scale` units.

`public static PropertyEntryDefinition FromInt32(string key, int value)`

:   Creates an entry holding a 32-bit signed integer.

`public static PropertyEntryDefinition FromInt32s(string key, params int[] values)`

:   Creates an entry holding a copy of a 32-bit signed integer array.

`public static PropertyEntryDefinition FromInt64(string key, long value)`

:   Creates an entry holding a 64-bit signed integer.

`public static PropertyEntryDefinition FromInt64s(string key, params long[] values)`

:   Creates an entry holding a copy of a 64-bit signed integer array.

`public static PropertyEntryDefinition FromStableId(string key, string value)`

:   Creates an entry holding a `StableId` as its raw text; null becomes empty.

`public static PropertyEntryDefinition FromStableIds(string key, params string[] values)`

:   Creates an entry holding a copy of an array of `StableId` raw texts. Tagged ID arrays are capped at `SimulationLimits.StableIdsPerTaggedArray` values, well below the `SimulationLimits.PropertyArrayValues` cap the other array tags get.

`public static PropertyEntryDefinition FromString(string key, string value)`

:   Creates an entry holding free text. Null is stored as null rather than coerced to empty the way `FromStableId` does, and both a null value and text that is not already Unicode NFC are reported as an invalid property value when compiled.

`public static PropertyEntryDefinition FromStrings(string key, params string[] values)`

:   Creates an entry holding a copy of a string array.

`public static PropertyEntryDefinition FromUInt64(string key, ulong value)`

:   Creates an entry holding a 64-bit unsigned integer.

`public static PropertyEntryDefinition FromUInt64s(string key, params ulong[] values)`

:   Creates an entry holding a copy of a 64-bit unsigned integer array.

---

## PropertySetDefinition

```csharp
public sealed class PropertySetDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/PropertyDefinitions.cs</small>

The serialized bag of authored key/value properties on a definition: the arguments
handed to whichever mechanics implementation that definition points at.

Keys must be valid `StableId` text and unique within the set, and the
set is capped at `SimulationLimits.PropertiesPerRecord` entries. None of
that is enforced while entries are added here; all of it is reported as a compile
diagnostic when the owning catalog is compiled.

**Constructors**

`public PropertySetDefinition()`

:   Creates an empty property set.

`public PropertySetDefinition(params PropertyEntryDefinition[] entries)`

:   Creates a property set holding the given entries. The array is copied, so later changes to the caller's array are not seen here; a null array yields an empty set.

**Properties**

`public PropertyEntryDefinition[] Entries`

:   The entries in authored order. Every call hands back a new array, so adding to or reordering the result does not change the set - but the entries themselves are the same objects, so editing one still edits this set.

**Methods**

`public int Compare()`

:   Orders two array-limit issues by raw key, then value tag, then declared value count. Every step is an ordinal comparison, so the order a compile reports these issues in does not shift with the current culture or with the order the properties were authored in.
    - `left` &mdash; The issue on the left of the comparison.
    - `right` &mdash; The issue on the right of the comparison.
    - **Returns** &mdash; A value less than, equal to, or greater than zero as `left` sorts before, with, or after `right`.

---

## ReactionDefinition

```csharp
public sealed class ReactionDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/ReactionDefinition.cs</small>

One rule that lets a combatant act out of turn: the registered reaction rule that
judges each candidate, when in a triggering effect's resolution it is offered,
and the effects it runs if it fires. A `CombatantDefinition` can carry
one intrinsically and a `StatusDefinition` can grant one for as long
as it is resident.

A reaction is offered when an effect publishes a tag the rule declares as a
trigger, so what sets it off is decided by `EffectDefinition.EffectTags`
and the rule's own signature, not by anything on this asset. Termination is taken
seriously here: the reaction graph is checked while content compiles, and a cycle
only compiles when every rule in it sets `OncePerRoot`, sets
`ConsumeRequiredStatusOnEnqueue`, or declares itself finite by
construction in its reaction signature. The depth and count ceilings on
`BattleRulesDefinition` are no part of that proof - they are runtime
budgets that suppress a reaction once it would cross one.

---

## ReactionTriggerPhase

```csharp
public enum ReactionTriggerPhase : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

Whether a reaction rule is offered before or after the primitive that
triggers it. Before-effect reactions are fully drained before that
primitive's target is revalidated and resolved; after-effect reactions
are drained after its events, death included, and before the next
primitive.

| Value | Meaning |
| --- | --- |
| `BeforeEffect` | &mdash; |
| `AfterEffect` | &mdash; |

---

## ResistanceMatchKind

```csharp
public enum ResistanceMatchKind : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

Whether a combatant's resistance entry is keyed by a status definition ID
or by a status tag. Every entry that matches an incoming status
accumulates into one clamped resistance chance, so a definition entry and
a tag entry for the same status both count.

| Value | Meaning |
| --- | --- |
| `StatusDefinition` | &mdash; |
| `StatusTag` | &mdash; |

---

## ResourceDefinition

:material-star: **Start here**

```csharp
public sealed class ResourceDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/ResourceDefinition.cs</small>

One spendable pool a combatant carries - mana, rage, ammunition, whatever the
game calls it - defined only by the range it may hold. It has no regeneration and
no behaviour of its own: skills spend it through their cost lists, effects move it
through resource primitives, and AI rules gate on it, so a resource does nothing
until something references it.

Health is not one of these. It is a stat, named by
`BattleRulesDefinition.MaximumHealthStat`, and the engine tracks it
separately. A combatant only holds the resources its own
`CombatantDefinition.ResourceDefaults` list seeds; amounts are whole
units, not the fixed-point raw values a stat uses.

---

## SchedulerDefinition

:material-star: **Start here**

```csharp
public sealed class SchedulerDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/SchedulerDefinition.cs</small>

The turn order one encounter runs under: which scheduling model hands out
opportunities to act, and the timing values that model reads. An
`EncounterDefinition` names exactly one, so the same rosters can fight
in strict action order in one encounter and against a filling ATB gauge in
another.

The asset's own stable ID is what is looked up in the scheduler registry, at the
contract version below, and the registration found there must agree with
`StateTag` or the catalog does not compile. The tag also decides which
fields carry meaning: the input pause policy and
`GaugeThresholdUnits` are read only by an ATB definition, which needs
a positive threshold. An action-order definition does not merely ignore them - it
requires both to be left at zero, so the inspector default of `PauseOnInput`
has to be cleared or the catalog does not compile.

---

## SkillCostDefinition

```csharp
public sealed class SkillCostDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

One resource a skill spends to be used. The compiler sorts a skill's cost list by
resource, so the order entries appear in the inspector never changes the compiled
skill, and the amount is debited when the command is accepted rather than when the
action resolves.

---

## SkillDefinition

:material-star: **Start here**

```csharp
public sealed class SkillDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/SkillDefinition.cs</small>

One action a combatant can take: how long it takes to cast and recover, what it
costs, who it is allowed to hit, and the ordered effects it runs on each target it
hits. A `CombatantDefinition` grants it, and either a submitted command
or an `AiRuleDefinition` names it when an opportunity comes round.

Targeting is delegated rather than described here: `Target` points at a
reusable `TargetDefinition`, while the two policies beside it decide
when the chosen targets are fixed and what happens if one stops being legal partway
through. The `Effects` list keeps its authored order, and the engine
plans each entry against every locked target before moving to the next, so
reordering the list changes what a battle produces. Costs are debited when the
command is accepted, not when the action finally resolves.

---

## StableIdDefinition

```csharp
public abstract class StableIdDefinition : ScriptableObject
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/StableIdDefinition.cs</small>

Base class for authoring assets whose identity survives file, folder, label,
and localization changes. Identity is never generated or repaired at runtime.

**Properties**

`public int AuthoringSchemaVersion`

:   Which authoring layout this asset was serialised under, or zero for an asset written before the field existed. It is stamped when the asset is created and is not corrected on load, so the editor's migration tooling can tell an unmigrated asset from one already at `CurrentSchemaVersion` rather than guessing.

`public string DisplayLabel`

:   A human-readable name for editor lists and for building display string tables, empty when unset. It carries no identity, so renaming it cannot break references or invalidate compiled content.

`public string LocalizationKey`

:   A key for looking this asset's name up in a translation table, empty when unset. Nothing in the package resolves it; it is stored and carried through so a game's own localisation layer can use it.

`public string StableIdRaw`

:   The identity text exactly as it was authored, or an empty string when none has been set. It is deliberately returned unvalidated: judging whether the text forms a usable ID belongs to the compiler, so a half-filled asset can still be listed and reported on instead of throwing when it is read.

---

## StartCombatantV3

```csharp
public sealed class StartCombatantV3
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/BattleStartV3.cs</small>

The opening state of one combatant: the compiled definition it is built from,
who decides for it, and the health, resources, statuses, and formation slot it
starts with. Its resource and status lists are sorted by id and rejected when an
id repeats, so the order they are passed in cannot change the battle. Stats and
skills are not set here; they come from the compiled combatant definition.

**Constructors**

`public StartCombatantV3()`

:   Describes one combatant's first tick. Every id is checked for shape here but resolved against compiled content only when the start request is created.
    - `combatantId` &mdash; Identity of this instance. Must be unique across the whole battle, not just within its team.
    - `combatantDefinitionId` &mdash; The compiled combatant definition supplying this instance's base stats, skills, and default AI policy.
    - `controlKind` &mdash; `Human` leaves decisions to submitted commands; `Automatic` requires an AI policy the content can resolve, from the override or the definition.
    - `aiPolicyOverrideId` &mdash; Replaces the definition's default AI policy for this instance, or `null` to keep that default.
    - `currentHealth` &mdash; Health at the first tick, from 0 to `maximumHealth`. Zero is accepted and starts the combatant dead, but a team still needs one living member.
    - `maximumHealth` &mdash; The health ceiling; must be greater than zero.
    - `targetable` &mdash; `false` both hides the combatant from target resolution and makes its own commands invalid, so it can neither be hit nor act.
    - `resources` &mdash; The resource pools this combatant owns; pools left out do not exist for it. Required, so pass an empty sequence rather than `null`.
    - `formationSlotId` &mdash; The formation slot this combatant occupies. Required, but not resolved against a compiled layout: it is carried into the snapshot as given.
    - `formationRowId` &mdash; The row the slot belongs to. Built-in row targets select by matching this id.
    - `formationSideId` &mdash; The side the slot belongs to. Built-in side targets select by matching this id.
    - `initialAtbGaugeUnits` &mdash; The gauge this combatant starts charged to. Only an ATB scheduler reads it, and then it must be strictly below that scheduler's gauge threshold; ordered schedulers ignore it.
    - `initialStatuses` &mdash; Statuses already applied at the first tick, at most one entry per status definition. Required, so pass an empty sequence rather than `null`.

**Properties**

`public StableId? AiPolicyOverrideId`

:   An AI policy that replaces the definition's default for this instance only, or `null` to keep that default. It is validated whichever control kind is set, so an unknown override fails the start even on a combatant a player drives.

`public StableId CombatantDefinitionId`

:   The compiled combatant definition this instance is built from, supplying its base stats, granted skills and default AI policy. Several instances may share one definition; nothing on the definition is copied here.

`public StableId CombatantId`

:   This instance's identity for the whole battle. Commands, targets, events and replays all name the combatant by it, and it must be unique across both teams, not merely within its own.

`public DecisionControlKind ControlKind`

:   Who decides this combatant's actions. `Human` waits for a submitted command at each opportunity; `Automatic` requires an AI policy the content can resolve, taken from `AiPolicyOverrideId` or the definition's default.

`public int CurrentHealth`

:   Health at the first tick, from 0 to `MaximumHealth`. Zero opens the battle with the combatant already dead, which is allowed as long as its team has one member above zero.

`public StableId FormationRowId`

:   The row that seat belongs to. Row-based target shapes select by matching this id, so combatants sharing a row are selected together whatever preset they came from.

`public StableId FormationSideId`

:   The side of the field that seat sits on. Side-based target shapes select by matching this id.

`public StableId FormationSlotId`

:   The formation seat this combatant stands in. It is carried into the snapshot exactly as given and never resolved against a compiled layout, so the engine can run a battle without any formation data present.

`public int InitialAtbGaugeUnits`

:   How far this combatant's gauge is already charged, from 0 to `SimulationLimits.AtbGauge`. Only an ATB scheduler reads it, and then it must sit strictly below that scheduler's threshold, so a combatant cannot open the battle already due to act; ordered schedulers ignore it.

`public FrozenList<StartStatusApplicationV3> InitialStatuses`

:   Statuses the combatant already carries at the first tick, ascending by status definition id and at most one entry per definition.

`public int MaximumHealth`

:   This instance's health ceiling, always above zero. It is set per start rather than by the compiled combatant definition, so one definition can field a frail and a sturdy copy in the same encounter.

`public FrozenList<StartResourceV3> Resources`

:   The resource pools this combatant owns, ascending by resource id. A pool left out does not exist for it at all, so a skill costing that resource can never be paid; each pool's ceiling comes from the compiled resource definition rather than from the start entry.

`public bool Targetable`

:   Whether the combatant takes part in target resolution. `false` both hides it from targeting and invalidates its own commands, so it neither hits nor is hit. It is independent of health: a combatant can start dead but targetable, or living but not.

---

## StartResourceV3

```csharp
public readonly struct StartResourceV3
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/BattleStartV3.cs</small>

One resource pool a combatant holds at the first tick, as a definition id and
an amount. Only the pools a start combatant lists exist for it during the
battle; the pool's ceiling always comes from the compiled resource definition,
never from here.

**Constructors**

`public StartResourceV3(StableId resourceId, int current)`

:   Seeds one resource pool. `current` is not range-checked here; it is validated against the compiled resource definition's minimum and maximum when the start request is created.
    - `resourceId` &mdash; The compiled resource definition this value fills.
    - `current` &mdash; The amount held at the first tick.

**Properties**

`public int Current`

:   The amount held at the first tick, not a live value.

`public StableId ResourceId`

:   The compiled resource definition this pool fills, and the id the battle addresses the pool by afterwards. A combatant's start resources are sorted on it and a repeat is rejected, so one definition can seed at most one pool per combatant.

---

## StartStatusApplicationV3

```csharp
public sealed class StartStatusApplicationV3
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/BattleStartV3.cs</small>

One status a combatant already carries when the battle opens. How
`StackCount` is realised depends on the status definition's stack
policy: an `Independent` status becomes that many single-stack instances,
any other policy becomes one instance holding that many stacks.

**Constructors**

`public StartStatusApplicationV3(StableId statusDefinitionId, StableId? sourceCombatantId, int stackCount)`

:   Describes one pre-applied status. The stack count is bounded here by the structural stack limit only; it is checked against the status definition's own stack cap when the start request is created.
    - `statusDefinitionId` &mdash; The compiled status definition to apply.
    - `sourceCombatantId` &mdash; The combatant credited as the source of the status, or `null` to credit the carrier itself. A supplied id must name a combatant taking part in the same battle, on either team.
    - `stackCount` &mdash; Stacks to apply; 1 to `SimulationLimits.IndependentStatusStacks`.

**Properties**

`public StableId? SourceCombatantId`

:   The combatant credited as having applied the status, or `null` to credit the carrier itself. It is resolved once every combatant on both teams is known, so it may name an opponent or a team-mate declared later in the start.

`public int StackCount`

:   How many stacks the status opens with. It is checked against the status definition's own cap as well as `SimulationLimits.IndependentStatusStacks`, and under the `Independent` stack policy each stack becomes a separate instance, so a large count here spends that much of the per-combatant status budget.

`public StableId StatusDefinitionId`

:   The compiled status definition being applied. A combatant's initial statuses are sorted on it and a repeat is rejected, so several opening stacks of the same status have to be expressed as one entry with a higher `StackCount`.

---

## StartTeamV3

```csharp
public sealed class StartTeamV3
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/BattleStartV3.cs</small>

One side of a battle: a team id and the combatants fighting under it. The member
list is sorted by combatant id, so the order it is passed in cannot change the
battle, and at least one member must start with health above zero.

**Constructors**

`public StartTeamV3(StableId teamId, IEnumerable<StartCombatantV3> combatants)`

:   Assembles one side of a battle.
    - `teamId` &mdash; Identity of the team. It must differ from the opposing team's, which the start request checks rather than this constructor.
    - `combatants` &mdash; One to `SimulationLimits.CombatantsPerTeam` non-null members with distinct ids, at least one of them living.

**Properties**

`public FrozenList<StartCombatantV3> Combatants`

:   The team's members, ascending by combatant id rather than in the order they were supplied, so two starts built from the same members are identical whichever way they were assembled.

`public StableId TeamId`

:   The team's identity. Relation-based target shapes decide ally from enemy by comparing it, and it is also what `BattleStartRequest.PerspectiveTeamId` names when the battle result is reported.

---

## StartingHealthMode

```csharp
public enum StartingHealthMode : byte
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

Chooses where a team member's starting current health comes from. The values
start at one deliberately: a zero byte is not a mode, so an asset that lost
the field fails validation instead of silently meaning full health.

| Value | Meaning |
| --- | --- |
| `FullHealth` | Start at the ceiling read from the combatant definition's maximum-health stat. |
| `ExplicitCurrentHealth` | Start at `TeamMemberDefinition.ExplicitCurrentHealth` instead of the ceiling. |

---

## StatDefinition

:material-star: **Start here**

```csharp
public sealed class StatDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/StatDefinition.cs</small>

One named number a combatant can carry, described only by the range it may hold.
Stats are anonymous to the engine: nothing is a health or a speed stat by name, it
becomes one because `BattleRulesDefinition` points its matching field
at this asset. That indirection is what lets a project name and re-shape its stat
line without the simulation caring.

Values are raw fixed-point everywhere, where 10000 means 1.0, both in the bounds
here and in the base values and status modifiers checked against them. A combatant
only has the stats its own `CombatantDefinition.BaseStats` list gives
it, so a stat asset nothing references affects no battle.

---

## StatusDefinition

:material-star: **Start here**

```csharp
public sealed class StatusDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/StatusDefinition.cs</small>

One condition that rides on a combatant for a while: how it stacks, how long it
lasts, what it modifies while resident, and what it does on its own clock. Effects
apply and remove it, dispels strip it, and the target's resistances and immunities
decide whether it lands at all.

This is the definition, not the instance. A status on the board holds only its own
bookkeeping - stacks, remaining duration, next periodic tick - and reads every rule
below by ID at each application, clock boundary, and dispel, so two combatants
carrying the same status can never disagree about how it behaves. Several fields
are only meaningful together and are cross-checked while content compiles: periodic
effects require a periodic phase, and `StatusStackPolicy.Refresh`
allows exactly one stack.

---

## StatusDurationClock

```csharp
public enum StatusDurationClock : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

Which clock decrements a status instance's remaining duration: the
owner's action start, the owner's action end, the owner's scheduler
opportunity, or elapsed battle ticks. The root action that created or
refreshed an instance never advances an owner-phase clock for it, and
only ElapsedTicks measures the authored amount in ticks.

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/ActionDefinitions.cs</small>

One adjustment a `StatusDefinition` applies for as long as it is
active. `Stage` decides where in the deterministic stat and formula
pipeline the adjustment joins and whether it is added or multiplied in. A status
may carry several modifiers, including several against the same stat, and the
authored order of the list is kept as the last tie-break between modifiers that
order equally.

---

## StatusPeriodicPhase

```csharp
public enum StatusPeriodicPhase : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

When a status's periodic effects fire. Owner-action ticks run immediately
before or after the owner's own skill effects; an elapsed boundary fires
on its own synthetic root action at the authored tick interval and is not
attached to whichever combatant happens to act next. None means the
status has no periodic effects, and authoring any is then invalid.

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

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

Whether a status reads as helpful, harmful, or neither. The engine uses
it to select instances for dispel effects, which match exactly one
polarity and only remove statuses their definition marks dispellable.

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

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/CoreDefinitions.cs</small>

One resistance entry on a `CombatantDefinition`, cutting the chance that a status
lands on it. `MatchKind` selects which key field below is read and leaves the other
ignored, and no two entries may repeat the same kind and key. Every entry that matches an
incoming status adds its chance into one total that is clamped at 100%, so a definition entry
and a tag entry for the same status both count.

---

## StatusStackPolicy

```csharp
public enum StatusStackPolicy : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

How a fresh application of a status interacts with an instance the target
already carries. Refresh keeps the single instance and resets its clocks,
AddStacksRefreshAll adds one stack up to the authored maximum and
refreshes the shared duration, Independent adds a separate instance with
its own duration and periodic cursor, Replace removes matching instances
before adding the new one, and KeepHigher keeps whichever definition has
the greater Strength.

| Value | Meaning |
| --- | --- |
| `Refresh` | &mdash; |
| `AddStacksRefreshAll` | &mdash; |
| `Independent` | &mdash; |
| `Replace` | &mdash; |
| `KeepHigher` | &mdash; |

---

## TargetDefinition

:material-star: **Start here**

```csharp
public sealed class TargetDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TargetDefinition.cs</small>

One reusable answer to "who may this skill hit": the registered target resolver that
picks and validates targets, plus the authored configuration handed to it. A
`SkillDefinition` points at one of these instead of describing its own
targeting.

Compilation copies the implementation reference and the properties into every skill
that references this asset, so one target may serve many skills and editing it changes
all of them. Both halves are checked then, not here: the resolver must resolve in the
mechanics registry by implementation ID and contract version together, and it validates
the authored properties itself, with any error failing the whole compile.

---

## TargetLockPolicy

```csharp
public enum TargetLockPolicy : byte
```

`TempoForge.Simulation` &middot; <small>TempoForge/Runtime/Simulation/Content/B3DefinitionPrimitives.cs</small>

When a skill captures the target IDs it will act on. This schema defines
only lock-at-acceptance: a compiled skill locks its targets when the
command is accepted, and what happens if one of them is invalid by the
time it is used is decided by `InvalidTargetPolicy`.

| Value | Meaning |
| --- | --- |
| `LockAtAcceptance` | &mdash; |

---

## TeamDefinition

:material-star: **Start here**

```csharp
public sealed class TeamDefinition : StableIdDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TeamDefinition.cs</small>

One reusable roster: the members that fight as a single side, each entry a combatant
definition plus the state it starts the battle in. The team carries no formation and no
side of the stage; an `EncounterDefinition` pairs it with a formation preset
and places each member, which is what lets the same team appear in several encounters.

A team needs at least one member, at least one of them starting above zero health, and a
`TeamMemberDefinition.CombatantInstanceId` that is unique inside the team.
None of that is enforced as the roster is edited; each failure is reported as a compile
diagnostic. The compiler sorts members by that instance ID, so the order entries appear
in the inspector never changes the compiled encounter.

---

## TeamMemberDefinition

```csharp
public sealed class TeamMemberDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

One roster entry of a `TeamDefinition`: which combatant definition
is instantiated and the state it starts the battle in. The compiler sorts
members by `CombatantInstanceId`, so the order entries appear in
the inspector never changes the compiled encounter.

---

## TeamMemberResourceOverrideDefinition

```csharp
public sealed class TeamMemberResourceOverrideDefinition
```

`TempoForge.Authoring` &middot; <small>TempoForge/Runtime/Authoring/Definitions/TeamEncounterDefinitions.cs</small>

Overrides the starting amount of one resource for a single team member. It
replaces the default the combatant definition already declares for that
resource; every resource left out of the list keeps its default.

---

