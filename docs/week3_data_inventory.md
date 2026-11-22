# Week 3 Data Inventory — PalmPOPT (`pipeline_v1`)

## 1. Raw / Source Inputs
- `Data Statistics Oil Palm 2023.pdf` — MPOB oil palm statistics reference report (PDF).
- `Laporan Tahunan MPOB 2023.pdf` — MPOB annual report reference document (PDF).
- `Pocket Stat Q1 Jan - Mac 2026.pdf` — MPOB Q1 2026 pocket statistics report (PDF).
- `weather_soil_api.csv` — Historical weather and soil time-series data from Open-Meteo API.

## 2. Processed & Integrated Outputs (`data/processed/pipeline_v1/palm_analysis/`)
- `prepared_text.jsonl` — Extracted and normalized text chunks/records from MPOB PDF documents.
- `prepared_timeseries.csv` — Cleaned and formatted weather/soil time-series dataset.
- `mapped_parameters_output.jsonl` — Domain-mapped PalmPOPT agronomic, milling, derivative, and biomass/waste parameters.
- `integrated_palm_dataset.jsonl` — Combined multi-source dataset integrating PDF/parameter records with time-series context.
- `week3_manifest.json` — Run metadata, file paths, record counts, and pipeline execution summary.

## 3. Planned / Pending Artifacts (Moved to Lab 4)
- `monthly_weather_summary.csv` — Monthly aggregation of weather and soil features (pending full aggregation & feature engineering in Lab 4).
