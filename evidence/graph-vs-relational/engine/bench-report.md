# Engine benchmark: cypherlite vs SQLite (both WebAssembly)

cypherlite with its statement clocks stubbed (telemetry-off proxy) vs normal: median time ratio 0.998 over 130 cells.

## W1: the PR workload (brief, derive, every named query), real graphs

| graphs | engine | n | load ms (median) | workload ms warm (median) | wasm MB peak (median) | RSS MB (median) |
|---|---|---|---|---|---|---|
| ≤40 nodes | graph | 65 | 147 | 24 | 18 | 172 |
| ≤40 nodes | graph-noclock | 65 | 144 | 24 | 18 | 171 |
| ≤40 nodes | sqlite | 65 | 47 | 8.6 | 8 | 151 |
| 41–400 nodes | graph | 3 | 220 | 277 | 19 | 205 |
| 41–400 nodes | graph-noclock | 3 | 221 | 278 | 19 | 209 |
| 41–400 nodes | sqlite | 3 | 62 | 79 | 35 | 216 |
| >400 nodes | graph | 2 | 408 | 860 | 25 | 298 |
| >400 nodes | graph-noclock | 2 | 410 | 960 | 25 | 299 |
| >400 nodes | sqlite | 2 | 142 | 322 | 66 | 378 |

## W2 multi-hop: real/big-prbench-parallel (349 nodes)

| query | cypherlite ms | SQLite ms (+edge table) | cypherlite / SQLite | cypherlite wasm MB | SQLite wasm MB | answer |
|---|---|---|---|---|---|---|
| B1-khop-k1 | 3.1 | 1.4 (+3.3) | 2.21× | 22 | 8 | = |
| B1-khop-k2 | 13 | 7.1 (+2.9) | 1.86× | 24 | 8 | = |
| B1-khop-k3 | 172 | 27 (+3.0) | 6.47× | 83 | 8 | = |
| B1-khop-k4 | 3,180 | 72 (+4.1) | 44.10× | 1,070 | 8 | = |
| B1-khop-k5 | trap at 4,072 MB | 149 (+5.2) | — | — | 8 |  |
| B1-khop-k6 | skipped | 202 (+7.2) | — | — | 8 |  |
| B1sp-khop-k1 | 42 | 1.6 (+3.2) | 25.94× | 22 | 8 | = |
| B1sp-khop-k2 | 80 | 11 (+3.2) | 7.07× | 31 | 8 | = |
| B1sp-khop-k3 | 211 | 30 (+3.7) | 7.08× | 42 | 8 | = |
| B1sp-khop-k4 | 244 | 69 (+9.1) | 3.55× | 44 | 8 | = |
| B1sp-khop-k5 | 260 | 103 (+3.1) | 2.51× | 44 | 8 | = |
| B1sp-khop-k6 | 266 | 146 (+3.1) | 1.83× | 44 | 8 | = |
| B2-cochange-d1 | 7.8 | 3.3 (+5.5) | 2.36× | 22 | 8 | = |
| B2-cochange-d2 | 16 | 13 (+9.4) | 1.23× | 23 | 8 | = |
| B2-cochange-d3 | 73 | 19 (+3.5) | 3.91× | 37 | 8 | = |
| B2-cochange-d4 | 204 | 25 (+3.0) | 8.28× | 68 | 8 | = |
| B2sp-cochange-d1 | 18 | 2.2 (+3.8) | 8.32× | 22 | 8 | = |
| B2sp-cochange-d2 | 20 | 9.1 (+4.3) | 2.23× | 22 | 8 | = |
| B2sp-cochange-d3 | 21 | 22 (+3.5) | 0.98× | 23 | 8 | = |
| B2sp-cochange-d4 | 22 | 30 (+4.6) | 0.73× | 23 | 8 | = |
| B3-shortest-prompt-commit | 12 | 202 (+3.4) | 0.06× | 22 | 8 | = |
| B4-provenance-chain | 10 | 3.1 (+3.3) | 3.32× | 23 | 8 | = |
| B5-cycle-closure | 2.4 | 0.6 (+4.6) | 4.00× | 22 | 8 | = |

