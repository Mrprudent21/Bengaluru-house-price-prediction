# Bengaluru House Price Prediction

An end-to-end machine learning project for predicting residential property prices in Bengaluru, India.

## Overview

This project was originally completed as a capstone exercise and has been rebuilt using a cleaner, reproducible data science workflow covering data understanding, cleaning, exploratory analysis, feature engineering, preprocessing, linear regression, validation, evaluation and interpretation.

## Dataset

The project uses the Bengaluru Home Prices dataset. The raw CSV is intentionally not included in this public repository.

Place the dataset locally at:

`data/Bengaluru_House_Data.csv`

## Methodology

1. Inspect the raw data and data quality.
2. Remove exact duplicates.
3. Parse `total_sqft`, including ranges and recognised units.
4. Extract numeric BHK from `size`.
5. Standardise location text.
6. Simplify availability to a `ready_to_move` indicator.
7. Apply data-quality and plausibility filters.
8. Explore the target and important relationships.
9. Split into training and test data.
10. Reduce rare locations using training-data-only frequency information.
11. Build preprocessing and linear regression in a scikit-learn pipeline.
12. Evaluate with five-fold cross-validation.
13. Evaluate once on the untouched test set.
14. Inspect residuals and coefficients.
15. Demonstrate predictions for new properties.

## Important modelling decisions

`price_per_sqft` is used for exploratory analysis only because it is derived from the target price and would cause target leakage if used as a predictor.

Rare locations are grouped into `Other` using a frequency threshold learned from the training data only.

Numeric variables use median imputation and standardisation. Categorical variables use most-frequent imputation and unknown categories are handled safely.

## Results

On the supplied dataset, the refined linear regression produced approximately:

| Metric | Test |
|---|---:|
| R² | 0.327 |
| RMSE | 131.88 lakhs |
| MAE | 51.17 lakhs |

Five-fold cross-validation on the training data produced approximately 112.34 lakhs RMSE and 0.419 R² on average.

## Repository structure

```text
Bengaluru-house-price-prediction/
├── README.md
├── data/
│   └── README.md
├── notebooks/
│   └── Bengaluru_House_Price_Prediction.ipynb
├── reports/
│   └── README.md
├── requirements.txt
└── .gitignore
```

## Reproducibility

Create a virtual environment, install the requirements, place the CSV in `data/`, then run the notebook from top to bottom.

## Limitations

The dataset is historical and does not contain every factor influencing property prices. Location grouping reduces geographic detail, availability is simplified, and a linear model may not capture nonlinear relationships.
