# Retail Sales Data (EDA)

End-to-end exploratory data analysis on a retail sales dataset using Python, pandas, matplotlib, and seaborn — completed as Task 1 (Level 1) of the OIBSIP Data Analytics track.

---

## Project Overview

This project performs a thorough exploratory data analysis on a retail sales dataset to uncover sales patterns, customer behaviour trends, and actionable business insights. The workflow covers initial inspection, descriptive statistics, time series analysis, customer demographics, product analysis, correlation analysis, and a custom non-obvious insight — closing with data-driven business recommendations.

---

## Dataset

- **Source:** Kaggle — Retail Sales Dataset
- **Size:** 1,000 rows × 9 columns
- **Columns:** Transaction ID, Date, Customer ID, Gender, Age, Product Category, Quantity, Price per Unit, Total Amount

---

## Workflow

### Step 1 — Library Imports

Imported `pandas`, `numpy`, `matplotlib.pyplot`, and `seaborn` for data manipulation and visualization.

### Step 2 — Initial Inspection

- `df.shape` — confirmed 1,000 rows and 9 columns
- `df.dtypes` — checked column types, converted `Date` to `datetime64` with `pd.to_datetime(..., format='mixed')`
- `df.isnull().sum()` / `df.duplicated().sum()` — checked for nulls and duplicate rows
- Descriptive statistics (mean, median, mode, standard deviation) computed for all numerical columns

### Step 3 — Time Series Analysis

- Created `Month` and `Quarter` period columns from `Date`
- Plotted **Monthly Sales Trend** and **Quarterly Sales Trend** line charts
- Investigated an unexpected September dip by comparing transaction counts per month against total sales, isolating whether the drop was driven by fewer transactions or smaller average purchases

### Step 4 — Customer Demographics

- **Gender Distribution** (pie chart) — Female 51.0%, Male 49.0%
- **Age Distribution** (pie chart) — binned into Under 20s, Twenties, Thirties, Forties, Fifties, and 60s and above using `pd.cut()`

### Step 5 — Product Analysis

- Grouped revenue and quantity sold by `Product Category`
- Compared **Product by Revenue** and **Product by Quantity Sold** (bar charts) side by side

### Step 6 — Correlation Analysis

- Built a correlation heatmap (`seaborn.heatmap`) across Transaction ID, Age, Quantity, Price per Unit, and Total Amount
- Identified the strongest relationships driving revenue

### Step 7 — Non-Obvious Insight

- Built a **Sales per Weekday** bar chart (average sales by day, reordered Monday–Sunday) to test whether the "weekends drive higher sales" assumption held
- Built a custom **Transactions per Month** bar chart to investigate whether September's revenue dip was driven by fewer transactions or smaller average purchases


---

## Key Insights

- **Price per Unit and Total Amount** are strongly correlated (r = 0.85), while **Quantity and Total Amount** are only moderately correlated (r = 0.37) — revenue is driven far more by item price than by purchase volume
- **Quantity and Price per Unit** are essentially uncorrelated (r = 0.02) — pricing does not influence how many units customers buy per transaction
- **Saturday** generates the highest average sales, followed by Monday, while **Wednesday** is the weakest day — notably, **Sunday does not follow the weekend pattern**, behaving more like a mid-week day
- **September** shows the lowest transaction volume of the year (65 transactions), which — combined with its sales dip — points to a genuine drop in customer visits rather than smaller purchases
- **Electronics** generates the highest revenue (₦156,905) despite not having the highest quantity sold, while **Beauty** is lowest on both metrics
- **Gender** is nearly evenly split (51% Female, 49% Male), and **age** is fairly evenly distributed across the Twenties through Fifties brackets, with under-20s and 60+ customers making up only 13.5% combined

---

## Recommendations

1. **Align staffing and stock with the weekday pattern** — since Saturday consistently outperforms other days while Wednesday lags, schedule additional staff and inventory ahead of weekends, and consider a mid-week promotion to lift Wednesday sales
2. **Prioritize price over volume in promotions** — since revenue is driven overwhelmingly by item price rather than quantity purchased, focus on upselling, bundling, and premium product placement rather than "buy more, save more" style discounts
3. **Take a broad-audience approach to marketing** — with gender and age fairly evenly distributed, avoid narrow demographic targeting and instead lean into messaging that resonates with the core 40s–50s customer base

---

## How to Run

1. Clone the repository

```
git clone https://github.com/ChimchetamIbeh/OIBSIP.git
cd OIBSIP/DataAnalytics-L1-EDARetailSales
```

2. Install dependencies

```
pip install pandas numpy matplotlib seaborn
```

3. Open the notebook

```
jupyter notebook Retail_Sales_Analysis.ipynb
```

> The dataset path in the notebook references a local file. Update the path in the `pd.read_csv()` call to match your local setup, or place the retail sales CSV in the same folder as the notebook.
