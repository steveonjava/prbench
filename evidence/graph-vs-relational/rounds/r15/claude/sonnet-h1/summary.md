# dev comparison

Outcome: **failed**. Quality: failed. Efficiency: inconclusive.

Writers: 50/50; order judgments: 100/100.

Failed attempts: 3; failed-attempt time: 92s; current pending cleanup: 0.

| Model | System | Samples | Median writer seconds | Median input tokens | Pending cleanup |
|---|---|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 207.68 | 107047 | 0 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 237.27 | 420374 | 0 |

## Gate findings

- claude-sonnet-5-5@medium: claimCoverage regressed against baseline
- claude-sonnet-5-5@medium: median paired writer time did not improve
- claude-sonnet-5-5@medium: median input tokens increased
- Unresolved: aadedd27d4a0deb22c268fa54e97e158229aa2d52690a3031c72f5a482dd4332
- Unresolved: 930244b17e2edf4f1feb2917af2c4c9f82affb61e067371734102d345479913a
- Unresolved: a60c2ed645f738e291ee4112da86795499fe191a27299f87a8c6f0d143c9a071
- Unresolved: 48466ba09c473efc160f4016d8c9ccb6018bec8cf3977f3a65a063de5d9c4cc4
- Unresolved: 048d566e3a4f1e2f965991799c77a28a30d11b558d63f8f90bdd0b0d395c97b3
- Unresolved: 8316bd63552091f9762c81d3a12c378ddc117c2658110b33c715fe9a92b01e9b
- Unresolved: d683296c9fac6a3a8cd540b39266009b21ec6248b33b41cd4fb34d534a6acf6f

## Paired performance

Candidate/baseline geometric mean writer ratio: 1.158; case-clustered 95% interval: [0.9642185381937322,1.3763796021016845].

- 5 replicate(s) still represent 5 independent cases in this split.
- Writer timing includes service waits and neutral observation overhead; runtime diagnostics may overlap.
- Diagnostic reuse cannot establish a fresh performance improvement.
- Raw judgments are preserved separately from source-backed adjudications.

## Scores

Composite (0-100) = 35·claims + 15·context + 15·uncertainties + 35·rubric (coverage as fractions of the fact sheet, rubric as mean/2) − 15·factual errors − 7·unsupported claims − 10·traps hit, floored at 0. Each draft is averaged over all its judgments; arm means are means of per-case means, with a 95% bootstrap interval over cases. Components are the primary evidence; the composite is a summary.

| Model | System | Drafts | Composite [95% CI] | Claims | Context | Uncert. | Rubric | Errors | Unsupported | Traps | $/draft | Cost covers | Subagents/draft | Input tokens | Queries |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 73.6 [70.8, 76.4] | 0.97 | 0.39 | 0.70 | 0.78 | 0.19 | 0.10 | 0.04 | 0.781 | reported total | – | 152956 | – |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 78.9 [74.6, 83.3] | 0.96 | 0.49 | 0.58 | 0.89 | 0.08 | 0.04 | 0.01 | 0.436 | reported total | – | 501302 | 1.0 |

Mixed-model writers (subagent threads on another model; each model's tokens are priced at its own rate, and Claude's reported cost already covers every model):

| Model | System | Mixed-model drafts | Models used |
|---|---|---:|---|
| claude-sonnet-5-5@medium | tracetoon-candidate | 25/25 | claude-haiku-5-5, claude-sonnet-5-5 |

Paired candidate − other system (same model, case and replicate). Leave one case out = lowest and highest composite Δ when each case in turn is dropped:

| Model | Against | Pairs | Composite Δ [95% CI] | Leave one case out | Factual errors Δ |
|---|---|---:|---|---|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 5.4 [2.6, 8.2] | 4.3 to 6.4 | -0.11 |

Per-case composite Δ (tracetoon-candidate − tracetoon-baseline, same model; mean over paired replicates, pairs in parentheses):

| Case | claude-sonnet-5-5@medium |
|---|---:|
| pr5 | 1.3 (5) |
| pr8 | 4.5 (5) |
| pr9 | 2.6 (5) |
| pr11 | 8.6 (5) |
| pr12 | 9.7 (5) |
| Mean of cases | 5.4 |

Judge reliability (timed-out and transient calls are retried, up to 3 attempts per order judgment; a malformed reply gets one format repair):

| Judge | Failed attempts | Timed out | Transient | Format | Other |
|---|---:|---:|---:|---:|---:|
| claude:claude-sonnet-5-5@medium | 3 | 0 | 0 | 3 | 0 |

## Accuracy

Error rate = share of judgments that found at least one factual error (mean of per-case means, 95% bootstrap interval over cases). Error classes are mean factual errors per judgment by kind of statement.

| Model | System | Drafts | Error rate [95% CI] | Errors | Unsupported | Claims | validation | code structure | attribution | motivation | pipeline | other | $/draft |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 0.16 [0.08, 0.24] | 0.19 | 0.10 | 0.97 | 0.13 | 0.00 | 0.03 | 0.00 | 0.00 | 0.03 | 0.781 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 0.08 [0.02, 0.14] | 0.08 | 0.04 | 0.96 | 0.06 | 0.00 | 0.01 | 0.00 | 0.00 | 0.01 | 0.436 |

