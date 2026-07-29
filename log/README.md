# Learning log

Monthly files, `YYYY-MM.md`. Four lines per entry:

```markdown
## 2026-07-29 — TMS coil distance
- **Did:** TMS.py on ernie, pos.distance 4 → 8 mm, Magstim 70mm Fig8
- **Predicted:** peak E drops ~60%
- **Got:** dropped 71%, 0.42 → 0.12 V/m at the C3 gyral crown
- **Gap:** falls faster than I assumed — near-field, not 1/r²
- **Reusable:** ~1 mm of coil-to-scalp costs roughly 8% of peak E in this range
```

The `Gap` line is the point. The `Reusable` line is what you'll come back for.

Numbers with units, always. "Field was low" is worthless in a month.

Log failures too — "wouldn't converge below 2 mm mesh" saves a future afternoon.

When a `Reusable` line shows up for the third time, promote it to
`rules-of-thumb.md`.
