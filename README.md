# 📈 Real-Time Exchange Rate Pipeline | Databricks Medallion Architecture

[![Databricks](https://img.shields.io/badge/Databricks-PySpark-red?style=flat-square&logo=databricks)](https://databricks.com/)
[![Delta Lake](https://img.shields.io/badge/Storage-Delta%20Lake-blue?style=flat-square)](https://delta.io/)
[![Language](https://img.shields.io/badge/Language-Python%20%7C%20PySpark-yellow?style=flat-square&logo=python)](https://www.python.org/)

---

## Description

An end-to-end data engineering pipeline built on Databricks, implementing the **Medallion Architecture** (Bronze, Silver, Gold). The pipeline ingests multi-currency exchange rate JSON payloads, applies automated schemas and data quality validations, and calculates daily aggregated financial metrics ready for BI.

> **Note:** If the project is imported into Databricks in production, you can use the **Exchange Rates Data API** for data ingestion. The access key (API KEY) should be stored in a **Databricks Secret** to ensure security and proper operation.

---

## Architecture & Data Pipeline

mermaid
graph TD
    A[External API / JSON Source] --> B[BRONZE LAYER<br>(bronze_cotacoes_raw)<br>Ingestion with raw schema preservation<br>Audit timestamp columns]
    B --> C[SILVER LAYER<br>(silver_cotacoes_limpo)<br>Cleaning, strict typing (Double/Timestamp)<br>Deduplication and schema validation]
    C --> D[GOLD LAYER<br>(gold_cotacoes_diarias)<br>Business aggregations (Min/Max/Daily Average)<br>Delta tables optimized for Power BI/SQL]


---

### 💡 Key Features & Highlights

- **Medallion Lakehouse Pattern:** Complete separation between raw storage, clean transformations, and aggregation models.
- **ACID Transactions:** Based on Delta Lake, with schema enforcement, schema evolution, and time-travel.
- **Cleaning & Validation:** Strict typing for financial numbers, duplicate elimination, and removal of null values.
- **Governance:** Ready for Unity Catalog (catalog.schema.table).

---

## 📁 Repository Structure

plaintext
databricks-medallion-cotacoes/
├── README.md                       # Main technical documentation
├── notebooks/                      # Databricks Notebooks (pipeline)
│   ├── 01_bronze_ingestao.py       # Raw JSON ingestion & metadata tracking
│   ├── 02_silver_transformacao.py  # Cleaning, type casting & deduplication
│   └── 03_gold_agregacao.py        # Daily metric aggregation for analytics
└── docs/                          # Additional documentation


---

## 🚀 How to Run on Databricks

**Prerequisites:**
- Databricks Workspace (Community or Cloud)
- PySpark & Delta Lake environment
- JSON data source configured in Unity Catalog Volume/DBFS

**Steps:**
1. Clone the repository: Workspace → Repos → Add Repo (GitHub URL)
2. Run the notebooks sequentially:
   - `01_bronze_ingestao`: Populate Bronze layer
   - `02_silver_transformacao`: Clean data
   - `03_gold_agregacao`: Calculate analytical tables

---

## 📊 Analytical Output (Gold Layer)

 Column                | Type      | Description                                      |
-----------------------|-----------|--------------------------------------------------|
 data_referencia       | Date      | Reference date of the transaction                |
 moeda_origem          | String    | Base currency code (e.g., USD, EUR)              |
 nome_par              | String    | Full name of the currency pair                   |
 media_valor_compra    | Double    | Rounded daily average buy rate                   |
 media_valor_venda     | Double    | Rounded daily average sell rate                  |
 max_valor_venda       | Double    | Highest sell rate recorded in the interval       |
 min_valor_venda       | Double    | Lowest sell rate recorded in the interval        |

---

## 🛠️ Tech Stack & Tools

- **Compute & Processing:** Apache Spark (PySpark), Databricks Repos
- **Storage Layer:** Delta Lake
- **Governance & Metastore:** Unity Catalog
- **Language:** Python 3.x, SQL

---

## 👤 Author & Contact

- **Salvador Peres — Data Engineer**
- [LinkedIn](https://www.linkedin.com/in/salvador-inacio-peres/)
- GitHub: [https://github.com/save169](#)
- Email: [save_169@yahoo.com.br]