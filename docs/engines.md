# Engines

!!! note "Generated page"
    Generated from the result rows and the override registry; do not edit by hand. Regenerated at every landing.

    Generated on 2026-10-10. Row set: 1050 rows, sha256 df6b74c069034ff1ef74b57dc19be46d5ce6e67e088a0595c84efb5301b5dbb1 (of the sorted row ids, one per line: the clean rows of the selection and the failed cells listed below).

For every engine in every lane, this page states what we run: the version, the container image digest where a row records one, the durability classes measured, the tiers, every setting a row carries, and each override of an engine's default with the reason. Everything below is read from the result rows and the override registry, so it cannot drift from what was measured. The rules these settings follow are on the [Methodology](methodology.md) page.

The rows are those of the campaign with instrument `2026-10`, selected as the published tables are: the newest clean row of each cell, on the serial CPU set. A failed attempt is listed as the result it is.

## What we run

### Tables

#### ArangoDB: `arangodb_tpc`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1`, `tpch10` | `arangodb:3.12.11` | `arangodb@sha256:563cb2c07af0aead37fd688b58f51d6eb534a3da6163621e130e67d7a55176c4` | `relaxed`, `strict` |

- Durability, `relaxed`: `waitForSync=false (default); RocksDB WAL synced every 100 ms`
- Durability, `strict`: `waitForSync=true: the commit waits for the WAL sync`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### DuckDB: `duckdb`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1`, `tpch10` | `1.5.4` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `fsync at commit, not configurable (DuckDB WAL)`
- Durability, `strict`: `fsync at commit, not configurable (DuckDB WAL)`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `cpuset`: `0-11`

Overrides of the engine's default on this arm:

- DuckDB is given one thread for each CPU the run may use; left alone it sizes its pool from the machine's cores and not from the CPUs the run was given. Override `duckdb_threads`.

#### MongoDB: `mongodb`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1`, `tpch10` | `mongodb 8.2.12` | `mongo@sha256:41afd6e1183f57e4e4d03ab733070671fca8553da2b36f15d6e3fc9760494d17` | `relaxed`, `strict` |

- Durability, `relaxed`: `write concern w=1, j=false (journal flushed every 100 ms)`
- Durability, `strict`: `write concern w=1, j=true (the journal is synced before the ack)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### PostgreSQL: `postgres`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1`, `tpch10` | `PostgreSQL 18.6` | `postgres@sha256:7341002d2b8c7c5bdd7542a671a95b36196c0b5b888daf454ae4fc33ba5346d7` | `relaxed`, `strict` |

- Durability, `relaxed`: `synchronous_commit=off`
- Durability, `strict`: `synchronous_commit=on`; server flags `synchronous_commit=on`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### PostgreSQL (tuned): `postgres_tuned`

This arm is an ablation of one engine's image defaults. It is measured and kept in the rows, and it is not printed in the result tables.

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1`, `tpch10` | `PostgreSQL 18.6` | `postgres@sha256:7341002d2b8c7c5bdd7542a671a95b36196c0b5b888daf454ae4fc33ba5346d7` | `relaxed`, `strict` |

- Durability, `relaxed`: `synchronous_commit=off`
- Durability, `strict`: `synchronous_commit=on`; server flags `synchronous_commit=on`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### SQLite: `sqlite`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1`, `tpch10` | `sqlite 3.46.1` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `WAL, synchronous=NORMAL: synced at checkpoint, not at commit`
- Durability, `strict`: `WAL, synchronous=FULL: synced at every commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `cpuset`: `0-11`

No override from the registry applies to this arm.

#### SurrealDB (embedded): `surrealdb_tpc`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1` | `surrealdb-embedded:2.3.10 (sdk 2.0.0)` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `SurrealKV, SURREAL_SYNC_DATA unset (the default): no sync at commit`
- Durability, `strict`: `SurrealKV, SURREAL_SYNC_DATA=true: sync at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g`
- Setting `cpuset`: `0-11`

No override from the registry applies to this arm.

Failed cells (a failure is a result):

- `tpch10` / `olap` / `relaxed` / rep 1: rc 137, killed for memory: `last line: PHASE build-running t=3369.2s rss=32345.8MiB`
- `tpch10` / `oltp` / `relaxed` / rep 1: rc 137, killed for memory: `last line: PHASE build-running t=3370.7s rss=32500.2MiB`
- `tpch10` / `oltp` / `strict` / rep 1: rc 137, killed for memory: `last line: PHASE build-running t=3371.8s rss=31952.5MiB`

#### SurrealDB (server): `surrealdb_tpc_server`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tpch1`, `tpch10` | `surrealdb-server:3.2.4+20260803.93ab219` | `surrealdb/surrealdb@sha256:6a5002363ff5b000b72a55f985203e951e3175e578002954b0e38f113e48a698` | `relaxed`, `strict` |

- Durability, `relaxed`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`
- Durability, `strict`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`tpch1`); `32g` (`tpch10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

Failed cells (a failure is a result):

- `tpch10` / `olap` / `relaxed` / rep 1: rc 1: `socket.gaierror: [Errno -3] Temporary failure in name resolution`

Registered for this lane, no row yet: ArcadeDB (embedded) (`arcadedb_embedded`, lane `l1tpc`), ArcadeDB (server) (`arcadedb_server`, lane `l1tpc`), ArcadeDB (server, image JVM defaults) (`arcadedb_imgdefaults_server`, lane `l1tpc`).

### Graphs

#### ArangoDB: `arangodb_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `arangodb:3.12.11` | `arangodb@sha256:563cb2c07af0aead37fd688b58f51d6eb534a3da6163621e130e67d7a55176c4` | `relaxed`, `strict` |
| `sf1`, `sf10` | `arangodb:3.12.12` | `arangodb@sha256:4bc086d5050ca7ea11c6d00a36d8b910c838bb54ad553f8c1b715769d3499bcf` | `relaxed`, `strict` |

