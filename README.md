
# NYC Taxi & HVFHV Data Pipeline 🚖

An end-to-end data engineering pipeline built in **Databricks** using **PySpark** to process and analyze NYC Open Data (TLC Trip Record Data). This project implements a **Medallion Architecture** to transform raw data into business-ready insights for Yellow Taxis, Green Taxis, and High-Volume For-Hire Vehicles (HVFHV).

---

## 🏗️ Architecture: Medallion Design
The pipeline is organized into three distinct layers to ensure data quality and traceability:

1.  **Bronze (Raw):** Ingests raw Parquet/CSV files directly from NYC Open Data. Data is stored in its original schema.
2.  **Silver (Cleaned):** * Handles schema enforcement and data type casting.
    * Removes outliers (e.g., negative distances).
    * **Logic Fix:** Cleans "Zero Fare" records where `total_amount` is positive (handling surcharges and tips).
3.  **Gold (Aggregated):** * Joins taxi data with Location Lookup tables.
    * Creates business-level DataFrames for Market Share analysis, Peak Hour trends, and Revenue per Vendor.

---

## 🏷️ Versioning Strategy
We use **Dataset-Specific Tagging** to manage releases. This allows the Yellow, Green, and HVFHV pipelines to be updated and versioned independently within the same repository.

**Tag Format:** `dataset_name/vX.Y.Z`

* `yellow/v1.0.0`: Stable release for Yellow Taxi logic.
* `green/v1.2.0`: Updated schema for Green Taxi.
* `hvfhv/v2.0.1`: Performance optimizations for High-Volume data.

---

## 🚀 Getting Started in Databricks

### 1. Clone the Repository
1.  In Databricks, go to **Git Folders**.
2.  Click **Add Repo** and paste this GitHub URL.
3.  Ensure your **Personal Access Token (PAT)** is configured in User Settings.

### 2. Dependencies
* **Runtime:** Databricks Runtime 13.x+ (includes Apache Spark 3.4+)
* **Format:** All notebooks are saved as `.ipynb` to preserve output visualizations.



## 📊 Insights & Dashboards
The **Gold Layer** feeds into a Databricks **AI/BI Dashboard** (available in the `dashboards/` folder as `.lvdash.json`). Key metrics include:

* **Market Share:** Percentage of total trips by license type.
* **Efficiency:** Average fare per mile across different boroughs.
* **Tipping Culture:** Analysis of `tip_amount` relative to `payment_type`.

---

## 🛠️ Data Quality Notes
* **Zero Fares:** Records with `$0.00` fare but positive totals are preserved as they represent "comped" rides where taxes/tips were still paid.
* **Location IDs:** Unknown zones (ID 264/265) are filtered out in the Gold layer for mapping accuracy.

---

## 📝 License
This project uses data from [NYC Open Data (TLC)](https://opendata.cityofnewyork.us/). Distribution is subject to the NYC Open Data Terms of Use.

---
