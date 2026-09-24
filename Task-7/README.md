Students Performance Analysis
Author: Sharon N
Assignment: Task 7

## Overview

This project performs exploratory data analysis (EDA) on a student performance dataset containing demographic information and exam scores. The goal is to inspect the data, compute descriptive statistics for exam scores, and engineer new features summarizing each student's overall performance.

The analysis is implemented in Python using a Jupyter/Colab notebook and script (`Task-7.ipynb` / `task_7.py`).

## Dataset

**File:** `StudentsPerformance.csv`

| Property | Value |
|---|---|
| Rows | 1,000 |
| Columns | 8 |

### Columns

| Column | Description |
|---|---|
| gender | Student gender |
| race/ethnicity | Student race/ethnicity group |
| parental level of education | Highest education level attained by a parent |
| lunch | Lunch type (standard or free/reduced) |
| test preparation course | Whether the student completed a test prep course |
| math score | Math exam score |
| reading score | Reading exam score |
| writing score | Writing exam score |

## Tools & Libraries

- Python 3
- **pandas** – data loading, cleaning, and aggregation
- **matplotlib** – data visualization
- **seaborn** – statistical visualization

## Project Workflow

The notebook/script follows a standard EDA pipeline:

1. **Import Libraries** – Load pandas, matplotlib, and seaborn.
2. **Load Data** – Read `StudentsPerformance.csv` into a DataFrame.
3. **Initial Inspection**
   - `df.head()` / `df.tail()` – Preview the first and last few rows.
   - `df.describe()` – View summary statistics for numeric columns.
   - `df.shape` – Check the dimensions of the dataset.
   - `df.columns` – List all column names.
   - `df.info()` – Check column data types and non-null counts.
4. **Data Quality Checks**
   - `df.isnull().sum()` – Check for missing values.
   - `df.duplicated().sum()` – Check for duplicate rows.
5. **Score Statistics** – For `math score`, `reading score`, and `writing score`:
   - Descriptive statistics (`describe()`)
   - Mean, median, standard deviation, and quantiles.
6. **Feature Engineering**
   - `Total Score` — the sum of math, reading, and writing scores.
   - `percentage` — `Total Score / 300 * 100`, giving each student's overall percentage.

## Key Insights

- The dataset covers 1,000 students with demographic attributes alongside math, reading, and writing scores.
- Descriptive statistics (mean, median, standard deviation, quantiles) for each subject score give a baseline for how students perform across the three exams.
- The engineered `Total Score` and `percentage` columns summarize each student's overall academic performance in a single figure, enabling further comparison across groups such as gender, lunch type, or test preparation status.

## Repository Structure

```
.
├── Task-7.ipynb                 # Main analysis notebook
├── task_7.py                     # Script version of the analysis
├── StudentsPerformance.csv       # Raw dataset
└── README.md                     # Project documentation
```

## How to Run

1. Clone or download this repository.
2. Ensure `StudentsPerformance.csv` is in the same directory as the script (or update the file path in the script to match its location, e.g. `/content/drive/MyDrive/Colab Notebooks/StudentsPerformance.csv` for Google Colab).
3. Install the required libraries if not already available:
   ```bash
   pip install pandas matplotlib seaborn
   ```
4. Run the script:
   ```bash
   python task_7.py
   ```
