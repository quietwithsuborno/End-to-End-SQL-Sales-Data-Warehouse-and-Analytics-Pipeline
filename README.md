# End-to-End Sales Data Warehouse and Analytics Pipeline

In this project, I transformed messy raw data from CRM and ERP sources into analytics-ready datasets using SQL and the Medallion Architecture. By building this end-to-end pipeline, I extracted meaningful business insights to support strategic decision-making, demonstrating a step-by-step methodology for converting raw, fragmented data into actionable business intelligence.

---

## 🎯 Objectives

### ⚙️ Data Engineering Goals
- Build a modern data warehouse using SQL Server
- Ingest and consolidate data from CRM and ERP source systems
- Implement Medallion Architecture (Bronze → Silver → Gold)
- Develop robust ETL pipelines for data cleansing and transformation
- Ensure high data quality, consistency, and integrity

### 📊 Data Analytics Goals

* **Sales Performance Analysis:** Evaluate historical sales data to identify growth patterns and seasonal trends.
* **Customer Behavior & Segmentation:** Analyze purchasing habits to categorize customer groups and understand behavioral drivers.
* **Product Trend Evaluation:** Assess product performance and contribution analysis to identify high-impact items and market trends.
* **Technical Insight Extraction:** Utilize advanced SQL techniques including ranking, performance evaluation, and contribution analysis to derive actionable intelligence.
* **Data-Driven Decision Support:** Uncover visual patterns through Excel to translate complex data into strategic business recommendations.

---

## 📂 Data Source

The dataset for this project consists of six source files provided by my **Mentor**, representing real-world data extracted from **CRM** and **ERP** systems. These files serve as the starting point for the data pipeline:

### 📱 CRM System Files:
* `cust_info.csv`: Contains customer-related information.
* `prd_info.csv`: Contains product details and specifications.
* `sales_details.csv`: Records of historical sales transactions.

### 🏢 ERP System Files:
* `CUST_AZ12.csv`: Internal customer tracking data.
* `LOC_A101.csv`: Location and branch-specific data.
* `PX_CAT_G1V2.csv`: Product categorization and inventory data.

---

## ⚙️ Data Engineering

### 🗺️ Data Flow Architecture
Below is the architectural representation of the data pipeline, following the Medallion Architecture (Bronze, Silver, and Gold layers).

<p align="center">
  <img src="docs/data_flow.png" alt="Data Flow Diagram" width="800">
</p>

To ensure data reliability and quality, I implemented a **Medallion Architecture**, organizing data into three distinct layers:

* **🥉 Bronze (Raw Layer):** Acts as the landing zone for raw source files. The data is kept in its original format to maintain a complete history (data lineage) and allow for reprocessing if needed.
* **🥈 Silver (Curated Layer):** The "Cleaning" zone. In this layer, data from CRM and ERP is merged, cleaned, and standardized. Duplicates are removed, and inconsistent formats are resolved to create a single version of truth.
* **🥇 Gold (Analytical Layer):** The "Business-Ready" zone. Data is modeled into **Fact** and **Dimension** tables (Star Schema), optimized for high-speed analytical queries and dashboarding.

### 🚀 ETL Process Details

I developed a comprehensive ETL pipeline to ensure the raw data is transformed into a high-quality analytical asset.

### 1. Extraction (Source Ingestion)
* **Extraction Method:** Implemented a **Pull Extraction** strategy.
* **Extraction Type:** **Full Extraction** of source datasets.
* **Techniques:** Utilized **File Parsing** to ingest raw CSV data into the staging environment.

### 2. Transformation (Data Refining)
Data was cleaned and enriched using advanced SQL techniques to ensure it was "analytics-ready":

* **Data Cleansing:** * Performed **Data Type Casting** for schema consistency.
    * Removed duplicates and applied **Data Filtering** to eliminate noise.
    * Handled missing data (NULLs), invalid values, and unwanted white spaces.
    * Identified and handled anomalies through **Outlier Detection**.
* **Data Integration & Enrichment:** * Unified disparate data from multiple sources (CRM + ERP).
    * Created **Derived Columns** and implemented **Business Rules & Logic**.
    * Applied **Normalization and Standardization** for unified naming conventions.
    * Performed **Data Aggregations** to pre-calculate key metrics.

### 3. Load (Data Warehousing)
* **Processing Type:** Optimized for **Batch Processing**.
* **Load Methods:** Implemented various strategies including **Full Load** (Truncate & Insert, Drop & Create) and **Upsert** for incremental updates.
* **Slowly Changing Dimensions (SCD):** Applied **SCD Type 1** logic to maintain the most current state of Dimension tables (Customers/Products) without keeping historical changes.

### 🗺️ Schema Diagram
Below is the Entity Relationship Diagram (ERD) representing the data warehouse structure:

<p align="center">
  <img src="docs/data_model.png" alt="Data Model Diagram" width="800">
</p>

### Data Model Structure:
* **Fact Table (`gold.fact_sales`):** Stores business metrics like `sales_amount`, `quantity`, and `price`, linked via foreign keys to dimensions.
* **Dimension Tables:**
    * **`gold.dim_customers`:** A unified master record for customers, including demographics like country, marital status, and gender.
    * **`gold.dim_products`:** A centralized product catalog with attributes like category, product line, and cost.

### Relationships:
The model utilizes a **One-to-Many (1:M)** relationship, ensuring high-speed joins and an intuitive structure for dashboarding in Power BI.

---

## 🔍 Exploratory Data Analysis (EDA)

Before proceeding to advanced visualization, I performed a deep dive into the Gold layer to validate data integrity, understand the business footprint, and audit the quality of the dataset.

### 1. Business Footprint & Sales Performance
A comprehensive audit of the dataset reveals a healthy 4-year operational span:
* **Time Coverage:** From **2010-12-29** to **2014-01-28**.
* **Revenue:** A total of **29,356,250** in sales generated from **60,423** items.
* **Order Structure:** I identified **27,659 unique orders** spanning **60,398 order lines**. 
    * This indicates that a typical order contains multiple items (**~2.18 items per order**).

### 2. Efficiency & Value Metrics (Derived Insights)
* **Average Order Value (AOV):** **1,061.36** (Calculated from Sales / Unique Orders).
* **Revenue per Item:** **485.85** (This perfectly aligns with the reported **Average Price of 486**, confirming cross-table consistency).
* **Customer Value:** Every customer in this dataset is 'active,' contributing an average of **1,588.20** in revenue over the period.

### 3. Product Catalog Composition (Assortment)
The product catalog consists of **295 unique SKUs**, showing a heavy focus on high-ticket and technical items:
* **Core Focus:** **Components (44.1%)** and **Bikes (33.7%)** make up **~78%** of the inventory.
* **Supplementary:** Clothing (12.2%) and Accessories (10.1%) complete the assortment.

### 4. Customer Demographics & Data Quality Observations 🚩
* **Gender Balance:** The base is nearly perfectly balanced with **50.6% Male** and **49.4% Female** customers.
* **Age Distribution Red Flag:** While the youngest customer is **40**, the oldest birthdate recorded results in an age of **110**. 
* **Data Quality Note:** An age of 110 is unusual for this retail profile. This has been flagged as a potential **data-quality artifact** (placeholder or default birthdate), requiring careful handling during targeted segmentation.
  
---

## 📊 Dashboard

---

## 💡 Business Insights

---

## 🛠️ Tech Stack
