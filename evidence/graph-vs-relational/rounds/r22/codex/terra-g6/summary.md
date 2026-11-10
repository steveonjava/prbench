# dev comparison

Outcome: **inconclusive**. Quality: inconclusive. Efficiency: inconclusive.

Writers: 50/50; order judgments: 100/100.

Failed attempts: 0; failed-attempt time: 0s; current pending cleanup: 0.

| Model | System | Samples | Median writer seconds | Median input tokens | Pending cleanup |
|---|---|---:|---:|---:|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 224.74 | 3232457 | 0 |
| gpt-6.1-terra@medium | tracetoon-candidate | 25 | 300.93 | 2086269 | 0 |

## Gate findings

- gpt-6.1-terra@medium: median paired writer time did not improve
- Unresolved: fd73a3d2035f15aa7df72ca4bedcde75280218ff4e9d6591292d157c78757c08

## Paired performance

Candidate/baseline geometric mean writer ratio: 1.284; case-clustered 95% interval: [1.2093348067236864,1.4164465295152684].

- 5 replicate(s) still represent 5 independent cases in this split.
- Writer timing includes service waits and neutral observation overhead; runtime diagnostics may overlap.
- Diagnostic reuse cannot establish a fresh performance improvement.
- Raw judgments are preserved separately from source-backed adjudications.

## Scores

Composite (0-100) = 35·claims + 15·context + 15·uncertainties + 35·rubric (coverage as fractions of the fact sheet, rubric as mean/2) − 15·factual errors − 7·unsupported claims − 10·traps hit, floored at 0. Each draft is averaged over all its judgments; arm means are means of per-case means, with a 95% bootstrap interval over cases. Components are the primary evidence; the composite is a summary.

| Model | System | Drafts | Composite [95% CI] | Claims | Context | Uncert. | Rubric | Errors | Unsupported | Traps | $/draft | Cost covers | Subagents/draft | Input tokens | Queries |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---|---:|---:|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 81.9 [77.5, 85.2] | 0.84 | 0.38 | 1.00 | 0.94 | 0.07 | 0.00 | 0.00 | 0.320* | all threads | 3.0 | 3096526 | – |
| gpt-6.1-terra@medium | tracetoon-candidate | 25 | 86.6 [82.8, 89.2] | 0.94 | 0.46 | 1.00 | 0.92 | 0.01 | 0.00 | 0.00 | 0.193* | all threads | 0.0 | 2101026 | 1.0 |

Mixed-model writers (subagent threads on another model; each model's tokens are priced at its own rate, and Claude's reported cost already covers every model):

| Model | System | Mixed-model drafts | Models used |
|---|---|---:|---|
| gpt-6.1-terra@medium | tracetoon-candidate | 25/25 | gpt-6-luna, gpt-6.1-terra |

Paired candidate − other system (same model, case and replicate). Leave one case out = lowest and highest composite Δ when each case in turn is dropped:

| Model | Against | Pairs | Composite Δ [95% CI] | Leave one case out | Factual errors Δ |
|---|---|---:|---|---|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 4.8 [3.8, 5.7] | 4.5 to 5.2 | -0.06 |

Per-case composite Δ (tracetoon-candidate − tracetoon-baseline, same model; mean over paired replicates, pairs in parentheses):

| Case | gpt-6.1-terra@medium |
|---|---:|
| pr5 | 3.1 (5) |
| pr8 | 5.3 (5) |
| pr9 | 5.7 (5) |
| pr11 | 5.9 (5) |
| pr12 | 3.8 (5) |
| Mean of cases | 4.8 |

## Accuracy

Error rate = share of judgments that found at least one factual error (mean of per-case means, 95% bootstrap interval over cases). Error classes are mean factual errors per judgment by kind of statement.