## W2 multi-hop: synthetic/synthetic-n1 (349 nodes)

| query | cypherlite ms | SQLite ms (+edge table) | cypherlite / SQLite | cypherlite wasm MB | SQLite wasm MB | answer |
|---|---|---|---|---|---|---|
| B1-khop-k1 | 3.4 | 1.5 (+3.3) | 2.27× | 22 | 8 | = |
| B1-khop-k2 | 14 | 7.5 (+3.7) | 1.85× | 24 | 8 | = |
| B1-khop-k3 | 177 | 29 (+4.2) | 6.13× | 83 | 8 | = |
| B1-khop-k4 | 2,887 | 63 (+4.0) | 46.12× | 1,070 | 8 | = |
| B1-khop-k5 | trap at 4,072 MB | 121 (+3.4) | — | — | 8 |  |
| B1-khop-k6 | skipped | 127 (+3.3) | — | — | 8 |  |
| B1sp-khop-k1 | 39 | 1.4 (+3.3) | 28.00× | 23 | 8 | = |
| B1sp-khop-k2 | 72 | 7.4 (+3.4) | 9.73× | 31 | 8 | = |
| B1sp-khop-k3 | 185 | 33 (+4.9) | 5.61× | 42 | 8 | = |
| B1sp-khop-k4 | 213 | 61 (+3.7) | 3.51× | 44 | 8 | = |
| B1sp-khop-k5 | 218 | 96 (+3.4) | 2.26× | 44 | 8 | = |
| B1sp-khop-k6 | 226 | 137 (+3.8) | 1.65× | 44 | 8 | = |
| B2-cochange-d1 | 5.1 | 2.3 (+3.4) | 2.22× | 22 | 8 | = |
| B2-cochange-d2 | 9.5 | 8.4 (+3.6) | 1.13× | 23 | 8 | = |
| B2-cochange-d3 | 48 | 15 (+3.6) | 3.30× | 37 | 8 | = |
| B2-cochange-d4 | 171 | 23 (+3.3) | 7.52× | 68 | 8 | = |
| B2sp-cochange-d1 | 14 | 2.2 (+3.4) | 6.36× | 22 | 8 | = |
| B2sp-cochange-d2 | 17 | 11 (+3.4) | 1.58× | 23 | 8 | = |
| B2sp-cochange-d3 | 18 | 15 (+3.7) | 1.17× | 23 | 8 | = |
| B2sp-cochange-d4 | 18 | 23 (+4.4) | 0.80× | 23 | 8 | = |
| B3-shortest-prompt-commit | 10 | 190 (+3.4) | 0.05× | 22 | 8 | = |
| B4-provenance-chain | 10 | 2.7 (+3.4) | 3.85× | 23 | 8 | = |
| B5-cycle-closure | 2.0 | 0.6 (+3.6) | 3.33× | 22 | 8 | = |

## W2 multi-hop: real/big-prbench-score (530 nodes)

