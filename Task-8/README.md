# 📊 Student Performance Analysis: Educational Equity Study

An exploratory data analysis (EDA) project that examines how **parental education**, **lunch type** (a proxy for family income) and **test preparation** are related to student performance in **Math, Reading and Writing**. The project ends with an **educational equity report** and practical **policy recommendations**.
---

## 🔍 Project Overview

Test scores are often used to judge students, but scores are shaped by many things outside the classroom. This project uses a dataset of 1,000 students to ask:

- Do students from lower-income households score lower, and by how much?
- Does a parent's level of education relate to a student's results?
- Does completing a test preparation course make a visible difference?
- How closely are Math, Reading and Writing scores related to each other?

The answers are turned into recommendations that a school or education department could act on.

---

## 🎯 Objectives

| # | Objective | Output |
|---|---|---|
| 1 | Compare average scores across **parental education levels** and **lunch types** | Grouped bar charts |
| 2 | Evaluate score **spread** for students who did vs. did not complete test preparation | Box plots + mean / std / variance tables |
| 3 | Map relationships between **Math, Reading and Writing** scores | Scatter plots + correlation heatmap |
| 4 | Turn the findings into an **equity and policy report** | Report and recommendations in the notebook |

---

## 📂 Dataset

**File:** `studentperformance_preproccesed.csv`
**Size:** 1,000 students × 10 columns
**Data quality:** 0 missing values, 0 duplicate rows

### Data dictionary

| Column | Type | Description | Values |
|---|---|---|---|
| `gender` | Categorical | Student gender | female (518), male (482) |
| `race/ethnicity` | Categorical | Anonymised group label | group A to group E |
| `parental level of education` | Categorical | Highest education level of the parents | some high school, high school, some college, associate's degree, bachelor's degree, master's degree |
| `lunch` | Categorical | Lunch programme (proxy for household income) | standard (645), free/reduced (355) |
| `test preparation course` | Categorical | Whether the student completed the prep course | none (642), completed (358) |
| `math score` | Numeric | Math exam score | 0 to 100 |
| `reading score` | Numeric | Reading exam score | 0 to 100 |
| `writing score` | Numeric | Writing exam score | 0 to 100 |
| `Total Score` | Numeric | Sum of the three scores | 0 to 300 |
| `percentage` | Numeric | `Total Score / 300 × 100` | 0 to 100 |

### Overall averages

| Math | Reading | Writing | Overall % |
|---|---|---|---|
| 66.1 | 69.2 | 68.1 | 67.8 |

---

## 🗂 Project Structure

```
student-performance-analysis/
│
├── Task8_completed.ipynb                  # Main notebook: code, charts and report
├── studentperformance_preproccesed.csv    # Preprocessed dataset
└── README.md                              # Project documentation
```

---

## 🛠 Tools and Libraries

| Tool | Used for |
|---|---|
| **Python 3** | Programming language |
| **pandas** | Loading data, grouping, averaging, pivot tables |
| **NumPy** | Numerical support |
| **Matplotlib** | Bar charts and figure formatting |
| **Seaborn** | Box plots, scatter plots, heatmap |
| **Google Colab / Jupyter** | Running the notebook |

---

## 🧪 Methodology

The notebook follows five steps.

**1. Load and inspect the data**
`df.info()`, `df.shape`, `df.columns` and `.unique()` check the size, data types and categories before any analysis.

**2. Group and average**
`groupby()` and `pivot_table()` calculate average scores for each group, for example each parental education level, split by lunch type. `reindex()` puts the education levels in a logical order (lowest to highest) instead of alphabetical.

**3. Compare groups visually**
Grouped bar charts show differences in averages. Box plots show the whole distribution (median, spread and outliers), not just the average.

**4. Measure variability**
`mean()`, `std()` and `var()` by test preparation status put numbers on how spread out the scores are.

**5. Measure relationships**
Scatter plots show how pairs of subjects move together, and `corr()` with a heatmap summarises the strength of those relationships.

---

## 📈 Visualizations

