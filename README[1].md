# Weather Data Visualizer

Terminal app (Python 3.10+) to load weather CSV data, validate entries, search, summarise,
plot temperature/rainfall trends (Matplotlib) and export reports.

## Quick start
```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt  # only needed for charts
python main.py
```
First launch seeds `data/weather_data.json` from `data/sample_weather.csv` (44 rows incl. edge cases).
Run tests: `python -m unittest discover tests -v`

## Features (mapped to the brief)
| Brief requirement | Where |
|---|---|
| Menu-driven terminal UI (ANSI colour; set `NO_COLOR=1` to disable) | `weather/cli.py` |
| Defensive validation (date, city, ranges, NaN/inf, blank) | `weather/validation.py` |
| Core logic: load CSV, stats, trend detection | `weather/analytics.py`, `storage.py` |
| JSON persistence, atomic writes, corrupt-file recovery | `weather/storage.py` |
| Keyword / city / date-range search | menu 3 |
| Executive summary (avg, min/max, totals, monthly, per city, trend) | menu 4 |
| Matplotlib charts (trend line, monthly rainfall, histogram) -> `output/` | menu 5 |
| Export Markdown, TXT audit log, CSV | menu 6 |
| Bulk CSV import with row-by-row error log | menu 7 (try `data/messy_import_demo.csv`) |
| Threshold warnings (heat >= 40 C, freeze <= 0 C, rain >= 100 mm) | menu 8 + on add |

## Suggested demo script
1. Launch -> banner and menu. 2. Option 2: enter `abc`, `99`, `2025-02-30` to show validation
catching errors, then a valid entry (try 45 C for a warning). 3. Option 4 summary, option 5 charts.
4. Option 7 with `data/messy_import_demo.csv` to show the error log.
5. Exit (0), relaunch, option 1 -> data persisted. 6. Option 6 export.

## Layout
```
main.py            entry point
weather/           models, validation, storage, analytics, plotting, export, cli
data/              sample_weather.csv/.json, messy_import_demo.csv
tests/             unit tests
output/            generated charts and reports
```
Ideas for next steps: Tkinter/Textual front-end, delete/edit records, live weather API with mock-cache fallback.
