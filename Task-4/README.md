Shopify Stock Price Analysis
Author: Sharon N
Assignment: Task 4

## Overview

This project performs exploratory data analysis (EDA) on historical Shopify (SHOP) daily stock price data. The goal is to clean the dataset, engineer return and volatility features, detect unusual trading-volume days, and visualize price, volume, and return trends over time.

The analysis is implemented in Python using a Jupyter/Colab notebook and script (`Task-4.ipynb` / `Task-4.py`).

## Dataset

**File:** `shopify_stock.csv`

| Property | Value |
|---|---|
| Rows | 2,469 |
| Columns | 7 |
| Frequency | Daily |

### Columns

| Column | Description |
|---|---|
| date | Trading date (timezone-aware) |
| open | Opening price |
| high | Highest price during the day |
| low | Lowest price during the day |
| close | Closing price |
| adj_close | Adjusted closing price |
| volume | Shares traded |

## Tools & Libraries

- Python 3
- **pandas** – data loading, cleaning, and aggregation
- **numpy** – numerical operations
- **matplotlib** – data visualization
- **seaborn** – statistical visualization (return distribution)

## Project Workflow

The notebook/script follows a standard EDA + feature engineering pipeline:

1. **Import Libraries** – Load pandas, numpy, and matplotlib.
2. **Load Data** – Read `shopify_stock.csv` into a DataFrame.
3. **Initial Inspection**
   - `df.head()` – Preview the first few rows.
   - `df.shape` – Check the dimensions of the dataset.
   - `df.info()` – Check column data types and non-null counts.
   - `df.describe()` – View summary statistics for numeric columns.
4. **Data Type Conversion** – Convert `date` from string to a timezone-aware datetime object for accurate time-based operations.
5. **Data Quality Checks & Cleaning**
   - `df.isnull().sum()` – Check for missing values.
   - `df.dropna()` – Remove rows with missing values.
   - `df.drop_duplicates()` – Remove duplicate rows.
6. **Sorting** – Sort the dataset chronologically by `date`.
7. **Feature Engineering**
   - `Daily_Delta` = `close - open` — the absolute price change for the day.
   - `Daily_Return` = `((close - open) / open) * 100` — the percentage price change for the day.
8. **Volume Analysis**
   - Compute average, maximum, and minimum trading volume.
   - Flag **anomalous trading days** where volume exceeds 2× the average volume.
9. **Return Statistics** – Compute the mean, variance, and standard deviation of `Daily_Return` to characterize volatility.
10. **Visualization**
    - Line chart of closing price over time.
    - Line chart of trading volume over time.
    - Histogram of daily return distribution (30 bins).

## Key Insights

- The dataset covers daily Shopify price history with Open, High, Low, Close, Adjusted Close, and Volume figures.
- `Daily_Delta` and `Daily_Return` quantify how much the stock moved within each trading day, in absolute and percentage terms.
- Trading days with volume above 2× the average are flagged as anomalous, highlighting potential news-driven or high-volatility events.
- Mean, variance, and standard deviation of daily returns summarize the stock's overall volatility.
- The closing price and volume trend charts show the stock's trajectory and trading activity over the full time period.
- The return distribution histogram shows how daily returns are spread, revealing the frequency of large vs. typical price swings.

## Repository Structure

```
.
├── Task-4.ipynb           # Main analysis notebook
├── Task-4.py               # Script version of the analysis
├── shopify_stock.csv       # Raw dataset
└── README.md               # Project documentation
```

## How to Run

1. Clone or download this repository.
2. Ensure `shopify_stock.csv` is in the same directory as the script.
3. Install the required libraries if not already available:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
4. Run the script:
   ```bash
   python Task-4.py
   ```

## Notes

- The script calls `sns.histplot()` for the return distribution but does not import `seaborn` — add `import seaborn as sns` alongside the other imports for this cell to run.
- `plt.savefig("chart.png")` is called after `plt.show()` for the volume chart, so the saved file will be blank; move `savefig()` before `show()` to actually save the figure.
