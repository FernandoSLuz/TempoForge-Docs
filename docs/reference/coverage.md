# Documentation coverage

Generated from source alongside the reference itself, so it cannot quietly drift. This page exists because a reference that hides its own gaps is worse than one that admits them.

| Scope | Documented | Total | Coverage |
| --- | --- | --- | --- |
| Public types | 97 | 317 | 31% |
| Public members | 217 | 1682 | 13% |

Measured over the 317 types this reference publishes.

## What is excluded, and why

A further **104** public types are left out. They are public only because `internal` is per-assembly in C# and this package spans several assemblies, so publishing them would describe plumbing as API. They carry `[EditorBrowsable(Never)]` in the source.

Coverage is reported over the published surface for the same reason: documenting the excluded types would raise this percentage without helping anyone read the package.

## By area

| Area | Types | Documented | Coverage |
| --- | --- | --- | --- |
| [Running a battle](running-a-battle.md) | 11 | 0 | 0% |
| [Commands, events and snapshots](commands-events-and-snapshots.md) | 17 | 0 | 0% |
| [Scheduling and tempo](scheduling-and-tempo.md) | 44 | 0 | 0% |
| [Effects and mechanics](effects-and-mechanics.md) | 41 | 6 | 15% |
| [Statuses, targeting and reactions](statuses-targeting-and-reactions.md) | 11 | 0 | 0% |
| [AI policies](ai-policies.md) | 6 | 0 | 0% |
| [Authoring definitions](authoring-definitions.md) | 57 | 2 | 4% |
| [Compiling and validating content](compiling-and-validating-content.md) | 11 | 2 | 18% |
| [Formations](formations.md) | 14 | 1 | 7% |
| [Skinning and appearance](skinning-and-appearance.md) | 17 | 17 | 100% |
| [Interface and widgets](interface-and-widgets.md) | 21 | 21 | 100% |
| [Stage and tokens](stage-and-tokens.md) | 10 | 10 | 100% |
| [Presentation adapters and recipes](presentation-adapters-and-recipes.md) | 16 | 16 | 100% |
| [Replay](replay.md) | 10 | 0 | 0% |
| [Analysis and balancing](analysis-and-balancing.md) | 13 | 13 | 100% |
| [Numerics and determinism](numerics-and-determinism.md) | 7 | 1 | 14% |
| [Editor tools](editor-tools.md) | 1 | 1 | 100% |
| [Other](other.md) | 10 | 7 | 70% |

## How to read this

Low coverage in an area is usually **not** a sign that the types are unclear. Much of the surface is small immutable data carriers and enums whose names and signatures are self-describing: a `StableId Id { get; }` needs no prose.

The areas worth caring about are the ones you call directly. Those are listed first on the [reference index](index.md).

