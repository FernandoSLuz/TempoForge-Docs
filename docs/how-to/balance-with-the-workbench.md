# 5. Workbench and balancing

Two questions this answers: *why did that number come out that way*, and *is this
actually fair across a thousand battles*.

---

## The Workbench

**Tools > TempoForge > Battle Workbench**

Pick a catalog, an encounter, and a seed, then step the battle. You get:

- **The scheduler queue** -- who acts next and why, tick by tick. Under ATB, the charge
  state of every combatant; under Action Order, the computed order.
- **Formula traces** -- every calculation that produced a number, with its inputs. This is
  the answer to "why was that hit 14 and not 12".
- **Event stream** -- in resolution order, with sequence numbers.
- **Snapshot inspection** -- combatants, statuses, shields, resources, cooldowns at any
  tick.
- **Replay capture and playback** -- record a run, replay it, confirm the hashes match.

Step by tick, by event, or by action. Stepping is exact: the workbench drives the same
`AdvanceTicks` your game does, so nothing you see here is a special debug path.

### Reading a formula trace

A damage number is usually a chain: base potency, source stat, target defence, status
modifiers, critical roll, variance. The trace shows each stage and its contribution, so
you can see whether a spike came from a crit, a missing defence stat, or an unintended
status stack.

If a number surprises you, this is the first place to look -- before changing any values.

## Monte Carlo batches

Single battles lie. A hero who wins seed 12345 comfortably may lose 60% of the time.

**Batch runs** execute the same encounter across many seeds and aggregate:

```csharp
using TempoForge.Analysis;

var runner = new BattleBatchRunner();
var result = runner.Run(new BattleBatchRequest(/* content, encounter, seed range */));

// Or use all cores:
var parallel = runner.RunParallel(request, workerCount: 8);
```

Determinism is what makes `RunParallel` safe: each seed is independent and reproducible, so
running them concurrently cannot change any individual outcome.

### Reproducing one outlier

When a batch reports a strange result at a particular seed:

```csharp
SingleBattleReproduction repro = runner.RunSingleForReproduction(request, seed: 90210u);
```

That gives you the full event stream and traces for exactly that battle, which you can then
step in the Workbench.

This is the loop that matters: **batch to find the outlier, reproduce to understand it,
trace to fix it.**

## What to measure

Useful aggregates from a batch:

| Metric | Tells you |
| --- | --- |
| Win rate per team | Raw fairness |
| Battle length distribution | Whether fights drag or end abruptly |
| Terminal result mix | How often draws and stalls happen |
| Damage and healing totals | Whether a role contributes at all |
| Resource starvation frequency | Whether costs are too steep |

A wide length distribution usually means variance is doing too much work; a narrow one with
a lopsided win rate means the matchup is decided by content, not by play.

## Exporting

`BatchExport` writes results for external analysis. Take them to a spreadsheet or a
notebook -- the package deliberately does not try to be a statistics tool.

## Balancing workflow

1. Author or change content.
2. **Content Validator** -- fix everything it reports.
3. Batch run a few hundred seeds for each encounter you care about.
4. Look at win rate and length distribution first. Ignore individual battles.
5. Reproduce the worst outlier; step it in the Workbench; read the traces.
6. Change **one** thing. Re-batch with the same seed range so the comparison is honest.

Changing one variable at a time matters more here than usual, because determinism means
your before and after are directly comparable -- that advantage is wasted if you change
three values at once.

## Stalling

A battle that cannot progress produces the `battle.stalled` **terminal result**, not a
hang. If batches show stalls, something in your content has no path to resolution: mutual
immunity, unpayable costs, or healing that outpaces all damage.

Stalls are data. Treat a nonzero stall rate as a content bug.

## Replays as regression tests

Record a replay of a battle you consider correct, then replay it after changing unrelated
content. If the hashes still match, you did not perturb it. If they diverge, you did --
possibly without meaning to.

The content manifest hash on the snapshot tells you whether a divergence is because the
content changed or because behaviour changed.

## Next

- **[Troubleshooting](../how-to/troubleshooting.md)**
- **[API reference](../reference/index.md)**
