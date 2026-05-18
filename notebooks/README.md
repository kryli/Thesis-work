# Notebook Guide

These notebooks support the empirical chapters of the bachelor thesis
**Research and Analysis of a Digital Taxi Platform Based on DodoGo**.

The thesis text is not included in this repository. The mapping below explains
which notebook supports which thesis section and which analysis appears in the
final argument.

The notebooks retain only NDA-safe outputs for GitHub review. Aggregate model
metrics, charts and non-sensitive summaries are kept where possible, while
outputs that may expose exact company financial values, personal records or raw
operational rows are cleared. The full code and markdown structure is preserved,
but the notebooks require private data files under `data/raw/` to execute.

## 01_eda_full_analysis.ipynb

Thesis sections:

- `3.2.1 Growth and Temporal Patterns`
- `3.2.2 Demand Forecasting with SARIMA`
- `3.2.3 Wait Time Dynamics`
- `3.2.4 Price Acceptance and Area-Level Fare Patterns`

Focus: platform growth, temporal demand patterns, SARIMA forecasting, wait-time
dynamics and price-acceptance diagnostics.

Main methods:

- Daily and monthly EDA.
- Hour and day-of-week demand profiles.
- SARIMA forecasting with baseline comparison.
- Wait-time decomposition where timestamps are available.
- Area-level price-acceptance diagnostics.

## 02_ml_fraud_cancellation.ipynb

Thesis section:

- `3.4.1 Cancellation Prediction and Suspicious-Pattern Detection`

Focus: cancellation behaviour, suspicious cancellation patterns, cancellation
prediction and driver risk categorisation.

Main methods:

- Cancellation reason analysis.
- Rule-based suspicious-pattern detection.
- XGBoost classification with stratified validation.
- Leakage-safe behavioural feature extension.
- Driver risk categories and value-risk matrix.

## 03_rfm_churn_positioning.ipynb

Thesis sections:

- `3.3.2 RFM Customer Segmentation`
- `3.3.3 Customer Churn Prediction`
- `3.4.2 Driver Positioning`

Focus: customer segmentation, churn prediction and driver positioning.

Main methods:

- RFM feature construction.
- K-Means customer segmentation.
- Gradient Boosting churn model.
- Leakage-safe behavioural feature extension.
- District and hour-level demand-supply gap analysis.

## 04_user_survival_cohort.ipynb

Thesis sections:

- `3.3.1 First-to-Second Trip Prediction`
- `3.3.4 Survival and Cohort Retention`
- `3.3.5 Customer Lifetime Value`

Focus: customer lifecycle, cohort retention, tourist segmentation and first-trip
return prediction.

Main methods:

- Kaplan-Meier survival analysis.
- Monthly cohort retention.
- Local, tourist SIM and international user segmentation.
- First-trip return prediction with Gradient Boosting.
- Contextual area and driver reliability features.
- Relative customer value concentration.

## 05_google_maps_osm_case.ipynb

Thesis sections:

- `2.5 Google Maps to OpenStreetMap Migration`
- `3.5 Google Maps to OpenStreetMap Migration`
- `4.7 Framework Reusability`

Focus: migration from Google Maps APIs to an OpenStreetMap-based stack.

Main methods:

- OSM road-network processing.
- Address and routing architecture analysis.
- Cost-ratio comparison.
- Operational interpretation of the migration.

## 06_driver_ltv_churn_survival.ipynb

Thesis section:

- `3.4.3 Driver Lifetime Value and Churn`

Focus: driver value, survival, churn prediction and retention prioritisation.

Main methods:

- Driver value distribution and Pareto analysis.
- Driver survival analysis.
- Leakage-aware churn modelling.
- Early-warning churn feature engineering.
- Driver risk matrix.

## Chapter 4 Link

Chapter 4 does not correspond to a single notebook. It synthesizes the notebook
findings into the As-Is / To-Be matrix, ranked recommendations and framework for
similar island or constrained ride-hailing markets.