- Durability, `relaxed`: `waitForSync=false (default); RocksDB WAL synced every 100 ms`
- Durability, `strict`: `waitForSync=true: the commit waits for the WAL sync`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `query_language`: `AQL`

No override from the registry applies to this arm.

#### ArcadeDB (embedded): `arcadedb_graph_embedded`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10`, `sf1full` | `26.10.1`, commit `d36b4ca3a` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `txWalFlush=0 (engine default): no flush at commit`
- Durability, `strict`: `txWalFlush=1: the WAL is flushed with a data-only sync (fdatasync) at every commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`); `32g` (`sf1full`)
- Setting `heap`: `4g` (`sf1`); `12g` (`sf10`); `16g` (`sf1full`)
- Setting `cpuset`: `0-11`
- Setting `query_language`: `openCypher (the engine also has its own SQL)`

No override from the registry applies to this arm.

#### ArcadeDB (server): `arcadedb_graph_server`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10`, `sf1full` | `server:26.10.1 (build d36b4ca3ae4c170abc73598e0dffa2bb58e06621/1791229620009/main)`, commit `d36b4ca3a` | `arcadedb-c25:26.10.1`; digest `sha256:8859153bae95b339a2c5453609fc760b283932e13be419a01055aaf451d221e5` | `relaxed`, `strict` |

- Durability, `relaxed`: `txWalFlush=0 (engine default): no flush at commit (set on the server's JAVA_OPTS by runner.py and recorded as durability_server_flags; the server exposes no read-back)`
- Durability, `strict`: `txWalFlush=1: the WAL is flushed with a data-only sync (fdatasync) at every commit (set on the server's JAVA_OPTS by runner.py and recorded as durability_server_flags; the server exposes no read-back)`; server flags `txWalFlush=1`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`); `32g` (`sf1full`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`sf1`); `24g` (`sf10`); `32g` (`sf1full`)
- Setting `heap`: `4g` (`sf1`); `12g` (`sf10`); `16g` (`sf1full`)
- Setting `server_heap`: `4g` (`sf1`); `12g` (`sf10`); `16g` (`sf1full`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `server_jvm_gc`: `G1`
- Setting `server_jvm_flags`: `-XX:HeapDumpPath=/home/arcadedb/log -XX:+UseCompactObjectHeaders -XX:+UseCompactObjectHeaders -Xms4g -Xmx4g -XX:+HeapDumpOnOutOfMemoryError` (`sf1`); `-XX:HeapDumpPath=/home/arcadedb/log -XX:+UseCompactObjectHeaders -XX:+UseCompactObjectHeaders -Xms12g -Xmx12g -XX:+HeapDumpOnOutOfMemoryError` (`sf10`); `-XX:HeapDumpPath=/home/arcadedb/log -XX:+UseCompactObjectHeaders -XX:+UseCompactObjectHeaders -Xms16g -Xmx16g -XX:+HeapDumpOnOutOfMemoryError` (`sf1full`)
- Setting `query_language`: `openCypher over HTTP (the engine also has its own SQL)`
- Setting `server_query_max_heap_elements`: `5000000`
- Setting `server_query_max_heap_source`: `read from the engine over HTTP (schema:database)`
- Setting `server_http_body_max_bytes`: `68719476736`
- Setting `server_http_body_max_source`: `read from the engine over HTTP (server?mode=default)`
- Setting `server_http_body_max_default`: `104857600`

Overrides of the engine's default on this arm:

- The ArcadeDB server is started with the limit on the records or groups that one sorting, grouping, or distinct query may hold in memory fixed at 5,000,000, while the embedded package leaves that limit at the engine's default, which grows with the heap, so the two deployments can run different limits. Override `arcadedb_query_cap`. Recorded on the rows: `server_query_max_heap_elements`: `5000000`; `server_query_max_heap_source`: `read from the engine over HTTP (schema:database)`.
- The ArcadeDB server that loads its data through the bulk endpoint is started with the limit on one HTTP request body raised to 64 GiB, where the engine's default is 100 MiB. The default refuses the single streamed request that carries the larger graph and cross-model loads (the engine's own message says to raise the limit or split the payload), so the load stays one request, as the embedded arm's is one call. The limit caps how much one request may carry and is no speed setting; the embedded arms have no HTTP body. Override `arcadedb_http_body_limit`. Recorded on the rows: `server_http_body_max_bytes`: `68719476736`; `server_http_body_max_source`: `read from the engine over HTTP (server?mode=default)`; `server_http_body_max_default`: `104857600`.

#### DuckPGQ: `duckpgq_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `duckdb:1.5.4 + duckpgq:f386a6c` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `fsync at commit, not configurable (DuckDB WAL)`
- Durability, `strict`: `fsync at commit, not configurable (DuckDB WAL)`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `duckpgq_threads`: `12`

Overrides of the engine's default on this arm:

- DuckDB is given one thread for each CPU the run may use; left alone it sizes its pool from the machine's cores and not from the CPUs the run was given. Override `duckdb_threads`. Recorded on the rows: `duckpgq_threads`: `12`.

Failed cells (a failure is a result):

- `sf1` / `oltp` / `relaxed` / rep 1: rc 1: `_duckdb.OutOfMemoryException: Out of Memory Error: failed to allocate data of size 8.0 GiB (684.3 MiB/6.3 GiB used)`
- `sf1` / `oltp` / `strict` / rep 1: rc 1: `_duckdb.OutOfMemoryException: Out of Memory Error: failed to allocate data of size 8.0 GiB (684.3 MiB/6.3 GiB used)`
- `sf10` / `oltp` / `relaxed` / rep 1: rc 1: `_duckdb.OutOfMemoryException: Out of Memory Error: failed to allocate data of size 32.0 GiB (5.0 GiB/19.1 GiB used)`
- `sf10` / `oltp` / `strict` / rep 1: rc 1: `_duckdb.OutOfMemoryException: Out of Memory Error: failed to allocate data of size 32.0 GiB (5.0 GiB/19.1 GiB used)`