| Model | System | Drafts | Error rate [95% CI] | Errors | Unsupported | Claims | validation | code structure | attribution | motivation | pipeline | other | $/draft |
|---|---|---:|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| gpt-6.1-terra@medium | tracetoon-baseline | 25 | 0.07 [0.00, 0.17] | 0.07 | 0.00 | 0.84 | 0.00 | 0.01 | 0.01 | 0.00 | 0.03 | 0.02 | 0.320 |
| gpt-6.1-terra@medium | tracetoon-candidate | 25 | 0.01 [0.00, 0.03] | 0.01 | 0.00 | 0.94 | 0.01 | 0.00 | 0.00 | 0.00 | 0.00 | 0.00 | 0.193 |

Candidate arms against baseline arms (any model; shared cases). Deltas are candidate minus baseline over per-case means, with a 95% bootstrap interval over cases. Coverage guard: claim coverage may drop by at most 0.05.

| Candidate | Against baseline | Cases | Error rate Δ [95% CI] | Composite Δ [95% CI] | Claims Δ | Guard | Cost ratio |
|---|---|---:|---|---|---:|---|---:|
| gpt-6.1-terra@medium | gpt-6.1-terra@medium | 5 | -0.06 [-0.16, 0.02] | 4.8 [3.8, 5.7] | 0.10 | ok | 1.7× cheaper |

