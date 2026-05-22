# Mini Monte Carlo

A local Python data observability tool that monitors a fake orders dataset for quality issues and alerts on anomalies.

## Install

```bash
pip install pandas numpy faker schedule
```

## Generate clean data

```bash
python generate_data.py
```

## Run the monitor once

```bash
python monitor.py
```

## Simulate a broken pipeline

Edit `generate_data.py` and call `generate_data(break_it=True)` or modify the `if __name__ == "__main__"` block to use `break_it=True`, then run:

```bash
python generate_data.py
python monitor.py
```

## Files

- `generate_data.py` — creates fake order data and writes `data/orders.csv`.
- `monitor.py` — reads the CSV, saves metadata snapshots, and alerts on issues.
- `alerts.py` — formats alert output for terminal visibility.
- `lineage.py` — maps data sources to downstream systems and prints impacted targets.
- `data/orders.csv` — generated sample dataset (do not create manually).
- `meta.db` — SQLite snapshot history file created automatically.

## Expected alerts when `break_it=True`

- Row count anomaly due to reduced volume.
- Schema change alert for removed `customer` column.
- NULL spike alert for `amount` with more than 20% null values.

## Notes

- The scheduler is included in `monitor.py` but commented out by default.
- All checks run locally with `pandas`, `numpy`, `faker`, and `schedule`.
