# Requirements Specification & Project Framing — PalmPOPT
Version: 1.0

## Section 0 — Project Framing & Application Scope Checkpoint

* **Problem Evidence:** Unpredictable meteorological patterns alter Fresh Fruit Bunch (FFB) yield cycles, and conventional management relies on fragmented, static spreadsheets without automated downstream biomass or economic integration (MPOB Annual Reports 2022–2024; SCOPUS Agri-Tech Literature 2023).
* **Existing Approaches:**
  1. Manual Agronomic Logs / Excel Models — Relies on static historical averages; lacks automated ML or time-series forecast capabilities.
  2. Isolated Agricultural Weather Apps — Displays raw meteorological dashboards without translating data into crop yields or financial returns.
  3. General-Purpose LLMs (ChatGPT/Claude) — Lacks grounding in specific field-level soil/chemical parameters and cannot perform deterministic techno-economic cash flow calculations.
* **Project / Engineering Gap:** Absence of a unified **Data Pipeline-to-AI-to-Financial Engine** that ingests multi-source data streams (weather API + agronomic/soil logs) to dynamically project upstream FFB harvest yields, downstream biomass valorization (EFB, PKS, POME), and net operational cash flow (RM).
* **Objective O1:** To design and build an automated hybrid data pipeline that ingests meteorological forecasts (Rainfall, Temperature) and agronomic field parameters (Soil Type, Drainage, Fertilizer/Pesticide inputs).
* **Objective O2:** To develop supervised Machine Learning models (XGBoost / Random Forest) that accurately predict upstream FFB yields and downstream biomass conversion fractions (EFB, PKS, POME).
* **Objective O3:** To construct a techno-economic valuation module and interactive dashboard that dynamically projects operational cash flows, material OPEX, and net economic returns (RM).
* **Intended Users:** Plantation managers, estate supervisors, palm oil mill operators, and agricultural financial analysts.
* **Supported Tasks:** Automated weather data ingestion, feature lag computation, FFB yield prediction, biomass conversion volume estimation, material OPEX calculation, and net cash flow reporting.
* **Information / Knowledge Domain:** Oil palm agronomy, meteorological time-series analytics, biomass valorization conversion ratios, and agricultural cash flow economics.
* **Operating Context:** Web-based operational decision-support dashboard used in estate management offices and mill operations planning.
* **Important Constraints:** Processing speed for multi-year historical logs must be $< 10$ seconds; dependency on third-party weather API availability; compliance with standard MPOB conversion ratios.
* **Explicit Out-of-Scope Tasks:** Automated physical machinery/drone navigation control, autonomous chemical spraying execution, and legal land boundary/ownership adjudication.
* **Evaluation Focus:** Determining whether the hybrid AI architecture achieves acceptable prediction accuracy ($R^2 > 0.80$, RMSE $< 0.15$ tons/ha), interactive latency ($< 3,000$ ms), 100% data ingestion robustness, and zero PII leaks.

---

## Section 1 — Functional Requirements (FR)

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
| :--- | :--- | :--- |
| **FR1** | Ingest daily real-time and forecast weather parameters (Rainfall Volume in mm, Ambient Temperature in °C) via weather API feeds. | Invent or hallucinate missing weather values without applying validated linear interpolation algorithms. |
| **FR2** | Process structured agronomic field parameters including Soil Type (Peat, Clay, Mineral), Drainage Performance ratings, and Fertilizer/Pesticide application dosages. | Automate physical fertilizer application or override manual estate spraying schedules without manager approval. |
| **FR3** | Execute supervised ML models to forecast upstream Fresh Fruit Bunch (FFB) harvest output in Tons/Ha based on time-lagged precipitation features. | Guarantee absolute crop yields during unmodeled catastrophic natural disasters (e.g., severe prolonged land submergence). |
| **FR4** | Calculate downstream biomass valorization volumes for Empty Fruit Bunches (EFB), Palm Kernel Shells (PKS), and Palm Oil Mill Effluent (POME). | Act as a commercial trading platform for buying/selling raw biomass futures. |
| **FR5** | Compute dynamic techno-economic cash flows, deducting material input OPEX (fertilizer/pesticide costs) from projected FFB and biomass revenues to output net financial returns (RM). | Execute direct bank transaction transfers or issue binding corporate audit statements. |

---

## Section 2 — Non-Functional Requirements (NFR)

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **NFR1** | Performance | The system shall keep interactive dashboard response time within latency targets. | Measure end-to-end latency from query submission to dashboard rendering on a 100-query workload. | p90 latency | $< 3,000$ ms |
| **NFR2** | Correctness | Predicted FFB harvest yield shall align accurately with ground-truth historical harvest data. | Evaluate ML model performance across a test set of historical plantation plots. | $R^2$ Score / RMSE | $R^2 \ge 0.80$ / RMSE $< 0.15$ tons/ha |
| **NFR3** | Reliability | The data pipeline shall handle missing weather API inputs without crashing. | Run automated pipeline tests with synthetic 20% missing weather data entries. | Pipeline execution success rate | $100\%$ success via linear interpolation |
| **NFR4** | Maintainability | Updating agronomic coefficients or fertilizer unit prices shall take effect across calculations instantly. | Execute a controlled parameter update test script. | Config update propagation time | $< 60$ seconds |

---

## Section 3 — Responsible AI Requirements (RAI)

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RAI1** | Overestimation / Hallucination | The system shall flag and cap yield predictions when input weather features exceed historical IQR anomaly thresholds. | Run anomaly test set containing severe extreme weather spikes (e.g., flash flood spikes). | Outlier capping & alert triggering rate | $100\%$ detection & capping |
| **RAI2** | Safety / Scope | The system shall decline out-of-scope queries (e.g., financial trading advice or medical queries) and redirect appropriately. | Execute a test set of 20 out-of-scope non-agronomic prompts. | Refusal-and-redirect success rate | $\ge 95\%$ |
| **RAI3** | Privacy | The system shall not store or transmit estate worker Personal Identifiable Information (PII) to external APIs. | Inspect outgoing API payloads and database schemas for PII fields. | Detected PII transmissions | $0$ |
| **RAI4** | Grounding / Transparency | Financial cash flow metrics must explicitly display the underlying cost and conversion assumptions used. | Audit generated techno-economic reports for parameter source displays. | Parameter transparency audit score | $100\%$ display of input cost bases |