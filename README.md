# Uber Real-Time Data Engineering Project

**End-to-End Azure Data Pipeline for Ride Booking & Analytics**

---

## 📌 Project Overview

This project builds a **production-grade, near real-time data engineering pipeline** for Uber-like ride booking data on Microsoft Azure. It demonstrates streaming ingestion, incremental processing, and curated analytics layers using modern Azure services.

The pipeline ingests ride events, processes them through Bronze → Silver → Gold layers, and exposes business-ready datasets for analytics and reporting.

---

## 🏗️ Architecture

### High-Level Architecture

```
Ride Booking App / Simulator
          │
          ▼
┌──────────────────────┐
│  Azure Event Hubs    │   ← Real-time ride events
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│  Azure Data Factory  │   ← Orchestration & Ingestion
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│   Bronze Layer       │   ← Raw data (ADLS Gen2)
│   (Delta / Parquet)  │
└──────────┬───────────┘
           │ Databricks Autoloader / Streaming
           ▼
┌──────────────────────┐
│   Silver Layer       │   ← Cleaned, validated, enriched
└──────────┬───────────┘
           │
           ▼
┌──────────────────────┐
│   Gold / OBT Layer   │   ← Business-ready (Star Schema / OBT)
│   (Delta Lake)       │
└──────────────────────┘
           │
           ▼
     Analytics / BI Tools
```

**Key Design Patterns:**
- **Medallion Architecture** (Bronze → Silver → Gold)
- **Event-Driven Ingestion** via Azure Event Hubs
- **Incremental & Streaming Processing** with Databricks
- **One Big Table (OBT)** or Star Schema in Gold layer for analytics

---

## 🛠️ Technology Stack

| Layer                  | Technology                        | Purpose |
|------------------------|-----------------------------------|-------|
| **Streaming Source**   | Azure Event Hubs                  | Real-time ride event ingestion |
| **Orchestration**      | Azure Data Factory                | Pipeline orchestration & control flow |
| **Storage**            | Azure Data Lake Gen2              | Bronze, Silver, Gold layers |
| **Processing Engine**  | Azure Databricks (PySpark)        | Transformations, Autoloader, Delta Lake |
| **Code & Transformations** | Python + SQL (in Databricks) | `ingest.py`, `silver.py`, `model.py`, `silver_obt.sql` |
| **API / Web Layer**    | FastAPI + Uvicorn                 | Ride booking simulator / web app |
| **Project Management** | uv + pyproject.toml               | Modern Python dependency management |
| **CI/CD / Dev**        | Databricks Asset Bundles (inferred) | Version-controlled deployment |

---

## ✨ Key Features

- **Real-time / Near Real-time Ingestion** — Ride events streamed via Azure Event Hubs
- **Multi-Layer Data Processing** — Clean separation between raw (Bronze), cleaned (Silver), and business (Gold/OBT)
- **Modular Transformation Code** — Reusable Python modules (`ingest.py`, `silver.py`, `model.py`)
- **Business-Ready Output** — `silver_obt.sql` for creating analytics-friendly One Big Table
- **Web Application** — FastAPI-based ride booking simulator (`api.py`)
- **Production Snapshots** — Full evidence of pipeline execution, ADLS structure, and Databricks jobs
- **Modern Python Tooling** — Uses `uv` for fast dependency management

---

## 📁 Project Structure

```
Uber-Data-Engineer-Project/
├── Uber_Azure_DE_Project_details.pdf      # Detailed project documentation
├── architecture.png                       # Architecture diagram
│
├── api.py                                 # FastAPI ride booking simulator
├── connection.py                          # Database / service connections
├── data.py                                # Data generation / simulation logic
│
├── Code_Files/
│   └── Uber_Project/
│       └── uber_ride_ingest/
│           ├── transformations/
│           │   ├── ingest.py              # Bronze layer ingestion
│           │   ├── silver.py              # Silver layer transformations
│           │   ├── model.py               # Gold / modeling logic
│           │   └── silver_obt.sql         # One Big Table creation
│           └── explorations/
│               └── sample_notebook.ipynb
│
├── project_snapshots/                     # Execution evidence
│   ├── pipeline_graph.png
│   ├── adf_execution.png
│   ├── event_namespace&hub.png
│   ├── bronze_adls.png
│   ├── silver_obt_gold_layer_testing.png
│   └── ...
│
├── requirements.txt
├── pyproject.toml
├── uv.lock
└── files_array.json
```

---

## 🔄 How It Works (High-Level Flow)

1. **Data Generation / Simulation**
   - `api.py` + `data.py` simulate ride booking events
   - Events are pushed to **Azure Event Hubs**

2. **Ingestion Layer (Bronze)**
   - Azure Data Factory or Databricks streaming job ingests from Event Hubs
   - Raw events stored in **Bronze** ADLS Gen2 (Delta/Parquet format)

3. **Silver Layer Processing**
   - `silver.py` performs cleaning, validation, and enrichment
   - Data written to **Silver** Delta tables

4. **Gold / Analytics Layer**
   - `model.py` + `silver_obt.sql` create business-ready datasets
   - One Big Table (OBT) or dimensional model for analytics consumption

5. **Orchestration & Monitoring**
   - Azure Data Factory pipelines control the flow
   - Full visibility via Databricks jobs and ADF monitoring

---

## 🏆 Key Technical Achievements

- End-to-end pipeline from real-time event ingestion to analytics-ready data
- Clean modular code structure for maintainability
- Proper layering (Bronze → Silver → Gold/OBT)
- Use of modern Python tooling (`uv`, `pyproject.toml`)
- Comprehensive project documentation with execution snapshots
- Web application layer for realistic data simulation

---

## 🧠 Skills Demonstrated

- **Azure Data Engineering** — Event Hubs, Data Factory, Data Lake Gen2, Databricks
- **Streaming & Incremental Processing**
- **Data Lakehouse Architecture** (Medallion pattern)
- **PySpark Transformations** & Delta Lake
- **API Development** (FastAPI for data simulation)
- **Modular & Maintainable Code Design**
- **Project Documentation** & Evidence Collection

---

## 🚀 Getting Started

### 1. Python Environment

```bash
# Using uv (recommended)
uv sync

# Or using pip
pip install -r requirements.txt
```

### 2. Run the Web Application (Ride Simulator)

```bash
uvicorn api:app --reload
```

### 3. Databricks / Pipeline Execution

- Deploy the transformation notebooks (`ingest.py`, `silver.py`, `model.py`) to your Databricks workspace
- Use the provided `silver_obt.sql` for Gold layer creation
- Trigger pipelines via Azure Data Factory

---

## 📄 License

This project is created for **learning and portfolio demonstration** purposes.

---

**Author:** Himanshu  
**Domain:** Azure Data Engineering | Real-time Pipelines | Lakehouse Architecture

---

*Built with modern data engineering practices on Microsoft Azure*