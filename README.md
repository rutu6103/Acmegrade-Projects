# Acmegrade Machine Learning Projects

A curated collection of two regression projects completed during the Acmegrade Data Science program. The repository emphasizes reproducible paths, clear explanations, comparable evaluation metrics and reusable model pipelines.

## Projects

| Project | Problem | Main techniques | Historical best result |
|---|---|---|---|
| [Audi Car Price Prediction](car-price-prediction/) | Estimate a used Audi's price | preprocessing pipelines, linear baseline, Random Forest, Extra Trees, CatBoost | CatBoost R² ≈ 0.964 |
| [BigMart Retail Sales Prediction](retail-sales-prediction/) | Estimate product-level outlet sales | cleaning, feature engineering, cross-validation, ensemble and boosting models | XGBoost R² ≈ 0.739 on log sales |

The sales project is intentionally described as **sales prediction**, not sales forecasting: the available data has no time-indexed sequence.

## Repository structure

```text
Acmegrade-Projects/
├── README.md
├── .gitignore
├── car-price-prediction/
│   ├── README.md
│   ├── requirements.txt
│   ├── data/README.md
│   ├── notebooks/audi_car_price_prediction.ipynb
│   └── outputs/{figures,metrics,models}/
└── retail-sales-prediction/
    ├── README.md
    ├── requirements.txt
    ├── data/README.md
    ├── notebooks/bigmart_sales_prediction.ipynb
    └── outputs/{figures,metrics,models}/
```

## How to run

1. Download each dataset using the instructions in its `data/README.md`.
2. Place the CSV in the stated `data/` directory without renaming it.
3. Create and activate a Python environment.
4. Install that project's dependencies with `pip install -r requirements.txt`.
5. Open Jupyter from the repository root or from the project's `notebooks/` directory.
6. Run the notebook from top to bottom.

Generated figures, metrics, predictions and fitted pipelines are written to the appropriate `outputs/` subfolders. Large generated models and raw datasets are intentionally excluded from version control.

## Reproducibility notes

- Fixed random seeds are used for train/test splitting and compatible estimators.
- Preprocessing is fitted only through scikit-learn pipelines.
- Complete pipelines are saved, not bare estimators.
- Historical scores are retained in documentation for context; rerunning may produce small differences across library versions and hardware.

## Author

Rutuja Kadam — [GitHub profile](https://github.com/rutu6103)
