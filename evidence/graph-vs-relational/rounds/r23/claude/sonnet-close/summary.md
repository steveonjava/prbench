# dev comparison

Outcome: **inconclusive**. Quality: inconclusive. Efficiency: inconclusive.

Writers: 50/50; order judgments: 100/100.

Failed attempts: 4; failed-attempt time: 90s; current pending cleanup: 0.

| Model | System | Samples | Median writer seconds | Median input tokens | Pending cleanup |
|---|---|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 178.04 | 125066 | 0 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 287.77 | 453982 | 0 |

## Gate findings

- claude-sonnet-5-5@medium: median paired writer time did not improve
- claude-sonnet-5-5@medium: median input tokens increased
- Unresolved: c0b33a6dd8787d1b150aa79ffd0a89480e8ea0a256f482de1db5b1e77c174a9b
- Unresolved: 5a16433179c33e4831316aaa47216f3e3b811437842d2120d15d0e8c367dcc35
- Unresolved: f87deecbc06fa899a1cdab6a097e215b63e1bd7388ab3a84b28511e8619495fe
- Unresolved: 6a41775510beaf6c39de698d9365679648b16a38d79d1e1f88e8dbf4299aaf4d
- Unresolved: 9d703fd0ddd3447f85ce7790bcf8998e98708de16860b4e4a0a687fef26056c9
- Unresolved: 290040fc0eff33ca89244f72e69ad8a44de8088e11f092331ef395a3e7c865e9
- Unresolved: 5d6f70e09e9faa3d26eed01d1c2d5af462962fb095c14e3ead1fbc941050867d
- Unresolved: 4841f060f56b908a7446c5508395052beee4c90e546e331c588668545e781d59
- Unresolved: f3e95851d6b9be53ca0150ebea7c8dcacc5927e3a501bc5e3ee3ee18b302c9a3

## Paired performance

Candidate/baseline geometric mean writer ratio: 1.470; case-clustered 95% interval: [1.2251799576015463,1.7763835808024113].

- 5 replicate(s) still represent 5 independent cases in this split.
- Writer timing includes service waits and neutral observation overhead; runtime diagnostics may overlap.
- Diagnostic reuse cannot establish a fresh performance improvement.
- Raw judgments are preserved separately from source-backed adjudications.

## Scores

Composite (0-100) = 35·claims + 15·context + 15·uncertainties + 35·rubric (coverage as fractions of the fact sheet, rubric as mean/2) − 15·factual errors − 7·unsupported claims − 10·traps hit, floored at 0. Each draft is averaged over all its judgments; arm means are means of per-case means, with a 95% bootstrap interval over cases. Components are the primary evidence; the composite is a summary.

| Model | System | Drafts | Composite [95% CI] | Claims | Context | Uncert. | Rubric | Errors | Unsupported | Traps | $/draft | Cost covers | Subagents/draft | Input tokens | Queries |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 73.7 [71.4, 76.1] | 0.96 | 0.38 | 0.73 | 0.74 | 0.09 | 0.11 | 0.00 | 0.690 | reported total | – | 296468 | – |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 78.9 [74.9, 82.9] | 0.96 | 0.45 | 0.60 | 0.88 | 0.08 | 0.03 | 0.00 | 0.407 | reported total | – | 482454 | – |

Mixed-model writers (subagent threads on another model; each model's tokens are priced at its own rate, and Claude's reported cost already covers every model):

| Model | System | Mixed-model drafts | Models used |
|---|---|---:|---|
| claude-sonnet-5-5@medium | tracetoon-candidate | 25/25 | claude-haiku-5-5, claude-sonnet-5-5 |

Paired candidate − other system (same model, case and replicate). Leave one case out = lowest and highest composite Δ when each case in turn is dropped:

| Model | Against | Pairs | Composite Δ [95% CI] | Leave one case out | Factual errors Δ |
|---|---|---:|---|---|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 5.2 [2.5, 8.0] | 4.0 to 6.1 | -0.01 |

Per-case composite Δ (tracetoon-candidate − tracetoon-baseline, same model; mean over paired replicates, pairs in parentheses):

| Case | claude-sonnet-5-5@medium |
|---|---:|
| pr5 | 1.8 (5) |
| pr8 | 5.4 (5) |
| pr9 | 1.4 (5) |
| pr11 | 9.9 (5) |
| pr12 | 7.4 (5) |
| Mean of cases | 5.2 |

Judge reliability (timed-out and transient calls are retried, up to 3 attempts per order judgment; a malformed reply gets one format repair):

| Judge | Failed attempts | Timed out | Transient | Format | Other |
|---|---:|---:|---:|---:|---:|
| claude:claude-opus-5-5@medium | 1 | 0 | 0 | 1 | 0 |
| claude:claude-sonnet-5-5@medium | 3 | 0 | 0 | 3 | 0 |

