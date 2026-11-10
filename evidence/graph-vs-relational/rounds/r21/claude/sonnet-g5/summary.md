# dev comparison

Outcome: **failed**. Quality: failed. Efficiency: inconclusive.

Writers: 50/50; order judgments: 100/100.

Failed attempts: 7; failed-attempt time: 177s; current pending cleanup: 0.

| Model | System | Samples | Median writer seconds | Median input tokens | Pending cleanup |
|---|---|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 178.04 | 125066 | 0 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 259.07 | 402214 | 0 |

## Gate findings

- claude-sonnet-5-5@medium: claimCoverage regressed against baseline
- claude-sonnet-5-5@medium: median paired writer time did not improve
- claude-sonnet-5-5@medium: median input tokens increased
- Unresolved: d1354f98d72f3ec6874f490bfe7e9d637058824ac5705a69c81e6931f0cdf61a
- Unresolved: 2efb9caaf4f3501e675b02ed2c337937fa5ee13e96944693307fe7b2b0ab4338
- Unresolved: a06156dc461786829eb2b3f3e78604109df98c993ab096d771d6a7f92a2362bc
- Unresolved: b9490b784043635bf438705ccee93ad6af153ff210ad5b14f4ac3305575384ae
- Unresolved: c90a07f0b421c72338a1fc8160c2c064cb4cbb60736437e4ef5c8c4fc21a4c33
- Unresolved: b454f6ba31043306d8c9e2e0bef950100b15bcba4358385172c37c3847275136
- Unresolved: 01c4338dfbfc083eabfad134e9de6c324cafba4ffdce2ca0a6b2bdd470b085f3
- Unresolved: 8d321464cf9f9c52ac137e4cb9b954b2d8ba336cc2988ba7369cb75284e814c1
- Unresolved: 578a9f942231ffb9c3c33e382a2a9804e22d4b84257d006b63bbca4c9f5c91e2
- Unresolved: 89b0546b9d01fccb39c4eff9dba201437d8365e7026e7595346f1063195e1187
- Unresolved: 0a2120a769799d2b063d0d5eaaf9e65ad6b08da5632807fd390473b379bc7e2d

## Paired performance

Candidate/baseline geometric mean writer ratio: 1.358; case-clustered 95% interval: [1.0675301363239338,1.7104313083456202].

- 5 replicate(s) still represent 5 independent cases in this split.
- Writer timing includes service waits and neutral observation overhead; runtime diagnostics may overlap.
- Diagnostic reuse cannot establish a fresh performance improvement.
- Raw judgments are preserved separately from source-backed adjudications.

## Scores

Composite (0-100) = 35·claims + 15·context + 15·uncertainties + 35·rubric (coverage as fractions of the fact sheet, rubric as mean/2) − 15·factual errors − 7·unsupported claims − 10·traps hit, floored at 0. Each draft is averaged over all its judgments; arm means are means of per-case means, with a 95% bootstrap interval over cases. Components are the primary evidence; the composite is a summary.

| Model | System | Drafts | Composite [95% CI] | Claims | Context | Uncert. | Rubric | Errors | Unsupported | Traps | $/draft | Cost covers | Subagents/draft | Input tokens | Queries |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 74.6 [73.0, 76.3] | 0.96 | 0.37 | 0.74 | 0.75 | 0.12 | 0.04 | 0.00 | 0.690 | reported total | – | 296468 | – |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 75.8 [69.1, 81.2] | 0.94 | 0.42 | 0.59 | 0.87 | 0.16 | 0.02 | 0.00 | 0.425 | reported total | – | 488995 | – |

Mixed-model writers (subagent threads on another model; each model's tokens are priced at its own rate, and Claude's reported cost already covers every model):

| Model | System | Mixed-model drafts | Models used |
|---|---|---:|---|
| claude-sonnet-5-5@medium | tracetoon-candidate | 25/25 | claude-haiku-5-5, claude-sonnet-5-5 |

Paired candidate − other system (same model, case and replicate). Leave one case out = lowest and highest composite Δ when each case in turn is dropped:

| Model | Against | Pairs | Composite Δ [95% CI] | Leave one case out | Factual errors Δ |
|---|---|---:|---|---|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 1.2 [-6.7, 7.5] | -1.4 to 5.0 | 0.04 |

Per-case composite Δ (tracetoon-candidate − tracetoon-baseline, same model; mean over paired replicates, pairs in parentheses):

| Case | claude-sonnet-5-5@medium |
|---|---:|
| pr5 | -13.9 (5) |
| pr8 | 6.3 (5) |
| pr9 | 0.4 (5) |
| pr11 | 11.7 (5) |
| pr12 | 1.6 (5) |
| Mean of cases | 1.2 |

Judge reliability (timed-out and transient calls are retried, up to 3 attempts per order judgment; a malformed reply gets one format repair):

| Judge | Failed attempts | Timed out | Transient | Format | Other |
|---|---:|---:|---:|---:|---:|
| claude:claude-opus-5-5@medium | 2 | 0 | 0 | 2 | 0 |
| claude:claude-sonnet-5-5@medium | 5 | 0 | 0 | 5 | 0 |

## Accuracy

Error rate = share of judgments that found at least one factual error (mean of per-case means, 95% bootstrap interval over cases). Error classes are mean factual errors per judgment by kind of statement.

