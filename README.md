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

![Data Lakehouse Architecture](docs/data_Lakehouse.drawio%20(1).svg)

---

## 🛠️ Key Features
* **Data Governance:** Implemented **Unity Catalog** for fine-grained access control and metadata management.
* **Orchestration:** Automated end-to-end workflows using **Databricks Workflows (Jobs)** with modular task dependencies.
* **Data Quality:** Systematic cleaning including handling nulls, string normalization, and referential integrity checks.
* **Scalability:** Used a dictionary-driven ingestion pattern to reduce code redundancy (**DRY principle**).

---



## 🔍 Data Modeling & Intelligence (Gold Layer)
The final layer transitions from source-aligned data to a **Star Schema** (Dimensional Model). This design decouples the analytics layer from the source system logic, providing a high-performance environment for Business Intelligence and Data Science.

However, before building a new data model, we must first understand the original data model:
* What are the main business objects?
* How are these objects related to each other?
* 
By clearly analyzing the initial data model, we can identify three primary domains for the new dimensional model:
* Sales
* Product
* Customer

These domains will serve as the core labels (or subject areas) for designing the new star schema.
![Data Lakehouse Architecture](docs/integration_model.png)


Based on this understanding of the source model and business domains, we designed the Gold Layer using a dimensional modeling approach. The resulting model consists of:

* **Fact Tables:** `fact_sales` (Grain: Individual Transaction). Captures business events and quantitative metrics.
* **Dimension Tables:** `dim_customers`, `dim_products`. Provides descriptive context for slicing and dicing metrics.


![Data Lakehouse Architecture](docs/data_model.PNG)


---


## Data Flow / Lineage

The diagram below shows the data lineage for our data Lakehouse. It helps to understand where the data comes from and makes it easier to troubleshoot issues.

![Data Lakehouse Architecture](docs/data_flow.png)

--- 

## 📂 Project Structure
```bach
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
```

## 🚀 Deployment & Execution
The solution is fully automated via **Databricks Workflows**, ensuring a reliable end-to-end data lifecycle.

1.  **Environment Setup:** Configure **Unity Catalog** by creating the three-tier namespace: `bronze`, `silver`, and `gold`.
2.  **Data Ingestion:** Upload source CSV files into the `raw_sources` Volume within the Bronze schema.
3.  **Pipeline Orchestration:** * Deploy the `orchestration` notebooks to manage task dependencies.
    * Configure a **Databricks Job** (`loading_bike_data_lakehouse`) with task-level retries and cluster scaling.
4.  **Monitoring:** Execute the job and monitor the run via the Databricks Jobs UI to verify schema evolution and data integrity.

---
## 🛠️ Technologies & Tools

| Component | Technology |
|-----------|-----------|
| **Platform** | Databricks (AWS/Azure) |
| **Storage** | Delta Lake (ACID transactions) |
| **Processing** | Apache Spark (PySpark) |
| **Orchestration** | Databricks Jobs |
| **Catalog** | Unity Catalog |
| **Version Control** | Git (GitHub integration) |
| **Data Modeling** | Star Schema (Kimball) |



---


## 📈 Future Roadmap
- [ ] **Slowly Changing Dimensions (SCD Type 2):** Implement historical tracking for `dim_customers` to maintain point-in-time accuracy for reporting.
- [ ] **Automated Data Quality:** Integrate **Great Expectations** or Databricks **Delta Live Tables (DLT)** for circuit-breaker quality checks.
- [ ] **CI/CD Integration:** Automate deployment using **GitHub Actions** and **Databricks Asset Bundles (DABs)** for a true production-grade DevOps lifecycle.
- [ ] **New data sources** APIs, Kafka, streaming data, and operational databases


## 👨‍💻 Author
[Youssef Bouraha] Data Scientist | Data Engineer [LinkedIn Profile] | [Portfolio Website]
