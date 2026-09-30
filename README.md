# HealthConnect Clinic: Data Analytics Project

## Overview

HealthConnect Clinic is a fictional healthcare provider facing a severe patient no-show problem: 48.46% of scheduled appointments (2,423 of 5,000) go unattended. This repository documents the end-to-end Data Analytics contribution to the HealthConnect Experience Lab project, part of the AnalystLab Africa Experience Lab Internship Programme, covering Weeks 4 through 8.

**Project question:** How can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?

## Project Journey

| Week | Stage | Output |
|---|---|---|
| Week 4 | Problem Understanding & Data Quality | Initial analysis document, dataset overview, 4 core KPI definitions |
| Week 5 | Initial Implementation | Univariate EDA, operational dashboard (4-panel) |
| Week 6 | Advanced Analytics & Integration | 2D risk matrix, composite risk tiers, policy simulations, decision-support dashboard |
| Week 7 | Testing & Validation | Chi-square hypothesis testing, sensitivity analysis, subgroup stability checks |
| Week 8 | Final Integration & Presentation | Executive decision-support package, cross-track integration, final video presentation |

## Repository Structure
data/

├── HealthConnect_Appointment_Data.csv # Raw source data (5,000 rows, 18 columns)

├── HealthConnect_Data_Dictionary.xlsx # Metadata and attribute specifications

├── HealthConnect_Appointment_Data_cleaned.csv # Week 4 cleaned baseline

├── HealthConnect_Week5_Prepared.csv # Week 5 dataset with ordered categoricals

├── HealthConnect_Week6_Enriched.csv # Primary dataset with composite risk_tier

└── HealthConnect_Week7_Validation_Tables.xlsx # Sensitivity matrix and segment cross-tabs


notebook/[2 notebooks] healthconnect_analysis.ipynb and Documentation.ipynb


visuals/
├── healthconnect_week5_dashboard_clean.png

├── healthconnect_week6_decision_support.png # Final decision-support dashboard

└── healthconnect_week7_validation_testing.png


docs/
├── week4_initial_analysis_document.md


├── week5_project_summary.md

├── week6_project_summary.md

├── week7_project_summary.md

└── week8_healthconnect_final_report.md # Final analytics and decision support package



## Key Findings

- **Booking lead time** is the strongest behavioral driver of no-shows. Rates climb from 24.84% (0 to 3 days out) to 60.49% (31 to 60 days out).
- **Prior no-show history** compounds risk, rising from 43.51% (no history) to 68.82% (3+ prior misses).
- **Distance to clinic** is a non-linear barrier: flat under 20km, then surging past it.
- **Reminders only work for one risk segment.** There's a statistically significant lift only for Tier 3 (High Risk) patients (p = 0.020), with no measurable effect for Tiers 1, 2, or 4.
- **Combined policy reform** (14-day booking cap plus targeted overbooking) projects reclaiming 1,048 patient slots, cutting the no-show rate from 48.46% to 27.50%.

## Methodology Notes

- Cancellations (5.26% of records) are treated as administrative releases rather than lost capacity, and are excluded from the no-show definition.
- `waiting_time_minutes` was tested and pruned from attendance analysis due to no correlation with outcome.
- Missing values in `distance_to_clinic_km` and `waiting_time_minutes` are median-imputed with `_was_missing` boolean flags.

## Tools

Python, Pandas, Seaborn/Matplotlib, SciPy (chi-square testing)

## Author

Brandon, Data Analytics Track, AnalystLab Africa Experience Lab
