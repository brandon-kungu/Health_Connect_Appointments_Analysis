# HealthConnect Clinic: Reducing Patient Appointment No-Shows

## AnalystLab Africa Experience Lab (Data Analytics Track)

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
  * `HealthConnect_Week7_Validation_Tables.xlsx`: Week 7 validation tables and sensitivity matrix[cite: 13]
* **`notebooks/`**
  * `week4_healthconnect_analysis.ipynb`: Week 4 exploratory data quality and hypothesis notebook[cite: 4]
  * `week5_healthconnect_analytics.ipynb`: Week 5 comprehensive analysis, KPIs and visual dashboard[cite: 5]
  * `week6_healthconnect_advanced_analytics.ipynb`: Week 6 advanced segmentation, risk tiers and simulations[cite: 7]
  * `week7_healthconnect_testing_validation.ipynb`: Week 7 hypothesis testing, segment validation and sensitivity analysis[cite: 13]
* **`visuals/`**
  * `healthconnect_week5_dashboard_clean.png`: Week 5 4-panel operational analytics dashboard
  * `healthconnect_week6_decision_support.png`: Week 6 advanced decision-support dashboard[cite: 7]
  * `healthconnect_week7_validation_testing.png`: Week 7 testing, KPI validation and sensitivity dashboard[cite: 13]
* **`docs/`**
  * `week4_handoff.md`: Week 4 to Week 5 transition and decisions log[cite: 4]
  * `week5_project_summary.md`: Week 5 execution report, cross-track notes and recommendations[cite: 5]
  * `week6_project_summary.md`: Week 6 advanced analytics, cross-track integration and testing plan[cite: 7]
  * `week7_project_summary.md`: Week 7 testing evidence, validation matrix and Week 8 readiness assessment[cite: 13]
* **`README.md`**: Project documentation and milestone tracker[cite: 5, 7, 13]

---

## Project Execution and Milestone Progress

### Week 4: Problem Formulation and Data Hygiene
* **Data Scale:** 5,000 appointment records representing 1,696 unique adult patients (48.5% No-Show, 46.3% Attended, 5.3% Cancelled)[cite: 1, 2].
* **Hygiene and Validation:** Categorized 1,366 blank entries in `reminder_channel` as "Not Applicable"[cite: 1, 4]. Imputed minor missing values in distance (90 rows) and wait time (60 rows) with median values[cite: 1, 4]. Verified zero duplicate primary keys and checked bounds (`previous_no_shows <= previous_appointments`)[cite: 1, 2].

### Week 5: Exploratory Analysis, KPI Development and Baseline Visualisation
* **Controlled EDA:** Disproved the hypothesis that wait times drive attendance (mean wait times are identical at ~24.2 min)[cite: 2]. Showed that reminder lift is risk-dependent[cite: 1].
* **KPI Quantifications:** Calculated Lead Time Band No-Show Rate (24.8% to 60.5%), Prior History Band No-Show Rate (43.5% to 68.8%), Distance Band No-Show Rate (46.5% to 57.8%), and Channel Performance (SMS outperforming at 45.8%)[cite: 1, 2].

### Week 6: Advanced Analytics, Decision Support and Cross-Track Integration
* **2D Compounding Risk Matrix:** Demonstrated that no-show probability reaches 81.0% when bookings made >30 days out intersect with patients having 3+ prior misses[cite: 1].
* **Composite Risk Stratification (Tiers 1–4):** Mapped clinic population into 4 actionable risk profiles; proved that reminder lift is concentrated in Tier 3 (High Risk: +6.85 pp)[cite: 1].
* **Operational Capacity Simulations:** Modeled Policy A (14-day booking cap: saves 782 slots, reducing no-shows to 32.8%) and Combined Reform (saves 1,048 slots, reducing no-shows to 27.5%)[cite: 1].
* **Cross-Track Integration:** Provided the Data Science track with `HealthConnect_Week6_Enriched.csv` containing interaction terms and confirmed pruning of `waiting_time_minutes`[cite: 2, 7].

### Week 7: Testing, Refinement and End-to-End Validation
* **Hypothesis Testing:** Conducted Chi-Square tests of independence confirming that lead time ($p = 4.40 \times 10^{-68}$) and prior history ($p = 2.32 \times 10^{-17}$) are statistically significant causal drivers[cite: 1, 2]. Validated that reminder lift is statistically significant in Tier 3 ($p = 0.020$), but non-significant in Tier 1 and Tier 4[cite: 1].
* **Segment Stability Testing:** Demonstrated that lead time decay is invariant across all clinical appointment types (General, Follow-up, Specialist, Diagnostic) and genders[cite: 2].
* **Sensitivity Stress-Testing:** Tested Policy A across compliance levels (25%, 50%, 75%, 100%), proving that 391 slots are recovered even at conservative 50% adoption (lowering no-shows to 40.64%).
* **Refined Policy Insight:** Advised clinic leadership to restrict two-way SMS reminders to Tier 2 and Tier 3 cohorts, preserving attendance gains while cutting notification messaging costs by ~60%[cite: 1].
* **HC-POD Model Validation:** Verified that Data Science tuned classification models correctly incorporate lead time $\times$ history interaction terms, aligning with empirical risk tier baselines[cite: 13].

---

## Actionable Business Recommendations

1. **Enact a 14-Day Rolling Booking Window:** Restrict open advance scheduling or require mandatory 48-hour digital confirmations for distant appointments to eliminate the 60.5% default rate on long-lead bookings[cite: 1, 2].
2. **Deploy Selective Algorithmic Overbooking:** Apply double-booking buffers exclusively to slots reserved by Tier 3 and Tier 4 patients (≥2 prior misses) to protect provider utilization without overburdening clinical staff[cite: 1].
3. **Route Long-Distance Patients to Telehealth:** Automatically divert routine follow-up consultations to virtual care for patients residing >20 km away to address the 57.8% transit friction barrier[cite: 1, 2].
4. **Target Automated Two-Way SMS:** Concentrate reminder budgets on Tier 2 and Tier 3 cohorts using SMS with interactive "Confirm / Reschedule" reply triggers[cite: 2].

---

## Tools and Technologies
* **Analysis and Data Pipeline:** Python 3 (Pandas, NumPy, SciPy)[cite: 13]
* **Visualisation and Plotting:** Matplotlib, Seaborn[cite: 13]
* **Target BI Platform:** Power BI / Tableau[cite: 13]
* **Version Control and Management:** Git, GitHub[cite: 13]* Git, GitHub[cite: 7]
