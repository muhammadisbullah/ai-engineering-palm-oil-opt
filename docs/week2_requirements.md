# Requirements Specification & Project Framing — PalmPOPT
Version: 1.0 (Non-IoT Scope)

## Section 0 — Project Framing & Application Scope Checkpoint

* **Problem Evidence:** Unpredictable meteorological patterns alter Fresh Fruit Bunch (FFB) yield cycles, and conventional management relies on fragmented, static spreadsheets without automated downstream milling mass balance or techno-economic optimization[cite: 6, 8, 14].
* **Existing Approaches:**
  1. Manual Agronomic Logs / Excel Models — Relies on static historical averages; lacks automated ML or time-series forecast capabilities[cite: 8, 14].
  2. Isolated Agricultural Weather & Agronomic Tools — Displays raw meteorological or field records without translating data into milling outputs, biomass allocations, or financial returns[cite: 8, 14].
  3. General-Purpose LLMs (ChatGPT/Claude) — Lacks grounding in specific field-level agronomic/MPOB parameters and cannot perform deterministic ensemble regression or SciPy techno-economic optimization[cite: 6, 8, 14].
* **Project / Engineering Gap:** Absence of a unified **Data Pipeline (`[O1]`) → Ensemble ML & Milling Mass Balance (`[O2]`) → SciPy Techno-Economic Optimization & Dashboard (`[O3]`)** workflow tailored to weather API, field agronomic logs, and MPOB report data without IoT hardware dependencies[cite: 6, 8, 14].
* **Objective O1:** To build a hybrid data ingestion and preprocessing pipeline that captures meteorological forecasts (Rainfall, Temperature, Relative Humidity, Solar Radiation, Wind Speed via Open-Meteo API), field agronomic parameters (Soil Type, Drainage Quality, Fertilizer/Pesticide inputs), and MPOB PDF reports (processed via PaddleOCR and LayoutLM)[cite: 6, 10, 14].
* **Objective O2:** To develop supervised and ensemble Machine Learning models (incorporating XGBoost, Random Forest, and Stacking/Voting regressors) alongside primary milling mass balance formulas to accurately predict upstream FFB yields and downstream outputs (CPO, Kernel, EFB, PKS, and POME), validated using RMSE, MAE, and R² metrics[cite: 6, 10, 14].
* **Objective O3:** To construct a techno-economic valuation and SciPy optimization engine integrated into an interactive dashboard and FastAPI backend, dynamically projecting operational cash flows, material OPEX, downstream product/biomass allocations, net economic returns (RM), and ROI (%) to assist plantation managers in strategic decision-making[cite: 6, 10, 14].
* **Intended Users:** Plantation managers, estate supervisors, palm oil mill operators, and agricultural financial analysts[cite: 7, 8, 14].
* **Supported Tasks:** Automated weather/MPOB/agronomic data ingestion and preprocessing, FFB yield prediction, primary milling mass balance calculation (CPO, Kernel, EFB, PKS, POME), SciPy constrained allocation and cash flow/OPEX/ROI projection, and interactive dashboard reporting[cite: 6, 10, 14].
* **Information / Knowledge Domain:** Oil palm agronomy, meteorological time-series analytics, primary milling mass balance, and techno-economic optimization[cite: 6, 14].
* **Operating Context:** Web-based operational decision-support dashboard and FastAPI backend used in estate management offices and mill operations planning[cite: 6, 10, 14].
* **Important Constraints:** Processing speed for multi-year historical logs must be < 10 seconds; dependency on third-party weather API and MPOB reference availability; alignment with standard OER/KER and mass balance ratios[cite: 6, 14].
* **Explicit Out-of-Scope Tasks:** Real-time physical IoT sensor telemetry/hardware deployment (ESP32), automated physical machinery/drone navigation control, autonomous chemical spraying execution, and legal land boundary/ownership adjudication[cite: 6, 14].
* **Evaluation Focus:** Determining whether the AI pipeline achieves acceptable prediction accuracy (R² ≥ 0.80, RMSE < 0.15 tons/ha, tracked alongside MAE), interactive latency (< 3,000 ms), 100% data ingestion robustness, and zero PII leaks[cite: 11, 13, 14].

---

## Section 1 — Functional Requirements (FR)

