# azure-databricks-f1-lakehouse
Building pipelines to learn Azure Databricks through Formula1 datasets


# Data Ingestion Framework Overview

This project implements a modular and parameter-driven data ingestion framework using Azure Databricks and PySpark.

The current version focuses on dynamically ingesting CSV and JSON files from
Azure Data Lake Storage (ADLS), applying optional dataset-specific transformations,
and loading the processed data into a curated storage layer.

The framework is designed to be extensible and will be enhanced with additional
features as learning progresses.

---

## Architecture

The project follows a simplified lakehouse-style architecture:

Raw Layer (ADLS)  →  Ingestion Engine  →  Processed Layer (ADLS)

Key components:

- Dynamic ingestion notebooks for CSV and JSON files
- Optional transformation notebooks for dataset-specific logic
- Parameter-driven execution using Databricks widgets
- Centralized configuration and utility modules

---

## Tech Stack

- Azure Databricks
- PySpark
- Spark SQL
- Azure Data Lake Storage Gen2
- Delta Lake (planned)
- GitHub
- Azure Data Factory (planned)

---

## Project Structure

F1_project/

- ├── app_lib/ # Common utilities and ingestion logic

- ├── custom_transformation/ # Dataset-specific transformation notebooks

- ├── ingestion/ # Main orchestration notebooks

- └── schemas/ # DDL-based schema definitions


---

## Current Features

- Parameter-driven ingestion of CSV and JSON files
- Support for custom schemas (DDL format)
- Optional transformation execution
- Modular transformation design
- Audit column population (ingestion timestamp)
- Partitioned writes (optional)

---

## Ingestion Workflow

1. Source file path, schema, and other parameters are passed via widgets
2. The common ingestion notebook loads the data into a Spark DataFrame
3. If a transformation notebook is specified, it is executed dynamically
4. Dataset-specific transformations are applied
5. Processed data is written to the curated container

---

## How to Run

1. Configure ADLS access and secret scopes
2. Update the 2 configuration files in `app_lib`
3. Upload raw CSV/JSON files to ADLS
4. Execute ingestion notebooks with required parameters or refer notebooks in ingestion folder
5. Validate output in the processed container

---

## Example Parameters

Example widget parameters for CSV ingestion:
    "p_csv_filepath" : "abfss://<container>@storage_account.dfs.core.windows.net/races.csv",
    "p_csv_filename" : "races",
    "p_csv_schema" : "raceId INT, year INT, round INT, circuitId INT, name STRING, date DATE, time STRING, url STRING",
    "p_csv_header" : "False",
    "p_transformations_file" : "races_csv_transformation",
    "p_partitions" : "year"
