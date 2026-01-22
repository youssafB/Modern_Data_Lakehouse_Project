# 🚲 Bike Data Lakehouse: End-to-End Medallion Architecture

## 📌 Executive Summary
This project demonstrates the implementation of a modern **Data Lakehouse** using the **Medallion Architecture**. By leveraging **Databricks** and **Unity Catalog**, I transformed raw, siloed ERP and CRM data into a high-performance, business-ready Star Schema.

The goal was to solve typical data engineering challenges: data silos, poor data quality, and lack of historical traceability.

---

## 🏗️ System Architecture
The pipeline follows a multi-layered approach to ensure data integrity and scalability:

* **🥉Bronze (Raw/Ingestion):** Direct ingestion of source CSVs into Delta tables (Schema-on-read, maintaining original state).
* **🥈 Silver (Curated/Cleaned):** Data deduplication, standardization of date formats, and business logic normalization (**PySpark/SQL**).
* **🥇Gold (Analytical/Aggregated):** Dimensional modeling (**Star Schema**) optimized for BI tools (PowerBI/Tableau) and advanced analytics.

> **📸 Visual Suggestion:** Insert a Draw.io diagram here showing: `[CSV Sources] -> [Bronze Volume] -> [Silver Tables] -> [Gold Fact/Dim]`. Use icons for Databricks and Unity Catalog.

---

## 🛠️ Key Features
* **Data Governance:** Implemented **Unity Catalog** for fine-grained access control and metadata management.
* **Orchestration:** Automated end-to-end workflows using **Databricks Workflows (Jobs)** with modular task dependencies.
* **Data Quality:** Systematic cleaning including handling nulls, string normalization, and referential integrity checks.
* **Scalability:** Used a dictionary-driven ingestion pattern to reduce code redundancy (**DRY principle**).

---

## 📂 Project Structure
```bash
├── bronze/                # Raw ingestion notebooks
├── silver/                # Cleaning & Transformation scripts
│   ├── crm/               # CRM-specific logic
│   └── erp/               # ERP-specific logic
├── gold/                  # Dimensional modeling (Star Schema)
├── orchestration/         # Notebooks to trigger layers
└── docs/                  # Architecture diagrams & Data Dictionary

---



## 🔍 Data Modeling & Intelligence (Gold Layer)
The final layer transitions from source-aligned data to a **Star Schema** (Dimensional Model). This design decouples the analytics layer from the source system logic, providing a high-performance environment for Business Intelligence and Data Science.

* **Fact Tables:** `fact_sales` (Grain: Individual Transaction). Captures business events and quantitative metrics.
* **Dimension Tables:** `dim_customers`, `dim_products`, `dim_stores`. Provides descriptive context for slicing and dicing metrics.
* **Data Products:** Implemented table and column-level documentation in **Unity Catalog** to ensure the data is "discoverable" and "self-service" ready for analysts.

> **📸 Visual Suggestion:** 
*Insert a screenshot of your Gold Layer ER Diagram showing the Fact table at the center connected to your Dimension tables.*

---

## 🚀 Deployment & Execution
The solution is fully automated via **Databricks Workflows**, ensuring a reliable end-to-end data lifecycle.

1.  **Environment Setup:** Configure **Unity Catalog** by creating the three-tier namespace: `bronze`, `silver`, and `gold`.
2.  **Data Ingestion:** Upload source CSV files into the `raw_sources` Volume within the Bronze schema.
3.  **Pipeline Orchestration:** * Deploy the `orchestration` notebooks to manage task dependencies.
    * Configure a **Databricks Job** (`loading_bike_data_lakehouse`) with task-level retries and cluster scaling.
4.  **Monitoring:** Execute the job and monitor the run via the Databricks Jobs UI to verify schema evolution and data integrity.

---

## 📈 Future Roadmap
- [ ] **Slowly Changing Dimensions (SCD Type 2):** Implement historical tracking for `dim_customers` to maintain point-in-time accuracy for reporting.
- [ ] **Automated Data Quality:** Integrate **Great Expectations** or Databricks **Delta Live Tables (DLT)** for circuit-breaker quality checks.
- [ ] **CI/CD Integration:** Automate deployment using **GitHub Actions** and **Databricks Asset Bundles (DABs)** for a true production-grade DevOps lifecycle.



## 👨‍💻 Author
[Youssef Bouraha] Data Scientist | Data Engineer [LinkedIn Profile] | [Portfolio Website]
