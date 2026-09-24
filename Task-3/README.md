AAPL Stock Price Analysis
Author: Sharon N
Assignment: Task 3

## Overview

This project performs exploratory data analysis (EDA) on historical AAPL (Apple Inc.) weekly stock price data. The goal is to load and clean the dataset, compute key summary statistics, and engineer a new feature that captures price movement within each trading period.

The analysis is implemented in Python using a Jupyter/Colab notebook and script (`Task-3.ipynb` / `Task-3.py`).

## Dataset

**File:** `AAPL.csv`

| Property | Value |
|---|---|
| Rows | 184 |
| Columns | 7 |
| Frequency | Weekly |

### Columns

| Column | Description |
|---|---|
| Date | Trading week date |
| Open | Opening price |
| High | Highest price during the period |
| Low | Lowest price during the period |
| Close | Closing price |
| Adj Close | Adjusted closing price |
| Volume | Shares traded |

## Tools & Libraries

- Python 3
- **pandas** – data loading, cleaning, and aggregation
- **numpy** – numerical operations
- **matplotlib** – data visualization

## Project Workflow

The notebook/script follows a standard EDA pipeline:

1. **Import Libraries** – Load pandas, numpy, and matplotlib.
2. **Load Data** – Read `AAPL.csv` into a DataFrame.
3. **Initial Inspection**
   - `df.head()` – Preview the first few rows.
   - `df.shape` – Check the dimensions of the dataset.
   - `df.info()` – Check column data types and non-null counts.
4. **Data Cleaning**
   - `df.dropna()` – Remove rows with missing values.
   - `df.drop_duplicates()` – Remove duplicate rows.
5. **Summary Statistics**
   - Average Open price and average Close price.
   - Highest High price and lowest Low price across the dataset.
6. **Feature Engineering** – Create a new column, `Delta`, calculated as `Close - Open`. This measures the net price change within each trading period.

## Key Insights

- The dataset covers weekly AAPL price history with Open, High, Low, Close, Adjusted Close, and Volume figures.
- Average open and close prices give a quick baseline for typical trading levels over the period.
- The highest High and lowest Low mark the full price range observed in the dataset.
- The engineered `Delta` column (`Close - Open`) highlights which weeks closed higher or lower than they opened, useful for spotting bullish vs. bearish periods.

## Repository Structure

```
.
├── Task-3.ipynb       # Main analysis notebook
├── Task-3.py           # Script version of the analysis
├── AAPL.csv            # Raw dataset
└── README.md           # Project documentation
```

## How to Run

1. Clone or download this repository.
2. Ensure `AAPL.csv` is in the same directory as the script (or update the file path in the script to match its location, e.g. `/content/drive/MyDrive/Colab Notebooks/AAPL.csv` for Google Colab).
3. Install the required libraries if not already available:
   ```bash
   pip install pandas numpy matplotlib
   ```
4. Run the script:
   ```bash
   python Task-3.py
   ```
