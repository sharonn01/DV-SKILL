# Superstore Sales — Exploratory Data Analysis (EDA)

## Overview

This project performs an end-to-end exploratory data analysis (EDA) on the **Sample Superstore** dataset — a classic retail dataset containing order-level records of sales, profit, discounts, shipping, categories, and regions.

The goal is to understand the business through data: which product categories perform best, how profit is distributed, whether discounts help or hurt profitability, and how key numeric metrics relate to each other. This is done using Python's data analysis and visualization stack: `pandas`, `numpy`, `matplotlib`, and `seaborn`.

This README explains the project from setup to output, and walks through what every section of the notebook (`Task2_BDA.ipynb`) does and why.

---

## Table of Contents

1. [Project Goals](#project-goals)
2. [Dataset Description](#dataset-description)
3. [Requirements & Setup](#requirements--setup)
4. [How to Run the Notebook](#how-to-run-the-notebook)
5. [Detailed Walkthrough of Each Step](#detailed-walkthrough-of-each-step)
6. [Analysis Parts Explained](#analysis-parts-explained)
7. [Key Business Questions Answered](#key-business-questions-answered)
8. [Understanding the Visualizations](#understanding-the-visualizations)
9. [Output](#output)
10. [Possible Extensions](#possible-extensions)

---

## Project Goals

- Load and clean a real-world-style retail dataset
- Engineer a useful derived feature (delivery time)
- Explore sales and profit trends across product categories
- Visually detect outliers and variation in profitability
- Investigate the relationship between discounts and profit
- Quantify relationships between numeric variables using correlation analysis

---

## Dataset Description

**File:** `samplesuperstore - samplesuperstore.csv`

This is the well-known "Sample Superstore" retail dataset. Typical columns include:

| Column | Description |
|---|---|
| `Order Date` | Date the order was placed |
| `Ship Date` | Date the order was shipped |
| `Category` | Product category (e.g., Furniture, Office Supplies, Technology) |
| `Sub-Category` | More specific product grouping |
| `Product Name` | Name of the product ordered |
| `Sales` | Revenue generated from the order |
| `Profit` | Profit earned (can be negative — a loss) |
| `Discount` | Discount applied to the order (as a fraction, e.g., 0.2 = 20%) |
| `Region` / `State` / `City` | Geographic info about the order |
| `Quantity` | Number of units ordered |

The notebook adds one derived column:
- **`Delivery Days`** = `Ship Date` − `Order Date` (in days), representing how long delivery took.

---

## Requirements & Setup

### Python Version
Python 3.x

### Libraries Used
```bash
pip install pandas numpy matplotlib seaborn
```

| Library | Purpose |
|---|---|
| `pandas` | Loading, cleaning, and manipulating tabular data |
| `numpy` | Numerical operations (used indirectly via pandas) |
| `matplotlib` | Base plotting engine, used for titles/labels/figure sizing |
| `seaborn` | High-level statistical visualizations (bar plots, box plots, scatter plots, heatmaps) |

### Environment
The notebook was built for **Google Colab** and includes a Google Drive mount step to access the CSV file stored in Drive. If you're running it **locally in Jupyter** instead:
- Skip the `drive.mount()` cell entirely.
- Change the file path in `pd.read_csv(...)` to wherever your CSV lives locally, e.g.:
  ```python
  df = pd.read_csv("samplesuperstore.csv")
  ```

---

## How to Run the Notebook

1. **Open the notebook** — either in Google Colab or a local Jupyter environment (JupyterLab / VS Code / Anaconda).
2. **Set up the data source:**
   - *Colab:* Run the drive-mount cell, authorize access, then make sure the CSV path matches where the file is stored in your Drive.
   - *Local:* Skip the mount cell and set the CSV path to your local file.
3. **Run all cells sequentially**, top to bottom (`Runtime > Run all` in Colab, or `Run > Run All Cells` in Jupyter). The notebook is linear — each step builds on the previous one, so skipping cells may cause errors (e.g., plotting before dates are converted).
4. **Review the output plots** as they render inline below each code cell.

---

## Detailed Walkthrough of Each Step

### Step 1 — Import Libraries
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```
Brings in the four core libraries needed for data handling and visualization.

### Step 2 — Mount Google Drive (Colab only)
```python
from google.colab import drive
drive.mount('/content/drive')
```
Gives the notebook access to files stored in your Google Drive so the CSV can be read.

### Step 3 — Load the Dataset
```python
df = pd.read_csv("/content/samplesuperstore - samplesuperstore.csv")
```
Reads the CSV into a pandas DataFrame called `df`, the central object used throughout the notebook.

### Step 4 — Initial Inspection
```python
df.head()      # first 5 rows — sanity check on structure
df.info()      # column names, data types, non-null counts
df.describe()  # summary statistics (mean, std, min, max, quartiles) for numeric columns
```
This is standard first-look practice: confirm the data loaded correctly, check for obvious issues, and understand the scale of each numeric column.

### Step 5 — Convert Dates
```python
df['Order Date'] = pd.to_datetime(df['Order Date'])
df['Ship Date'] = pd.to_datetime(df['Ship Date'])
```
By default, dates are read as plain text (strings). Converting them to proper `datetime` objects allows date arithmetic — which is needed for the next step.

### Step 6 — Re-check Data Types
```python
df.info()
```
Confirms the two date columns are now `datetime64` type instead of `object` (string).

### Step 7 — Engineer a New Feature: Delivery Days
```python
df['Delivery Days'] = (df['Ship Date'] - df['Order Date']).dt.days
```
Calculates how many days elapsed between order and shipment — a useful operational metric not present in the raw data.

### Step 8 — Explore Categories & Check for Missing Data
```python
df['Category'].unique()   # list all distinct product categories
df.isnull().sum()         # count missing values per column
```
Confirms what categories exist in the data and whether any cleaning (e.g., handling nulls) is needed before analysis.

### Step 9 — Aggregate Sales by Category
```python
category_sales = df.groupby('Category')['Sales'].sum()
```
Groups all rows by `Category` and sums the `Sales` column — giving total revenue per category.

### Step 10 — Bar Chart of Sales by Category
```python
category_sales.plot(kind='bar', figsize=(8,5))
plt.title("Sales by Category")
plt.ylabel("Total Sales")
plt.show()
```
Visualizes which category brings in the most total revenue.

### Step 11 — Sales Distribution Histogram
```python
sns.histplot(df['Sales'], bins=30)
plt.title("Sales Distribution")
plt.show()
```
Shows how individual order sales values are spread out — typically revealing that most orders are small, with a long tail of large ones.

---

## Analysis Parts Explained

The notebook is organized into four labeled analytical "parts," each answering a specific business question.

### Part 1: Bar Plots — Category Comparison
**Purpose:** Compare sales and profit across categories to see which performs best.

```python
sns.barplot(data=df, x="Category", y="Profit")
sns.barplot(data=df, x="Category", y="Sales")
```
**Question answered:** *Which category generates the maximum profit?*
Bar plots here show the **average** value per category (seaborn's default aggregation is the mean), letting you compare Furniture, Office Supplies, and Technology side by side for both sales and profit.

### Part 2: Box Plots — Distribution & Outliers
**Purpose:** Box plots reveal more than a single average — they show the full spread of the data.

```python
sns.boxplot(data=df, y="Profit")
sns.boxplot(data=df, x="Category", y="Profit")
```
A box plot displays:
- **Median** (the line inside the box)
- **Interquartile range** (the box itself — middle 50% of the data)
- **Variation/spread** (the whiskers)
- **Outliers** (individual points beyond the whiskers)

**Why it matters:** A category might have a good *average* profit but still contain many loss-making orders (negative profit outliers) — box plots expose that nuance in a way a bar chart cannot.

### Part 3: Discount vs. Profit — Scatter Plot
**Purpose:** Determine whether discounting helps or hurts profitability.

```python
df["Discount"].unique()
sns.scatterplot(data=df, x="Discount", y="Profit")
```
**Question answered:** *At what discount level does profit start decreasing?*
Each point represents one order — plotting Discount against Profit typically reveals a threshold beyond which profit turns negative, which is valuable for setting discount policy.

### Part 4: Correlation Heatmap
**Purpose:** Quantify relationships between all numeric variables at once.

```python
numeric_df = df.select_dtypes(include="number")
corr = numeric_df.corr()
sns.heatmap(corr, annot=True)
plt.title("Correlation Heatmap")
plt.show()
```
**What correlation means:** A value close to **+1** means two variables move together (e.g., Sales up → Profit up). A value close to **−1** means they move in opposite directions (e.g., Discount up → Profit down). A value near **0** means little to no linear relationship.

The heatmap gives a compact, color-coded summary of how `Sales`, `Profit`, `Discount`, `Quantity`, and `Delivery Days` relate to one another — with the actual correlation numbers annotated on each cell.

---

## Key Business Questions Answered

| Question | Answered By |
|---|---|
| Which category generates the most sales? | Category sales bar chart (Step 10) |
| Which category generates the most profit? | Part 1 bar plot |
| How consistent is profit within each category? | Part 2 box plots |
| Are there loss-making outlier orders? | Part 2 box plots |
| Does discounting hurt profit, and at what point? | Part 3 scatter plot |
| How strongly are Sales, Profit, and Discount related? | Part 4 correlation heatmap |
| How long does delivery typically take? | `Delivery Days` feature (Step 7) |

---

## Understanding the Visualizations

- **Bar plots** — good for comparing a single aggregated metric (e.g., mean/sum) across categories.
- **Histograms** — good for seeing the overall shape/spread of one numeric variable.
- **Box plots** — good for comparing distributions, spotting outliers, and understanding variability, not just averages.
- **Scatter plots** — good for spotting relationships or patterns between two continuous variables.
- **Heatmaps** — good for summarizing many pairwise relationships at a glance.

---

## Output

All visualizations render **inline within the notebook** — no image files or reports are saved to disk by default. If you want to save any chart, add this after a plotting cell, before `plt.show()`:
```python
plt.savefig("chart_name.png", dpi=300, bbox_inches="tight")
```

---

## Possible Extensions

- Segment the discount-vs-profit analysis by category (some categories may tolerate discounts better than others)
- Analyze profit and delivery days by `Region` or `State`
- Build a simple regression model to predict `Profit` from `Sales`, `Discount`, and `Quantity`
- Add a time-series view of sales/profit trends by month or quarter using `Order Date`
- Export cleaned data and summary tables to CSV for use in a dashboard (e.g., Tableau, Power BI)
