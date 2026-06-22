# 🫀 Heart Disease Risk Prediction
### End-to-End Data Science Pipeline — Healthcare Domain

![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=flat&logo=jupyter&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.x-F7931E?style=flat&logo=scikitlearn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-Gradient%20Boosting-189AB4?style=flat)
![SHAP](https://img.shields.io/badge/SHAP-Explainability-FF6B6B?style=flat)
![License](https://img.shields.io/badge/License-MIT-green?style=flat)

---

## 📌 Overview

This project builds a full machine learning pipeline to predict the presence of **heart disease** in patients using 13 routine clinical measurements. It covers the complete data science workflow — from raw data ingestion and exploratory analysis to model training, evaluation, and explainability — applied to one of the most studied clinical datasets in ML research.

> **Clinical Motivation:** Cardiovascular disease is the #1 cause of death globally (~17.9 million deaths/year, WHO). Early risk stratification using routine lab and ECG data can meaningfully reduce this burden by enabling targeted intervention before symptoms escalate.

---

## 📂 Project Structure

```
heart-disease-prediction/
│
├── heart_disease_prediction.ipynb   # Main notebook (run this)
├── README.md                        # Project documentation
└── requirements.txt                 # Python dependencies
```

---

## 📊 Dataset

| Property | Details |
|---|---|
| **Name** | UCI Cleveland Heart Disease Dataset |
| **Source** | [UCI Machine Learning Repository](https://archive.ics.uci.edu/ml/datasets/heart+disease) |
| **Patients** | 303 |
| **Features** | 13 clinical measurements |
| **Target** | Binary (1 = Heart Disease, 0 = No Disease) |
| **Class Balance** | ~54% disease / 46% healthy — well balanced |

### Feature Description

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
| `ca` | Ordinal | Number of major vessels (0–3) |
| `thal` | Categorical | Thalassemia type |
| `target` | Binary | **Heart disease present ← label** |

---

## 🔬 Methodology

### 1. Exploratory Data Analysis
- Target class distribution and balance check
- Distribution plots of all continuous features, split by disease status
- Categorical feature disease-rate analysis
- Pearson correlation heatmap and target-correlation ranking
- Clinical scatter plot: Age vs Max Heart Rate

### 2. Feature Engineering
Five new clinically-motivated features are derived:

| Feature | Derivation | Rationale |
|---|---|---|
| `age_group` | Age bucketed into 4 risk tiers | Clinical protocols stratify risk by decade |
| `hr_reserve` | `(220 - age) - thalach` | Unused cardiac capacity; low reserve = poor fitness |
| `silent_ischemia` | Flag for `cp == 0` | Asymptomatic presentation is paradoxically highest risk |
| `hypertension` | Flag for `trestbps >= 140` | Stage-2 hypertension is a primary cardiovascular risk factor |
| `st_risk` | `oldpeak × slope` | Composite ST-segment severity score |

### 3. Models Trained

All models are wrapped in **sklearn Pipelines** (StandardScaler → Classifier) to prevent data leakage during cross-validation.

| Model | Notes |
|---|---|
| Logistic Regression | Interpretable linear baseline |
| Random Forest | Non-linear ensemble, robust to outliers |
| XGBoost | Gradient boosting; state-of-the-art for tabular data |

### 4. Evaluation
- 5-Fold Stratified Cross-Validation (AUC-ROC)
- Test set: Accuracy, F1-Score, AUC-ROC
- ROC curves (all models overlaid)
- Confusion matrices
- Per-class classification report

### 5. Explainability
- **Random Forest Gini importance** — global feature ranking
- **SHAP TreeExplainer (XGBoost)** — beeswarm summary plot + mean impact bar chart

---

## 🏆 Results

> Exact values depend on your environment. Typical results on this dataset:

| Model | Test Accuracy | F1-Score | AUC-ROC |
|---|---|---|---|
| Logistic Regression | ~0.85 | ~0.86 | ~0.91 |
| Random Forest | ~0.87 | ~0.88 | ~0.92 |
| **XGBoost** | **~0.90** | **~0.90** | **~0.93** |

XGBoost consistently achieves the highest AUC-ROC and is the recommended model.

---

## 🔍 Key Findings

- **Chest pain type (`cp`)** is the strongest predictor. Asymptomatic patients (`cp=0`) show paradoxically high disease rates — a phenomenon known as *silent ischemia*.
- **Max heart rate (`thalach`)** is significantly lower in disease patients, reflecting reduced cardiovascular reserve.
- **Number of blocked vessels (`ca`)** provides direct anatomical evidence of coronary artery disease.
- **ST depression (`oldpeak`)** is a well-validated ECG ischemia marker and a top SHAP driver.
- The engineered **`hr_reserve`** feature adds meaningful predictive signal beyond the original 13 features.

---

## ⚙️ Setup & Usage

### Requirements
```
numpy
pandas
matplotlib
seaborn
scikit-learn
xgboost
shap
jupyter
```

Install all dependencies:
```bash
pip install -r requirements.txt
```

### Run the Notebook
```bash
git clone https://github.com/Sushit-prog/heart-disease-prediction.git
cd heart-disease-prediction
jupyter notebook heart_disease_prediction.ipynb
```

> The notebook downloads the dataset automatically from a public URL — no manual download needed. XGBoost and SHAP are also installed automatically on first run if not present.

---

## 🚀 Potential Extensions

- Hyperparameter optimization with **Optuna** (Bayesian search)
- Ensemble stacking with a Logistic Regression meta-learner
- Probability calibration (Platt scaling) for clinical risk thresholds
- SMOTE oversampling for larger, imbalanced production datasets
- REST API deployment via **FastAPI + Docker**
- Production drift monitoring with **Evidently AI**

---

## ⚠️ Limitations

- Small dataset (303 patients) — real clinical deployment requires 10,000+ records
- Single-centre bias (Cleveland Clinic) — may not generalize across demographics
- Cross-sectional data only — no longitudinal follow-up
- Missing confounders (BMI, smoking history, family history, medications)

---

## 📚 References

- Detrano, R. et al. (1989). *International application of a new probability algorithm for the diagnosis of coronary artery disease.* American Journal of Cardiology.
- UCI ML Repository: [Heart Disease Dataset](https://archive.ics.uci.edu/ml/datasets/heart+disease)
- Lundberg, S. M., & Lee, S. I. (2017). *A Unified Approach to Interpreting Model Predictions.* NeurIPS.
- WHO Cardiovascular Disease Fact Sheet (2023): [who.int](https://www.who.int/news-room/fact-sheets/detail/cardiovascular-diseases-(cvds))

---

## 📄 License

This project is licensed under the MIT License.

---

<p align="center">Built as part of a Data Science internship project | Domain: Healthcare</p>
