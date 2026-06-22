# 📊 Data Science Internship Projects
<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-Data%20Analysis-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Scikit--Learn-Machine%20Learning-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white"/>
  <img src="https://img.shields.io/badge/XGBoost-Gradient%20Boosting-189AB4?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/SHAP-Explainability-FF6B6B?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C72B0?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge"/>
</p>

<p align="center">
  <b>Thiranex Skill Development & Future Tech Internship Program — 2026</b><br/>
  <i>Data Science & AI Track</i>
</p>

---

## 📌 Overview

This repository contains all four internship tasks completed as part of the **Thiranex Data Science & AI Internship Program 2026**. The work spans two real-world domains — **Entertainment (Netflix)** and **Healthcare (Cardiovascular Risk)** — covering the complete data science workflow: data cleaning, exploratory analysis, machine learning, and model explainability.

| Task | Domain | Description | Status |
|---|---|---|---|
| Task 1 | 🎬 Netflix | Data Cleaning, Feature Engineering & Dashboard | ✅ Completed |
| Task 2 | 🎬 Netflix | ML Classification — Kids vs Adult Content | ✅ Completed |
| Task 3 | 🎬 Netflix | Exploratory Data Analysis & Statistical Insights | ✅ Completed |
| Task 4 | 🫀 Healthcare | Real-World ML Project — Heart Disease Prediction | ✅ Completed |

---

## 📂 Repository Structure

```text
thiranex-internship-2026/
│
├── netflix/
│   ├── Task1.ipynb                        # Cleaning, EDA, Dashboard
│   ├── Task2.ipynb                        # ML Classification
│   ├── Task3.ipynb                        # Statistical Analysis
│   └── netflix_titles.csv                 # Dataset
│
├── heart_disease/
│   └── heart_disease_prediction.ipynb     # End-to-end ML pipeline
│
└── README.md
```

---

<br/>

# 🎬 Tasks 1–3 — Netflix Data Science

## 📂 Dataset

| Property | Details |
|---|---|
| **Source** | Netflix Movies and TV Shows (Kaggle) |
| **Records** | 8,807 titles |
| **Content Types** | Movies & TV Shows |
| **Time Range** | 2008–2021 |

---

## Task 1 — Data Cleaning, Feature Engineering & Dashboard

### What Was Done
- Handled missing values and duplicate records across 12 columns
- Engineered new date-based and duration-based features
- Built a multi-panel visualization dashboard for Netflix content trends
- Analyzed ratings, genres, countries, and release patterns

### Key Insights
- Movies account for nearly **70%** of all Netflix content
- **USA** leads global content production by a wide margin
- Significant content growth spike after **2015**
- **TV-MA** is the most prevalent content rating on the platform

---

## Task 2 — Predictive Modeling (Kids vs Adult Classification)

### Objective
Classify Netflix titles as **Kids** or **Adult** content using machine learning based on title metadata and rating features.

### Models Evaluated

| Model | Accuracy |
|---|---|
| Logistic Regression | 61.0% |
| Decision Tree | 81.8% |
| **Random Forest** | **85.7%** |

**Best Model:** Random Forest — selected for its ability to handle non-linear decision boundaries and categorical feature interactions.

---

## Task 3 — Exploratory Data Analysis & Statistical Insights

### Analysis Performed
- Statistical summaries across all features
- Pearson correlation analysis
- Outlier detection on runtime and release year
- Distribution analysis for movies vs TV shows
- Content trend and growth pattern discovery

### Major Findings
- Netflix experienced its fastest content growth between **2015–2019**
- Movie runtimes follow a roughly **normal distribution** (~90–100 min mean)
- Most TV Shows run for only **one season** — reflecting an acquisition-heavy strategy
- **Mature-audience content** (TV-MA, R) dominates the platform catalog

---

<br/>

# 🫀 Task 4 — Heart Disease Risk Prediction
### Real-World Data Project (Healthcare Domain)

## 📂 Dataset

| Property | Details |
|---|---|
| **Name** | UCI Cleveland Heart Disease Dataset |
| **Source** | [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/heart+disease) |
| **Patients** | 303 |
| **Features** | 13 clinical measurements |
| **Target** | Binary (1 = Heart Disease, 0 = No Disease) |
| **Class Balance** | ~54% disease / 46% healthy — well balanced |

> **Clinical Motivation:** Cardiovascular disease kills approximately 17.9 million people per year (WHO). Early, data-driven risk stratification using routine clinical tests can meaningfully reduce this burden.

