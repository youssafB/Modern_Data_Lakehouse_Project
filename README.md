# Modern_Data_Lakehouse_Project

# 🚀 Bike Data Lakehouse: End-to-End Medallion Architecture

[![Databricks](https://img.shields.io/badge/Platform-Databricks-orange?style=flat-square&logo=databricks)](https://www.databricks.com/) 
[![Spark](https://img.shields.io/badge/Engine-PySpark-blue?style=flat-square&logo=apachespark)](https://spark.apache.org/) 
[![Delta Lake](https://img.shields.io/badge/Storage-Delta_Lake-cyan?style=flat-square)](https://delta.io/)

## 📌 Executive Summary
This project demonstrates the implementation of a modern **Data Lakehouse** using the **Medallion Architecture**. By leveraging **Databricks** and **Unity Catalog**, I transformed raw, siloed ERP and CRM data into a high-performance, business-ready Star Schema. 

The goal was to solve typical data engineering challenges: data silos, poor data quality, and lack of historical traceability.

---

## 🏗️ System Architecture
The pipeline follows a multi-layered approach to ensure data integrity and scalability:

1.  **Bronze (Raw/Ingestion):** Direct ingestion of source CSVs into Delta tables (Schema-on-read, maintaining original state).
2.  **Silver (Curated/Cleaned):** Data deduplication, standardization of date formats, and business logic normalization using PySpark and Spark SQL.
3.  **Gold (Analytical/Aggregated):** Dimensional modeling (Star Schema) optimized for BI tools (PowerBI/Tableau) and advanced analytics.

> **Note:** I utilized **Unity Catalog** to manage data governance, ensuring a clear separation between raw, cleaned, and production-ready data layers.

---

## 🛠️ Key Features & Engineering Strategy
* **Modular Pipeline Design:** Built using an orchestration pattern where a master job triggers individual layer notebooks, allowing for easy debugging and maintenance.
* **Data Governance:** Implemented fine-grained access control and metadata descriptions via Unity Catalog.
* **Performance Optimization:** Leveraged the **Delta Lake** format for ACID transactions, time travel, and efficient file management (Compaction/Z-Order).
* **Clean Code (DRY):** Optimized repetitive ingestion tasks using Python dictionaries and loops to handle multiple source files dynamically.

---

## 📂 Project Structure
```bash
├── bronze/                # Raw ingestion notebooks (Manual & Automated)
├── silver/                # Data cleaning & Quality validation
│   ├── crm/               # CRM source transformations
│   └── erp/               # ERP source transformations
├── gold/                  # Dimensional modeling (Star Schema)
├── orchestration/         # Notebooks to trigger end-to-end runs
└── assets/                # Architecture diagrams and SQL DDLs




## Repository Structure

```text
.
├── datasets/
├── code/
│   ├── init_lakehouse.ipynb
│   ├── bronze/
│   │   ├── bronze.ipynb
│   │   └── bronze_config.py
│   ├── silver/
│   │   ├── crm/
│   │   │   ├── silver_crm_cust_info.ipynb
│   │   │   ├── silver_crm_prd_info.ipynb
│   │   │   └── silver_crm_sales_details.ipynb
│   │   ├── erp/
│   │   │   ├── silver_erp_cust_az12.ipynb
│   │   │   ├── silver_erp_loc_a101.ipynb
│   │   │   └── silver_erp_px_cat_g1v2.ipynb
│   │   └── silver_orchestration.ipynb
│   └── gold/
│       ├── gold_dim_customers.ipynb
│       ├── gold_dim_products.ipynb
│       ├── gold_fact_sales.ipynb
│       └── gold_orchestration.ipynb
├── doc/
├── .gitignore
└── README.md
