# datamesh

A curated collection of **GitHub Copilot skills** for building and operating data engineering workloads on [Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/get-started/microsoft-fabric-overview). Each skill is a structured, agent-readable guide that teaches a Copilot coding agent (or any compatible AI assistant) how to interact with a specific Fabric service from the command line.

---

## Overview

The skills in this repository cover the full data engineering lifecycle on Microsoft Fabric:

| Skill | Category | What it does |
|---|---|---|
| [`check-updates`](.github/skills/check-updates) | Maintenance | Checks for marketplace updates to this skills collection once per week |
| [`e2e-medallion-architecture`](.github/skills/e2e-medallion-architecture) | Architecture | Implements a complete Bronze / Silver / Gold lakehouse using PySpark, Delta Lake, and Fabric Pipelines |
| [`spark-authoring-cli`](.github/skills/spark-authoring-cli) | Spark | Creates notebooks, lakehouses, Livy sessions, and Fabric pipelines via CLI |
| [`spark-consumption-cli`](.github/skills/spark-consumption-cli) | Spark | Runs interactive PySpark / Spark SQL analysis, Delta time-travel, and cross-lakehouse joins |
| [`sqldw-authoring-cli`](.github/skills/sqldw-authoring-cli) | SQL | Executes DDL/DML, `COPY INTO` ingestion, schema evolution, and stored procedures on Fabric Data Warehouse |
| [`sqldw-consumption-cli`](.github/skills/sqldw-consumption-cli) | SQL | Runs read-only T-SQL queries against Fabric Data Warehouse, Lakehouse SQL endpoints, and Mirrored Databases |
| [`eventhouse-authoring-cli`](.github/skills/eventhouse-authoring-cli) | KQL | Creates KQL tables, functions, ingestion mappings, materialized views, and retention/caching policies |
| [`eventhouse-consumption-cli`](.github/skills/eventhouse-consumption-cli) | KQL | Runs read-only KQL queries, schema discovery, time-series analytics, and ingestion monitoring |
| [`powerbi-authoring-cli`](.github/skills/powerbi-authoring-cli) | Power BI | Creates and deploys Power BI semantic models (TMDL), triggers refreshes, and manages data sources |
| [`powerbi-consumption-cli`](.github/skills/powerbi-consumption-cli) | Power BI | Executes read-only DAX queries and discovers semantic model metadata via the MCP server |

---

## Repository Structure

```
.github/
└── skills/
    ├── check-updates/
    │   └── SKILL.md
    ├── e2e-medallion-architecture/
    │   └── SKILL.md
    ├── eventhouse-authoring-cli/
    │   ├── SKILL.md
    │   └── references/
    ├── eventhouse-consumption-cli/
    │   ├── SKILL.md
    │   └── references/
    ├── powerbi-authoring-cli/
    │   ├── SKILL.md
    │   └── references/
    ├── powerbi-consumption-cli/
    │   ├── SKILL.md
    │   └── references/
    ├── spark-authoring-cli/
    │   ├── SKILL.md
    │   └── resources/
    ├── spark-consumption-cli/
    │   └── SKILL.md
    ├── sqldw-authoring-cli/
    │   ├── SKILL.md
    │   └── references/
    └── sqldw-consumption-cli/
        ├── SKILL.md
        └── references/
README.md
```

Each skill directory contains:
- **`SKILL.md`** — the main skill document read by the agent at invocation time.  It includes a YAML front-matter block with the skill `name` and `description`, followed by task tables, step-by-step instructions, code patterns, and must/prefer/avoid guidelines.
- **`references/`** or **`resources/`** *(where present)* — supplementary reference material linked from the main skill document (quick-reference cards, script templates, discovery queries, TMDL guides, etc.).

---

## Skill highlights

### Medallion Architecture (`e2e-medallion-architecture`)
Guides the agent through provisioning a complete three-layer data lakehouse:

| Layer | Purpose |
|---|---|
| **Bronze** | Raw data landed exactly as received; append-only, partitioned by ingestion date |
| **Silver** | Deduplicated, validated, conformed data; schema enforcement, business-date partitioning |
| **Gold** | Pre-calculated metrics optimised for Power BI; ZORDER, compaction, SQL endpoint exposure |

The skill creates separate Fabric workspaces and lakehouses per layer, deploys PySpark notebooks via the REST API, executes Bronze → Silver → Gold sequentially, and connects a Power BI semantic model to the Gold layer.

### Spark (`spark-authoring-cli` / `spark-consumption-cli`)
Covers the full Spark development workflow on Fabric:
- Lakehouse and notebook creation via `az rest`
- Livy session management for interactive PySpark
- Delta Lake patterns (upsert with `MERGE`, time-travel, `OPTIMIZE`/`VACUUM`)
- Pipeline orchestration and infrastructure-as-code patterns

### SQL Data Warehouse (`sqldw-authoring-cli` / `sqldw-consumption-cli`)
Covers T-SQL authoring and querying on Fabric Data Warehouse and Lakehouse SQL endpoints:
- DDL/DML, `COPY INTO` bulk ingestion, `OPENROWSET`
- Stored procedures, views, schema evolution
- Snapshot isolation and time-travel recovery
- Read-only queries, row counts, schema discovery, CSV/JSON export

### Eventhouse / KQL (`eventhouse-authoring-cli` / `eventhouse-consumption-cli`)
Covers real-time analytics with KQL on Fabric Eventhouse:
- Table/function/mapping creation and update policies
- Retention, caching, and partitioning policies
- Materialized views
- Time-series analysis with `bin()`, `summarize`, `join`, and `render`

### Power BI (`powerbi-authoring-cli` / `powerbi-consumption-cli`)
Covers Power BI semantic model lifecycle:
- Create and update models from TMDL definition files
- Dataset refresh, data-source configuration, permission management
- Deployment pipeline stages
- Read-only DAX queries and metadata discovery via MCP server

---

## Getting started

These skills are designed to be consumed by AI coding agents (GitHub Copilot, Claude Code, Cursor, Windsurf, Codex, etc.) that support the skills-for-fabric convention.  The agent reads the relevant `SKILL.md` at invocation time and follows the instructions to interact with Microsoft Fabric on your behalf.

### Prerequisites
- An active [Microsoft Fabric](https://app.fabric.microsoft.com) capacity and workspace
- [Azure CLI](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli) (`az`) installed and authenticated (`az login`)
- An AI coding assistant configured to load skills from `.github/skills/`

### Invoking a skill

Trigger phrases are listed in each skill's `description` field.  Examples:

```
"set up medallion architecture for my sales data"
"create a KQL table in my eventhouse"
"query the warehouse and show me row counts"
"refresh my Power BI dataset"
"analyze the orders table with PySpark"
```

---

## Contributing

Contributions are welcome.  When adding or modifying a skill:

1. Keep the YAML front-matter `name` consistent with the directory name.
2. Update the `description` field with clear trigger phrases.
3. Link supplementary material from the main `SKILL.md` rather than embedding it inline.
4. Follow the must/prefer/avoid pattern used in existing skills for actionable guidance.
