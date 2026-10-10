# Reproduce

Every published number can be repeated on your own hardware. The benchmark runs each engine in a container pinned by image digest (or an installed package pinned by version) and writes one result
row per measurement; the tables on the results page are generated from those rows.

!!! note "Status"
    The reproduction instructions move here with the benchmark code. Until then the code and its instructions are in
    [humemai/arcadedb-embedded-python](https://github.com/humemai/arcadedb-embedded-python) under `benchmarks/`.

A reproduction is comparable when it keeps the memory cap, the durability class and the corpus the same, and compares engines on the same machine. Absolute times on different hardware will differ;
the order of engines and the size of the gaps are what a reproduction should be compared on.
