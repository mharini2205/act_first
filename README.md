# act-first

A Claude Code plugin that answers one question, fast:

> **I just ran into this thing. What do I do in the next 30 minutes?**

Not "here's what it is." Not "here are five papers." The smallest thing you can
actually run, the knobs to turn once it runs, and what to watch.

---

## Why

There are two ways to learn an unfamiliar system.

**The slow one:** read what it is, find who's used it, watch the talks, skim the
papers, build a vocabulary. Three days later you can discuss it and you still
can't predict what it will do.

**The fast one:** install it, run the example that shipped with it, change a
number, watch what moves. Twenty minutes later you have a wrong mental model,
which is far more useful than no mental model — because now you have a specific
question, and *now* the reading pays off.

This plugin makes the fast one the default. It refuses to lead with background.
Background is something you earn by getting stuck on something specific.

---

## Install

```bash
git clone https://github.com/mharini2205/act-first.git ~/.claude/plugins/act-first
```

Or from inside Claude Code:

```
/plugin install mharini2205/act-first
```

Then restart Claude Code. Three commands appear: `/act`, `/unstick`, `/log`.

The skills also fire on their own when you describe a task that fits — you don't
have to remember to invoke them.

---

## Use

```bash
/act SimNIBS TMS coil parameters
```

```bash
/unstick simnibs_python throws ModuleNotFoundError on charm
```

```bash
/log doubled dIdt, expected 2x E-field, got 2.05x
```

---

## What you get back

Every answer comes in the same shape, short enough to act on immediately:

```
FIRST CONTACT — <minutes>

Surface:  <the specific runnable thing>
Do this:  <exact commands, copy-pasteable>
Works if: <the observable output that means it ran>

THEN PROBE

  1. <knob> → predict: <direction + magnitude> → watch: <output>
  2. <knob> → predict: <...>                   → watch: <...>
  3. <knob> → predict: <...>                   → watch: <...>

READ ONLY IF
  <the specific question that would block you> → <specific source, section>

LOG
  <the one sentence worth keeping>
```

---

## Worked example

Real output shape for `/act SimNIBS TMS coil parameters`, using the example that
actually ships with SimNIBS 4.6:

```
FIRST CONTACT — 15 min

Surface:  simnibs/examples/simulations/TMS.py — the bundled Magstim 70mm
          figure-8 example. Run it unmodified first.
Do this:  cd to a folder containing your m2m_ernie/
          simnibs_python <install>/simnibs_env/Lib/site-packages/simnibs/
            examples/simulations/TMS.py
Works if: a tms_simu/ directory appears with a .msh you can open in Gmsh

THEN PROBE

  1. pos.distance  4 → 8 mm   → predict: peak E drops well over half,
                                near-field falls faster than 1/r²
                              → watch: max normE in the output summary
  2. dIdt  1e6 → 2e6 A/s      → predict: exactly 2× — it's linear
                              → watch: max normE     [sanity anchor]
  3. fnamecoil  Fig8 → circular
                              → predict: lower peak, much wider spread
                              → watch: focality, not just the peak

READ ONLY IF
  Knob 2 isn't exactly 2× → SimNIBS docs, "Field calculation" — check whether
  you're reading dA/dt or the full E including the ohmic term.

LOG
  How much peak E you lose per mm of coil-to-scalp distance. You'll reuse
  that number constantly.
```

Note knob 2: the sanity anchor. If doubling a linear driver doesn't double the
output, something in the setup is wrong and knobs 1 and 3 are meaningless. Check
the anchor before trusting anything else.

---

## What's inside

| | |
|---|---|
| `skills/act-first/` | The main skill. Picks the executable surface, designs the probes. |
| `skills/act-first/references/executable-surfaces.md` | Concept type → fastest runnable thing. Covers simulation packages, papers, patents, codebases, specs. |
| `skills/act-first/references/probe-design.md` | Prediction-first method, wide brackets, sanity anchors, what to do when a prediction is badly wrong. |
| `skills/unstick/` | Time-boxed escalation when nothing runs, plus the downgrade ladder. |
| `skills/learning-log/` | Captures the gap between prediction and result — the part that transfers. |
| `agents/surface-scout.md` | Subagent that verifies entry points against your real filesystem instead of guessing paths. |
| `commands/` | `/act`, `/unstick`, `/log` |

---

## The ideas it's built on

**Every concept has an executable surface.** A tool has a bundled demo. An
equation has a ten-line plot. A paper has a figure you can fake-data your way
into. A patent has claim 1, which you map element-by-element onto your own
device. A regulation has one governing number. Finding that surface fast is the
whole skill.

**A run without a prediction teaches almost nothing.** The number isn't the
lesson — the gap between what you expected and what happened is the lesson.
That's why every probe carries a prediction written *before* the run.

**Bracket wide, not narrow.** 0.5× and 2×, not ±5%. Small perturbations vanish
into numerical noise. Wide brackets reveal the shape of the relationship, and
the shape is what transfers to the next problem.

**Always include a sanity anchor.** One run whose answer you already know. Zero
in, zero out. If the anchor fails, stop — everything else from that setup is
uninterpretable.

**A broken install is not a reason to stop learning.** Drop down the ladder —
coarse mesh, library, closed form, spreadsheet, dimensional analysis, paper
estimate — until something runs *now*. Rung 7 today beats rung 1 next week, and
the cruder rung usually preserves the parameter relationships you were after.

**Reading is triggered, not scheduled.** You read when you have a question a run
produced. Earned background is worth ten times unearned background.

---

## License

MIT
