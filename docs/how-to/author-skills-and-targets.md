# Skills, targets and timing

A skill is what a combatant does, a target asset is what it may be aimed at, and timing is how
long it occupies the actor. Author the target first, then the skill that references it.

## Target contracts

A **Target** asset (**Assets > Create > TempoForge > Target**) names a resolver implementation,
its contract version, and the properties that implementation requires. It resolves nothing
itself: it declares a *shape*, and the engine performs exact resolution when a command arrives.

| Implementation | Candidates | Requested IDs |
| --- | --- | --- |
| `target.self.v1` | the actor | 0 -- automatic |
| `target.one-ally.v1` | one living ally, actor included | exactly 1 |
| `target.one-other-ally.v1` | one living ally, actor excluded | exactly 1 |
| `target.one-enemy.v1` | one living enemy | exactly 1 |
| `target.all-allies.v1`, `target.all-enemies.v1`, `target.all-combatants.v1` | every living ally, enemy or combatant | 0 -- automatic |
| `target.random-ally.v1`, `target.random-enemy.v1`, `target.random-all.v1` | living allies, enemies or combatants, drawn at random | 0 -- automatic |
| `target.formation-row.v1`, `target.formation-side.v1` | living combatants in one authored row or side | 0 -- automatic |

Every shipped contract accepts living, targetable combatants only.

### Required properties

Two families carry a property, and compiling the catalog fails without it:

| Implementation | Key | Value |
| --- | --- | --- |
| the three random targets | `target-count` | how many candidates to draw |
| `formation-row`, `formation-side` | `formation-id` | the stable ID of the row or side |

A shipped target rejects any other key. A random target whose `target-count` exceeds the number
of living candidates refuses the command rather than drawing fewer, and its draw takes numbers
from the battle RNG without replacement, which is why it replays exactly.

### What the interface reads

`DecisionShapeCompiler.Compile(snapshot, catalog)` projects the pending decision into
`DecisionOptions`, and each offered skill carries a `TargetShape`:

| Field | Meaning |
| --- | --- |
| `Relation` | `Self`, `Ally`, `Enemy` or `Any` |
| `LifeState` | which life state may be picked |
| `MinimumTargets`, `MaximumTargets` | how many IDs the command must carry |
| `MaximumResolvedTargets` | the ceiling the engine may resolve to |
| `ActorMayAppear` | whether the actor is a legal pick |
| `AutomaticSelection` | true when zero requested IDs means the engine selects |

Skills on cooldown, unaffordable skills, and skills restricted by a status the actor holds are
omitted, so a tray bound to this offers only legal choices. It is display only: it never
re-resolves targets and never touches the engine.

## Skills

A **Skill** asset (**Assets > Create > TempoForge > Skill**) references one Target, lists up to
64 effect entries with unique entry IDs, and carries the tags that statuses restrict against.

`MinimumRequestedTargets` and `MaximumRequestedTargets` record how many IDs a command for this
skill carries: both 0 for a target that selects automatically, both 1 for a single pick. The
compiler does not cross-check them against the target's own contract, so keep the two in step.

`TargetLockPolicy` has one value, `LockAtAcceptance`. Targets are fixed when the command is
accepted, not when the action resolves. That is what makes a long cast meaningful, and it is why
the next field exists.

### When a locked target stops being valid

`InvalidTargetPolicy` decides what happens when a locked target is no longer a candidate by the
time effects run:

| Value | Consequence |
| --- | --- |
| `SkipInvalid` | the target is dropped and the rest of the action resolves |
| `CancelAction` | the whole action is cancelled |
| `RetargetStable` | the lowest-ordered unlocked candidate replaces it, and a retarget event is emitted |

`SkipInvalid` is the quiet choice. `RetargetStable` is what a single-target attack wants if you
would rather it hit something than nothing.

## Cast and recovery

`CastTicks` and `RecoveryTicks` are the two fields you will change most while balancing.

- **`CastTicks: 0`** -- the action resolves in the tick it was accepted.
- **`CastTicks` above 0** -- the actor holds a cast that completes that many ticks later, and
  cannot accept another command until it does.
- **`RecoveryTicks`** -- how long the actor stays occupied after resolving, before the scheduler
  offers it another opportunity. It must be at least 1; the compiler rejects 0.

`Interruptible` only matters when `CastTicks` is above 0, because a skill without a cast has no
cast state to interrupt. Interrupting is the job of a skill carrying the built-in interrupt
effect, and such a skill is refused at submission unless every locked target is mid-cast
(`cast.not-active`) in an interruptible cast (`cast.not-interruptible`).

`InterruptRefundPolicy` decides what the interrupted actor keeps: `None` leaves the resources
paid at acceptance spent, `Full` restores them, clamped to the resource maximum.

!!! note "TimingResolutionKind"
    `InterruptFirstLockedCast` interrupts the single locked target as part of resolving the
    action. The compiler requires `CastTicks: 0` and exactly one requested target. Set it only on
    a skill that also carries the interrupt effect, since that effect is what drives the
    submission-time check for a live interruptible cast.

## Cooldowns and costs

`CooldownAmount: 0` means no cooldown. Above 0, two fields decide when the cooldown starts and
what it counts down:

| Field | Value | Consequence |
| --- | --- | --- |
| `CooldownStartPolicy` | `Queue` | starts when the command is accepted |
| `CooldownStartPolicy` | `Resolve` | starts when the action resolves |
| `CooldownClockKind` | `ElapsedTicks` | counts battle ticks, whoever is acting |
| `CooldownClockKind` | `OwnerOpportunities` | counts the owner's own acting opportunities |

With a long cast, `Queue` blocks a second use during the wind-up and `Resolve` leaves the skill
ready again if the cast is interrupted. `OwnerOpportunities` keeps "every third turn" meaning the
same thing for a fast and a slow combatant; `ElapsedTicks` does not.

Costs are resource-and-amount pairs: at most 16 per skill, each amount above 0, each resource
named once. `ActionCostPaymentPolicy` has one value, `Acceptance` -- the amounts leave the pool
when the command is accepted, before any cast completes. Giving them back is the refund policy's
job.

### Why a command was refused

The engine checks a submitted skill command in a fixed order and returns the first failure:
`command.skill.not-granted` (the combatant was never granted it), `command.skill.restricted` (a
status restricts one of its tags), `command.skill.cooldown`, `command.cost.unpayable`, then
`target.request.invalid` (the requested IDs do not fit the contract). An actor that is already
mid-action fails earlier still, with `command.actor.busy`.

## Next

- **[Combatants, teams and encounters](author-combatants-and-encounters.md)** -- grant these
  skills to someone and assemble a runnable battle.
- **[Schedulers and tempo](../explanation/schedulers.md)** -- how cast and recovery ticks turn
  into acting order.
- **[Take a decision from the player](../tutorials/take-player-input.md)** -- turn a target shape
  into a tray the player can use.
