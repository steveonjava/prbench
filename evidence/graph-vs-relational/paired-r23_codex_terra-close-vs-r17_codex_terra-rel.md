# Paired delta: A vs B

- A: `r23/codex/terra-close`
- B: `r17/codex/terra-rel`

Each run is compared with its own baseline per (case, replicate); outcome is +1 when every judgment prefers the candidate, −1 when every judgment prefers the baseline, 0 otherwise.

| Pairs | A better | B better | Equal | A W/T/L | B W/T/L | Composite Δ-of-Δ [95% CI] |
|---|---|---|---|---|---|---|
| 25 | 4 | 5 | 16 | 12/12/1 | 13/11/1 | +0.7 [-0.4, +1.9] |

| Arm | Composite | Factual errors / judgment |
|---|---|---|
| A candidate | 86.6 | 0.00 |
| A baseline | 83.2 | 0.07 |
| B candidate | 85.0 | 0.00 |
| B baseline | 82.2 | 0.07 |

| Case | Pairs | A better | B better | Equal | Δ-of-Δ |
|---|---|---|---|---|---|
| pr5 | 5 | 1 | 0 | 4 | +2.8 |
| pr8 | 5 | 0 | 0 | 5 | -0.6 |
| pr9 | 5 | 2 | 1 | 2 | +1.5 |
| pr11 | 5 | 0 | 4 | 1 | -0.6 |
| pr12 | 5 | 1 | 0 | 4 | +0.2 |

Δ-of-Δ = (A cand − A base) − (B cand − B base); interval is a case bootstrap (5000 resamples, seed 7).
