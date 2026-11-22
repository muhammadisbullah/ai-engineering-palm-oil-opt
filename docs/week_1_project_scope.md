# Lab 1: Project Scope — PalmPOPT

**Project Name:** PalmPOPT  
**Domain:** Agricultural AI Engineering / Smart Plantation & Biomass Valorization  

---

### 1. Problem Statement
Plantation managers and palm oil mill operators face severe operational and financial volatility due to unpredictable weather patterns (rainfall, temperature, relative humidity, solar radiation, and wind speed) affecting Fresh Fruit Bunch (FFB) yields, while lacking integrated tools to map FFB outputs through primary milling mass balances and downstream biomass valorization (CPO, Kernel, EFB, PKS, POME) alongside operational cash flow and economic returns[cite: 11, 13]. AI engineering provides the optimal framework to build a modular pipeline that integrates meteorological, agronomic, and MPOB data with ensemble machine learning and constrained techno-economic optimization (`SciPy`) for data-driven decision support[cite: 11, 13].

### 2. Evidence of the Problem
* **Evidence 1:** Unpredictable rainfall patterns and prolonged dry or wet spells lead to significant yield variations in oil palm plantations, causing severe supply chain disruptions for downstream processing mills.
  * *Source / citation:* Malaysian Palm Oil Board (MPOB) Annual Report & Yield Statistics Reports (2022–2024).
* **Evidence 2:** Conventional plantation management relies on disconnected spreadsheets for weather logging, fertilizer/pesticide budgeting, and mill production tracking, making it difficult to link upstream yield forecasts with downstream mass balance, OPEX, and net economic return projections.
  * *Source / citation:* Industry case studies on palm oil supply chain digitalization (SCOPUS-indexed sustainable agriculture literature, 2023).

### 3. Initial Related Work (at least 3)
* **Study / solution 1:** Manual Agronomic & Static Statistical Excel Models
  * *Source / citation:* Standard plantation management record-keeping practices.
  * *Key limitation:* Relies on static averages or manual spreadsheets; cannot easily model non-linear multi-parameter interactions across weather, soil, and agronomic logs or automate multi-constraint optimization
* **Study / solution 2:** Isolated Weather & Agronomic Monitoring Dashboards
  * *Source / citation:* Agricultural meteorological and farm management software platforms
  * *Key limitation:* Displays environmental or field records separately without linking FFB yield forecasts to primary milling mass balance formulas
* **Study / solution 3:** General-Purpose Generative AI Chatbots (e.g., ChatGPT / Claude)
  * *Source / citation:* Commercial Foundation Models.
  * *Key limitation:* Lack grounding in structured agronomic/MPOB datasets, exhibit hallucination risks, and cannot execute reproducible supervised ensemble regression (`RMSE`, `MAE`, `R²`) or constrained numerical optimization (`SciPy`)

### 4. Engineering Gap / Limitation
Existing approaches are either fragmented (separating weather/agronomic data from milling mass balance and financial valuation) or reliant on static rules and disconnected tools. There is a technical gap in building a unified **Data Pipeline (`[O1]`) Ensemble ML & Milling Mass Balance (`[O2]`) SciPy Techno-Economic Optimization & Dashboard (`[O3]`)** workflow tailored to non-IoT meteorological, field agronomic, and MPOB data sources

### 5. Initial Project Objectives (2–3)
* **O1:** To build a hybrid data ingestion and preprocessing pipeline that captures meteorological forecasts (Rainfall, Temperature via Open-Meteo API), field agronomic parameters (Soil Type, Drainage, Fertilizer/Pesticide inputs), MPOB PDF reports (processed via PaddleOCR and LayoutLM), and real-time IoT hardware telemetry (ESP32 sensors filtered using Isolation Forest).

* **O2:** To develop supervised and ensemble Machine Learning models (incorporating XGBoost, Random Forest, and Stacking/Voting regressors) optimized with primary milling mass balance formulas to accurately predict upstream FFB yields and downstream biomass conversion fractions (CPO, Kernel, EFB, PKS, and POME), validated using RMSE and MAE metrics.
  
* **O3:**To construct a techno-economic valuation and SciPy optimization engine integrated into an interactive Streamlit dashboard and FastAPI backend, dynamically projecting operational cash flows, material OPEX, downstream product allocation, and net economic returns (RM) to assist plantation managers in strategic decision-making.


### 6. Target Users
Undergraduate researchers, plantation managers, estate supervisors, and palm oil mill operational planners.

### 7. Data Sources (at least 2)
* **Source 1:** Open-Meteo API — Historical and forecast meteorological parameters including rainfall, temperature, relative humidity, solar radiation, and wind speed — *URL:* https://open-meteo.com/
* **Source 2:** MPOB Statistical & Agronomic Reports / Guidelines — Reference records for OER, KER, FFB yield benchmarks, and biomass conversion ratios — *URL:* https://www.mpob.gov.my/
* **Source 3:** Field & Agronomic Logs — Plantation records for soil type, drainage quality, fertilizer type/rate, and pesticide/herbicide inputs

### 8. Similar to EduAdvisor
Shares a structured parameter-driven advisory approach, utilizing a modular AI architecture (Data Ingestion & Preprocessing $\rightarrow$ Predictive & Analytical Engine $\rightarrow$ Optimization/Valuation $\rightarrow$ UI Dashboard) to deliver automated, reliable decision support to end users

### 9. Different from EduAdvisor
EduAdvisor focuses on static text document retrieval (RAG) for university course advising, whereas PalmPOPT processes numerical/tabular meteorological, agronomic, and MPOB data to execute ensemble machine learning regression, milling mass balance calculations, and constrained SciPy techno-economic optimization

### 10. Responsible AI Risks (at least 2)
* **Risk 1 — Overestimation / Hallucination Risk:** Models trained on incomplete historical weather or MPOB logs might project unrealistic yield or economic return spikes, leading plantation managers into inaccurate budgeting and resource allocation.
* **Risk 2 — Data Drift & Climate Vulnerability:** Climate shifts and evolving agronomic practices can cause data drift over time, reducing model accuracy (`RMSE`, `MAE`, `R²`) and potentially misinforming estate and mill planning
