# Synthetic Sample Data

This folder contains small synthetic CSV files for schema inspection only. The rows use test values and do not represent real passengers, drivers, trips or financial results.

The thesis results and saved notebook outputs are based on the original operational exports, not on these sample files. The sample files are included to show the field structure, separators, date formats and value formats used by the analysis.

All sample files use English field aliases for readability on GitHub. The
original platform exports use the encodings and platform-native field names
described in `../data-description.md`.

Files:

- `orders_old_platform_sample.csv`: earlier platform order export structure.
- `orders_new_platform_sample.csv`: newer platform order export structure.
- `drivers_sample.csv`: driver profile and performance export structure.
- `clients_sample.csv`: client account export structure.

All files are semicolon-separated and encoded as UTF-8.
