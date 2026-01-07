# ICU 30-Day Mortality Risk Stratification (MIMIC-III) — Baseline vs Full + Power BI

## What this is
A small end-to-end healthcare analytics project using **MIMIC-III** to predict **30-day mortality after ICU admission**.

The key point is not “a fancy model”, but demonstrating that **early clinical information improves decision usefulness**:
- **Baseline**: Age + Gender
- **Full model**: Age + Gender + **first 24h lab tests**

Outputs are validated as **risk stratification** (Low/Medium/High) and visualized in **Power BI**.

---

## Why I built it
Hiring teams often ask whether I can work with **raw clinical databases** and build a complete pipeline:
- define a cohort correctly
- avoid time leakage
- engineer features
- compare models
- communicate results in a business-friendly dashboard

This project is designed to demonstrate exactly that.

---

## Data (not included)
Data come from **MIMIC-III** (restricted access).  
This repository includes **code + figures only** (no raw patient data).

Tables used:
- PATIENTS, ADMISSIONS, ICUSTAYS, LABEVENTS

---

## Method (high level)
1. Build ICU-stay level cohort (**ICUSTAY_ID**) and label outcome: `death_30d`
2. Baseline features: age, gender
3. Full features: lab values within **first 24h of ICU** (aggregations like mean/min/max)
4. Train/test split and model comparison (ROC-AUC + PR-AUC)
5. Export predictions and validate risk stratification using **observed mortality by risk group**
6. Visualize in **Power BI**

---

## Results (what to look at)
### 1) Baseline vs Full risk stratification
- Baseline shows limited separation
- Full model shows clear separation (High-risk group has much higher observed mortality)

**Power BI / Figures**
- `figures/full_risk_group_mortality.png`
- `figures/baseline_risk_group_mortality.png`
- `powerbi/dashboard.png`

---

## Repo contents
- `*.ipynb` : full pipeline (data loading → features → modeling → export)
- `figures/` : plots used in the write-up
- `powerbi/` : dashboard screenshot(s)

---

## Key takeaway
Early ICU laboratory measurements provide meaningful clinical signal beyond demographics alone, enabling clearer **risk stratification** for 30-day mortality.
