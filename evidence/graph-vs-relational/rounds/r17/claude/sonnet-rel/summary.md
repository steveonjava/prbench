# dev comparison

Outcome: **failed**. Quality: failed. Efficiency: inconclusive.

Writers: 50/50; order judgments: 100/100.

Failed attempts: 6; failed-attempt time: 134s; current pending cleanup: 0.

| Model | System | Samples | Median writer seconds | Median input tokens | Pending cleanup |
|---|---|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 207.68 | 107047 | 0 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 240.57 | 402186 | 0 |

## Gate findings

- claude-sonnet-5-5@medium: claimCoverage regressed against baseline
- claude-sonnet-5-5@medium: contextCoverage regressed against baseline
- No measured claim/context coverage improvement against baseline
- claude-sonnet-5-5@medium: median paired writer time did not improve
- claude-sonnet-5-5@medium: median input tokens increased
- Unresolved: 746173d879176b4c87d8135f06d098d66a4fab9efb7a562f64792d0b8cfd9e10
- Unresolved: cad45bde0ea21c88a6e9ab68f5fcfd47e1459771ce85a6635df43e08865b4e8e
- Unresolved: 235a00dfc5e515663d382955433625f79a9e9f13275e1971f5c98096521846df
- Unresolved: bfea4030b73a00f8b0598c56ef07310024335ac3aeea99b9f5752f3b25a34b6b
- Unresolved: 628d7f368aaeb3988c6e4a8fd6e0028467ba5a111bc8fa56ea00c7fec0b2251c
- Unresolved: 5dcf45fdc5319a83b02d1678e9cbb2cf5513ba17890cafde56ecb27d30f19749
- Unresolved: 4a103a8dd45779e1481b81c5276fe43c0d645739320c8bb76acf664ad04bcc0e
- Unresolved: 8ec465873799357623461bef509c9fc6068c01b58bef7dda3dd7014536588511
- Unresolved: 0d00669db5a3d59a7935f8b444275d3908205f8582770a8e565a73ddca61090f
- Unresolved: 4352ea1848a7e7ec563b5a27fe6961ede2497e031c4e1dacae401d330ef97afc
- Unresolved: d2f7bd3716caa4fab9724d37c0b83a98b1c1f59022d3415e637919e18df2e83a
- Unresolved: 1575284aa6ba387c83a3b71d63a45a9a57563fae981b6bea5242070d263cef86
- Unresolved: c3c47737e2a7430061b9b78ffc295a7f3adb086369476eb12b365a0f72801c48

## Paired performance

Candidate/baseline geometric mean writer ratio: 1.191; case-clustered 95% interval: [0.9837247749220075,1.4255482724574298].

- 5 replicate(s) still represent 5 independent cases in this split.
- Writer timing includes service waits and neutral observation overhead; runtime diagnostics may overlap.
- Diagnostic reuse cannot establish a fresh performance improvement.
- Raw judgments are preserved separately from source-backed adjudications.

## Scores

Composite (0-100) = 35·claims + 15·context + 15·uncertainties + 35·rubric (coverage as fractions of the fact sheet, rubric as mean/2) − 15·factual errors − 7·unsupported claims − 10·traps hit, floored at 0. Each draft is averaged over all its judgments; arm means are means of per-case means, with a 95% bootstrap interval over cases. Components are the primary evidence; the composite is a summary.

| Model | System | Drafts | Composite [95% CI] | Claims | Context | Uncert. | Rubric | Errors | Unsupported | Traps | $/draft | Cost covers | Subagents/draft | Input tokens | Queries |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 75.0 [72.4, 77.7] | 0.97 | 0.40 | 0.73 | 0.78 | 0.15 | 0.11 | 0.04 | 0.781 | reported total | – | 152956 | – |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 73.0 [67.4, 78.1] | 0.94 | 0.38 | 0.52 | 0.86 | 0.14 | 0.09 | 0.10 | 0.412 | reported total | – | 465448 | 1.0 |

Mixed-model writers (subagent threads on another model; each model's tokens are priced at its own rate, and Claude's reported cost already covers every model):

| Model | System | Mixed-model drafts | Models used |
|---|---|---:|---|
| claude-sonnet-5-5@medium | tracetoon-candidate | 25/25 | claude-haiku-5-5, claude-sonnet-5-5 |

Paired candidate − other system (same model, case and replicate). Leave one case out = lowest and highest composite Δ when each case in turn is dropped:

| Model | Against | Pairs | Composite Δ [95% CI] | Leave one case out | Factual errors Δ |
|---|---|---:|---|---|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | -2.1 [-7.8, 3.6] | -4.5 to 0.4 | -0.01 |

Per-case composite Δ (tracetoon-candidate − tracetoon-baseline, same model; mean over paired replicates, pairs in parentheses):

| Case | claude-sonnet-5-5@medium |
|---|---:|
| pr5 | -6.8 (5) |
| pr8 | 7.5 (5) |
| pr9 | -1.6 (5) |
| pr11 | 2.3 (5) |
| pr12 | -11.8 (5) |
| Mean of cases | -2.1 |

Judge reliability (timed-out and transient calls are retried, up to 3 attempts per order judgment; a malformed reply gets one format repair):

| Judge | Failed attempts | Timed out | Transient | Format | Other |
|---|---:|---:|---:|---:|---:|
| claude:claude-opus-5-5@medium | 1 | 0 | 0 | 1 | 0 |
| claude:claude-sonnet-5-5@medium | 5 | 0 | 0 | 5 | 0 |

