# dev comparison

Outcome: **inconclusive**. Quality: inconclusive. Efficiency: inconclusive.

Writers: 50/50; order judgments: 100/100.

Failed attempts: 1; failed-attempt time: 87s; current pending cleanup: 0.

| Model | System | Samples | Median writer seconds | Median input tokens | Pending cleanup |
|---|---|---:|---:|---:|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 224.74 | 3232457 | 0 |
| gpt-6.1-terra@medium | tracetoon-candidate | 25 | 319.00 | 2238457 | 0 |

## Gate findings

- gpt-6.1-terra@medium: median paired writer time did not improve
- Unresolved: 4febda63a6ca1f0b559389c5294e3be0e3ecdbbe190a70a67363578a72df8071
- Unresolved: 8263c323a87175ee3a0cd4e883a7698c28bb6bbe5585bb1924e850f87cc07cfe
- Unresolved: ed00e5224ba71499c6d7b0ca56e4f715a80c72cb4542590f5aff20342eb27d8a
- Unresolved: 17a52bdc2d0bde7cc89011983afbed0ca9e5eb59369a8455211878275c07917b
- Unresolved: 2175aea23902c63276cf01e9d1dd88338ca418e87bd62004e43d7bbda95bc250

## Paired performance

Candidate/baseline geometric mean writer ratio: 1.423; case-clustered 95% interval: [1.336451588275476,1.573853091942473].

- 5 replicate(s) still represent 5 independent cases in this split.
- Writer timing includes service waits and neutral observation overhead; runtime diagnostics may overlap.
- Diagnostic reuse cannot establish a fresh performance improvement.
- Raw judgments are preserved separately from source-backed adjudications.

## Scores

Composite (0-100) = 35·claims + 15·context + 15·uncertainties + 35·rubric (coverage as fractions of the fact sheet, rubric as mean/2) − 15·factual errors − 7·unsupported claims − 10·traps hit, floored at 0. Each draft is averaged over all its judgments; arm means are means of per-case means, with a 95% bootstrap interval over cases. Components are the primary evidence; the composite is a summary.

| Model | System | Drafts | Composite [95% CI] | Claims | Context | Uncert. | Rubric | Errors | Unsupported | Traps | $/draft | Cost covers | Subagents/draft | Input tokens | Queries |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 82.6 [78.9, 86.3] | 0.87 | 0.39 | 1.00 | 0.93 | 0.08 | 0.00 | 0.00 | 0.320* | all threads | 3.0 | 3096526 | – |
| gpt-6.1-terra@medium | tracetoon-candidate | 25 | 85.5 [82.7, 88.3] | 0.96 | 0.49 | 0.99 | 0.90 | 0.11 | 0.00 | 0.00 | 0.212* | all threads | 0.0 | 2249787 | – |

Mixed-model writers (subagent threads on another model; each model's tokens are priced at its own rate, and Claude's reported cost already covers every model):

| Model | System | Mixed-model drafts | Models used |
|---|---|---:|---|
| gpt-6.1-terra@medium | tracetoon-candidate | 25/25 | gpt-6-luna, gpt-6.1-terra |

Paired candidate − other system (same model, case and replicate). Leave one case out = lowest and highest composite Δ when each case in turn is dropped:

| Model | Against | Pairs | Composite Δ [95% CI] | Leave one case out | Factual errors Δ |
|---|---|---:|---|---|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 2.9 [-0.3, 5.4] | 2.2 to 4.4 | 0.03 |

Per-case composite Δ (tracetoon-candidate − tracetoon-baseline, same model; mean over paired replicates, pairs in parentheses):

| Case | gpt-6.1-terra@medium |
|---|---:|
| pr5 | -3.0 (5) |
| pr8 | 5.4 (5) |
| pr9 | 4.6 (5) |
| pr11 | 5.8 (5) |
| pr12 | 1.8 (5) |
| Mean of cases | 2.9 |

Judge reliability (timed-out and transient calls are retried, up to 3 attempts per order judgment; a malformed reply gets one format repair):

| Judge | Failed attempts | Timed out | Transient | Format | Other |
|---|---:|---:|---:|---:|---:|
| codex:gpt-6.1-sol@medium | 1 | 0 | 0 | 1 | 0 |

## Accuracy

Error rate = share of judgments that found at least one factual error (mean of per-case means, 95% bootstrap interval over cases). Error classes are mean factual errors per judgment by kind of statement.

| Model | System | Drafts | Error rate [95% CI] | Errors | Unsupported | Claims | validation | code structure | attribution | motivation | pipeline | other | $/draft |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 0.08 [0.00, 0.24] | 0.08 | 0.00 | 0.87 | 0.01 | 0.00 | 0.00 | 0.00 | 0.04 | 0.03 | 0.320 |
| gpt-6.1-terra@medium | tracetoon-candidate | 25 | 0.11 [0.03, 0.19] | 0.11 | 0.00 | 0.96 | 0.02 | 0.05 | 0.00 | 0.00 | 0.00 | 0.04 | 0.212 |

