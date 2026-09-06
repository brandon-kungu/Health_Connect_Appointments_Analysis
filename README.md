# HealthConnect Clinic: Reducing Patient Appointment No-Shows

## AnalystLab Africa Experience Lab - Data Analytics

### Project Overview
HealthConnect Clinic is an outpatient healthcare provider managing appointment-based services that experiences a critical attendance deficit (48.5% no-show rate across 5,000 scheduled visits)[cite: 1, 2, 5]. This project applies structured data analytics to identify the primary drivers of missed appointments, establish measurable Key Performance Indicators (KPIs), resolve behavioral anomalies, and provide actionable operational recommendations to reclaim clinical slot capacity[cite: 1, 5].

---

### Project Structure

* **`data/`**
  * `HealthConnect_Appointment_Data.csv`: Raw, untouched appointment records (5,000 rows)
  * `HealthConnect_Data_Dictionary.xlsx`: Variable definitions and schema metadata
  * `HealthConnect_Appointment_Data_cleaned.csv`: Week 4 cleaned baseline (imputed and recoded)
  * `HealthConnect_Week5_Prepared.csv`: Week 5 audited analytical dataset with ordered bins
* **`notebooks/`**
  * `week4_healthconnect_analysis.ipynb`: Week 4 exploratory data quality and hypothesis notebook
  * `week5_healthconnect_analytics.ipynb`: Week 5 comprehensive analysis, KPIs and visual dashboard
* **`visuals/`**
  * `healthconnect_week5_eda_charts.png`: Exploratory distribution and subgroup plots
  * `healthconnect_week5_dashboard_clean.png`: 4-panel operational analytics dashboard
* **`docs/`**
  * `week4_initial_analysis_document.md`: Week 4 problem definition and initial findings report
  * `week4_handoff.md`: Week 4 to Week 5 transition and decisions log
  * `week5_project_summary.md`: Week 5 execution report, cross-track notes and recommendations
* **`README.md`**: Project documentation and milestone tracker

---

## Project Execution and Milestone Progress

### Week 4: Problem Formulation and Data Hygiene
* **Data Scale:** 5,000 appointment records representing 1,696 unique adult patients (48.5% No-Show, 46.3% Attended, 5.3% Cancelled)[cite: 1, 2].
* **Hygiene and Validation:**
  * Categorized 1,366 blank entries in `reminder_channel` as "Not Applicable", as they coincided with `reminder_sent == 'No'` rather than missing information[cite: 1, 4].
  * Imputed minor missing values in `distance_to_clinic_km` (90 rows, 1.8%) and `waiting_time_minutes` (60 rows, 1.2%) using median substitution, preserving boolean `_was_missing` indicator flags[cite: 1, 4].
  * Verified zero primary key duplicates and checked historical bounds (`previous_no_shows <= previous_appointments`)[cite: 1, 2].
* **Core Discovery:** Identified booking lead time and patient non-attendance history as dominant signals; noted a flat aggregate reminder effect (47.4% vs. 51.4%) as an open investigation question for Week 5[cite: 1, 4].

### Week 5: Exploratory Analysis, KPI Development and Strategic Insights
* **Data Preparation and Validation:** Confirmed strict date consistency (`booking_lead_days == appointment_date - booking_date`), zero negative lead days, standardized string categorical domains, and established ordered intervals for analysis (`lead_bucket`, `prev_ns_bucket`, `dist_bucket`).
* **Controlled EDA and Resolving the Reminder Paradox:**
  * **Confounding Variable Resolution:** While reminders showed only an aggregate ~4% lift, controlling for patient risk tiers revealed a **9.8% to 10.2% drop in no-shows** when reminders are delivered to patients with 2 or 3+ prior missed appointments[cite: 1].
  * **Operational Wait Times:** Evaluated queue durations and found identical average wait times between Attended (24.3 min) and No-Show (24.2 min) appointments, disproving post-arrival queue friction as a driver of no-shows.
* **Formal KPI Framework:**
  * **KPI 1 (No-Show Rate by Lead Time Band):** Monotonically escalates from **24.8%** (0–3 days) to **60.5%** (31–60 days)[cite: 1, 2]. Over 48% of clinic appointments are booked >30 days in advance[cite: 2].
  * **KPI 2 (No-Show Rate by Prior No-Show Count):** Scales from **43.5%** for patients with zero prior misses to **68.8%** for those with 3+ previous no-shows[cite: 1, 2].
  * **KPI 3 (No-Show Rate by Transit Distance Band):** Remains relatively stable under 20 km (46.5%–49.4%), surging to **57.8%** beyond the 20 km threshold[cite: 1, 2].
  * **KPI 4 (Reminder Channel Efficacy):** **SMS** achieves the best performance with a **45.8%** no-show rate, outperforming Email (48.4%) and WhatsApp (49.8%)[cite: 2].
* **Dashboard Visualisation:** Designed and rendered an integrated 4-panel operational analytics dashboard in Python (Matplotlib/Seaborn) with ordered categorical factors[cite: 5].
* **Cross-Track Collaboration:** Transferred high-signal predictive features (`lead_bucket`, `prev_ns_bucket`) and target separation protocols (`Cancelled` vs. `No-Show`) to the Data Science track to support baseline model training[cite: 5].

---

## Actionable Business Recommendations

1. **Implement a 14–21 Day Booking Horizon:** Restrict open scheduling windows or require mandatory re-confirmation for appointments scheduled >14 days in advance to counteract the 60.5% default rate on long horizons[cite: 1, 2].
2. **Deploy Risk-Tiered Overbooking:** Apply targeted double-booking algorithms strictly to appointment slots booked by chronic offenders (>= 2 prior no-shows) to preserve provider utilization without overburdening staff.
3. **Route Long-Distance Patients to Telehealth:** Automatically suggest virtual consultation slots for routine follow-ups when patients reside >20 km away, mitigating the transit-related attendance drop-off[cite: 1, 2].
4. **Transition to Two-Way SMS Notifications:** Prioritize SMS as the default reminder vehicle and implement interactive confirmation/cancellation triggers to reclaim slots early[cite: 2].

---

## Tools and Technologies
* **Analysis and Data Pipeline:** Python 3 (Pandas, NumPy)[cite: 5]
* **Visualisation and Plotting:** Matplotlib, Seaborn[cite: 5]
* **Target BI Platform:** Power BI / Tableau[cite: 5]
* **Version Control and Management:** Git, GitHub[cite: 5]
