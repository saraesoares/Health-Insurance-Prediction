# Predicting Health Insurance Coverage

Predicting whether a US customer has health insurance, based on demographic, employment, income, and housing attributes. Built as a binary classification pipeline following CRISP-DM, from raw data exploration through model comparison and a held-out Kaggle test submission.

## Problem

Given customer attributes (age, employment status, income, housing, vehicles, marital status, region), predict the binary `health_ins` label. The target is class-imbalanced. Final models are scored by F1 on a masked Kaggle test set.

## Method

1. **Data understanding**: variable typing (nominal/ordinal/interval/ratio), summary statistics, distribution plots, duplicate/negative-value checks.
2. **Data preparation**: missing-value imputation (mode for categorical, mean for numeric), outlier handling on `age` via IQR, feature engineering (`age_group`, `income_group`, `gas_group`), log-transform on `income` (heavily skewed), one-hot/label encoding, standard scaling of continuous variables.
3. **Class imbalance**: three dataset variants compared — unbalanced, SMOTE-oversampled, and SMOTE + random undersampling (hybrid). The hybrid version was carried forward.
4. **Modeling**: KNN, Decision Tree, Random Forest, Gradient Boosting, Gaussian Naive Bayes — each with 10-fold cross-validation and a held-out validation split. (SVM, Logistic Regression, and a Neural Network were also tried with comparable results and omitted from the final notebook.)
5. **Final evaluation**: predictions on `customer_test_masked.csv`, submitted to the course's private Kaggle competition (F1-scored leaderboard).

## Results

Validation-set metrics (from the internal 80/20 split of `customer.csv`):

| Model | Precision | Recall | F1 | ROC-AUC | Log loss |
|---|---:|---:|---:|---:|---:|
| KNN (k=3) | 0.889 | 0.741 | 0.808 | 0.825 | 6.31 |
| Decision Tree | 0.745 | 0.692 | 0.717 | 0.729 | 9.77 |
| **Random Forest** | **0.880** | **0.833** | **0.856** | **0.860** | **5.04** |
| Gradient Boosting | 0.810 | 0.679 | 0.738 | 0.760 | 8.62 |
| Gaussian Naive Bayes | 0.758 | 0.591 | 0.664 | 0.702 | 10.72 |

**Final Kaggle submission**: Gradient Boosting, F1 = 0.74 on the masked test set.

## Findings

* Higher income brackets show near-universal insurance coverage; uninsured customers are concentrated in lower income groups.
* Probability of having insurance increases steadily with age — low in the 20s–40s, near-certain by 60+.
* `is_employed` and `age` both show positive correlation with `health_ins`; `income` shows a weaker positive correlation.
* Target class is heavily imbalanced, motivating the balanced-dataset comparison in the modeling step.

## Repository Structure

```
health-insurance-prediction/
├── README.md
├── environment.yml
├── .gitignore
├── LICENSE
├── notebooks/
│   └── IDS_project.ipynb
└── data/
    └── README.md
```

## Setup

```bash
conda env create -f environment.yml
conda activate health-insurance-prediction
jupyter notebook notebooks/IDS_project.ipynb
```

Dataset (`customer.csv`, `customer_test_masked.csv`, `customer_datadictionary.txt`, `sample_submission.csv`) is not included in this repository — see [`data/README.md`](data/README.md) for how to obtain it.

## Report

Full writeup, narrative and code: [`notebooks/IDS_project.ipynb`](notebooks/IDS_project.ipynb) (HTML export: [`reports/IDS_project.html`](reports/IDS_project.html))
Slide summary: [`reports/presentation.pdf`](reports/presentation.pdf)

## Acknowledgements

Developed as part of the *Introduction to Data Science* course, Faculty of Sciences, University of Porto, 2024/2025, in collaboration with a group of 3 students: Beatriz Pereira, Rita Simões, Sara Soares (me). All group members contributed to the design and implementation of the pipeline described above.