# Documentation coverage

Generated from source alongside the reference itself, so it cannot quietly drift. This page exists because a reference that hides its own gaps is worse than one that admits them.

| Scope | Documented | Total | Coverage |
| --- | --- | --- | --- |
| Public types | 114 | 417 | 27% |
| Public members | 236 | 2219 | 11% |

## By area

| Area | Types | Documented | Coverage |
| --- | --- | --- | --- |
| [Running a battle](running-a-battle.md) | 18 | 0 | 0% |
| [Commands, events and snapshots](commands-events-and-snapshots.md) | 24 | 0 | 0% |
| [Scheduling and tempo](scheduling-and-tempo.md) | 52 | 0 | 0% |
| [Effects and mechanics](effects-and-mechanics.md) | 41 | 6 | 15% |
| [Statuses, targeting and reactions](statuses-targeting-and-reactions.md) | 16 | 0 | 0% |
| [AI policies](ai-policies.md) | 6 | 0 | 0% |
| [Authoring definitions](authoring-definitions.md) | 69 | 2 | 3% |
| [Compiling and validating content](compiling-and-validating-content.md) | 15 | 2 | 13% |
| [Formations](formations.md) | 32 | 2 | 6% |
| [Skinning and appearance](skinning-and-appearance.md) | 21 | 21 | 100% |
| [Interface and widgets](interface-and-widgets.md) | 23 | 23 | 100% |
| [Stage and tokens](stage-and-tokens.md) | 11 | 11 | 100% |
| [Presentation adapters and recipes](presentation-adapters-and-recipes.md) | 17 | 17 | 100% |
| [Replay](replay.md) | 10 | 0 | 0% |
| [Analysis and balancing](analysis-and-balancing.md) | 13 | 13 | 100% |
| [Numerics and determinism](numerics-and-determinism.md) | 16 | 1 | 6% |
| [Editor tools](editor-tools.md) | 23 | 9 | 39% |
| [Other](other.md) | 10 | 7 | 70% |

## How to read this

Low coverage in an area is usually **not** a sign that the types are unclear. Much of the surface is small immutable data carriers and enums whose names and signatures are self-describing: a `StableId Id { get; }` needs no prose.

The areas worth caring about are the ones you call directly. Those are listed first on the [reference index](index.md).

