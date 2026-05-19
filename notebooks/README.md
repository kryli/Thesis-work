# Notebook Guide

These notebooks contain the empirical analysis used in the bachelor thesis
**Research and Analysis of a Digital Taxi Platform Based on DodoGo**.

The thesis document is not included in this repository. The guide below shows
which notebook is connected to each thesis section and what type of analysis it
contains.

The private source data are not included. To run the notebooks, place the
required CSV files in `data/raw/`. Saved outputs are kept where they help review
the analysis, but sensitive company information is shown through indexes,
shares, percentages or model metrics instead of absolute financial values.

## 01_eda_full_analysis.ipynb

Thesis sections:

- `3.2.1 Growth and Temporal Patterns`
- `3.2.2 Demand Forecasting with SARIMA`
- `3.2.3 Wait Time Dynamics`
- `3.2.4 Price Acceptance and Area-Level Fare Patterns`

Focus: platform growth, daily and weekly demand patterns, forecasting,
wait-time dynamics and price-acceptance checks.

Main contents:

- Daily and monthly demand analysis.
- Hour and day-of-week demand profiles.
- SARIMA demand forecasting with a baseline comparison.
- Wait-time analysis where timestamps are available.
- Area-level price-acceptance diagnostics.

## 02_ml_fraud_cancellation.ipynb

Thesis section:

- `3.4.1 Cancellation Prediction and Suspicious-Pattern Detection`

Focus: cancellation behaviour, suspicious cancellation patterns and prediction
of cancellation risk.

Main contents:

- Cancellation reason analysis.
- Rule-based suspicious-pattern detection.
- XGBoost cancellation model with stratified validation.
- Behavioural feature extension.
- Driver risk categories based on cancellation patterns.

## 03_rfm_churn_positioning.ipynb

Thesis sections:

- `3.3.2 RFM Customer Segmentation`
- `3.3.3 Customer Churn Prediction`
- `3.4.2 Driver Positioning`

Focus: customer segmentation, customer churn prediction and driver positioning
across demand areas.

Main contents:

- RFM feature construction.
- K-Means customer segmentation.
- Gradient Boosting churn model.
- Behavioural feature extension.
- District and hour-level demand-supply gap analysis.

## 04_user_survival_cohort.ipynb

Thesis sections:

- `3.3.1 First-to-Second Trip Prediction`
- `3.3.4 Survival and Cohort Retention`
- `3.3.5 Customer Lifetime Value`

Focus: customer lifecycle, retention, tourist segmentation and first-trip return
prediction.

Main contents:

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

Main contents:

- OSM road-network processing.
- Address and routing architecture analysis.
- Relative cost comparison.
- Operational interpretation of the migration.

## 06_driver_ltv_churn_survival.ipynb

Thesis section:

- `3.4.3 Driver Lifetime Value and Churn`

Focus: driver value, driver survival, churn prediction and retention
prioritisation.

Main contents:

- Driver value distribution and Pareto analysis.
- Driver survival analysis.
- Leakage-aware churn modelling.
- Early-warning churn feature engineering.
- Driver risk matrix.
- Relative customer lifetime value analysis.

## Chapter 4 Link

Chapter 4 uses results from all notebooks. The findings are combined into the
As-Is / To-Be matrix, ranked recommendations and a framework for similar island
or constrained ride-hailing markets.