Candidate arms against baseline arms (any model; shared cases). Deltas are candidate minus baseline over per-case means, with a 95% bootstrap interval over cases. Coverage guard: claim coverage may drop by at most 0.05.

| Candidate | Against baseline | Cases | Error rate Δ [95% CI] | Composite Δ [95% CI] | Claims Δ | Guard | Cost ratio |
|---|---|---:|---|---|---:|---|---:|
| gpt-6.1-terra@medium | gpt-6.1-terra@medium | 5 | 0.03 [-0.09, 0.14] | 2.9 [-0.3, 5.4] | 0.09 | ok | 1.5× cheaper |

\* Estimated from token counts and src/report/prices.json (USD per million tokens, short-context list prices for models whose runs report no USD (Codex), as reported by third-party trackers on 2026-11-06 (morphllm.com/openai-api-pricing); verify against the provider's pricing page.).

Cost covers: "all threads" includes every subagent thread the writer spawned (researcher, drafter, reviewer…), from the artifact or, for runs saved before that was recorded, recomputed from the accepted attempt's saved Codex traces ("traces"), with each model response counted once. "Main thread only" omits subagents and understates cost when the skill delegates. $/draft in the accuracy table and its cost ratios use the same figures.

## gpt-6.1-terra@medium, replicate 1: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-09T13:28:30.362Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 1 | 2 | 2 | 2 | 0 | 33% | 1.00 | -0.20 [-0.80, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 0.45 | 86% | 41% | 100% | 0.00 | 166 | – |
| tracetoon-candidate | 20 | 0.05 | 0.00 | 1.05 | 95% | 47% | 100% | 0.00 | 349 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 4 | 1 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.80 | 2.00 | 2.00 | 2.00 | 1.60 | 2.00 | – | 2.00 | 2.00 |
| tracetoon-candidate | 1.65 | 1.65 | 2.00 | 2.00 | 2.00 | 1.75 | 1.25 | 1.80 | 2.00 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 60% of 5 pair verdicts agree; Cohen's kappa 0.33.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-baseline: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 2: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-09T13:28:30.453Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 0.20 | 92% | 36% | 100% | 0.00 | 156 | – |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 1.00 | 94% | 51% | 100% | 0.00 | 385 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 4 | 1 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.65 | 2.00 | 1.90 | 2.00 | 1.50 | 2.00 | 1.00 | 1.80 | 2.00 |
| tracetoon-candidate | 1.95 | 1.85 | 2.00 | 2.00 | 2.00 | 2.00 | 1.00 | 1.92 | 2.00 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.00.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 3: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-09T13:28:30.546Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 1 | 2 | 2 | 2 | 0 | 33% | 1.00 | -0.20 [-0.80, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 1 | 1 | 3 | 3 | 0 | 50% | 1.00 | 0.00 [-0.60, 0.60] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 1 | 0 | 4 | 4 | 0 | 100% | 1.00 | 0.20 [0.00, 0.60] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.10 | 0.00 | 0.45 | 89% | 34% | 100% | 0.00 | 185 | – |
| tracetoon-candidate | 20 | 0.05 | 0.00 | 1.15 | 96% | 51% | 96% | 0.00 | 377 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 5 | 0 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.70 | 2.00 | 1.85 | 2.00 | 1.60 | 2.00 | 1.00 | 1.80 | 1.90 |
| tracetoon-candidate | 1.70 | 1.75 | 1.89 | 2.00 | 1.95 | 1.85 | 1.00 | 1.78 | 1.80 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 40% of 5 pair verdicts agree; Cohen's kappa 0.06.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 4: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-09T13:28:30.639Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 1 | 3 | 1 | 1 | 0 | 25% | 0.63 | -0.40 [-1.00, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 1 | 3 | 1 | 1 | 0 | 25% | 0.63 | -0.40 [-1.00, 0.40] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.20 | 0.00 | 0.50 | 79% | 45% | 100% | 0.00 | 168 | – |
| tracetoon-candidate | 20 | 0.45 | 0.00 | 0.80 | 96% | 47% | 100% | 0.00 | 352 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 4 | 1 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.55 | 1.79 | 1.95 | 2.00 | 1.30 | 2.00 | 2.00 | 2.00 | 2.00 |
| tracetoon-candidate | 1.80 | 1.70 | 1.95 | 2.00 | 2.00 | 1.50 | 1.30 | 1.60 | 2.00 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.58.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 5: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-09T13:28:30.729Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.10 | 0.00 | 0.60 | 89% | 37% | 100% | 0.00 | 180 | – |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 0.90 | 96% | 50% | 99% | 0.00 | 353 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 5 | 0 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.90 | 1.50 | 2.00 | 1.95 | 2.00 | 1.55 | 2.00 | 1.00 | 1.13 | 1.85 |
| tracetoon-candidate | 1.85 | 1.70 | 2.00 | 2.00 | 2.00 | 1.90 | 1.00 | 2.00 | 1.75 | 1.95 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 40% of 5 pair verdicts agree; Cohen's kappa -0.15.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

