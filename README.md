# Modern_Data_Lakehouse_Project



## Repository Structure

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
