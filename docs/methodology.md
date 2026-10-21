# Methodology

These are the rules every published result follows. A result that breaks one of them is not published as a comparison; it is published as a declared exception, or not at all.

## The rules

1. **Same task, same data, same machine.** Every engine in a lane answers the same queries over the same corpus on the same dedicated machine. The machine's specification is on the results page.
2. **Answers are checked.** Each query's answer is reduced to a digest and compared between engines. A fast wrong answer is a failure, not a result.
3. **Settings are published.** Each engine runs at its documented defaults unless a setting is required to run the task (a memory limit, a durability class, an index the task needs).
   Every deviation is listed on the [Engines](engines.md) page with the reason. An index added for one engine is added, in its equivalent form, for every engine that has one.
4. **Equal resources.** Every engine gets the same memory cap and CPU allotment inside a lane, and the same durability classes are measured for every engine that offers them
   (a relaxed class and a strict class where the engine supports both).
5. **Repetitions and medians.** Each cell is run five times, and the page prints the median with the minimum and maximum, never a single run and never the mean.
6. **Budgets and censoring.** A query that cannot finish within its time budget is recorded as censored, with the budget, and is never silently dropped or counted as fast. Where an engine
   can be asked to stop a query itself, the budget is enforced by the engine; otherwise it is checked between iterations.
7. **Failures are results.** An engine that runs out of memory, times out or refuses a task has that recorded as its result for the cell, with the error it gave.
8. **Versions are exact.** Every row records the engine version and, for containers, the image digest it ran on. A cell never mixes rows from different versions: when an engine ships a new
   version, new rows are added next to the old ones. ArcadeDB is pinned by upstream commit rather than by release number, because its build line reads the same development version for every commit;
   its embedded and server arms in one table are built from the same commit and run the same JVM.
9. **Warm-up is declared.** Whether a timing includes the first run, a warm-up, or an index build is stated in the table it appears in.
10. **History is kept.** A correction or a new version adds rows; the earlier rows stay visible.

## The 2026-11 instrument

The protocol version is `2026-11`, in development until its first release, and every row is stamped with the instrument that measured it. There is one method and no switch for another: the harness refuses
to run a cell under any other instrument value. These choices are part of the instrument and are the same for every cell:

- **A warm-up before the sparse search.** Every sparse engine runs 1,000 untimed searches on queries that are not in the timed set, so a query or result cache cannot flatter an engine.
- **The CPU idle state is held for each timed cell**, at the lowest latency target, so a single-client time under a millisecond does not include a core waking up. A cell that cannot take the hold still runs, and the row says so.
- **The dense lane indexes the vector id** on every engine that would otherwise scan for the record it deletes, so the delete column compares indexed lookups.
- **The JVM initial heap follows each engine's own documentation.** The cap on the heap (`-Xmx`) is the same for every JVM engine. Embedded ArcadeDB leaves `-Xms` unset, as the Python bindings document; served ArcadeDB, Elasticsearch and Neo4j keep the initial heap their documentation recommends (initial equal to maximum).
- **Served ArcadeDB is measured with the vendor's official Python driver as the headline**, and the same cell runs again on the lean HTTP client of the harness as a labelled sensitivity row. Bulk loads and transactions stay on the lean client.
- **Large results are read on each engine's documented bulk path** (Arrow for embedded ArcadeDB and DuckDB), with the plain-Python read timed beside it. Small results do not move. The typed read must return the same answer as the plain read, or the cell ends.
- **Memory, disk and IO are read at the end of every phase** of a cell (load, index build, warm-up, queries, and idle), between two timed sections and never inside one. The headline memory is the memory the cell's containers own, the same kernel counter for every engine; the heap figures of JVM engines are context and are not compared across engines. Disk and IO are read the same way for every engine.
- **The dense lane compares engines at matched recall.** After the build, the lane runs one timed pass per search-beam value on the same index (`ef` of 50, 100, 200 and 400 for the HNSW engines; ArangoDB's `nProbe` at 0.5, 1, 2 and 4 times its calibrated value). The headline is the lowest median latency among the passes whose recall@10 reaches 0.95, with the beam that won it. An engine that never reaches 0.95 is printed as `not reached` with its best recall, never as a slower or lower-recall number. Engines with no beam setting run one pass.
- **Product-quantization (PQ) arms are off for now.** They run beside the full-precision and int8 arms only when enabled, with the same setting for every engine that offers it: 32 subspaces of 256 centroids, and a re-rank of the stored vectors where the engine can do one. They stay off until the measured ArcadeDB release carries the upstream PQ fixes (ArcadeData/arcadedb#10516 to #10519), because before them ArcadeDB's SQL search ignores a PQ index and would measure exact search under a PQ label.

The harness documents these choices in [PROTOCOL.md](https://github.com/humemai/arcadedb-embedded-python/blob/main/benchmarks/experiments/PROTOCOL.md) and
[FAIRNESS.md](https://github.com/humemai/arcadedb-embedded-python/blob/main/benchmarks/experiments/FAIRNESS.md).
The 2026-10 instrument was a development version and is retired: nothing is measured with it again, and no result from it is published.

## Reading a result

A bar or a number is only meaningful with its footnotes: the category (in-process or server), the durability class, the scale, the version, and whether any query in the cell was censored.
The results page carries all of these next to every number.

## What this benchmark does not claim

It does not rank databases in general. It measures the tasks listed in each lane on the stated machine and settings. A different workload, scale or tuning can change the order, which is why
the settings are published and why vendors are asked to review them.
