# Titanic — Exploratory & Descriptive Analysis

Project: concise EDA and cleaning pipeline for the Titanic dataset (Kaggle/classic dataset). This repository contains a Jupyter notebook that walks through dataset inspection, cleaning, and basic analyses (survival by sex, class and age).

## Repository structure

- `data/raw/titanic.csv` — original raw CSV used for analysis.
- `data/cleaned/titanic_cleaned.csv` — cleaned dataset produced by the notebook (created when the cleaning cell is run).
- `notebook/titanic_EDA.ipynb` — the main analysis notebook (load, inspect, clean, visualize, reflect).
- `README.md` — this file.

## Overview

This project performs a reproducible exploratory and descriptive analysis of the Titanic dataset. The notebook:

- Loads and inspects data quality (missing values, types).
- Applies pragmatic cleaning (impute Age, extract `Title`, derive `CabinDeck`, drop noisy identifiers).
- Saves a cleaned CSV to `data/cleaned/titanic_cleaned.csv`.
- Produces visual summaries and a short reflection describing results and next steps.

## Key cleaning choices (what notebook does)

- `Age`: median imputation and an `age_missing` indicator column.
- `Title`: extracted from `Name` to capture honorifics (Mr/Mrs/Miss/etc.).
- `Cabin`: extract deck letter (first character) as `CabinDeck` and add `cabin_missing` flag; raw `Cabin` dropped due to high sparsity.
- `Embarked`: small number of missings filled with mode.
- Drop noisy/identifier fields: `PassengerId`, `Ticket`, and the raw `Name` and `Cabin` columns.

These choices balance simplicity and signal: they are suitable for initial modeling and interpretation but are documented in the notebook as decisions with caveats.

## How to run

Prerequisites

- Python 3.8+ (recommended)
- Install required packages (if using the notebook interactively):

```bash
pip install pandas matplotlib seaborn
```

Steps

1. Open and run the notebook: [notebook/titanic_EDA.ipynb](notebook/titanic_EDA.ipynb).
2. Run cells sequentially. The cleaning cell will save `data/cleaned/titanic_cleaned.csv` when executed.
3. Inspect visualizations and the reflection section for suggestions on next steps.

Optional: to reproduce programmatically, run the notebook with `papermill` or convert it to a script.

## Summary of findings

- Females have a substantially higher survival rate than males (~74% vs ~19%).
- First-class passengers show much higher survival than third-class (approx 63% vs 24%).
- Children and younger passengers show elevated survival; Age has ~20% missingness and should be handled carefully for inference.

## Next steps / recommendations

- Fit multivariable models (logistic regression / tree-based) to estimate adjusted effects for `Sex`, `Pclass`, `Age`, and `Title`.
- Use multiple imputation for `Age` and compare with median imputation to assess sensitivity.
- Engineer features from `Ticket` (grouping) and `Name` (family features), and explore interactions (e.g., `Sex × Pclass`).

## Contact

If you want additional features (automated tests, `requirements.txt`, a small CLI to run cleaning, or a modelling notebook), ask and I will add them.
