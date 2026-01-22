# 30-Day Readmission Risk Dashboard (Diabetes Dataset)

## 📊 Overview

This project analyzes inpatient encounter data from the UCI **Diabetes 130-US hospitals (1999–2008)** dataset to identify patterns associated with **30-day readmissions** and build a baseline machine learning model that generates **readmission risk scores**.

It includes:
- **Dashboard-style EDA** (readmission rates by key segments)
- A **baseline Logistic Regression model** (risk scoring)
- An operational **Top 10% “high-risk queue”** for follow-up prioritization
- A cleaned dataset + scored outputs used for a Streamlit dashboard

---

## 🎯 Objective

- Explore readmission patterns across key patient segments (age, length of stay, medication burden, demographics)
- Train a baseline model to predict **readmission within 30 days** (`readmit_30`)
- Convert model outputs into an actionable workflow:
  - **Flag the Top 10% highest predicted risk** encounters as high risk (`high_risk_top10`)
- Build a Streamlit dashboard for trend monitoring and risk queue review

---

## 🗂️ Contents

- `/notebooks/`
  - `01_readmission_analysis.ipynb` — end-to-end analysis (cleaning → EDA → ML → risk queue)
- `/outputs/`
  - `scored_sample.csv` — small sample dataset for GitHub/demo use  
  *(Full scored dataset is generated locally and not stored in the repo.)*
- `/app/`
  - `app.py` — Streamlit dashboard (Overview + Risk Queue + Model View)

---

## 🧼 Data Preparation (High-Level)

Key steps in the notebook:
- Converted UCI missing markers (`"?"`) → `NaN`
- Created binary target:
  - `readmit_30 = 1` if `readmitted == "<30"`
  - else `0`
- Dropped non-informative ID columns:
  - `encounter_id`, `patient_nbr`
- Dropped high-missing columns for a simpler MVP:
  - `weight`, `medical_specialty`, `payer_code`
- Created dashboard-friendly bins:
  - `num_meds_bin` (medication count bins)
  - `time_bin` (length-of-stay bins)

---

## 📈 Exploratory Insights (Dashboard-Style)

Readmission rates were explored across:
- **Age buckets**
- **Time in hospital** (including binned trend)
- **Number of medications** (including binned trend)
- **Gender** (rate + count)
- **Race** (rate + count)

Counts were included alongside rates to avoid over-interpreting small sample sizes.

---

## 🤖 Machine Learning (Baseline)

**Model:** Logistic Regression (with preprocessing pipeline: imputation + one-hot encoding + scaling)

**Test Set Performance**
- **ROC-AUC:** 0.6125  
- **PR-AUC:** 0.1729  

---

## 🚨 High-Risk Queue (Top 10% Rule)

Instead of choosing a fixed probability threshold, this project uses an operational approach:
- **Flag the Top 10% highest predicted risks** as `high_risk_top10`

**Top 10% Rule (Test Set)**
- Predicted high-risk rate: **10.1%**
- Readmission class metrics (`readmit_30 = 1`):
  - **Precision:** 0.20  
  - **Recall:** 0.18  
  - **F1:** 0.19  

**Interpretation:**  
This creates a manageable follow-up list while prioritizing the highest-risk encounters, which is closer to real-world workflows.

---

## 🧰 Tools Used

- **Python (pandas, NumPy)** — cleaning + analysis  
- **scikit-learn** — preprocessing + modeling  
- **matplotlib** — visualization  
- **Google Colab + Google Drive** — development environment  
- **Streamlit** — dashboard app

---

## ▶️ How to Run

### Notebook
Open and run:
- `notebooks/01_readmission_analysis.ipynb`


