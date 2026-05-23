# 🎬 Netflix Data Science Project — Full Analysis Suite

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C72B0?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Google%20Colab-Notebooks-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white"/>
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge"/>
</p>

<p align="center">
  <b>Thiranex Skill Development & Future Tech Internship Program — 2026</b><br/>
  Three end-to-end Data Science tasks on the Netflix Movies & TV Shows dataset
</p>

---

## 📌 Project Overview

This repository contains three complete Data Science projects built on the
**Netflix Movies and TV Shows** dataset (Kaggle, 8,807 titles). Each task
progressively deepens the analysis — from raw data cleaning to machine learning
classification — demonstrating a full data science workflow on a single,
real-world dataset.

| Task | Title | Type | Status |
|------|-------|------|--------|
| 01 | Data Cleaning & Visualization | Data Engineering + Dashboarding | ✅ Completed |
| 02 | Predictive Modeling | Machine Learning Classification | ✅ Completed |
| 03 | Exploratory Data Analysis | Statistical Analysis + Reporting | ✅ Completed |

---

## 📂 Dataset

| Property | Detail |
|----------|--------|
| **Source** | [Kaggle — Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) |
| **Raw Shape** | 8,807 rows × 12 columns |
| **Cleaned Shape** | 8,804 rows × 17 columns |
| **Content Types** | Movies & TV Shows |
| **Time Range** | 2008 – 2021 |
| **Coverage** | 748 countries, 42 genres, 4,528 directors |

netflix-data-science/
│
├── 📓 Task1.ipynb                  # Data Cleaning & Dashboard
├── 📓 Task2.ipynb                  # Predictive Modeling (ML)
├── 📓 Task3.ipynb                  # EDA & Statistical Analysis
│
├── 📊 netflix_dashboard.png        # Task 1 — 7-panel dashboard
├── 📊 task2_model_dashboard.png    # Task 2 — Model evaluation dashboard
├── 📊 eda_correlation_heatmap.png  # Task 3 — Correlation heatmap
├── 📊 eda_outlier_boxplots.png     # Task 3 — Outlier boxplots
├── 📊 eda_distributions.png        # Task 3 — Distribution charts
├── 📊 eda_patterns.png             # Task 3 — Deep pattern analysis
│
├── 📄 netflix_titles.csv           # Raw dataset
└── 📝 README.md                    # This file

---

## 📋 Task 1 — Data Cleaning & Visualization

### Objective
Clean a raw Netflix dataset, handle all data quality issues, engineer
new features, and present findings through a professional dark-themed dashboard.

### Data Cleaning Pipeline

| Column | Issue | Strategy |
|--------|-------|----------|
| `director` | 2,634 missing | Filled → `'Unknown'` |
| `cast` | 825 missing | Filled → `'No Cast Info'` |
| `country` | 831 missing | Filled → Mode |
| `date_added` | 10 missing | Filled → Mode |
| `rating` | 4 missing | Filled → Mode |
| `duration` | 3 missing | Rows dropped |
| Duplicates | 3 found | Removed |

### Feature Engineering

| New Feature | Source | Purpose |
|-------------|--------|---------|
| `year_added` | `date_added` | Trend analysis |
| `month_added` | `date_added` | Seasonal patterns |
| `month_name` | `date_added` | Human-readable labels |
| `duration_value` | `duration` | Numeric duration |
| `duration_unit` | `duration` | min vs seasons |

### Dashboard

![Netflix Dashboard](netflix_dashboard.png)

| Panel | Chart | Insight |
|-------|-------|---------|
| 1 | Pie Chart | 69.6% Movies vs 30.4% TV Shows |
| 2 | Bar Chart | USA leads content production |
| 3 | Line Chart | Explosive growth post-2015 |
| 4 | Bar Chart | TV-MA is most common rating |
| 5 | Bar Chart | International Movies is #1 genre |
| 6 | Histogram | Movies average 99 min runtime |
| 7 | Heatmap | July & December peak content drops |

---

## 🤖 Task 2 — Predictive Modeling (ML Classification)

### Objective
Build and evaluate multiple machine learning models to classify Netflix
titles as **Kids** or **Adult** content based on content features —
a real-world content moderation problem.

### Target Variable
Kids  (0) → Ratings: TV-Y, TV-Y7, TV-Y7-FV, G, PG, TV-G, TV-PG
Adult (1) → Ratings: TV-MA, TV-14, R, NR, NC-17, UR
### Class Distribution
| Class | Count | Percentage |
|-------|-------|------------|
| Adult | 6,746 | 76.6% |
| Kids | 2,058 | 23.4% |

> **Note:** Class imbalance handled using `class_weight='balanced'`
> across all models.

### Feature Set
```python
features = [
    'type_encoded',    # Movie or TV Show
    'country_encoded', # Top 10 countries + Other
    'genre_encoded',   # Top 15 genres + Other
    'year_added',      # Year content was added
    'month_added',     # Month content was added
    'duration_value',  # Runtime in minutes or seasons
    'release_year'     # Original release year
]
```

### Model Results

| Model | Accuracy | Kids F1 | Adult F1 |
|-------|:--------:|:-------:|:--------:|
| Logistic Regression | 61.04% | 0.46 | 0.69 |
| Decision Tree | 81.83% | 0.64 | 0.88 |
| **Random Forest** ✅ | **85.69%** | **0.66** | **0.91** |

### Model Evaluation Dashboard

![Model Dashboard](task2_model_dashboard.png)