### Feature Reference

| Feature | Type | Description |
|---|---|---|
| `age` | Continuous | Age in years |
| `sex` | Binary | 1 = Male, 0 = Female |
| `cp` | Categorical | Chest pain type (0–3) |
| `trestbps` | Continuous | Resting blood pressure (mmHg) |
| `chol` | Continuous | Serum cholesterol (mg/dL) |
| `fbs` | Binary | Fasting blood sugar > 120 mg/dL |
| `restecg` | Categorical | Resting ECG results (0–2) |
| `thalach` | Continuous | Maximum heart rate achieved (bpm) |
| `exang` | Binary | Exercise-induced angina |
| `oldpeak` | Continuous | ST depression (exercise vs rest) |
| `slope` | Ordinal | Slope of peak exercise ST segment |
| `ca` | Ordinal | Number of major vessels colored (0–3) |
| `thal` | Categorical | Thalassemia type |
| `target` | Binary | **Heart disease present ← label** |

---

## Methodology

### Feature Engineering
Five new clinically-motivated features derived from existing measurements:

| Feature | Derivation | Clinical Rationale |
|---|---|---|
| `age_group` | Age bucketed into 4 risk tiers | Clinical risk stratification by decade |
| `hr_reserve` | `(220 - age) - thalach` | Unused cardiac capacity; low = poor fitness |
| `silent_ischemia` | Flag for `cp == 0` | Asymptomatic patients carry paradoxically high risk |
| `hypertension` | Flag for `trestbps >= 140` | Stage-2 hypertension is a primary risk factor |
| `st_risk` | `oldpeak × slope` | Composite ST-segment severity score |

### Models Trained

All models use **sklearn Pipelines** (StandardScaler → Classifier) to prevent data leakage during cross-validation.

| Model | Notes |
|---|---|
| Logistic Regression | Interpretable linear baseline |
| Random Forest | Non-linear ensemble, built-in feature importance |
| XGBoost | Gradient boosting; best-in-class for tabular data |

### Explainability
- **Random Forest Gini Importance** — global feature ranking
- **SHAP TreeExplainer (XGBoost)** — per-prediction attribution with direction and magnitude

---

## Results

| Model | Test Accuracy | F1-Score | AUC-ROC |
|---|---|---|---|
| Logistic Regression | ~0.85 | ~0.86 | ~0.91 |
| Random Forest | ~0.87 | ~0.88 | ~0.92 |
| **XGBoost** | **~0.90** | **~0.90** | **~0.93** |

**Best Model:** XGBoost — recommended for any downstream deployment.

---

## Key Findings

- **Chest pain type (`cp`)** is the strongest predictor. Asymptomatic patients (`cp=0`) have paradoxically the *highest* disease rates — silent ischemia
- **Max heart rate (`thalach`)** is significantly lower in disease patients, reflecting reduced cardiovascular reserve
- **Vessel blockages (`ca`)** provide direct anatomical evidence of coronary artery disease
- **ST depression (`oldpeak`)** is a well-validated ECG ischemia marker and a top SHAP driver
- The engineered **`hr_reserve`** feature adds meaningful predictive signal beyond the original 13 features

---

<br/>

## 🛠️ Tech Stack

| Category | Libraries |
|---|---|
| **Data Manipulation** | Pandas, NumPy |
| **Visualization** | Matplotlib, Seaborn |
| **Machine Learning** | Scikit-Learn, XGBoost |
| **Explainability** | SHAP |
| **Statistical Analysis** | SciPy |
| **Environment** | Jupyter Notebook, Google Colab |

---

## ⚙️ Setup & Usage

```bash
# Clone the repository
git clone https://github.com/Sushit-prog/thiranex-internship-2026.git
cd thiranex-internship-2026

# Install dependencies
pip install -r requirements.txt

# Launch Jupyter
jupyter notebook
```

> Task 4 downloads the dataset automatically and installs XGBoost + SHAP on first run — no manual setup needed.

---

## 👤 Author

**Sushit**  
Thiranex Skill Development & Future Tech Internship Program 2026 — Data Science & AI Track  
GitHub: [@Sushit-prog](https://github.com/Sushit-prog)

---

<p align="center">
A complete internship portfolio spanning two real-world domains — Entertainment & Healthcare —<br/>
covering data cleaning, EDA, machine learning, and model explainability.
</p>