| Model | System | Drafts | Error rate [95% CI] | Errors | Unsupported | Claims | validation | code structure | attribution | motivation | pipeline | other | $/draft |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| claude-sonnet-5-5@medium | tracetoon-baseline | 25 | 0.10 [0.03, 0.18] | 0.12 | 0.04 | 0.96 | 0.07 | 0.00 | 0.00 | 0.00 | 0.03 | 0.02 | 0.690 |
| claude-sonnet-5-5@medium | tracetoon-candidate | 25 | 0.13 [0.00, 0.33] | 0.16 | 0.02 | 0.94 | 0.04 | 0.01 | 0.00 | 0.00 | 0.00 | 0.11 | 0.425 |

Candidate arms against baseline arms (any model; shared cases). Deltas are candidate minus baseline over per-case means, with a 95% bootstrap interval over cases. Coverage guard: claim coverage may drop by at most 0.05.

| Candidate | Against baseline | Cases | Error rate Δ [95% CI] | Composite Δ [95% CI] | Claims Δ | Guard | Cost ratio |
|---|---|---:|---|---|---:|---|---:|
| claude-sonnet-5-5@medium | claude-sonnet-5-5@medium | 5 | 0.03 [-0.15, 0.22] | 1.2 [-6.7, 7.5] | -0.03 | ok | 1.6× cheaper |

## claude-sonnet-5-5@medium, replicate 1: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T22:05:41.946Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.05 | 0.00 | 1.05 | 96% | 38% | 76% | 0.00 | 412 | $2.27 |
| tracetoon-candidate | 20 | 0.15 | 0.00 | 0.60 | 96% | 42% | 62% | 0.00 | 419 | $1.98 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.50 | 1.20 | 1.35 | 1.90 | 0.20 | 1.60 | 0.00 | 1.75 | 2.00 |
| tracetoon-candidate | 1.90 | 1.40 | 2.00 | 1.35 | 2.00 | 1.90 | 1.90 | 1.76 | 1.75 | 1.95 |

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

## claude-sonnet-5-5@medium, replicate 2: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T22:05:42.064Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 3 | 2 | 1 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.20 | 0.15 | 1.05 | 94% | 31% | 75% | 0.00 | 330 | $4.05 |
| tracetoon-candidate | 20 | 0.10 | 0.00 | 0.35 | 95% | 40% | 65% | 0.00 | 416 | $2.07 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.15 | 1.35 | 1.35 | 2.00 | 1.05 | 1.50 | 0.40 | 1.67 | 1.95 |
| tracetoon-candidate | 1.90 | 1.40 | 2.00 | 1.45 | 2.00 | 1.75 | 1.80 | 1.80 | 1.75 | 1.80 |

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

## claude-sonnet-5-5@medium, replicate 3: tracetoon-baseline

# prbench report

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T22:05:42.185Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 2 | 3 | 0 | 0 | 0 | 40% | 1.00 | -0.20 [-1.00, 0.60] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 1 | 3 | 1 | 1 | 0 | 25% | 0.63 | -0.40 [-1.00, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 1 | 3 | 1 | 1 | 0 | 25% | 0.63 | -0.40 [-1.00, 0.40] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 0.60 | 98% | 42% | 76% | 0.00 | 420 | $3.50 |
| tracetoon-candidate | 20 | 0.30 | 0.05 | 0.55 | 92% | 42% | 58% | 0.00 | 401 | $2.02 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.30 | 1.80 | 1.45 | 1.95 | 1.05 | 1.40 | 0.82 | 1.60 | 2.00 |
| tracetoon-candidate | 1.70 | 1.25 | 2.00 | 1.10 | 2.00 | 1.80 | 1.70 | 1.64 | 1.60 | 1.80 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.64.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T22:05:42.302Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 1 | 3 | 1 | 1 | 0 | 25% | 0.63 | -0.40 [-1.00, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.15 | 0.05 | 1.05 | 95% | 38% | 71% | 0.00 | 437 | $3.97 |
| tracetoon-candidate | 20 | 0.05 | 0.05 | 0.55 | 95% | 45% | 54% | 0.00 | 377 | $2.24 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.60 | 1.60 | 1.85 | 2.00 | 0.80 | 1.20 | 0.42 | 1.33 | 2.00 |
| tracetoon-candidate | 1.60 | 1.35 | 1.80 | 1.10 | 2.00 | 1.80 | 1.95 | 1.95 | 1.33 | 2.00 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 20% of 5 pair verdicts agree; Cohen's kappa -0.25.

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

Rubric v6. Judges: claude:claude-opus-5-5@medium, claude:claude-sonnet-5-5@medium. Generated 2026-11-09T22:05:42.401Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | claude:claude-opus-5-5@medium | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |
| tracetoon-baseline vs tracetoon-candidate | claude:claude-sonnet-5-5@medium | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.20 | 0.00 | 1.05 | 99% | 37% | 72% | 0.00 | 402 | $3.47 |
| tracetoon-candidate | 20 | 0.20 | 0.00 | 0.45 | 92% | 40% | 57% | 0.00 | 422 | $2.32 |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 0 | 5 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.85 | 1.60 | 1.50 | 1.40 | 2.00 | 0.85 | 1.70 | 0.42 | 1.75 | 2.00 |
| tracetoon-candidate | 1.95 | 1.45 | 1.95 | 1.25 | 1.75 | 1.85 | 1.70 | 1.95 | 1.75 | 1.80 |

## Judge agreement

- claude:claude-opus-5-5@medium vs claude:claude-sonnet-5-5@medium: 20% of 5 pair verdicts agree; Cohen's kappa 0.05.

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

