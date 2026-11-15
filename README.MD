# PySpark Retail Data Warehouse Revision

## Files and flow

```text
retail_orders.csv
      │ read with explicit schema
      ▼
Notebook: Bronze (raw + ingestion timestamp)
      │ type conversion, derived amounts, validation, deduplication
      ▼
Silver (clean order lines)
      │ build dimensions and fact at one-row-per-order-line grain
      ▼
Gold star schema
  ├── dim_customer
  ├── dim_product
  ├── dim_date
  └── fact_sales (partitioned by year)
      │
      ▼
data_lake/gold/*.parquet
```

1. Open `pyspark_retail_warehouse.ipynb` in VS Code.
2. Ensure Java 17+ is installed and available on PATH.
3. In the notebook environment run `pip install -r requirements.txt`.
4. Run cells from top to bottom. The CSV is deliberately local to the notebook.
5. The notebook writes Parquet into `data_lake/gold/`.

Each section includes questions, worked answers, and explanations. The dataset has 300 synthetic order-line records with a full year of 2025 dates. The SCD Type 2 section is conceptual because this single snapshot has no customer history.