#### FalkorDB: `falkordb_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `falkordb:4.20.6 (redis 8.6.3)` | `falkordb/falkordb@sha256:0a9fe4d1ee0bdda8e0a85ff36d3f03ca9ab91cd9441c4a836afae32e4014e2f7` | `relaxed`, `strict` |
| `sf1`, `sf10` | `falkordb:6.0.1 (redis 8.10.2)` | `falkordb/falkordb@sha256:2756fdea96acff753e49c459dc279a21a50915d7b2b38bff8a3950d10f984fd8` | `relaxed`, `strict` |

- Durability, `relaxed`: `appendonly=no, RDB save '3600 1 300 100 60 10000' (image default): nothing is synced at commit`
- Durability, `strict`: `appendonly=yes, appendfsync=always: the AOF is fdatasynced at every write`; server flags `appendonly=yes, appendfsync=always`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `query_language`: `Cypher over the Redis protocol`
- Setting `falkordb_appendonly`: `no` (`sf1`, `sf10`); `yes` (`sf1`, `sf10`)
- Setting `falkordb_appendfsync`: `always` (`sf1`, `sf10`); `everysec` (`sf1`, `sf10`)
- Setting `falkordb_save`: `3600 1 300 100 60 10000`

No override from the registry applies to this arm.

#### LadybugDB: `ladybug_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `ladybug:0.20.4` | not recorded in the rows | `relaxed`, `strict` |
| `sf1`, `sf10` | `ladybug:0.21.2` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `fsync at commit, not configurable (LadybugDB WAL)`
- Durability, `strict`: `fsync at commit, not configurable (LadybugDB WAL)`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `query_language`: `Cypher, embedded`

No override from the registry applies to this arm.

#### Memgraph: `memgraph_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `memgraph:3.13.1` | `memgraph/memgraph@sha256:4710bee1ab5b47599876e30f17ae1679d0bbb2262d84dc06641521fecb7c89ce` | `relaxed`, `strict` |

- Durability, `relaxed`: `storage-wal-enabled=true, storage-wal-file-flush-every-n-tx=100000 (image default): the WAL is fsynced every 100,000 transactions, not at commit`
- Durability, `strict`: `storage-wal-file-flush-every-n-tx=1: the WAL is fsynced at every commit`; server flags `storage-wal-file-flush-every-n-tx=1`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `query_language`: `Cypher over Bolt`
- Setting `memgraph_storage_mode`: `IN_MEMORY_TRANSACTIONAL`
- Setting `memgraph_wal_enabled`: `true`

No override from the registry applies to this arm.

#### MongoDB: `mongodb_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `mongodb 8.2.12` | `mongo@sha256:41afd6e1183f57e4e4d03ab733070671fca8553da2b36f15d6e3fc9760494d17` | `relaxed`, `strict` |

- Durability, `relaxed`: `write concern w=1, j=false (journal flushed every 100 ms)`
- Durability, `strict`: `write concern w=1, j=true (the journal is synced before the ack)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `query_language`: `the aggregation pipeline ($lookup joins over both ends of each friendship)`

No override from the registry applies to this arm.

#### Neo4j: `neo4j_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `neo4j:2026.08.1` | `neo4j@sha256:e702d6b535d9d3ae01ee7b132ec87aa40e23d3f0ace82fbfc344e2048cb81960` | `relaxed`, `strict` |

- Durability, `relaxed`: `fsync at commit, not configurable (no durability setting in SHOW SETTINGS at 2026.08.1)`
- Durability, `strict`: `fsync at commit, not configurable (no durability setting in SHOW SETTINGS at 2026.08.1)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `heap`: `4g` (`sf1`); `12g` (`sf10`)
- Setting `server_heap`: `4g` (`sf1`); `12g` (`sf10`)
- Setting `server_pagecache`: `3.0g` (`sf1`); `11.0g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `query_language`: `Cypher over Bolt`
- Setting `neo4j_pagecache`: `3.00GiB` (`sf1`); `11.00GiB` (`sf10`)
- Setting `neo4j_checkpoint_interval`: `5s`
- Setting `neo4j_checkpoint_interval_default`: `15m`

Overrides of the engine's default on this arm:

- Neo4j's page cache is sized from the memory the run was given, what is left after its heap and a fixed reserve, where its image would set one small fixed size whatever the container holds. Override `neo4j_pagecache`. Recorded on the rows: `neo4j_pagecache`: `3.00GiB` (`sf1`); `11.00GiB` (`sf10`).
- Neo4j checkpoints its store every 5 seconds, where its default is every 15 minutes, so that the disk reading taken after a run finds the data on disk. Override `neo4j_checkpoint`. Recorded on the rows: `neo4j_checkpoint_interval`: `5s`; `neo4j_checkpoint_interval_default`: `15m`.

#### SurrealDB (embedded): `surrealdb_graph`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `surrealdb-embedded:2.3.10 (sdk 2.0.0)` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `SurrealKV, SURREAL_SYNC_DATA unset (the default): no sync at commit`
- Durability, `strict`: `SurrealKV, SURREAL_SYNC_DATA=true: sync at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `query_language`: `SurrealQL, embedded`

No override from the registry applies to this arm.

#### SurrealDB (server): `surrealdb_graph_server`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `sf1`, `sf10` | `surrealdb-server:3.2.4+20260803.93ab219` | `surrealdb/surrealdb@sha256:6a5002363ff5b000b72a55f985203e951e3175e578002954b0e38f113e48a698` | `relaxed`, `strict` |

- Durability, `relaxed`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`; `RocksDB, sync=never: no sync at commit (the OS flushes)`
- Durability, `strict`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`; `RocksDB, sync=every (the engine default): synced at every commit`; server flags `sync=every`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`sf1`); `24g` (`sf10`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `query_language`: `SurrealQL over WebSocket`
- Setting `surreal_sync_mode`: `every transaction commit` (`sf1`, `sf10`); `never` (`sf1`, `sf10`)

No override from the registry applies to this arm.

Registered for this lane, no row yet: PostgreSQL + AGE (`pgage_graph`, lane `l2`).

### Vectors

#### ArangoDB: `arangodb_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small` | `arangodb:3.12.11` | `arangodb@sha256:563cb2c07af0aead37fd688b58f51d6eb534a3da6163621e130e67d7a55176c4` | `relaxed` |

- Durability, `relaxed`: `waitForSync=false (default); RocksDB WAL synced every 100 ms`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g`
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

