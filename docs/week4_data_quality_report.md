# Week 4 Data Quality Report — PalmPOPT

## 1. Executive Summary & Quality-Gate Decision
- **Project**: PalmPOPT (modelling fresh fruit bunch [FFB] yields, crude palm oil [CPO] and palm kernel milling mass balances, downstream derivative allocations, and biomass/waste valuation for EFB and POME)
- **Audited Topic / Lab**: Topic 3 (Lab 3) existing outputs and manifests
- **Quality-Gate Decision**: **[PASS / CONDITIONAL PASS / FAIL]** — *(State the final gate decision based on schema consistency, text/time-series quality, and manifest traceability)*
- **Summary of Key Findings**: *(Summarise key findings across the MPOB PDF/text pathway and the weather/soil time-series pathway)*

## 2. Scope & Audited Topic 3 Artefacts
- **Part B Prepared Artefacts (`data/processed/`) & Source Traceability (`data/week3_manifest.json`)**:
  - `prepared_text.jsonl` — *(State presence, record count, and reference entry in `data/week3_manifest.json`)*
  - `prepared_timeseries.csv` — *(State presence, date/row range, and reference entry in `data/week3_manifest.json`)*
- **Pipeline Outputs (`data/pipeline_v1/<selected_type>/` & `pipeline_manifest.json`)**:
  - `mapped_parameters_output.jsonl` / `integrated_palm_dataset.jsonl` — *(State exact repository paths under `data/pipeline_v1/<selected_type>/` and alignment with `pipeline_manifest.json`)*
- **Non-Duplication Note**: Existing Topic 3 notebook outputs, inventory, and manifests were reused directly without creating duplicate copies or unnecessary new pipeline runs.

## 3. Data Quality Dimensions & Audit Criteria
- **Completeness**: Check for null/NaN values, truncated records, missing required fields, or gaps across text and time-series records.
- **Validity & Schema Consistency**: Check JSONL keys/structure, column data types, timestamp/date formats, and palm/weather/soil parameter units.
- **Accuracy & Domain Plausibility**: Check whether values are plausible for oil palm agronomy, milling mass balance, downstream/biomass context, and MPOB / Open-Meteo data.
- **Consistency & Cross-Source Alignment**: Check alignment across `data/week3_manifest.json`, `pipeline_manifest.json`, inventory documentation, and integrated records.
- **Uniqueness & Timeliness**: Check for duplicate records/chunks and verify coverage/currency of the audited periods.

## 4. Pathway-by-Pathway Audit Findings
### 4.1 Text / Document Pathway (MPOB PDFs -> Prepared / Mapped / Integrated Text)
- **Audited File(s)**: *(List exact file paths audited)*
- **Findings**: *(Document PDF extraction artifacts such as table formatting remnants, excessive line breaks/whitespace, or short/noisy chunks that affect downstream mapping)*

### 4.2 Time-Series / Tabular Pathway (Weather & Soil -> Prepared / Integrated Data)
- **Audited File(s)**: *(List exact file paths audited)*
- **Findings**: *(Document numeric/datetime types, missing or extreme values, and consistency between prepared time-series and integrated records)*

## 5. Audit Evidence & Verification
- Referenced existing Topic 3 notebook outputs, `data/week3_manifest.json`, `pipeline_manifest.json`, and `week3_data_inventory.md`.
- **Additional Validation Evidence (As Needed)**: *(Include concise metric summaries, tables, or small permitted screenshots/chart outputs only where existing Topic 3 evidence does not already cover a check)*

## 6. Issues, Risks & Remediation Plan
| ID | Pathway / Artefact | Issue Description | Severity (High/Med/Low) | Remediation Action (For Later Topics) |
| :--- | :--- | :--- | :--- | :--- |
| DQ-01 | Text pathway | *(e.g., PDF line-break/table-fragment noise in extracted text)* | Medium | Clean whitespace/line breaks and filter low-value fragments in later processing |
| DQ-02 | Manifest / Path alignment | *(e.g., verify file naming and path consistency across manifests and docs)* | Low | Align manifest references and documentation paths before next stage |

## 7. Quality-Gate Justification & Topic 5 Hand-Off
- **Gate Justification**: *(Explain why PASS, CONDITIONAL PASS, or FAIL was selected against your quality thresholds)*
- **Hand-Off Notes for Topic 5**: *(Specify what to address or carry forward when transitioning into Topic 5)*

## 8. Progress Link & Governance Compliance
- **GitHub Commit Reference**: *(Record verified existing GitHub commit hash and commit message)*
- **README Link**: *(Confirm link to `docs/week4_data_quality_report.md` in `README.md`)*
- **Data Governance & Privacy Check**: Confirmed only authorised, non-sensitive evidence is committed; restricted/raw paths are recorded at a safe disclosure level.