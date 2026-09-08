# Audi Car Price Prediction

## Business question

Can vehicle specifications and usage history estimate the market price of a used Audi? A reliable estimate can support initial valuation, listing review and identification of unusually priced vehicles.

## Dataset

The analysis uses 10,668 Audi listings with vehicle model, year, transmission, mileage, fuel type, tax, miles per gallon and engine size. Price is the regression target. Download instructions and the exact expected filename are in [`data/README.md`](data/README.md).

## Workflow

1. Validate the dataset schema and inspect data quality.
2. Explore price distribution, mileage and numeric correlations.
3. Median-impute and scale numeric features; mode-impute and one-hot encode categories.
4. Create a fixed 80/20 train/test split.
5. Compare Linear Regression, Random Forest, Extra Trees and CatBoost.
6. Evaluate with R², MAE and RMSE.
7. Save figures, test predictions, metrics and the complete best pipeline.

## Results and plain-language interpretation

The original run produced approximately:

| Model | Test R² | Test MAE |
|---|---:|---:|
| Linear Regression | 0.792 | £3,382 |
| Random Forest | 0.954 | £1,539 |
| Tuned Random Forest | 0.959 | £1,505 |
| CatBoost | **0.964** | — |

An R² of 0.964 means the model explained roughly 96.4% of price variation in this held-out sample. It does **not** mean that every individual price is 96.4% accurate. MAE gives a more practical view: the tree models' predictions were typically about £1.5k away from the listed price.

The large improvement over Linear Regression indicates that price depends on nonlinear combinations—for example, mileage may affect a newer premium model differently from an older entry-level model.

## Output files created after running

- `outputs/figures/price_distribution_and_mileage.png`
- `outputs/figures/numeric_correlation.png`
- `outputs/figures/actual_vs_predicted.png`
- `outputs/metrics/model_comparison.csv`
- `outputs/metrics/test_predictions.csv`
- `outputs/metrics/run_summary.json`
- `outputs/models/car_price_pipeline.joblib`

The former `catboost_info/` folder and standalone `model.pkl` are excluded. CatBoost logs are temporary training diagnostics, while the old pickle did not contain the preprocessing required for raw inputs. The notebook saves one complete reusable pipeline instead.

## Limitations

- The data represents one brand, geography and historical period.
- Listing price may differ from the final transaction price.
- Market shifts and rare premium models can reduce accuracy on new data.
