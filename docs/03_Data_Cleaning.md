# 3. Data Cleaning & Manipulation

## Tools Used
- RStudio (tidyverse)
- Microsoft Excel (validation and checks)

## Cleaning Steps
1. **Loaded CSVs** from `data/raw/` into R.
2. **Standardized column names** to match between datasets.
3. **Created calculated fields**:
   - `ride_length` = `ended_at` - `started_at`
   - `day_of_week` = weekday of `started_at`
4. **Converted data types** for time and date fields.
5. **Removed anomalies**:
   - Negative ride lengths
   - Trips longer than 24 hours
6. **Merged datasets** into a single table for comparison.
7. Saved cleaned dataset to `data/cleaned/` as `cyclistic_q1_2019_2020_cleaned.csv`.

## Result
The cleaned dataset contains only valid rides with accurate date, time, and rider type information, ready for descriptive analysis.