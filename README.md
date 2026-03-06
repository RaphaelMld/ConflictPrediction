# Conflict Prediction Using Socio-Economic Indicators


[![Institution](https://img.shields.io/badge/Sorbonne_Université-M1_MIND-darkred.svg)]()

This repository contains a machine learning pipeline designed to predict the probability of a country engaging in an armed conflict in the following year ($T+1$). By framing conflict prediction as a supervised binary classification problem, this project leverages global socio-economic indicators to identify underlying risk factors.

Developed for the Master 1 MIND (2025-2026) program at Sorbonne Université.

## Task Definition and Data Sources

The prediction system is built on a defined scope of **113 countries** covering the period **1960–2024**, utilizing two primary data sources:

* **Target Variable ($Y$):** Peace (0) or Conflict (1), sourced from the **UCDP/PRIO Armed Conflict Dataset** (Uppsala Conflict Data Program, v25.1).
  * *Citation: Gleditsch et al., 2002; Davies et al., 2025.*
* **Explanatory Variables ($X$):** National socio-economic indicators (GDP, demographics, agriculture, etc.) retrieved from the World Bank Group's **data360 API**.


## Methodology

1. **Data Preprocessing:** Handling missing values via interpolation and generating `was_interpolated` flags to preserve data integrity.

2. **Dimensionality Reduction:** Scaling (Robust/Standard) followed by Principal Component Analysis (PCA) retaining 95% of the variance.
3. **Modeling:** Evaluation of ensemble methods including ExtraTrees, XGBoost, LightGBM, CatBoost, and Random Forest.
4. **Interpretability:** SHAP value analysis to extract key socio-economic drivers (e.g., cereal yields reducing conflict risk, while specific youth demographics increase it).


## Key Results

* **Best Performing Models:** The project evaluated models across two distinct data pipelines. The test partition was evaluated on the 2012–2023 time range.

| Model | Dataset Approach | Recall | Precision | F1 (Test) | F1 (Train) | Gap (Train-Test) | ROC-AUC |
| :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: |
| **CatBoost** | Non-Dense | 0.845 | 0.758 | **0.799** | 0.987 | 0.188 | 0.917 |
| **ExtraTrees** | Dense | 0.759 | 0.698 | **0.727** | 0.746 | **0.019** | 0.781 |

* **The Trade-off:** **CatBoost** achieved the highest absolute scores but showed significant overfitting. In contrast, **ExtraTrees** proved to be the most robust and reliable model for new data, thanks to its minimal train-test gap (0.019).
* **SHAP Insights:** Socio-economic factors strongly influence geopolitical stability. For example:
  * **Decreases conflict risk:** High agricultural productivity (e.g., Cereal yield).
  * **Increases conflict risk:** Demographic pressures (e.g., High proportion of youth aged 0-14).



## Authors

* **Raphaël Malidin** - [RaphaelMld](https://github.com/RaphaelMld)
* **Florian Biardeau** - [florianbiardeau](https://github.com/florianbiardeau)