#### Chroma: `chroma_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `1.5.9` | `dbbench:dense` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

#### DuckDB VSS: `duckdb_vss_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `1.5.4` | `dbbench:dense` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `fsync at commit, not configurable (DuckDB WAL)`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `quantization`: `fp32`

Overrides of the engine's default on this arm:

- DuckDB is given one thread for each CPU the run may use; left alone it sizes its pool from the machine's cores and not from the CPUs the run was given. Override `duckdb_threads`.
- DuckDB's vector rows keep their HNSW index in the database through a persistence feature that its vector extension still labels experimental and that has to be switched on for the index to be stored at all. Override `duckdb_vss`.

#### LanceDB: `lancedb_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `0.39.0` | `dbbench:dense` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `quantization`: `INT8`

No override from the registry applies to this arm.

#### Milvus: `milvus_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `milvus:3.0.1` | `milvusdb/milvus@sha256:2b2fc2cf499ad897c93d4b90ee251646f718522845261a342d74d7c0c66bb274` | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

#### Milvus: `milvus_dense_int8`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `milvus:3.0.1` | `milvusdb/milvus@sha256:2b2fc2cf499ad897c93d4b90ee251646f718522845261a342d74d7c0c66bb274` | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `INT8`

No override from the registry applies to this arm.

#### MongoDB: `mongodb_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `mongodb 8.2.12 + MongoDb Search Community Version 1.70.4 at localhost:27028` | `dbbench:mongo-search` | `relaxed` |

- Durability, `relaxed`: `write concern w=1, j=false (journal flushed every 100 ms)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

#### Neo4j: `neo4j_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `neo4j:2026.08.1` | `neo4j@sha256:e702d6b535d9d3ae01ee7b132ec87aa40e23d3f0ace82fbfc344e2048cb81960` | `relaxed` |

- Durability, `relaxed`: `fsync at commit, not configurable (no durability setting in SHOW SETTINGS at 2026.08.1)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `heap`: `8g` (`small`); `24g` (`deep10m`)
- Setting `server_heap`: `8g` (`small`); `24g` (`deep10m`)
- Setting `server_pagecache`: `7.0g` (`small`); `11.0g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `fp32`

Overrides of the engine's default on this arm:

- Neo4j's page cache is sized from the memory the run was given, what is left after its heap and a fixed reserve, where its image would set one small fixed size whatever the container holds. Override `neo4j_pagecache`.

#### pgvector: `pgvector_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `pgvector:0.8.6 on PostgreSQL 18.6` | `pgvector/pgvector@sha256:1d50c689b0a6511b9ea0a15615281c81a59fd04a08eb35057ec8646fb3a2118a` | `relaxed` |

- Durability, `relaxed`: `synchronous_commit=off`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

#### Qdrant: `qdrant_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `qdrant:1.19.1` | `qdrant/qdrant@sha256:0699e7733a6fa7fa7f6b95dcbed84ebb04584110da525cdfdef9f305c4f57738` | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

#### Qdrant: `qdrant_dense_int8`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `qdrant:1.19.1` | `qdrant/qdrant@sha256:0699e7733a6fa7fa7f6b95dcbed84ebb04584110da525cdfdef9f305c4f57738` | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `INT8`

No override from the registry applies to this arm.

#### sqlite-vec: `sqlite_vec_dense`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small`, `deep10m` | `0.1.9` | `dbbench:dense` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `WAL, synchronous=NORMAL: synced at checkpoint, not at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`small`); `36g` (`deep10m`)
- Setting `cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

#### sqlite-vec: `sqlite_vec_dense_int8`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `deep10m` | `0.1.9` | `dbbench:dense` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `WAL, synchronous=NORMAL: synced at checkpoint, not at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `36g`
- Setting `cpuset`: `0-11`
- Setting `quantization`: `INT8`

No override from the registry applies to this arm.

#### SurrealDB (embedded): `surrealdb_dense`

No clean row yet; the failed cells below are all there is.

Failed cells (a failure is a result):

- `small` / `search` / `relaxed` / rep 1: rc -1: `timeout_after_7200s`
- `deep10m` / `search` / `relaxed` / rep 1: rc -1: `timeout_after_28800s`

#### SurrealDB (server): `surrealdb_dense_server`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `small` | `surrealdb-server:3.2.4+20260803.93ab219` | `surrealdb/surrealdb@sha256:6a5002363ff5b000b72a55f985203e951e3175e578002954b0e38f113e48a698` | `relaxed` |

- Durability, `relaxed`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g`
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`
- Setting `quantization`: `fp32`

No override from the registry applies to this arm.

Failed cells (a failure is a result):

- `deep10m` / `search` / `relaxed` / rep 1: rc 1: `socket.gaierror: [Errno -3] Temporary failure in name resolution`