Candidate arms against baseline arms (any model; shared cases). Deltas are candidate minus baseline over per-case means, with a 95% bootstrap interval over cases. Coverage guard: claim coverage may drop by at most 0.05.

| Candidate | Against baseline | Cases | Error rate Δ [95% CI] | Composite Δ [95% CI] | Claims Δ | Guard | Cost ratio |
|---|---|---:|---|---|---:|---|---:|
| claude-sonnet-5-5@medium | claude-sonnet-5-5@medium | 5 | -0.08 [-0.17, 0.00] | 5.4 [2.6, 8.2] | -0.01 | ok | 1.8× cheaper |

## claude-sonnet-5-5@medium, replicate 1: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T09:55:42.246Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 1 | 3 | 1 | 1 | 0 | 25% | 0.63 | -0.40 [-1.00, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 1.10 | 97% | 36% | 72% | 0.00 | 452 | $4.29 |
| tracetoon-candidate | 20 | 0.20 | 0.00 | 0.55 | 93% | 49% | 55% | 0.00 | 483 | $2.14 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.90 | 1.25 | 1.40 | 1.40 | 1.95 | 1.45 | 1.75 | 0.43 | 1.60 | 1.95 |
| tracetoon-candidate | 1.90 | 1.25 | 1.95 | 1.60 | 2.00 | 2.00 | 1.55 | 2.00 | 1.60 | 1.80 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.17.

## Warnings

- pr11: tracetoon-baseline: fresh validation evidence partial
- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-baseline: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-baseline: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-baseline: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## claude-sonnet-5-5@medium, replicate 2: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T09:55:42.343Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.10 | 0.15 | 0.50 | 98% | 36% | 68% | 0.00 | 316 | $3.07 |
| tracetoon-candidate | 20 | 0.10 | 0.05 | 0.70 | 95% | 51% | 66% | 0.00 | 450 | $2.05 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.25 | 1.50 | 1.50 | 1.95 | 1.10 | 1.80 | 0.25 | 1.50 | 2.00 |
| tracetoon-candidate | 1.90 | 1.30 | 2.00 | 1.35 | 2.00 | 1.95 | 1.35 | 1.67 | 1.50 | 1.90 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 40% of 5 pair verdicts agree; Cohen's kappa -0.36.

## Warnings

- pr11: tracetoon-baseline: fresh validation evidence partial
- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-baseline: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-baseline: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-baseline: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## claude-sonnet-5-5@medium, replicate 3: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T09:55:42.443Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.25 | 0.10 | 1.05 | 97% | 40% | 68% | 0.20 | 391 | $3.64 |
| tracetoon-candidate | 20 | 0.10 | 0.05 | 0.45 | 97% | 51% | 53% | 0.00 | 493 | $2.21 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.30 | 1.45 | 1.20 | 1.95 | 1.65 | 1.70 | 0.20 | 1.00 | 2.00 |
| tracetoon-candidate | 2.00 | 1.45 | 1.95 | 1.50 | 1.90 | 2.00 | 1.55 | 1.89 | 1.60 | 1.90 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.44.

## Warnings

- pr11: tracetoon-baseline: fresh validation evidence partial
- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-baseline: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-baseline: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-baseline: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## claude-sonnet-5-5@medium, replicate 4: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T09:55:42.551Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 1 | 1 | 3 | 3 | 0 | 50% | 1.00 | 0.00 [-0.60, 0.60] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 3 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.10 | 0.80 | 98% | 35% | 70% | 0.00 | 418 | $4.45 |
| tracetoon-candidate | 20 | 0.00 | 0.10 | 0.85 | 96% | 51% | 58% | 0.05 | 438 | $2.19 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.90 | 1.35 | 1.95 | 1.50 | 2.00 | 1.20 | 1.45 | 0.64 | 1.43 | 2.00 |
| tracetoon-candidate | 1.85 | 1.40 | 1.90 | 1.30 | 1.95 | 2.00 | 1.55 | 1.84 | 1.43 | 2.00 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.17.

## Warnings

- pr11: tracetoon-baseline: fresh validation evidence partial
- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-baseline: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-baseline: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-baseline: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## claude-sonnet-5-5@medium, replicate 5: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T09:55:42.656Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 2 | 3 | 2 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 2 | 3 | 2 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.60 | 0.15 | 0.60 | 96% | 48% | 71% | 0.00 | 410 | $4.07 |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 0.35 | 98% | 46% | 57% | 0.00 | 451 | $2.29 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.50 | 1.45 | 1.60 | 1.95 | 1.30 | 1.45 | 0.57 | 1.75 | 2.00 |
| tracetoon-candidate | 1.95 | 1.50 | 2.00 | 1.35 | 2.00 | 2.00 | 1.85 | 1.90 | 1.75 | 2.00 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.00.

## Warnings

- pr11: tracetoon-baseline: fresh validation evidence partial
- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-baseline: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-baseline: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-baseline: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

