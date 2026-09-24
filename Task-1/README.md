# Sample Superstore – Sales Data Analysis

**Author:** Sharon N — 2 BCA, Batch 1
**Course:** Big Data Analytics (BDA)
**Assignment:** Task 1

## Overview

This project performs exploratory data analysis (EDA) on the **Sample Superstore** dataset, a retail sales dataset containing order-level transaction records. The goal is to clean the data, engineer a useful new feature, and uncover initial insights into sales performance across product categories.

The analysis is implemented in Python using a Jupyter/Colab notebook (`Task_1_BDA.ipynb`).

## Dataset

**File:** `samplesuperstore.csv`

| Property | Value |
|---|---|
| Rows | 10,194 |
| Columns | 21 |
| Missing values | None |

### Columns

| Column | Description |
|---|---|
| Row ID | Unique row identifier |
| Order ID | Unique order identifier |
| Order Date | Date the order was placed |
| Ship Date | Date the order was shipped |
| Ship Mode | Shipping method used |
| Customer ID / Customer Name | Customer identifiers |
| Segment | Customer segment (e.g., Consumer, Corporate, Home Office) |
| Country/Region, City, State/Province, Postal Code, Region | Geographic details |
| Product ID | Unique product identifier |
| Category | Top-level product category (Office Supplies, Furniture, Technology) |
| Sub-Category | Product sub-category |
| Product Name | Name of the product |
| Sales | Sale amount ($) |
| Quantity | Units sold |
| Discount | Discount applied |
| Profit | Profit ($) |

## Tools & Libraries

- **Python 3**
- **pandas** – data loading, cleaning, and aggregation
- **numpy** – numerical operations
- **matplotlib** – data visualization
- **seaborn** – statistical visualization

## Project Workflow

The notebook follows a standard EDA pipeline:

1. **Import Libraries** – Load `pandas`, `numpy`, `matplotlib`, and `seaborn`.
2. **Load Data** – Read `samplesuperstore.csv` into a DataFrame.
3. **Initial Inspection**
   - `df.head()` – Preview the first few rows.
   - `df.info()` – Check column data types and non-null counts.
   - `df.describe()` – View summary statistics for numeric columns.
4. **Data Type Conversion** – Convert `Order Date` and `Ship Date` from strings to proper `datetime` objects for accurate date-based calculations.
5. **Feature Engineering** – Create a new column, **`Delivery Days`**, calculated as the difference (in days) between `Ship Date` and `Order Date`. This measures how long each order took to ship.
6. **Data Quality Checks**
   - `df['Category'].unique()` – List the distinct product categories.
   - `df.isnull().sum()` – Confirm there are no missing values in any column.
7. **Aggregation** – Group the data by `Category` and sum `Sales` to find total sales per category.
8. **Visualization**
   - A **bar chart** of total sales by category.
   - A **histogram** showing the distribution of the `Sales` column across 30 bins.

## Key Insights

- The dataset is clean, with **zero missing values** across all 21 columns.
- Products fall into three categories: **Office Supplies**, **Furniture**, and **Technology**.
- A new **Delivery Days** metric was engineered to enable future analysis of shipping performance.
- Total sales vary noticeably by category, visualized via a bar chart.
- The overall sales distribution is right-skewed, with most orders falling in the lower sales range and a smaller number of high-value orders — visualized via a histogram.

## Repository Structure

```

├── Task_1_BDA.ipynb           # Main analysis notebook
├── samplesuperstore.csv       # Raw dataset
└── README.md                  # Project documentation
```

## How to Run

1. Clone or download this repository.
2. Ensure `samplesuperstore.csv` is in the same directory as the notebook (or update the file path in the notebook to match its location, e.g. `/content/samplesuperstore.csv` for Google Colab).
3. Install the required libraries if not already available:
   ```bash
   pip install pandas numpy matplotlib seaborn
   ```
4. Open `Task
