# Titanic-Data-Cleaning

Data cleaning on the Titanic dataset — transforming a messy, real-world dataset into a clean, analysis-ready one.

# Titanic Dataset Cleaning with Python

---

## Project Overview

This project demonstrates a complete data cleaning workflow in Python; taking the Titanic dataset from its raw, messy state through to a fully cleaned, analysis-ready dataset. Every cleaning decision is backed by a "data quality report," justified in markdown, and verified with a before/after comparison.

---

## Dataset

- **Source:** Kaggle; Titanic Dataset (891 rows, 12 columns)
- **Columns include:** PassengerId, Survived, Pclass, Name, Sex, Age, SibSp, Parch, Ticket, Fare, Cabin, Embarked

---

## Workflow

### Step 1 - Data Quality Report

- Checked dataset shape, data types, null counts, and duplicate rows
- Ran summary statistics (`.describe()`) to catch value range anomalies
- Findings: `Age` had 177 missing values, `Cabin` had 687 missing (77%), `Embarked` had 2 missing, and 0 duplicate rows

### Step 2 - Missing Data Handling

- `Age`: Extracted passenger titles (Mr, Mrs, Miss, Master, etc.) from the `Name` column, since age varies meaningfully by title. Missing ages were filled using the median age within each title group, rather than a single overall median, to avoid distorting age patterns (e.g., filling a missing child's age with an adult average)
- `Cabin`: 77% missing values made imputation unreliable. Converted into a binary `Has_Cabin` feature instead, and the original column dropped
- `Embarked`: Only 2 missing. Filled with `'U'` (Unknown) to stay consistent with the existing single-letter port codes (S, C, Q)

### Step 3 — Duplicate Removal

- Confirmed 0 duplicate rows in the dataset; no rows removed

### Step 4 — Standardisation

- Verified `Sex` and `Embarked` had no case mismatches or inconsistent labels
- Converted `Sex` to title case (`Male`/`Female`) for formatting consistency
- No date columns present requiring reformatting

### Step 5 — Outlier Detection

- **Fare:** Z-score method flagged 20 outliers (~2.2%), confirmed to be primarily 1st class passengers. Capped to the maximum non-outlier fare within 1st class, rather than a global threshold, to preserve realistic class-based pricing. 
- **Age:** Z-score method flagged 7 outliers, corresponding to elderly passengers. Retained as-is, since these represent real passengers rather than data errors

### Step 6 — Data Type Correction

- Reviewed all column dtypes; found them already appropriately typed (numeric columns as int64/float64, categorical columns as object). No corrections required

### Step 7 — Before/After Summary

- Produced a before/after comparison table covering null counts, duplicate counts, and row counts, plus a separate outlier summary documenting the decisions made for `Fare` and `Age`

### Step 8 — Export

- Saved the cleaned dataset to `titanic_cleaned.csv`

---

## Key Insights

- Missing data isn't random. `Age`'s missingness and `Cabin`'s near-total absence both hint at real historical patterns rather than arbitrary gaps — cabin numbers were mainly recorded for 1st class passengers, which is why converting `Cabin` into a `Has_Cabin` flag preserved more useful signal than trying to impute 687 missing values outright
- Group-aware imputation matters. Filling missing `Age` values using the median within each passenger title (Mr, Mrs, Miss, Master, etc.) avoided a common mistake — a single dataset-wide median would have quietly turned children (title "Master") into adults in the cleaned data
- Not all outliers should be treated the same way. `Fare` outliers were capped to a class-specific ceiling, since 1st class fares are legitimately higher rather than erroneous, while `Age` outliers were retained as-is, since elderly passengers are real people, not data errors
- Small missingness still needs a documented decision. Even though `Embarked` was only missing 2 out of 891 values, it still required a deliberate, explainable choice (filling with `'U'` to match the existing single-letter port format) rather than being ignored

---

## How to Run

1. Clone the repository

```
git clone https://github.com/ChimchetamIbeh/OIBSIP.git
cd OIBSIP/DataAnalytics-L1-CleaningDataTitanic
```

2. Install dependencies

```
pip install pandas numpy 
```

3. Open the notebook

```
jupyter notebook Cleaning_Data.ipynb
```

> The dataset path in the notebook references a local file. Update the path in the `pd.read_csv()` call to match your local setup, or place the Titanic dataset CSV in the same folder as the notebook.
