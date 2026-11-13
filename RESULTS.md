# Results — Tunisia Desertification Risk Mapping

## 1. Model Comparison and Selection

Three machine learning models were evaluated:

- Random Forest
- XGBoost
- Logistic Regression

Logistic Regression achieved the highest numerical scores during model comparison. However, XGBoost was selected as the final model because the SHAP analysis revealed non-linear ecological relationships and vegetation thresholds that a linear model could not adequately represent.

The selection prioritized ecological interpretability over reproducing the mathematical structure of the DRI.

## 2. Model Explainability (SHAP)

SHAP analysis identified the following feature importance pattern:

1. NDVI
2. BSI
3. Temperature
4. Rainfall
5. Temporal features

NDVI and BSI were the dominant contributors to High-risk predictions.

### Ecological thresholds

The NDVI dependence analysis revealed a non-linear response:

- **Below 0.15:** Strong positive contribution to High-risk predictions.
- **Between 0.15 and 0.20:** Sharp decrease in contribution.
- **Above 0.20:** Strong negative contribution, followed by stabilization.

### Spatial contributions

Spatial SHAP analysis revealed:

- NDVI, rainfall, and temperature exhibit clear north–south patterns.
- BSI has a more localized contribution in north-central Tunisia.
- The strongest positive total SHAP contributions occur in southern Tunisia.
- Central transition zones contain areas with projected risk increases.

## 3. Spatial and Temporal Validation

Several validation experiments were conducted to examine whether the model's learned relationship with the DRI-derived risk classes remained consistent across different geographical and temporal settings.

### 2025 risk distribution

The predicted national distribution closely reproduced the DRI-derived reference distribution.

| Risk Class | DRI Labels | Model Predictions |
|---|---:|---:|
| High | 63.76% | 63.02% |
| Medium | 26.96% | 27.71% |
| Low | 9.28% | 9.27% |

The differences between the two distributions remained below one percentage point per class.

<p align="center">
  <img src=["https://github.com/amalherchh/AI-Desertification-Risk-Mapping-Tunisia/blob/main/map.png?raw=true"](https://github.com/amalherchh/Tunisia-Desertification-Risk-Mapping/blob/main/map.png?raw=true) alt="Tunisia Desertification Risk Map" width="800">
</p>

### Out-of-region validation

The model was evaluated on three held-out governorates, with training performed on the remaining 23 governorates.

| Governorate | Main observation |
|---|---|
| Bizerte | Consistent classification across models |
| Kairouan | Most challenging test, containing all three risk classes |
| Tataouine | Predominantly High-risk cells |

Kairouan provided the most informative regional comparison because it contained a more diverse distribution of risk classes.

### Rolling-origin temporal validation

The training period was progressively expanded from 2018–2019 to 2018–2024.

XGBoost maintained consistent performance across the successive temporal evaluation folds.

### Spatial block cross-validation

Leave-one-governorate-out validation was performed across all 24 governorates.

The evaluation examined how the model behaved when applied to geographical regions excluded from training, rather than relying exclusively on observations from familiar locations.

## 4. National Desertification Risk Forecast (2025–2030)

The forecast indicates an expansion of High-risk areas across Tunisia.

| Risk Class | 2025 | 2030 (Projected) | Relative Change |
|---|---:|---:|---:|
| Low | 9.3% | 6.2% | −33.3% |
| Medium | 28.5% | 25.5% | −10.5% |
| High | 62.2% | 68.3% | +9.8% |

The High-risk share is projected to increase by **6.1 percentage points** between 2025 and 2030.

### Spatial distribution of projected changes

The projected deterioration is concentrated mainly in northern and central Tunisia, particularly along the:

**Kef – Siliana – Kairouan – Sidi Bouzid corridor.**

Additional clusters appear in northwestern and northeastern Tunisia.

The southern region remains comparatively stable because many grid cells are already classified as High risk, producing a classification ceiling effect.

### Grid-cell transitions

| Transition | Share of Grid Cells |
|---|---:|
| Remain in the same risk class | 87.8% |
| Worsen by one class | 11.4% |
| Improve by one class | 0.8% |
| Worsen by two classes | 1 cell |

## 5. Forecast Reliability Assessment

The complete forecasting pipeline was evaluated through an out-of-time backtest.

- **Training period:** 2018–2021.
- **Forecast evaluation period:** 2022–2025.
- **Evaluation:** Comparison between projected environmental risk classes and known DRI-derived outcomes.

The backtest achieved **84.7% classification agreement**, with annual agreement ranging from 80.3% to 88.5%.

Environmental extrapolation errors:

| Variable | Error |
|---|---:|
| NDVI | 0.026 |
| BSI | 0.019 |
| Temperature | 0.36 °C |
| Rainfall | Largest relative error |

This experiment evaluates the complete environmental extrapolation and classification pipeline, rather than the classifier using observed environmental inputs.

## 6. Key Findings

- NDVI and BSI emerged as the dominant environmental contributors to predicted desertification risk.
- SHAP analysis revealed a non-linear NDVI response, with a notable transition around 0.15–0.20.
- Spatial and temporal validation examined the consistency of the learned environmental relationships across different regions and observation periods.
- High-risk land is projected to expand from 62.2% in 2025 to 68.3% in 2030.
- Projected deterioration is concentrated primarily in central and northern transition zones.
- The forecasting pipeline was further examined through an out-of-time historical backtest.

## 7. Interpretation and Limitations

The results must be interpreted in the context of the proxy-label approach.

The risk classes used for model development were derived from an AHP-based Desertification Risk Index rather than independently observed, field-verified desertification measurements. Consequently, model evaluation reflects its ability to reproduce the constructed environmental risk classification, not its ability to measure actual desertification with equivalent certainty.

Similarly, the 2026–2030 results represent projections based on historical environmental trends, not confirmed future observations.

The framework primarily captures remotely sensed and climate-related environmental conditions. Human drivers, including land-use pressure, agricultural practices, and population activities, are not yet fully represented.

Integrating complementary human-activity indicators, incorporating field observations, and exploring alternative environmental forecasting methods are important directions for further development.
