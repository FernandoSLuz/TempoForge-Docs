# TempoForge

**Deterministic, replayable turn and tempo battles for Unity.** Action-order or ATB
scheduling, formations, statuses, reactions, AI policies, a Monte Carlo balancing
workbench, and a skinnable battle interface.

> Documentation only. The product source is not in this repository.

---

## Learn it from scratch

Read these in order. Each one ends where the next begins.

| # | Guide | You will be able to |
| --- | --- | --- |
| 1 | **[Getting started](docs/01-getting-started.md)** | Run the demo, prove determinism, start a battle from code |
| 2 | **[Core concepts](docs/02-core-concepts.md)** | Explain the driver, engine, presenter split and why it holds |
| 3 | **[Authoring content](docs/03-authoring-content.md)** | Create combatants, skills, effects, encounters |
| 4 | **[Skins and presets](docs/04-skins-and-presets.md)** | Make the interface look like *your* game |
| 5 | **[Workbench and balancing](docs/05-workbench-and-balancing.md)** | Step a battle, read formula traces, run Monte Carlo |
| 6 | **[Troubleshooting](docs/06-troubleshooting.md)** | Fix the errors you are most likely to hit |
| - | **[API reference](docs/api-reference.md)** | Look up any public type or member |

**If you have 10 minutes:** guide 1, then the "five-minute" section of guide 4.

---

## What it actually does

You author content as assets: stats, resources, skills, effects, statuses, reactions,
AI policies, formations, teams, encounters. A **compiler** freezes that catalog into
immutable content. The **engine** runs a battle from `(content, encounter, seed)` and
emits an event stream plus snapshots.

The same `(encounter, scheduler, formation, seed)` tuple **always** produces the same
state hashes and the same replay -- on every machine and platform. That is not a promise,
it is structural:

- `TempoForge.Simulation` is compiled with `noEngineReferences: true`. It cannot touch a
  `GameObject`, a `Transform`, or `UnityEngine.Random` even by accident.
- Amounts are `Fixed64` and chances are `Chance64`, both integer-backed. No float ever
  reaches a value that feeds a hash.
- The presentation layer receives values and draws them. It never mutates a battle, and
  a purity audit enforces that in tests.

Pause, speed, and skip scale the *visual* clock only. A battle watched at 4x and one
watched paused-and-stepped produce identical results.

## What ships

- Two schedulers out of the box: **Action Order** and **ATB**, with a registry for your
  own.
- Effects, statuses, shields, resources, cooldowns, cast times, interrupts, reactions
  with cycle-safe validation, and pluggable AI policies.
- **Formations**: authored slot layouts projected to any viewport, with an editor.
- **Replays**: a versioned envelope with migrations, so a recorded battle still plays
  back after you ship a patch.
- **Battle Workbench**: step tick by tick, inspect the scheduler queue and every formula
  trace, and run Monte Carlo batches across many seeds.
- **Content Validator**: catches broken references and illegal content before runtime.
- Four shipped interface skins, plus a Skin Browser that turns any of them into an asset
  you own.
- No third-party dependencies. No DRM, no telemetry, no online activation.

## Requirements

- Unity **2022.3 LTS** or newer.
- Built-in render pipeline, URP, or HDRP. No render-pipeline package required.

The interface is drawn with a signed-distance-field shader, so it stays crisp at any
resolution and ships no textures. Glow is drawn in-shader, which is why the package needs
no post-processing stack and cannot conflict with your volumes.

## Support

Open an issue on this repository for documentation problems. For product issues, include
your Unity version and the `(encounter, seed)` pair that reproduces it -- determinism
means that is usually enough to reproduce exactly.
