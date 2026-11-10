# Evidence: Tracetoon graph brief vs a relational evidence store

Public evidence for the comparison between Tracetoon's evidence-graph brief (on Relate, the
open-source successor of cypherlite) and a relational evidence store (SQLite tables, FTS5 BM25
and local embeddings), plus SQLite running the same graph queries. This is research evidence:
the relational and SQLite implementations are not proposed for upstream Tracetoon. They live on
the steveonjava fork in branches:

- `steveonjava/tracetoon` `r17-relational` (9f05d15): relational arm used in the comparison.
- `steveonjava/tracetoon` `r16-sqlite-parity` (c088a54): SQLite port of the graph queries with byte-identical briefs.
- `steveonjava/tracetoon` `feat/evidence-sqlite`, `feat/evidence-sqlite-extras`, `feat/evidence-relational`, `feat/shape-relational`, `feat/shape-relational-h3`, `feat/graph-*`: the parallel exploration branches, including the engine benchmark script (`scripts/bench-engines.ts` on `feat/evidence-sqlite-extras`).
- `steveonjava/tracetoon` `r18-a`..`r22-fixes`, `closeout`: graph iterations; the shipping build is `closeout` (bd55f75), proposed upstream as `feat/evidence-graph`.

## Contents

- `briefs/graph-vs-base.html`: the graph vs original-workflow report (no relational content).
- `briefs/graph-vs-relational.html`: the graph vs relational report, with feedback for the Relate team.
- `comparison-tables.md`: per-round graph vs relational paired tables (r15–r22).
- `paired-*.md`: round-23 paired analyses (`prbench` `scripts/paired-delta.ts`).
- `rounds/<round>/<provider>/<run>/summary.md`: harness summaries for each run (aggregates only; no session logs or drafts).
- `engine/bench-report.md`, `engine/paths-report.txt`: cypherlite v0.16.1 vs SQLite engine benchmark.
- `engine/relate-vs-cypherlite-timings.json`: `query brief` / `prepare` timings, Relate aa0f79e vs cypherlite, on tracetoon's dev cases.

## Method

prbench (harness with `--systems baseline,candidate`, `crossjudge`, `paired-delta`), dataset
real-cases@1.0.0 dev split (5 cases × 5 replicates), judges Opus 5.5 + Sonnet 5.5 (Claude) and
Sol 6.1 + Terra 6.1 (Codex), each pair judged in both orders; consensus win = all 4 judgments
agree. Δ-of-Δ = (graph − its base) − (relational − its base), case bootstrap 5000, seed 7.
See `docs/reproduce-graph-vs-base.md` in prbench for how runs are built and launched.
