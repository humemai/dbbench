# DBBench

DBBench is an independent, open benchmark of database engines. It runs the same tasks on the same machine with published settings, records every result with the exact engine version
that produced it, and keeps the history, so a number can always be traced and a change can always be seen.

!!! note "Status"
    The first documented protocol version is `2026-10`. The benchmark code is still developed in
    [humemai/arcadedb-embedded-python](https://github.com/humemai/arcadedb-embedded-python) (`benchmarks/`) and moves into this repository after its first paper. The live results are on
    the [project page](https://humem.ai/projects/dbbench); these documents describe how they are produced.

## Lanes

| lane | what it measures |
|---|---|
| Tables | documents and SQL analytics |
| Graphs | interactive queries and analytical queries over a social graph |
| Vectors | dense and sparse similarity search |
| Time series | ingestion and the usual monitoring queries |
| Cross-model | queries that combine more than one data model in one transaction |
| Lifecycle | durability, restarts and the cost of staying consistent |

Every engine is compared only in the lanes it is built for. An in-process engine and a server engine are different categories and are labelled as such.

## Where to go next

- [Methodology](methodology.md): the rules every run follows.
- [Engines](engines.md): what we run for each engine, and how to tell us it is wrong.
- [Reproduce](reproduce.md): how to repeat a result on your own hardware.
- [Result rows](results-schema.md): what one published measurement contains.
- [Contribute](contribute.md): corrections, new engines, new queries.
- [Changelog](changelog.md): changes to the protocol.
