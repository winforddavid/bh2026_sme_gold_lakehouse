# SME Data Warehouse: Medallion Architecture & Star Schema on Databricks

This repository contains a complete, end-to-end Data Engineering portfolio project demonstrating a robust Small to Medium Enterprise (SME) data warehouse solution. Built on the Databricks Lakehouse Platform, the project implements the Medallion Architecture to transform raw data into a curated Gold Layer optimized for high-performance business intelligence.

🚀 Project Overview

The project addresses a realistic business scenario where an executive team requires deep insights into sales performance, including monthly revenue trends, top-selling products, regional performance, and customer loyalty (repeat customers).

Key Features:

•
Medallion Architecture: Logical data separation into Bronze (Raw), Silver (Cleaned/Conformed), and Gold (Curated) layers.

•
Slowly Changing Dimensions (SCD Type 2): Historical tracking of customer data for accurate point-in-time reporting.

•
Star Schema Design: Optimized Gold layer for BI tools like PowerBI and Databricks SQL.

•
Automated Data Pipelines: Production-ready SQL scripts for Databricks Workflows.

•
DirectQuery Integration: Seamless connection to PowerBI for live reporting.




🏗️ Architecture & Data Flow

The data follows a structured journey from source systems to the final consumption layer. This ensures data quality, governance, and reliability.

mermaid

Source






📊 Data Modeling: The Gold Layer

The Gold layer is designed as a Star Schema, the industry standard for analytical reporting. This structure simplifies complex queries and maximizes performance.

Star Schema Diagram

mermaid

Source



Table Definitions

Table Type
Table Name
Description
Fact
fact_sales
Central table containing sales metrics and foreign keys to all dimensions.
Dimension
dim_date
Pre-populated calendar table for time-series analysis.
Dimension
dim_product
Descriptive product attributes (Category, Name, Price).
Dimension
dim_customer
Customer attributes with SCD Type 2 tracking for historical accuracy.
Dimension
dim_region
Geographical attributes for regional sales analysis.







🛠️ Implementation Details

1. Slowly Changing Dimensions (SCD Type 2)

We implement SCD Type 2 in the Silver layer to ensure that if a customer moves regions, their historical sales remain attributed to the correct location at the time of purchase.

2. Databricks Workflow Automation

The pipeline is automated using Databricks Workflows, with scripts designed for idempotency (using MERGE INTO) and performance (using OPTIMIZE and ZORDER).

3. Reporting Queries

The repository includes optimized SQL for answering critical business questions:

•
Monthly Revenue Trends

•
Top 10 Products by Revenue

•
Regional Revenue Distribution

•
Repeat Customer Identification




📈 PowerBI Integration

The Gold layer is served via a Databricks SQL Warehouse and connected to PowerBI using DirectQuery. This ensures that the dashboard always reflects the most current data without the need for manual refreshes.

Dashboard Components:

•
Executive KPIs: Total Revenue, Units Sold, and Repeat Customer Count.

•
Trend Analysis: Monthly Revenue area charts.

•
Categorical Insights: Product category performance.

•
Geographical Mapping: Interactive regional revenue maps.




📂 Repository Structure

Plain Text


├── sql/
│   ├── bronze/          # Raw table DDL and sample ingestion
│   ├── silver/          # Cleaning logic and SCD Type 2 implementation
│   ├── gold/            # Star Schema DDL, DML, and Reporting Queries
│   └── automation/      # Production-ready Workflow scripts
├── diagrams/            # Mermaid source and rendered images
├── docs/                # Detailed design and deployment guides
└── README.md            # Project overview and documentation






📝 Conclusion

This project serves as a comprehensive template for building enterprise-grade data warehouses on Databricks. By following the Medallion Architecture and implementing robust data modeling practices, we provide a scalable foundation for actionable business intelligence.

