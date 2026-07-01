# Customer Churn Prediction — MLOps Pipeline

> End-to-end ML pipeline with full CI/CD automation.



---

## Problem Statement

A telecom company loses revenue every time a customer churns.
Predicting churn early lets the retention team reach out
proactively with offers before the customer leaves.

**Challenge:** Only ~27% of customers churn — heavily imbalanced.
Accuracy alone is misleading. Recall matters most — missing a
churner is more costly than a false alarm.

---

## CI/CD Pipeline

Every push to main automatically:

```
git push
    ↓
Job 1: Lint + Unit Tests     ← catches code bugs immediately
    ↓ (only if pass)
Job 2: Train + Metric Gate   ← catches model regressions
    ↓ (only if metrics pass thresholds)
Job 3: Docker Build          ← proves image builds correctly
    ↓
Pipeline Summary             ← full status report
```

**Metric thresholds enforced by CI:**
| Metric | Threshold |
|---|---|
| ROC-AUC | ≥ 0.70 |
| Recall | ≥ 0.60 |
| F1 Score | ≥ 0.55 |

If any metric falls below threshold — pipeline fails,
PR is blocked, model never reaches production.

---

## Full MLOps Stack

| Layer | Tool |
|---|---|
| Code versioning | Git |
| Data versioning | DVC |
| Experiment tracking | MLflow |
| Containerization | Docker |
| CI/CD automation | GitHub Actions |

---

## Quickstart

```bash
git clone https://github.com/MuhammadNaeem48916/churn-mlops
cd churn-mlops
pip install -r requirements.txt
python src/create_dataset.py
python src/train.py logistic
pytest tests/ -v
python tests/check_metrics.py
```

---

## Key concepts demonstrated

| Concept | Implementation |
|---|---|
| CI/CD pipeline | .github/workflows/ci.yml |
| Metric gating | tests/check_metrics.py |
| Unit testing | tests/test_train.py |
| Branch protection | Required status checks on main |
| Class imbalance | class_weight="balanced" + recall metric |
| Docker in CI | Build both images in pipeline |
| Artifact upload | metrics JSON + confusion matrix saved per run |

---

## Skills demonstrated

`MLOps` `CI/CD` `GitHub Actions` `Docker` `MLflow` `DVC`
`Git` 

---
