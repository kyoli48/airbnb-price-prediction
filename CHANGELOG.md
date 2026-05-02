# Changelog

## Dependency Setup (2026-05-02)

### Packaging
- Added [requirements.txt](requirements.txt) so the project dependencies can be installed with a single command using `pip install -r requirements.txt`.

### Notebook Bootstrap
- Added an auto-install setup cell near the top of the notebook so missing Python packages are installed the first time the notebook runs in a fresh environment.
- The setup cell checks for `numpy`, `pandas`, `matplotlib`, `seaborn`, and `scikit-learn` before installing anything.

### Environment Guidance
- Recommended using a virtual environment for local runs so the notebook dependencies stay isolated from system Python.

## Notebook Enhancements (2026-05-01)

### Bug Fixes
- **RMSE calculation corrected** — was reporting MSE (mean squared error) instead of RMSE. Changed to `np.sqrt(mean_squared_error(...))`.
- **Cell ordering fix** — `residuals` variable was referenced before being defined; moved computation upstream.
- Removed duplicate boxplot and duplicate feature importance cells.

### Standardization & Normalization (Section 11a)
*Addresses professor feedback on scaling data to improve model performance.*

- Added a dedicated **scaling comparison section** benchmarking No Scaling vs StandardScaler vs MinMaxScaler on Ridge regression.
- Includes a reference table explaining each method's formula and when to use it.
- Bar chart visualization comparing MAE and R² across scaling strategies.
- Markdown discussion of why scaling matters for this dataset (features span very different ranges).

### Feature Engineering (Section 6)
- **Log-transformed** right-skewed numeric features (`minimum_nights`, `number_of_reviews`, `calculated_host_listings_count`) to reduce outlier influence.
- **Frequency-encoded `neighbourhood`** (811 unique values) instead of one-hot encoding, which produced a massive sparse matrix that hurt tree-based models.
- **Extracted `days_since_last_review`** as a numeric recency proxy for listing activity.

### Model Improvements
- Added **Ridge** and **Lasso** regression (were imported but never used).
- Increased Random Forest estimators from 30 to 200 and max depth from 12 to 20.
- Increased Gradient Boosting estimators from 50 to 300, max depth from 3 to 5, and added subsampling.
- Changed cross-validation from 3-fold to **5-fold** (matching the `CV_FOLDS` config variable).
- Added **hyperparameter tuning** via `RandomizedSearchCV` for Gradient Boosting (Section 12a).

### Analysis Depth
- Added **correlation heatmap** (seaborn) to EDA section.
- Added **error analysis by segment** — breaks down MAE by room type and price tier.
- Replaced placeholder "Key Findings" with substantive write-up covering data quality, scaling impact, model performance, and limitations.
- Updated "Next Steps" with actionable recommendations (target encoding, XGBoost/LightGBM, per-city models, SHAP values).
- Standardized section headers from mixed `#`/`##` to consistent `##` formatting.
