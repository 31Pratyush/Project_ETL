# PySpark ETL with Amazon EMR Studio | Star Schema on PostgreSQL (RDS)

This project demonstrates how to build a scalable and analytics-ready star schema data warehouse using PySpark on Amazon EMR

## Tech Stack

- **Amazon EMR Studio** – PySpark development and notebook-based orchestration  
- **Amazon EMR** – Distributed data processing with Apache Spark  
- **AWS RDS (PostgreSQL)** – Source and destination for both raw and transformed data  
- **JDBC Connector** – Spark ↔ PostgreSQL integration  



## Source Schema (ClassicModels)

The source schema is a normalized OLTP dataset (`classicmodels`) that includes:

- `customers`
- `orders`
- `orderdetails`
- `employees`
- `offices`
- `products`
- `payments`


## Project Objectives

- Extract OLTP data from AWS RDS PostgreSQL into Spark DataFrames (via JDBC)
- Clean, enrich, and transform data using PySpark on Amazon EMR
- Create a star schema optimized for analytical querying
- Load the final dimension and fact tables into a new schema `classicmodels_star_schema` in the same RDS instance

---

## Star Schema Design

### Dimension Tables:

| Table            | Description                                                  |
|------------------|--------------------------------------------------------------|
| `dim_customers`  | Extended customer info with rep and regional office          |
| `dim_products`   | Product details, category, and vendor info                   |
| `dim_employees`  | Employee hierarchy with manager and office mapping           |
| `dim_offices`    | Office location metadata (region, country, city)             |
| `dim_date`       | Time dimension generated from order dates                    |

### Fact Table:

| Table           | Description                                                   |
|-----------------|---------------------------------------------------------------|
| `fact_orders`   | Central sales fact table with metrics and surrogate key joins |


## Key Features

- Developed using EMR Studio notebooks
- Spark jobs executed on Amazon EMR(scalable compute)
- Surrogate keys for dimension tables
- Time dimension auto-generated for OLAP support
- Raw and transformed data managed in AWS RDS PostgreSQL

---

## Workflow

1. **Extract**: Load OLTP tables from RDS into Spark DataFrames via JDBC  
2. **Transform**: Apply joins, enrichments, business logic, and key generation  
3. **Model**: Design dimensions and fact table for a star schema  
4. **Load**: Write processed tables back to `classicmodels_star_schema` schema in PostgreSQL (RDS)

## Best Practices Used

- **Star Schema Design**: Optimized for analytical queries with clear separation of dimension and fact tables.
- **Surrogate Keys**: Used in dimension tables for better integrity and OLAP compatibility.
- **Distributed Processing**: PySpark on Amazon EMR enables scalable and efficient data transformations.
- **Notebook-Based Development**: EMR Studio notebooks allow modular, trackable development.
- **Clean ETL Workflow**: Distinct stages—Extract, Transform, Model, Load—make the pipeline maintainable and reusable.

## How to Run This Project

To run the project, ensure you have access to Amazon EMR, EMR Studio, and an RDS PostgreSQL instance with the `classicmodels` schema. 
Upload the notebooks to EMR Studio, configure JDBC access, and run the transformations. 
Final star schema tables will be written back to your RDS instance under the `classicmodels_star_schema` schema.

## Author

- Pratyush Sahay
- email: pratyush(dot)310899@gmail(dot)com 



