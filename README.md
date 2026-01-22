# 
<img width="942" height="576" alt="image" src="https://github.com/user-attachments/assets/ecbfb380-b184-4915-9f35-ddf03ea59c9e" />
 Bike Data Lakehouse: End-to-End Medallion Architecture

## 📌 Executive Summary
This project demonstrates the implementation of a modern **Data Lakehouse** using the **Medallion Architecture**. By leveraging **Databricks** and **Unity Catalog**, I transformed raw, siloed ERP and CRM data into a high-performance, business-ready Star Schema.

The goal was to solve typical data engineering challenges: data silos, poor data quality, and lack of historical traceability.

---

## 🏗️ System Architecture
The pipeline follows a multi-layered approach to ensure data integrity and scalability:

* **Bronze (Raw/Ingestion):** Direct ingestion of source CSVs into Delta tables (Schema-on-read, maintaining original state).
* **Silver (Curated/Cleaned):** Data deduplication, standardization of date formats, and business logic normalization (**PySpark/SQL**).
* **Gold (Analytical/Aggregated):** Dimensional modeling (**Star Schema**) optimized for BI tools (PowerBI/Tableau) and advanced analytics.

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
