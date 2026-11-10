# dev comparison

Outcome: **failed**. Quality: failed. Efficiency: inconclusive.

Writers: 50/50; order judgments: 100/100.

Failed attempts: 5; failed-attempt time: 96s; current pending cleanup: 0.

| Model | System | Samples | Median writer seconds | Median input tokens | Pending cleanup |
|---|---|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 207.68 | 107047 | 0 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 276.22 | 467951 | 0 |

## Gate findings

- claude-sonnet-5-5@medium: claimCoverage regressed against baseline
- claude-sonnet-5-5@medium: median paired writer time did not improve
- claude-sonnet-5-5@medium: median input tokens increased
- Unresolved: 864645ea2613891946cae8019e16d300b87a2a3860ee3b645523905d8679c342
- Unresolved: b44ab1032f660c3c687d11d6150f759a1a9a3b61a53248e7b7dec1568672bc3b
- Unresolved: 9a4b43ece7f5a3b19bbdbd4c85df03ad590bb36421f5ee2e750dceba5d8046b5
- Unresolved: c924c37ea9e9bf91afb5d65ac14ff7a8c2c9542ccf1d9b39444796224aaf3a66
- Unresolved: 7bc79c9c85f17abd998f7fe1e6a243411a0e36fd54e76ba82c7b18dcecd498c1
- Unresolved: 2bd9aecc373da1c39b74077c0fc8215d714cdb0ee7abadeb0c800383911cdf77
- Unresolved: dd4e6a18d2a37f9f58287f20d6d803b49e2d769bddccd3a700c3b557f3741d72
- Unresolved: db919799e6a180b8c366d3ae4b36fae2d144d8415113e7b09dfaa8222a677391

## Paired performance

Candidate/baseline geometric mean writer ratio: 1.404; case-clustered 95% interval: [1.1142920841329658,1.7661016262369686].

- 5 replicate(s) still represent 5 independent cases in this split.
- Writer timing includes service waits and neutral observation overhead; runtime diagnostics may overlap.
- Diagnostic reuse cannot establish a fresh performance improvement.
- Raw judgments are preserved separately from source-backed adjudications.

## Scores

Composite (0-100) = 35·claims + 15·context + 15·uncertainties + 35·rubric (coverage as fractions of the fact sheet, rubric as mean/2) − 15·factual errors − 7·unsupported claims − 10·traps hit, floored at 0. Each draft is averaged over all its judgments; arm means are means of per-case means, with a 95% bootstrap interval over cases. Components are the primary evidence; the composite is a summary.

| Model | System | Drafts | Composite [95% CI] | Claims | Context | Uncert. | Rubric | Errors | Unsupported | Traps | $/draft | Cost covers | Subagents/draft | Input tokens | Queries |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 73.5 [70.4, 76.7] | 0.97 | 0.38 | 0.70 | 0.77 | 0.16 | 0.13 | 0.04 | 0.781 | reported total | – | 152956 | – |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 77.9 [72.4, 81.7] | 0.95 | 0.43 | 0.63 | 0.87 | 0.13 | 0.00 | 0.00 | 0.411 | reported total | – | 575067 | 1.5 |

Mixed-model writers (subagent threads on another model; each model's tokens are priced at its own rate, and Claude's reported cost already covers every model):

| Model | System | Mixed-model drafts | Models used |
|---|---|---:|---|
| claude-sonnet-5-5@medium | tracetoon-candidate | 25/25 | claude-haiku-5-5, claude-sonnet-5-5 |

Paired candidate − other system (same model, case and replicate). Leave one case out = lowest and highest composite Δ when each case in turn is dropped:

| Model | Against | Pairs | Composite Δ [95% CI] | Leave one case out | Factual errors Δ |
|---|---|---:|---|---|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 4.4 [-1.4, 10.2] | 2.4 to 6.8 | -0.03 |

Per-case composite Δ (tracetoon-candidate − tracetoon-baseline, same model; mean over paired replicates, pairs in parentheses):

| Case | claude-sonnet-5-5@medium |
|---|---:|
| pr5 | 0.4 (5) |
| pr8 | 11.9 (5) |
| pr9 | -5.3 (5) |
| pr11 | 2.7 (5) |
| pr12 | 12.2 (5) |
| Mean of cases | 4.4 |

Judge reliability (timed-out and transient calls are retried, up to 3 attempts per order judgment; a malformed reply gets one format repair):

| Judge | Failed attempts | Timed out | Transient | Format | Other |
|---|---:|---:|---:|---:|---:|
| claude:claude-sonnet-5-5@medium | 5 | 0 | 0 | 5 | 0 |