\* Estimated from token counts and src/report/prices.json (USD per million tokens, short-context list prices for models whose runs report no USD (Codex), as reported by third-party trackers on 2026-11-06 (morphllm.com/openai-api-pricing); verify against the provider's pricing page.).

Cost covers: "all threads" includes every subagent thread the writer spawned (researcher, drafter, reviewer…), from the artifact or, for runs saved before that was recorded, recomputed from the accepted attempt's saved Codex traces ("traces"), with each model response counted once. "Main thread only" omits subagents and understates cost when the skill delegates. $/draft in the accuracy table and its cost ratios use the same figures.

## gpt-6.1-terra@medium, replicate 1: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-10T00:47:08.657Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 0.40 | 82% | 41% | 100% | 0.00 | 166 | – |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 0.35 | 91% | 47% | 100% | 0.00 | 330 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 4 | 1 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.75 | 2.00 | 2.00 | 2.00 | 1.55 | 2.00 | – | 1.80 | 2.00 |
| tracetoon-candidate | 1.75 | 1.85 | 2.00 | 2.00 | 1.95 | 2.00 | 1.35 | 1.89 | 2.00 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 60% of 5 pair verdicts agree; Cohen's kappa -0.25.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-baseline: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 2: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-10T00:47:08.771Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 1 | 3 | 1 | 1 | 0 | 25% | 0.63 | -0.40 [-1.00, 0.40] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.00 | 0.00 | 0.20 | 91% | 36% | 100% | 0.00 | 156 | – |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 1.10 | 95% | 46% | 100% | 0.00 | 348 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 4 | 1 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.60 | 2.00 | 1.95 | 2.00 | 1.55 | 2.00 | 1.00 | 2.00 | 2.00 |
| tracetoon-candidate | 1.75 | 1.65 | 2.00 | 2.00 | 2.00 | 2.00 | 1.20 | 1.80 | 2.00 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 60% of 5 pair verdicts agree; Cohen's kappa 0.17.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 3: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-10T00:47:08.865Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 1 | 4 | 0 | 0 | 0 | 20% | 0.38 | -0.60 [-1.00, 0.20] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 0 | 5 | 0 | 0 | 0 | 0% | 0.06 | -1.00 [-1.00, -1.00] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 4 | 1 | 0 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.15 | 0.00 | 0.40 | 87% | 33% | 100% | 0.00 | 185 | – |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 0.50 | 95% | 51% | 100% | 0.00 | 370 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 5 | 0 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 1.95 | 1.60 | 2.00 | 1.95 | 2.00 | 1.60 | 2.00 | 1.00 | 2.00 | 1.85 |
| tracetoon-candidate | 1.80 | 1.80 | 2.00 | 2.00 | 2.00 | 2.00 | 1.15 | 2.00 | 2.00 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.00.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 4: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-10T00:47:08.961Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 3 | 2 | 2 | 0 | 0% | 0.25 | -0.60 [-1.00, -0.20] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.10 | 0.00 | 0.60 | 80% | 43% | 100% | 0.00 | 168 | – |
| tracetoon-candidate | 20 | 0.05 | 0.00 | 0.75 | 95% | 40% | 100% | 0.00 | 311 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 4 | 1 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.75 | 1.89 | 1.90 | 2.00 | 1.30 | 2.00 | – | 1.80 | 2.00 |
| tracetoon-candidate | 1.80 | 1.80 | 1.84 | 2.00 | 1.95 | 2.00 | 1.15 | 2.00 | 1.80 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 80% of 5 pair verdicts agree; Cohen's kappa 0.55.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-baseline: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

## gpt-6.1-terra@medium, replicate 5: tracetoon-baseline

# prbench report

Rubric v6. Judges: codex:gpt-6.1-sol@medium, codex:gpt-6.1-terra@medium. Generated 2026-11-10T00:47:09.058Z.

Evidence gaps are unverified claims, not errors or fabrication. Fresh evidence coverage is reported per artifact; partial capture may still establish individual results. Inconclusive preferences are excluded from win/tie statistics, intervals and judge agreement.

Completed 10 of 10 expected case/pair/judge results (each requires both orders).

Each pair is judged in both orders; a win needs both orders to agree. An evidence-dependent abstention in either order makes the pair inconclusive; other disagreements are ties (a *flip* when the orders picked opposite systems). "all judges agree" includes only pairs completed by every configured judge, and counts a win only when every judge gave it. With few cases, treat p-values and intervals as a sense of scale, not proof.

## dev split (5 cases)

pr11, pr12, pr5, pr8, pr9

### Head to head

| x vs y | judge | x wins | y wins | ties | flips | inconclusive | x win rate | sign test p | mean (x−y) [95% CI] |
|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-sol@medium | 0 | 2 | 3 | 3 | 0 | 0% | 0.50 | -0.40 [-0.80, 0.00] |
| tracetoon-baseline vs tracetoon-candidate | codex:gpt-6.1-terra@medium | 0 | 4 | 1 | 1 | 0 | 0% | 0.13 | -0.80 [-1.00, -0.40] |
| tracetoon-baseline vs tracetoon-candidate | all judges agree | 0 | 1 | 4 | 4 | 0 | 0% | 1.00 | -0.20 [-0.60, 0.00] |

### Per system (means over every judgment of that system)

| system | judgments | factual errors | unsupported overclaims | evidence gaps | claims covered | context covered | uncertainties respected | traps hit | median words | total agent cost |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 20 | 0.10 | 0.00 | 0.60 | 82% | 37% | 100% | 0.00 | 180 | – |
| tracetoon-candidate | 20 | 0.00 | 0.00 | 0.40 | 93% | 45% | 100% | 0.00 | 356 | – |

### Fresh writer evidence coverage (artifact counts)

| system | artifacts | recorded | partial | unavailable |
|---|---|---|---|---|
| tracetoon-baseline | 5 | 5 | 0 | 0 |
| tracetoon-candidate | 5 | 0 | 5 | 0 |

### Rubric (mean of 0–2 scores; n/a items excluded)

| system | problem | rationale | validation | consequences | orientation | entry | economy | feedback | links | scope |
|---|---|---|---|---|---|---|---|---|---|---|
| tracetoon-baseline | 2.00 | 1.60 | 2.00 | 1.90 | 2.00 | 1.55 | 2.00 | 1.00 | 1.80 | 1.90 |
| tracetoon-candidate | 1.75 | 1.75 | 2.00 | 2.00 | 1.95 | 2.00 | 1.10 | 1.86 | 1.67 | 2.00 |

## Judge agreement

- codex:gpt-6.1-sol@medium vs codex:gpt-6.1-terra@medium: 20% of 5 pair verdicts agree; Cohen's kappa -0.43.

## Warnings

- pr11: tracetoon-candidate: fresh validation evidence partial
- pr12: tracetoon-candidate: fresh validation evidence partial
- pr5: tracetoon-candidate: fresh validation evidence partial
- pr8: tracetoon-candidate: fresh validation evidence partial
- pr9: tracetoon-candidate: fresh validation evidence partial

