# HealthConnect Clinic: Reducing Patient Appointment No-Shows

## AnalystLab Africa Experience Lab — Data Analytics Track

### Project Overview
HealthConnect Clinic is an outpatient healthcare provider managing appointment-based services that experiences a critical attendance deficit (48.5% no-show rate across 5,000 scheduled visits)[cite: 1, 5]. This project applies structured data analytics to identify the primary drivers of missed appointments, establish measurable Key Performance Indicators (KPIs), resolve behavioral anomalies, model capacity recapture policies, and provide actionable operational recommendations to reclaim clinical slot capacity[cite: 1, 5, 7].

---

### Repository Structure

* **`data/`**
  * `HealthConnect_Appointment_Data.csv`: Raw, untouched appointment records (5,000 rows)[cite: 5]
  * `HealthConnect_Data_Dictionary.xlsx`: Variable definitions and schema metadata[cite: 5]
  * `HealthConnect_Appointment_Data_cleaned.csv`: Week 4 cleaned baseline (imputed and recoded)[cite: 4]
  * `HealthConnect_Week5_Prepared.csv`: Week 5 audited analytical dataset with ordered bins
  * `HealthConnect_Week6_Enriched.csv`: Week 6 enriched dataset with risk stratification tiers[cite: 7]
* **`notebooks/`**
  * `week4_healthconnect_analysis.ipynb`: Week 4 exploratory data quality and hypothesis notebook[cite: 4]
  * `week5_healthconnect_analytics.ipynb`: Week 5 comprehensive analysis, KPIs and visual dashboard[cite: 5]
  * `week6_healthconnect_advanced_analytics.ipynb`: Week 6 advanced segmentation, risk tiers and simulations[cite: 7]
* **`visuals/`**
  * `healthconnect_week5_eda_charts.png`: Week 5 exploratory distribution and subgroup plots
  * `healthconnect_week5_dashboard_clean.png`: Week 5 4-panel operational analytics dashboard
  * `healthconnect_week6_decision_support.png`: Week 6 advanced decision-support dashboard[cite: 7]
* **`docs/`**
  * `week4_initial_analysis_document.md`: Week 4 problem definition and initial findings report[cite: 4]
  * `week4_handoff.md`: Week 4 to Week 5 transition and decisions log[cite: 4]
  * `week5_project_summary.md`: Week 5 execution report, cross-track notes and recommendations[cite: 5]
  * `week6_project_summary.md`: Week 6 advanced analytics, cross-track integration and testing plan[cite: 7]
* **`README.md`**: Project documentation and milestone tracker[cite: 5, 7]

---

## Project Execution and Milestone Progress

### Week 4: Problem Formulation and Data Hygiene
* **Data Scale:** 5,000 appointment records representing 1,696 unique adult patients (48.5% No-Show, 46.3% Attended, 5.3% Cancelled)[cite: 1, 2].
* **Hygiene and Validation:**
  * Categorized 1,366 blank entries in `reminder_channel` as "Not Applicable", as they coincided with `reminder_sent == 'No'` rather than missing information[cite: 1, 4].
  * Imputed minor missing values in `distance_to_clinic_km` (90 rows, 1.8%) and `waiting_time_minutes` (60 rows, 1.2%) using median substitution, preserving boolean `_was_missing` indicator flags[cite: 1, 4].
  * Verified zero primary key duplicates and checked historical bounds (`previous_no_shows <= previous_appointments`)[cite: 1, 2].
* **Core Discovery:** Identified booking lead time and patient non-attendance history as dominant signals; noted a flat aggregate reminder effect (47.4% vs. 51.4%) as an open investigation question for Week 5[cite: 1, 4].

### Week 5: Exploratory Analysis, KPI Development and Baseline Visualisation
* **Data Preparation Audit:** Confirmed strict calendar date consistency (`booking_lead_days == appointment_date - booking_date`), zero negative lead days, standardized string categorical domains, and established ordered intervals for analysis (`lead_bucket`, `prev_ns_bucket`, `dist_bucket`).
* **Controlled EDA & Resolving the Reminder Paradox:**
  * **Confounding Variable Resolution:** While reminders showed only an aggregate ~4% lift, controlling for patient risk tiers revealed a **9.8% to 10.2% drop in no-shows** when reminders are delivered to patients with 2 or 3+ prior missed appointments[cite: 1].
  * **Operational Wait Times:** Evaluated queue durations and found identical average wait times between Attended (24.3 min) and No-Show (24.2 min) appointments, disproving post-arrival queue friction as a driver of no-shows[cite: 2].
