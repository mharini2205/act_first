---
name: unstick
description: Time-boxed escalation when first contact fails — an install won't complete, a solver errors, a script crashes, or the user has been stuck on setup for a while. Use when the user says something won't run, won't install, won't converge, throws an error they can't place, or when they report being stuck or having burned time on getting something working. The goal is to keep the learning moving even if the tool never runs.
---

# Unstick

A broken install is not a reason to stop learning. It's a reason to drop to a
cruder surface that still teaches the same relationships.

Most time lost to "getting set up" is lost because there was no time limit on
trying. Impose one.

## The clock

| Elapsed on this blocker | Action |
|---|---|
| 0-5 min | Read the actual error text. Not the last line — the first real error. |
| 5-15 min | Search the exact error string. Check versions, paths, permissions. |
| 15-30 min | **Downgrade the surface.** Move down the ladder. Keep learning. |
| 30+ min | The install is now its own separate task. Park it, log it, work the proxy. |

The 15-minute mark is the important one. Past it, continuing to fight the
installer has a worse expected return than switching to an approximation — and
the approximation often turns out to be sufficient for the actual question.

## The downgrade ladder

Drop rungs until something runs *right now*:

1. Full simulation / real tool
2. Coarse mesh, 2D, or symmetric version
3. A different implementation — library, online calculator, another package
4. Closed-form analytic approximation in a short script
5. Spreadsheet with the governing equation
6. Dimensional analysis — how does the answer scale?
7. Order-of-magnitude estimate on paper

State plainly which rung you're proposing and what it does and does not
preserve. A rung-4 approximation usually keeps the parameter *relationships*
(the thing you're trying to learn) while losing absolute accuracy (usually not
the thing you need yet).

## Diagnosing before downgrading

Fast checks, in this order — they catch most of it:

1. **First error, not last.** Stack traces print the least useful line last.
2. **Is it your input or their code?** Run the vendor's unmodified example. If
   that also fails, it's the install; if it works, it's your input. This one
   check splits the search space in half and takes two minutes.
3. **Path problems.** Spaces in paths, backslashes, non-ASCII characters, a
   path longer than 260 characters. On Windows these cause errors that name
   something else entirely.
4. **Version skew.** The tool, its Python, and its dependencies. Print all three.
5. **Permissions / antivirus.** A silent quarantine looks exactly like a
   corrupt download.
6. **Disk and memory.** Solvers fail with confusing messages when either runs out.

## Report it honestly

When downgrading, say exactly this much:

```
BLOCKED ON: <the actual failure, one line>
LIKELY:     <best hypothesis, with confidence>
DOWNGRADE:  rung <n> — <what you'll run instead>
PRESERVES:  <what this still teaches>
LOSES:      <what it doesn't>
PARKED:     <what to come back to, and what would unblock it>
```

Do not present a downgraded result as if it came from the real tool. Carry the
caveat forward into any number you produce from it.
