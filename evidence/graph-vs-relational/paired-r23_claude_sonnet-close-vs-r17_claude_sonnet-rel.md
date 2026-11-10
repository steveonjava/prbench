# Paired delta: A vs B

- A: `r23/claude/sonnet-close`
- B: `r17/claude/sonnet-rel`

Each run is compared with its own baseline per (case, replicate); outcome is +1 when every judgment prefers the candidate, −1 when every judgment prefers the baseline, 0 otherwise.

| Pairs | A better | B better | Equal | A W/T/L | B W/T/L | Composite Δ-of-Δ [95% CI] |
|---|---|---|---|---|---|---|
| 25 | 12 | 1 | 12 | 18/6/1 | 6/17/2 | +7.3 [+1.7, +13.8] |

| Arm | Composite | Factual errors / judgment |
|---|---|---|
| A candidate | 78.9 | 0.08 |
| A baseline | 73.7 | 0.09 |
| B candidate | 73.0 | 0.14 |
| B baseline | 75.0 | 0.15 |

| Case | Pairs | A better | B better | Equal | Δ-of-Δ |
|---|---|---|---|---|---|
| pr5 | 5 | 3 | 0 | 2 | +8.6 |
| pr8 | 5 | 2 | 0 | 3 | -2.1 |
| pr9 | 5 | 2 | 1 | 2 | +3.0 |
| pr11 | 5 | 2 | 0 | 3 | +7.6 |
| pr12 | 5 | 3 | 0 | 2 | +19.2 |

Δ-of-Δ = (A cand − A base) − (B cand − B base); interval is a case bootstrap (5000 resamples, seed 7).