| Section | Chart | What it shows |
|---|---|---|
| Grouped bars | Scores by **parental education** (Math / Reading / Writing) | How each subject changes as parental education rises |
| Grouped bars | Scores by **lunch type** | Gap between free/reduced and standard lunch |
| Grouped bars | **Parental education × lunch type** (Math, Reading, Writing, Percentage) | Whether the lunch gap remains at every education level |
| Box plots | Math, Reading, Writing by **test preparation** | Median, spread and outliers for each group |
| Scatter plots | Math vs Reading, Math vs Writing, Reading vs Writing | Direction and tightness of each relationship |
| Heatmap | Correlation matrix of the three scores | All three correlations at a glance |

**How to read a box plot:** the line inside the box is the median, the box covers the middle 50% of students, the whiskers show the normal range, and dots are unusually high or low scores. A taller box means more spread.

---

## 💡 Results and Key Insights

### 1. Lunch type shows a large gap that holds at every education level

| Lunch type | Math | Reading | Writing | Overall % |
|---|---|---|---|---|
| Standard | 70.0 | 71.7 | 70.8 | 70.8 |
| Free/reduced | 58.9 | 64.7 | 63.0 | 62.2 |
| **Gap** | **11.1** | **7.0** | **7.8** | **8.6** |

The gap is biggest in Math, and it shows up at **every** parental education level:

| Parental education | Standard lunch % | Free/reduced lunch % | Gap |
|---|---|---|---|
| Some high school | 69.2 | 57.2 | 12.0 |
| High school | 66.3 | 57.4 | 8.9 |
| Some college | 71.4 | 63.0 | 8.4 |
| Associate's degree | 71.8 | 65.4 | 6.4 |
| Bachelor's degree | 74.8 | 67.1 | 7.7 |
| Master's degree | 78.0 | 67.1 | 10.9 |

### 2. Higher parental education goes with higher scores

| Parental education | Math | Reading | Writing | Overall % |
|---|---|---|---|---|
| Some high school | 63.5 | 66.9 | 64.9 | 65.1 |
| High school | 62.1 | 64.7 | 62.4 | 63.1 |
| Some college | 67.1 | 69.5 | 68.8 | 68.5 |
| Associate's degree | 67.9 | 70.9 | 69.9 | 69.6 |
| Bachelor's degree | 69.4 | 73.0 | 73.4 | 71.9 |
| Master's degree | 69.7 | 75.4 | 75.7 | 73.6 |

The pattern is upward overall, though not perfectly: the two lowest levels are close together. The span from lowest to highest is about **10.5 points**.

### 3. Test preparation is linked to higher and slightly more consistent scores

| Subject | Completed (mean) | None (mean) | Difference | Std dev (completed) | Std dev (none) |
|---|---|---|---|---|---|
| Math | 69.7 | 64.1 | +5.6 | 14.4 | 15.2 |
| Reading | 73.9 | 66.5 | +7.4 | 13.6 | 14.5 |
| Writing | 74.4 | 64.5 | +9.9 | 13.4 | 15.0 |

- Writing improves the most; Math improves the least.
- Scores are a little less spread out for students who completed the course (lower std dev and variance).
- Only **about 36%** of students (358 of 1,000) completed the course.

### 4. Reading and Writing move almost together; Math is more independent

| Pair | Correlation |
|---|---|
| Reading and Writing | **0.95** |
| Math and Reading | 0.82 |
| Math and Writing | 0.80 |

Reading and Writing are almost the same signal. Math is strongly related to both, but a student who reads well can still struggle in Math.

---

## 🏫 Educational Equity and Policy Recommendations

| # | Recommendation | Why (from the data) | Suggested action |
|---|---|---|---|
| 1 | **Support free/reduced lunch students** | Lowest scores, gap of about 8.6 points overall and 11.1 in Math | Free tutoring and study help, starting with Math |
| 2 | **Make test preparation free and open to all** | Completers score about 7 to 8 points higher, but only 36% take the course | Offer during school hours; invite low-scoring students first |
| 3 | **Support students whose parents have less formal education** | About 10.5-point span between lowest and highest groups | Mentoring, subject and career guidance, family information sessions |
| 4 | **Assess Reading and Math separately** | Math correlates about 0.80 with Reading, so it is not fully predicted by it | Use a separate Math check to find students who need help |
| 5 | **Track gaps every year** | Gaps are easy to miss in overall averages | Report scores by lunch type, parental education and test preparation; pilot new programmes on a small group first |

---

---

⭐ If you found this project useful, consider giving it a star.
