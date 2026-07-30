# Probe design

Running a model once teaches you a number. Running it three times with a
prediction before each teaches you the system.

## The loop

```
predict → run → compare → explain the gap → next knob
```

The compare step is where learning happens. Skipping the prediction turns the
whole exercise back into passive consumption, just slower and with more clicks.

## Writing a prediction

A prediction must be falsifiable within one run. It needs a **direction** and a
**rough magnitude**.

- Bad: "the field will change"
- Bad: "the field will increase"
- Good: "doubling the coil current roughly doubles peak E — linear, so ~2×"
- Good: "moving the coil 1 cm further out cuts the field at depth by more than
  half, because near-field falls off faster than 1/r²"

Being wrong is not a failure. Being wrong *loudly and specifically* is the
entire point — a vague prediction can't be wrong, so it can't teach.

## Choosing the three knobs

Pick knobs on **independent axes**. Three geometry knobs tell you about one
thing three times. One from each family tells you about three things.

| Family | Examples |
|---|---|
| Geometry | distance, size, spacing, orientation, depth |
| Drive | amplitude, frequency, duration, waveform |
| Material / config | conductivity, permittivity, mesh density, boundary condition, solver tolerance |

Always include at least one knob from the **numerics** side (mesh, tolerance,
timestep). If refining the mesh changes your answer, your answer wasn't
converged and none of the physics knobs meant anything.

## Bracket wide

Use 0.5× and 2×, or an order of magnitude, not ±5%.

Small perturbations sit inside numerical noise and inside your own uncertainty
about the setup. Wide brackets reveal the *shape* of the relationship — linear,
inverse-square, threshold, saturating — and shape is the transferable knowledge.

## Sanity anchors

One of the three runs should be a case where you already know the answer:

- Zero input → zero output
- Doubling a linear driver → doubling the result
- Infinite distance → negligible field
- A published benchmark value for the same configuration
- A symmetric setup → a symmetric result

If the anchor fails, **stop**. Every other result from that setup is
uninterpretable. Fix the anchor first. Most wasted simulation time comes from
trusting a configuration that never passed a sanity check.

## When a prediction is badly wrong

A large gap is a gift. Work it in this order:

1. **Units.** mm vs m, A vs kA, T vs mT, rad vs deg. This is the cause more
   often than anything else combined.
2. **The anchor.** Re-run the case you know. If it now fails, the setup drifted.
3. **Did the knob actually apply?** Confirm the input file changed and the
   solver read it. Silent no-ops are common.
4. **Regime.** Were you assuming a linear/quasi-static/far-field regime the run
   isn't in?
5. **Genuinely new physics.** Only after 1-4. Now the reading is worth it — and
   you have the exact question to read for.

## One at a time

Change one knob per run. Two knobs at once and you cannot attribute the change,
which costs you a third run to disentangle — more expensive than doing it
serially in the first place.

The exception: a deliberate two-factor sweep when you already suspect an
interaction and have a hypothesis about its shape.

## Stop condition

Stop probing when you can **predict the next run correctly**. That's the
operational definition of understanding the parameter, and it's the moment to
move to the next question instead of collecting more runs.