## Accuracy

Error rate = share of judgments that found at least one factual error (mean of per-case means, 95% bootstrap interval over cases). Error classes are mean factual errors per judgment by kind of statement.

| Model | System | Drafts | Error rate [95% CI] | Errors | Unsupported | Claims | validation | code structure | attribution | motivation | pipeline | other | $/draft |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 0.07 [0.01, 0.14] | 0.09 | 0.11 | 0.96 | 0.07 | 0.00 | 0.00 | 0.01 | 0.00 | 0.01 | 0.690 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 0.08 [0.01, 0.15] | 0.08 | 0.03 | 0.96 | 0.00 | 0.01 | 0.01 | 0.00 | 0.04 | 0.02 | 0.407 |

Candidate arms against baseline arms (any model; shared cases). Deltas are candidate minus baseline over per-case means, with a 95% bootstrap interval over cases. Coverage guard: claim coverage may drop by at most 0.05.

| Candidate | Against baseline | Cases | Error rate Δ [95% CI] | Composite Δ [95% CI] | Claims Δ | Guard | Cost ratio |
|---|---|---:|---|---|---:|---|---:|
| claude-sonnet-5-5@medium | claude-sonnet-5-5@medium | 5 | 0.01 [-0.06, 0.09] | 5.2 [2.5, 8.0] | 0.01 | ok | 1.7× cheaper |

## claude-sonnet-5-5@medium, replicate 1: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-10T02:51:08.110Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 1.10 | 95% | 39% | 74% | 0.00 | 412 | $2.27 |
| tracetoon-candidate | 20 | 0.25 | 0.00 | 0.70 | 95% | 47% | 59% | 0.00 | 440 | $2.03 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.90 | 1.50 | 1.25 | 1.35 | 1.95 | 0.45 | 1.65 | 0.11 | 1.33 | 2.00 |
| tracetoon-candidate | 1.95 | 1.25 | 1.95 | 1.60 | 1.90 | 1.85 | 1.80 | 1.40 | 1.33 | 1.95 |

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

## claude-sonnet-5-5@medium, replicate 2: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-10T02:51:08.259Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.05 | 0.25 | 0.90 | 94% | 30% | 73% | 0.00 | 330 | $4.05 |
| tracetoon-candidate | 20 | 0.10 | 0.05 | 0.45 | 94% | 43% | 62% | 0.00 | 435 | $2.03 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.25 | 1.25 | 1.45 | 1.95 | 0.85 | 1.60 | 0.29 | 1.33 | 1.90 |
| tracetoon-candidate | 1.95 | 1.50 | 2.00 | 1.45 | 2.00 | 1.85 | 1.60 | 1.60 | 1.25 | 1.90 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 100% of 5 pair verdicts agree; Cohen's kappa 1.00.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-10T02:51:08.417Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.10 | 0.25 | 0.75 | 97% | 40% | 77% | 0.00 | 420 | $3.50 |
| tracetoon-candidate | 20 | 0.05 | 0.05 | 0.55 | 98% | 46% | 55% | 0.00 | 365 | $1.87 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.20 | 1.60 | 1.50 | 1.95 | 1.00 | 1.35 | 0.81 | 1.75 | 1.95 |
| tracetoon-candidate | 1.80 | 1.40 | 2.00 | 1.55 | 1.95 | 1.85 | 1.85 | 1.53 | 1.60 | 1.95 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 100% of 5 pair verdicts agree; Cohen's kappa 1.00.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-10T02:51:08.598Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.10 | 0.05 | 1.05 | 95% | 42% | 69% | 0.00 | 437 | $3.97 |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 0.75 | 98% | 43% | 63% | 0.00 | 465 | $2.17 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.55 | 1.55 | 1.75 | 2.00 | 0.85 | 1.30 | 0.57 | 1.50 | 1.95 |
| tracetoon-candidate | 1.80 | 1.35 | 2.00 | 1.25 | 2.00 | 1.90 | 1.85 | 2.00 | 1.50 | 2.00 |

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

## claude-sonnet-5-5@medium, replicate 5: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-10T02:51:08.725Z.

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
| tracetoon-baseline | 20 | 0.20 | 0.00 | 0.90 | 98% | 38% | 72% | 0.00 | 402 | $3.47 |
| tracetoon-candidate | 20 | 0.00 | 0.05 | 0.35 | 97% | 44% | 63% | 0.00 | 448 | $2.07 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.90 | 1.50 | 1.30 | 1.45 | 2.00 | 0.75 | 1.55 | 0.00 | 1.75 | 2.00 |
| tracetoon-candidate | 1.90 | 1.45 | 2.00 | 1.35 | 1.95 | 2.00 | 1.70 | 1.76 | 1.75 | 2.00 |

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

