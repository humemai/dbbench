# DBBench

An independent, open benchmark of database engines: the same tasks, on the same machine, with published settings, so anyone can check a result and any vendor can tell us when
a setting is not what they recommend.

- **Results:** <https://humem.ai/research/dbbench>
- **Documentation:** <https://docs.humem.ai/dbbench/> (methodology, engine settings, how to reproduce, how to contribute a correction)

## Lanes

Tables (documents and SQL analytics), graphs (interactive and analytical queries), vectors (dense and sparse), time series, cross-model queries, and lifecycle (durability and restarts).
Engines are compared inside each lane; an engine appears only in the lanes it is built for.

## Status

This repository holds the documentation and, after the first paper, will hold the benchmark code. Until then the code is developed in
[humemai/arcadedb-embedded-python](https://github.com/humemai/arcadedb-embedded-python) under `benchmarks/`, and the results are published on the project page above.
The first documented protocol version is `2026-10`.

## Contributing

If a setting we use for your engine differs from what you recommend, open an issue with the engine, the version, what differs and where your documentation says so; see
[Contribute](https://docs.humem.ai/dbbench/latest/contribute/). A corrected configuration is re-run, and the earlier result stays visible in the history.

## License

MIT, see [LICENSE](LICENSE).
