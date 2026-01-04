# 🛒 Ecommerce Product Funnel Analytics (Databricks)

An end-to-end **batch analytics pipeline** for ecommerce product funnel analysis built using **Databricks, Apache Spark, Delta Lake, SQL, and Tableau**.  
This project demonstrates **incremental data processing, Lakehouse architecture (Bronze–Silver–Gold), job orchestration, monitoring, and dashboard-ready analytics**.

---

## 📌 Project Overview

This project simulates a **production-style ecommerce analytics pipeline** where raw user event data is processed **incrementally by date** and transformed into **business-ready metrics**.

The pipeline:
- Ingests raw event data incrementally
- Cleans and deduplicates events
- Produces daily funnel and product-level KPIs
- Is fully automated using **Databricks Jobs** with parameterized runs (`RUN_DATE`)
- Exposes **Gold-layer tables** for BI dashboards (Tableau / Databricks SQL)

---


## 🏗 Architecture (Lakehouse Design)

```text
Landing (simulated daily data arrival)
        ↓
Bronze Layer (raw incremental ingestion - Delta Lake)
        ↓
Silver Layer (cleaned, typed, deduplicated events)
        ↓
Gold Layer (business-ready aggregated metrics)
        ↓
BI Layer (Tableau / Databricks SQL dashboards)
```


## 🧰 Technology Stack

- Databricks (Serverless Compute)
- Apache Spark (PySpark)
- Delta Lake
- Databricks Jobs & Scheduling
- SQL
- Tableau

---

## 📁 Repository Structure

```text
ecommerce-product-funnel-analytics-databricks/
├── notebooks/
│   ├── 00_replay_to_landing.ipynb
│   ├── 00_setup_and_load.ipynb
│   ├── 01_bronze_ingestion.ipynb
│   ├── 02_dataset_profiling.ipynb
│   ├── 03_silver_events_cleaning.ipynb
│   ├── 04_gold_funnel_metrics.ipynb
│   ├── 05_gold_product_daily_metrics.ipynb
│   └── 06_pipeline_monitoring.ipynb
│
├── sql/
│   └── analytical_queries.sql        # Validation & KPI checks
│
├── tableau/
│   └── dashboard_screenshots/         # Tableau Public dashboard images
│
├── docs/
│   └── architecture_diagrams/         # Pipeline & Lakehouse diagrams
│
└── README.md
```

---

## 🔄 Pipeline Workflow

### 0️⃣ Replay to Landing
**Notebook:** `00_replay_to_landing`

- Simulates daily data arrival
- Replays event data into a landing directory
- Controlled using the `RUN_DATE` parameter

---

### 1️⃣ Bronze Layer — Incremental Ingestion
**Notebook:** `01_bronze_ingestion`

- Reads only data for the given `RUN_DATE`
- Appends raw events into a Bronze Delta table
- Adds ingestion metadata:
  - `run_date`
  - `ingestion_ts`
  - `batch_id`

✔ Append-only, incremental ingestion design

---

### 2️⃣ Dataset Profiling
**Notebook:** `02_dataset_profiling`

- Schema inspection
- Null value checks
- Duplicate analysis
- Basic data quality validation

ℹ️ One-time exploratory step (not scheduled)

---

### 3️⃣ Silver Layer — Event Cleaning
**Notebook:** `03_silver_events_cleaning`

- Reads data from Bronze
- Normalizes categorical fields
- Removes duplicates
- Filters invalid records
- Uses Delta MERGE logic

✔ Produces clean, analytics-ready event data

---

### 4️⃣ Gold Layer — Funnel Metrics
**Notebook:** `04_gold_funnel_metrics`

Creates **daily funnel-level KPIs**, including:
- Total events
- Unique users
- Sessions
- Views, carts, purchases
- Revenue
- Conversion rates

**Output Table:** `gold_funnel_metrics`

---

### 5️⃣ Gold Layer — Product Daily Metrics
**Notebook:** `05_gold_product_daily_metrics`

- Product-level daily performance metrics
- Purchase counts
- Revenue contribution by product

**Output Table:** `gold_product_daily_metrics`

---

### 6️⃣ Pipeline Monitoring
**Notebook:** `06_pipeline_monitoring`

- Centralized run logging
- Tracks:
  - Run date
  - Rows processed per layer
  - Execution status
- Enables observability, debugging, and auditing

---

## ⏱️ Job Orchestration & Scheduling

The entire pipeline is orchestrated using **a single Databricks Job** with task dependencies:

Replay → Bronze → Silver → Gold Funnel → Gold Product → Monitoring



- Parameterized using `RUN_DATE`
- Supports manual backfills and scheduled runs
- Runs on Databricks **Serverless Compute**

✔ Demonstrates production-grade batch orchestration

---

## 📊 Analytics & Dashboarding

- Gold tables are **dashboard-ready**
- Designed for:
  - Tableau
  - Databricks SQL Dashboards
- Metrics update automatically as new daily runs complete

---

## ✅ Key Concepts Demonstrated

- Incremental batch processing
- Medallion (Bronze–Silver–Gold) architecture
- Delta Lake MERGE patterns
- Idempotent pipeline design
- Databricks Jobs & scheduling
- Centralized pipeline monitoring
- Business-ready data modeling

---

## 🚀 Use Cases

- Product funnel analysis
- Conversion tracking
- Daily revenue monitoring
- Portfolio project for:
  - Data Engineer
  - Analytics Engineer
  - BI Engineer roles

---

## 👤 Author

**Sajith Pemarathna**  
Berlin, Germany
