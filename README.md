# AI Ops Command Center — Tower Load Forecast → CNPS Impact (Demo)

This repository demonstrates an end-to-end AI solution for operations:
**ticket telemetry → capacity/load forecasting → detractor risk estimation → interactive stakeholder dashboard.**

> Important: **ML model training runs locally** (Python).  
> The GitHub Pages site is a **demo dashboard** that reads sanitized CSV outputs (no server-side compute).

## North Star metric
**North Star:** Improve experience outcomes by reducing detractor risk and improving CNPS over time.  
Operationally, the dashboard uses two leading indicators:
1) **Tower Load Index (TLI)**: a capacity stress signal per tower-month  
2) **Predicted detractor risk**: probability that experience degrades given operational conditions

## Why these ML models?
This solution uses gradient-boosted trees (e.g., XGBoost) as the practical baseline for tabular operational data:
- Works well with non-linear relationships and interactions common in ticketing operations
- Handles mixed feature types (after one-hot encoding for categories)
- Provides feature importance for governance narratives and explainability

## Data privacy & sanitization
The public dataset is sanitized:
- Removed direct identifiers (e.g., requestor/owner IDs)
- Reduced ticket dates to month-level granularity
- Bucketized aging signal (“Days Open Bucket”) to reduce re-identification risk

## What’s in GitHub Pages?
The GitHub Pages dashboard (`index.html`) is a single-file, interactive product-style UI:
- Tower drilldowns
- CNPS score trend (North Star proxy)
- Detractor risk trend
- TLI observed + forecast
- Scenario simulation (demo): reducing aging backlog → reduced TLI → lower risk

## How to run ML locally (high-level)
1) Start from `sanitized_sample.csv`
2) Build tower-month aggregates (tickets, p90 aging, CNPS score)
3) Compute **TLI** from weighted operational signals
4) Train:
   - **TLI forecast model** (regression using lag features)
   - **CNPS detractor risk model** (classification producing risk probabilities)
5) Export results to:
   - `outputs/tower_month_kpis.csv`
   - `outputs/tli_forecast.csv`
   - `outputs/cnps_risk_by_tower_month.csv`
6) Commit outputs + `index.html` and enable GitHub Pages

DEMO LINK - https://balajigopinath-pmp.github.io/ai-ops-command-center/

## Hosting
- GitHub Pages hosts static files only, so training is not executed on the site.
- The dashboard visualizes exported results for a clean, shareable portfolio artifact.

## About
Balaji Gopinath, PMP, CSM  
Portfolio: https://www.balajigopinath.work

Focus: Implementing AI in program governance and operational excellence—turning operational data into decision systems that improve reliability, stakeholder experience, and execution predictability.
