# Data Description

This repository does not include the original operational exports used for the
empirical results. Instead, it includes small synthetic sample CSV files with
test values so that reviewers can inspect the expected field structure.

This file describes the expected local data structure, sample files, parsing
rules and the way each dataset is used in the notebooks.

## Expected Local Layout

To run the notebooks locally, place the source files in:

```text
data/raw/orders_old_platform.csv
data/raw/orders_new_platform.csv
data/raw/drivers.csv
data/raw/clients.csv
```

The `data/raw/` directory is ignored by Git.

For schema inspection without the source exports, use:

```text
data/sample/orders_old_platform_sample.csv
data/sample/orders_new_platform_sample.csv
data/sample/drivers_sample.csv
data/sample/clients_sample.csv
```

The sample files are semicolon-separated CSV files with 60 synthetic rows each.
They contain test names, test phone numbers, test addresses and generated
numeric values. All sample files use English field aliases for readability on
GitHub, while the original exports use the platform-native field names listed
below. The sample files are not used as evidence for the thesis results.

## Dataset Overview

### `orders_old_platform.csv`

- Unit of observation: one order from the earlier platform export.
- Main role: historical demand, growth baseline and pre-migration patterns.
- Used in notebooks: NB01.
- Sample file: `data/sample/orders_old_platform_sample.csv`.

### `orders_new_platform.csv`

- Unit of observation: one order from the newer platform export.
- Main role: main order-level source for demand, cancellations, geography,
  wait time and model features.
- Used in notebooks: NB01, NB02, NB03, NB04, NB06.
- Sample file: `data/sample/orders_new_platform_sample.csv`.

### `drivers.csv`

- Unit of observation: one driver profile or performance row.
- Main role: driver activity, cancellation behaviour, value concentration,
  survival and churn features.
- Used in notebooks: NB02, NB03, NB06.
- Sample file: `data/sample/drivers_sample.csv`.

### `clients.csv`

- Unit of observation: one client account row.
- Main role: customer lifecycle, account-level order counts, bonus flag and
  user-segment proxies.
- Used in notebooks: NB04, NB06.
- Sample file: `data/sample/clients_sample.csv`.

The old and new order exports come from different platform periods. The
notebooks therefore avoid assuming that every field is perfectly comparable
across both files. Where definitions differ, the analysis uses common fields
such as order date, status, area, distance and successful order indicators.

## File Structure

### `orders_old_platform.csv`

Purpose: historical order activity before the current platform export.

Expected format:

- Semicolon-separated CSV.
- `latin-1` encoding.
- Order-level rows.
- Date, status, area and basic trip fields are used for historical demand and
  growth analysis.

Typical field groups:

- Order identifier and status.
- Creation or trip timestamps where available.
- Pickup and destination areas.
- Distance and trip structure fields.
- Driver and client reference fields where available.

Main analytical fields:

| Field | Use in the analysis |
|---|---|
| `order_id` | Counting orders and checking duplicates |
| `order_status` | Separating completed, cancelled and other trips |
| `created_at` | Historical demand and growth analysis |
| `pickup_time` | Timing context where the field is available |
| `accepted_at` | Driver acceptance timing where the field is available |
| `origin` / `destination` | Route and area context |
| `trip_value` | Aggregate or relative trip-value analysis |
| `trip_distance` | Trip-structure analysis |
| `service_class` | Tariff or service category |
| `passenger_reference` | Internal join or account reference, not shown in saved outputs |
| `driver_reference` | Internal driver reference, not shown in saved outputs |

Main use:

- Growth trajectory.
- Early demand baseline.
- Comparison with the newer platform period.

### `orders_new_platform.csv`

Purpose: main operational order export used in most analyses.

Expected format:

- Semicolon-separated CSV.
- `windows-1251` encoding.
- Decimal comma in numeric fields.
- Order-level rows.

Typical field groups:

- Order identifier and current status.
- Creation, arrival, trip start and completion timestamps.
- Client and driver reference fields.
- Pickup, intermediate and destination addresses or areas.
- Tariff, distance and trip value fields.
- Payment, commission and operational accounting fields.

Main analytical fields:

| Field | Use in the analysis |
|---|---|
| `order_id` | Counting orders and joining order-level records |
| `order_status` | Completed, cancelled or other order outcome |
| `created_at` | Demand, seasonality and forecasting |
| `requested_at` | Requested order time where available |
| `driver_arrived_at` | Wait-time analysis |
| `trip_started_at` | Wait-time and trip-flow checks |
| `completed_at` | Completion timing and lifecycle features |
| `client_reference` | Internal client reference, not shown in saved outputs |
| `driver_reference` | Driver-level joins and driver activity features |
| `pickup_address` / `destination_address` | Route context and address-level diagnostics |
| `pickup_area` / `destination_area` | Geography and demand-supply analysis |
| `tariff` | Tariff category |
| `trip_distance_km` | Trip-distance and trip-structure analysis |
| `trip_value` | Value-related analysis, shown only through indexes or ratios |
| `driver_commission` | Commission context, shown only in aggregate or relative form |
| `payment_components` | Payment-channel context where needed |

Important parsing notes:

- The creation timestamp is parsed with day-month-year and hour-minute format.
- Trip value and trip distance use decimal comma in the source export.
- Completed and cancelled trips are identified from the platform status text.

Main use:

- Demand and seasonality analysis.
- SARIMA forecasting.
- Wait-time analysis where timestamps are available.
- Geography and area-level demand diagnostics.
- Cancellation modelling.
- Customer lifecycle and first-trip return features.
- Driver churn trend features.

### `drivers.csv`

