DSA 2050 – Week 6 Guided Regression Lab

shawn kamuyu ID: 675405

# Lab objective
Predict `Sales_KES` from advertising spend, store visits, discount percent, region, customer segment and product category, and test whether each model genuinely improves on a simple baseline. The lab uses leakage safe pipelines, training-only cross-validation, residual analysis and subgroup error checks.

# Models compared
Mean baseline, median baseline, Linear Regression, Ridge Regression (alpha = 1) and a shallow Decision Tree (max_depth = 4, min_samples_leaf = 8). An unrestricted tree was also fitted to demonstrate overfitting.

# Best model
*Ridge Regression** (essentially tied with Linear Regression).

| Model | Test MAE | Test RMSE | Test R² |
|---|---|---|---|
| Median baseline | 39,147 | 48,649 | -0.006 |
| Mean baseline | 39,197 | 48,716 | -0.008 |
| Decision Tree (depth 4) | 23,776 | 28,768 | 0.648 |
| Linear Regression | 13,758 | 17,470 | 0.870 |
| *Ridge Regression** | *13,714* | *17,459* | *0.870* |

*Selected model MAE:** KES 13,714 on the test set (5-fold CV MAE on training data: KES 15,971).

# Two key findings
1. Ridge/Linear Regression cut MAE by about 65% compared with the strongest baseline, and the improvement holds in cross-validation. `StoreVisits` is the most informative predictor: removing it drops R² from 0.87 to 0.24, while removing `AdvertisingSpend_KES` drops it to 0.69.
2. Errors are not uniform. Retail has the highest segment MAE (about 15,600 vs about 10,500 for SME), and the largest errors are mostly over-predictions for low-store-visit records. The unrestricted tree has a training MAE of 0 but a test MAE of about 26,800, which shows overfitting.

# Three limitations
1. Small dataset (320 rows; 64 in the test set), so subgroup results are noisy.
2. The data looks like clean teaching/synthetic data and has few predictors (no seasonality, store size, competition or other external factors).
3. The model shows association, not causation, and may drift on future data.

# Files
- `DSA2050_Week6_Guided_Regression_Lab.ipynb`
- `DSA2050_Week6_Sales_Data.csv`
- `README.md`