### Key Takeaways
- **Logistic Regression** struggled due to non-linear decision boundaries
- **Decision Tree** captured genre and country-based rules effectively
- **Random Forest** won with 86% accuracy — ensemble voting reduced overfitting
- Kids F1 of **0.66** on a heavily imbalanced minority class is strong

---

## 📊 Task 3 — Exploratory Data Analysis (EDA)

### Objective
Perform deep statistical analysis to uncover hidden patterns, correlations,
and influencing factors across the Netflix dataset — going beyond charts
into quantitative insights.

### Analysis Phases

| Phase | Method | Tool |
|-------|--------|------|
| Statistical Summaries | Mean, Median, Std, Skewness, Kurtosis | Pandas + SciPy |
| Correlation Analysis | Pearson correlation matrix + heatmap | Seaborn |
| Outlier Detection | IQR method + Boxplots | Matplotlib |
| Distribution Analysis | KDE plots + histograms | Seaborn |
| Pattern Mining | Director, country, genre, growth trends | Pandas + Matplotlib |

### Statistical Findings

| Metric | Movies | TV Shows |
|--------|--------|----------|
| Mean Duration | 100 min | 1.8 seasons |
| Median Duration | 98 min | 1 season |
| Std Deviation | 28 min | 1.6 seasons |
| Skewness | 0.203 ✅ Normal | 3.419 ⚠️ Right-skewed |
| Kurtosis | 2.294 | 16.134 ⚠️ Heavy tails |

### Correlation Matrix Highlights

| Feature Pair | Correlation | Interpretation |
|-------------|:-----------:|----------------|
| `type` ↔ `duration_value` | **0.885** | Movies & TV Shows occupy completely separate duration spaces |
| `release_year` ↔ `duration` | **-0.249** | Newer content trends shorter |
| `release_year` ↔ `type` | **-0.182** | Older Netflix titles lean toward Movies |
| All other pairs | < 0.15 | Negligible relationships |

### Outlier Analysis

| Column | Outliers | % | Explanation |
|--------|:--------:|:---:|-------------|
| `duration_value` | 2 | 0.02% | Negligible — data is clean |
| `release_year` | 719 | 8.17% | Classic films pre-2004 added to library |
| `year_added` | 56 | 0.64% | Early Netflix titles before 2015 |

### EDA Visualizations

![Correlation Heatmap](eda_correlation_heatmap.png)
![Distributions](eda_distributions.png)
![Patterns](eda_patterns.png)
![Outliers](eda_outlier_boxplots.png)

### Key Conclusions

1. **Growth Explosion** — Netflix grew 94,350% from 2010 to 2019, peaking
   at 2,016 titles added in a single year, driven by international expansion.

2. **Mature Audience Focus** — TV-MA dominates ratings; Kids content
   represents only 23.4% of the entire library.

3. **Movie Distribution is Healthy** — Skewness of 0.203 confirms movies
   follow a near-normal runtime distribution centered around 99 minutes.

4. **TV Shows Are Heavily Skewed** — Skewness of 3.419 and kurtosis of
   16.134 reveal most shows run for just 1 season, with very few
   long-running outliers pulling the distribution right.

5. **Legacy Content Strategy** — 8.17% of titles are classic pre-2004
   films, confirming Netflix deliberately blends new originals with
   timeless catalog content.

6. **Top Creator** — Rajiv Chilaka leads with 19 titles, primarily
   children's animation — a niche but consistent production pipeline.

---

## 🔍 Overall Project Insights

> Across all three tasks, three themes consistently emerge:

**1. Netflix is a Movie-First Platform shifting toward TV**
The 70/30 Movie-to-Show ratio is narrowing year over year,
with TV Show additions growing faster post-2018.

**2. International Content is the Growth Engine**
International Movies is the #1 genre. USA, India, and UK lead
production — but 748 countries contribute content globally.

**3. Data Quality was High but Strategic**
Missing directors (30%) reflect real-world data — many titles
are stand-up specials or documentaries with no traditional director.
The data wasn't messy by accident; it reflects Netflix's diverse
content formats.

---

## 🛠️ Tech Stack

| Tool | Version | Purpose |
|------|---------|---------|
| Python | 3.10 | Core language |
| Pandas | 2.x | Data manipulation & cleaning |
| NumPy | 1.x | Numerical operations |
| Matplotlib | 3.x | Visualizations & dashboards |
| Seaborn | 0.x | Statistical charts & heatmaps |
| Scikit-learn | 1.x | ML models & evaluation metrics |
| SciPy | 1.x | Statistical analysis |
| Google Colab | — | Cloud notebook environment |

---

## 🚀 How to Run

1. Clone this repository
```bash
git clone https://github.com/yourusername/netflix-data-science.git
cd netflix-data-science
```

2. Install dependencies
```bash
pip install pandas numpy matplotlib seaborn scikit-learn scipy
```

3. Download the dataset from
[Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)
and place `netflix_titles.csv` in the root folder

4. Open notebooks in order
Task1.ipynb → Task2.ipynb → Task3.ipynb
5. Run all cells (`Runtime → Run All` in Google Colab)

---

## 👤 Author

**Sushit**
Thiranex Internship Program 2026 — Data Science & AI Track

<p>
  <a href="https://github.com/yourusername">
    <img src="https://img.shields.io/badge/GitHub-Profile-181717?style=flat-square&logo=github"/>
  </a>
  <a href="https://linkedin.com/in/yourprofile">
    <img src="https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=flat-square&logo=linkedin"/>
  </a>
</p>

---

<p align="center">
  Built with 🔴 and lots of data — Thiranex Internship 2026
</p>
---