* **Formal KPI Framework:**
  * **KPI 1 (No-Show Rate by Lead Time Band):** Monotonically escalates from **24.8%** (0–3 days) to **60.5%** (31–60 days)[cite: 1, 2]. Over 48% of clinic appointments are booked >30 days in advance[cite: 2].
  * **KPI 2 (No-Show Rate by Prior No-Show Count):** Scales from **43.5%** for patients with zero prior misses to **68.8%** for those with 3+ previous no-shows[cite: 1, 2].
  * **KPI 3 (No-Show Rate by Transit Distance Band):** Remains relatively stable under 20 km (46.5%–49.4%), surging to **57.8%** beyond the 20 km threshold[cite: 1, 2].
  * **KPI 4 (Reminder Channel Efficacy):** **SMS** achieves the best performance with a **45.8%** no-show rate, outperforming Email (48.4%) and WhatsApp (49.8%)[cite: 2].
* **Dashboard Visualisation:** Designed and rendered an integrated 4-panel operational analytics dashboard in Python (Matplotlib/Seaborn) with ordered categorical factors[cite: 5].

### Week 6: Advanced Analytics, Decision Support and Cross-Track Integration
* **2D Risk Matrix Modeling:**
  * Evaluated the compounding interaction between **Booking Lead Time** and **Prior No-Show History**[cite: 1, 7].
  * Quantified the spectrum from the lowest risk cell (0–3 days + 0 prior misses: **17.1% no-show rate**, N=181) to the critical default zone (31–60 days + 3+ prior misses: **81.0% no-show rate**, N=42)[cite: 1].
* **Composite Patient Risk Stratification (Tiers 1–4):**
  * Synthesized multi-factor behavioral, operational, and geospatial friction into 4 operational tiers[cite: 1, 7]:
    * **Tier 1 - Low Risk (N=726):** **25.9%** no-show rate; reminders produce negligible lift (**0.35 pp**).
    * **Tier 2 - Moderate Risk (N=2,497):** **46.1%** no-show rate (50% of clinic traffic); reminders yield **3.44 pp lift**.
    * **Tier 3 - High Risk (N=1,466):** **58.4%** no-show rate; reminders deliver their highest ROI (**6.85 pp lift**)[cite: 1].
    * **Tier 4 - Critical Risk (N=311):** **73.3%** no-show rate; passive reminders plateau (**1.11 pp lift**), necessitating structural policy changes[cite: 1].
* **Operational Capacity Recapture Simulation:**
  * **Policy A (14-Day Booking Horizon Cap):** Reclaiming distant slot attrition recaptures **782 appointment slots**, lowering clinic-wide no-shows from **48.5% to 32.8%**[cite: 1].
  * **Policy B (Targeted 15% Overbooking on Tiers 3 & 4):** Recovers **266 appointment slots**, reducing overall no-shows to **43.1%**[cite: 1].
  * **Combined Policy Reform (A + B):** Recaptures **1,048 patient slots**, reducing clinic-wide no-show rate to **27.5%**.
* **Decision-Support Visual Dashboard (2.0):** Built and exported `healthconnect_week6_decision_support.png` featuring the 2D Heatmap, Tier Volume Distribution, Reminder Sensitivity, and Policy Simulation[cite: 7].
* **Mandatory Cross-Track Integration (Data Analytics → Data Science):**
  * Provided the Data Science track with `HealthConnect_Week6_Enriched.csv` containing engineered risk tiers and interaction terms (`lead_days * prior_no_shows`)[cite: 7].
  * Advised on target separation (isolating 263 `Cancelled` rows from binary default targets) and confirmed the pruning of `waiting_time_minutes` due to zero signal[cite: 2, 7].

---

## Actionable Business Recommendations

1. **Enact a 14-Day Rolling Booking Window:** Restrict open advance scheduling or require mandatory 48-hour digital confirmations for distant appointments to eliminate the 60.5% default rate on long-lead bookings[cite: 1, 2].
2. **Deploy Selective Algorithmic Overbooking:** Apply double-booking buffers exclusively to slots reserved by Tier 3 and Tier 4 patients (≥2 prior misses) to protect provider utilization without overburdening clinical staff[cite: 1].
3. **Route Long-Distance Patients to Telehealth:** Automatically divert routine follow-up consultations to virtual care for patients residing >20 km away to address the 57.8% transit friction barrier[cite: 1, 2].
4. **Target Automated Two-Way SMS:** Concentrate reminder budgets on Tier 2 and Tier 3 cohorts using SMS with interactive "Confirm / Reschedule" reply triggers[cite: 2].

---

## Tools and Technologies
* **Analysis and Data Pipeline:** Python 3 (Pandas, NumPy)[cite: 7]
* **Visualisation and Plotting:** Matplotlib, Seaborn[cite: 7]
* **Target BI Platform:** Power BI / Tableau[cite: 7]
* **Version Control and Management:** Git, GitHub[cite: 7]
