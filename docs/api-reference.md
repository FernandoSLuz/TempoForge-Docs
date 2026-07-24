# TempoForge API reference

Generated from the shipped source. 410 public types across 5 namespaces.

Members shown are the public surface. Anything not listed here is an implementation detail and may change between releases without notice.

## Contents

- [TempoForge.Simulation](#tempoforgesimulation) - 221 types
- [TempoForge.Authoring](#tempoforgeauthoring) - 81 types
- [TempoForge.Presentation](#tempoforgepresentation) - 72 types
- [TempoForge.Analysis](#tempoforgeanalysis) - 13 types
- [TempoForge.Editor](#tempoforgeeditor) - 23 types

---

## Types you will use most

### `BattleEngine`

`TempoForge.Simulation` - class

The authoritative battle. Your driver creates it, advances it, and submits commands. Nothing in the presentation layer holds one.

```csharp
BattleCommand Command
DeterministicRng RngAfterSelection
AiDecisionTrace Trace
int DrawCount
uint NextBelow(uint exclusiveUpperBound)
CompiledBattleContent Content
BattleStartRequest StartRequest
uint Seed
SimulationContractProfile Profile
BattleSnapshot GetSnapshot()
BattleMechanicsRegistry MechanicsRegistry
FrozenList<AiDecisionTrace> DrainAiDecisionTraces()
FormulaAttributionTraceBatch DrainFormulaAttributionTraces()
static BattleEngine Create()
BattleEngine Clone()
static BattleEngine Restore()
CommandResult Submit(BattleCommand command)
StepEventResult StepEvent()
StepActionResult StepAction()
FrozenList<BattleEvent> RunUntilBoundary()
AdvanceTicksResult AdvanceTicks(int count)
Sha256Digest ContentManifestHash
StableId SchedulerId
SchedulerState SchedulerState
long Tick
ulong NextCommandSequence
ulong NextEventSequence
ulong NextActionSequence
ulong NextApplicationSequence
ulong NextOpportunitySequence
ulong NextReactionSequence
ulong CompletedRootActionCount
DeterministicRng Rng
List<TeamState> Teams
List<CombatantState> Combatants
StableId? B1PendingDecisionActorId
List<ResourceState> Resources
List<CooldownState> Cooldowns
List<ActiveActionState> ActiveActions
List<CombatantStatState> Stats
// ... 12 more public members
```

### `BattlePresenter`

`TempoForge.Presentation` - class

Pure presentation consumer. Receives events and snapshots and drives visuals. It never calls Submit, AdvanceTicks, a forecast, or RNG.

```csharp
bool IsIdle
int QueuedBeatCount
int ActiveFloatingNumberCount
int ForcedInstantBeatCount
int CameraShakeRequestCount
BattleStage2D Stage
Action CameraShakeCallback
StableId PlayerTeamId
void Bind(PresenterBinding presenterBinding)
void SetViewport(FormationViewport value)
void EnqueueEvents(IReadOnlyList<BattleEvent> events)
void AdoptSnapshot(BattleSnapshot snapshot)
void Tick(float presentationDeltaSeconds)
void SkipAll()
void Teardown()
```

### `BattleUiRoot`

`TempoForge.Presentation` - class

The interface. Raises `CommandChosen` with the player's intent and submits nothing. `ApplySkin` restyles the whole thing at runtime.

```csharp
event Action<BattleUiCommandChoice> CommandChosen
DecisionOptions CurrentDecision
IReadOnlyList<SkillCommandShape> OfferedSkills
bool OffersConcede
IReadOnlyList<StableId> TimelineActors
IReadOnlyList<UiStatusEntry> StatusEntries
IReadOnlyList<string> FeedbackLines
bool IsResultShown
StableId? ResultId
string ResultText
BattleUiCommandChoice? LastCommandChoice
CompiledBattleSkin Skin
RectTransform TransportMount
void Initialize()
void ApplySkin(BattleSkinPreset preset)
void Tick(float presentationDeltaSeconds)
void ShowDecision(DecisionOptions options)
void ClearDecision()
void SetTooltip(TooltipData tooltip)
bool TryGetTooltip(StableId skillId, out TooltipData tooltip)
void UpdateTimeline(FrozenList<DecisionEntry> decisions)
void UpdateStatus(BattleSnapshot snapshot, DisplayStringTable labels)
void AppendFeedback(BattleEvent battleEvent, DisplayStringTable labels)
void ShowResult(BattleResultState result, DisplayStringTable labels)
void ChooseSkill(StableId skillId, IReadOnlyList<StableId> targets)
void ChooseConcede()
bool LegacyInputAvailable
string InputUnavailableMessage
```

### `BattleSkinPreset`

`TempoForge.Presentation` - class

One asset holding the entire interface look. `Compile()` returns the immutable `CompiledBattleSkin` the widgets read.

```csharp
string StableIdText
string DisplayName
string Description
CompiledBattleSkin Compile()
void CopyFrom(CompiledBattleSkin source, string newStableId, string newDisplayName)
```

### `BattleSkinDefaults`

`TempoForge.Presentation` - class

The four shipped skins, defined in code so the interface is never unstyled and no art is redistributed. `Resolve(preset)` never returns null.

```csharp
float CornerRadius
float StrokeWidth
float GlowRadius
float GlowIntensity
float ShadowRadius
float GradientSpread
SkinFillMode FillMode
SkinShape PipShape
static SkinPaletteTokens SlateNocturnePalette()
static SkinPaletteTokens ParchmentAtlasPalette()
static SkinPaletteTokens NeonCircuitPalette()
static SkinPaletteTokens MinimalMonoPalette()
static CompiledBattleSkin Default()
static CompiledBattleSkin SlateNocturne()
static CompiledBattleSkin ParchmentAtlas()
static CompiledBattleSkin NeonCircuit()
static CompiledBattleSkin MinimalMono()
static IReadOnlyList<CompiledBattleSkin> All()
static bool TryFind(string stableId, out CompiledBattleSkin skin)
static CompiledBattleSkin Resolve(BattleSkinPreset preset)
static SkinTypographyTokens DefaultTypography()
static SkinFloatingNumberTokens DefaultFloatingNumbers()
static SkinMotionTokens DefaultMotion()
static SkinSurfaceTokens SlateNocturnePanel()
static SkinSurfaceTokens SlateNocturnePanelRaised()
static SkinSurfaceTokens SlateNocturneButton()
static SkinSurfaceTokens SlateNocturneButtonSelected()
static SkinSurfaceTokens SlateNocturneButtonDisabled()
static SkinSurfaceTokens SlateNocturneTooltip()
static SkinSurfaceTokens SlateNocturneBackdrop()
static SkinBarTokens SlateNocturneHealthBar()
static SkinBarTokens SlateNocturneShieldBar()
static SkinBarTokens SlateNocturneResourceBar()
static SkinBarTokens SlateNocturneCastBar()
static SkinBarTokens SlateNocturneGauge()
static SkinStatusPipTokens SlateNocturnePips()
static CompiledSkinLayout DefaultLayout()
```

### `BattleStageFrame`

`TempoForge.Presentation` - class

Controls where the stage sits: fixed-aspect or full-screen, fractional margins reserving space for your interface, and stage scale.

```csharp
FormationViewport AppliedViewport
void ApplyNow()
FormationViewport Resolve(int screenWidth, int screenHeight, Rect safeAreaPixels)
```

### `BattleNumberFormat`

`TempoForge.Presentation` - class

Formats Fixed64 and Chance64 for players. Their own ToString returns raw scaled integers because it feeds canonical encoding, so never show that to a player.

```csharp
static string Amount(Fixed64 value)
static string WholeAmount(Fixed64 value)
static string AmountRange(Fixed64 minimum, Fixed64 maximum)
static string Percent(Chance64 value)
static string Ticks(int ticks)
```

---

## TempoForge.Simulation

The engine. Compiled with `noEngineReferences: true`, so it cannot touch a GameObject, a Transform, or UnityEngine.Random even by accident. This is what makes determinism auditable.

| Type | Kind | Public members |
| --- | --- | --- |
| `ActionCostState` | class | 2 |
| `ActionOrderScheduler` | class | 10 |
| `ActionOrderSchedulerAdjustmentAdapter` | class | 4 |
| `ActionOrderSchedulerStateCodec` | class | 6 |
| `ActionOrderState` | class | 4 |
| `ActiveActionState` | class | 12 |
| `ActiveCastState` | class | 3 |
| `AdvanceTicksResult` | class | 9 |
| `AiCandidateDescription` | class | 5 |
| `AiCandidatePlan` | class | 1 |
| `AiCandidateTrace` | class | 6 |
| `AiContext` | class | 4 |
| `AiDecisionTrace` | class | 12 |
| `AiValidationContext` | class | 1 |
| `AtbScheduler` | class | 10 |
| `AtbSchedulerAdjustmentAdapter` | class | 4 |
| `AtbSchedulerStateCodec` | class | 6 |
| `AtbState` | class | 4 |
| `B3CreationDiagnostic` | class | 9 |
| `B3CreationResult` | class | 3 |
| `BattleClock` | class | 1 |
| `BattleCommand` | class | 8 |
| `BattleEngine` | class | 52 |
| `BattleEvent` | class | 5 |
| `BattleForecast` | class | 1 |
| `BattleFormulaService` | class | 4 |
| `BattleIds` | class | 0 |
| `BattleMechanicsRegistry` | class | 12 |
| `BattleResultState` | class | 9 |
| `BattleSchedulerRegistry` | class | 7 |
| `BattleSchedulerResolveResult` | class | 5 |
| `BattleSnapshot` | class | 40 |
| `BattleStartRequest` | class | 10 |
| `BattleStateView` | class | 16 |
| `CanonicalBattleSerializer` | class | 24 |
| `CanonicalReadException` | class | 1 |
| `CanonicalReader` | class | 13 |
| `CanonicalWriter` | class | 15 |
| `CombatantStatState` | class | 3 |
| `CombatantState` | class | 12 |
| `CommandResult` | class | 10 |
| `CompiledActionCost` | class | 3 |
| `CompiledAiCondition` | class | 3 |
| `CompiledAiPolicyDefinition` | class | 4 |
| `CompiledAiRule` | class | 6 |
| `CompiledAutomaticDecisionPolicy` | class | 3 |
| `CompiledBattleContent` | class | 33 |
| `CompiledBattleRulesV3` | class | 23 |
| `CompiledCombatantDefinition` | class | 10 |
| `CompiledEffectEntry` | class | 4 |
| `CompiledMechanicsBinding` | class | 2 |
| `CompiledReactionDefinition` | class | 9 |
| `CompiledResourceDefinition` | class | 4 |
| `CompiledSchedulerDefinition` | class | 10 |
| `CompiledSkillDefinition` | class | 8 |
| `CompiledSkillTiming` | class | 12 |
| `CompiledStatDefinition` | class | 4 |
| `CompiledStatModifier` | class | 4 |
| `CompiledStatusDefinition` | class | 18 |
| `CompiledStatusDuration` | class | 2 |
| `CompiledStatusPeriodicPolicy` | class | 2 |
| `ContractVersions` | class | 0 |
| `CooldownState` | class | 6 |
| `DecisionEntry` | class | 4 |
| `DiagnosticIds` | class | 0 |
| `EffectPlan` | class | 3 |
| `EffectPlanningContext` | class | 5 |
| `EffectPrimitive` | class | 23 |
| `EffectValidationContext` | class | 1 |
| `ExecutionFrame` | class | 25 |
| `ForecastRequest` | class | 3 |
| `ForecastResult` | class | 10 |
| `FormulaAttribution` | class | 12 |
| `FormulaAttributionTrace` | class | 7 |
| `FormulaAttributionTraceBatch` | class | 4 |
| `FormulaContext` | class | 15 |
| `FormulaEvaluationRequest` | class | 5 |
| `FormulaPreview` | class | 6 |
| `FormulaPreviewContext` | class | 1 |
| `FormulaResult` | class | 4 |
| `FormulaValidationContext` | class | 1 |
| `FrozenList` | class | 4 |
| `GaugeEntry` | class | 3 |
| `MechanicsDiagnosticIds` | class | 0 |
| `MechanicsExecutionFrameData` | class | 13 |
| `MechanicsIds` | class | 0 |
| `MechanicsResolveResult` | class | 3 |
| `PropertySet` | class | 5 |
| `ReactionContext` | class | 8 |
| `ReactionCycleDiagnostic` | class | 3 |
| `ReactionEvaluation` | class | 4 |
| `ReactionGraphValidator` | class | 1 |
| `ReactionRootBudgetState` | class | 6 |
| `ReactionSignature` | class | 3 |
| `ReactionValidationContext` | class | 1 |
| `ReadyTickEntry` | class | 2 |
| `RecordedCommand` | class | 6 |
| `ReplayCheckpoint` | class | 5 |
| `ReplayEnvelope` | class | 30 |
| `ReplayExecutionResult` | class | 12 |
| `ReplayExecutor` | class | 2 |
| `ReplayMigrationChain` | class | 1 |
| `ReplayMigrationResult` | class | 5 |
| `ReplayReadResult` | class | 3 |
| `ReplaySerializer` | class | 3 |
| `ReplayWriteException` | class | 1 |
| `ResourceState` | class | 4 |
| `RestoreDiagnosticIds` | class | 0 |
| `RoundState` | class | 5 |
| `SchedulerAdjustmentContext` | class | 6 |
| `SchedulerAdjustmentResult` | class | 7 |
| `SchedulerAdvanceContext` | class | 7 |
| `SchedulerAdvanceResult` | class | 7 |
| `SchedulerCombatantTimingView` | class | 6 |
| `SchedulerCreateContext` | class | 3 |
| `SchedulerCreateResult` | class | 5 |
| `SchedulerDiagnosticIds` | class | 0 |
| `SchedulerDueTimer` | class | 5 |
| `SchedulerIds` | class | 0 |
| `SchedulerOpportunityContext` | class | 4 |
| `SchedulerOpportunityResult` | class | 6 |
| `SchedulerState` | class | 13 |
| `SchedulerStateDecodeResult` | class | 5 |
| `SchedulerTransitionResult` | class | 6 |
| `SchedulerWork` | class | 12 |
| `ShieldState` | class | 9 |
| `SimulationContractProfile` | class | 19 |
| `SimulationLimits` | class | 0 |
| `StartCombatant` | class | 11 |
| `StartCombatantV3` | class | 13 |
| `StartResource` | class | 3 |
| `StartStatusApplicationV3` | class | 3 |
| `StartTeam` | class | 3 |
| `StartTeamV3` | class | 2 |
| `StatusApplicationPreview` | class | 6 |
| `StatusInstanceState` | class | 12 |
| `StepActionResult` | class | 8 |
| `StepEventResult` | class | 8 |
| `SystemStatusActionState` | class | 5 |
| `TaggedValue` | class | 36 |
| `TargetContext` | class | 4 |
| `TargetRequestContract` | class | 8 |
| `TargetRequestResult` | class | 5 |
| `TargetValidationContext` | class | 1 |
| `TeamState` | class | 2 |
| `ValidationReport` | class | 6 |
| `AiConditionTrace` | struct | 3 |
| `Chance64` | struct | 11 |
| `CommandSubmissionBoundary` | struct | 6 |
| `CompiledResourceDefault` | struct | 2 |
| `CompiledStatValue` | struct | 2 |
| `CompiledStatusResistance` | struct | 3 |
| `DeterministicRng` | struct | 10 |
| `Diagnostic` | struct | 6 |
| `Fixed64` | struct | 17 |
| `FormulaContribution` | struct | 5 |
| `FormulaModifierInput` | struct | 6 |
| `FormulaRandomInputDescriptor` | struct | 6 |
| `FormulaRandomSample` | struct | 3 |
| `MechanicsImplementationReference` | struct | 5 |
| `MechanicsRegistryBinding` | struct | 6 |
| `PropertyEntry` | struct | 2 |
| `ReactionGraphEdge` | struct | 2 |
| `RngState` | struct | 8 |
| `Sha256Digest` | struct | 9 |
| `StableId` | struct | 8 |
| `StartResourceV3` | struct | 2 |
| `IAiPolicy` | interface | 0 |
| `IBattleScheduler` | interface | 0 |
| `IEffectResolver` | interface | 0 |
| `IFormula` | interface | 0 |
| `IMechanicsImplementation` | interface | 0 |
| `IMechanicsRandomSource` | interface | 0 |
| `IReactionRule` | interface | 0 |
| `IReplayMigration` | interface | 0 |
| `ISchedulerAdjustmentAdapter` | interface | 0 |
| `ISchedulerAdjustmentAdapterProvider` | interface | 0 |
| `ISchedulerStateCodec` | interface | 0 |
| `ISchedulerStateCodecProvider` | interface | 0 |
| `ITargetResolver` | interface | 0 |
| `ActionCostPaymentPolicy` | enum | 0 |
| `AdvanceTicksOutcome` | enum | 0 |
| `AiConditionKind` | enum | 0 |
| `AutomaticTargetMode` | enum | 0 |
| `B3CreationStage` | enum | 0 |
| `BattleResultPolicyKind` | enum | 0 |
| `CommandDisposition` | enum | 0 |
| `CooldownClockKind` | enum | 0 |
| `CooldownStartPolicy` | enum | 0 |
| `DecisionControlKind` | enum | 0 |
| `EffectPrimitiveTag` | enum | 0 |
| `ExecutionFrameTag` | enum | 0 |
| `ForecastStopReason` | enum | 0 |
| `FormulaContributionKind` | enum | 0 |
| `FormulaRandomBoundKind` | enum | 0 |
| `InputPausePolicy` | enum | 0 |
| `InterruptRefundPolicy` | enum | 0 |
| `InvalidTargetPolicy` | enum | 0 |
| `MechanicsCategoryTag` | enum | 0 |
| `ModifierStage` | enum | 0 |
| `ReactionTriggerPhase` | enum | 0 |
| `RecordedCommandDisposition` | enum | 0 |
| `ReplayDivergenceHashKind` | enum | 0 |
| `ResistanceMatchKind` | enum | 0 |
| `SchedulerAdjustmentKind` | enum | 0 |
| `SchedulerAdvanceStopReason` | enum | 0 |
| `SchedulerDueTimerKind` | enum | 0 |
| `SchedulerOpportunityOutcome` | enum | 0 |
| `SchedulerStateTag` | enum | 0 |
| `SchedulerWorkTag` | enum | 0 |
| `StatusDurationClock` | enum | 0 |
| `StatusPeriodicPhase` | enum | 0 |
| `StatusPolarity` | enum | 0 |
| `StatusStackPolicy` | enum | 0 |
| `StepActionOutcome` | enum | 0 |
| `StepEventOutcome` | enum | 0 |
| `TaggedValueTag` | enum | 0 |
| `TargetLifeState` | enum | 0 |
| `TargetLockPolicy` | enum | 0 |
| `TargetTeamRelation` | enum | 0 |
| `TimingResolutionKind` | enum | 0 |

## TempoForge.Authoring

Definition assets you create in the Project window, plus the compiler that freezes a catalog into immutable content.

| Type | Kind | Public members |
| --- | --- | --- |
| `AiConditionDefinition` | class | 0 |
| `AiPolicyDefinition` | class | 0 |
| `AiRuleDefinition` | class | 0 |
| `AuthoringCompileOptions` | class | 3 |
| `AuthoringCompileRequest` | class | 5 |
| `AuthoringCompileResult` | class | 4 |
| `AuthoringDiagnostic` | class | 10 |
| `AuthoringDiagnosticIds` | class | 0 |
| `AuthoringFieldTokens` | class | 0 |
| `AuthoringLimits` | class | 0 |
| `AuthoringValidationReport` | class | 3 |
| `BattleContentCatalog` | class | 0 |
| `BattleContentCompiler` | class | 2 |
| `BattleRulesDefinition` | class | 0 |
| `CombatantDefinition` | class | 0 |
| `CombatantResourceEntryDefinition` | class | 0 |
| `CombatantStatEntryDefinition` | class | 0 |
| `CompiledAuthoringCatalog` | class | 5 |
| `CompiledEncounterFormationLayout` | class | 3 |
| `CompiledEncounterFormationTeam` | class | 4 |
| `CompiledEncounterSnapshot` | class | 4 |
| `CompiledFormationPreset` | class | 4 |
| `CompiledFormationSlot` | class | 9 |
| `EffectDefinition` | class | 0 |
| `EffectUseDefinition` | class | 0 |
| `EncounterDefinition` | class | 0 |
| `EncounterFormationCompileRequest` | class | 3 |
| `EncounterFormationCompileResult` | class | 4 |
| `EncounterFormationTeamRequest` | class | 4 |
| `EncounterTeamDefinition` | class | 0 |
| `FormationAssignmentDefinition` | class | 0 |
| `FormationFieldTokens` | class | 0 |
| `FormationInverseDragRequest` | class | 5 |
| `FormationInverseDragResult` | class | 5 |
| `FormationLayoutCompiler` | class | 4 |
| `FormationPresetCompileRequest` | class | 2 |
| `FormationPresetCompileResult` | class | 4 |
| `FormationPresetDefinition` | class | 4 |
| `FormationProjectionRequest` | class | 3 |
| `FormationProjectionResult` | class | 8 |
| `FormationSlotDefinition` | class | 11 |
| `FormationVfxAnchorDefinition` | class | 3 |
| `FrozenSortedIndex` | class | 2 |
| `InitialStatusApplicationDefinition` | class | 0 |
| `MechanicsImplementationReferenceDefinition` | class | 0 |
| `PropertyEntryDefinition` | class | 19 |
| `PropertyEntrySnapshot` | class | 20 |
| `PropertySetDefinition` | class | 2 |
| `ReactionDefinition` | class | 0 |
| `ResourceDefinition` | class | 0 |
| `SchedulerDefinition` | class | 0 |
| `SkillCostDefinition` | class | 0 |
| `SkillDefinition` | class | 0 |
| `StableIdDefinition` | class | 4 |
| `StatDefinition` | class | 0 |
| `StatusDefinition` | class | 0 |
| `StatusModifierDefinition` | class | 0 |
| `StatusResistanceDefinition` | class | 0 |
| `TargetDefinition` | class | 0 |
| `TeamDefinition` | class | 0 |
| `TeamMemberDefinition` | class | 0 |
| `TeamMemberResourceOverrideDefinition` | class | 0 |
| `AspectRatio` | struct | 5 |
| `CompiledFormationAnchor` | struct | 2 |
| `FormationAssignment` | struct | 2 |
| `FormationDelta` | struct | 5 |
| `FormationDragPoint` | struct | 2 |
| `FormationHandleKey` | struct | 7 |
| `FormationOccupancy` | struct | 6 |
| `FormationPoint` | struct | 5 |
| `FormationProjectionEntry` | struct | 3 |
| `FormationViewport` | struct | 7 |
| `MovedFormationPoint` | struct | 2 |
| `PortableSourceCoordinate` | struct | 10 |
| `ProjectedFormationPoint` | struct | 5 |
| `AuthoringCategoryTag` | enum | 0 |
| `AuthoringDiagnosticSeverity` | enum | 0 |
| `AuthoringValueTag` | enum | 0 |
| `FormationFacing` | enum | 0 |
| `FormationHandleKind` | enum | 0 |
| `StartingHealthMode` | enum | 0 |

## TempoForge.Presentation

Stage, tokens, interface, skins, and adapters. Reads values only; it never mutates a battle.

| Type | Kind | Public members |
| --- | --- | --- |
| `BattleNumberFormat` | class | 5 |
| `BattlePresenter` | class | 15 |
| `BattleSkinDefaults` | class | 37 |
| `BattleSkinPreset` | class | 5 |
| `BattleStage2D` | class | 9 |
| `BattleStageBloom` | class | 1 |
| `BattleStageFrame` | class | 3 |
| `BattleUiRoot` | class | 28 |
| `BeatDeriver` | class | 2 |
| `BuiltInAnimationAdapter` | class | 2 |
| `BuiltInAudioAdapter` | class | 2 |
| `BuiltInPoolAdapter` | class | 5 |
| `BuiltInVfxAdapter` | class | 2 |
| `CombatantTokenView` | class | 21 |
| `CompiledBattleSkin` | class | 13 |
| `CompiledSkinBars` | class | 5 |
| `CompiledSkinLayout` | class | 10 |
| `CompiledSkinSurfaces` | class | 7 |
| `DecisionOptions` | class | 5 |
| `DecisionShapeCompiler` | class | 1 |
| `DisplayStringTable` | class | 4 |
| `FeedbackLogView` | class | 2 |
| `FloatingNumberLabel` | class | 5 |
| `PointerFocusRelay` | class | 4 |
| `PresentationBeat` | class | 5 |
| `PresentationBeatSpec` | class | 11 |
| `PresentationLog` | class | 3 |
| `PresentationRecipeDefinition` | class | 9 |
| `PresentationRecipeResolver` | class | 2 |
| `PresentationRecipeSet` | class | 2 |
| `PresenterBinding` | class | 10 |
| `ResultBannerView` | class | 5 |
| `SafeAreaFitter` | class | 2 |
| `SkillCommandShape` | class | 2 |
| `SkillTrayView` | class | 15 |
| `SkinMaterialPool` | class | 6 |
| `SkinSurfaceGraphic` | class | 5 |
| `SkinnedTokenPlate` | class | 10 |
| `SkinnedValueBar` | class | 10 |
| `SkinnedWidgetFactory` | class | 8 |
| `StatusRosterView` | class | 9 |
| `TimelineStripView` | class | 7 |
| `TooltipPanelView` | class | 4 |
| `TransportBarView` | class | 12 |
| `BattleUiCommandChoice` | struct | 4 |
| `PresentationBeatContext` | struct | 9 |
| `PresentationCue` | struct | 5 |
| `SkinBarTokens` | struct | 9 |
| `SkinFloatingNumberTokens` | struct | 7 |
| `SkinMaterialRequest` | struct | 9 |
| `SkinMotionTokens` | struct | 12 |
| `SkinPaletteTokens` | struct | 15 |
| `SkinRegionTokens` | struct | 9 |
| `SkinStatusPipTokens` | struct | 6 |
| `SkinSurfaceTokens` | struct | 18 |
| `SkinTypographyTokens` | struct | 8 |
| `StageTokenPlacement` | struct | 9 |
| `TargetShape` | struct | 7 |
| `TooltipData` | struct | 11 |
| `UiStatusEntry` | struct | 6 |
| `IAnimationAdapter` | interface | 0 |
| `IAudioAdapter` | interface | 0 |
| `IPoolAdapter` | interface | 0 |
| `IVfxAdapter` | interface | 0 |
| `FloatingNumberStyle` | enum | 0 |
| `PresentationSelectorKind` | enum | 0 |
| `PresentationVfxAnchorKind` | enum | 0 |
| `SkinAnchor` | enum | 0 |
| `SkinEasing` | enum | 0 |
| `SkinFillMode` | enum | 0 |
| `SkinShape` | enum | 0 |
| `StageFrameMode` | enum | 0 |

## TempoForge.Analysis

Batch runs and Monte Carlo export for balancing.

| Type | Kind | Public members |
| --- | --- | --- |
| `AnalysisDiagnosticIds` | class | 0 |
| `AnalysisLimits` | class | 0 |
| `BatchExport` | class | 2 |
| `BatchSeedPlan` | class | 3 |
| `BattleBatchAggregate` | class | 17 |
| `BattleBatchLimits` | class | 3 |
| `BattleBatchRequest` | class | 7 |
| `BattleBatchResult` | class | 5 |
| `BattleBatchRunner` | class | 3 |
| `BattleOutcomeRecord` | class | 17 |
| `SingleBattleReproduction` | class | 2 |
| `TeamWinCount` | class | 2 |
| `BatchOutcomeKind` | enum | 0 |

## TempoForge.Editor

Workbench, formation editor, content validator, and Skin Browser.

| Type | Kind | Public members |
| --- | --- | --- |
| `AuthoringMigrationBatchOrchestrator` | class | 1 |
| `AuthoringMigrationRegistry` | class | 2 |
| `BattleSkinBrowserWindow` | class | 5 |
| `BattleSkinPresetEditor` | class | 3 |
| `CompilerBackedMigrationPrecommitValidator` | class | 4 |
| `EditorDiagnosticNavigationIndex` | class | 2 |
| `EditorDiagnosticNavigationRecord` | class | 4 |
| `MigrationAssetSnapshot` | class | 13 |
| `MigrationBatchResult` | class | 5 |
| `MigrationChange` | class | 4 |
| `MigrationObjectReferenceToken` | class | 6 |
| `MigrationPrecommitValidationResult` | class | 1 |
| `MigrationPreview` | class | 5 |
| `MigrationSerializedField` | class | 5 |
| `MigrationSerializedValue` | class | 4 |
| `MigrationStepResult` | class | 3 |
| `SkinPreviewRenderer` | class | 6 |
| `IAuthoringAssetMigration` | interface | 0 |
| `IAuthoringMigrationCommitFaultInjector` | interface | 0 |
| `IAuthoringMigrationPrecommitValidator` | interface | 0 |
| `IAuthoringStableIdChangingMigration` | interface | 0 |
| `MigrationCommitCheckpoint` | enum | 0 |
| `MigrationSerializedValueKind` | enum | 0 |