#### Elasticsearch: `elasticsearch_sparse`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tiny`, `small`, `medium` | `9.5.4` | `docker.elastic.co/elasticsearch/elasticsearch@sha256:33178ff49e06da93e3c51c5d87401b26e7a6dea0ef9bb26539cfddc46478b420` | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`tiny`); `16g` (`small`); `32g` (`medium`)
- Setting `heap`: `4g` (`tiny`); `8g` (`small`); `16g` (`medium`)
- Setting `server_heap`: `4g` (`tiny`); `8g` (`small`); `16g` (`medium`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

Overrides of the engine's default on this arm:

- Elasticsearch runs with its security features switched off, so none of its requests pays for authentication or encryption; its image turns both on unless told otherwise. Override `es_security`.
- Elasticsearch's index is created with no replica, because a single-node cluster has nowhere to place one and the index would otherwise stay yellow. Override `es_replicas`.

#### Milvus: `milvus_sparse`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tiny`, `small`, `medium` | `milvus:3.0.1` | `milvusdb/milvus@sha256:2b2fc2cf499ad897c93d4b90ee251646f718522845261a342d74d7c0c66bb274` | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`tiny`); `16g` (`small`); `32g` (`medium`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### pgvector: `pgvector_sparse`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tiny`, `small`, `medium` | `pgvector:0.8.6 on PostgreSQL 18.6` | `pgvector/pgvector@sha256:1d50c689b0a6511b9ea0a15615281c81a59fd04a08eb35057ec8646fb3a2118a` | `relaxed` |

- Durability, `relaxed`: `synchronous_commit=off`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`tiny`); `16g` (`small`); `32g` (`medium`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### Qdrant: `qdrant_sparse`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `tiny`, `small`, `medium` | `qdrant:1.19.1` | `qdrant/qdrant@sha256:0699e7733a6fa7fa7f6b95dcbed84ebb04584110da525cdfdef9f305c4f57738` | `relaxed` |

- Durability, `relaxed`: `engine default; no transactional write timed on this lane`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `8g` (`tiny`); `16g` (`small`); `32g` (`medium`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

Registered for this lane, no row yet: ArangoDB (`arangodb_dense_int8`, lane `l3d`), ArcadeDB (embedded) (`arcadedb_dense_embedded`, lane `l3d`), ArcadeDB (embedded) (`arcadedb_dense_embedded_int8`, lane `l3d`), ArcadeDB (embedded, fp32) (`arcadedb_sparse_embedded_fp32`, lane `l3s`), ArcadeDB (embedded, int8) (`arcadedb_sparse_embedded`, lane `l3s`), ArcadeDB (embedded, no settle step) (`arcadedb_sparse_embedded_nocompact`, lane `l3s`), ArcadeDB (server) (`arcadedb_dense_server`, lane `l3d`), ArcadeDB (server) (`arcadedb_dense_server_int8`, lane `l3d`), ArcadeDB (server, fp32) (`arcadedb_sparse_server_fp32`, lane `l3s`), ArcadeDB (server, int8) (`arcadedb_sparse_server`, lane `l3s`), Elasticsearch (`elasticsearch_dense`, lane `l3d`), Elasticsearch (`elasticsearch_dense_int8`, lane `l3d`), FalkorDB (`falkordb_dense`, lane `l3d`), LadybugDB (`ladybug_dense`, lane `l3d`), LanceDB (`lancedb_dense_fp32`, lane `l3d`), Memgraph (`memgraph_dense`, lane `l3d`), Memgraph (`memgraph_dense_int8`, lane `l3d`), MongoDB (`mongodb_dense_int8`, lane `l3d`), Neo4j (`neo4j_dense_int8`, lane `l3d`), Qdrant (`qdrant_sparse_uint8`, lane `l3s`).

### Time series

#### ArangoDB: `arangodb_ts`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100`, `ts1000` | `arangodb:3.12.11` (from `backend_version`) | `arangodb@sha256:563cb2c07af0aead37fd688b58f51d6eb534a3da6163621e130e67d7a55176c4` | `relaxed` |

- Durability, `relaxed`: `waitForSync=false (default); RocksDB WAL synced every 100 ms`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`ts100`); `32g` (`ts1000`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### DuckDB: `duckdb`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100`, `ts1000` | `duckdb 1.5.4` (from `backend_version`) | `dbbench:duckdb` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `fsync at commit, not configurable (DuckDB WAL)`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`ts100`); `32g` (`ts1000`)
- Setting `cpuset`: `0-11`

Overrides of the engine's default on this arm:

- DuckDB is given one thread for each CPU the run may use; left alone it sizes its pool from the machine's cores and not from the CPUs the run was given. Override `duckdb_threads`.

#### MongoDB: `mongodb`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100`, `ts1000` | `mongodb 8.2.12` (from `backend_version`) | `mongo@sha256:41afd6e1183f57e4e4d03ab733070671fca8553da2b36f15d6e3fc9760494d17` | `relaxed` |

- Durability, `relaxed`: `write concern w=1, j=false (journal flushed every 100 ms)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`ts100`); `32g` (`ts1000`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### QuestDB: `questdb`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100`, `ts1000` | `questdb Build Information: QuestDB 10.0.1, JDK 25.0.2, Commit Hash 7a391566ac827e0d8c269b91f2415c16b0a32a84` (from `backend_version`) | `questdb/questdb@sha256:931af4156771ee2948ec2431988c3a93b257487d993f1b74771545c8dce5c23d` | `relaxed` |

- Durability, `relaxed`: `cairo.commit.mode=nosync (default): no fsync at commit`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`ts100`); `32g` (`ts1000`)
- Setting `heap`: `8g` (`ts100`); `16g` (`ts1000`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### SQLite: `sqlite`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100`, `ts1000` | `sqlite 3.46.1` (from `backend_version`) | `dbbench:client` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `WAL, synchronous=NORMAL: synced at checkpoint, not at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g` (`ts100`); `32g` (`ts1000`)
- Setting `cpuset`: `0-11`

No override from the registry applies to this arm.

#### SurrealDB (embedded): `surrealdb_ts`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100` | `surrealdb-embedded:2.3.10 (sdk 2.0.0)` (from `backend_version`) | `dbbench:client` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `SurrealKV, SURREAL_SYNC_DATA unset (the default): no sync at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `16g`
- Setting `cpuset`: `0-11`

No override from the registry applies to this arm.

Failed cells (a failure is a result):

- `ts1000` / `ingest` / `relaxed` / rep 1: rc 137, killed for memory: `last line: PHASE ingest-running t=1923.0s rss=32510.0MiB`

#### SurrealDB (server): `surrealdb_ts_server`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100`, `ts1000` | `surrealdb-server:3.2.4+20260803.93ab219` (from `backend_version`) | `surrealdb/surrealdb@sha256:6a5002363ff5b000b72a55f985203e951e3175e578002954b0e38f113e48a698` | `relaxed` |

- Durability, `relaxed`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`ts100`); `32g` (`ts1000`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### TimescaleDB: `timescaledb`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `ts100`, `ts1000` | `timescaledb 2.30.1 on PostgreSQL 18.6 on x86_64-pc-linux-musl, compiled by gcc` (from `backend_version`) | `timescale/timescaledb@sha256:f7036933154c52dbc500f7b08ff8e28404a8ccabbf8ce3528142cde6ab253eef` | `relaxed` |

- Durability, `relaxed`: `synchronous_commit=off`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `8g`
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `16g` (`ts100`); `32g` (`ts1000`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

Registered for this lane, no row yet: ArcadeDB (`arcadedb_ts_doc`, lane `l4`), ArcadeDB (`arcadedb_ts_doc_server`, lane `l4`), ArcadeDB (`arcadedb_ts_native`, lane `l4`), ArcadeDB (`arcadedb_ts_native_server`, lane `l4`), PostgreSQL (`postgres_ts`, lane `l4`).

### Cross-model

#### ArangoDB: `arangodb_e2`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `e2`, `e2_500k` | `arangodb:3.12.11` | `arangodb@sha256:563cb2c07af0aead37fd688b58f51d6eb534a3da6163621e130e67d7a55176c4` | `relaxed`, `strict` |

- Durability, `relaxed`: `waitForSync=false (default); RocksDB WAL synced every 100 ms`
- Durability, `strict`: `waitForSync=true: the commit waits for the WAL sync`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### MongoDB: `mongodb_e2`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `e2`, `e2_500k` | `mongodb 8.2.12 + MongoDb Search Community Version 1.70.4 at localhost:27028` | `dbbench:mongo-search`; digest `sha256:447135ddc03eed653fd613e2a9a56ac6623ad4c3877ae6b9f9e240aa8be97a72` | `strict` |
| `e2`, `e2_500k` | `mongodb 8.2.12 + MongoDb Search Community Version 1.70.4 at localhost:27028` | `dbbench:mongo-search`; digest `sha256:64bf722bc986a217881308c2ea6bca134c04f80fe86ec49d8f2caf8a511d6eec` | `relaxed` |

- Durability, `relaxed`: `write concern w=1, j=false (journal flushed every 100 ms)`
- Durability, `strict`: `write concern w=1, j=true (the journal is synced before the ack)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### Neo4j (vector index): `neo4j_e2`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `e2`, `e2_500k` | `neo4j:2026.08.1` | `neo4j@sha256:e702d6b535d9d3ae01ee7b132ec87aa40e23d3f0ace82fbfc344e2048cb81960` | `relaxed`, `strict` |

- Durability, `relaxed`: `fsync at commit, not configurable (no durability setting in SHOW SETTINGS at 2026.08.1)`
- Durability, `strict`: `fsync at commit, not configurable (no durability setting in SHOW SETTINGS at 2026.08.1)`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `heap`: `6g` (`e2`); `16g` (`e2_500k`)
- Setting `server_heap`: `6g` (`e2`); `16g` (`e2_500k`)
- Setting `server_pagecache`: `5.0g` (`e2`); `15.0g` (`e2_500k`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

Overrides of the engine's default on this arm:

- Neo4j's page cache is sized from the memory the run was given, what is left after its heap and a fixed reserve, where its image would set one small fixed size whatever the container holds. Override `neo4j_pagecache`.

#### PostgreSQL + pgvector + AGE: `pg_age_e2`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `e2`, `e2_500k` | `PostgreSQL 18.6 + pgvector:0.8.6 + age:1.8.0` | `dbbench:pg-age`; digest `sha256:1ab18fe1d6c24dd0bf8022f3ac3ecf9432a153a184065701b332732e1aeba3bd` | `relaxed` |
| `e2`, `e2_500k` | `PostgreSQL 18.6 + pgvector:0.8.6 + age:1.8.0` | `dbbench:pg-age`; digest `sha256:cbcf2d6975b79bbae4564ea62ee0a28396fb666276123a9e0abc24e7044f9843` | `strict` |

- Durability, `relaxed`: `synchronous_commit=off`
- Durability, `strict`: `synchronous_commit=on`; server flags `synchronous_commit=on`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

#### Qdrant + Neo4j (no shared transaction): `composed_qdrant_neo4j`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `e2`, `e2_500k` | `qdrant-local:1.19.1+neo4j:2026.08.1` | `neo4j@sha256:e702d6b535d9d3ae01ee7b132ec87aa40e23d3f0ace82fbfc344e2048cb81960` | `relaxed`, `strict` |

- Durability, `relaxed`: `fsync at commit, not configurable (no durability setting in SHOW SETTINGS at 2026.08.1); Qdrant WAL at its default`
- Durability, `strict`: `fsync at commit, not configurable (no durability setting in SHOW SETTINGS at 2026.08.1); Qdrant WAL at its default`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `heap`: `6g` (`e2`); `16g` (`e2_500k`)
- Setting `server_heap`: `6g` (`e2`); `16g` (`e2_500k`)
- Setting `server_pagecache`: `5.0g` (`e2`); `15.0g` (`e2_500k`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

Overrides of the engine's default on this arm:

- Neo4j's page cache is sized from the memory the run was given, what is left after its heap and a fixed reserve, where its image would set one small fixed size whatever the container holds. Override `neo4j_pagecache`.
- Neo4j checkpoints its store at a short fixed interval instead of its much longer default, so that the disk reading taken after a run finds the data on disk. Override `neo4j_checkpoint`.

#### SurrealDB (embedded): `surrealdb_e2`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `e2` | `surrealdb-embedded:2.3.10 (sdk 2.0.0)` | not recorded in the rows | `relaxed`, `strict` |

- Durability, `relaxed`: `SurrealKV, SURREAL_SYNC_DATA unset (the default): no sync at commit`
- Durability, `strict`: `SurrealKV, SURREAL_SYNC_DATA=true: sync at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `12g`
- Setting `cpuset`: `0-11`

No override from the registry applies to this arm.

Failed cells (a failure is a result):

- `e2_500k` / `atomicity` / `relaxed` / rep 1: rc -1: `timeout_after_7200s`
- `e2_500k` / `hybrid` / `relaxed` / rep 1: rc -1: `timeout_after_7200s`
- `e2_500k` / `hybrid` / `strict` / rep 1: rc -1: `timeout_after_7200s`

#### SurrealDB (server): `surrealdb_e2_server`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `e2`, `e2_500k` | `surrealdb-server:3.2.4+20260803.93ab219` | `surrealdb/surrealdb@sha256:6a5002363ff5b000b72a55f985203e951e3175e578002954b0e38f113e48a698` | `relaxed`, `strict` |

- Durability, `relaxed`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`
- Durability, `strict`: `RocksDB at the engine default; SurrealDB 3.2.4 exposes no sync setting and the behaviour at commit is not verified`
- Setting `topology`: `client_server`
- Setting `mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `client_mem_cap`: `8g`
- Setting `server_mem_cap`: `12g` (`e2`); `32g` (`e2_500k`)
- Setting `cpuset`: `0-11`
- Setting `server_cpuset`: `0-11`

No override from the registry applies to this arm.

Registered for this lane, no row yet: ArcadeDB (one transaction) (`arcadedb_e2`, lane `e2`), ArcadeDB (server, one transaction) (`arcadedb_e2_server`, lane `e2`), DuckDB (vss + DuckPGQ) (`duckdb_e2`, lane `e2`), LadybugDB (vector extension) (`ladybug_e2`, lane `e2`), Memgraph (vector index) (`memgraph_e2`, lane `e2`).

### Lifecycle

#### SurrealDB (embedded): `surrealdb_lifecycle`

| Tiers | Version | Image | Durability classes |
|---|---|---|---|
| `lc10k`, `lc100k`, `lc1m`, `lc10m` | `surrealdb-embedded:2.3.10 (sdk 2.0.0)` | `dbbench:client` (a tag; no digest in the rows) | `relaxed` |

- Durability, `relaxed`: `SurrealKV, SURREAL_SYNC_DATA unset (the default): no sync at commit`
- Setting `topology`: `embedded`
- Setting `mem_cap`: `8g` (`lc10k`, `lc100k`); `24g` (`lc1m`); `28g` (`lc10m`)
- Setting `cpuset`: `0-11`
- Setting `store`: `surrealkv`

No override from the registry applies to this arm.

Failed cells (a failure is a result):

- `lc1m` / `vector` / `relaxed` / rep 1: rc -1: `timeout_after_28800s`
- `lc10m` / `doc_idx10` / `relaxed` / rep 1: rc 137, killed for memory: `container exited 137 with no output (cgroup OOM kill: raise the envelope or bound the harness's peak memory)`
- `lc10m` / `graph` / `relaxed` / rep 1: rc 137, killed for memory: `container exited 137 with no output (cgroup OOM kill: raise the envelope or bound the harness's peak memory)`
- `lc10m` / `vector` / `relaxed` / rep 1: rc 137, killed for memory: `container exited 137 with no output (cgroup OOM kill: raise the envelope or bound the harness's peak memory)`

Registered for this lane, no row yet: ArcadeDB (`arcadedb_e4`, lane `e4`), ArcadeDB (embedded) (`arcadedb_embedded`, lane `lifecycle`), ArcadeDB (server) (`arcadedb_server`, lane `lifecycle`).

## Gaps in the rows

What the rows do not yet say, found by reading them. An empty list would mean the rows are complete.

- Every lane has at least one row.
- Arms registered in the runner with no row yet:
    - lane e2: arcadedb_e2
    - lane e2: arcadedb_e2_server
    - lane e2: duckdb_e2
    - lane e2: ladybug_e2
    - lane e2: memgraph_e2
    - lane e4: arcadedb_e4
    - lane l1tpc: arcadedb_embedded
    - lane l1tpc: arcadedb_imgdefaults_server
    - lane l1tpc: arcadedb_server
    - lane l2: pgage_graph
    - lane l3d: arangodb_dense_int8
    - lane l3d: arcadedb_dense_embedded
    - lane l3d: arcadedb_dense_embedded_int8
    - lane l3d: arcadedb_dense_server
    - lane l3d: arcadedb_dense_server_int8
    - lane l3d: elasticsearch_dense
    - lane l3d: elasticsearch_dense_int8
    - lane l3d: falkordb_dense
    - lane l3d: ladybug_dense
    - lane l3d: lancedb_dense_fp32
    - lane l3d: memgraph_dense
    - lane l3d: memgraph_dense_int8
    - lane l3d: mongodb_dense_int8
    - lane l3d: neo4j_dense_int8
    - lane l3s: arcadedb_sparse_embedded
    - lane l3s: arcadedb_sparse_embedded_fp32
    - lane l3s: arcadedb_sparse_embedded_nocompact
    - lane l3s: arcadedb_sparse_server
    - lane l3s: arcadedb_sparse_server_fp32
    - lane l3s: qdrant_sparse_uint8
    - lane l4: arcadedb_ts_doc
    - lane l4: arcadedb_ts_doc_server
    - lane l4: arcadedb_ts_native
    - lane l4: arcadedb_ts_native_server
    - lane l4: postgres_ts
    - lane lifecycle: arcadedb_embedded
    - lane lifecycle: arcadedb_server
- Arms with a recorded failure and no clean row:
    - SurrealDB (embedded) (surrealdb_dense), lane l3d
- Override stamps that at least one row lacks or contradicts:
    - DuckDB (duckdb), lane l1tpc: `duckdb_threads` for `duckdb_threads` is missing, tier tpch1
    - DuckDB (duckdb), lane l1tpc: `duckdb_threads` for `duckdb_threads` is missing, tier tpch10
    - DuckDB (duckdb), lane l4: `duckdb_threads` for `duckdb_threads` is missing, tier ts100
    - DuckDB (duckdb), lane l4: `duckdb_threads` for `duckdb_threads` is missing, tier ts1000
    - DuckDB VSS (duckdb_vss_dense), lane l3d: `duckdb_hnsw_persistence` for `duckdb_vss` is missing, tier deep10m
    - DuckDB VSS (duckdb_vss_dense), lane l3d: `duckdb_hnsw_persistence` for `duckdb_vss` is missing, tier small
    - DuckDB VSS (duckdb_vss_dense), lane l3d: `duckdb_threads` for `duckdb_threads` is missing, tier deep10m
    - DuckDB VSS (duckdb_vss_dense), lane l3d: `duckdb_threads` for `duckdb_threads` is missing, tier small
    - Elasticsearch (elasticsearch_sparse), lane l3s: `es_replicas` for `es_replicas` is missing, tier medium
    - Elasticsearch (elasticsearch_sparse), lane l3s: `es_replicas` for `es_replicas` is missing, tier small
    - Elasticsearch (elasticsearch_sparse), lane l3s: `es_replicas` for `es_replicas` is missing, tier tiny
    - Elasticsearch (elasticsearch_sparse), lane l3s: `es_security_enabled` for `es_security` is missing, tier medium
    - Elasticsearch (elasticsearch_sparse), lane l3s: `es_security_enabled` for `es_security` is missing, tier small
    - Elasticsearch (elasticsearch_sparse), lane l3s: `es_security_enabled` for `es_security` is missing, tier tiny
    - Neo4j (neo4j_dense), lane l3d: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier deep10m
    - Neo4j (neo4j_dense), lane l3d: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier small
    - Neo4j (neo4j_graph), lane l2: `neo4j_checkpoint_interval` for `neo4j_checkpoint` is missing, tier sf1
    - Neo4j (neo4j_graph), lane l2: `neo4j_checkpoint_interval` for `neo4j_checkpoint` is missing, tier sf10
    - Neo4j (neo4j_graph), lane l2: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier sf1
    - Neo4j (neo4j_graph), lane l2: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier sf10
    - Neo4j (vector index) (neo4j_e2), lane e2: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier e2
    - Neo4j (vector index) (neo4j_e2), lane e2: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier e2_500k
    - Qdrant + Neo4j (no shared transaction) (composed_qdrant_neo4j), lane e2: `neo4j_checkpoint_interval` for `neo4j_checkpoint` is missing, tier e2
    - Qdrant + Neo4j (no shared transaction) (composed_qdrant_neo4j), lane e2: `neo4j_checkpoint_interval` for `neo4j_checkpoint` is missing, tier e2_500k
    - Qdrant + Neo4j (no shared transaction) (composed_qdrant_neo4j), lane e2: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier e2
    - Qdrant + Neo4j (no shared transaction) (composed_qdrant_neo4j), lane e2: `neo4j_pagecache` for `neo4j_pagecache` is missing, tier e2_500k
- Rows with no image digest:
    - ArcadeDB (embedded) (arcadedb_graph_embedded), lane l2: the rows carry no image field
    - Chroma (chroma_dense), lane l3d: the rows carry a tag only
    - DuckDB (duckdb), lane l1tpc: the rows carry no image field
    - DuckDB (duckdb), lane l4: the rows carry a tag only
    - DuckDB VSS (duckdb_vss_dense), lane l3d: the rows carry a tag only
    - DuckPGQ (duckpgq_graph), lane l2: the rows carry no image field
    - LadybugDB (ladybug_graph), lane l2: the rows carry no image field
    - LanceDB (lancedb_dense), lane l3d: the rows carry a tag only
    - MongoDB (mongodb_dense), lane l3d: the rows carry a tag only
    - SQLite (sqlite), lane l1tpc: the rows carry no image field
    - SQLite (sqlite), lane l4: the rows carry a tag only
    - SurrealDB (embedded) (surrealdb_e2), lane e2: the rows carry no image field
    - SurrealDB (embedded) (surrealdb_graph), lane l2: the rows carry no image field
    - SurrealDB (embedded) (surrealdb_lifecycle), lane lifecycle: the rows carry a tag only
    - SurrealDB (embedded) (surrealdb_tpc), lane l1tpc: the rows carry no image field
    - SurrealDB (embedded) (surrealdb_ts), lane l4: the rows carry a tag only
    - sqlite-vec (sqlite_vec_dense), lane l3d: the rows carry a tag only
    - sqlite-vec (sqlite_vec_dense_int8), lane l3d: the rows carry a tag only
- Tiers whose rows mix versions:
    - ArangoDB (arangodb_graph), lane l2: sf1, sf10
    - FalkorDB (falkordb_graph), lane l2: sf1, sf10
    - LadybugDB (ladybug_graph), lane l2: sf1, sf10

## How to tell us a setting is wrong

If a setting we use for your engine differs from what you recommend for this task, open an issue (see [Contribute](contribute.md)) with the engine, the version, the setting, and a link to your documentation.
A corrected configuration is re-run on the same machine and published beside the earlier result, with the reason for the change.
