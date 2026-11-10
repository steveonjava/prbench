| arm | provider | run | tracetoon rev | composite cand / base (case-mean) | Δ vs own base [95% CI] | consensus W–T–L vs base | factual errors/judgment cand / base | cost/draft USD cand / base |
|---|---|---|---|---|---|---|---|---|
| published graph | claude | r15/claude/sonnet-h1 | 96686e9 | 78.9 / 73.6 | +5.4 [+2.5, +8.2] | 10–15–0 | 0.08 / 0.19 | 0.436 / 0.781 |
| relational | claude | r17/claude/sonnet-rel | 9f05d15 | 73.0 / 75.0 | −2.1 [−8.0, +3.6] | 6–17–2 | 0.14 / 0.15 | 0.412 / 0.781 |
| graph g2 | claude | r18/claude/sonnet-g2 | b12d2c9 | 77.9 / 73.5 | +4.4 [−1.4, +10.2] | 12–13–0 | 0.13 / 0.16 | 0.411 / 0.781 |
| graph g3 | claude | r19/claude/sonnet-g3 | 7038fac | 75.7 / 73.9 | +1.8 [−2.3, +4.7] | 8–16–1 | 0.09 / 0.14 | 0.422 / 0.781 |
| graph g4b | claude | r20/claude/sonnet-g4b | 4dd6e7c | 76.8 / 74.2 | +2.5 [−4.1, +8.7] | 14–10–1 | 0.16 / 0.08 | 0.418 / 0.690 |
| graph g5 | claude | r21/claude/sonnet-g5 | 0101b31 | 75.8 / 74.6 | +1.2 [−6.7, +8.4] | 12–12–1 | 0.16 / 0.12 | 0.425 / 0.690 |
| graph g6 | claude | r22/claude/sonnet-g6 | 7483847 | 76.2 / 74.2 | +2.0 [−2.3, +6.2] | 16–8–1 | 0.12 / 0.09 | 0.430 / 0.690 |
| published graph | codex | r15/codex/terra-d1 | 96686e9 | 84.3 / 81.8 | +2.5 [+1.4, +3.6] | 7–16–2 | 0.09 / 0.04 | 0.172 / 0.320 |
| relational | codex | r17/codex/terra-rel | 9f05d15 | 85.0 / 82.2 | +2.8 [+0.3, +4.9] | 13–11–1 | 0.00 / 0.07 | 0.169 / 0.320 |
| graph g2 | codex | r18/codex/terra-g2 | b12d2c9 | 85.5 / 82.6 | +2.9 [−0.3, +5.4] | 8–15–2 | 0.11 / 0.08 | 0.212 / 0.320 |
| graph g2v (bm25+vector) | codex | r18/codex/terra-g2v | b12d2c9 | 84.4 / 82.3 | +2.0 [−1.0, +4.9] | 9–14–2 | 0.14 / 0.09 | 0.216 / 0.320 |
| graph g3 | codex | r19/codex/terra-g3 | 7038fac | 85.8 / 82.2 | +3.6 [+1.2, +6.4] | 10–13–2 | 0.07 / 0.08 | 0.186 / 0.320 |
| graph g4 | codex | r20/codex/terra-g4 | 4dd6e7c | 86.5 / 83.2 | +3.3 [+0.4, +5.6] | 10–14–1 | 0.05 / 0.05 | 0.189 / 0.320 |
| graph g5 | codex | r21/codex/terra-g5 | 0101b31 | 86.8 / 82.4 | +4.4 [+2.5, +6.7] | 14–11–0 | 0.00 / 0.06 | 0.190 / 0.320 |

| graph arm | provider | rev | graph better / rel better / equal (25 case×rep pairs) | Δ-of-Δ (graph − rel) [95% CI] | factual errors/judgment graph vs rel |
|---|---|---|---|---|---|
| published graph (r15/claude/sonnet-h1) | claude | 96686e9 | 6 / 1 / 18 | +7.4 [+1.1, +15.4] | 0.08 vs 0.14 |
| graph g2 (r18/claude/sonnet-g2) | claude | b12d2c9 | 8 / 2 / 15 | +6.5 [−0.4, +15.9] | 0.13 vs 0.14 |
| graph g3 (r19/claude/sonnet-g3) | claude | 7038fac | 8 / 5 / 12 | +3.9 [−0.5, +10.0] | 0.09 vs 0.14 |
| graph g4b (r20/claude/sonnet-g4b) | claude | 4dd6e7c | 11 / 3 / 11 | +4.6 [+0.1, +9.5] | 0.16 vs 0.14 |
| graph g5 (r21/claude/sonnet-g5) | claude | 0101b31 | 8 / 1 / 16 | +3.3 [−2.9, +9.7] | 0.16 vs 0.14 |
| graph g6 (r22/claude/sonnet-g6) | claude | 7483847 | 12 / 2 / 11 | +4.1 [−1.2, +9.9] | 0.12 vs 0.14 |
| published graph (r15/codex/terra-d1) | codex | 96686e9 | 1 / 7 / 17 | −0.3 [−1.8, +1.2] | 0.09 vs 0.00 |
| graph g2 (r18/codex/terra-g2) | codex | b12d2c9 | 1 / 7 / 17 | +0.1 [−1.0, +1.1] | 0.11 vs 0.00 |
| graph g2v (bm25+vector) (r18/codex/terra-g2v) | codex | b12d2c9 | 3 / 8 / 14 | −0.8 [−3.9, +1.7] | 0.14 vs 0.00 |
| graph g3 (r19/codex/terra-g3) | codex | 7038fac | 5 / 8 / 12 | +0.8 [−1.5, +2.3] | 0.07 vs 0.00 |
| graph g4 (r20/codex/terra-g4) | codex | 4dd6e7c | 2 / 5 / 18 | +0.5 [−1.2, +2.3] | 0.05 vs 0.00 |
| graph g5 (r21/codex/terra-g5) | codex | 0101b31 | 6 / 4 / 15 | +1.6 [+0.1, +2.8] | 0.00 vs 0.00 |


## Addendum: r22 Codex (completed after packaging)

Graph arm `r22/codex/terra-g6` (tracetoon `7483847`) against relational `r17/codex/terra-rel`, same method as above:

| | vs own base | consensus | errors | paired vs relational (graph / rel / equal) | Δ-of-Δ [95% CI] |
|---|---|---|---|---|---|
| Codex graph r22 | +4.8 [3.8, 5.7] (86.6 vs 81.9) | 14–0 | 0.01 | 6 / 5 / 14 | +1.95 [+0.34, +3.39] |

Per case Δ-of-Δ: pr11 +1.8, pr12 +2.8, pr5 +4.3, pr8 −0.9, pr9 +1.9.
