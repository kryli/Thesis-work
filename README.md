# DodoGo Bachelor Thesis Code Repository

This repository is the code companion for the bachelor thesis
**Research and Analysis of a Digital Taxi Platform Based on DodoGo**.

It is prepared for academic review. The repository does not include the thesis
text, raw operational data, credentials, personal records or company-internal
documents. Its purpose is to show which notebooks support which parts of the
thesis and to make the analytical workflow inspectable.

## Connection to the Thesis

The thesis text is submitted separately. This repository supports the empirical
and business-analytical parts of the thesis:

- **Chapter 1** explains the theoretical and methodological background.
- **Chapter 2** describes the Mauritius market, the DodoGo platform and the
  Google Maps to OpenStreetMap migration context.
- **Chapter 3** contains the main methodology and results. This is the chapter
  most directly supported by the notebooks.
- **Chapter 4** uses the analytical results to build the As-Is / To-Be matrix,
  ranked recommendations and reusable framework for similar markets.

## Thesis Section to Notebook Map

| Thesis part | Notebook | Analysis reflected in the thesis |
|---|---|---|
| `3.2.1 Growth and Temporal Patterns` | `01_eda_full_analysis.ipynb` | Platform growth phases, daily and hourly demand patterns, weekday effects |
| `3.2.2 Demand Forecasting with SARIMA` | `01_eda_full_analysis.ipynb` | SARIMA model, baseline comparison, short and long horizon forecast limits |
| `3.2.3 Wait Time Dynamics` | `01_eda_full_analysis.ipynb` | Timestamp-based wait-time decomposition and operational interpretation |
| `3.2.4 Price Acceptance and Area-Level Fare Patterns` | `01_eda_full_analysis.ipynb` | Area-level fare-completion relationship and supply/deadhead interpretation |
| `3.3.1 First-to-Second Trip Prediction` | `04_user_survival_cohort.ipynb` | First-trip return model, baseline and extended feature set |
| `3.3.2 RFM Customer Segmentation` | `03_rfm_churn_positioning.ipynb` | RFM features, K-Means clustering and six customer segments |
| `3.3.3 Customer Churn Prediction` | `03_rfm_churn_positioning.ipynb` | Gradient Boosting churn model and leakage-safe behavioural extension |
| `3.3.4 Survival and Cohort Retention` | `04_user_survival_cohort.ipynb` | Kaplan-Meier survival curve, monthly cohorts and retention profile |
| `3.3.5 Customer Lifetime Value` | `04_user_survival_cohort.ipynb` | Relative customer value concentration and bonus-program association |
| `3.4.1 Cancellation Prediction and Suspicious-Pattern Detection` | `02_ml_fraud_cancellation.ipynb` | XGBoost cancellation model, extended features and suspicious cancellation rules |
| `3.4.2 Driver Positioning` | `03_rfm_churn_positioning.ipynb` | District-level demand-supply gaps and undersupplied zones |
| `3.4.3 Driver Lifetime Value and Churn` | `06_driver_ltv_churn_survival.ipynb` | Driver value groups, survival analysis, churn model and risk matrix |
| `3.5 Google Maps to OpenStreetMap Migration` | `05_google_maps_osm_case.ipynb` | OSM-based routing/geocoding case and infrastructure cost ratio |
| `3.6 Summary of Results` | all notebooks | Fifteen-analysis summary table used to synthesize Chapter 3 |
| `Chapter 4: Recommendations` | all notebooks | Analytical basis for the As-Is / To-Be matrix and ranked recommendations |

## Repository Scope

Included:

- Jupyter notebooks used for the analytical part of the thesis.
- Notebook-level documentation explaining the purpose, methods and thesis links.
- Data schema and loading notes for reviewers who have private access to the data.
- Python dependency list.

Excluded:

- Raw CSV/XLSX data files.
- Final thesis `.docx`/`.pdf` files.
- Sensitive notebook outputs and execution counts.
- Generated external figure files.
- Credentials, API keys, billing identifiers, phone numbers or personal records.

The notebooks retain only NDA-safe outputs, such as aggregate model metrics and
non-sensitive charts. Outputs that may expose exact company financial values,
personal records or raw operational rows are cleared. The code cells remain
available for inspection and can be rerun only when the private data files are
available locally.

## Structure

```text
.
├── README.md
├── requirements.txt
├── .gitignore
├── data/
│   ├── data-description.md
│   └── raw/                  # ignored; private data goes here locally
└── notebooks/
    ├── README.md
    ├── 01_eda_full_analysis.ipynb
    ├── 02_ml_fraud_cancellation.ipynb
    ├── 03_rfm_churn_positioning.ipynb
    ├── 04_user_survival_cohort.ipynb
    ├── 05_google_maps_osm_case.ipynb
    ├── 06_driver_ltv_churn_survival.ipynb
    └── figures/              # ignored; generated locally
```

## Notebook Run Order

1. `01_eda_full_analysis.ipynb` - demand, temporal patterns, SARIMA, wait-time
   and price-acceptance analysis.
2. `02_ml_fraud_cancellation.ipynb` - cancellation patterns, suspicious behaviour
   and cancellation prediction.
3. `03_rfm_churn_positioning.ipynb` - RFM segmentation, customer churn and
   district-level driver positioning.
4. `04_user_survival_cohort.ipynb` - survival analysis, cohort retention, tourist
   segmentation and first-trip return.
5. `05_google_maps_osm_case.ipynb` - Google Maps to OpenStreetMap migration case.
6. `06_driver_ltv_churn_survival.ipynb` - driver value, survival, churn and risk
   matrix.

The notebooks are independent enough to inspect separately, but the numbering
follows the thesis narrative.

## Data

Raw data is not committed. To run the notebooks locally, place the private files
here:

```text
data/raw/orders_old_platform.csv
data/raw/orders_new_platform.csv
data/raw/drivers.csv
data/raw/clients.csv
```

The expected encodings and parsing notes are documented in
[`data/data-description.md`](data/data-description.md).

## Environment

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

`prophet` is optional and is used only in an exploratory comparison block. The
core thesis analyses rely on pandas, scikit-learn, XGBoost, statsmodels and
lifelines.

## NDA Note

DodoGo is a real operating company. This repository is intentionally limited to
code and methodological documentation. It avoids raw data, thesis drafts,
credentials, personal records and exact company financial outputs.
