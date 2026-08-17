# 🏨 Hotel Booking Data Pipeline & Dashboard Development on Snowflake

A end-to-end data engineering project that builds a multi-layered data pipeline for hotel booking analytics using Snowflake's cloud data platform. Raw booking data is ingested, cleaned, transformed, and aggregated through a Bronze → Silver → Gold medallion architecture, culminating in an interactive business dashboard.

---

## 📌 Project Overview

This project demonstrates how to design and implement a scalable data pipeline for hotel booking data using Snowflake. It follows the **Medallion Architecture** (Raw → Bronze → Silver → Gold) to progressively refine data from raw ingestion to business-ready aggregates, enabling meaningful insights through dashboards.

---

## 🏗️ Architecture

```
Raw Data  →  Bronze Layer  →  Silver Layer  →  Gold Layer  →  Dashboard
(Ingestion)   (Cleaning)      (Transformation)  (Aggregation)   (Insights)
```

| Layer | Description |
|-------|-------------|
| **Raw Data** | Original source data loaded into Snowflake staging area as-is |
| **Bronze** | Initial processing — data type casting, deduplication, basic validation |
| **Silver** | Business transformations — joins, derived columns, data enrichment |
| **Gold** | Aggregated summary tables optimized for reporting and dashboards |

---

## 📁 Repository Structure

```
Hotel-Booking-Data-Pipeline-and-Dashboard-Development-on-Snowflake/
│
├── Raw Data/                    # Source CSV/data files for hotel bookings
│
├── Bronze Processing/           # SQL scripts for Bronze layer (ingestion & cleaning)
│
├── Silver Transformation/       # SQL scripts for Silver layer (business transformations)
│
├── Gold Aggregate/              # SQL scripts for Gold layer (aggregated metrics)
│
├── Business_Requirement.docx    # Business requirements and KPI definitions
│
└── README.md
```

---

## 🔧 Tech Stack

| Tool | Purpose |
|------|---------|
| **Snowflake** | Cloud data warehouse — storage, compute, and SQL processing |
| **SQL** | Data transformation and aggregation logic across all layers |
| **Snowflake Stages** | Staging raw data files before loading |
| **Snowflake Tasks / Streams** | Orchestrating pipeline execution (if applicable) |
| **Snowflake Dashboard** | Built-in visualization for KPI reporting |

---

## 🚀 Getting Started

### Prerequisites

- A Snowflake account (free trial available at [snowflake.com](https://www.snowflake.com))
- Basic knowledge of SQL and Snowflake architecture
- Access to the raw hotel booking dataset

### Setup Steps

**1. Clone the Repository**

```bash
git clone https://github.com/Shandeep-Raula/Hotel-Booking-Data-Pipeline-and-Dashboard-Development-on-Snowflake.git
cd Hotel-Booking-Data-Pipeline-and-Dashboard-Development-on-Snowflake
```

**2. Set Up Snowflake Environment**

```sql
-- Create a dedicated database and warehouse
CREATE DATABASE HOTEL_BOOKING_DB;
CREATE WAREHOUSE HOTEL_WH WITH WAREHOUSE_SIZE = 'X-SMALL' AUTO_SUSPEND = 60;
USE DATABASE HOTEL_BOOKING_DB;
```

**3. Load Raw Data**

Upload the raw CSV files from the `Raw Data/` folder into a Snowflake internal stage or external stage (S3/Azure Blob), then load into raw tables:

```sql
-- Example: Create a stage and copy data
CREATE STAGE hotel_raw_stage;
PUT file://path/to/raw_data.csv @hotel_raw_stage;
COPY INTO RAW_HOTEL_BOOKINGS FROM @hotel_raw_stage FILE_FORMAT = (TYPE = 'CSV' SKIP_HEADER = 1);
```

**4. Run Bronze Layer Scripts**

Execute all SQL scripts in the `Bronze Processing/` folder to clean and standardize raw data:

```sql
-- Run Bronze layer transformations
-- Handles: data type casting, deduplication, null handling, basic validation
```

**5. Run Silver Layer Scripts**

Execute scripts in `Silver Transformation/` to apply business logic and enrich data:

```sql
-- Run Silver layer transformations
-- Handles: joins, derived columns, booking status classification, date calculations
```

**6. Run Gold Layer Scripts**

Execute scripts in `Gold Aggregate/` to build summary tables for reporting:

```sql
-- Run Gold layer aggregations
-- Handles: KPI computation, revenue summaries, occupancy rates, booking trends
```

**7. Build Dashboard**

Connect your Snowflake Gold layer tables to Snowflake's built-in dashboards or export to a BI tool (e.g., Tableau, Power BI, Streamlit) for visualization.

---

## 📊 Key Business Metrics (KPIs)

Based on the business requirements, the pipeline supports the following analytics:

| KPI | Description |
|-----|-------------|
| **Total Bookings** | Total number of hotel reservations over a period |
| **Cancellation Rate** | Percentage of bookings that were cancelled |
| **Average Daily Rate (ADR)** | Average revenue earned per occupied room per day |
| **Revenue Per Available Room (RevPAR)** | Total revenue divided by available rooms |
| **Occupancy Rate** | Percentage of available rooms that are occupied |
| **Lead Time Analysis** | Average number of days between booking and check-in |
| **Booking Channel Distribution** | Breakdown by direct, OTA, corporate, walk-in, etc. |
| **Repeat Guest Rate** | Proportion of returning guests vs new guests |
| **Country-wise Demand** | Geographic distribution of guest origins |
| **Seasonal Trends** | Monthly/quarterly booking and revenue patterns |

---

## 🔄 Data Pipeline Flow

```
1. Raw CSV data uploaded to Snowflake stage
        ↓
2. Bronze Layer — Ingest & Clean
   • Cast data types
   • Remove duplicates
   • Handle nulls and invalid values
   • Standardize formats (dates, strings)
        ↓
3. Silver Layer — Transform & Enrich
   • Apply business rules
   • Derive new columns (stay duration, total revenue, etc.)
   • Join with dimension tables (hotel type, country, segment)
   • Classify booking status (confirmed, cancelled, no-show)
        ↓
4. Gold Layer — Aggregate
   • Compute KPIs and summary metrics
   • Create fact and dimension tables for reporting
   • Optimize for query performance
        ↓
5. Dashboard — Visualize
   • Interactive charts and tables
   • Filter by date, hotel type, market segment, country
```

---

## 📋 Business Requirements

Refer to [`Business_Requirement.docx`](./Business_Requirement.docx) for the full list of stakeholder requirements, KPI definitions, and expected dashboard outputs.



