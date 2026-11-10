# Data Inventory - Week 3 Project

This document details the inventory of datasets ingested and processed within the PalmPOPT data engineering pipeline.

## Ingested Datasets

| Dataset Name | Source | File Format | Type | Description / Purpose |
| :--- | :--- | :--- | :--- | :--- |
| **Data Statistics Oil Palm 2023.pdf** | MPOB | `.pdf` | Raw Text / Tables | Contains official annual statistics on oil palm yield, production, and land areas. |
| **Laporan Tahunan MPOB 2023.pdf** | MPOB | `.pdf` | Raw Text / Report | Annual report covering macroeconomic performance, industry insights, and agronomy data. |
| **Pocket Stat Q1 Jan - Mac 2026.pdf** | MPOB | `.pdf` | Raw Text / Statistics | Quarterly statistical updates providing short-term performance indicators. |
| **weather_soil_api.csv** | Open-Meteo API | `.csv` | Raw Time-Series | Daily macroclimate data (temperature at 2m, total precipitation, and 0-7cm soil moisture) for Peninsular Malaysia. |

## Processed & Integrated Outputs

| Output File Name | Location | Format | Description |
| :--- | :--- | :--- | :--- |
| `prepared_text.jsonl` | `data/processed/` | `.jsonl` | Chunked and structured text extracted from MPOB PDF documents. |
| `prepared_timeseries.csv` | `data/processed/` | `.csv` | Aggregated daily climate and soil data over 365 days. |
| `integrated_palm_dataset.jsonl` | `data/processed/` | `.jsonl` | Integrated dataset mapping domain parameters (*Weather*, *Soil*, *Cost*, *Yield*) to chunked text. |
| `monthly_weather_summary.csv` | `data/processed/pipeline_v1/palm_analysis/` | `.csv` | Monthly aggregated climate indicators for predictive modeling (Part C output). |