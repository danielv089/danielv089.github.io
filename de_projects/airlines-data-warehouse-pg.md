---
layout: default
title: Bookstore Python ETL 
nav_order: 4
---

# 2022 Airlines Departure Data Warehouse in PostgreSQL

[![Static Badge](https://img.shields.io/badge/Open%20GitHub%20Repository-blue?style=for-the-badge&logo=github)](https://github.com/danielv089/airlines-data-warehouse-pg)

## 📌 Overview

This project demonstrates the design of the 2022 Airlines Departure Data Warehouse using PostgreSQL. It is modeling historical U.S. domestic departure flight data into a query-optimized data warehouse following using dimensional modeling (star schema) approach. The goal of this project is to transform raw CSV files into a data warehouse that supports efficient querying, reporting, and analytics for airline departure operations and performance metrics. The project uses the Medallion Architecture which organizes data processing into layered zones — Bronze, Silver, and Gold.

Key Features:
- Dimensional database modelling (star schema).
- Applying Medallion Architecture.
- Demonstrating SQL usage and quaries for extracting meaningfull information.
- Provide insights into airline performance, delays, cancellations, and operational trends.

![schema_figure](/de_projects/assets/airlines-data-warehouse-pg/airlines_dw_schema.jpg)

## 🧱 Architecture Layers

### Bronze Layer
- Raw flight, cancellation, carrier, weather, and airport data stored in CSV files
- Data loaded into staging tables in the bronze schema without transformation.
- Data quality check performed (check row count, null values, duplicated rows and date range).
- Preserving raw data.

### Silver Layer
- Data validation, cleansing and transformation, when needed. 
- The raw data is already relatively clean, so minimal transformation was applied.
- Data separation in columns to apply consistent formatting and ensure atomicity and the 1NF.
- There is missing data in the weather reports due of cancelled flights mostly.

### Gold Layer
- Creating and loading data into dimension and fact tables.
- Follows a star schema structure for business intelligence, reporting, and analytics.
- Creating indexes to increase query performance.
- Date dimension table added to support time based aggregation.
- Generating flight_id as surrogate key by combining multiple columns uniquely identifying each flight.

## 🗃️ ERD Diagram

![dw_figure](/de_projects/assets/airlines-data-warehouse-pg/departure_dw_erd.jpg)

## Exploratory Data Analysis (EDA)
- Exploratory Data Analysis performed to gain more insight from the departure dataset.
- In this section I am leveraging SQL queries to extract summary statistics and trends.
- Demonstrates SQL concepts, including aggregation, window functions, ranking, subqueries and analytical computations.

  [![eda](https://img.shields.io/badge/EDA%3A%20Queries%20%26%20Results%20-%20blue?style=for-the-badge)](https://github.com/danielv089/airlines-data-warehouse-pg/blob/main/analytics_sql_scripts/eda.sql)
  

## 🧰 Tech Stack
- **PostgreSQL**
- **SQL**

## 📁 Repository Structure
``` 
├── analytics_sql_scripts
│   └── eda.sql
├── data
│   ├── ActiveWeather.csv
│   ├── Cancellation.csv
│   ├── Carriers.csv
│   ├── CompleteData.csv
│   └── Stations.csv
├── data_warehouse_sql_scripts
│   ├── 1_bronze_layer
│   │   ├── bronze_layer_quality_check.txt
│   │   ├── ddl_create_bronze_layer_tables.sql
│   │   └── dml_loading_bronze_layer_data.txt
│   ├── 2_silver_layer
│   │   ├── ddl_creating_silver_layer_tables.sql
│   │   └── dml_loading_silver_layer_data.sql
│   ├── 3_gold_layer
│   │   ├── add_surrogatekey_to_fact_table.sql
│   │   ├── create_indexes.sql
│   │   ├── ddl_creating_gold_layer_tables.sql
│   │   └── dml_loading_gold_layer_data.sql
│   ├── ddl_create_database.sql
│   └── ddl_create_schemas.sql
├── docs
│   ├── airlines_dw.png
│   └── departure_dw_erd.jpg
├── EDA.md
├── LICENSE
└── README.md
```

## 🔗 References

- Kaggle - 2022 US Airlines Domestic Departure Data
  https://www.kaggle.com/datasets/jl8771/2022-us-airlines-domestic-departure-data

- PostgreSQL Documentation
  https://www.postgresql.org/docs/

✅ This project uses only publicly available data for educational purposes.

