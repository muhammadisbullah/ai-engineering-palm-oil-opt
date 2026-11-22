# System Architecture v1.0 & Decisions Record — PalmPOPT
Version: 1.0 (Non-IoT Scope)

---

## 1. Architectural Overview & Simplest Baseline

* **Baseline Architecture (Simple):** `User Query → Model API → Response`[cite: 12]
  * *Limitation:* The baseline model lacks access to Open-Meteo weather feeds, field agronomic logs, MPOB report parameters, time-lagged feature engineering, primary milling mass balance formulas, or SciPy techno-economic optimization[cite: 6, 12]. It cannot meet NFR2 (yield accuracy), NFR3 (pipeline robustness), or RAI4 (financial transparency)[cite: 12].
* **Requirements-Driven V1 Architecture:** To satisfy requirements FR1–FR5, NFR1–NFR4, and RAI1–RAI4, PalmPOPT incorporates dedicated modules for weather API, agronomic log, and MPOB data ingestion/preprocessing (`[O1]`), ensemble ML yield forecasting and primary milling mass balance (`[O2]`), SciPy techno-economic optimization (`[O3]`), anomaly guardrails, FastAPI backend, and an interactive dashboard UI[cite: 6, 10, 12].

---

## 2. Component Architecture Breakdown

```text
+-----------------------------------------------------------------------------------+
|                        [O3] INTERACTIVE DASHBOARD & FASTAPI                       |
|            [ Streamlit Dashboard UI + FastAPI Backend Service ]                   |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                              SCOPE & SAFETY CONTROL                               |
|             [ Validates Input Ranges, IQR Outliers & Out-of-Scope Inputs ]        |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                       [O1] DATA INGESTION & PREPROCESSING                       |
|  +------------------------------+  +--------------------+  +--------------------+  |
|  | Open-Meteo Weather API       |  | Field & Agronomic  |  | MPOB PDF Reports   |  |
|  | (Rain, Temp, RH, Solar, Wind)|  | Logs (Soil, Drain.,|  | (PaddleOCR &       |  |
|  |                              |  | Fert./Pesticide)   |  |  LayoutLM)         |  |
|  +------------------------------+  +--------------------+  +--------------------+  |
|                                         |                                         |
|  * Imputation (Linear / KNN / MissForest) & Rolling Averages                      |
|  * Min-Max Normalization & Feature Engineering                                    |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                [O2] ENSEMBLE ML & PRIMARY MILLING MASS BALANCE                    |
|  +------------------------------+  +--------------------------------------------+  |
|  | Ensemble ML Yield Models     |  | Primary Milling Mass Balance               |  |
|  | (XGBoost, Random Forest,     |  | - CPO & Kernel (OER / KER)                 |  |
|  |  Stacking/Voting) -> FFB     |  | - Biomass Streams: EFB, PKS, POME          |  |
|  +------------------------------+  +--------------------------------------------+  |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                 [O3] SCIPY TECHNO-ECONOMIC OPTIMIZATION ENGINE                    |
|  [ Maximizes Net Return (Z) via SciPy -> Cash Flows, Material OPEX, ROI (%) ]    |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                         EVALUATION & MONITORING POINT                             |
|              [ Tracks Latency (p90), RMSE, MAE, R² & Anomaly Alerts ]             |
+-----------------------------------------------------------------------------------+
```[cite: 6, 10, 12]

---

Requirement ID,System Need,Architecture Component Response
FR1 / NFR3,"Weather API, agronomic log & MPOB ingestion with resilience against missing data.",Open-Meteo Client + Agronomic/MPOB Parser + Imputation/Interpolation Engine
FR2 / FR3 / NFR2,Agronomic/weather feature engineering & non-linear FFB yield prediction.,"Feature Engineering Pipeline + Ensemble ML Regressor Engine (XGBoost, RF, Stacking/Voting)"
FR4 / FR5 / RAI4,Primary milling mass balance & SciPy techno-economic cash flow/ROI calculation.,Milling Mass Balance Module + SciPy Techno-Economic & Valuation Engine
NFR1,Low interaction latency for dashboard rendering.,Streamlit UI + FastAPI Backend with optimized Python pipeline
RAI1 / RAI2,Extreme weather anomaly capping & out-of-scope query refusal.,Scope & Safety Control Layer (IQR Outlier Capper & Input Validator)
NFR4,"Instant update of market price constants, mass balance fractions & agronomic factors.",Decoupled YAML/JSON Configuration File Loader
---

Decision ID,Requirement / Constraint,Alternatives Considered,Selected Option,Trade-off Accepted
ADR-01,NFR2 / FR3: Upstream FFB yield prediction requires modeling non-linear agronomic and meteorological interactions.,"1. Pure LLM Prompting2. Linear Regression3. Supervised & Ensemble Tree Models (XGBoost, RF, Stacking/Voting)","Ensemble Tree Models (XGBoost, RF, Stacking/Voting)","Requires offline retraining when new harvest data arrives, but improves predictive accuracy (RMSE, MAE, R² >= 0.80) and deterministic outputs."
ADR-02,FR1 / NFR3: Meteorological API feeds and logs experience sporadic missing values or gaps.,1. Drop missing rows2. Zero-filling3. Linear Interpolation / Imputation + Rolling Averages,Linear Interpolation / Imputation + Rolling Averages,"Adds slight preprocessing overhead, but prevents pipeline crashes and preserves temporal continuity."
ADR-03,FR4 / FR5 / RAI4: Milling mass balance and techno-economic optimization must remain verifiable and free of LLM hallucinations.,1. End-to-end LLM financial generation2. Deterministic Mass Balance + SciPy Techno-Economic Engine,Deterministic Mass Balance + SciPy Techno-Economic Engine,"Requires explicit formula and parameter setup, but provides verifiable mass balances, cash flows, OPEX, ROI (%), and net return (RM)."

---

Objective,Requirement ID,Evaluation Criterion,Architecture Element,Later Evidence / Testing Method
O1,FR1 / NFR3,Data Pipeline Robustness,"Open-Meteo, Agronomic & MPOB Ingestion + Imputation/Normalization Preprocessor",Automated pipeline script execution with missing synthetic weather/input data (test_pipeline.py).
O2,FR3 / NFR2 / RAI1,"FFB Yield Accuracy, Mass Balance & Anomaly Capping",Ensemble ML Regressor + Milling Mass Balance + IQR Anomaly Guardrail,"Evaluation script calculating RMSE, MAE, R² Score, and outlier capping rate on test split (eval_model.py)."
O3,FR4 / FR5 / RAI4,SciPy Techno-Economic Optimization & Transparency,SciPy Optimization & Valuation Engine + FastAPI Backend,"Unit/integration tests comparing cash flows, OPEX, ROI (%), and net RM against reference benchmarks (test_economics.py)."
O3,NFR1,System Response Latency,Streamlit User Interface + FastAPI Backend + Feature Pipeline,End-to-end latency logging during 100 interactive session simulations (benchmark_latency.py).
