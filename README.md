# Databricks Support Copilot Mini

A small Databricks learning project built to get hands-on with **Spark**, **Delta tables**, and **medallion architecture** through a simple support analytics use case.

The project simulates a lightweight support intelligence workflow:
- raw support tickets and FAQ data are ingested into **Bronze** tables
- cleaned and standardized into **Silver**
- aggregated into a **Gold** analytics table for business-facing insights

The goal was not to build a large production platform, but to understand how a Databricks-style workflow is structured end to end.

---

## Project Overview

This project uses a small synthetic support dataset containing:
- support tickets
- FAQ / knowledge base entries

Using Databricks notebooks and Spark, the data is transformed across three layers:

### Bronze
Raw ingested data stored as Delta tables:
- `bronze_tickets`
- `bronze_faq`

### Silver
Cleaned and standardized data:
- `silver_tickets`
- `silver_faq`

Transformations included:
- converting `created_at` into a proper date
- standardizing `priority` and `status`
- trimming and cleaning text fields

### Gold
Business-ready aggregated table:
- `gold_issue_summary`

This Gold table groups support tickets by:
- product
- issue type
- status

and calculates ticket counts to surface recurring support patterns.

---

## Final Insight

The final Gold table showed that:

- **Sensor A / Connectivity / OPEN** was the top recurring issue cluster
- the remaining issue categories were mostly one-off cases

This demonstrates how even a small Databricks pipeline can turn raw operational data into something more actionable for business or product teams.

---

## Tech Used

- **Databricks Free Edition**
- **PySpark**
- **Delta Lake**
- **Databricks notebooks**
- **Medallion architecture (Bronze / Silver / Gold)**

---

## Table Structure

### Bronze Tables
- `workspace.support_demo.bronze_tickets`
- `workspace.support_demo.bronze_faq`

### Silver Tables
- `workspace.support_demo.silver_tickets`
- `workspace.support_demo.silver_faq`

### Gold Table
- `workspace.support_demo.gold_issue_summary`

---

## Example Gold Output

```sql
+---------+------------+------+------------+
|  product|  issue_type|status|ticket_count|
+---------+------------+------+------------+
| Sensor A|Connectivity|  OPEN|           3|
|Gateway X|       Setup|  OPEN|           1|
|Gateway X|Connectivity|  OPEN|           1|
|Gateway X|       Setup|CLOSED|           1|
| Sensor A|       Usage|CLOSED|           1|
| Sensor B|    Firmware|CLOSED|           1|
| Sensor B|     Battery|CLOSED|           1|
| Sensor B|     Billing|CLOSED|           1|
| Sensor C|       Usage|  OPEN|           1|
| Sensor C|    Firmware|  OPEN|           1|
+---------+------------+------+------------+
```

---

## Why I Built This

I wanted to get practical exposure to Databricks in a way that was small, structured, and relevant to real-world data work.

Rather than treating Databricks as just a notebook environment, I used this project to understand:
- how raw data is ingested and persisted as Delta tables
- how Spark transformations fit into a medallion workflow
- how Databricks can support business-facing analytics from a lakehouse-style pipeline

This was intentionally a compact learning project, but it helped me understand the workflow logic behind scalable Databricks solutions.

---

## What I Learned

Through this project, I got hands-on experience with:
- creating and working in Databricks notebooks
- reading local CSV data into Databricks
- converting pandas data into Spark DataFrames
- writing managed Delta tables
- structuring a Bronze / Silver / Gold pipeline
- using Spark to clean, standardize, and aggregate data

---

## What I Would Add Next

Given more time, I would extend this with:
- scheduled pipeline execution
- dashboards or visual reporting
- MLflow experiment tracking
- a retrieval layer on top of the FAQ data for a small GenAI / RAG extension
- governance and lineage exploration through Unity Catalog concepts

---

## Repository Structure

```text
databricks-support-copilot-mini/
├─ data/
│  ├─ tickets.csv
│  └─ faq.csv
├─ notebooks/
│  └─ 01_bronze_ingest_and_transform.py
└─ README.md
```

---

## Short Summary

A compact Databricks support analytics demo using **Spark** and **Delta Lake** to implement a **Bronze / Silver / Gold** medallion pipeline over support tickets and FAQ data, producing business-ready issue summaries from raw operational data.
