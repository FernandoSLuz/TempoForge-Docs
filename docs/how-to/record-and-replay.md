# Record and replay a battle

Turn a live battle into a file of bytes, play it back to confirm it reproduces, and read the
divergence report when it does not. A replay carries its own copy of the compiled content, so it
stays playable after you edit your catalog.

## Capture a replay

`ReplayEnvelope.Capture` reads a live engine and returns the whole recording: the compiled content,
the start request, the seed, every recorded command, and the periodic checkpoints the engine kept
along the way. Capture at any point — the envelope covers history up to that moment, not to the end
of the fight.

```csharp
using TempoForge.Simulation;

var replay = ReplayEnvelope.Capture(engine);
var bytes = ReplaySerializer.Write(replay);
System.IO.File.WriteAllBytes(path, bytes);
```

`Capture` serialises the envelope before returning it, so a recording that could not be written
throws `ReplayWriteException` instead of handing you an unwritable envelope. It refuses more than
4,096 recorded commands, more than 128 periodic checkpoints (the engine keeps one per 32 commands),
or a file over 64 MiB.

Commands the transport refused never enter the recording. Commands the rules rejected do, with the
reason id they were rejected for, so a played-back battle refuses them again at the same point.

In the editor, open **Tools > TempoForge > Battle Workbench**, expand the **Replay** section and
press **Capture**, then **Save**. Only an authoritative session can capture; a preview session and
a session already playing a replay both refuse.

## Write and read the file

`ReplaySerializer.Write` returns UTF-8 bytes of canonical JSON, and canonical means byte-exact.
Reading re-encodes the file and compares, so a file that is valid JSON but not the exact canonical
form is rejected: reordered fields, an extra field, a byte-order mark, a trailing newline and `00`
in place of `0` all fail. Treat the bytes as opaque and never hand-edit them.

`ReplaySerializer.Read` returns a result rather than throwing, and a failure carries one diagnostic.

```csharp
ReplayReadResult read = ReplaySerializer.Read(bytes, compiled.MechanicsRegistry);
if (!read.Succeeded) Debug.LogError(read.Diagnostic.Value.ToString());
```

| Diagnostic id | Cause |
| --- | --- |
| `replay.invalid` | The bytes are not the canonical form for the format they declare |
| `replay.incompatible` | The declared format or version tuple is not one this package reads |
| `replay.hash-mismatch` | An embedded hash does not match the bytes it covers |
| `replay.limit` | The file exceeds a command, checkpoint, property or byte limit |

Pass the mechanics registry that compiled your content. The single-argument overload builds the
shipped built-ins, and cannot decode content that binds an implementation you registered yourself.

!!! note "A replay does not read your project"
    The compiled content and the start request travel inside the file, hashed. Playback rebuilds an
    engine from those embedded bytes, so it never consults the catalog currently in your project.

## Play it back

`ReplayExecutor.Execute` creates a fresh engine from the embedded content, start request and seed,
drives it to each recorded submission boundary, resubmits each recorded command there, and compares
hashes at every checkpoint and at the end.

```csharp
var executed = ReplayExecutor.Execute(
    read.Replay, compiled.SchedulerRegistry, compiled.MechanicsRegistry);

if (executed.Succeeded)
    Debug.Log("Reproduced: " + executed.Snapshot.StateHash);
```

On success `Snapshot` is the final state, and its `StateHash` and `EventChainHash` equal the ones
recorded at capture. The result also hands back `FormulaAttributionTraces` and `AiDecisionTraces`
produced while replaying, which sit outside the battle state and the hashes.

In the Workbench, press **Open Replay** in the toolbar, then **Run To End**. **Step Recorded**
submits the next recorded command one at a time while a human decision is exposed. The window
verifies each command and checkpoint as it passes them and freezes on the first disagreement.

## Detect divergence

On a failed execution, `Diagnostic` is `replay.divergence` with a sentence naming the boundary,
`CommandIndex` and `CheckpointIndex` say how far it got, and `ExpectedHash` and `ActualHash` give
the recorded value against the one produced now. `HashKind` says which hash disagreed:

| `HashKind` | Meaning |
| --- | --- |
| `PreCommandState` | The state reached just before a recorded command differed |
| `CommandEvent` | A resubmitted command produced a different result or event hash |
| `State` | A checkpoint's battle state differed |
| `EventChain` | The state matched but the events leading to it did not |

### Content drift or behaviour drift

Because the content ships inside the file, a divergence is never your project's content changing. It
means the same content no longer resolves the same way: engine code changed, or a mechanics
implementation registered under an unchanged id now behaves differently.

To ask the other question — whether your *current* content still produces that battle — recompile
the catalog, create an engine from the same encounter and the same seed, run it to the end, and
compare `snapshot.ContentManifestHash` with `replay.ContentManifestHash`. If those differ, your
content changed. If they match and the replay still diverges, behaviour changed.

## Upgrade older replays

Three replay formats exist. Content authored today compiles to the third, and `Read` and `Execute`
accept all three, so nothing you capture now needs upgrading. `ReplayMigrationChain` is the
mechanism for a future format bump: it holds `IReplayMigration` steps that each advance exactly one
version, and the constructor throws if a step skips a version or two steps claim the same origin.
No migrations are registered for you.

```csharp
var chain = new ReplayMigrationChain(myMigrations);
var upgraded = chain.Migrate(bytes, fromVersion, targetVersion);
if (upgraded.Succeeded)
    read = ReplaySerializer.Read(upgraded.Bytes, compiled.MechanicsRegistry);
```

`Migrate` never mutates the array you pass. It fails with `replay.migration.missing` when no step
covers a version in the range, and `replay.migration.invalid-result` when a step returns nothing usable.

## Replays as regression tests

Record a battle you consider correct, keep the bytes with your test data, and executing that file
later is one assertion. It answers a narrow question honestly: whether the engine and the
implementations you register still reproduce the battle that was recorded. For the content question,
re-run the same encounter and seed against the recompiled catalog and compare the manifest hash.

Neither check replaces looking at aggregates. [Run Monte Carlo batches](monte-carlo-batches.md)
tells you whether a change was fair; [Step a battle in the Workbench](balance-with-the-workbench.md)
is where you find out why one number came out the way it did.

## Next

- **[Step a battle in the Workbench](balance-with-the-workbench.md)** — capture, open and step a
  recording in the editor.
- **[Determinism](../explanation/determinism.md)** — what makes a replay reproduce, and the choices
  on your side that break it.
- **[Replay reference](../reference/replay.md)** — the full member list for every replay type.
