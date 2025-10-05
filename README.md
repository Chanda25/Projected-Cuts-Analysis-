# 📦 Projected Cuts Analysis – End-to-End Data Pipeline & Dashboard

## 🔍 Business Problem

In supply chain operations, **inventory shortages (cuts)** lead to lost sales and cost impact.
The goal of this project is to analyze **forecast demand, available stock, projected cuts, and cost impact** across SKUs and warehouses to:

* Identify high-risk SKUs
* Pinpoint warehouse bottlenecks
* Quantify financial impact of shortages

---

## 🛠️ Project Workflow

This project demonstrates a **complete data pipeline**:

**1️⃣ Data Storage (MySQL – XAMPP)**

* Dataset stored in MySQL database.
* Tables contained daily inventory, forecast demand, and warehouse data.
* Example SQL extraction:

```sql
SELECT 
    Date, Month, Warehouse_ID, SKU_ID, SKU_Name,
    Opening_Stock, Incoming_Qty, Sales_Qty, Closing_Stock,
    Unit_Cost, Available_stock, Forecasted_Demand, Safety_Stock
FROM inventory_data;
```

---

**2️⃣ Data Cleaning & Transformation (Alteryx)**

* Connected to MySQL, imported raw tables.
* Steps performed:

  * Removed duplicates & null values
  * Calculated `Projected_cuts = Forecasted_Demand – Available_stock`
  * Calculated `Projected_cuts_cost = Projected_cuts × Unit_Cost`
  * Exported cleaned data to CSV for visualization

**Workflow Example:**

* Input Data → Join → Formula → Summarize → Output CSV

---

**3️⃣ Visualization & Analytics (Power BI)**

* Imported cleaned CSV files into Power BI.
* Built an interactive **4-page dashboard**:

### 📊 Page 1: Executive Summary

* KPIs: Forecast Demand, Available Stock, Projected Cuts, Cost Impact
* Top 10 SKUs by cuts
* Cuts vs Forecast demand trend

### 📦 Page 2: SKU Analysis

* Drilldown at SKU level
* Cuts % of forecast
* Cost impact per SKU
* Scatter plot: Cuts vs Unit Cost

### 🏭 Page 3: Warehouse Analysis

* Cuts and cost impact by warehouse
* Fulfillment rate %
* Heatmap of SKU × Warehouse

### 💰 Page 4: Cost Analysis

* Total cut cost impact
* Top SKUs and warehouses by financial loss
* Cost trend over time
* Treemap: Cost impact by category

---

## 📂 Repository Structure

```
projected-cuts-analysis/
│
├── README.md                  # Project explanation
├── sql-scripts/               # MySQL queries
│   └── initial_extraction.sql
├── alteryx-workflow/          # Alteryx flow (screenshot / .yxzp file)
│   └── projected_cuts_flow.png
├── data/                      # Cleaned sample data
│   └── cleaned_supply_chain.csv
├── pbix/                      # Power BI report
│   └── projected_cuts.pbix
├── dashboards/                # Dashboard screenshots
│   ├── executive_summary.png
│   ├── sku_analysis.png
│   ├── warehouse_analysis.png
│   └── cost_analysis.png
└── docs/                      # Business problem + data dictionary
    └── data_dictionary.md
```

---

## 📈 Key KPIs & DAX Measures

* **Total Forecast Demand** = `SUM(Forecasted_Demand)`
* **Total Projected Cuts** = `SUM(Projected_cuts)`
* **Projected Cuts % of Forecast** = `DIVIDE([Projected Cuts], [Forecast Demand], 0)`
* **Warehouse Fulfillment Rate** = `(Forecast – Cuts) ÷ Forecast`
* **Total Cost Impact** = `SUM(Projected_cuts_cost)`

---

## 📌 Results & Insights

* Identified **Top 10 SKUs** responsible for 70% of projected cuts.
* **Warehouse X** had the lowest fulfillment rate (~68%).
* High-value SKUs in **Category A** contributed 40% of total cost impact.

---

## 🛠️ Tools & Skills Used

* **XAMPP (MySQL):** Database storage & extraction
* **Alteryx:** ETL, data cleaning, transformation
* **Power BI:** DAX, data modeling, dashboards
* **GitHub:** Project documentation & version control

---