| query | cypherlite ms | SQLite ms (+edge table) | cypherlite / SQLite | cypherlite wasm MB | SQLite wasm MB | answer |
|---|---|---|---|---|---|---|
| B1-khop-k1 | 4.0 | 1.7 (+5.6) | 2.35× | 23 | 8 | = |
| B1-khop-k2 | 27 | 14 (+4.0) | 1.97× | 28 | 8 | = |
| B1-khop-k3 | 517 | 70 (+4.1) | 7.40× | 160 | 8 | = |
| B1-khop-k4 | trap at 3,477 MB | 156 (+4.7) | — | — | 8 |  |
| B1-khop-k5 | skipped | 291 (+4.1) | — | — | 8 |  |
| B1-khop-k6 | skipped | 400 (+3.6) | — | — | 8 |  |
| B1sp-khop-k1 | 102 | 2.0 (+4.9) | 50.75× | 26 | 8 | = |
| B1sp-khop-k2 | 266 | 21 (+10) | 12.76× | 45 | 8 | = |
| B1sp-khop-k3 | 805 | 108 (+6.8) | 7.47× | 69 | 8 | = |
| B1sp-khop-k4 | 1,099 | 186 (+4.6) | 5.90× | 81 | 8 | = |
| B1sp-khop-k5 | 897 | 321 (+5.2) | 2.79× | 82 | 8 | = |
| B1sp-khop-k6 | 938 | 357 (+4.7) | 2.62× | 82 | 8 | = |
| B2-cochange-d1 | 6.5 | 2.8 (+5.7) | 2.32× | 23 | 8 | = |
| B2-cochange-d2 | 51 | 16 (+4.2) | 3.22× | 30 | 8 | = |
| B2-cochange-d3 | 465 | 22 (+4.7) | 20.74× | 163 | 8 | = |
| B2-cochange-d4 | 7,411 | 37 (+5.1) | 202.50× | 1,608 | 8 | = |
| B2sp-cochange-d1 | 17 | 2.3 (+5.5) | 7.26× | 23 | 8 | = |
| B2sp-cochange-d2 | 26 | 9.8 (+4.3) | 2.67× | 26 | 8 | = |
| B2sp-cochange-d3 | 26 | 22 (+4.2) | 1.22× | 26 | 8 | = |
| B2sp-cochange-d4 | 27 | 38 (+5.0) | 0.72× | 26 | 8 | = |
| B3-shortest-prompt-commit | 30 | 611 (+4.1) | 0.05× | 23 | 8 | = |
| B4-provenance-chain | 20 | 4.2 (+4.2) | 4.69× | 28 | 8 | = |
| B5-cycle-closure | 2.5 | 0.5 (+5.7) | 5.00× | 23 | 8 | = |

## W2 multi-hop: real/big-tracetoon-graph (876 nodes)

| query | cypherlite ms | SQLite ms (+edge table) | cypherlite / SQLite | cypherlite wasm MB | SQLite wasm MB | answer |
|---|---|---|---|---|---|---|
| B1-khop-k1 | 5.4 | 1.8 (+6.2) | 3.00× | 24 | 8 | = |
| B1-khop-k2 | 42 | 20 (+6.0) | 2.07× | 33 | 8 | = |
| B1-khop-k3 | 1,797 | 134 (+6.0) | 13.38× | 560 | 8 | = |
| B1-khop-k4 | trap at 4,090 MB | 312 (+5.7) | — | — | 8 |  |
| B1-khop-k5 | skipped | 548 (+6.9) | — | — | 10 |  |
| B1-khop-k6 | skipped | 754 (+5.8) | — | — | 10 |  |
| B1sp-khop-k1 | 217 | 1.9 (+5.8) | 114.00× | 31 | 8 | = |
| B1sp-khop-k2 | 348 | 21 (+5.5) | 16.71× | 54 | 8 | = |
| B1sp-khop-k3 | 1,811 | 124 (+6.5) | 14.61× | 97 | 8 | = |
| B1sp-khop-k4 | 2,763 | 293 (+5.5) | 9.44× | 119 | 8 | = |
| B1sp-khop-k5 | 3,236 | 513 (+5.4) | 6.31× | 131 | 10 | = |
| B1sp-khop-k6 | 3,380 | 712 (+5.7) | 4.75× | 135 | 10 | = |
| B2-cochange-d1 | 10 | 3.1 (+5.6) | 3.32× | 25 | 8 | = |
| B2-cochange-d2 | 182 | 29 (+5.3) | 6.22× | 67 | 8 | = |
| B2-cochange-d3 | 7,071 | 62 (+7.8) | 114.24× | 2,320 | 8 | = |
| B2-cochange-d4 | trap at 4,096 MB | 103 (+5.5) | — | — | 8 |  |
| B2sp-cochange-d1 | 37 | 2.9 (+6.8) | 12.86× | 27 | 8 | = |
| B2sp-cochange-d2 | 48 | 28 (+5.4) | 1.69× | 29 | 8 | = |
| B2sp-cochange-d3 | 46 | 59 (+5.3) | 0.78× | 29 | 8 | = |
| B2sp-cochange-d4 | 51 | 94 (+6.5) | 0.54× | 29 | 8 | = |
| B3-shortest-prompt-commit | 52 | 1,061 (+7.9) | 0.05× | 24 | 12 | = |
| B4-provenance-chain | 25 | 4.9 (+5.5) | 5.06× | 34 | 8 | = |
| B5-cycle-closure | 3.0 | 0.8 (+5.7) | 3.75× | 24 | 8 | = |

