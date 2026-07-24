# 6. Troubleshooting

Ordered by how often each one actually happens.

---

## The interface looks flat

Panels and bars render as plain rectangles with no shading, gradient, or glow.

**Cause:** the skinned-surface shader could not be loaded, so the widgets fell back to flat
surfaces. The console carries one warning saying so.

**Fix:** reimport `Assets/TempoForge/Runtime/Presentation/Resources`. The shader lives in a
`Resources` folder on purpose -- that guarantees it survives build shader stripping without
you adding it to **Always Included Shaders**.

The fallback is intentional: a missing shader degrades to flat colour rather than rendering
magenta.

## Numbers display as 50000 instead of 5

You are calling `ToString()` on a `Fixed64` or `Chance64`.

Those types hold raw scaled integers (`Fixed64.Scale` is 10,000; `Chance64.Scale` is
1,000,000) and their string form feeds canonical encoding, so it must never change. Use:

```csharp
BattleNumberFormat.Amount(value);           // "5.25"
BattleNumberFormat.WholeAmount(value);      // "5"
BattleNumberFormat.AmountRange(min, max);   // "10-14"
BattleNumberFormat.Percent(chance);         // "87.5%"
```

## Compilation fails

`BattleContentCompiler.Compile` returns `Succeeded = false` with diagnostics naming the
exact asset and field. The usual causes:

| Diagnostic area | Usual cause |
| --- | --- |
| Missing or duplicate stable ID | An asset was created without setting its ID, or copied |
| Unresolved resolver implementation | An effect names an implementation or contract version that is not registered |
| Broken reference | A skill references a deleted effect or target |
| Reaction cycle | A reaction chain triggers itself |
| Quota or limit violation | An authored value exceeds a documented cap |

Run **Tools > TempoForge > Content Validator** to see all of them without entering play
mode.

If you supply your own registries, remember `AuthoringCompileRequest.WithBuiltIns(catalog)`
is what registers the shipped implementations. A plain request registers nothing.

## The battle does not advance

Check the outcome your pump returned:

| Outcome | Meaning | What to do |
| --- | --- | --- |
| `NoScheduledWork` | Nothing left to schedule | Usually a content problem: no living actor has an available action |
| `FatalInvariant` | An invariant broke | Stop pumping. Report it with the seed and encounter |
| `Terminal` with `battle.stalled` | Battle cannot resolve | Content bug: mutual immunity, unpayable costs, or healing outpacing damage |

Also confirm you are converting time to an **integer** tick count and that it is not always
rounding to zero -- with a very high frame rate and a low `TicksPerSecond`, `(int)accumulator`
can stay 0 for several frames. That is correct behaviour, but if it is *always* 0 your
multiplier is wrong.

## Clicking a skill does nothing

1. Is there an `EventSystem` in the scene? Without one, no uGUI element receives input.
2. Is a decision actually pending for a **human**-controlled actor? The tray hides itself
   when there is no human decision.
3. Are you subscribed to `CommandChosen` and submitting? The interface deliberately submits
   nothing itself.
4. Is the skill legal right now? The tray only offers shapes the snapshot permits --
   cooldowns, costs, and status restrictions filter it.

## Keyboard shortcuts do not work

Number-key shortcuts require the legacy Input Manager (**Project Settings > Player > Active
Input Handling: Input Manager or Both**). `BattleUiRoot.InputUnavailableMessage` explains
this at runtime.

The interface stays fully usable by pointer without it -- only the shortcuts are gone.

## The same seed gives different results

Something non-deterministic is reaching the battle. The engine itself cannot see Unity's
RNG, so it is on your side:

- Seeding from `UnityEngine.Random`, `DateTime.Now`, or a frame count.
- **Content changed.** The result is a function of content *and* seed. Compare the content
  manifest hash on the snapshot.
- Submitting commands at different ticks. Command sequence and requested tick are part of
  the input; a human decision submitted a frame later is a different battle.

For human-decision scenarios, author the **PauseOnInput** scheduler policy so presentation
speed cannot shift submission ticks. The shipped starter scenarios are all automatic for
this reason.

## A replay will not play back

- **Replay format version** older than the migration chain covers -- `ReplayMigration`
  reports which version it could not upgrade.
- **Content manifest hash mismatch** -- the replay was recorded against different content.
  This is detected, not silently mis-played.
- **Stable ID changed.** Renaming an asset is safe; changing its ID is not.

## Tokens are the wrong size or in the wrong place

Formation slots are authored in normalized space and projected to the viewport. Use
**Tools > TempoForge > Formation Editor** rather than moving transforms, because transforms
are outputs here, not inputs.

For where the stage sits overall, add **TempoForge > Battle Stage Frame** and set its mode
and margins.

## The interface overlaps my own UI

Every interface region is independently placeable from the skin: `Status`, `Timeline`,
`SkillTray`, `Feedback`, `Result`, `Transport`, `Tooltip`. Each has `Visible`, `Anchor`,
`Offset`, `Size`, and `Scale`.

Set `Visible = false` on anything you are replacing -- a hidden region is never created, so
it costs nothing.

**For a shipping build, hide the `Transport` region** or tick **Hide Transport Controls** on
`BattleUiRoot`. Those are development controls.

## Motion feels wrong or makes testers uncomfortable

On the skin's **Motion** group:

- `MotionScale = 0` snaps every transition instantly.
- `ReduceMotion = true` also skips decorative motion. Wire it to a player accessibility
  setting.

## Editor windows are empty after a script reload

Reopen the window. The Workbench and Skin Browser rebuild their state on focus; they hold no
static Unity object references, because those survive a domain reload and then hand out
destroyed objects.

## Getting help

Include:

- Unity version and render pipeline.
- The **encounter ID** and **seed**.
- The console output, including any TempoForge warning.
- Ideally the replay file.

Because battles are deterministic, an encounter plus a seed usually reproduces the problem
exactly.
