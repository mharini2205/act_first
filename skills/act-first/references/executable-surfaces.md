# Executable surfaces by concept type

The surface is the smallest runnable thing that produces observable output. This
is the lookup table. Match the concept to a row, then make it specific to what's
actually on the user's machine.

## General

| You encountered | Fastest surface | Works if |
|---|---|---|
| A software tool | Its own bundled example/demo, run **unmodified** | The vendor's example output appears |
| A physics or math relation | 10-line script or spreadsheet that plots it over a realistic range | The curve has the shape you expected |
| An algorithm | A library implementation on toy input, before reading how it works | Output on a case you can verify by hand |
| An API or service | The quickstart request with your own key | A 200 and a body you recognize |
| A file format | Open one real example and dump its structure | You can name what each field holds |
| A standard or regulation | Find the single governing number, check your case against it | You have "we're at X, limit is Y" |
| A statistical method | Run it on data where you know the answer, then on your real data | The known case comes out right |
| A hardware spec | Back-of-envelope calc in the spec's own units | A number you can compare to the datasheet |
| A dataset | Load it, print shape, plot one column | You know its size, units, and range |

## Simulation software (SimNIBS, COMSOL, ANSYS, FEniCS, etc.)

The bundled example is almost always the right surface. These packages ship
working models precisely so you can confirm the install.

1. **Run the shipped example unmodified.** Do not touch a parameter. This
   separates "I don't understand the physics" from "my install is broken" —
   the single most expensive confusion to leave unresolved.
2. **Find the smallest geometry.** Coarse mesh, 2D if available, axisymmetric if
   available. Solve time under two minutes or you can't iterate.
3. **Change one number and re-run.** Now the parameter has meaning, because you
   watched it move something.
4. **Only then** open the theory manual, with the specific question your run
   produced.

Look for examples in: an `examples/`, `simnibs_examples/`, `Applications/`, or
`tutorials/` directory inside the install root; the docs site's "getting
started"; a `*.mph`, `*.msh`, `*.geo`, or project file shipped with the package.

If the mesh/solve is too slow to iterate: drop to the analytic limit case. A
current loop's on-axis field has a closed form. A point source in a homogeneous
half-space has a closed form. Those get you the parameter *relationships* in
minutes while the real solver runs in the background.

## A research paper

Do not read it front to back. That is the slow path.

| Goal | Surface |
|---|---|
| Understand the method | Reproduce their simplest figure with **fake data** of the right shape |
| Check if it applies to you | Extract their key equation, plug in *your* numbers, see if the answer is sane |
| Evaluate the claim | Find the one measurement the claim rests on, ask what would falsify it |
| Reuse their model | Find whether they released code; run it before reading the paper |

Reading order that works: Figures → Methods → Results → Discussion → Intro.
The intro is written to justify the work, not to teach you the work.

## A patent or claim

The surface is a mapping exercise, not reading.

1. Take **claim 1** only. Independent claims are what bind.
2. Split it into its elements — one line per limitation.
3. Put your own device next to it, element by element.
4. The first element you *don't* have is your answer. Stop there.

Dependent claims only matter once claim 1 reads on you.

## A biological mechanism

Ask "what measurement would show this?" The assay is the surface. If you can
name the readout, the units, and the expected effect size, you understand the
mechanism operationally — which is more than a paragraph of prose gives you.

## A codebase you inherited

| Goal | Surface |
|---|---|
| Understand what it does | Run its test suite; read the test names |
| Understand a function | Call it with a trivial input, print the result |
| Understand the data flow | Add one print/log at the boundary and run the real path |
| Evaluate whether to use it | Build it from clean checkout, time how long that took |

Reading source top-to-bottom is the slowest available option. Execution traces
the path for you.

## When nothing installs

The escalation ladder — each rung is cruder and faster, and every rung still
teaches the parameter relationships:

1. Full simulation
2. Coarse / 2D / symmetric simulation
3. Library or online calculator
4. Closed-form analytic approximation in a script
5. Spreadsheet with the governing equation
6. Dimensional analysis — which way does the answer scale?
7. Order-of-magnitude estimate on paper

Rung 7 done today beats rung 1 done next week. Drop rungs until something runs
*now*, then climb back up.
