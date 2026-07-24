# API reference

Every public type in TempoForge, grouped by what it is for rather than by namespace. **417 types.**

!!! tip "Filter as you type"
    Start typing in the box below to narrow the table. Use the search icon in the header to search the whole site instead.

<input type="text" id="api-filter" class="api-filter" placeholder="Filter types, groups, or descriptions..." autocomplete="off" aria-label="Filter API types">
<p id="api-filter-count" class="api-filter-count"></p>

<div class="api-table" markdown>

| Type | Kind | Area | What it is for |
| --- | --- | --- | --- |
| [`AdvanceTicksOutcome`](running-a-battle.md#advanceticksoutcome) | enum | Running a battle | _Undocumented._ |
| [`AdvanceTicksResult`](running-a-battle.md#advanceticksresult) | class | Running a battle | _Undocumented._ |
| [`BattleEngine`](running-a-battle.md#battleengine) | class | Running a battle | _Undocumented._ |
| [`BattleResultState`](running-a-battle.md#battleresultstate) | class | Running a battle | _Undocumented._ |
| [`BattleStartRequest`](running-a-battle.md#battlestartrequest) | class | Running a battle | _Undocumented._ |
| [`CommandDisposition`](running-a-battle.md#commanddisposition) | enum | Running a battle | _Undocumented._ |
| [`CommandResult`](running-a-battle.md#commandresult) | class | Running a battle | _Undocumented._ |
| [`ContractVersions`](running-a-battle.md#contractversions) | class | Running a battle | _Undocumented._ |
| [`ExecutionFrame`](running-a-battle.md#executionframe) | class | Running a battle | _Undocumented._ |
| [`ExecutionFrameTag`](running-a-battle.md#executionframetag) | enum | Running a battle | _Undocumented._ |
| [`MechanicsExecutionFrameData`](running-a-battle.md#mechanicsexecutionframedata) | class | Running a battle | _Undocumented._ |
| [`RestoreDiagnosticIds`](running-a-battle.md#restorediagnosticids) | class | Running a battle | _Undocumented._ |
| [`SimulationContractProfile`](running-a-battle.md#simulationcontractprofile) | class | Running a battle | _Undocumented._ |
| [`SimulationLimits`](running-a-battle.md#simulationlimits) | class | Running a battle | _Undocumented._ |
| [`StepActionOutcome`](running-a-battle.md#stepactionoutcome) | enum | Running a battle | _Undocumented._ |
| [`StepActionResult`](running-a-battle.md#stepactionresult) | class | Running a battle | _Undocumented._ |
| [`StepEventOutcome`](running-a-battle.md#stepeventoutcome) | enum | Running a battle | _Undocumented._ |
| [`StepEventResult`](running-a-battle.md#stepeventresult) | class | Running a battle | _Undocumented._ |
| [`ActionCostState`](commands-events-and-snapshots.md#actioncoststate) | class | Commands, events and snapshots | _Undocumented._ |
| [`ActiveActionState`](commands-events-and-snapshots.md#activeactionstate) | class | Commands, events and snapshots | _Undocumented._ |
| [`ActiveCastState`](commands-events-and-snapshots.md#activecaststate) | class | Commands, events and snapshots | _Undocumented._ |
| [`BattleCommand`](commands-events-and-snapshots.md#battlecommand) | class | Commands, events and snapshots | _Undocumented._ |
| [`BattleEvent`](commands-events-and-snapshots.md#battleevent) | class | Commands, events and snapshots | _Undocumented._ |
| [`BattleIds`](commands-events-and-snapshots.md#battleids) | class | Commands, events and snapshots | _Undocumented._ |
| [`BattleSnapshot`](commands-events-and-snapshots.md#battlesnapshot) | class | Commands, events and snapshots | _Undocumented._ |
| [`CombatantState`](commands-events-and-snapshots.md#combatantstate) | class | Commands, events and snapshots | _Undocumented._ |
| [`CommandSubmissionBoundary`](commands-events-and-snapshots.md#commandsubmissionboundary) | struct | Commands, events and snapshots | _Undocumented._ |
| [`CooldownState`](commands-events-and-snapshots.md#cooldownstate) | class | Commands, events and snapshots | _Undocumented._ |
| [`DecisionControlKind`](commands-events-and-snapshots.md#decisioncontrolkind) | enum | Commands, events and snapshots | _Undocumented._ |
| [`DecisionEntry`](commands-events-and-snapshots.md#decisionentry) | class | Commands, events and snapshots | _Undocumented._ |
| [`PropertyEntry`](commands-events-and-snapshots.md#propertyentry) | struct | Commands, events and snapshots | _Undocumented._ |
| [`PropertySet`](commands-events-and-snapshots.md#propertyset) | class | Commands, events and snapshots | _Undocumented._ |
| [`RecordedCommand`](commands-events-and-snapshots.md#recordedcommand) | class | Commands, events and snapshots | _Undocumented._ |
| [`RecordedCommandDisposition`](commands-events-and-snapshots.md#recordedcommanddisposition) | enum | Commands, events and snapshots | _Undocumented._ |
| [`ReplayCheckpoint`](commands-events-and-snapshots.md#replaycheckpoint) | class | Commands, events and snapshots | _Undocumented._ |
| [`ResourceState`](commands-events-and-snapshots.md#resourcestate) | class | Commands, events and snapshots | _Undocumented._ |
| [`StartCombatant`](commands-events-and-snapshots.md#startcombatant) | class | Commands, events and snapshots | _Undocumented._ |
| [`StartResource`](commands-events-and-snapshots.md#startresource) | class | Commands, events and snapshots | _Undocumented._ |
| [`StartTeam`](commands-events-and-snapshots.md#startteam) | class | Commands, events and snapshots | _Undocumented._ |
| [`TaggedValue`](commands-events-and-snapshots.md#taggedvalue) | class | Commands, events and snapshots | _Undocumented._ |
| [`TaggedValueTag`](commands-events-and-snapshots.md#taggedvaluetag) | enum | Commands, events and snapshots | _Undocumented._ |
| [`TeamState`](commands-events-and-snapshots.md#teamstate) | class | Commands, events and snapshots | _Undocumented._ |
| [`ActionCostPaymentPolicy`](scheduling-and-tempo.md#actioncostpaymentpolicy) | enum | Scheduling and tempo | _Undocumented._ |
| [`ActionOrderScheduler`](scheduling-and-tempo.md#actionorderscheduler) | class | Scheduling and tempo | _Undocumented._ |
| [`ActionOrderSchedulerAdjustmentAdapter`](scheduling-and-tempo.md#actionorderscheduleradjustmentadapter) | class | Scheduling and tempo | _Undocumented._ |
| [`ActionOrderSchedulerStateCodec`](scheduling-and-tempo.md#actionorderschedulerstatecodec) | class | Scheduling and tempo | _Undocumented._ |
| [`ActionOrderState`](scheduling-and-tempo.md#actionorderstate) | class | Scheduling and tempo | _Undocumented._ |
| [`AtbScheduler`](scheduling-and-tempo.md#atbscheduler) | class | Scheduling and tempo | _Undocumented._ |
| [`AtbSchedulerAdjustmentAdapter`](scheduling-and-tempo.md#atbscheduleradjustmentadapter) | class | Scheduling and tempo | _Undocumented._ |
| [`AtbSchedulerStateCodec`](scheduling-and-tempo.md#atbschedulerstatecodec) | class | Scheduling and tempo | _Undocumented._ |
| [`AtbState`](scheduling-and-tempo.md#atbstate) | class | Scheduling and tempo | _Undocumented._ |
| [`AutomaticTargetMode`](scheduling-and-tempo.md#automatictargetmode) | enum | Scheduling and tempo | _Undocumented._ |
| [`BattleClock`](scheduling-and-tempo.md#battleclock) | class | Scheduling and tempo | _Undocumented._ |
| [`BattleForecast`](scheduling-and-tempo.md#battleforecast) | class | Scheduling and tempo | _Undocumented._ |
| [`BattleSchedulerRegistry`](scheduling-and-tempo.md#battleschedulerregistry) | class | Scheduling and tempo | _Undocumented._ |
| [`BattleSchedulerResolveResult`](scheduling-and-tempo.md#battleschedulerresolveresult) | class | Scheduling and tempo | _Undocumented._ |
| [`CompiledActionCost`](scheduling-and-tempo.md#compiledactioncost) | class | Scheduling and tempo | _Undocumented._ |
| [`CompiledAutomaticDecisionPolicy`](scheduling-and-tempo.md#compiledautomaticdecisionpolicy) | class | Scheduling and tempo | _Undocumented._ |
| [`CompiledSchedulerDefinition`](scheduling-and-tempo.md#compiledschedulerdefinition) | class | Scheduling and tempo | _Undocumented._ |
| [`CompiledSkillTiming`](scheduling-and-tempo.md#compiledskilltiming) | class | Scheduling and tempo | _Undocumented._ |
| [`CooldownClockKind`](scheduling-and-tempo.md#cooldownclockkind) | enum | Scheduling and tempo | _Undocumented._ |
| [`CooldownStartPolicy`](scheduling-and-tempo.md#cooldownstartpolicy) | enum | Scheduling and tempo | _Undocumented._ |
| [`GaugeEntry`](scheduling-and-tempo.md#gaugeentry) | class | Scheduling and tempo | _Undocumented._ |
| [`IBattleScheduler`](scheduling-and-tempo.md#ibattlescheduler) | interface | Scheduling and tempo | _Undocumented._ |
| [`ISchedulerAdjustmentAdapter`](scheduling-and-tempo.md#ischeduleradjustmentadapter) | interface | Scheduling and tempo | _Undocumented._ |
| [`ISchedulerAdjustmentAdapterProvider`](scheduling-and-tempo.md#ischeduleradjustmentadapterprovider) | interface | Scheduling and tempo | _Undocumented._ |
| [`ISchedulerStateCodec`](scheduling-and-tempo.md#ischedulerstatecodec) | interface | Scheduling and tempo | _Undocumented._ |
| [`ISchedulerStateCodecProvider`](scheduling-and-tempo.md#ischedulerstatecodecprovider) | interface | Scheduling and tempo | _Undocumented._ |
| [`InputPausePolicy`](scheduling-and-tempo.md#inputpausepolicy) | enum | Scheduling and tempo | _Undocumented._ |
| [`InterruptRefundPolicy`](scheduling-and-tempo.md#interruptrefundpolicy) | enum | Scheduling and tempo | _Undocumented._ |
| [`ReadyTickEntry`](scheduling-and-tempo.md#readytickentry) | class | Scheduling and tempo | _Undocumented._ |
| [`RoundState`](scheduling-and-tempo.md#roundstate) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerAdjustmentContext`](scheduling-and-tempo.md#scheduleradjustmentcontext) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerAdjustmentResult`](scheduling-and-tempo.md#scheduleradjustmentresult) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerAdvanceContext`](scheduling-and-tempo.md#scheduleradvancecontext) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerAdvanceResult`](scheduling-and-tempo.md#scheduleradvanceresult) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerAdvanceStopReason`](scheduling-and-tempo.md#scheduleradvancestopreason) | enum | Scheduling and tempo | _Undocumented._ |
| [`SchedulerCombatantTimingView`](scheduling-and-tempo.md#schedulercombatanttimingview) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerCreateContext`](scheduling-and-tempo.md#schedulercreatecontext) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerCreateResult`](scheduling-and-tempo.md#schedulercreateresult) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerDiagnosticIds`](scheduling-and-tempo.md#schedulerdiagnosticids) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerDueTimer`](scheduling-and-tempo.md#schedulerduetimer) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerDueTimerKind`](scheduling-and-tempo.md#schedulerduetimerkind) | enum | Scheduling and tempo | _Undocumented._ |
| [`SchedulerIds`](scheduling-and-tempo.md#schedulerids) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerOpportunityContext`](scheduling-and-tempo.md#scheduleropportunitycontext) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerOpportunityOutcome`](scheduling-and-tempo.md#scheduleropportunityoutcome) | enum | Scheduling and tempo | _Undocumented._ |
| [`SchedulerOpportunityResult`](scheduling-and-tempo.md#scheduleropportunityresult) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerState`](scheduling-and-tempo.md#schedulerstate) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerStateDecodeResult`](scheduling-and-tempo.md#schedulerstatedecoderesult) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerStateTag`](scheduling-and-tempo.md#schedulerstatetag) | enum | Scheduling and tempo | _Undocumented._ |
| [`SchedulerTransitionResult`](scheduling-and-tempo.md#schedulertransitionresult) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerWork`](scheduling-and-tempo.md#schedulerwork) | class | Scheduling and tempo | _Undocumented._ |
| [`SchedulerWorkTag`](scheduling-and-tempo.md#schedulerworktag) | enum | Scheduling and tempo | _Undocumented._ |
| [`TimingResolutionKind`](scheduling-and-tempo.md#timingresolutionkind) | enum | Scheduling and tempo | _Undocumented._ |
| [`AiValidationContext`](effects-and-mechanics.md#aivalidationcontext) | class | Effects and mechanics | _Undocumented._ |
| [`BattleFormulaService`](effects-and-mechanics.md#battleformulaservice) | class | Effects and mechanics | Pure formula input and evaluation boundary shared by runtime, forecast, replay, Workbench, tooltips, and range previews. |
| [`BattleMechanicsRegistry`](effects-and-mechanics.md#battlemechanicsregistry) | class | Effects and mechanics | _Undocumented._ |
| [`BattleStateView`](effects-and-mechanics.md#battlestateview) | class | Effects and mechanics | Immutable, RNG-free projection supplied to non-formula mechanics extensions. |
| [`EffectPlan`](effects-and-mechanics.md#effectplan) | class | Effects and mechanics | _Undocumented._ |
| [`EffectPlanningContext`](effects-and-mechanics.md#effectplanningcontext) | class | Effects and mechanics | _Undocumented._ |
| [`EffectPrimitive`](effects-and-mechanics.md#effectprimitive) | class | Effects and mechanics | _Undocumented._ |
| [`EffectPrimitiveTag`](effects-and-mechanics.md#effectprimitivetag) | enum | Effects and mechanics | _Undocumented._ |
| [`EffectValidationContext`](effects-and-mechanics.md#effectvalidationcontext) | class | Effects and mechanics | _Undocumented._ |
| [`FormulaAttribution`](effects-and-mechanics.md#formulaattribution) | class | Effects and mechanics | _Undocumented._ |
| [`FormulaAttributionTrace`](effects-and-mechanics.md#formulaattributiontrace) | class | Effects and mechanics | Consumer-owned evidence linking full formula attribution bytes to the gameplay event that references their hash. |
| [`FormulaAttributionTraceBatch`](effects-and-mechanics.md#formulaattributiontracebatch) | class | Effects and mechanics | Bounded immutable formula evidence returned to one consumer call. |
| [`FormulaContext`](effects-and-mechanics.md#formulacontext) | class | Effects and mechanics | _Undocumented._ |
| [`FormulaContribution`](effects-and-mechanics.md#formulacontribution) | struct | Effects and mechanics | _Undocumented._ |
| [`FormulaContributionKind`](effects-and-mechanics.md#formulacontributionkind) | enum | Effects and mechanics | _Undocumented._ |
| [`FormulaEvaluationRequest`](effects-and-mechanics.md#formulaevaluationrequest) | class | Effects and mechanics | Immutable coordinates for one formula primitive. |
| [`FormulaModifierInput`](effects-and-mechanics.md#formulamodifierinput) | struct | Effects and mechanics | _Undocumented._ |
| [`FormulaPreview`](effects-and-mechanics.md#formulapreview) | class | Effects and mechanics | _Undocumented._ |
| [`FormulaPreviewContext`](effects-and-mechanics.md#formulapreviewcontext) | class | Effects and mechanics | _Undocumented._ |
| [`FormulaRandomBoundKind`](effects-and-mechanics.md#formularandomboundkind) | enum | Effects and mechanics | _Undocumented._ |
| [`FormulaRandomInputDescriptor`](effects-and-mechanics.md#formularandominputdescriptor) | struct | Effects and mechanics | _Undocumented._ |
| [`FormulaRandomSample`](effects-and-mechanics.md#formularandomsample) | struct | Effects and mechanics | _Undocumented._ |
| [`FormulaResult`](effects-and-mechanics.md#formularesult) | class | Effects and mechanics | _Undocumented._ |
| [`FormulaValidationContext`](effects-and-mechanics.md#formulavalidationcontext) | class | Effects and mechanics | _Undocumented._ |
| [`IAiPolicy`](effects-and-mechanics.md#iaipolicy) | interface | Effects and mechanics | _Undocumented._ |
| [`IEffectResolver`](effects-and-mechanics.md#ieffectresolver) | interface | Effects and mechanics | _Undocumented._ |
| [`IFormula`](effects-and-mechanics.md#iformula) | interface | Effects and mechanics | _Undocumented._ |
| [`IMechanicsImplementation`](effects-and-mechanics.md#imechanicsimplementation) | interface | Effects and mechanics | _Undocumented._ |
| [`IMechanicsRandomSource`](effects-and-mechanics.md#imechanicsrandomsource) | interface | Effects and mechanics | _Undocumented._ |
| [`IReactionRule`](effects-and-mechanics.md#ireactionrule) | interface | Effects and mechanics | _Undocumented._ |
| [`ITargetResolver`](effects-and-mechanics.md#itargetresolver) | interface | Effects and mechanics | _Undocumented._ |
| [`MechanicsCategoryTag`](effects-and-mechanics.md#mechanicscategorytag) | enum | Effects and mechanics | _Undocumented._ |
| [`MechanicsDiagnosticIds`](effects-and-mechanics.md#mechanicsdiagnosticids) | class | Effects and mechanics | _Undocumented._ |
| [`MechanicsIds`](effects-and-mechanics.md#mechanicsids) | class | Effects and mechanics | _Undocumented._ |
| [`MechanicsRegistryBinding`](effects-and-mechanics.md#mechanicsregistrybinding) | struct | Effects and mechanics | _Undocumented._ |
| [`MechanicsResolveResult`](effects-and-mechanics.md#mechanicsresolveresult) | class | Effects and mechanics | _Undocumented._ |
| [`ReactionValidationContext`](effects-and-mechanics.md#reactionvalidationcontext) | class | Effects and mechanics | _Undocumented._ |
| [`SchedulerAdjustmentKind`](effects-and-mechanics.md#scheduleradjustmentkind) | enum | Effects and mechanics | _Undocumented._ |
| [`StatusApplicationPreview`](effects-and-mechanics.md#statusapplicationpreview) | class | Effects and mechanics | RNG-free status application calculation used by runtime and tooltips. |
| [`TargetValidationContext`](effects-and-mechanics.md#targetvalidationcontext) | class | Effects and mechanics | _Undocumented._ |
| [`ValidationReport`](effects-and-mechanics.md#validationreport) | class | Effects and mechanics | _Undocumented._ |
| [`CombatantStatState`](statuses-targeting-and-reactions.md#combatantstatstate) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`ReactionContext`](statuses-targeting-and-reactions.md#reactioncontext) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`ReactionCycleDiagnostic`](statuses-targeting-and-reactions.md#reactioncyclediagnostic) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`ReactionEvaluation`](statuses-targeting-and-reactions.md#reactionevaluation) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`ReactionGraphEdge`](statuses-targeting-and-reactions.md#reactiongraphedge) | struct | Statuses, targeting and reactions | _Undocumented._ |
| [`ReactionGraphValidator`](statuses-targeting-and-reactions.md#reactiongraphvalidator) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`ReactionRootBudgetState`](statuses-targeting-and-reactions.md#reactionrootbudgetstate) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`ReactionSignature`](statuses-targeting-and-reactions.md#reactionsignature) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`ShieldState`](statuses-targeting-and-reactions.md#shieldstate) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`StatusInstanceState`](statuses-targeting-and-reactions.md#statusinstancestate) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`SystemStatusActionState`](statuses-targeting-and-reactions.md#systemstatusactionstate) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`TargetContext`](statuses-targeting-and-reactions.md#targetcontext) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`TargetLifeState`](statuses-targeting-and-reactions.md#targetlifestate) | enum | Statuses, targeting and reactions | _Undocumented._ |
| [`TargetRequestContract`](statuses-targeting-and-reactions.md#targetrequestcontract) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`TargetRequestResult`](statuses-targeting-and-reactions.md#targetrequestresult) | class | Statuses, targeting and reactions | _Undocumented._ |
| [`TargetTeamRelation`](statuses-targeting-and-reactions.md#targetteamrelation) | enum | Statuses, targeting and reactions | _Undocumented._ |
| [`AiCandidateDescription`](ai-policies.md#aicandidatedescription) | class | AI policies | _Undocumented._ |
| [`AiCandidatePlan`](ai-policies.md#aicandidateplan) | class | AI policies | _Undocumented._ |
| [`AiCandidateTrace`](ai-policies.md#aicandidatetrace) | class | AI policies | _Undocumented._ |
| [`AiConditionTrace`](ai-policies.md#aiconditiontrace) | struct | AI policies | _Undocumented._ |
| [`AiContext`](ai-policies.md#aicontext) | class | AI policies | _Undocumented._ |
| [`AiDecisionTrace`](ai-policies.md#aidecisiontrace) | class | AI policies | _Undocumented._ |
| [`AiConditionDefinition`](authoring-definitions.md#aiconditiondefinition) | class | Authoring definitions | _Undocumented._ |
| [`AiConditionKind`](authoring-definitions.md#aiconditionkind) | enum | Authoring definitions | _Undocumented._ |
| [`AiPolicyDefinition`](authoring-definitions.md#aipolicydefinition) | class | Authoring definitions | _Undocumented._ |
| [`AiRuleDefinition`](authoring-definitions.md#airuledefinition) | class | Authoring definitions | _Undocumented._ |
| [`AuthoringValueTag`](authoring-definitions.md#authoringvaluetag) | enum | Authoring definitions | _Undocumented._ |
| [`BattleContentCatalog`](authoring-definitions.md#battlecontentcatalog) | class | Authoring definitions | The sole root of a closed authoring graph. |
| [`BattleResultPolicyKind`](authoring-definitions.md#battleresultpolicykind) | enum | Authoring definitions | _Undocumented._ |
| [`BattleRulesDefinition`](authoring-definitions.md#battlerulesdefinition) | class | Authoring definitions | _Undocumented._ |
| [`CombatantDefinition`](authoring-definitions.md#combatantdefinition) | class | Authoring definitions | _Undocumented._ |
| [`CombatantResourceEntryDefinition`](authoring-definitions.md#combatantresourceentrydefinition) | class | Authoring definitions | _Undocumented._ |
| [`CombatantStatEntryDefinition`](authoring-definitions.md#combatantstatentrydefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledAiCondition`](authoring-definitions.md#compiledaicondition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledAiPolicyDefinition`](authoring-definitions.md#compiledaipolicydefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledAiRule`](authoring-definitions.md#compiledairule) | class | Authoring definitions | _Undocumented._ |
| [`CompiledBattleContent`](authoring-definitions.md#compiledbattlecontent) | class | Authoring definitions | _Undocumented._ |
| [`CompiledBattleRulesV3`](authoring-definitions.md#compiledbattlerulesv3) | class | Authoring definitions | _Undocumented._ |
| [`CompiledCombatantDefinition`](authoring-definitions.md#compiledcombatantdefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledEffectEntry`](authoring-definitions.md#compiledeffectentry) | class | Authoring definitions | _Undocumented._ |
| [`CompiledMechanicsBinding`](authoring-definitions.md#compiledmechanicsbinding) | class | Authoring definitions | _Undocumented._ |
| [`CompiledReactionDefinition`](authoring-definitions.md#compiledreactiondefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledResourceDefault`](authoring-definitions.md#compiledresourcedefault) | struct | Authoring definitions | _Undocumented._ |
| [`CompiledResourceDefinition`](authoring-definitions.md#compiledresourcedefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledSkillDefinition`](authoring-definitions.md#compiledskilldefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledStatDefinition`](authoring-definitions.md#compiledstatdefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledStatModifier`](authoring-definitions.md#compiledstatmodifier) | class | Authoring definitions | _Undocumented._ |
| [`CompiledStatValue`](authoring-definitions.md#compiledstatvalue) | struct | Authoring definitions | _Undocumented._ |
| [`CompiledStatusDefinition`](authoring-definitions.md#compiledstatusdefinition) | class | Authoring definitions | _Undocumented._ |
| [`CompiledStatusDuration`](authoring-definitions.md#compiledstatusduration) | class | Authoring definitions | _Undocumented._ |
| [`CompiledStatusPeriodicPolicy`](authoring-definitions.md#compiledstatusperiodicpolicy) | class | Authoring definitions | _Undocumented._ |
| [`CompiledStatusResistance`](authoring-definitions.md#compiledstatusresistance) | struct | Authoring definitions | _Undocumented._ |
| [`EffectDefinition`](authoring-definitions.md#effectdefinition) | class | Authoring definitions | _Undocumented._ |
| [`EffectUseDefinition`](authoring-definitions.md#effectusedefinition) | class | Authoring definitions | _Undocumented._ |
| [`EncounterDefinition`](authoring-definitions.md#encounterdefinition) | class | Authoring definitions | _Undocumented._ |
| [`EncounterTeamDefinition`](authoring-definitions.md#encounterteamdefinition) | class | Authoring definitions | _Undocumented._ |
| [`FormationAssignmentDefinition`](authoring-definitions.md#formationassignmentdefinition) | class | Authoring definitions | _Undocumented._ |
| [`InitialStatusApplicationDefinition`](authoring-definitions.md#initialstatusapplicationdefinition) | class | Authoring definitions | _Undocumented._ |
| [`InvalidTargetPolicy`](authoring-definitions.md#invalidtargetpolicy) | enum | Authoring definitions | _Undocumented._ |
| [`MechanicsImplementationReference`](authoring-definitions.md#mechanicsimplementationreference) | struct | Authoring definitions | _Undocumented._ |
| [`MechanicsImplementationReferenceDefinition`](authoring-definitions.md#mechanicsimplementationreferencedefinition) | class | Authoring definitions | _Undocumented._ |
| [`ModifierStage`](authoring-definitions.md#modifierstage) | enum | Authoring definitions | _Undocumented._ |
| [`PropertyEntryDefinition`](authoring-definitions.md#propertyentrydefinition) | class | Authoring definitions | _Undocumented._ |
| [`PropertyEntrySnapshot`](authoring-definitions.md#propertyentrysnapshot) | class | Authoring definitions | _Undocumented._ |
| [`PropertySetDefinition`](authoring-definitions.md#propertysetdefinition) | class | Authoring definitions | _Undocumented._ |
| [`ReactionDefinition`](authoring-definitions.md#reactiondefinition) | class | Authoring definitions | _Undocumented._ |
| [`ReactionTriggerPhase`](authoring-definitions.md#reactiontriggerphase) | enum | Authoring definitions | _Undocumented._ |
| [`ResistanceMatchKind`](authoring-definitions.md#resistancematchkind) | enum | Authoring definitions | _Undocumented._ |
| [`ResourceDefinition`](authoring-definitions.md#resourcedefinition) | class | Authoring definitions | _Undocumented._ |
| [`SchedulerDefinition`](authoring-definitions.md#schedulerdefinition) | class | Authoring definitions | _Undocumented._ |
| [`SkillCostDefinition`](authoring-definitions.md#skillcostdefinition) | class | Authoring definitions | _Undocumented._ |
| [`SkillDefinition`](authoring-definitions.md#skilldefinition) | class | Authoring definitions | _Undocumented._ |
| [`StableIdDefinition`](authoring-definitions.md#stableiddefinition) | class | Authoring definitions | Base class for authoring assets whose identity survives file, folder, label, and localization changes. |
| [`StartCombatantV3`](authoring-definitions.md#startcombatantv3) | class | Authoring definitions | _Undocumented._ |
| [`StartResourceV3`](authoring-definitions.md#startresourcev3) | struct | Authoring definitions | _Undocumented._ |
| [`StartStatusApplicationV3`](authoring-definitions.md#startstatusapplicationv3) | class | Authoring definitions | _Undocumented._ |
| [`StartTeamV3`](authoring-definitions.md#startteamv3) | class | Authoring definitions | _Undocumented._ |
| [`StartingHealthMode`](authoring-definitions.md#startinghealthmode) | enum | Authoring definitions | _Undocumented._ |
| [`StatDefinition`](authoring-definitions.md#statdefinition) | class | Authoring definitions | _Undocumented._ |
| [`StatusDefinition`](authoring-definitions.md#statusdefinition) | class | Authoring definitions | _Undocumented._ |
| [`StatusDurationClock`](authoring-definitions.md#statusdurationclock) | enum | Authoring definitions | _Undocumented._ |
| [`StatusModifierDefinition`](authoring-definitions.md#statusmodifierdefinition) | class | Authoring definitions | _Undocumented._ |
| [`StatusPeriodicPhase`](authoring-definitions.md#statusperiodicphase) | enum | Authoring definitions | _Undocumented._ |
| [`StatusPolarity`](authoring-definitions.md#statuspolarity) | enum | Authoring definitions | _Undocumented._ |
| [`StatusResistanceDefinition`](authoring-definitions.md#statusresistancedefinition) | class | Authoring definitions | _Undocumented._ |
| [`StatusStackPolicy`](authoring-definitions.md#statusstackpolicy) | enum | Authoring definitions | _Undocumented._ |
| [`TargetDefinition`](authoring-definitions.md#targetdefinition) | class | Authoring definitions | _Undocumented._ |
| [`TargetLockPolicy`](authoring-definitions.md#targetlockpolicy) | enum | Authoring definitions | _Undocumented._ |
| [`TeamDefinition`](authoring-definitions.md#teamdefinition) | class | Authoring definitions | _Undocumented._ |
| [`TeamMemberDefinition`](authoring-definitions.md#teammemberdefinition) | class | Authoring definitions | _Undocumented._ |
| [`TeamMemberResourceOverrideDefinition`](authoring-definitions.md#teammemberresourceoverridedefinition) | class | Authoring definitions | _Undocumented._ |
| [`AuthoringCategoryTag`](compiling-and-validating-content.md#authoringcategorytag) | enum | Compiling and validating content | _Undocumented._ |
| [`AuthoringCompileOptions`](compiling-and-validating-content.md#authoringcompileoptions) | class | Compiling and validating content | _Undocumented._ |
| [`AuthoringCompileRequest`](compiling-and-validating-content.md#authoringcompilerequest) | class | Compiling and validating content | _Undocumented._ |
| [`AuthoringCompileResult`](compiling-and-validating-content.md#authoringcompileresult) | class | Compiling and validating content | _Undocumented._ |
| [`AuthoringDiagnostic`](compiling-and-validating-content.md#authoringdiagnostic) | class | Compiling and validating content | _Undocumented._ |
| [`AuthoringDiagnosticIds`](compiling-and-validating-content.md#authoringdiagnosticids) | class | Compiling and validating content | _Undocumented._ |
| [`AuthoringDiagnosticSeverity`](compiling-and-validating-content.md#authoringdiagnosticseverity) | enum | Compiling and validating content | _Undocumented._ |
| [`AuthoringFieldTokens`](compiling-and-validating-content.md#authoringfieldtokens) | class | Compiling and validating content | _Undocumented._ |
| [`AuthoringLimits`](compiling-and-validating-content.md#authoringlimits) | class | Compiling and validating content | _Undocumented._ |
| [`AuthoringValidationReport`](compiling-and-validating-content.md#authoringvalidationreport) | class | Compiling and validating content | _Undocumented._ |
| [`BattleContentCompiler`](compiling-and-validating-content.md#battlecontentcompiler) | class | Compiling and validating content | Deterministic, synchronous, fail-closed compiler. |
| [`CompiledAuthoringCatalog`](compiling-and-validating-content.md#compiledauthoringcatalog) | class | Compiling and validating content | _Undocumented._ |
| [`CompiledEncounterSnapshot`](compiling-and-validating-content.md#compiledencountersnapshot) | class | Compiling and validating content | _Undocumented._ |
| [`FrozenSortedIndex`](compiling-and-validating-content.md#frozensortedindex) | class | Compiling and validating content | A defensively copied, key-sorted immutable index. |
| [`PortableSourceCoordinate`](compiling-and-validating-content.md#portablesourcecoordinate) | struct | Compiling and validating content | _Undocumented._ |
| [`AspectRatio`](formations.md#aspectratio) | struct | Formations | _Undocumented._ |
| [`CompiledEncounterFormationLayout`](formations.md#compiledencounterformationlayout) | class | Formations | _Undocumented._ |
| [`CompiledEncounterFormationTeam`](formations.md#compiledencounterformationteam) | class | Formations | _Undocumented._ |
| [`CompiledFormationAnchor`](formations.md#compiledformationanchor) | struct | Formations | _Undocumented._ |
| [`CompiledFormationPreset`](formations.md#compiledformationpreset) | class | Formations | _Undocumented._ |
| [`CompiledFormationSlot`](formations.md#compiledformationslot) | class | Formations | _Undocumented._ |
| [`EncounterFormationCompileRequest`](formations.md#encounterformationcompilerequest) | class | Formations | _Undocumented._ |
| [`EncounterFormationCompileResult`](formations.md#encounterformationcompileresult) | class | Formations | _Undocumented._ |
| [`EncounterFormationTeamRequest`](formations.md#encounterformationteamrequest) | class | Formations | _Undocumented._ |
| [`FormationAssignment`](formations.md#formationassignment) | struct | Formations | _Undocumented._ |
| [`FormationDelta`](formations.md#formationdelta) | struct | Formations | _Undocumented._ |
| [`FormationDragPoint`](formations.md#formationdragpoint) | struct | Formations | _Undocumented._ |
| [`FormationFacing`](formations.md#formationfacing) | enum | Formations | _Undocumented._ |
| [`FormationFieldTokens`](formations.md#formationfieldtokens) | class | Formations | _Undocumented._ |
| [`FormationHandleKey`](formations.md#formationhandlekey) | struct | Formations | _Undocumented._ |
| [`FormationHandleKind`](formations.md#formationhandlekind) | enum | Formations | _Undocumented._ |
| [`FormationInverseDragRequest`](formations.md#formationinversedragrequest) | class | Formations | _Undocumented._ |
| [`FormationInverseDragResult`](formations.md#formationinversedragresult) | class | Formations | _Undocumented._ |
| [`FormationLayoutCompiler`](formations.md#formationlayoutcompiler) | class | Formations | Pure deterministic formation compiler and integer projection service. |
| [`FormationOccupancy`](formations.md#formationoccupancy) | struct | Formations | _Undocumented._ |
| [`FormationPoint`](formations.md#formationpoint) | struct | Formations | _Undocumented._ |
| [`FormationPresetCompileRequest`](formations.md#formationpresetcompilerequest) | class | Formations | _Undocumented._ |
| [`FormationPresetCompileResult`](formations.md#formationpresetcompileresult) | class | Formations | _Undocumented._ |
| [`FormationPresetDefinition`](formations.md#formationpresetdefinition) | class | Formations | Mutable Unity authoring data. |
| [`FormationProjectionEntry`](formations.md#formationprojectionentry) | struct | Formations | _Undocumented._ |
| [`FormationProjectionRequest`](formations.md#formationprojectionrequest) | class | Formations | _Undocumented._ |
| [`FormationProjectionResult`](formations.md#formationprojectionresult) | class | Formations | _Undocumented._ |
| [`FormationSlotDefinition`](formations.md#formationslotdefinition) | class | Formations | _Undocumented._ |
| [`FormationVfxAnchorDefinition`](formations.md#formationvfxanchordefinition) | class | Formations | _Undocumented._ |
| [`FormationViewport`](formations.md#formationviewport) | struct | Formations | _Undocumented._ |
| [`MovedFormationPoint`](formations.md#movedformationpoint) | struct | Formations | _Undocumented._ |
| [`ProjectedFormationPoint`](formations.md#projectedformationpoint) | struct | Formations | _Undocumented._ |
| [`BattleSkinDefaults`](skinning-and-appearance.md#battleskindefaults) | class | Skinning and appearance | The shipped skins, defined in code rather than as serialized assets. |
| [`BattleSkinPreset`](skinning-and-appearance.md#battleskinpreset) | class | Skinning and appearance | Every value the battle interface draws itself with, in one asset. |
| [`CompiledBattleSkin`](skinning-and-appearance.md#compiledbattleskin) | class | Skinning and appearance | The immutable skin the HUD reads. |
| [`CompiledSkinBars`](skinning-and-appearance.md#compiledskinbars) | class | Skinning and appearance | The resolved bar set for one skin. |
| [`CompiledSkinLayout`](skinning-and-appearance.md#compiledskinlayout) | class | Skinning and appearance | The resolved layout and region set for one skin. |
| [`CompiledSkinSurfaces`](skinning-and-appearance.md#compiledskinsurfaces) | class | Skinning and appearance | The resolved surface set for one skin. |
| [`SkinAnchor`](skinning-and-appearance.md#skinanchor) | enum | Skinning and appearance | Where a HUD region attaches inside the safe area. |
| [`SkinBarTokens`](skinning-and-appearance.md#skinbartokens) | struct | Skinning and appearance | A value bar: health, shield, resource, cast, or gauge. |
| [`SkinEasing`](skinning-and-appearance.md#skineasing) | enum | Skinning and appearance | The easing curve applied to a skinned transition. |
| [`SkinFillMode`](skinning-and-appearance.md#skinfillmode) | enum | Skinning and appearance | How a skinned surface fills its rectangle. |
| [`SkinFloatingNumberTokens`](skinning-and-appearance.md#skinfloatingnumbertokens) | struct | Skinning and appearance | Rise-and-fade numbers for damage, healing, and shields. |
| [`SkinMaterialPool`](skinning-and-appearance.md#skinmaterialpool) | class | Skinning and appearance | Reference-counted material pool for skinned surfaces, owned by a component rather than by static state. |
| [`SkinMaterialRequest`](skinning-and-appearance.md#skinmaterialrequest) | struct | Skinning and appearance | The full parameter set for one skinned-surface material. |
| [`SkinMotionTokens`](skinning-and-appearance.md#skinmotiontokens) | struct | Skinning and appearance | Transition timings. |
| [`SkinPaletteTokens`](skinning-and-appearance.md#skinpalettetokens) | struct | Skinning and appearance | The semantic colour roles a skin assigns once and reuses everywhere. |
| [`SkinRegionTokens`](skinning-and-appearance.md#skinregiontokens) | struct | Skinning and appearance | Where one HUD region sits. |
| [`SkinShape`](skinning-and-appearance.md#skinshape) | enum | Skinning and appearance | The silhouette a skinned surface draws. |
| [`SkinStatusPipTokens`](skinning-and-appearance.md#skinstatuspiptokens) | struct | Skinning and appearance | The status pip strip drawn above a combatant. |
| [`SkinSurfaceGraphic`](skinning-and-appearance.md#skinsurfacegraphic) | class | Skinning and appearance | Draws one `kinSurfaceTokens` as a uGUI graphic through the TempoForge skinned-surface shader. |
| [`SkinSurfaceTokens`](skinning-and-appearance.md#skinsurfacetokens) | struct | Skinning and appearance | Fill, stroke, and glow for one skinned surface. |
| [`SkinTypographyTokens`](skinning-and-appearance.md#skintypographytokens) | struct | Skinning and appearance | Type sizing and treatment. |
| [`BattleNumberFormat`](interface-and-widgets.md#battlenumberformat) | class | Interface and widgets | Turns the simulation's fixed-point types into player-facing text. |
| [`BattleUiCommandChoice`](interface-and-widgets.md#battleuicommandchoice) | struct | Interface and widgets | A player-chosen command the driver (not the UI) will submit. |
| [`BattleUiRoot`](interface-and-widgets.md#battleuiroot) | class | Interface and widgets | The battle interface. |
| [`DecisionOptions`](interface-and-widgets.md#decisionoptions) | class | Interface and widgets | The complete set of legal command shapes for one pending decision: filtered granted skills plus whether concession is offered. |
| [`DecisionShapeCompiler`](interface-and-widgets.md#decisionshapecompiler) | class | Interface and widgets | Pure compiler of legal command shapes from a snapshot and compiled catalog. |
| [`DisplayStringTable`](interface-and-widgets.md#displaystringtable) | class | Interface and widgets | A non-authoritative map from stable id to display text. |
| [`FeedbackLogView`](interface-and-widgets.md#feedbacklogview) | class | Interface and widgets | The rolling battle log. |
| [`FloatingNumberLabel`](interface-and-widgets.md#floatingnumberlabel) | class | Interface and widgets | One rise-and-fade combat number. |
| [`PointerFocusRelay`](interface-and-widgets.md#pointerfocusrelay) | class | Interface and widgets | Forwards pointer enter and exit as plain C# events. |
| [`ResultBannerView`](interface-and-widgets.md#resultbannerview) | class | Interface and widgets | The terminal result banner. |
| [`SafeAreaFitter`](interface-and-widgets.md#safeareafitter) | class | Interface and widgets | Insets a `ectTransform` to the device safe area so HUD regions never land under a notch, a punch-hole camera, or a home indicator. |
| [`SkillCommandShape`](interface-and-widgets.md#skillcommandshape) | class | Interface and widgets | One legal skill command shape offered to the pending actor. |
| [`SkillTrayView`](interface-and-widgets.md#skilltrayview) | class | Interface and widgets | The command tray offered to a pending human actor: one button per legal skill shape plus concede. |
| [`SkinnedTokenPlate`](interface-and-widgets.md#skinnedtokenplate) | class | Interface and widgets | The floating plate above one combatant: name, health, shield, cast progress, scheduler gauge, and status pips. |
| [`SkinnedValueBar`](interface-and-widgets.md#skinnedvaluebar) | class | Interface and widgets | A skinned value bar: track, an optional trailing ghost showing the value just lost, the live fill, and an optional numeric readout. |
| [`SkinnedWidgetFactory`](interface-and-widgets.md#skinnedwidgetfactory) | class | Interface and widgets | Builds the skinned uGUI primitives the HUD is assembled from. |
| [`StatusRosterView`](interface-and-widgets.md#statusrosterview) | class | Interface and widgets | The combatant roster: one row per combatant with name, health bar, shield readout, and status count. |
| [`TargetShape`](interface-and-widgets.md#targetshape) | struct | Interface and widgets | The display-only shape of a skill's target request, taken from the compiled target contract. |
| [`TimelineStripView`](interface-and-widgets.md#timelinestripview) | class | Interface and widgets | The turn-order strip: one chip per upcoming actor, left to right, with the actor about to act raised and accented. |
| [`TooltipData`](interface-and-widgets.md#tooltipdata) | struct | Interface and widgets | A passive tooltip value computed by the DRIVER through the public preview surface (`BattleFormulaService.Preview` / `PreviewStatusApplication`, `FormulaPreview`, and `IEffectResolv... |
| [`TooltipPanelView`](interface-and-widgets.md#tooltippanelview) | class | Interface and widgets | The skill tooltip: cost, timing, target shape, and the driver-computed preview figures. |
| [`TransportBarView`](interface-and-widgets.md#transportbarview) | class | Interface and widgets | Scenario picker, seed field, and playback controls, drawn with the skin. |
| [`UiStatusEntry`](interface-and-widgets.md#uistatusentry) | struct | Interface and widgets | One combatant's surfaced status-panel row. |
| [`BattlePresenter`](stage-and-tokens.md#battlepresenter) | class | Stage and tokens | The pure presentation consumer. |
| [`BattleStage2D`](stage-and-tokens.md#battlestage2d) | class | Stage and tokens | A neutral 2D battle stage. |
| [`BattleStageBloom`](stage-and-tokens.md#battlestagebloom) | class | Stage and tokens | Optional stage bloom and vignette. |
| [`BattleStageFrame`](stage-and-tokens.md#battlestageframe) | class | Stage and tokens | Controls where the battle stage sits on screen and how large it is. |
| [`BeatDeriver`](stage-and-tokens.md#beatderiver) | class | Stage and tokens | Pure event-to-beat derivation. |
| [`CombatantTokenView`](stage-and-tokens.md#combatanttokenview) | class | Stage and tokens | A neutral 2D token view for one combatant. |
| [`PresentationBeat`](stage-and-tokens.md#presentationbeat) | class | Stage and tokens | One immutable presentation beat: the event context plus the resolved recipe. |
| [`PresentationBeatContext`](stage-and-tokens.md#presentationbeatcontext) | struct | Stage and tokens | The non-authoritative, immutable data a beat needs, extracted entirely from one gameplay event's property set. |
| [`PresenterBinding`](stage-and-tokens.md#presenterbinding) | class | Stage and tokens | The explicit dependency bundle a driver hands to a `attlePresenter`. |
| [`StageFrameMode`](stage-and-tokens.md#stageframemode) | enum | Stage and tokens | How the stage rectangle is derived from the screen. |
| [`StageTokenPlacement`](stage-and-tokens.md#stagetokenplacement) | struct | Stage and tokens | Immutable placement of one token, taken verbatim from the compiled formation layout projected through `ormationLayoutCompiler`. |
| [`BuiltInAnimationAdapter`](presentation-adapters-and-recipes.md#builtinanimationadapter) | class | Presentation adapters and recipes | Neutral built-in animation adapter. |
| [`BuiltInAudioAdapter`](presentation-adapters-and-recipes.md#builtinaudioadapter) | class | Presentation adapters and recipes | Neutral built-in audio adapter. |
| [`BuiltInPoolAdapter`](presentation-adapters-and-recipes.md#builtinpooladapter) | class | Presentation adapters and recipes | Simple keyed GameObject pool. |
| [`BuiltInVfxAdapter`](presentation-adapters-and-recipes.md#builtinvfxadapter) | class | Presentation adapters and recipes | Neutral built-in VFX adapter. |
| [`FloatingNumberStyle`](presentation-adapters-and-recipes.md#floatingnumberstyle) | enum | Presentation adapters and recipes | Floating-number presentation style; purely cosmetic. |
| [`IAnimationAdapter`](presentation-adapters-and-recipes.md#ianimationadapter) | interface | Presentation adapters and recipes | Plays a keyed animation for a beat phase. |
| [`IAudioAdapter`](presentation-adapters-and-recipes.md#iaudioadapter) | interface | Presentation adapters and recipes | Plays a keyed one-shot sound. |
| [`IPoolAdapter`](presentation-adapters-and-recipes.md#ipooladapter) | interface | Presentation adapters and recipes | Keyed instance pool for token views, floating numbers, and pooled VFX. |
| [`IVfxAdapter`](presentation-adapters-and-recipes.md#ivfxadapter) | interface | Presentation adapters and recipes | Plays a keyed one-shot visual effect at the cue position. |
| [`PresentationBeatSpec`](presentation-adapters-and-recipes.md#presentationbeatspec) | class | Presentation adapters and recipes | One of the three fixed beats (In / Impact / Out) of a recipe. |
| [`PresentationCue`](presentation-adapters-and-recipes.md#presentationcue) | struct | Presentation adapters and recipes | Immutable spatial context handed to a visual adapter. |
| [`PresentationLog`](presentation-adapters-and-recipes.md#presentationlog) | class | Presentation adapters and recipes | Non-authoritative, log-once warning ledger shared by the presenter and its adapters. |
| [`PresentationRecipeDefinition`](presentation-adapters-and-recipes.md#presentationrecipedefinition) | class | Presentation adapters and recipes | A stable-id presentation recipe (In / Impact / Out beats) authored as a B4-style ScriptableObject. |
| [`PresentationRecipeResolver`](presentation-adapters-and-recipes.md#presentationreciperesolver) | class | Presentation adapters and recipes | Pure, deterministic recipe resolution. |
| [`PresentationRecipeSet`](presentation-adapters-and-recipes.md#presentationrecipeset) | class | Presentation adapters and recipes | An explicit, ordered list of presentation recipes. |
| [`PresentationSelectorKind`](presentation-adapters-and-recipes.md#presentationselectorkind) | enum | Presentation adapters and recipes | How a recipe selector narrows an event to a specific mechanic. |
| [`PresentationVfxAnchorKind`](presentation-adapters-and-recipes.md#presentationvfxanchorkind) | enum | Presentation adapters and recipes | Where a beat's VFX anchors, resolved through the compiled slot. |
| [`IReplayMigration`](replay.md#ireplaymigration) | interface | Replay | _Undocumented._ |
| [`ReplayDivergenceHashKind`](replay.md#replaydivergencehashkind) | enum | Replay | _Undocumented._ |
| [`ReplayEnvelope`](replay.md#replayenvelope) | class | Replay | _Undocumented._ |
| [`ReplayExecutionResult`](replay.md#replayexecutionresult) | class | Replay | _Undocumented._ |
| [`ReplayExecutor`](replay.md#replayexecutor) | class | Replay | _Undocumented._ |
| [`ReplayMigrationChain`](replay.md#replaymigrationchain) | class | Replay | _Undocumented._ |
| [`ReplayMigrationResult`](replay.md#replaymigrationresult) | class | Replay | _Undocumented._ |
| [`ReplayReadResult`](replay.md#replayreadresult) | class | Replay | _Undocumented._ |
| [`ReplaySerializer`](replay.md#replayserializer) | class | Replay | _Undocumented._ |
| [`ReplayWriteException`](replay.md#replaywriteexception) | class | Replay | _Undocumented._ |
| [`AnalysisDiagnosticIds`](analysis-and-balancing.md#analysisdiagnosticids) | class | Analysis and balancing | Permanent diagnostic identifiers for analysis batch contract 1. |
| [`AnalysisLimits`](analysis-and-balancing.md#analysislimits) | class | Analysis and balancing | Structural limits for analysis batch contract 1. |
| [`BatchExport`](analysis-and-balancing.md#batchexport) | class | Analysis and balancing | Deterministic CSV and JSON text generation for batch results. |
| [`BatchOutcomeKind`](analysis-and-balancing.md#batchoutcomekind) | enum | Analysis and balancing | The recorded stop reason of one batch battle. |
| [`BatchSeedPlan`](analysis-and-balancing.md#batchseedplan) | class | Analysis and balancing | An immutable deduplicated ascending seed list. |
| [`BattleBatchAggregate`](analysis-and-balancing.md#battlebatchaggregate) | class | Analysis and balancing | The deterministic single-threaded ordered reduction over the sorted records of one completed batch. |
| [`BattleBatchLimits`](analysis-and-balancing.md#battlebatchlimits) | class | Analysis and balancing | Per-battle stopping bounds. |
| [`BattleBatchRequest`](analysis-and-balancing.md#battlebatchrequest) | class | Analysis and balancing | The complete immutable input of one Monte Carlo batch. |
| [`BattleBatchResult`](analysis-and-balancing.md#battlebatchresult) | class | Analysis and balancing | The complete immutable result of one batch execution. |
| [`BattleBatchRunner`](analysis-and-balancing.md#battlebatchrunner) | class | Analysis and balancing | The deterministic scripted AI-versus-AI Monte Carlo runner. |
| [`BattleOutcomeRecord`](analysis-and-balancing.md#battleoutcomerecord) | class | Analysis and balancing | The immutable outcome of one batch battle. |
| [`SingleBattleReproduction`](analysis-and-balancing.md#singlebattlereproduction) | class | Analysis and balancing | A single-seed rerun derived by the exact batch per-battle algorithm plus the strict replay bytes captured from the same engine. |
| [`TeamWinCount`](analysis-and-balancing.md#teamwincount) | class | Analysis and balancing | One winning team and how many batch records it won. |
| [`B3CreationDiagnostic`](numerics-and-determinism.md#b3creationdiagnostic) | class | Numerics and determinism | _Undocumented._ |
| [`B3CreationResult`](numerics-and-determinism.md#b3creationresult) | class | Numerics and determinism | _Undocumented._ |
| [`B3CreationStage`](numerics-and-determinism.md#b3creationstage) | enum | Numerics and determinism | _Undocumented._ |
| [`CanonicalBattleSerializer`](numerics-and-determinism.md#canonicalbattleserializer) | class | Numerics and determinism | _Undocumented._ |
| [`CanonicalReadException`](numerics-and-determinism.md#canonicalreadexception) | class | Numerics and determinism | _Undocumented._ |
| [`CanonicalReader`](numerics-and-determinism.md#canonicalreader) | class | Numerics and determinism | _Undocumented._ |
| [`CanonicalWriter`](numerics-and-determinism.md#canonicalwriter) | class | Numerics and determinism | _Undocumented._ |
| [`Chance64`](numerics-and-determinism.md#chance64) | struct | Numerics and determinism | A deterministic probability value where 1,000,000 raw units equal 100%. |
| [`DeterministicRng`](numerics-and-determinism.md#deterministicrng) | struct | Numerics and determinism | _Undocumented._ |
| [`Diagnostic`](numerics-and-determinism.md#diagnostic) | struct | Numerics and determinism | _Undocumented._ |
| [`DiagnosticIds`](numerics-and-determinism.md#diagnosticids) | class | Numerics and determinism | _Undocumented._ |
| [`Fixed64`](numerics-and-determinism.md#fixed64) | struct | Numerics and determinism | _Undocumented._ |
| [`FrozenList`](numerics-and-determinism.md#frozenlist) | class | Numerics and determinism | _Undocumented._ |
| [`RngState`](numerics-and-determinism.md#rngstate) | struct | Numerics and determinism | _Undocumented._ |
| [`Sha256Digest`](numerics-and-determinism.md#sha256digest) | struct | Numerics and determinism | _Undocumented._ |
| [`StableId`](numerics-and-determinism.md#stableid) | struct | Numerics and determinism | _Undocumented._ |
| [`AuthoringMigrationBatchOrchestrator`](editor-tools.md#authoringmigrationbatchorchestrator) | class | Editor tools | Explicit, synchronous Editor migration transaction. |
| [`AuthoringMigrationRegistry`](editor-tools.md#authoringmigrationregistry) | class | Editor tools | _Undocumented._ |
| [`BattleSkinBrowserWindow`](editor-tools.md#battleskinbrowserwindow) | class | Editor tools | Browse the shipped skins, preview them with the real shader, and turn any of them into an editable asset in one click. |
| [`BattleSkinPresetEditor`](editor-tools.md#battleskinpreseteditor) | class | Editor tools | Inspector for `attleSkinPreset` with a live preview above the fields. |
| [`CompilerBackedMigrationPrecommitValidator`](editor-tools.md#compilerbackedmigrationprecommitvalidator) | class | Editor tools | Builds the exact, explicit authoring closure rooted at one catalog and validates detached migration output through the production compiler. |
| [`EditorDiagnosticNavigationIndex`](editor-tools.md#editordiagnosticnavigationindex) | class | Editor tools | _Undocumented._ |
| [`EditorDiagnosticNavigationRecord`](editor-tools.md#editordiagnosticnavigationrecord) | class | Editor tools | _Undocumented._ |
| [`IAuthoringAssetMigration`](editor-tools.md#iauthoringassetmigration) | interface | Editor tools | _Undocumented._ |
| [`IAuthoringMigrationCommitFaultInjector`](editor-tools.md#iauthoringmigrationcommitfaultinjector) | interface | Editor tools | _Undocumented._ |
| [`IAuthoringMigrationPrecommitValidator`](editor-tools.md#iauthoringmigrationprecommitvalidator) | interface | Editor tools | The product integration compiles and validates the complete affected catalog closure from detached staged snapshots. |
| [`IAuthoringStableIdChangingMigration`](editor-tools.md#iauthoringstableidchangingmigration) | interface | Editor tools | Optional, deliberately conspicuous escape hatch for a future documented public migration that must change gameplay identity. |
| [`MigrationAssetSnapshot`](editor-tools.md#migrationassetsnapshot) | class | Editor tools | _Undocumented._ |
| [`MigrationBatchResult`](editor-tools.md#migrationbatchresult) | class | Editor tools | _Undocumented._ |
| [`MigrationChange`](editor-tools.md#migrationchange) | class | Editor tools | _Undocumented._ |
| [`MigrationCommitCheckpoint`](editor-tools.md#migrationcommitcheckpoint) | enum | Editor tools | _Undocumented._ |
| [`MigrationObjectReferenceToken`](editor-tools.md#migrationobjectreferencetoken) | class | Editor tools | Editor-only identity for a serialized Unity object reference. |
| [`MigrationPrecommitValidationResult`](editor-tools.md#migrationprecommitvalidationresult) | class | Editor tools | _Undocumented._ |
| [`MigrationPreview`](editor-tools.md#migrationpreview) | class | Editor tools | _Undocumented._ |
| [`MigrationSerializedField`](editor-tools.md#migrationserializedfield) | class | Editor tools | _Undocumented._ |
| [`MigrationSerializedValue`](editor-tools.md#migrationserializedvalue) | class | Editor tools | Immutable scalar copied from a SerializedProperty. |
| [`MigrationSerializedValueKind`](editor-tools.md#migrationserializedvaluekind) | enum | Editor tools | _Undocumented._ |
| [`MigrationStepResult`](editor-tools.md#migrationstepresult) | class | Editor tools | _Undocumented._ |
| [`SkinPreviewRenderer`](editor-tools.md#skinpreviewrenderer) | class | Editor tools | Draws skin previews in editor windows and inspectors using the same shader the runtime interface uses. |
| [`AudioArtBinding`](other.md#audioartbinding) | class | Other | Binds a recipe audio key (an sfx-* clip name) to art. |
| [`DisplayStringTableAsset`](other.md#displaystringtableasset) | class | Other | The shipped serialized string-table asset the demo driver supplies to the presenter (specification section 3: display text comes from an explicit table, never from compiled snapsho... |
| [`Entry`](other.md#entry) | class | Other | One stable-id-to-display-name pair. |
| [`ForecastRequest`](other.md#forecastrequest) | class | Other | _Undocumented._ |
| [`ForecastResult`](other.md#forecastresult) | class | Other | _Undocumented._ |
| [`ForecastStopReason`](other.md#forecaststopreason) | enum | Other | _Undocumented._ |
| [`ParticleArtBinding`](other.md#particleartbinding) | class | Other | Binds a recipe VFX key (a particle-* sprite name) to art. |
| [`SessionEndState`](other.md#sessionendstate) | enum | Other | Typed end-of-session states surfaced by the driver. |
| [`TempoForgeDemoBootstrap`](other.md#tempoforgedemobootstrap) | class | Other | The runtime demo driver (specification section 9). |
| [`TokenArtBinding`](other.md#tokenartbinding) | class | Other | Binds a starter combatant definition id to its generated token sprite (the token-* art keys from the art manifest). |

</div>

