# 1. Install and run the demo

Import the package, press Play on the shipped scene, and watch a full battle resolve. Then
run one seed twice and see for yourself that nothing about the battle moved.

---

## Install

1. Import TempoForge into a Unity **2022.3 LTS or newer** project.
2. Open `Assets/TempoForge/Samples/RuntimeDemo/TempoForgeDemo.unity` and press **Play**.

There is no third step. Everything imports under `Assets/TempoForge/`, no third-party package
comes with it, and the render pipeline does not matter -- built-in, URP and HDRP all work with
no pipeline package added.

Three things you might expect to set up and do not:

- **No shader or material step.** Every panel, bar, plate and pip is drawn procedurally by one
  shader that ships inside a `Resources` folder, so it survives build shader stripping.
- **No font asset.** With no font assigned on the skin, text falls back to Unity's built-in
  `LegacyRuntime.ttf`.
- **Six drawn characters are included, and you may ship them.** They live under
  `Samples/Characters/`, the demo uses them, and they are licensed with the package for use in your
  own commercial projects &mdash; not look-but-do-not-touch demo art. The two archetypes without a
  drawing fall back to a generated role glyph, which is what an unfilled slot looks like. To swap in
  your own, see [Use your own character art](../how-to/use-your-own-art.md).

## Run the demo scene

Play compiles the two starter catalogs and starts the first scenario, **Tutorial Duel**, on
seed `12345`. You do not have to press anything: every combatant in the starter content is
AI-controlled, so the battle runs itself to a result.

| On screen | Where | Fed from |
| --- | --- | --- |
| Plate over each token: name, health bar, shield bar while a shield holds, one pip per status | Above the stage tokens | the snapshot |
| Roster, one row per combatant | Top left | the snapshot |
| Turn-order strip | Top centre | the snapshot's decision entries |
| Battle log | Bottom left | the event stream |
| Scenario picker, seed field, playback row, status line | Top right | your driver |
| Result banner | Centre, at the end | the terminal result |

The skill tray along the bottom stays hidden for the whole battle. It appears only while a
**human**-controlled actor has a decision pending, and no shipped scenario has one;
[tutorial 4](take-player-input.md) adds that.

!!! note "The scene has no Event System"
    The shipped scene holds a camera, the driver and the interface, and nothing else. uGUI needs
    an `EventSystem` in the scene before any element receives pointer input, so add
    **GameObject ▸ UI ▸ Event System** before you click the on-screen controls. The keyboard
    shortcuts below work without one.

The picker spans eight authored scenarios: Tutorial Duel, Mirror Brawl, Boss and Minions,
Healer Check, DOT Pressure, Reaction Showcase, Formation Showcase, and ATB Rush, which runs
the ATB scheduler out of its own catalog. `<` and `>` move the selection only -- the running
battle continues until you press **Start**.

## Prove determinism

Every other page rests on this property, so watch it happen once.

=== "From the Inspector"

    1. Select the **TempoForgeDemo** object and note its **Seed** field (`12345`).
    2. Press Play, let the battle finish, and read the last log lines and the result.
    3. Stop and press Play again, touching nothing. The same events resolve in the same order
       with the same numbers, and the same side wins.
    4. Change **Seed** by one and press Play. The battle diverges.

=== "From the transport bar"

    1. Add an Event System, press Play, then type a number into **Seed**.
    2. Press **Start**. A fresh engine runs the selected scenario on that seed.
    3. Press **Start** again with the same number. It resolves identically.

    Text the field cannot read as an unsigned integer is ignored, and the current seed is kept.

A battle is a function of its inputs: the encounter, its scheduler, its formation, the seed,
and the commands submitted. Hold those and the engine reproduces the same state hash, the same
event-chain hash and the same result every time.

!!! tip "Compare hashes, not log lines"
    The demo displays no hashes. Open the same scenario and seed in
    **Tools ▸ TempoForge ▸ Battle Workbench**, which prints the event-chain hash beside its
    event log -- that is the value which must not move. See
    [Step a battle in the Workbench](../how-to/balance-with-the-workbench.md).

!!! warning "Content is an input too"
    Edit a stat, a skill or an encounter and the same seed gives a different battle. That is not
    a determinism failure, it is a different set of inputs.
    [Determinism](../explanation/determinism.md) lists everything the tuple covers.

## What the transport controls change

At 1x, one second of presentation time becomes 30 simulation ticks, handed to the engine as an
integer tick count. The controls change how that conversion happens and nothing else.

| Control | Key | What it changes |
| --- | --- | --- |
| **Pause** | `Space` | The driver stops requesting ticks. Visual beats already queued keep playing out. |
| **Speed** | `Tab` | Cycles 0.5x, 1x, 2x, 4x. Presentation time converts to ticks that much faster, and queued beats play at that rate. |
| **Skip** | `Enter` | Finishes every queued visual beat now. No simulation value is touched. |
| `<` `>` | -- | Selects the previous or next scenario, wrapping at both ends. |
| **Start** | -- | Tears down the current battle and creates a fresh engine for the selected scenario on the seed in the field. |

None of that can change a result. Advancing seven ticks at a time and advancing seven hundred
produce the same hashes, so your frame rate and your speed setting are invisible to the
simulation. The shipped test suite asserts this directly: it runs the demo driver and a
Workbench session over the same tuple at different tick batch sizes and requires both hashes
to match.

The keyboard shortcuts need the legacy input backend (**Project Settings ▸ Player ▸ Active
Input Handling: Input Manager** or **Both**). Without it the buttons still work.

!!! note "Human decisions are the exception"
    Once a player chooses, the tick their command lands on is itself an input, so a faster or
    slower clock could move it. Authoring the scheduler's input pause policy as `PauseOnInput`
    removes that risk -- see [Schedulers and tempo](../explanation/schedulers.md).

For a shipping build, tick **Hide Transport Controls** on the `BattleUiRoot` component. The
region is then not built at all, so the picker and playback row cost nothing.

## Next

- **[2. Run a battle from your own code](run-a-battle-from-code.md)** -- compile a catalog,
  create an engine from an encounter and a seed, and pump it yourself.
- **[Determinism](../explanation/determinism.md)** -- what reproduces a battle exactly, and
  which of your own choices can break it.
- **[Troubleshooting](../how-to/troubleshooting.md#the-interface-looks-flat)** -- if the
  interface renders as flat rectangles with no shading.
