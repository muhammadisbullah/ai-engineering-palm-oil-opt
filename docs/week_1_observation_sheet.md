# Lab 1: Observation Sheet - PalmPOPT

## System Name
PalmPOPT — Hybrid AI-Driven Agricultural Weather Forecasting & Biomass Yield-Economic Optimization System

## Group Members
[Nama Ahli Kumpulan / Nama Anda]

---

## 1. What problem does this system solve? Who benefits?
* **Problem:** Plantation managers and palm oil mill operators face severe operational and financial volatility due to unpredictable weather patterns (rainfall fluctuations and temperature stress) affecting oil palm yields, while lacking integrated tools to forecast downstream biomass valorization (EFB, PKS, POME) and operational cash flow.
* **Beneficiaries:** Plantation managers, estate supervisors, palm oil mill operators, and agricultural financial analysts.

## 2. Which AI stack layer is most visible to users?
* **Layer:** Application Layer (UI Dashboard)
* **Explanation:** Users interact directly with the web dashboard displaying weather trends, yield predictions, and financial cash flow projections. The underlying data ingestion pipeline, feature engineering scripts, and machine learning regression models remain invisible behind the application interface.

## 3. Quality dimensions — at least 3, with measurement method
* **Dimension 1: Prediction Accuracy (Upstream FFB Yield)**  
  * *Measure:* Evaluated using Root Mean Square Error (RMSE) against historical harvest records to ensure errors remain below acceptable agricultural thresholds.
* **Dimension 2: System Latency**  
  * *Measure:* Measured by the time elapsed from weather API data ingestion and feature processing to the final rendering of yield and cash flow forecasts on the dashboard (target $< 3$ seconds).
* **Dimension 3: Reliability / Robustness**  
  * *Measure:* Tested by observing the pipeline's ability to handle missing weather data feeds or zero-inflation anomalies using linear interpolation without crashing.

## 4. What did the system do WELL? Give a specific example.
* **Example:** When processing multi-year meteorological data combined with soil classification logs, the automated feature engineering pipeline successfully generates 30-day and 90-day rainfall rolling averages to accurately capture water stress trends affecting fruit bunch development.

## 5. What did it do POORLY? Give a specific example.
* **Example:** During extreme, unprecedented climate anomalies (such as sudden flash floods), machine learning regression models may temporarily overestimate or underestimate immediate harvest yields due to unrecorded localized drainage capacities.

## 6. Responsible AI risks — at least 2. Who is harmed and how?
* **Risk 1 — Overestimation / Hallucination Risk:** Models trained on incomplete historical weather logs might project unrealistic yield spikes, leading plantation managers into incorrect financial budgeting and material procurement.
* **Risk 2 — Data Drift & Climate Vulnerability:** Rapid global climate shifts can cause severe data drift over time, reducing prediction accuracy and potentially misinforming long-term estate planning.

## 7. If you could fix ONE thing, what and why?
* **Fix & Reason:** Implement an automated validation guardrail that cross-references live weather anomaly alerts with real-time IoT soil sensor data to dynamically adjust yield confidence intervals before displaying financial cash flow projections to users.