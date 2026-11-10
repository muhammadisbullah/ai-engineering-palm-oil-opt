# Pipeline Architectural Decisions - Week 3 Project

This document records key architectural decisions and engineering rationales implemented throughout the development of the PalmPOPT data pipeline.

---

## 1. Document Extraction and Chunking Strategy
* **Decision:** Adopted `pypdf` with paragraph-aware chunking for processing MPOB annual and statistical reports.
* **Rationale:** Standard character-level chunking risks truncating agricultural domain terms and statistical figures. Paragraph-aware chunking preserves semantic integrity, ensuring higher quality downstream keyword matching and LLM retrieval.

## 2. Time-Series Data Acquisition & Spatial Resolution
* **Decision:** Retained Open-Meteo API as the primary weather provider, focusing on coordinate parameters `(Lat: 3.5, Long: 102.5)` covering Peninsular Malaysia.
* **Rationale:** Open-Meteo offers open-access, reliable daily historical climate parameters (air temperature, precipitation, and topsoil moisture) that correlate directly with Fresh Fruit Bunch (FFB) yield dynamics.

## 3. Data Lineage and Provenance Tracking
* **Decision:** Implemented cryptographic SHA-256 hashing alongside JSON manifest generation (`week3_manifest.json` and `pipeline_manifest.json`).
* **Rationale:** Enforces data integrity and reproducibility across the AI pipeline. Any alteration in raw input files automatically invalidates manifest hashes, ensuring enterprise-grade data lineage compliance.

## 4. Pipeline Modularisation (Part C Output Architecture)
* **Decision:** Versioned the downstream processing outputs into a dedicated `pipeline_v1` directory structure.
* **Rationale:** Isolates exploratory datasets from production-ready inputs, allowing seamless model training and visualization integration without altering raw source files.