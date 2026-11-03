# eCTD Module 3 Gap Analyzer - AI-Assisted Regulatory Affairs

A browser-based pre-submission audit tool for CMC (eCTD Module 3) draft sections, plus a simulated validation study with a Word report, Excel workbook and Power BI dashboard assets.

> **Simulation notice:** all validation documents are synthetic (fictional drugs, invented data). No real dossier, client data or live regulatory submission was used. This is academic, training-level work.

## What the tool does
- Audits draft sections 3.2.S.2, S.3, S.4, S.7, P.2, P.5, P.8 against ICH M4Q(R1), Q1A/Q1B/Q1E, Q2(R2), Q3A/B/C/D, Q6A and M7.
- Deterministic rule engine: impurity thresholds scaled to maximum daily dose, Q3C solvent and Q3D PDE limit checks, stability condition/batch/timepoint rules, DMF/LOA checks.
- 11 authorities: US FDA, EMA, MHRA, PMDA, Health Canada, TGA, Swissmedic, CDSCO, NMPA, ANVISA, WHO PQ.
- Outputs a gap matrix, compliance score, gate decision, verdict and a Module 2.3 QOS draft with `[DATA GAP]` markers.

## Simulated validation results
| Metric | Result |
|---|---|
| Synthetic documents | 10 (3 compliant, 7 with seeded defects) |
| Checks executed | 96 (35 Missing, 15 Partial, 46 Compliant) |
| Verdict agreement with expected | 10 / 10 |
| Seeded defects detected / false positives | 39 / 39, 0 |
| Gates passed at 90% | 3 / 10 |
| Regional re-runs | 110 (10 documents x 11 authorities) |

Seeded defects were written against the tool's own rules, so these figures are a regression test, not independent accuracy evidence.

## Repository contents
| File | Purpose |
|---|---|
| `eCTD_Module_3_Gap_Analyzer.html` | The tool (open in a browser, runs offline) |
| `eCTD_Gap_Analyzer_Simulated_Validation_Report.docx` | 8-page validation report |
| `eCTD_Gap_Analyzer_Simulated_Data.xlsx` | Data + formulas (Documents, Findings, Defect_Validation, Regional, Guideline_Coverage, Dashboard) |
| `PowerBI/eCTD_Gap_Analyzer_Interactive_Dashboard.html` | Interactive 4-page dashboard (open in a browser, works offline) |
| `PowerBI/Measures.dax` | DAX measures |
| `PowerBI/eCTD_Gap_Analyzer_Theme.json` | Power BI theme |
| `PowerBI/Dashboard_Build_Guide.md` | Step-by-step dashboard build |
| `PowerBI/Dashboard_Layout_Preview.png` | Layout mock-up |

## Limitations
- Synthetic data only; not validated on real submissions.
- Benchmark text is a condensed summary; verify against current ICH and agency documents.
- A screening aid, not a substitute for qualified regulatory review.

## Author
Rushikesh Mohan Kumbhar - M.Pharm (Regulatory Affairs) candidate, Savitribai Phule Pune University.
