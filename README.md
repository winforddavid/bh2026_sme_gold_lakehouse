# SME Data Warehouse: Medallion Architecture & Star Schema on Databricks

This repository contains a complete, end-to-end Data Engineering portfolio project demonstrating a robust Small to Medium Enterprise (SME) data warehouse solution. Built on the Databricks Lakehouse Platform, the project implements the Medallion Architecture to transform raw data into a curated Gold Layer optimized for high-performance business intelligence.

## 🚀 Project Overview

The project addresses a realistic business scenario where an executive team requires deep insights into sales performance, including monthly revenue trends, top-selling products, regional performance, and customer loyalty (repeat customers).

**Key Features:**

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




## 🏗️ Architecture & Data Flow

The data follows a structured journey from source systems to the final consumption layer. This ensures data quality, governance, and reliability.

graph LR
    subgraph "Source Systems"
        S1[Sales DB]
        S2[Product Catalog]
        S3[CRM System]
        S4[Regional ERP]
    end

    subgraph "Bronze Layer (Raw)"
        B1[(bronze_sales_raw)]
        B2[(bronze_products_raw)]
        B3[(bronze_customers_raw)]
        B4[(bronze_regions_raw)]
    end

    subgraph "Silver Layer (Cleaned & Conformed)"
        SL1[(silver_sales)]
        SL2[(silver_products)]
        SL3[(silver_customers - SCD 2)]
        SL4[(silver_regions)]
    end

    subgraph "Gold Layer (Business Curated)"
        G1[(fact_sales)]
        G2[(dim_date)]
        G3[(dim_product)]
        G4[(dim_customer)]
        G5[(dim_region)]
    end

    subgraph "Consumption Layer"
        R1[PowerBI Dashboard]
        R2[Databricks SQL Analytics]
        R3[Executive Reports]
    end

    %% Flow connections
    S1 --> B1
    S2 --> B2
    S3 --> B3
    S4 --> B4

    B1 -- "Clean/Cast" --> SL1
    B2 -- "Standardize" --> SL2
    B3 -- "SCD Type 2 Logic" --> SL3
    B4 -- "Standardize" --> SL4

    SL1 -- "Join/Aggregate" --> G1
    SL2 --> G3
    SL3 --> G4
    SL4 --> G5
    
    %% Date dimension population
    D_GEN[Date Generator] --> G2

    G1 --> R1
    G1 --> R2
    G1 --> R3
    G2 & G3 & G4 & G5 --> R1
    G2 & G3 & G4 & G5 --> R2
    G2 & G3 & G4 & G5 --> R3







## 📊 Data Modeling: The Gold Layer

The Gold layer is designed as a Star Schema, the industry standard for analytical reporting. This structure simplifies complex queries and maximizes performance.

Star Schema Diagram

mermaid

Source



## Table Definitions

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







## 🛠️ Implementation Details

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




## 📈 PowerBI Integration

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




## 📂 Repository Structure

Plain Text


SQL
   bronze      # Raw table DDL and sample ingestion
   \
   silver      # Cleaning logic and SCD Type 2 implementation
   \
   gold        # Star Schema DDL, DML, and Reporting Queries
   \
   automation   # Production-ready Workflow scripts
   \
Diagrams        # Mermaid source and rendered images
\
Docs            # Detailed design and deployment guides
\
readme.md      # Project overview and documentation



## 📝 Conclusion

This project serves as a comprehensive template for building enterprise-grade data warehouses on Databricks. By following the Medallion Architecture and implementing robust data modeling practices, we provide a scalable foundation for actionable business intelligence.

