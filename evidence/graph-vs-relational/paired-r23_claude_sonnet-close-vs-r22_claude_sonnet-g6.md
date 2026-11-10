# Paired delta: A vs B

- A: `r23/claude/sonnet-close`
- B: `r22/claude/sonnet-g6`

Each run is compared with its own baseline per (case, replicate); outcome is +1 when every judgment prefers the candidate, −1 when every judgment prefers the baseline, 0 otherwise.

| Pairs | A better | B better | Equal | A W/T/L | B W/T/L | Composite Δ-of-Δ [95% CI] |
|---|---|---|---|---|---|---|
| 25 | 4 | 2 | 19 | 18/6/1 | 16/8/1 | +3.2 [+1.2, +5.7] |

| Arm | Composite | Factual errors / judgment |
|---|---|---|
| A candidate | 78.9 | 0.08 |
| A baseline | 73.7 | 0.09 |
| B candidate | 76.2 | 0.12 |
| B baseline | 74.2 | 0.09 |

| Case | Pairs | A better | B better | Equal | Δ-of-Δ |
|---|---|---|---|---|---|
| pr5 | 5 | 1 | 1 | 3 | +7.9 |
| pr8 | 5 | 0 | 0 | 5 | +2.4 |
| pr9 | 5 | 1 | 0 | 4 | +1.3 |
| pr11 | 5 | 0 | 1 | 4 | +0.7 |
| pr12 | 5 | 2 | 0 | 3 | +3.8 |

Δ-of-Δ = (A cand − A base) − (B cand − B base); interval is a case bootstrap (5000 resamples, seed 7).
