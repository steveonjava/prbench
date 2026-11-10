# Paired delta: A vs B

- A: `r23/codex/terra-close2`
- B: `r17/codex/terra-rel`

Each run is compared with its own baseline per (case, replicate); outcome is +1 when every judgment prefers the candidate, −1 when every judgment prefers the baseline, 0 otherwise.

| Pairs | A better | B better | Equal | A W/T/L | B W/T/L | Composite Δ-of-Δ [95% CI] |
|---|---|---|---|---|---|---|
| 25 | 4 | 5 | 16 | 13/10/2 | 13/11/1 | +2.4 [+1.1, +4.0] |

| Arm | Composite | Factual errors / judgment |
|---|---|---|
| A candidate | 87.5 | 0.00 |
| A baseline | 82.3 | 0.04 |
| B candidate | 85.0 | 0.00 |
| B baseline | 82.2 | 0.07 |

| Case | Pairs | A better | B better | Equal | Δ-of-Δ |
|---|---|---|---|---|---|
| pr5 | 5 | 1 | 1 | 3 | +1.9 |
| pr8 | 5 | 2 | 1 | 2 | +0.2 |
| pr9 | 5 | 1 | 2 | 2 | +1.7 |
| pr11 | 5 | 0 | 1 | 4 | +3.4 |
| pr12 | 5 | 0 | 0 | 5 | +4.9 |

Δ-of-Δ = (A cand − A base) − (B cand − B base); interval is a case bootstrap (5000 resamples, seed 7).