## Accuracy

Error rate = share of judgments that found at least one factual error (mean of per-case means, 95% bootstrap interval over cases). Error classes are mean factual errors per judgment by kind of statement.

| Model | System | Drafts | Error rate [95% CI] | Errors | Unsupported | Claims | validation | code structure | attribution | motivation | pipeline | other | $/draft |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 0.13 [0.06, 0.20] | 0.15 | 0.11 | 0.97 | 0.10 | 0.01 | 0.03 | 0.00 | 0.00 | 0.01 | 0.781 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 0.12 [0.03, 0.24] | 0.14 | 0.09 | 0.94 | 0.08 | 0.02 | 0.02 | 0.00 | 0.00 | 0.02 | 0.412 |

Candidate arms against baseline arms (any model; shared cases). Deltas are candidate minus baseline over per-case means, with a 95% bootstrap interval over cases. Coverage guard: claim coverage may drop by at most 0.05.

| Candidate | Against baseline | Cases | Error rate Δ [95% CI] | Composite Δ [95% CI] | Claims Δ | Guard | Cost ratio |
|---|---|---:|---|---|---:|---|---:|
| claude-sonnet-5-5@medium | claude-sonnet-5-5@medium | 5 | -0.01 [-0.16, 0.16] | -2.1 [-7.8, 3.6] | -0.03 | ok | 1.9× cheaper |

## claude-sonnet-5-5@medium, replicate 1: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T11:43:18.477Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 2 | 3 | 0 | 0 | 0 | 40% | 1.00 | -0.20 [-1.00, 0.60] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 1 | 1 | 3 | 2 | 0 | 50% | 1.00 | 0.00 [-0.60, 0.60] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 1 | 1 | 3 | 2 | 0 | 50% | 1.00 | 0.00 [-0.60, 0.60] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.05 | 1.30 | 98% | 38% | 75% | 0.00 | 452 | $4.29 |
| tracetoon-candidate | 20 | 0.30 | 0.05 | 0.50 | 97% | 37% | 56% | 0.30 | 410 | $2.07 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.20 | 1.75 | 1.55 | 2.00 | 1.40 | 1.20 | 0.47 | 1.60 | 1.95 |
| tracetoon-candidate | 1.95 | 1.45 | 1.65 | 1.25 | 1.95 | 1.55 | 1.90 | 2.00 | 1.75 | 1.75 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.25.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T11:43:18.572Z.

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
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 3 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.15 | 0.10 | 0.50 | 96% | 36% | 72% | 0.00 | 316 | $3.07 |
| tracetoon-candidate | 20 | 0.10 | 0.05 | 0.70 | 96% | 37% | 57% | 0.00 | 393 | $2.26 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.35 | 1.50 | 1.45 | 1.95 | 1.25 | 1.65 | 0.36 | 1.50 | 1.90 |
| tracetoon-candidate | 1.85 | 1.30 | 1.95 | 1.35 | 2.00 | 1.95 | 1.65 | 1.67 | 1.50 | 1.90 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 20% of 5 pair verdicts agree; Cohen's kappa -0.18.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T11:43:18.669Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 1 | 2 | 2 | 2 | 0 | 33% | 1.00 | -0.20 [-0.80, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 2 | 2 | 1 | 1 | 0 | 50% | 1.00 | 0.00 [-0.80, 0.80] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 1 | 2 | 2 | 2 | 0 | 33% | 1.00 | -0.20 [-0.80, 0.40] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.20 | 0.25 | 0.75 | 97% | 41% | 72% | 0.20 | 391 | $3.64 |
| tracetoon-candidate | 20 | 0.25 | 0.15 | 0.35 | 90% | 43% | 50% | 0.20 | 390 | $1.97 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.35 | 1.65 | 1.30 | 1.95 | 1.70 | 1.55 | 0.20 | 1.00 | 2.00 |
| tracetoon-candidate | 1.90 | 1.35 | 1.75 | 1.45 | 1.95 | 1.50 | 1.80 | 1.90 | 1.67 | 1.80 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.71.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T11:43:18.767Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 2 | 2 | 1 | 1 | 0 | 50% | 1.00 | 0.00 [-0.80, 0.80] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 1 | 4 | 3 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 3 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.10 | 0.65 | 98% | 36% | 73% | 0.00 | 418 | $4.45 |
| tracetoon-candidate | 20 | 0.05 | 0.05 | 0.50 | 94% | 38% | 47% | 0.00 | 390 | $2.01 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.30 | 1.65 | 1.65 | 2.00 | 1.50 | 1.25 | 0.67 | 1.43 | 2.00 |
| tracetoon-candidate | 1.80 | 1.40 | 1.90 | 1.15 | 2.00 | 1.80 | 1.90 | 1.88 | 1.43 | 2.00 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.21.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T11:43:18.867Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.40 | 0.05 | 0.95 | 97% | 49% | 75% | 0.00 | 410 | $4.07 |
| tracetoon-candidate | 20 | 0.00 | 0.15 | 0.70 | 94% | 33% | 52% | 0.00 | 397 | $1.98 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.50 | 1.40 | 1.60 | 1.95 | 1.35 | 1.45 | 0.53 | 1.50 | 2.00 |
| tracetoon-candidate | 1.75 | 1.35 | 1.90 | 1.35 | 2.00 | 1.80 | 1.90 | 1.53 | 1.50 | 1.90 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 20% of 5 pair verdicts agree; Cohen's kappa 0.00.

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