## W2 multi-hop: synthetic/synthetic-n10 (5,258 nodes)

| query | cypherlite ms | SQLite ms (+edge table) | cypherlite / SQLite | cypherlite wasm MB | SQLite wasm MB | answer |
|---|---|---|---|---|---|---|
| B1-khop-k1 | 13 | 7.2 (+25) | 1.83× | 59 | 14 | = |
| B1-khop-k2 | 261 | 138 (+25) | 1.89× | 113 | 20 | = |
| B1-khop-k3 | trap at 3,777 MB | 1,442 (+29) | — | — | 60 |  |
| B1-khop-k4 | skipped | 6,051 (+25) | — | — | 125 |  |
| B1-khop-k5 | skipped | 15,284 (+26) | — | — | 216 |  |
| B1-khop-k6 | skipped | 26,093 (+30) | — | — | 311 |  |
| B1sp-khop-k1 | 9,129 | 7.1 (+26) | 1285.80× | 437 | 14 | = |
| B1sp-khop-k2 | 14,362 | 141 (+26) | 102.00× | 438 | 20 | = |
| B1sp-khop-k3 | 169,172 | 1,678 (+28) | 100.79× | 1,368 | 60 | = |
| B1sp-khop-k4 | timeout | 7,113 (+28) | — | — | 125 |  |
| B1sp-khop-k5 | skipped | 16,433 (+26) | — | — | 216 |  |
| B1sp-khop-k6 | skipped | 28,670 (+38) | — | — | 311 |  |
| B2-cochange-d1 | 31 | 6.4 (+25) | 4.83× | 61 | 14 | = |
| B2-cochange-d2 | 5,879 | 47 (+26) | 125.35× | 1,316 | 17 | = |
| B2-cochange-d3 | trap at 3,754 MB | 134 (+24) | — | — | 17 |  |
| B2-cochange-d4 | skipped | 230 (+27) | — | — | 17 |  |
| B2sp-cochange-d1 | 92 | 6.3 (+24) | 14.56× | 58 | 14 | = |
| B2sp-cochange-d2 | 359 | 49 (+25) | 7.31× | 70 | 17 | = |
| B2sp-cochange-d3 | 408 | 126 (+27) | 3.23× | 73 | 17 | = |
| B2sp-cochange-d4 | 437 | 223 (+27) | 1.96× | 73 | 17 | = |
| B3-shortest-prompt-commit | 39,704 | 47,980 (+28) | 0.83× | 180 | 374 | = |
| B4-provenance-chain | 174 | 27 (+25) | 6.47× | 108 | 14 | = |
| B5-cycle-closure | 11 | 3.0 (+30) | 3.53× | 58 | 14 | = |

## W2 multi-hop: synthetic/synthetic-n50 (26,726 nodes)

| query | cypherlite ms | SQLite ms (+edge table) | cypherlite / SQLite | cypherlite wasm MB | SQLite wasm MB | answer |
|---|---|---|---|---|---|---|
| B1-khop-k1 | 75 | 37 (+123) | 2.03× | 261 | 72 | = |
| B1-khop-k2 | 1,461 | 814 (+126) | 1.80× | 521 | 104 | = |
| B1-khop-k3 | trap at 4,037 MB | 31,794 (+122) | — | — | 1,115 |  |
| B1-khop-k4 | skipped | trap at 2,048 MB | — | — | — |  |
| B1-khop-k5 | skipped | skipped | — | — | — |  |
| B1-khop-k6 | skipped | skipped | — | — | — |  |
| B1sp-khop-k1 | trap at 4,084 MB | 35 (+116) | — | — | 72 |  |
| B1sp-khop-k2 | skipped | 867 (+167) | — | — | 104 |  |
| B1sp-khop-k3 | skipped | 30,357 (+123) | — | — | 1,115 |  |
| B1sp-khop-k4 | skipped | trap at 2,048 MB | — | — | — |  |
| B1sp-khop-k5 | skipped | skipped | — | — | — |  |
| B1sp-khop-k6 | skipped | skipped | — | — | — |  |
| B2-cochange-d1 | 144 | 20 (+118) | 7.12× | 266 | 72 | = |
| B2-cochange-d2 | trap at 4,071 MB | 58 (+124) | — | — | 72 |  |
| B2-cochange-d3 | skipped | 156 (+131) | — | — | 72 |  |
| B2-cochange-d4 | skipped | 249 (+121) | — | — | 72 |  |
| B2sp-cochange-d1 | 249 | 20 (+133) | 12.14× | 261 | 72 | = |
| B2sp-cochange-d2 | 1,882 | 58 (+116) | 32.44× | 261 | 72 | = |
| B2sp-cochange-d3 | 2,270 | 146 (+122) | 15.60× | 261 | 72 | = |
| B2sp-cochange-d4 | 2,362 | 256 (+145) | 9.22× | 261 | 72 | = |
| B3-shortest-prompt-commit | timeout | trap at 2,048 MB | — | — | — |  |
| B4-provenance-chain | 976 | 147 (+127) | 6.63× | 570 | 72 | = |
| B5-cycle-closure | 51 | 10 (+141) | 4.90× | 261 | 72 | = |

