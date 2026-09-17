# Linkiir Data Adapters

Databases and analytics targets: relational engines, NoSQL engines, cloud warehouses, search, and BI dataset push.

**Catalog id:** `lkdata` — every node template in this catalog carries a `LKDATA_` node type id.
**Published adapters:** 0 &nbsp;•&nbsp; **Published libraries:** 0

---

## Subscribe

In Grid, go to **Settings → Catalogs → Subscribe** and paste:

```
https://github.com/Linkiir/linkiir-data-adapters
```

This is a public repository, so Grid clones it anonymously and no SSH key is needed. Leave **Ref** at `main` to track the latest published content.

Install it under the name **`linkiir-data-adapters`**. The install name is recorded on every node built from this catalog, so keeping it consistent makes a node's origin readable in support.

Subscribing needs the **Manage catalogs** permission (Administration tier).

> **Note:** this catalog is registered but holds no adapters yet, so a subscribe will be refused until its first node or library is published. The roadmap below is what is coming.

## Published adapters

_None yet._

## Published libraries

_None yet._

## Roadmap

| Adapter | Node type | Connects to | Status |
|---|---|---|---|
| Couchbase Query + Upsert | source, destination | Couchbase Query Service (SQL++/N1QL) | Next |
| PostgreSQL / SQL Server / MySQL / Oracle | source, destination | relational databases | Planned |
| MongoDB / Redis / Cassandra / DynamoDB / Neo4j | source, destination | NoSQL engines | Planned |
| Snowflake / BigQuery / Databricks / Redshift / Synapse / Fabric | destination | cloud warehouses | Planned |
| Elasticsearch / OpenSearch | source, destination | search | Planned |
| Power BI push / Tableau Hyper | destination | BI datasets | Planned |
| Epic Clarity / Caboodle | source | Epic reporting database | Planned |

Status meanings: **Next** is in active development, **Planned** is scoped but not started. See [the Integration Network](https://linkiir.com/network/) for the full adapter list and where each one stands.

## Configuration and credentials

Every adapter ships with its credential fields **empty**, and that is deliberate. Password fields are encrypted with each grid's own key, so a value shipped from here could not decrypt on your machine — it would fail with an error blaming your key. Fill them in on the node after you build it.

Two fields appear on most adapters and are worth knowing:

- **Live Mode** — when off, requests are prepared and logged but never sent. Use it to prove configuration before touching a real system.
- **Verify TLS** — leave on. Turn it off only against a local service with a self-signed certificate.

## Support and status

Adapters here are **Beta** unless the roadmap table says otherwise: they work and run somewhere, but the template is still being finished, so expect a Linkiir engineer alongside you on a first deployment. **GA** means the template is hardened and running across multiple customers.

Every adapter has a named owner at Linkiir who maintains it. For a problem with a specific adapter, quote its node type id.

## Versioning

- **Adapters** are versioned by the `version` field in `node_config.json`. A change that does not move the version forward is refused by the validator.
- **Library versions are immutable.** A published `libraries/<name>/<version>/` directory is never edited; a fix ships as a new version directory. Several versions sit side by side and each node pins the one it uses, so updating this catalog cannot disturb a node pinned to an older library.

Before applying an update, Grid shows you the incoming commit and diff. Read [CHANGELOG.md](CHANGELOG.md) for what changed and why.

## Repository layout

```
catalog.json                              the manifest Grid validates
nodes/<slug>/node_config.json             an adapter's definition
nodes/<slug>/*.lua                        its scripts
nodes/<slug>/samples/                     de-identified test messages
libraries/<name>/<version>/library.json   a published library version
libraries/<name>/<version>/<name>/*.lua   its modules
```

The layout is identical to Grid's own on-disk layout, so a pull needs no transform.

---

Published by Linkiir Inc. Part of the [Linkiir catalog set](https://github.com/Linkiir?q=adapters) — see [the Catalogs documentation](https://help.linkiir.com/docs/catalogs/) for how catalogs reach a grid.
