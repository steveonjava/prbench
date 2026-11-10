# Paired delta: A vs B

- A: `r23/codex/terra-close`
- B: `r22/codex/terra-g6`

Each run is compared with its own baseline per (case, replicate); outcome is +1 when every judgment prefers the candidate, −1 when every judgment prefers the baseline, 0 otherwise.

| Pairs | A better | B better | Equal | A W/T/L | B W/T/L | Composite Δ-of-Δ [95% CI] |
|---|---|---|---|---|---|---|
| 25 | 5 | 8 | 12 | 12/12/1 | 14/11/0 | -1.3 [-2.2, -0.3] |

| Arm | Composite | Factual errors / judgment |
|---|---|---|
| A candidate | 86.6 | 0.00 |
| A baseline | 83.2 | 0.07 |
| B candidate | 86.6 | 0.01 |
| B baseline | 81.9 | 0.07 |

| Case | Pairs | A better | B better | Equal | Δ-of-Δ |
|---|---|---|---|---|---|
| pr5 | 5 | 1 | 3 | 1 | -1.5 |
| pr8 | 5 | 0 | 1 | 4 | +0.3 |
| pr9 | 5 | 3 | 1 | 1 | -0.4 |
| pr11 | 5 | 0 | 3 | 2 | -2.3 |
| pr12 | 5 | 1 | 0 | 4 | -2.5 |

Δ-of-Δ = (A cand − A base) − (B cand − B base); interval is a case bootstrap (5000 resamples, seed 7).