## W2 multi-hop: synthetic/synthetic-n200 (107,426 nodes)

| query | cypherlite ms | SQLite ms (+edge table) | cypherlite / SQLite | cypherlite wasm MB | SQLite wasm MB | answer |
|---|---|---|---|---|---|---|
| B1-khop-k1 | timeout | 152 (+564) | — | — | 260 |  |
| B1-khop-k2 | skipped | 3,322 (+484) | — | — | 448 |  |
| B1-khop-k3 | skipped | trap at 2,048 MB | — | — | — |  |
| B1-khop-k4 | skipped | skipped | — | — | — |  |
| B1-khop-k5 | skipped | skipped | — | — | — |  |
| B1-khop-k6 | skipped | skipped | — | — | — |  |
| B1sp-khop-k1 | timeout | 174 (+528) | — | — | 260 |  |
| B1sp-khop-k2 | skipped | 3,372 (+505) | — | — | 448 |  |
| B1sp-khop-k3 | skipped | trap at 2,048 MB | — | — | — |  |
| B1sp-khop-k4 | skipped | skipped | — | — | — |  |
| B1sp-khop-k5 | skipped | skipped | — | — | — |  |
| B1sp-khop-k6 | skipped | skipped | — | — | — |  |
| B2-cochange-d1 | timeout | 71 (+502) | — | — | 260 |  |
| B2-cochange-d2 | skipped | 119 (+571) | — | — | 260 |  |
| B2-cochange-d3 | skipped | 196 (+515) | — | — | 260 |  |
| B2-cochange-d4 | skipped | 288 (+504) | — | — | 260 |  |
| B2sp-cochange-d1 | timeout | 72 (+478) | — | — | 260 |  |
| B2sp-cochange-d2 | skipped | 116 (+511) | — | — | 260 |  |
| B2sp-cochange-d3 | skipped | 192 (+497) | — | — | 260 |  |
| B2sp-cochange-d4 | skipped | 289 (+480) | — | — | 260 |  |
| B3-shortest-prompt-commit | timeout | trap at 2,048 MB | — | — | — |  |
| B4-provenance-chain | timeout | 611 (+484) | — | — | 260 |  |
| B5-cycle-closure | timeout | 43 (+531) | — | — | 260 |  |

## Outcome B check (fixed in advance)

B holds for a workload where cypherlite is faster, or its time or memory grows more slowly with graph size or hops, than SQLite's.

| workload | cypherlite faster in | SQLite faster in | cypherlite failed (timeout/trap) | SQLite failed | B |
|---|---|---|---|---|---|
| B1 | 0 | 18 | 7 | 2 | no |
| B1sp | 0 | 27 | 3 | 2 | no |
| B2 | 0 | 18 | 4 | 0 | no |
| B2sp | 6 | 18 | 1 | 0 | no |
| B3 | 5 | 0 | 2 | 2 | yes |
| B4 | 0 | 6 | 1 | 0 | no |
| B5 | 0 | 6 | 1 | 0 | no |