Purpose: driver-level profile and performance export.

Expected format:

- Semicolon-separated CSV.
- `windows-1251` encoding.
- Decimal comma in numeric fields.
- Driver-level rows.

Typical field groups:

- Driver name and callsign.
- Completed, cancelled and total order counts.
- Efficiency and online time.
- Aggregated trip value and commission fields.
- Payment component fields.

Main analytical fields:

| Field | Use in the analysis |
|---|---|
| `driver_reference` | Internal join key between driver and order exports |
| `callsign` | Dispatch or operational driver identifier |
| `completed_orders` | Driver activity and value concentration |
| `cancelled_orders` | Driver cancellation profile |
| `unpaid_orders` | Operational quality context where available |
| `total_orders` | Cancellation rate and activity denominators |
| `efficiency` | Driver productivity feature |
| `hours_online` | Productivity, survival and churn features |
| `driver_value` | Relative driver value indexes and shares |
| `driver_commission` | Commission context in aggregate or relative form |
| `payment_components` | Payment-channel context where needed |

Important parsing notes:

- Driver names are used only for internal joins between driver and order exports.
- Online time is parsed from text such as hours and minutes into numeric hours.
- Monetary fields are used to construct relative value indexes in saved outputs.

Main use:

- Driver cancellation profile.
- Driver positioning and risk categories.
- Driver value concentration.
- Driver survival and churn prediction.
- Driver risk matrix.

### `clients.csv`

Purpose: client-level account export.

Expected format:

- Semicolon-separated CSV.
- `windows-1251` encoding.
- Client-level rows.
- Many balance columns are sparse because the platform export contains a broad
  multi-currency schema.

Typical field groups:

- Client name and contact fields.
- Successful and unsuccessful order counts.
- Bonus balance fields.
- Account metadata fields.

Main analytical fields:

| Field | Use in the analysis |
|---|---|
| `client_reference` | Internal account reference, not shown in saved outputs |
| `phone_prefix` | Aggregate local, tourist SIM or international proxy |
| `birth_date` | Profile field, not used for individual-level output |
| `email_reference` | Internal contact field, not shown in saved outputs |
| `city` | Account city field where available |
| `account_activity` | Platform account activity flag or status |
| `successful_orders` | Customer lifecycle and value analysis |
| `unsuccessful_orders` | Account activity context |
| `balance_fields` | Sparse platform balance fields, not shown as raw values |
| `bonus_balance_fields` | Bonus-user flag and relative bonus-program analysis |

Important parsing notes:

- Names, phone numbers and email fields are not printed in saved outputs.
- Phone prefixes are used only to create aggregate user-type proxies such as
  local, tourist SIM and international users.
- Bonus balance is converted to a binary or relative feature, not shown as a raw
  account value.

Main use:

- Customer account activity.
- Tourist versus local segmentation.
- First-trip and lifecycle interpretation.
- Relative customer lifetime value analysis.

## Common Derived Fields

The notebooks create derived fields rather than relying only on raw export
columns.

| Derived field | Source | Meaning |
|---|---|---|
| `date` | order creation timestamp | Standard datetime field for temporal analysis |
| `is_completed` | order status | Completed-trip indicator |
| `is_cancelled` | order status | Cancelled-trip indicator |
| `driver_name` | driver field in orders | Internal join key for driver-level analysis |
| `cancel_rate` | driver or order counts | Share of cancelled orders |
| `trips_per_day` | completed trips and tenure | Driver activity intensity |
| `days_since_last` | last completed trip | Churn-related inactivity measure |
| `value_index` | trip or driver value field | Relative value measure with median-based scaling |
| `ltv_index` | successful orders and trip value | Relative customer value measure |
| `user_type` | phone prefix | Aggregate local, tourist SIM or international proxy |

The saved outputs prefer indexes, shares and ratios for value-related fields.
This keeps the analytical meaning visible without publishing absolute company
financial values.

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

df_drivers = pd.read_csv(
    "../data/raw/drivers.csv",
    sep=";",
    encoding="windows-1251",
)

df_clients = pd.read_csv(
    "../data/raw/clients.csv",
    sep=";",
    encoding="windows-1251",
    low_memory=False,
)
```

After loading, the notebooks parse platform-native date, distance and value
columns into analytical variables such as `date`, `trip_distance_km`,
`trip_value`, `is_completed` and `is_cancelled`.

To inspect the sample files:

```python
import pandas as pd

sample_new = pd.read_csv(
    "../data/sample/orders_new_platform_sample.csv",
    sep=";",
)
```

The sample files use UTF-8 for readability on GitHub. The original platform
exports use the encodings shown in the loading example above.

## Data Quality Notes

- The data are operational exports, not a research survey.
- Some timestamp fields are missing or unavailable for part of the historical
  period.
- The old and new platform exports do not have identical schemas.
- Customer accounts may contain duplicates or incomplete profile fields.
- Phone-prefix segmentation is a proxy and should be interpreted carefully.
- Driver-level exports are partly cross-sectional, so churn analysis combines
  profile data with order timelines.
- Area names and address fields may contain platform-specific spelling or
  grouping differences.

These limitations are reflected in the notebook interpretations and in the
thesis limitations section.

## Data Access Rules

- Original source records are not committed.
- Real names, phone numbers and emails are not committed.
- Credentials, system URLs and billing identifiers are not committed.
- Absolute company financial outputs are not shown in saved notebook outputs.
- Value-related results are shown as indexes, shares, percentages or ratios.
- Synthetic sample files are included only to demonstrate schema and parsing
  expectations.
- The notebooks are kept as code and methodological documentation for academic
  review.
