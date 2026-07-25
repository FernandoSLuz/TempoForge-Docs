# Presentation adapters and recipes

16 types in this area.

!!! abstract "On this page"
    [BuiltInAnimationAdapter](#builtinanimationadapter) &middot; [BuiltInAudioAdapter](#builtinaudioadapter) &middot; [BuiltInPoolAdapter](#builtinpooladapter) &middot; [BuiltInVfxAdapter](#builtinvfxadapter) &middot; [FloatingNumberStyle](#floatingnumberstyle) &middot; [IAnimationAdapter](#ianimationadapter) &middot; [IAudioAdapter](#iaudioadapter) &middot; [IPoolAdapter](#ipooladapter) &middot; [IVfxAdapter](#ivfxadapter) &middot; [PresentationBeatSpec](#presentationbeatspec) &middot; [PresentationCue](#presentationcue) &middot; [PresentationLog](#presentationlog) &middot; [PresentationRecipeDefinition](#presentationrecipedefinition) &middot; [PresentationRecipeSet](#presentationrecipeset) &middot; [PresentationSelectorKind](#presentationselectorkind) &middot; [PresentationVfxAnchorKind](#presentationvfxanchorkind)

## BuiltInAnimationAdapter

```csharp
public sealed class BuiltInAnimationAdapter : IAnimationAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/BuiltInPresentationAdapters.cs</small>

Neutral built-in animation adapter. Customers bind a stable-id key to a
handler (their own flip-book, Animator trigger, etc.). Out of the box no
keys are bound, so every key degrades to a single logged warning and a
no-op, never a gameplay effect. Fully replaceable per B6-08.

**Constructors**

`public BuiltInAnimationAdapter(PresentationLog log = null)`

:   &mdash;

**Methods**

`public void Play(string animationKey, PresentationCue cue)`

:   &mdash;

`public void Register(string animationKey, Action<PresentationCue> handler)`

:   Binds a key to a neutral flip-book/animator handler.

---

## BuiltInAudioAdapter

```csharp
public sealed class BuiltInAudioAdapter : IAudioAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/BuiltInPresentationAdapters.cs</small>

Neutral built-in audio adapter. Registered keys map to a clip played
through an optional shared `udioSource`; unknown keys
degrade to a single warning and a no-op.

**Constructors**

`public BuiltInAudioAdapter(AudioSource source = null, PresentationLog log = null)`

:   &mdash;

**Methods**

`public void Play(string audioKey)`

:   &mdash;

`public void Register(string audioKey, AudioClip clip)`

:   Binds a key to a one-shot clip.

---

## BuiltInPoolAdapter

```csharp
public sealed class BuiltInPoolAdapter : IPoolAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/BuiltInPresentationAdapters.cs</small>

Simple keyed GameObject pool. Instances are reused across acquire/release
cycles so open/close loops leak nothing. Each key is capped at
`aximumPerKey` live instances; an over-cap acquire degrades
to a single warning and a null result rather than allocating forever.

**Constructors**

`public BuiltInPoolAdapter(Transform root = null, PresentationLog log = null)`

:   &mdash;

**Methods**

`public GameObject Acquire(string key)`

:   &mdash;

`public int ActiveCount(string key)`

:   &mdash;

`public int IdleCount(string key)`

:   Idle (recycled) instances retained for a key.

`public void RegisterPrototype(string key, GameObject prototype)`

:   Binds a key to a prototype cloned on acquire.

`public void Release(GameObject instance)`

:   &mdash;

---

## BuiltInVfxAdapter

```csharp
public sealed class BuiltInVfxAdapter : IVfxAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/BuiltInPresentationAdapters.cs</small>

Neutral built-in VFX adapter. Registered keys spawn a pooled instance of
a prototype at the cue position through the shared pool; unknown keys
degrade to a single warning and a no-op.

**Constructors**

`public BuiltInVfxAdapter(IPoolAdapter pool = null, PresentationLog log = null)`

:   &mdash;

**Methods**

`public void Play(string vfxKey, PresentationCue cue)`

:   &mdash;

`public void RegisterKey(string vfxKey)`

:   Registers a VFX key as bound to art.

---

## FloatingNumberStyle

```csharp
public enum FloatingNumberStyle
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Recipes/PresentationRecipeDefinition.cs</small>

Floating-number presentation style; purely cosmetic.

| Value | Meaning |
| --- | --- |
| `None` | &mdash; |
| `Damage` | &mdash; |
| `Heal` | &mdash; |
| `Shield` | &mdash; |
| `Resource` | &mdash; |
| `Status` | &mdash; |
| `Critical` | &mdash; |

---

## IAnimationAdapter

:material-puzzle: **Extension point** &mdash; implement this yourself to change behaviour

```csharp
public interface IAnimationAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/PresentationAdapters.cs</small>

Plays a keyed animation for a beat phase. Implementations bind the
stable-id key to their own art; a missing key must degrade silently.

---

## IAudioAdapter

:material-puzzle: **Extension point** &mdash; implement this yourself to change behaviour

```csharp
public interface IAudioAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/PresentationAdapters.cs</small>

Plays a keyed one-shot sound. Timing is presentation-only.

---

## IPoolAdapter

:material-puzzle: **Extension point** &mdash; implement this yourself to change behaviour

```csharp
public interface IPoolAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/PresentationAdapters.cs</small>

Keyed instance pool for token views, floating numbers, and pooled VFX.
`cquire` returns null when a key exceeds its structural
cap so the caller degrades visibly rather than allocating without bound.

---

## IVfxAdapter

:material-puzzle: **Extension point** &mdash; implement this yourself to change behaviour

```csharp
public interface IVfxAdapter
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/PresentationAdapters.cs</small>

Plays a keyed one-shot visual effect at the cue position.

---

## PresentationBeatSpec

```csharp
public sealed class PresentationBeatSpec
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Recipes/PresentationRecipeDefinition.cs</small>

One of the three fixed beats (In / Impact / Out) of a recipe. Timing is
a raw Fixed64 seconds value bounded to the section 10 cap; every field is
non-authoritative and never enters any battle hash.

**Constructors**

`public PresentationBeatSpec()`

:   &mdash;

`public PresentationBeatSpec()`

:   &mdash;

**Properties**

`public string AnimationKey`

:   &mdash;

`public string AudioKey`

:   &mdash;

`public bool CameraShake`

:   &mdash;

`public long ClampedDurationRaw`

:   Raw duration clamped to the 0..30 s structural cap.

`public long DurationRawSeconds`

:   Raw Fixed64 seconds as authored (may be out of range).

`public float DurationSeconds`

:   Clamped duration expressed in presentation seconds.

`public bool ExceedsDurationCap`

:   True when the authored duration exceeds the structural cap.

`public FloatingNumberStyle FloatingNumberStyle`

:   &mdash;

`public string VfxAnchorId`

:   &mdash;

`public PresentationVfxAnchorKind VfxAnchorKind`

:   &mdash;

`public string VfxKey`

:   &mdash;

---

## PresentationCue

```csharp
public readonly struct PresentationCue
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/PresentationAdapters.cs</small>

Immutable spatial context handed to a visual adapter. It carries the
world placement resolved by the stage plus the participant identifiers
for the beat, never any authoritative value or engine reference.

**Constructors**

`public PresentationCue()`

:   &mdash;

**Properties**

`public FormationFacing Facing`

:   Facing derived from the compiled formation slot.

`public Transform Parent`

:   Optional parent for spawned instances; may be null.

`public StableId SourceId`

:   Beat source identifier; may be the default (invalid) id.

`public StableId TargetId`

:   Beat target identifier; may be the default (invalid) id.

`public Vector3 WorldPosition`

:   Stage-space position the adapter should present at.

---

## PresentationLog

```csharp
public sealed class PresentationLog
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Adapters/PresentationAdapters.cs</small>

Non-authoritative, log-once warning ledger shared by the presenter and
its adapters. A missing adapter key degrades to a single warning per
key so a render frame never spams the console or throws.

**Constructors**

`public PresentationLog(Action<string> sink = null)`

:   &mdash;

**Properties**

`public int WarningCount`

:   Distinct keys that have produced a warning so far.

**Methods**

`public bool HasWarnedFor(string key)`

:   &mdash;

`public void WarnOnce(string key, string message)`

:   Emits at most one warning per `key`. Subsequent calls with the same key are silently ignored (documented degrade).

---

## PresentationRecipeDefinition

```csharp
public sealed class PresentationRecipeDefinition : StableIdDefinition
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Recipes/PresentationRecipeDefinition.cs</small>

A stable-id presentation recipe (In / Impact / Out beats) authored as a
B4-style ScriptableObject. Recipes are excluded from B3 compilation and
from every authoritative hash; editing one can never change a simulation
output. Selectors bind an event type plus an optional mechanic id or tag.

**Properties**

`public string EventTypeIdRaw`

:   Raw serialized event type id the recipe reacts to.

`public PresentationBeatSpec ImpactBeat`

:   &mdash;

`public PresentationBeatSpec InBeat`

:   &mdash;

`public PresentationBeatSpec OutBeat`

:   &mdash;

`public PresentationSelectorKind SelectorKind`

:   &mdash;

`public int SelectorSpecificity`

:   Deterministic specificity rank: exact id (3) beats tag (2) beats event default (1). Higher wins; ties break by recipe stable id.

`public string SelectorValueRaw`

:   Raw serialized exact-id or tag value; empty for defaults.

**Methods**

`public PresentationBeatSpec GetBeat(int phaseIndex)`

:   Fetches the beat for a fixed phase index (0=In,1=Impact,2=Out).

`public bool TryGetEventTypeId(out StableId id)`

:   Parses the event type id; false when it is unset or invalid.

`public bool TryGetSelectorValue(out StableId id)`

:   Parses the selector value; false for defaults or bad ids.

---

## PresentationRecipeSet

```csharp
public sealed class PresentationRecipeSet : StableIdDefinition
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Recipes/PresentationRecipeSet.cs</small>

An explicit, ordered list of presentation recipes. Resolution reads only
this list and never scans the project, so a set is a closed, reviewable
unit of skinnable content. The set is non-authoritative and never enters
any battle hash.

**Properties**

`public bool ExceedsRecipeCap`

:   True when the set exceeds its structural cap.

`public IReadOnlyList<PresentationRecipeDefinition> Recipes`

:   The explicit recipe list in authored order.

---

## PresentationSelectorKind

```csharp
public enum PresentationSelectorKind
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Recipes/PresentationRecipeDefinition.cs</small>

How a recipe selector narrows an event to a specific mechanic. The
deterministic specificity ordering is exact id > tag > event
default, matching `resentationRecipeResolver`.

| Value | Meaning |
| --- | --- |
| `EventDefault` | &mdash; |
| `SkillId` | &mdash; |
| `SkillTag` | &mdash; |
| `StatusId` | &mdash; |
| `StatusTag` | &mdash; |
| `ReactionId` | &mdash; |

---

## PresentationVfxAnchorKind

```csharp
public enum PresentationVfxAnchorKind
```

`TempoForge.Presentation` &middot; <small>TempoForge/Runtime/Presentation/Recipes/PresentationRecipeDefinition.cs</small>

Where a beat's VFX anchors, resolved through the compiled slot.

| Value | Meaning |
| --- | --- |
| `Slot` | &mdash; |
| `Approach` | &mdash; |
| `Anchor` | &mdash; |

---

