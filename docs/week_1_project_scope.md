# Lab 1: Project Scope — PalmPOPT

**Project Name:** PalmPOPT  
**Domain:** Agricultural AI Engineering / Smart Plantation & Biomass Valorization  

---

### 1. Problem Statement
Plantation managers and palm oil mill operators face severe operational and financial volatility due to unpredictable weather patterns (rainfall fluctuations and temperature stress) affecting oil palm yields, while lacking integrated tools to forecast downstream biomass valorization (EFB, PKS, POME) and operational cash flow. AI engineering provides the optimal framework to construct an end-to-end data pipeline and decision support system that unifies real-time weather feeds, soil/chemical parameters, and machine learning models for dynamic yield and financial optimization.

### 2. Evidence of the Problem
* **Evidence 1:** Unpredictable rainfall patterns and prolonged dry or wet spells lead to significant yield variations in oil palm plantations, causing severe supply chain disruptions for downstream processing mills.
  * *Source / citation:* Malaysian Palm Oil Board (MPOB) Annual Report & Yield Statistics Reports (2022–2024).
* **Evidence 2:** Conventional plantation management relies on disconnected spreadsheets for weather logging, fertilizer budgeting, and mill production tracking, making it impossible to perform dynamic financial forecasting based on real-time field parameters.
  * *Source / citation:* Industry case studies on palm oil supply chain digitalization (SCOPUS-indexed sustainable agriculture literature, 2023).

### 3. Initial Related Work (at least 3)
* **Study / solution 1:** Manual Agronomic & Static Statistical Excel Models
  * *Source / citation:* Standard plantation management record-keeping practices.
  * *Key limitation:* Relies on historical averages; cannot process real-time weather forecasts, time-lagged precipitation interactions, or automated non-linear ML predictions.
* **Study / solution 2:** Isolated Commercial Weather Station Monitoring Apps
  * *Source / citation:* Agricultural IoT weather monitoring software platforms.
  * *Key limitation:* Provides raw meteorological dashboards but lacks machine learning engines to translate weather trends into actionable downstream biomass output or net financial cash flow projections.
* **Study / solution 3:** General-Purpose Generative AI Chatbots (e.g., ChatGPT / Claude)
  * *Source / citation:* Commercial Foundation Models.
  * *Key limitation:* Lack grounding in specific field-level soil/chemical data vectors, exhibit hallucination risks, and cannot execute deterministic mathematical techno-economic cash flow calculations.

### 4. Engineering Gap / Limitation
Existing market approaches are either fragmented (separating weather telemetry from financial budgeting), dependent on static human estimation, or ungrounded in combined upstream-downstream agronomic data pipelines. There is a distinct technical gap in developing a unified **Data Pipeline-to-AI-to-Financial Engine** that ingests multi-source parameter streams to predict both upstream harvest yields and downstream bio-valorization economics in real time.

### 5. Initial Project Objectives (2–3)
* **O1:** To design and build an automated hybrid data pipeline that ingests meteorological forecasts (Rainfall, Temperature) and field agronomic parameters (Soil Type, Drainage, Fertilizer/Pesticide inputs).
* **O2:** To develop supervised Machine Learning models (XGBoost / Random Forest) that accurately predict upstream FFB yields and downstream biomass conversion fractions (EFB, PKS, POME).
* **O3:** To construct a techno-economic valuation module and interactive dashboard that dynamically projects operational cash flows, material OPEX, and net economic returns (RM).

### 6. Target Users
Undergraduate researchers, plantation managers, estate supervisors, and palm oil mill operational planners.

### 7. Data Sources (at least 2)
* **Source 1:** Open-Meteo / Malaysian Meteorological Department API — Historical and forecast data for daily precipitation (mm) and temperature (°C) — *URL:* https://open-meteo.com/
* **Source 2:** MPOB Agronomic & Yield Guidelines PDF — Standard conversion factors for FFB yield rates and biomass ratios — *URL:* https://www.mpob.gov.my/

### 8. Similar to EduAdvisor
Shares a structured parameter-driven advisory approach, utilizing a modular AI architecture (Ingestion $\rightarrow$ Pipeline $\rightarrow$ Model $\rightarrow$ UI Dashboard) to deliver automated, reliable decision support to end users.

### 9. Different from EduAdvisor
EduAdvisor focuses on static text document retrieval (RAG) for university course advising, whereas PalmPOPT processes dynamic numerical/time-series meteorological streams and agronomic parameters to execute predictive machine learning regression and techno-economic cash flow calculations.

### 10. Responsible AI Risks (at least 2)
* **Risk 1 — Overestimation / Hallucination Risk:** Models trained on incomplete historical weather logs might project unrealistic yield spikes, leading plantation managers into incorrect financial budgeting.
* **Risk 2 — Data Drift & Climate Vulnerability:** Rapid global climate shifts can cause severe data drift over time, reducing prediction accuracy and potentially misinforming long-term estate planning.