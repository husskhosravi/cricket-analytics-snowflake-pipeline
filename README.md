### 📌 Cricket Analytics Project Summary (Scalable Data Warehouse on Snowflake)

This project showcases a fully automated, production-grade data pipeline built on Snowflake for cricket analytics. It ingests semi-structured match data in JSON format from AWS S3 using Snowpipe, processes it through Streams and Tasks, and transforms it into a clean, analytical star schema. The model includes fact and dimension tables capturing players, teams, matches, and ball-by-ball events. Key features include incremental loading, dynamic JSON flattening, surrogate key generation, SCD handling, and dependency-managed task orchestration, making it a scalable solution for real-time sports data warehousing and analysis.

---

### 📦 Project Overview

* End-to-end pipeline using Snowflake & AWS S3
* Handles nested JSON for cricket match data
* Fully automated with Snowpipe, Streams, and Tasks
* Final model supports analytical queries and reporting

---

### 🧱 Architecture

| Component      | Technology                 |
| -------------- | -------------------------- |
| Cloud Storage  | AWS S3                     |
| Data Warehouse | Snowflake                  |
| File Format    | JSON                       |
| Ingestion      | Snowpipe (auto-ingest)     |
| Processing     | Snowflake Tasks + Streams  |
| Scheduling     | 1-minute DAG orchestration |

📌 **Visual pipeline:**


---

### 🧠 Core Concepts Demonstrated

* Semi-structured data handling (JSON)
* Auto-ingestion from S3 using Snowpipe
* Incremental loads with Streams
* Orchestration with dependency-based Tasks
* SCD Type-0 and Type-1 modelling
* Complex SQL with arrays, object parsing, and flattening

---

### 🧩 Data Model Design

**Tables:**

* `DW.MATCH_INFO` – Match-level metadata
* `DW.MATCH_INNINGS` – Ball-by-ball fact table
* `DW.PLAYERS` – Players with multi-team support (array)
* `DW.TEAMS` – Teams with type (club/national)

**Highlights:**

* Surrogate keys via Snowflake sequences
* `FILENAME` as deduplication + join key
* `IS_POWERPLAY` derived using `CASE`, fallback defaults

---

### 🔄 Pipeline Flow

```
1. Upload JSON to S3
2. Snowpipe loads to RAW.RAW_DATA
3. Stream detects new rows
4. Tasks process and flatten JSON:
    - Teams
    - Players
    - Match Info
    - Innings
5. DW Layer loads using sequenced keys
```

---

### 📁 Repo File Layout

```
📂 cricket-snowflake-dw
│
├── README.md
├── task_flow.png
├── sql/
│   ├── raw_layer.sql
│   ├── staging_layer.sql
│   ├── dw_layer.sql
│   └── ddl_all_tables.sql
└── queries/
    └── match_analysis_queries.sql
```

---

### 🧠 What I Learned

* Handling nested JSON at scale
* Automating full ingestion + transformation pipeline
* Writing maintainable SQL with complex logic
* Managing SCD logic using `MERGE`, `ARRAY_CAT`, `ARRAY_DISTINCT`
* Scheduling DAGs using Snowflake native features (no Airflow needed)

---

### 🏁 Final Notes

✅ Supports ODI, T20, Test, and Women’s leagues
✅ Easily extendable with dashboards or materialised views
✅ Plug-and-play with public cricket data from Cricsheet
