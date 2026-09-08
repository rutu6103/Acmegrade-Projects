# Generated outputs

The ZIP contains empty output directories by design because the datasets are not bundled. Running each notebook from top to bottom creates the documented figures, metrics, prediction tables and complete model pipeline in that project's own `outputs/` directory.

Do not add `catboost_info/` or the previous `model.pkl`. The former contains temporary logs. The latter saves only the estimator and omits the transformations required to turn raw vehicle fields into model-ready features. Each revised notebook saves a complete `.joblib` pipeline instead.
