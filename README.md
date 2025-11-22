# Syntecxhub – Project 2: Pandas CSV Reader & Basic Analysis

This repository contains my Week 1 **Data Science Internship** task for **Project 2 – Pandas CSV reader & basic analysis**.

The goal of this project is to:
- Read CSV files into Pandas DataFrames
- Inspect the data (head, tail, types, info)
- Compute basic summary statistics
- Filter rows, select columns and slice subsets
- Save filtered/subsetted results to CSV/Excel files

---

## 📁 Files in this Repository

- `Project2_Pandas_Analysis.ipynb` – Main Jupyter Notebook with all code and explanations.
- `athlete_events.csv` – Main dataset containing Olympic athlete information.
- `noc_regions.csv` – Mapping of NOC codes to full country/region names.
- `outputs/` – Folder containing saved filtered results:
  - `age_above_30.*` – Athletes older than 30.
  - `medal_winners.*` – Athletes who won a medal.
  - `subset_output.*` – Selected columns (Name, Age, Sex, Sport, Country).
  - `slice_data.*` – First 10 rows (example slice).

(*Files may be in `.csv` or `.xlsx` format depending on environment support.*)

---

## 📊 Dataset Description

### `athlete_events.csv`
Contains information about Olympic athletes:
- `ID` – Athlete ID  
- `Name` – Athlete name  
- `Sex` – Gender (M/F)  
- `Age` – Age (may contain missing values)  
- `Height`, `Weight` – Physical attributes  
- `Team` – Team / country name  
- `NOC` – National Olympic Committee 3-letter code  
- `Games`, `Year`, `Season`, `City` – Olympic edition info  
- `Sport`, `Event` – Sport and event details  
- `Medal` – Medal type (Gold/Silver/Bronze) or empty

### `noc_regions.csv`
- `NOC` – 3-letter country code
- `region` – Full country/region name
- `notes` – Additional notes (if any)

These two datasets are merged on the `NOC` column to add a readable **Country** field.

---

## 🧮 Steps Performed (as per Project Requirements)

1. **Loaded CSV files**
   ```python
   athletes = pd.read_csv("athlete_events.csv")
   noc = pd.read_csv("noc_regions.csv")

2. **Merged datasets on NOC**
   ```python
   merged_df = athletes.merge(noc, on="NOC", how="left")
   merged_df = merged_df.rename(columns={"region": "Country"})

3. **Inspected Data**
   ```python
   merged_df.head()
   merged_df.tail()
   merged_df.info()
   merged_df.dtypes

4. **Computed summary statistics**
   ```python
   merged_df.describe()                    # summary for numeric columns
   merged_df.mean(numeric_only=True)       # mean
   merged_df.median(numeric_only=True)     # median
   merged_df.min(numeric_only=True)        # min
   merged_df.max(numeric_only=True)        # max
   merged_df.count()                       # non-null counts

5. **Filtering operations**
    ```python
   Athletes older than 30:
     age_filter = merged_df[merged_df["Age] > 30]
  
   Athletes who won a medal:
     medal_winners = merged_df[merged_df["Medal"].notna()]

6. **Selecting columns & slicing subsets**
    ```python
    Selected important columns:
     subset = merged_df[["Name", "Age", "Sex", "Sport", "Country"]]
    
   Example slice (first 10 rows):
     slice_data = merged_df.iloc[0:10]

7. **Saved filtered results to files**
    ```python
   age_filter.to_csv("outputs/age_above_30.csv", index=False)
   medal_winners.to_csv("outputs/medal_winners.csv", index=False)
   subset.to_csv("outputs/subset_output.csv", index=False)
   slice_data.to_csv("outputs/slice_data.csv", index=False)

   


