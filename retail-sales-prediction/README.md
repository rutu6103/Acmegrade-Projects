# BigMart Retail Sales Prediction

## Business question

Can product and outlet characteristics estimate sales for a product–store combination? Such estimates can support assortment review, store benchmarking and inventory planning.

## Why this is prediction, not time-series forecasting

The dataset contains product and store attributes but no dated sales sequence. Therefore the appropriate technical description is **tabular regression** or **retail sales prediction**.

## Dataset

The dataset contains 8,523 rows and 12 columns. `Item_Outlet_Sales` is the target. The source and exact setup instructions are in [`data/README.md`](data/README.md).

## Workflow

1. Inspect missing values and inconsistent category labels.
2. Standardize fat-content labels and derive broad item category and outlet age.
3. Treat zero visibility as missing and impute within the model pipeline.
4. Log-transform the skewed sales target.
5. Compare linear, regularized, ensemble and gradient-boosting regressors.
6. Use five-fold cross-validation plus a held-out test set.
7. Save predictions, metrics, figures and the complete selected pipeline.

## Results and plain-language interpretation

The historical run reported approximately:

| Model | Mean CV R² (log sales) |
|---|---:|
| Linear Regression | 0.721 |
| Ridge | 0.721 |
| Random Forest | 0.707 |
| Extra Trees | 0.681 |
| XGBoost | 0.686 |

After hyperparameter searches, the held-out R² values were approximately **0.739 for XGBoost**, **0.738 for LightGBM** and **0.711 for Random Forest**. These figures show that boosting captured some nonlinear behaviour beyond the linear baseline, although the improvement was moderate.

The original notebook also printed training scores as high as 1.0 for individual tree ensembles. Those are not final accuracy results: they indicate that flexible models can memorize training records. Cross-validation and held-out test results are the appropriate measures of generalization.

## Output files created after running

- `outputs/figures/sales_distribution_and_mrp.png`
- `outputs/figures/sales_by_outlet_type.png`
- `outputs/figures/actual_vs_predicted.png`
- `outputs/metrics/model_comparison.csv`
- `outputs/metrics/test_predictions.csv`
- `outputs/metrics/run_summary.json`
- `outputs/models/retail_sales_pipeline.joblib`

## Limitations

- The data does not support trend, seasonality or future-date forecasting.
- Sales are influenced by promotions, stock availability and local demand that are not recorded.
- Results may not transfer unchanged to different retailers or time periods.
