# Sales-dashboard
# 📊 Data Analytics & Business Intelligence — Task 1

**Data Cleaning, Exploratory Data Analysis (EDA), SQL Querying, Dashboard Development & Business Reporting**

> Internship Task-1 · Maincrafts Technology
> Prepared by **Amirthaa** — B.Tech CSE (AI & Data Science), Joy University, Tirunelveli
> Dataset: Superstore Sales Dataset

---

## 📌 Table of Contents

- [Objective](#-objective)
- [Dataset Overview](#-dataset-overview)
- [Tools Used](#-tools-used)
- [Project Structure](#-project-structure)
- [Part A: Data Cleaning (Excel)](#part-a--data-cleaning-using-excel)
- [Part B: Exploratory Data Analysis (Excel)](#part-b--exploratory-data-analysis-eda-in-excel)
- [Part C: SQL Data Extraction](#part-c--sql-data-extraction)
- [Part D: Power BI / Tableau Dashboard](#part-d--power-bi--tableau-dashboard)
- [Business Insights Report](#-business-insights-report)
- [Challenges & Learnings](#-challenges--learnings)
- [Deliverables](#-deliverables)
- [Conclusion](#-conclusion)

---

## 🎯 Objective

This project builds the core foundation of the data analytics workflow — taking a raw, imperfect business dataset and progressively transforming it into cleaned data, structured analysis, a queryable database, an interactive dashboard, and a business-ready insights report.

In real organizations, **70–80% of analytics work** involves cleaning and preparing data before any meaningful analysis happens. This task simulates that reality end-to-end.

---

## 🗂 Dataset Overview

**Superstore Sales Dataset** — 600+ rows of retail transaction data.

| Field | Description |
|---|---|
| `Order ID` | Unique identifier for each transaction |
| `Order Date` | Date the order was placed |
| `Customer Name` | Name of the purchasing customer |
| `Region` | Geographic region (East, West, North, South) |
| `Category` | Product category |
| `Sales` | Revenue generated |
| `Quantity` | Units sold |
| `Profit` | Profit earned |
| `Discount` | Discount rate applied |

---

## 🛠 Tools Used

- **Microsoft Excel** — data cleaning, formulas, pivot tables
- **MySQL Workbench / SSMS** — SQL data extraction
- **Power BI / Tableau** — interactive dashboarding
- **GitHub** — documentation & version control

---

## 📁 Project Structure

```
├── data/
│   ├── raw_sales_data.xlsx
│   └── cleaned_sales_data.xlsx
├── sql/
│   └── queries.sql
├── dashboard/
│   ├── sales_dashboard.pbix
│   └── dashboard_screenshot.png
├── report/
│   └── business_insights_report.pdf
└── README.md
```

> 📌 *Adjust this tree to match your actual repo folders/filenames.*

---

## Part A — Data Cleaning Using Excel

### Step 1: Inspecting the Raw Data

The raw dataset was audited for:

- Missing values
- Duplicate rows
- Incorrect date formats
- Blank cells
- Inconsistent text casing (e.g. `East`, `EAST`, `east`)

`COUNTIF` and `ISNUMBER` were used to quantify the scale of each issue before deciding on a cleaning strategy, and Conditional Formatting was used to visually surface duplicates and blanks.

### Step 2: Cleaning the Data

| Function / Feature | Purpose |
|---|---|
| `TRIM` | Removed leading/trailing/extra spaces from text fields |
| `PROPER` | Standardized text casing for consistent grouping |
| `IF` | Flagged records failing validation checks |
| `ISNUMBER` | Verified numeric fields held valid numeric data |
| `COUNTIF` | Counted duplicates and inconsistent entries |
| `MID` / `FIND` | Extracted/corrected substrings in ID and date fields |
| Data Validation | Restricted future entry errors on Region/Category |
| Conditional Formatting | Highlighted duplicates, blanks, outliers |
| Remove Duplicates | Removed exact duplicate rows |

**Cleaning steps performed:**

1. Removed duplicate rows (confirmed with `COUNTIF` before deleting)
2. Flagged missing values in critical fields (`Sales`, `Profit`) rather than silently imputing them
3. Converted `Order Date` to a consistent `DD-MM-YYYY` format
4. Standardized `Region`/`Category` text using `TRIM` + `PROPER`
5. Verified numeric columns were properly typed using `ISNUMBER`

Final output saved as **`cleaned_sales_data.xlsx`**.

> 📌 *Insert a before/after screenshot of the raw vs. cleaned data, and note the row count removed during dedup.*

---

## Part B — Exploratory Data Analysis (EDA) in Excel

### Step 3: Summary Metrics

| Metric | Formula | Value |
|---|---|---|
| Total Sales | `SUM(Sales)` | `[insert]` |
| Total Profit | `SUM(Profit)` | `[insert]` |
| Total Orders | `COUNT(Order ID)` | `[insert]` |
| Average Order Value | `AVERAGE(Sales)` | `[insert]` |
| Total Quantity Sold | `SUM(Quantity)` | `[insert]` |

### Step 4: Analysis by Business Dimension

Five Pivot Tables were built:

1. **Sales by Region**
2. **Profit by Category**
3. **Sales by Month**
4. **Top 10 Customers**
5. **Top 5 Products**

> 📌 *Insert pivot table screenshots + a one-line takeaway under each.*

---

## Part C — SQL Data Extraction

### Step 5: Table Schema

```sql
CREATE TABLE sales (
    order_id VARCHAR(50),
    order_date DATE,
    customer_name VARCHAR(100),
    region VARCHAR(50),
    category VARCHAR(50),
    sales DECIMAL(10,2),
    quantity INT,
    profit DECIMAL(10,2),
    discount DECIMAL(5,2)
);
```

> **Import note:** Importing `.xlsx` directly via MySQL Workbench's Restore tool fails (it expects a SQL dump, not a spreadsheet). Fix: export to CSV first, then use the **Table Data Import Wizard**. Also note MySQL (`DATE_FORMAT()`) and SQL Server/SSMS (`FORMAT()`) use different date-formatting syntax — queries aren't directly portable between the two.

### Step 6: Queries

**1. Total sales by region**
```sql
SELECT region, SUM(sales) AS total_sales
FROM sales
GROUP BY region;
```

**2. Top profitable categories**
```sql
SELECT category, SUM(profit) AS total_profit
FROM sales
GROUP BY category
ORDER BY total_profit DESC
LIMIT 5;
```

**3. Monthly sales trend**
```sql
SELECT MONTH(order_date) AS month,
       SUM(sales) AS total_sales
FROM sales
GROUP BY month
ORDER BY month;
```

**4. Discount impact on profit**
```sql
SELECT discount, AVG(profit) AS avg_profit
FROM sales
GROUP BY discount;
```

> 📌 *Insert actual query result screenshots/values here.*

---

## Part D — Power BI / Tableau Dashboard

### Step 7: Visualizations

| Visualization | Purpose |
|---|---|
| KPI Cards | Total Sales, Total Profit, Total Orders |
| Bar Chart | Sales by Region |
| Line Chart | Monthly Sales Trend |
| Pie Chart | Category Distribution |
| Top Customers Table | Ranked high-value customers |

### Step 8: Filters / Slicers

- Region filter
- Category filter
- Date filter

> 📌 *Insert dashboard screenshot below:*
>
> `![Dashboard Screenshot](dashboard/dashboard_screenshot.png)`

---

## 📈 Business Insights Report

| Question | Finding |
|---|---|
| Which region generates the highest sales? | `[insert finding]` |
| Which category is most profitable? | `[insert finding]` |
| Are discounts affecting profit? | `[insert finding]` |
| Which month performs best? | `[insert finding]` |

### Key Recommendations for Management

- `[Insert recommendation based on regional performance]`
- `[Insert recommendation based on category profitability]`
- `[Insert recommendation based on discount analysis]`
- `[Insert recommendation based on seasonal trend]`

---

## 🧩 Challenges & Learnings

- MySQL Workbench's Restore tool cannot import `.xlsx` directly — resolved via CSV export + Import Wizard
- `DATE_FORMAT()` (MySQL) vs `FORMAT()` (SQL Server) are not interchangeable across platforms
- `TRIM` + `PROPER` together were needed to fully standardize region names — `PROPER` alone doesn't strip extra whitespace, which silently breaks `GROUP BY`

> 📌 *Add any challenges specific to your own process.*

---

## ✅ Deliverables

- [ ] Cleaned Excel file (`cleaned_sales_data.xlsx`)
- [ ] SQL query file (`.sql`)
- [ ] Power BI (`.pbix`) / Tableau file
- [ ] Dashboard screenshot
- [ ] Business insights report (PDF)

---

## 🏁 Conclusion

This task delivered hands-on, end-to-end exposure to the analytics workflow used in professional data analyst roles — from a messy, real-world-style dataset through to a business-ready insights report. Beyond individual tool skills (Excel formulas, Pivot Tables, SQL aggregation, Power BI/Tableau visualization), it reinforced that most analytics value comes from disciplined data preparation and clear business communication.

---

*Built as part of the Data Analytics & Business Intelligence Internship at Maincrafts Technology.*
