# 📊 Cyclistic Bike Analysis – Progress Report

## 1. Project Setup
- Initialized project inside **GitHub repo**: `cyclistic-bike-analysis`.
- Structured project folders:
  - `data/raw/2014/H1/` → raw trip data for Q1–Q2.
  - `data/raw/2014/H2/` → raw trip data for Q3–Q4.
  - `notebooks/` → Jupyter notebooks for exploration & preprocessing.
  - `docs/` → Notes and supporting documentation.

---

## 2. Data Discovery
- Inspected files in the `H1` and `H2` directories.  
- Found the following key datasets:
  - `Divvy_Trips_2014_Q1Q2.csv` → trips for the first half of 2014.
  - `Divvy_Trips_2014_H2.csv` → trips for the second half of 2014.
- Verified existence of supporting files like station info (`Divvy_Stations_2014-Q3Q4.csv`) and metadata (`README.txt`).

---

## 3. Data Loading
- Created a Python helper function to **build paths relative to the repo root**:
  ```python
  def repo_path(*parts):
      return os.path.abspath(os.path.join("..", *parts))

- Successfully loaded trip data:
  - H1 (Q1–Q2): **905,699 rows × 12 columns**
  - H2 (Q3–Q4): **1,548,937 rows × 12 columns**

---

## 4. Data Integration
- Combined the datasets using `pandas.concat()`:
  ```python
  trips_2014 = pd.concat([trips_h1, trips_h2], ignore_index=True)

- Result: **2,454,636 total rows × 12 columns.**

---

## 5. Data Verification

- Confirmed that both H1 and H2 datasets have the same schema.
- Verified column names:
   ```bash
   ['trip_id', 'starttime', 'stoptime', 'bikeid', 'tripduration', 'from_station_id', 'from_station_name', 'to_station_id', 'to_station_name', 'usertype', 'gender', 'birthyear']

- Ensured no missing or mismatched columns between H1 and H2.

---

## 6. Challenges & Fixes

- **FileNotFoundError**: initially occurred because of incorrect filenames.
   - Fixed by updating script to use actual dataset names
  (`Divvy_Trips_2014_Q1Q2.csv`, `Divvy_Trips_2014_H2.csv`).
- **Mixed data types warning (DtypeWarning)**: Pandas detected inconsistent data types.
   - Acknowledged but not yet resolved (future task: enforce consistent dtypes on load).

---

## 7. Current Script

Final working script (as of now):
```Python
   import os
   import pandas as pd
   
   # Helper: build paths relative to the repo root
   def repo_path(*parts):
    return os.path.abspath(os.path.join("..", *parts))

   # --- Load H1 data (Q1 & Q2) ---
   h1_path = repo_path("data", "raw", "2014", "H1", "Divvy_Trips_2014_Q1Q2.csv")
   trips_h1 = pd.read_csv(h1_path)

   # --- Load H2 data (Q3 & Q4, combined file) ---
   h2_path = repo_path("data", "raw", "2014", "H2", "Divvy_Trips_2014_H2.csv")
   trips_h2 = pd.read_csv(h2_path)

   # --- Combine H1 and H2 ---
   trips_2014 = pd.concat([trips_h1, trips_h2], ignore_index=True)

   # --- Quick check ---
   print("H1 shape:", trips_h1.shape)
   print("H2 shape:", trips_h2.shape)
   print("Combined shape:", trips_2014.shape)
   print("Columns:", trips_2014.columns.tolist())
```

---

## 8. Next Steps:

- **Data Cleaning**:
   - Standardize dtype (fix mixed types in `trip`, `station_id`, `birthyear`).
   - Handle missing or null values (`gender`, `birthyear`.)
- **Feature Engineering**:
   - Extract time components (`month`, `day`, `hour`, `weekday`) from `starttime`.
- **Data Validation**:
   - Check for duplicate
   - Verfify consistency of station IDs and name across H1 and H2.
- **Exploratory Analysis**:
   - Compare member vs casual user trends.
   - Seasonal ridership patterns (Q1-Q4).
   - Age and gender distributions.