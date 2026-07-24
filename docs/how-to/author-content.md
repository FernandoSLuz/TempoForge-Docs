# 3. Authoring content

Everything is a ScriptableObject created from **Assets > Create > TempoForge**. Every
asset carries a **Stable Id** that is independent of its filename.

> Renaming an asset is safe. Changing its stable ID is a breaking change: replays and
> saves referencing the old ID will not resolve. Treat stable IDs like database column
> names.

The starter content in `Assets/TempoForge/Samples/StarterContent/` is a worked example of
every asset type below. Reading it is faster than reading this page.

---

## Build order

Author bottom-up. Each layer references the one above it:

```
1. Stat, Resource                  the vocabulary
2. Status, Effect                  what things do
3. Target, Skill                   how they are aimed and used
4. AI Policy, Reaction             how they respond
5. Combatant                       who has them
6. Formation Preset, Team          where they stand and whose side they are on
7. Battle Rules, Scheduler         how the battle runs
8. Encounter                       one runnable battle
9. Battle Content Catalog          everything above, collected
```

Trying to author an Encounter first means creating everything else anyway, in a worse
order.

## The vocabulary layer

**Stat** -- a named number: power, defense, speed, magic, spirit, critical chance,
maximum health. Stats are referenced by formulas, not read directly.

**Resource** -- a spendable pool: energy, focus. Has a maximum, a starting value, and
regeneration behaviour. Skill costs reference resources.

Keep this set small. Every stat you add appears in every combatant and every balance
conversation.

## What things do

**Effect** -- one mechanical outcome, built from primitives: calculate-and-damage,
calculate-and-heal, apply-status, apply-shield, modify-resource, dispel, interrupt,
adjust-scheduler. An effect names a **resolver implementation** and a **contract version**,
plus properties such as potency and the source stat.

**Status** -- a lasting condition: burn, poison, regen, stun, slow, haste, taunt,
vulnerable, fortify, empower. Statuses can:

- tick effects over time,
- modify stats,
- restrict skills carrying particular tags,
- stack, with a defined stacking rule.

The `RestrictedSkillTags` field is how a stun actually prevents actions: it forbids skills
tagged accordingly, rather than special-casing stun in the engine.

## Aiming and using

**Target** -- a targeting contract: team relation (self, ally, enemy, any), allowed life
state, minimum and maximum requested IDs, maximum resolved targets, whether the actor may
appear, and whether zero requested IDs means automatic selection.

The contract is what the interface reads to know what the player may pick. It is a
*shape*, not a resolution -- the engine performs exact resolution itself.

**Skill** -- what a combatant does. Carries a target resolver, a list of effect entries,
tags, and **timing**: cast ticks, recovery ticks, cooldown, and costs.

Timing is the tempo knob. A skill with `CastTicks > 0` is interruptible while winding up;
`RecoveryTicks` is how long the actor is occupied afterwards.

## Responding

**AI Policy** -- how a non-player combatant chooses. Four ship as built-ins: priority
brawler, weighted caster, weighted random, conditional healer. Policies are deterministic
and draw from the battle RNG in a defined order.

**Reaction** -- a triggered response: retaliate, thorns, guard, cleanse, focus gain.
Reactions have trigger conditions and their own effects.

Reaction graphs are **validated for cycles at compile time**, so a reaction that triggers
itself is a compile error rather than an infinite loop at runtime.

## Who and where

**Combatant** -- stat values, resource pools, granted skills, reactions, and an AI policy.

**Formation Preset** -- authored slots in normalized space, each with facing, sorting
layer and order, an approach point, and named anchors that visual effects attach to.
Edit these in **Tools > TempoForge > Formation Editor** rather than by hand.

**Team** -- a side. Groups combatants and maps them onto formation slots.

## How the battle runs

**Battle Rules** -- global rules: victory and defeat conditions, turn limits, stalling
behaviour.

**Scheduler** -- Action Order or ATB, with its own parameters. Remember this is part of
encounter identity, not a runtime toggle.

**Encounter** -- one runnable battle: teams, formation, scheduler, rules. Produces the
`StartRequest` the engine consumes.

## Collecting it

**Battle Content Catalog** -- every definition the compiler should freeze. One catalog per
game is normal; the samples ship two so the ATB showcase can be compiled separately.

```csharp
var result = new BattleContentCompiler().Compile(
    AuthoringCompileRequest.WithBuiltIns(catalog));

if (!result.Succeeded)
{
    for (var i = 0; i < result.Diagnostics.Count; i++)
        Debug.LogError(result.Diagnostics[i].Message);
}
```

`WithBuiltIns` registers the shipped effects, targets, formulas, mechanics, schedulers, and
AI policies. Use the plain request form when you are supplying your own registries.

## Validate before you run

**Tools > TempoForge > Content Validator**.

It reports broken references, missing stable IDs, duplicate IDs, illegal quotas, unresolved
resolver implementations, and reaction cycles -- with navigation to the offending asset.

Run it after every batch of authoring. Compile diagnostics say the same things, but the
validator lets you fix them without entering play mode.

## Migrations

When you change an authored schema, `AuthoringMigrationRegistry` and the migration commands
under **Tools > TempoForge** upgrade existing assets in place, with a precommit validator
that refuses a migration that would not compile.

## Next

- **[Skins and presets](../tutorials/skinning-your-battle.md)** -- the interface.
- **[Workbench and balancing](../how-to/balance-with-the-workbench.md)** -- is any of this fair?
