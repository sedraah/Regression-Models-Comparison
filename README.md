# Concrete Compressive Strength Prediction (Regression)

## Overview

This project builds and compares four regression models to predict the compressive strength of concrete mixtures (in MPa) from ingredient-level features. Models evaluated include Linear Regression, Ridge Regression, K-Nearest Neighbors Regression, and Decision Tree Regression, with StandardScaler applied where appropriate and 5-fold cross-validation used to assess generalization.

---

## Dataset

**Source:** [Concrete Compressive Strength Data Set — Kaggle](https://www.kaggle.com/datasets/elikplim/concrete-compressive-strength-data-set)

The original dataset contains 1,030 rows and 9 columns. The version used in this project has been pre-cleaned as follows:

- Removed 25 duplicate rows
- Column names simplified to short `snake_case` names
- All columns verified as numeric
- No missing values and no duplicate rows remain

**Final shape:** 1,005 rows × 9 columns (8 features + 1 target)

**Target variable:** `compressive_strength_mpa` — continuous, measured in MPa

---

### Regression Models, Evaluation & Comparison
- Split data: 80% train / 20% test, `random_state=42`
- Apply `StandardScaler` to produce `X_train_scaled` and `X_test_scaled`
- Regression models were trained with the following configurations:

| Model | Key Parameters | Data Used |
|---|---|---|
| Linear Regression | default | Scaled |
| Ridge Regression | `alpha=1.0` | Scaled |
| KNN Regression | `n_neighbors=7` | Scaled |
| Decision Tree Regression | `max_depth=6`, `random_state=42` | Unscaled |

- Evaluate each model on the test set using MAE, RMSE, and R²

### Model Comparison

| Model | Test MAE | RMSE | R² |
|---|---|---|---|
| Linear Regression | 8.8960 | 11.1922 | 0.5801 |
| Ridge Regression | 8.8983 | 11.1942 | 0.5800 |
| KNN Regression | 7.5322 | 9.6689 | 0.6866 |
| **Decision Tree Regression** | **5.9225** | **7.8464** | **0.7936** |

### 5-Fold Cross-Validation (Decision Tree)

```
R² scores: [0.7943  0.7428  0.7117  0.7981  0.7639]
Mean CV R²: 0.7621
```

### Key Insight

The Decision Tree Regressor achieved the best performance across all three metrics with the lowest MAE (5.92), lowest RMSE (7.85), and highest R² (0.7936). Using multiple evaluation metrics is important because each tells a different part of the story: MAE gives the average prediction error in interpretable units, RMSE penalizes larger errors more heavily, and R² shows how much of the variance in concrete strength the model explains. Relying on any single metric can give a misleading picture of model quality.