## Accuracy

Error rate = share of judgments that found at least one factual error (mean of per-case means, 95% bootstrap interval over cases). Error classes are mean factual errors per judgment by kind of statement.

| Model | System | Drafts | Error rate [95% CI] | Errors | Unsupported | Claims | validation | code structure | attribution | motivation | pipeline | other | $/draft |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 0.16 [0.10, 0.22] | 0.16 | 0.13 | 0.97 | 0.09 | 0.00 | 0.02 | 0.00 | 0.00 | 0.05 | 0.781 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 0.12 [0.01, 0.25] | 0.13 | 0.00 | 0.95 | 0.10 | 0.00 | 0.00 | 0.00 | 0.02 | 0.01 | 0.411 |

Candidate arms against baseline arms (any model; shared cases). Deltas are candidate minus baseline over per-case means, with a 95% bootstrap interval over cases. Coverage guard: claim coverage may drop by at most 0.05.

| Candidate | Against baseline | Cases | Error rate Δ [95% CI] | Composite Δ [95% CI] | Claims Δ | Guard | Cost ratio |
|---|---|---:|---|---|---:|---|---:|
| claude-sonnet-5-5@medium | claude-sonnet-5-5@medium | 5 | -0.04 [-0.15, 0.07] | 4.4 [-1.4, 10.2] | -0.02 | ok | 1.9× cheaper |

## claude-sonnet-5-5@medium, replicate 1: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T13:20:12.930Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 1.25 | 97% | 37% | 71% | 0.00 | 452 | $4.29 |
| tracetoon-candidate | 20 | 0.20 | 0.00 | 0.60 | 98% | 40% | 60% | 0.00 | 433 | $2.04 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.85 | 1.25 | 1.50 | 1.50 | 2.00 | 1.35 | 1.55 | 0.44 | 1.29 | 1.95 |
| tracetoon-candidate | 1.95 | 1.50 | 1.95 | 1.30 | 2.00 | 1.75 | 1.70 | 1.62 | 1.29 | 2.00 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 60% of 5 pair verdicts agree; Cohen's kappa 0.17.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T13:20:13.034Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.05 | 0.20 | 0.40 | 96% | 34% | 74% | 0.00 | 316 | $3.07 |
| tracetoon-candidate | 20 | 0.05 | 0.00 | 0.40 | 93% | 38% | 68% | 0.00 | 382 | $2.00 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.90 | 1.50 | 1.40 | 1.35 | 1.90 | 1.05 | 1.55 | 0.57 | 1.50 | 1.90 |
| tracetoon-candidate | 1.90 | 1.40 | 1.95 | 1.25 | 1.95 | 1.80 | 1.50 | 1.80 | 1.50 | 1.90 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.12.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T13:20:13.141Z.

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
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.25 | 0.15 | 1.05 | 99% | 37% | 70% | 0.20 | 391 | $3.64 |
| tracetoon-candidate | 20 | 0.15 | 0.00 | 0.60 | 94% | 46% | 60% | 0.00 | 435 | $2.09 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.35 | 1.45 | 1.05 | 1.95 | 1.65 | 1.70 | 0.20 | 1.00 | 1.95 |
| tracetoon-candidate | 1.95 | 1.40 | 1.85 | 1.55 | 2.00 | 1.70 | 1.80 | 2.00 | 1.33 | 1.95 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.55.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T13:20:13.244Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.15 | 0.20 | 0.90 | 97% | 36% | 64% | 0.00 | 418 | $4.45 |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 0.95 | 96% | 45% | 61% | 0.00 | 420 | $1.96 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.90 | 1.35 | 1.75 | 1.65 | 2.00 | 1.30 | 1.40 | 0.30 | 1.56 | 2.00 |
| tracetoon-candidate | 1.75 | 1.40 | 1.85 | 1.15 | 2.00 | 1.90 | 1.75 | 1.72 | 1.33 | 2.00 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 60% of 5 pair verdicts agree; Cohen's kappa 0.29.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T13:20:13.348Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.35 | 0.10 | 0.75 | 97% | 48% | 73% | 0.00 | 410 | $4.07 |
| tracetoon-candidate | 20 | 0.25 | 0.00 | 0.45 | 98% | 45% | 67% | 0.00 | 470 | $2.19 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.50 | 1.15 | 1.65 | 1.95 | 1.00 | 1.65 | 0.07 | 1.75 | 2.00 |
| tracetoon-candidate | 2.00 | 1.40 | 2.00 | 1.50 | 1.95 | 1.85 | 1.65 | 1.94 | 1.75 | 2.00 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.00.

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