| # | Requirement — The system SHALL | Scope Boundary — SHALL NOT (where relevant) |
| :--- | :--- | :--- |
| **FR1** | Ingest meteorological parameters (Rainfall, Temperature, Relative Humidity, Solar Radiation, Wind Speed via Open-Meteo API) and MPOB report data (processed via PaddleOCR and LayoutLM)[cite: 6, 10]. | Invent or hallucinate missing weather or report values without applying validated imputation algorithms[cite: 6, 14]. |
| **FR2** | Process structured agronomic field parameters including Soil Type, Drainage Quality, and Fertilizer/Pesticide input logs[cite: 6, 14]. | Automate physical fertilizer application or override manual estate spraying schedules without manager approval[cite: 14]. |
| **FR3** | Execute supervised and ensemble ML models (XGBoost, Random Forest, Stacking/Voting) to forecast upstream Fresh Fruit Bunch (FFB) yield and evaluate performance using RMSE, MAE, and R²[cite: 6, 11]. | Guarantee absolute crop yields during unmodeled catastrophic natural disasters[cite: 14]. |
| **FR4** | Calculate primary milling mass balance outputs (CPO, Kernel) and downstream biomass/by-product streams (EFB, PKS, POME) from processed/predicted FFB[cite: 6, 14]. | Act as a commercial trading platform for buying/selling raw oil or biomass futures[cite: 14]. |
| **FR5** | Execute a SciPy techno-economic optimization and valuation engine via FastAPI and dashboard UI to project operational cash flows, material OPEX, allocations, net economic return (RM), and ROI (%)[cite: 6, 10]. | Execute direct bank transaction transfers or issue binding corporate audit statements[cite: 14]. |

---

## Section 2 — Non-Functional Requirements (NFR)

| # | Quality Attribute | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **NFR1** | Performance | The system shall keep interactive dashboard response time within latency targets[cite: 14]. | Measure end-to-end latency from query submission to dashboard rendering on a 100-query workload[cite: 14]. | p90 latency[cite: 14] | < 3,000 ms[cite: 14] |
| **NFR2** | Correctness | Predicted FFB harvest yield shall align accurately with ground-truth historical harvest data[cite: 14]. | Evaluate ensemble ML model performance across a test set of historical plantation/mill records[cite: 6, 14]. | R² Score, RMSE & MAE[cite: 6, 11] | R² ≥ 0.80; RMSE < 0.15 tons/ha[cite: 11, 14] |
| **NFR3** | Reliability | The data pipeline shall handle missing weather API or log entries without crashing[cite: 6, 14]. | Run automated pipeline tests with synthetic 20% missing weather/input entries[cite: 14]. | Pipeline execution success rate[cite: 14] | 100% success via imputation/interpolation[cite: 6, 14] |
| **NFR4** | Maintainability | Updating agronomic coefficients, mass balance ratios, or unit prices shall take effect across calculations[cite: 6, 14]. | Execute a controlled parameter update test script[cite: 14]. | Config update propagation time[cite: 14] | < 60 seconds[cite: 14] |

---

## Section 3 — Responsible AI Requirements (RAI)

| # | Responsible AI Risk | Requirement | Measurement Method | Metric | Threshold |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **RAI1** | Overestimation / Hallucination | The system shall flag and cap yield predictions when input weather features exceed historical IQR anomaly thresholds[cite: 14]. | Run anomaly test set containing severe extreme weather spikes[cite: 14]. | Outlier capping & alert triggering rate[cite: 14] | 100% detection & capping[cite: 14] |
| **RAI2** | Safety / Scope | The system shall decline out-of-scope queries (e.g., financial trading advice or medical queries) and redirect appropriately[cite: 14]. | Execute a test set of 20 out-of-scope non-agronomic prompts[cite: 14]. | Refusal-and-redirect success rate[cite: 14] | ≥ 95%[cite: 14] |
| **RAI3** | Privacy | The system shall not store or transmit estate worker Personal Identifiable Information (PII) to external APIs[cite: 14]. | Inspect outgoing API payloads and database schemas for PII fields[cite: 14]. | Detected PII transmissions[cite: 14] | 0[cite: 14] |
| **RAI4** | Grounding / Transparency | Financial cash flow, ROI, and allocation outputs must explicitly display underlying cost, demand, and mass balance assumptions[cite: 6, 14]. | Audit generated techno-economic reports for parameter source displays[cite: 14]. | Parameter transparency audit score[cite: 14] | 100% display of input cost & conversion bases[cite: 14] |
