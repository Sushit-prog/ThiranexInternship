# 🎬 Netflix Content Analysis — Data Cleaning & Visualization

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/Pandas-Data%20Cleaning-150458?style=for-the-badge&logo=pandas&logoColor=white"/>
  <img src="https://img.shields.io/badge/Seaborn-Visualization-4C72B0?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Google%20Colab-Notebook-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white"/>
  <img src="https://img.shields.io/badge/Status-Completed-brightgreen?style=for-the-badge"/>
</p>

<p align="center">
  <b>Internship Task 1 — Thiranex Skill Development & Future Tech Program (2026)</b>
</p>

---

## 📖 Overview

This project performs end-to-end data cleaning, feature engineering, and visual analysis
on the **Netflix Movies and TV Shows** dataset sourced from Kaggle.

The goal is to uncover meaningful patterns in Netflix's content library — including
growth trends, content distribution, audience ratings, genre popularity, and
regional production — through a structured data pipeline and a professional
multi-chart dashboard.

---

## 📂 Dataset

| Property | Detail |
|----------|--------|
| **Source** | [Kaggle — Netflix Movies and TV Shows](https://www.kaggle.com/datasets/shivamb/netflix-shows) |
| **Raw Shape** | 8,807 rows × 12 columns |
| **Cleaned Shape** | 8,804 rows × 17 columns |
| **Content Types** | Movies & TV Shows |
| **Time Range** | 2008 – 2021 |

---

## 🧹 Data Cleaning Pipeline

### Missing Value Treatment

| Column | Missing Count | Strategy Applied |
|--------|:---:|------------------|
| `director` | 2,634 | Filled → `'Unknown'` |
| `cast` | 825 | Filled → `'No Cast Info'` |
| `country` | 831 | Filled → Mode (most frequent country) |
| `date_added` | 10 | Filled → Mode |
| `rating` | 4 | Filled → Mode |
| `duration` | 3 | Rows dropped (negligible loss) |

### Duplicate Handling
- Scanned entire dataset for duplicate `show_id` and row-level duplicates
- **3 duplicate rows** detected and removed
- Post-cleaning dataset contains **zero duplicates**

### Feature Engineering

| New Column | Derived From | Purpose |
|------------|-------------|---------|
| `year_added` | `date_added` | Trend analysis over time |
| `month_added` | `date_added` | Seasonal pattern analysis |
| `month_name` | `date_added` | Human-readable month labels |
| `duration_value` | `duration` | Numeric duration for statistics |
| `duration_unit` | `duration` | Differentiates min vs seasons |

---

## 📊 Dashboard

> *7-panel dark-themed dashboard built with Matplotlib & Seaborn*

![Netflix Dashboard](netflix_dashboard.png)

| Panel | Chart Type | What It Shows |
|-------|-----------|---------------|
| 1 | Pie Chart | Movies vs TV Shows split |
| 2 | Horizontal Bar | Top 10 content-producing countries |
| 3 | Line Chart | Yearly content growth trend |
| 4 | Bar Chart | Content distribution by rating |
| 5 | Horizontal Bar | Top 8 genres on Netflix |
| 6 | Histogram | Movie duration distribution |
| 7 | Heatmap | Monthly content addition (2015–2021) |

---

## 🔍 Key Insights

| # | Insight | Finding |
|---|---------|---------|
| 🎬 | **Content Split** | ~69% Movies vs ~31% TV Shows — movies dominate but TV is growing |
| 🌍 | **Top Countries** | USA, India, and UK are the top 3 content-producing nations |
| 📈 | **Growth Trend** | Netflix expanded aggressively post-2015, peaking in 2019–2020 |
| 🔞 | **Audience Rating** | TV-MA is #1 — Netflix primarily targets mature audiences (17+) |
| 🎭 | **Top Genre** | International Movies leads, reflecting Netflix's global strategy |
| ⏱️ | **Movie Duration** | Average runtime ~99 min; sweet spot is 80–120 minutes |
| 📅 | **Content Timing** | Most titles added in **July** and **December** — peak viewing seasons |

---

## 🛠️ Tech Stack

| Tool | Version | Purpose |
|------|---------|---------|
| Python | 3.10 | Core language |
| Pandas | 2.x | Data loading, cleaning & manipulation |
| Matplotlib | 3.x | Base visualizations & dashboard layout |
| Seaborn | 0.x | Statistical charts & heatmaps |
| Google Colab | — | Cloud-based notebook environment |

---

## 📁 Project Structure
