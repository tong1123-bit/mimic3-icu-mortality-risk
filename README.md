# ICU 30-Day Mortality Risk Stratification (MIMIC-III)

## What is this project?
This project builds a **30-day mortality risk stratification model for ICU patients** using real-world clinical data from the **MIMIC-III database**.

The goal is not just to train a predictive model, but to demonstrate:
- how to work with a raw medical database,
- how to compare a simple baseline with more informative models,
- and how to communicate results clearly using **Power BI**.

---

## Why this matters
In healthcare analytics, a model with a higher AUC is not always more useful in practice.  
What matters is whether the model can **separate patients into meaningful risk groups** that align with real clinical outcomes.

This project focuses on:
- proper cohort construction,
- avoiding data leakage,
- and validating models via **observed mortality by risk group**, not metrics alone.

---

## Data source
- **MIMIC-III** (public ICU database, restricted access)
- Tables used:
  - PATIENTS
  - ADMISSIONS
  - ICUSTAYS
  - LABEVENTS

> Raw patient-level data are not included in this repository.

---

## Study design (high level)
- Unit of analysis: **ICU stay (ICUSTAY_ID)**
- Population: adult ICU patients
- Outcome: **death within 30 days after ICU admission**
- Feature window: **first 24 hours in ICU only**

---

## Models compared
### Baseline model
- Age  
- Gender  

### Full model
- Age  
- Gender  
- Laboratory measurements from the **first 24 hours in ICU**  
  (aggregated statistics such as mean / min / max)

### Algorithms
- Logistic Regression  
- Random Forest  
- Histogram-based Gradient Boosting  

Random Forest achieved the best overall performance and was used for downstream analysis.

---

## Key results
### Risk stratification performance
Predicted probabilities were grouped into:
- **Low risk**
- **Medium risk**
- **High risk**

Observed 30-day mortality was then calculated for each group.

**Baseline model**
- Limited separation between risk groups

![Baseline Risk Group Mortality](baseline_risk_group_mortality.png)

**Full model**
- Clear and monotonic separation
- High-risk group shows substantially higher observed mortality

![Full Risk Group Mortality](full_risk_group_mortality.png)

---

## Visualization (Power BI)
Model outputs were exported and visualized using **Power BI** to support decision-oriented interpretation.

Included in this repository:
- Power BI dashboard file (`.pbix`)
- Risk group comparison and outcome plots

---

## Repository contents
- `MIMIC_*.ipynb`  
  End-to-end pipeline: cohort creation, feature engineering, modeling, and export
- `baseline_risk_group_mortality.png`  
- `full_risk_group_mortality.png`  
- `powerbidashboard.pbix`

---

## Takeaway
Early laboratory data from the first 24 hours of ICU admission provide meaningful clinical signal beyond demographics alone, enabling clearer and more actionable **risk stratification** for 30-day mortality.
