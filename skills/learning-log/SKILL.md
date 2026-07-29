---
name: learning-log
description: Capture what a run actually taught — specifically the gap between what was predicted and what happened. Use after a simulation, experiment, or probe completes, when the user reports a surprising result, or when they ask to record, log, or save what they learned. Also use when the user asks what they have learned about a topic so far, to read the log back.
---

# Learning log

The durable output of a probe is not the number. It's the gap between the
prediction and the result. That gap is what transfers to the next problem; the
number does not.

Log the gap. Skip everything else.

## Where

`log/YYYY-MM.md` in the project root, appended newest-last. One month per file.
Create the file if it isn't there.

## Format

Keep entries to four lines. A long entry won't get written and won't get reread.

```markdown
## <YYYY-MM-DD> — <topic, a few words>
- **Did:** <the run, one line, with the setup that matters>
- **Predicted:** <what was expected>
- **Got:** <what happened, with the number>
- **Gap:** <why they differed — or "as predicted" if no gap>
```

Add a fifth line only when it earns its place:

```markdown
- **Reusable:** <the rule of thumb this produced>
```

`Reusable` is the whole point of the exercise. It's the line you'll actually
come back for. Write it whenever the run produced something you'd apply to a
different problem — a scaling law, a gotcha, a threshold, a default that turned
out to be wrong.

## Rules

- **Numbers with units.** "Field was low" is worthless in a month. "Peak E was
  0.8 V/m at 45 mm, expected ~3" is a data point.
- **"As predicted" is a real entry.** A confirmed prediction is evidence your
  model is calibrating. Log it in one line and move on.
- **Log failures too.** "Wouldn't converge below 2 mm mesh" saves a future
  afternoon.
- **Don't log what the code already records.** Parameter values live in the
  input file. Log the *interpretation*.

## Reading it back

When asked what's been learned about a topic, grep the log rather than
summarizing from memory, and lead with the `Reusable` lines — those are the
findings, and they're the ones that compound.

Every few weeks, when entries accumulate: promote repeated `Reusable` lines into
a `log/rules-of-thumb.md` and note the entries they came from. A rule that
showed up three times has earned a permanent home.
