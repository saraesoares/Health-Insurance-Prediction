# Data

This project uses a customer dataset provided via a private Kaggle competition. No data is included in this repository.

## Access

The data was distributed through a course-restricted Kaggle competition (`https://www.kaggle.com/t/3cfa310942d4425c947467d71f12d05e`), open to enrolled students during the 2024/2025 term. It is not public.

* If you're a course participant with an active Kaggle account for this competition, download the files from the competition's "Data" tab.
* If the competition has since closed or been archived, the files may no longer be downloadable via Kaggle.
* Do not commit any of these files to this repositor, they were provided under the course's academic-use terms, not for public release.

## Required files

Download the following files directly to the `data/` directory:

| File | Purpose |
|---|---|
| `customer.csv` | Full labeled dataset — used for exploration, training, and validation |
| `customer_test_masked.csv` | 804 entries with `health_ins` masked (set to null) — final hold-out set for Kaggle submission |
| `customer_datadictionary.txt` | Variable definitions and coding |
| `sample_submission.csv` | Required format for Kaggle prediction submissions |

## Target variable

`health_ins` (binary): whether the customer has health insurance. The class is imbalanced — see the notebook's Section II (Data Understanding) for the exact split and Section IV for how balancing was handled during modeling.

## Notes

* Column `Unnamed: 0` (row index artifact) and `custid` (primary key) are dropped/indexed early in preprocessing — see `notebooks/IDS_project.ipynb`, cell after Section II.1.
* Any preprocessing applied to `customer.csv` must be applied identically to `customer_test_masked.csv` before generating predictions (the assignment brief requires this explicitly).