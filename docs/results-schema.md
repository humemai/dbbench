# Result rows

One published measurement is one row. A row says what ran, on what, and how it went. The fields below are the ones every row carries; lanes add their own metrics.

| field | meaning |
|---|---|
| `backend` | the engine and arm that ran, for example an in-process arm or a server arm |
| `lane` | the lane (tables, graphs, vectors, time series, cross-model, lifecycle) |
| `scale` / `tier` | the corpus size |
| `workload` | the task within the lane |
| `rep` | the repetition number |
| `engine_version` | the exact engine version; container runs also record the image digest |
| `durability_class` | the durability class the run used, where the engine offers more than one |
| `mem_cap` | the memory cap the run had |
| `error` / `oom_killed` | what went wrong, if anything; a failure is a result |
| metric fields | latencies (median and percentiles), throughput, peak memory and the like, per lane |
| `*_censored` / `*_budget_s` | whether a query hit its time budget, and the budget |

Rows are never edited. A correction adds a row; the history keeps both.
