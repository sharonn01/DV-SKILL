Healthcare Dataset EDA — Billing, Stay Duration & Admission Trends
Author: Sharon N
Assignment: Task 6

## Overview

This project extends the earlier healthcare dataset cleaning (Task 5) into a fuller exploratory data analysis (EDA). It examines how billing costs, hospital stay duration, and admission volume vary across medical conditions, insurance providers, and time, and tests the relationships between patient age, stay length, and billing amount.

The analysis is implemented in Python using a Jupyter/Colab notebook and script (`Task-6.ipynb` / `Task_6.py`).

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
- **seaborn** – statistical visualization (violin plot, heatmap)

## Project Workflow

The notebook/script follows a four-stage EDA pipeline:

1. **Data Preparation**
   - Load `healthcare_dataset.csv` into a DataFrame.
   - Inspect with `df.head()`, `df.shape`, `df.describe()`.
   - Check for missing values (`df.isnull().sum()`) and drop them (`df.dropna()`).
   - Convert `Date of Admission` and `Discharge Date` to timezone-aware datetime objects.
2. **Feature Engineering**
   - `Hospital_Stays` — length of stay in days, calculated as `Discharge Date − Date of Admission`.
   - `Admission Month` — the admission date truncated to year-month, for trend tracking.
3. **Financial Analysis**
   - Group billing amounts by `Medical Condition` and `Insurance Provider`, then visualize as a stacked bar chart to compare total spend across condition/insurer combinations.
4. **Clinical and Temporal Analysis**
   - Violin plot of `Hospital_Stays` by `Medical Condition` to compare stay-length distributions.
   - Line chart of monthly admission counts to track volume trends over time.
   - Correlation matrix (and heatmap) between `Age`, `Hospital_Stays`, and `Billing Amount`.

## Visualizations

| Chart | What it shows |
|---|---|
| Stacked Bar Chart (Billing by Condition & Insurer) | Total billing amount per medical condition, segmented by insurance provider — highlights which condition/insurer pairs drive the highest costs. |
| Violin Plot (Hospital Stay Distribution) | Full distribution of stay lengths per medical condition, including spread and clustering, not just the average. |
| Line Chart (Monthly Admissions) | Number of admissions per month, used to spot upward/downward trends or seasonality. |
| Heatmap (Correlation Matrix) | Strength of relationship between Age, Hospital Stays, and Billing Amount, from -1 to +1. |

## Key Insights

- Billing costs vary by both medical condition and insurance provider — the stacked bar chart identifies which combinations contribute most to total healthcare spend.
- Hospital stay length differs across medical conditions, with some conditions showing wider or more unpredictable stay distributions than others.
- Monthly admission counts reveal whether patient volume is growing, shrinking, or seasonal.
- The correlation matrix tests whether older patients or longer stays are associated with higher billing amounts.

## Repository Structure

```
.
├── Task-6.ipynb              # Main analysis notebook
├── Task_6.py                  # Script version of the analysis
├── healthcare_dataset.csv     # Raw dataset
└── README.md                  # Project documentation
```

## How to Run

1. Clone or download this repository.
2. Ensure `healthcare_dataset.csv` is in the same directory as the script (or update the file path in the script to match its location, e.g. `/content/drive/MyDrive/Colab Notebooks/healthcare_dataset (1).csv` for Google Colab).
3. Install the required libraries if not already available:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
4. Run the script:
   ```bash
   python Task_6.py
   ```
