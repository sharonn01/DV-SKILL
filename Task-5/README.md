Healthcare Dataset Analysis
Author: Sharon N
Assignment: Task 5

## Overview

This project performs exploratory data analysis (EDA) on a healthcare records dataset containing patient-level admission and treatment information. The goal is to clean the data, standardize categorical values, and engineer a new feature measuring length of hospital stay.

The analysis is implemented in Python using a Jupyter/Colab notebook and script (`Task-5.ipynb` / `Task-5.py`).

## Dataset

**File:** `healthcare_dataset.csv`

| Property | Value |
|---|---|
| Rows | 55,500 |
| Columns | 15 |

### Columns

| Column | Description |
|---|---|
| Name | Patient name |
| Age | Patient age |
| Gender | Patient gender |
| Blood Type | Patient blood type |
| Medical Condition | Diagnosed medical condition |
| Date of Admission | Date the patient was admitted |
| Doctor | Attending doctor |
| Hospital | Hospital name |
| Insurance Provider | Patient's insurance provider |
| Billing Amount | Amount billed for treatment |
| Room Number | Assigned room number |
| Admission Type | Type of admission (e.g., Urgent, Emergency, Elective) |
| Discharge Date | Date the patient was discharged |
| Medication | Medication prescribed |
| Test Results | Test result outcome (e.g., Normal, Inconclusive) |

## Tools & Libraries

- Python 3
- **pandas** – data loading, cleaning, and aggregation
- **numpy** – numerical operations
- **matplotlib** – data visualization

## Project Workflow

The notebook/script follows a standard EDA pipeline:

1. **Import Libraries** – Load pandas, numpy, and matplotlib.
2. **Load Data** – Read `healthcare_dataset.csv` into a DataFrame.
3. **Initial Inspection**
   - `df.head()` – Preview the first few rows.
   - `df.info()` – Check column data types and non-null counts.
   - `df.isnull()` – Check for missing values.
4. **Data Cleaning** – `df.dropna()` to remove rows with missing values.
5. **Standardize Categorical Values** – Convert the `Admission Type` column to lowercase for consistency.
6. **Data Type Conversion** – Convert `Date of Admission` and `Discharge Date` from strings to timezone-aware datetime objects.
7. **Feature Engineering** – Create a new column, `Total days`, calculated as `Discharge Date − Date of Admission`, giving each patient's length of stay.

## Key Insights

- The dataset covers patient-level hospital records including demographics, admission/discharge dates, billing, and treatment outcomes.
- Standardizing `Admission Type` to lowercase makes the category values consistent for later grouping or filtering.
- The engineered `Total days` column enables analysis of hospital stay duration, which can be broken down by condition, admission type, or hospital in further analysis.

## Repository Structure

```
.
├── Task-5.ipynb              # Main analysis notebook
├── Task-5.py                  # Script version of the analysis
├── healthcare_dataset.csv     # Raw dataset
└── README.md                  # Project documentation
```

## How to Run

1. Clone or download this repository.
2. Ensure `healthcare_dataset.csv` is in the same directory as the script (or update the file path in the script to match its location, e.g. `/content/drive/MyDrive/Colab Notebooks/healthcare_dataset.csv` for Google Colab).
3. Install the required libraries if not already available:
   ```bash
   pip install pandas numpy matplotlib
   ```
4. Run the script:
   ```bash
   python Task-5.py
   ```

## Notes

- The script references columns `Admission_Type`, `Admission_Date`, and `Discharge_Date` (with underscores), but the actual CSV headers use spaces: `Admission Type`, `Date of Admission`, and `Discharge Date`. As written, these lines will raise a `KeyError` — either rename the columns after loading (`df.columns = df.columns.str.replace(" ", "_")`) or update the script to reference the exact column names shown above.
