# PalmPOPT — AI-Driven Agricultural Weather Forecasting & Biomass Yield-Economic Optimization System
> An integrated AI Engineering solution that synthesizes meteorological forecasting and field-level agronomic parameters to predict upstream palm oil yields, project downstream biomass valorization output, and dynamically model operational cash flow.

---

## Problem Statement
Plantation managers and palm oil mill operators face severe financial and operational volatility due to unpredictable meteorological patterns and uncoordinated resource management. Extreme rainfall fluctuations and temperature stress directly alter Fresh Fruit Bunch (FFB) development cycles, yet field management relies heavily on static, experience-based scheduling. Furthermore, there is a lack of integrated decision-support tools that bridge the gap between upstream agricultural yield prediction, downstream biomass valorization potential (EFB, PKS, POME), and dynamic operational cash flow forecasting. AI engineering provides the optimal framework to construct an end-to-end data pipeline and decision support system that unifies real-time weather feeds, soil/chemical parameters, and machine learning models for dynamic yield and financial optimization.

---

## Proposed Solution
PalmPOPT introduces a hybrid predictive analytics platform that integrates real-time weather API feeds with agronomic field parameters (Rainfall Volume, Ambient Temperature, Soil Type, Drainage Performance, and Fertilizer/Pesticide Classifications). The solution deploys:
1. **A Data Engineering Pipeline:** Imputing missing weather values, computing rolling 30/90-day precipitation indicators, and normalizing agronomic inputs.
2. **An AI Predictive Engine:** Leveraging supervised machine learning (XGBoost / Random Forest) to forecast upstream FFB yield (Tons/Ha) and downstream biomass conversion volumes.
3. **A Techno-Economic Engine:** Translating predicted crop outputs and input material costs into dynamic cash flow projections, gross revenue, and net economic returns (RM) presented through an interactive web dashboard.

---

## Evidence of Problem
- **Evidence 1 (Yield Fluctuations & Climate Vulnerability):** Unpredictable rainfall patterns and prolonged dry or wet spells lead to significant yield variations in oil palm plantations, causing severe supply chain disruptions for downstream palm oil processing mills.
  - *Source / Citation:* Malaysian Palm Oil Board (MPOB) Annual Report & Yield Statistics Reports (2022–2024).
- **Evidence 2 (Fragmented Operational & Economic Analytics):** Conventional plantation management relies on disconnected spreadsheets for weather logging, fertilizer budgeting, and mill production tracking, making it impossible to perform dynamic financial forecasting based on real-time field parameters.
  - *Source / Citation:* Industry case studies on palm oil supply chain digitalization (SCOPUS-indexed sustainable agriculture literature, 2023).

---

## Initial Related Work / Existing Approaches
- **Study / Solution 1:** Manual Agronomic & Static Statistical Excel Models
  - *Source / Citation:* Standard plantation management record-keeping practices.
  - *Key Limitation:* Relies on historical averages; cannot process real-time weather forecasts, time-lagged precipitation interactions, or automated non-linear ML predictions.
- **Study / Solution 2:** Isolated Commercial Weather Station Monitoring Apps
  - *Source / Citation:* Agricultural IoT weather monitoring software platforms.
  - *Key Limitation:* Provides raw meteorological dashboards but lacks machine learning engines to translate weather trends into actionable downstream biomass output or net financial cash flow projections.
- **Study / Solution 3:** General-Purpose Generative AI Chatbots (e.g., ChatGPT / Claude)
  - *Source / Citation:* Commercial Foundation Models.
  - *Key Limitation:* Lack grounding in specific field-level soil/chemical data vectors, exhibit hallucination risks, and cannot execute deterministic mathematical techno-economic cash flow calculations.

---

## Engineering Gap / Limitation
Existing market approaches are either fragmented (separating weather telemetry from financial budgeting), dependent on static human estimation, or ungrounded in combined upstream-downstream agronomic data pipelines. There is a distinct technical gap in developing a unified **Data Pipeline-to-AI-to-Financial Engine** that ingests multi-source parameter streams (weather API + IoT soil/chemical logs) to predict both upstream harvest yields and downstream bio-valorization economics in real time.

---

## Project Objectives
- **O1:** To design and build an automated hybrid data pipeline that ingests meteorological forecasts (Rainfall, Temperature) and field agronomic parameters (Soil Type, Drainage, Fertilizer/Pesticide inputs).
- **O2:** To develop supervised Machine Learning models (XGBoost / Random Forest) that accurately predict upstream FFB yields and downstream biomass conversion fractions (EFB, PKS, POME).
- **O3:** To construct a techno-economic valuation module and interactive dashboard that dynamically projects operational cash flows, material OPEX, and net economic returns (RM) to assist plantation managers in decision-making.

---

## Target Users
1. **Plantation Managers & Estate Supervisors:** Planning fertilizer application schedules, irrigation/drainage interventions, and labor allocation based on weather forecast analytics.
2. **Palm Oil Mill Operators & Supply Chain Managers:** Estimating incoming raw FFB tonnage and downstream biomass processing capacity (EFB, PKS, POME valorization).
3. **Agro-Commodity Executives & Financial Analysts:** Evaluating dynamic operational cash flow forecasts, material costs (OPEX), and net financial returns.

---

## Data Sources
- **Source 1 (Meteorological Data):** Open-Meteo / Malaysian Meteorological Department API — Historical and 7-day forecast data for daily precipitation (mm) and temperature (°C).
  - *URL:* https://open-meteo.com/
- **Source 2 (Agronomic & Crop Guidelines):** MPOB Agronomic & Yield Guidelines PDF — Standard conversion factors for FFB yield rates, soil type classifications, and biomass conversion ratios.
  - *URL:* https://www.mpob.gov.my/
- **Source 3 (Material & Economic Cost Metrics):** Industry Market Price Reports — Historical price benchmarks for FFB (RM/Ton), fertilizers/pesticides (RM/Kg), and biomass by-products.

---

## Responsible AI Risks
- **Risk 1 — Hallucination / Overestimation Risk:** Machine learning models trained on incomplete weather historical data might overestimate harvest yields during extreme flood events, leading to incorrect financial budgeting.
- **Risk 2 — Data Drift & Climate Change Vulnerability:** Unprecedented weather anomalies driven by global climate change could cause data drift, reducing model accuracy if historical training sets are not continuously updated.
- **Risk 3 — Economic Discrepancy Risk:** Over-reliance on automated financial projections without validating current raw material market price fluctuations could impact operational OPEX calculations.

---

## Weekly Progress
| Week | Focus | Deliverable | Status |
| :---: | :--- | :--- | :---: |
| **W1** | System map + project scope definition | `README.md` + `/docs` (Scope & System Map) | ✅ |
| **W2** | Data engineering, SRS & architecture v1.0 | `week2_requirements.md` + Architecture | ✅ |
| **W3** | Data pipeline implementation & EDA | Jupyter Notebooks + Preprocessing Pipeline | ⏳ |
