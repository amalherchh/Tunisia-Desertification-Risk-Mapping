# Tunisia Desertification Risk Mapping

AI-based desertification and land degradation risk mapping for Tunisia using satellite imagery, climate data, and machine learning. Built as a layer within **SmartSDG Tunisia**, supporting SDG 15 (Life on Land, Target 15.3) and SDG 13 (Climate Action).

An internship project (Manouba School of Engineering, Ecological Engineering) by **Amal Herch**, supervised by **Ali Ben Abbes**, Academic Year 2025–2026.


Full results: [`RESULTS.md`](./RESULTS.md)

## What this project does

Since no field-verified desertification ground-truth exists for Tunisia at national scale, this project:

1. Fuses Sentinel-2 (NDVI, SAVI, BSI), CHIRPS (rainfall), and ERA5-Land (temperature) data onto a shared 5 km national grid, 2016–2025.
2. Builds a **Desertification Risk Index (DRI)** using the Analytic Hierarchy Process (AHP) to derive defensible weights from expert judgment, then classifies it into Low/Medium/High risk via Jenks Natural Breaks.
3. Trains and compares **Random Forest, XGBoost, and Logistic Regression** classifiers against that proxy label, selecting **XGBoost** as the final model based on SHAP-verified non-linear ecological threshold learning (not raw accuracy).
4. Validates the model temporally, per-governorate (out-of-region), via rolling-origin cross-validation, and via spatial block (leave-one-governorate-out) cross-validation.
5. Forecasts risk for **2026–2030** using per-cell linear trend extrapolation + the trained classifier, and stress-tests that forecasting method with an out-of-time backtest (2018–2021 → predict 2022–2025, compare to known outcomes).
6. Delivers results as an interactive dashboard.

## Headline results

- **Final model:** XGBoost — 98.6% accuracy / 98.2% balanced accuracy on the held-out test set, selected over a higher-scoring Logistic Regression because SHAP confirmed it captures genuine non-linear ecological thresholds rather than just reconstructing the DRI formula.
- **Validated** temporally (98.4% agreement on 2025), spatially (97.4% mean accuracy across leave-one-governorate-out folds), and via rolling-origin cross-validation (97.6% mean accuracy).
- **2030 forecast:** High-risk land area projected to grow from 63.0% (2025) to 69.0% (2030), driven mainly by erosion of the Medium-risk transition zone in central Tunisia.
- **Forecast backtest:** 84.7% classification agreement when the same forecasting method was tested against already-known 2022–2025 outcomes.

Full numbers, tables, and per-governorate breakdowns: [`RESULTS.md`](./RESULTS.md)


## Dashboard

Results are delivered as an interactive dashboard with four sections: Risk Map (grid-cell or governorate level, any year 2018–2030), Governorate Explorer, Trends & Forecast, and Methodology.

## References

Saaty (1980, AHP) · Breiman (2001, Random Forests) · Chen & Guestrin (2016, XGBoost) · Lundberg & Lee (2017, SHAP) · Jenks (1967, Natural Breaks) · Sentinel-2, CHIRPS, ERA5-Land documentation · UNCCD SDG Indicator 15.3.1 Guidance

Amal Herch, 2025–2026
