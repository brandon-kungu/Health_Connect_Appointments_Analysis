# HealthConnect Clinic Experience Lab
### AnalystLab Africa Experience Lab Internship Programme, Data Analytics Track

## Project Overview

HealthConnect Clinic is a fictional healthcare provider facing a high rate of missed
appointments. This project explores how data and AI can help reduce no-shows and
improve the patient support experience. The Data Analytics track is focused on
understanding the appointment data, identifying attendance patterns, and defining
KPIs to guide the analysis.

**Central Project Question:** How can HealthConnect Clinic use data and AI to reduce
missed appointments and improve the patient support experience?

## Repository Structure

​```
healthconnect-clinic-experience-lab/
├── README.md
├── data/
│   ├── HealthConnect_Appointment_Data.csv
│   ├── HealthConnect_Data_Dictionary.xlsx
│   └── HealthConnect_Appointment_Data_cleaned.csv
├── notebooks/
│   └── week4_healthconnect_analysis.ipynb
└── docs/
    └── week4_initial_analysis_document.md
​```


## Week 4: Problem Understanding

**Objective:** Understand the HealthConnect appointment dataset and define the
business questions and KPIs that will guide deeper analysis.

**Files:**
- `data/HealthConnect_Appointment_Data.csv`, original dataset (5,000 appointment records)
- `data/HealthConnect_Data_Dictionary.xlsx`, variable definitions
- `data/HealthConnect_Appointment_Data_cleaned.csv`, cleaned dataset (missing values
  imputed and flagged, reminder_channel blanks recoded)
- `notebooks/week4_healthconnect_analysis.ipynb`, exploratory notebook
- `docs/week4_initial_analysis_document.md`, written analysis document and summary

**Key Findings:**
- Booking lead time and prior no-show history are the strongest predictors of
  no-show risk in this dataset.
- Distance to the clinic has a moderate effect, rising sharply beyond 20km.
- Reminders (sent or not, and by channel) show a surprisingly weak effect on
  attendance, worth investigating further in later stages.
- The dataset is clean overall, with only two small genuine gaps
  (distance_to_clinic_km, waiting_time_minutes).

**Proposed KPIs:**
1. No-show rate by booking lead time band
2. No-show rate by prior no-show count band
3. No-show rate by distance band
4. Reminder effectiveness rate, by channel
5. No-show rate by appointment type, time slot, and age group

**Proposed Focus for Week 5:** Calculate and visualise the five KPIs above, and begin
testing the reminder-effectiveness question more rigorously, for example by
controlling for booking lead time.

## Tools Used

- Python (Pandas, NumPy)
- Jupyter Notebook

## Author

Brandon, Data Analytics Intern, Analyst Lab Africa.
