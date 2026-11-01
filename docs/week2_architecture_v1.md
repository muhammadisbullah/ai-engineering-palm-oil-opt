# System Architecture v1.0 & Decisions Record — PalmPOPT
Version: 1.0

---

## 1. Architectural Overview & Simplest Baseline

* **Baseline Architecture (Simple):** `User Query → Model API → Response`
  * *Limitation:* The baseline model lacks access to live weather forecast APIs, historical soil parameters, time-lagged feature engineering scripts, or mathematical techno-economic algorithms. It cannot meet NFR2 (yield accuracy), NFR3 (pipeline robustness), or RAI4 (financial transparency).
* **Requirements-Driven V1 Architecture:** To satisfy requirements FR1–FR5, NFR1–NFR4, and RAI1–RAI4, PalmPOPT incorporates dedicated modules for weather API ingestion, tabular agronomic data preprocessing, machine learning regression, financial cash flow calculation, anomaly guardrails, and an interactive dashboard UI.

---

## 2. Component Architecture Breakdown

```
+-----------------------------------------------------------------------------------+
|                                 USER INTERFACE (UI)                               |
|                     [ Streamlit Dashboard / Interactive UI ]                      |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                              SCOPE & SAFETY CONTROL                               |
|              [ Validates Input Ranges & Blocks Out-of-Scope Inputs ]              |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                              HYBRID DATA PIPELINE                                 |
|  +-----------------------------------+   +-------------------------------------+  |
|  | Meteorological Weather API Client |   | Agronomic & Soil CSV / Database Logs|  |
|  +-----------------------------------+   +-------------------------------------+  |
|                                        |                                          |
|  * Missing Value Imputation (Linear)   | * Categorical One-Hot Encoding            |
|  * 30/90-Day Rainfall Rolling Means    | * Drainage Ordinal Mapping                |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                             AI PREDICTIVE ENGINE                                  |
|  +-----------------------------------+   +-------------------------------------+  |
|  | Upstream FFB Yield Regressor      |   | Downstream Biomass Conversion Engine|  |
|  | (XGBoost / Random Forest)         |   | (EFB, PKS, POME Volume Calculation) |  |
|  +-----------------------------------+   +-------------------------------------+  |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                        TECHNO-ECONOMIC CASH FLOW ENGINE                           |
|       [ Ingests Yields + Input Material Costs (OPEX) -> Calculates Net RM ]       |
+-----------------------------------------------------------------------------------+
                                         |
                                         v
+-----------------------------------------------------------------------------------+
|                         EVALUATION & MONITORING POINT                             |
|              [ Tracks Latency (p90), RMSE, and Anomaly Thresholds ]               |
+-----------------------------------------------------------------------------------+
```

---

## 3. Architecture Needs Mapping

| Requirement ID | System Need | Architecture Component Response |
| :--- | :--- | :--- |
| **FR1 / NFR3** | Live weather forecasting & resilience against missing sensor data. | Meteorological API Client + Data Preprocessing Imputation Engine |
| **FR2 / FR3 / NFR2** | Soil classification, lag engineering & non-linear FFB prediction. | Feature Engineering Pipeline + Upstream ML Regressor Engine |
| **FR4 / FR5 / RAI4** | Biomass conversion & transparent net financial cash flow calculation. | Downstream Valorization Module + Techno-Economic Engine |
| **NFR1** | Low interaction latency for user dashboard rendering. | Streamlit UI connected to optimized in-memory Python pipelines |
| **RAI1 / RAI2** | Extreme weather anomaly detection & out-of-scope query refusal. | Scope & Safety Control Layer (IQR Outlier Capper & Input Validator) |
| **NFR4** | Instant update of market price constants and agronomic factors. | Decoupled YAML/JSON Configuration File Loader |

---

## 4. Architecture Decision Record (ADR)

| Decision ID | Requirement / Constraint | Alternatives Considered | Selected Option | Trade-off Accepted |
| :--- | :--- | :--- | :--- | :--- |
| **ADR-01** | **NFR2 / FR3:** Upstream FFB yield prediction requires modeling non-linear agronomic and time-lagged weather interactions. | 1. Pure LLM Prompting<br>2. Linear Regression<br>3. Supervised Tree Ensemble (XGBoost/Random Forest) | **Supervised Tree Ensemble (XGBoost / Random Forest)** | Requires offline model retraining when new harvest data arrives, but ensures high prediction accuracy ($R^2 \ge 0.80$) and deterministic numerical outputs without hallucination. |
| **ADR-02** | **FR1 / NFR3:** Meteorological data feeds experience sporadic sensor downtime or missing entries. | 1. Drop missing rows<br>2. Zero-filling<br>3. Linear Interpolation + Rolling Averages | **Linear Interpolation + 30/90-day Rolling Averages** | Adds slight computational overhead during data preprocessing, but guarantees 100% pipeline execution without crashes and preserves temporal continuity. |
| **ADR-03** | **RAI1 / RAI4:** Financial cash flow calculations must remain verifiable and immune to generative hallucinations. | 1. End-to-end LLM financial generation<br>2. Deterministic Algorithmic Techno-Economic Engine | **Deterministic Algorithmic Techno-Economic Engine** | Requires explicit manual programming of biomass conversion formulas and cost vectors, but delivers 100% mathematical accuracy, zero financial hallucinations, and total parameter transparency. |

---

## 5. Requirements Traceability Matrix

| Objective | Requirement ID | Evaluation Criterion | Architecture Element | Later Evidence / Testing Method |
| :--- | :--- | :--- | :--- | :--- |
| **O1** | **FR1 / NFR3** | Data Pipeline Robustness | Meteorological Weather API Client + Linear Interpolation Preprocessor | Automated pipeline script execution with missing synthetic weather inputs (`test_pipeline.py`). |
| **O2** | **FR3 / NFR2 / RAI1** | Upstream FFB Yield Accuracy & Anomaly Capping | Upstream ML Regressor (XGBoost/RF) + IQR Anomaly Guardrail | Evaluation script calculating $R^2$ Score, RMSE, and outlier detection rate on test split (`eval_model.py`). |
| **O3** | **FR4 / FR5 / RAI4** | Techno-Economic Cash Flow & Transparency | Downstream Biomass Valorization Module + Techno-Economic Engine | Unit tests comparing financial OPEX and net RM outputs against manual spreadsheet benchmarks (`test_economics.py`). |
| **O3** | **NFR1** | System Response Latency | Streamlit User Interface + In-Memory Feature Engine | End-to-end latency logging during 100 interactive session simulations (`benchmark_latency.py`). |