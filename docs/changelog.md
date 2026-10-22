# Changelog

Changes to the protocol, newest first. Engine versions are not listed here; they are on every result row.

## 2026-11 (in development)

The protocol version, in development until its first release. The method is described on the [Methodology](methodology.md) page.

Method changes made while it is in development, before any result is published with them:

- Served ArcadeDB leaves the initial heap (`-Xms`) unset, like embedded ArcadeDB. Neo4j and Elasticsearch keep a pinned initial heap, as their vendors recommend.
- Neo4j's heap and page cache come from its own `neo4j-admin server memory-recommendation` for each memory cap. Elasticsearch's heap is the smaller of the tier heap, 50% of the cap and 26 GiB.
- Milvus runs as 3.0.3 on the vendor's Docker Compose standalone (three containers sharing the cell's memory cap), ingests by bulk import, waits for every segment to be flushed and the index to be finished before timed searches, and records the storage mode, the output fields and the filter. Storage V3 is a sensitivity setting.

## 2026-10

A development release, superseded by 2026-11 before any comparison was published from it.
