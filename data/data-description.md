# Data Description

Raw data is not included in this repository because it comes from a real operating
ride-hailing platform and is covered by confidentiality constraints.

## Expected Local Layout

To run the notebooks locally, place the private files in:

```text
data/raw/orders_old_platform.csv
data/raw/orders_new_platform.csv
data/raw/drivers.csv
data/raw/clients.csv
```

The `data/raw/` directory is ignored by Git.

## Dataset Overview

| File | Description | Notes |
|---|---|---|
| `orders_old_platform.csv` | Orders before the platform migration | Semicolon-separated, `latin-1` encoding |
| `orders_new_platform.csv` | Orders after the platform migration | Semicolon-separated, `windows-1251` encoding; decimal comma in numeric fields |
| `drivers.csv` | Driver profile and performance export | `windows-1251`; decimal comma in monetary fields |
| `clients.csv` | Client profile export | `windows-1251`; many sparse platform-schema columns |

## Loading Notes

```python
import pandas as pd

df_old = pd.read_csv(
    "../data/raw/orders_old_platform.csv",
    sep=";",
    encoding="latin-1",
    low_memory=False,
)

df_new = pd.read_csv(
    "../data/raw/orders_new_platform.csv",
    sep=";",
    encoding="windows-1251",
    low_memory=False,
)

for col in ["Стоимость", "Суммарное расстояние (км)"]:
    df_new[col] = df_new[col].astype(str).str.replace(",", ".").astype(float)
```

## Confidentiality Rules Used in This Repository

- Raw records are not committed.
- Personal data such as names, phone numbers and emails is not committed.
- Credentials, system URLs and billing identifiers are not committed.
- Exact company financial outputs are not included in notebook outputs.
- The notebooks are kept as code-first artefacts for academic review.
