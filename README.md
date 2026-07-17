# Azure ELT Sales Pipeline

An end-to-end data engineering pipeline built on Microsoft Azure that ingests, cleans, and aggregates sales data using the medallion architecture (Bronze / Silver / Gold).

## Overview

This project demonstrates a real-world ELT (Extract, Load, Transform) workflow commonly used in production data platforms. Raw data is ingested from a public HTTP source, loaded into a data lake, and progressively refined through three layers using Azure Databricks and Delta Lake.

## Architecture
HTTP Source (CSV)
↓
Azure Data Factory (Ingest)
↓
Azure Data Lake Storage Gen2 — Bronze (raw data)
↓
Azure Databricks — PySpark transformation
↓
Silver Layer (cleaned, deduplicated, Delta format)
↓
Gold Layer (business-level aggregation, Delta format)
↓
Power BI (visualization)

## Technologies used

- **Azure Data Factory** — data ingestion pipeline (Copy Data tool)
- **Azure Data Lake Storage Gen2** — hierarchical data lake storage
- **Azure Databricks** — Spark-based compute for transformations
- **PySpark** — data cleaning and aggregation logic
- **Delta Lake** — ACID-compliant storage format for Silver and Gold layers
- **Power BI** — dashboard visualization

## Pipeline steps

1. **Ingestion (Bronze):** Azure Data Factory pulls a CSV file from a public HTTP endpoint and lands it in the Bronze container of ADLS Gen2, preserving raw data in its original form.

2. **Transformation (Silver):** A Databricks notebook reads the Bronze CSV, removes duplicate records and null values, and writes the cleaned dataset to the Silver container in Delta format.

3. **Aggregation (Gold):** The Silver dataset is grouped by day to calculate total sales and total tips, producing a business-ready summary table saved to the Gold container in Delta format.

4. **Visualization:** The Gold layer is connected to Power BI / Databricks visualizations to present day-wise sales trends.

## Key concepts demonstrated

- Medallion architecture (Bronze/Silver/Gold)
- ELT pipeline design on cloud infrastructure
- Delta Lake for reliable, versioned data storage
- PySpark DataFrame transformations
- Azure resource provisioning (Storage, Data Factory, Databricks)

## Notebook

See [`bronze_to_silver_gold.ipynb`](./bronze_to_silver_gold.ipynb) for the full transformation code.

## Author

Sonu Kushwah  
[LinkedIn](https://linkedin.com/in/sonu7804) | [GitHub](https://github.com/sonu7804)
