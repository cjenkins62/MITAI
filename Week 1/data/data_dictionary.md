# Data Dictionary — Uber NYC TLC Pickups

**Source:** [FiveThirtyEight Uber TLC FOIL response](https://github.com/fivethirtyeight/uber-tlc-foil-response)  
**Files in this folder:** `uber-raw-data-apr14.csv` through `uber-raw-data-sep14.csv`  
**Grain:** One row per Uber pickup event  
**Coverage:** April–September 2014, New York City  
**Last updated:** 2026-08-06

---

## Raw columns

| Raw column | Analysis name | Type | Description | Valid range / notes |
|------------|---------------|------|-------------|---------------------|
| `Date/Time` | `pickup_time` | datetime | Timestamp of pickup | Format `M/D/YYYY H:MM:SS`; parse with `pd.to_datetime(..., errors="coerce")` |
| `Lat` | `lat` | float | Pickup latitude (WGS84) | NYC metro ~40.5–41.0; drop nulls; investigate outliers |
| `Lon` | `lon` | float | Pickup longitude (WGS84) | NYC metro ~-74.3 to -73.7; drop nulls; investigate outliers |
| `Base` | `base` | categorical | TLC dispatch base code | 5 bases in April 2014 (e.g. `B02512`, `B02682`); do not impute |

---

## Derived features (analysis dataset)

| Column | Type | Description | Source |
|--------|------|-------------|--------|
| `hour` | int | Hour of day (0–23) | `pickup_time.dt.hour` |
| `day_of_week` | categorical | Day name (Monday–Sunday) | `pickup_time.dt.day_name()` |
| `date` | date | Calendar date | `pickup_time.dt.date` |
| `month` | string | Year-month (`2014-04`) | `pickup_time.dt.to_period("M")` — used for multi-month comparison |

---

## KPI linkage

| KPI | How to compute | Primary columns |
|-----|----------------|-----------------|
| Pickups per hour | `groupby(["date", "hour"]).size()` | `pickup_time` |
| Pickups per day | `groupby("date").size()` | `pickup_time` |
| Peak-hour demand | Max of hourly pickup counts | `pickup_time` |
| Demand by base | `groupby("base").size()` | `base` |
| Weekday vs weekend | Compare counts by `day_of_week` | `pickup_time` |

---

## Data quality notes

- **April 2014:** No missing values in raw file; 564,516 rows.
- **Coordinates:** Never mean-impute lat/lon — drop invalid rows instead.
- **Timestamps:** Invalid dates become `NaT` after parsing; drop rather than fill.
- **Growth:** Total pickups grow ~1.8× from April to September 2014 (Uber expansion in NYC).
- **Outliers:** Some lat/lon values fall outside core NYC — investigate before mapping.

---

## File inventory

| File | Period | Rows (approx.) |
|------|--------|----------------|
| `uber-raw-data-apr14.csv` | April 2014 | 564,516 |
| `uber-raw-data-may14.csv` | May 2014 | 652,435 |
| `uber-raw-data-jun14.csv` | June 2014 | 663,844 |
| `uber-raw-data-jul14.csv` | July 2014 | 796,121 |
| `uber-raw-data-aug14.csv` | August 2014 | 829,275 |
| `uber-raw-data-sep14.csv` | September 2014 | 1,028,136 |
