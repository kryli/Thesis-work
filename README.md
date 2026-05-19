# DodoGo Bachelor Thesis Code Repository

This repository is the code companion for the bachelor thesis
**Research and Analysis of a Digital Taxi Platform Based on DodoGo**.

The thesis document is submitted separately. This repository contains the
notebooks, environment notes and data documentation needed to inspect the
analytical workflow behind the thesis.

## Contents

- [Project Purpose](#project-purpose)
- [Repository Scope](#repository-scope)
- [Repository Structure](#repository-structure)
- [Notebooks](#notebooks)
- [Data](#data)
- [Environment](#environment)
- [Confidentiality](#confidentiality)

## Project Purpose

DodoGo is a digital taxi platform operating in Mauritius. The thesis studies the
platform from a data science and business analytics perspective: demand growth,
forecasting, cancellations, customer retention, driver positioning, driver churn
and the migration from Google Maps APIs to an OpenStreetMap-based stack.

The notebooks support the empirical part of the thesis. They are included so
that the reviewer can inspect the analysis logic, modelling choices and saved
aggregate outputs without access to the thesis text or private operational data.

## Repository Scope

Included:

- Six Jupyter notebooks used for the empirical analysis.
- A notebook guide with the link between notebooks and thesis sections.
- A data guide with expected file layout, analytical fields and parsing notes.
- A Python dependency list.

Excluded:

- Raw CSV or spreadsheet data.
- Final thesis `.docx` or `.pdf` files.
- Credentials, access keys, billing identifiers and system URLs.
- Personal records such as phone numbers, names and emails.
- Absolute company financial outputs.

Saved notebook outputs are kept only where they help review the work. Sensitive
values are shown through indexes, shares, percentages, ratios or model metrics.

## Repository Structure

```text
.
|-- README.md
|-- requirements.txt
|-- data/
|   |-- data-description.md
|   `-- raw/
`-- notebooks/
    |-- README.md
    |-- 01_eda_full_analysis.ipynb
    |-- 02_ml_fraud_cancellation.ipynb
    |-- 03_rfm_churn_positioning.ipynb
    |-- 04_user_survival_cohort.ipynb
    |-- 05_google_maps_osm_case.ipynb
    `-- 06_driver_ltv_churn_survival.ipynb
```

`data/raw/` is ignored by Git and is used only for private local data files.

## Notebooks

The notebooks follow the thesis narrative:

1. [`01_eda_full_analysis.ipynb`](notebooks/01_eda_full_analysis.ipynb) covers
   platform growth, demand patterns, SARIMA forecasting, wait time and
   price-acceptance analysis.
2. [`02_ml_fraud_cancellation.ipynb`](notebooks/02_ml_fraud_cancellation.ipynb)
   covers cancellation patterns, suspicious behaviour and cancellation
   prediction.
3. [`03_rfm_churn_positioning.ipynb`](notebooks/03_rfm_churn_positioning.ipynb)
   covers RFM segmentation, customer churn and driver positioning.
4. [`04_user_survival_cohort.ipynb`](notebooks/04_user_survival_cohort.ipynb)
   covers customer survival, cohort retention, tourist segmentation and
   first-trip return prediction.
5. [`05_google_maps_osm_case.ipynb`](notebooks/05_google_maps_osm_case.ipynb)
   covers the Google Maps to OpenStreetMap migration case.
6. [`06_driver_ltv_churn_survival.ipynb`](notebooks/06_driver_ltv_churn_survival.ipynb)
   covers driver value, driver survival, churn prediction and risk
   prioritisation.

For the detailed thesis-section mapping, see
[`notebooks/README.md`](notebooks/README.md).

## Data

Raw data is not committed. To run the notebooks locally, the private files must
be placed in:

```text
data/raw/orders_old_platform.csv
data/raw/orders_new_platform.csv
data/raw/drivers.csv
data/raw/clients.csv
```

The expected file roles, analytical fields, encodings and data quality notes are
documented in [`data/data-description.md`](data/data-description.md).

## Environment

Create a local environment and install the required packages:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

The core analysis uses pandas, NumPy, scikit-learn, XGBoost, statsmodels,
lifelines, matplotlib and seaborn.

## Confidentiality

DodoGo is a real operating company. This repository is limited to code,
methodological notes and reviewer-facing saved outputs. It does not include raw
operational data, thesis drafts, credentials, personal records or absolute
company financial values.
