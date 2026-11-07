# Related work

Four academic benchmarks already address multi-model databases.

- [UniBench](https://www.helsinki.fi/en/researchgroups/unified-database-management-systems-udbms/research/unibench-towards-benchmarking-multi-model-dbms), from the University of Helsinki: relational, JSON, XML, key-value, and graph data in one social commerce scenario, with multi-model queries and transactions.
- [M2Bench](https://www.vldb.org/pvldb/vol16/p747-moon.pdf), from Seoul National University: analytic tasks over relational, document, property graph, and array data, run on polyglot persistence (MySQL, MongoDB, Neo4j, and SciDB), ArangoDB, and AgensGraph.
- [MMSBench-Net](https://ceur-ws.org/Vol-3714/paper6.pdf), from the University of Basel: a scenario-based benchmark over relational, document, and graph data, used to compare Polypheny and SurrealDB.
- [GRBench](https://arxiv.org/abs/2608.31027), by Liu and colleagues: relational and graph data together, evaluated on relational extensions, multi-model databases, and dedicated graph-relational systems.

None of the four lists vectors or time series among its data models.

## What MMDBBench does differently

- It adds vectors and time series to the models a multi-model engine serves.
- It runs a specialist database for each model as a baseline, so the question is what one engine gains or gives up against a specialist, not only how two multi-model systems compare.
- Tasks are written in SQL, Cypher, and each engine's native language, and the answers are checked between engines.
- It runs on one platform, x86 Linux, with pinned engine versions and published settings.
- The raw result rows are open: see [Result rows](results-schema.md).

These descriptions come from each benchmark's own page or paper, linked above. They say what each one states about itself, not how it performs.
