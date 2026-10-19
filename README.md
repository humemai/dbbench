# DBBench

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23481288.svg)](https://doi.org/10.5281/zenodo.23481288)

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

## Citing DBBench

Cite a release of this repository rather than the web page, because the page changes with every measurement. Each release is archived on Zenodo with its own DOI, and GitHub's "Cite this repository" button gives an APA and a BibTeX entry from [CITATION.cff](CITATION.cff).

The DOI for all versions is [10.5281/zenodo.23481288](https://doi.org/10.5281/zenodo.23481288); the Zenodo record lists the DOI of each release, for when the exact numbers matter.

```bibtex
@misc{kim2026dbbench,
  title     = {{DBBench}: an independent, open benchmark of database engines},
  author    = {Kim, Taewoon},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.23481288},
  url       = {https://github.com/humemai/dbbench},
}
```

## Contributing

If a setting we use for your engine differs from what you recommend, open an issue with the engine, the version, what differs and where your documentation says so; see
[Contribute](https://docs.humem.ai/dbbench/latest/contribute/). A corrected configuration is re-run, and the earlier result stays visible in the history.

## License

MIT, see [LICENSE](LICENSE).
