# Triage Priority Prediction (KTAS)

Predict emergency vs non-emergency cases using only initial triage information and minimize under-triage by prioritizing recall for emergency cases.

## Why this project
In virtual care and emergency settings, identifying high-risk patients early is critical. Under-triage (missing true emergencies) can delay care and worsen outcomes. This project builds a decision-support model aligned with real-world triage principles.

## Dataset
Emergency department triage dataset based on the Korean Triage and Acuity Scale (KTAS).

- Target (binary):
  - Emergency = KTAS 1–3
  - Non-Emergency = KTAS 4–5
- Features (initial information only):
  - Demographics: sex, age
  - Arrival context: arrival mode, injury
  - Clinical assessment: chief complaint, mental state, pain, NRS pain
  - Vitals: SBP, DBP, HR, RR, BT

> Note: This is a decision-support prototype. It does not provide diagnosis or treatment recommendations.

## Evaluation focus
Primary metric: **Recall (Emergency)** to reduce under-triage  
Secondary: Precision (Emergency), ROC-AUC, PR-AUC  
Reporting: Confusion matrix and under-triage rate (FN / (TP + FN))

## Project structure (planned)
- `notebooks/` EDA and modeling notebooks
- `src/` training and evaluation scripts
- `data/README.md` instructions to obtain the dataset (no raw data stored)

## Next steps
- Exploratory data analysis (missingness, outliers, class imbalance)
- Baseline model (logistic regression)
- Improved model (tree-based model)
- Subgroup checks (e.g., age/sex) to identify potential bias
