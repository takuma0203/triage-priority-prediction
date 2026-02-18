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

## Decision threshold (recall-prioritized)
Because under-triage (missing true emergencies) is more harmful than over-triage in triage settings, we set the decision threshold to **0.30** to prioritize recall for emergency cases.

At threshold=0.30:
- Recall (Emergency): 0.925
- Precision (Emergency): 0.660
- False Negatives (under-triage): 11 (reduced from 35 at threshold=0.50)
- False Positives (over-triage): 70

## Results (baseline vs with chief complaint text)
Adding chief complaint text (TF-IDF) substantially improved discrimination performance:

- ROC-AUC improved from 0.745 → 0.854.
- At a safety-first threshold=0.30:
  - Recall (Emergency): 0.925 → 0.939
  - False Negatives (under-triage): 11 → 9
  - False Positives (over-triage): 70 → 55

This indicates chief complaint text provides important signal for triage prioritization.

## Next steps
- Exploratory data analysis (missingness, outliers, class imbalance)
- Baseline model (logistic regression)
- Improved model (tree-based model)
- Subgroup checks (e.g., age/sex) to identify potential bias
