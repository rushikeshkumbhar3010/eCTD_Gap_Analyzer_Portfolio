# Power BI Dashboard Build Guide (about 30 minutes)

Source data: `../eCTD_Gap_Analyzer_Simulated_Data.xlsx` (all data is synthetic).
Preview of the target look: `Dashboard_Layout_Preview.png`.

## 1. Load the data
1. Power BI Desktop > **Get data > Excel workbook** > select the workbook.
2. Tick these tables: `tblDocuments`, `tblFindings`, `tblDefects`, `tblRegional`, `tblGuidelines`.
3. In Power Query rename them to `Documents`, `Findings`, `Defects`, `Regional`, `Guidelines`.
4. Check types: `Score` columns = Decimal number (format as %), counts = Whole number, text columns = Text.
5. **Home > Close & Apply**.

## 2. Model
- Model view: create one-to-many relationships (single direction)
  - `Documents[DocID]` to `Findings[DocID]`
  - `Documents[DocID]` to `Defects[DocID]`
  - `Documents[DocID]` to `Regional[DocID]`
- **Modeling > New table**: `Threshold = GENERATESERIES(0.5, 1, 0.05)` (gate slider).
- Paste the measures from `Measures.dax` (one **New measure** each).
- **View > Themes > Browse for themes** > `eCTD_Gap_Analyzer_Theme.json`.

## 3. Pages and visuals

### Page 1 - Executive Overview
| Visual | Fields |
|---|---|
| Cards (6) | Documents Audited, Total Checks, Missing, Partial, Average Doc Score, Docs Passing Gate |
| Donut | Legend: `Documents[Verdict]` (column); Values: count of `Documents[DocID]` |
| Stacked bar | Axis: `Findings[Guideline]`; Values: Missing, Partial, Compliant |
| Column chart | Axis: `Documents[DocID]`; Values: Compliance Score; add a constant line at the gate (Analytics pane > Constant line, or use Gate Threshold) |
| Slicer | `Threshold[Value]` (single select, label "Passing score") |

Colours: Missing `#C62828`, Partial `#B26A00`, Compliant `#1A7F37`. Use **Verdict Color** and **Score Color** under Format > Conditional formatting > Field value.

### Page 2 - Findings Explorer
- Slicers: `Documents[Authority]`, `Documents[Section]`, `Findings[Status]`, `Findings[Guideline]`.
- Table: DocID, Element, Guideline, Status, Risk, Action. Conditional-format `Status` background (Missing red, Partial amber, Compliant green).

### Page 3 - Regional Sensitivity
- Matrix: Rows `Regional[DocID]`, Columns `Regional[Authority]`, Values `Regional Score` with background colour scale (red to green, centre 0.5).
- Second matrix or table: `Regional[Verdict]` by authority to show where the verdict changes (D07).
- Card: Authorities With Major Risk, Regional Runs.

### Page 4 - Tool Validation
- Cards: True Positives, False Positives, False Negatives, Precision, Recall.
- Matrix: Rows `Defects[Guideline]`, Values: Seeded (Sum), Detected (Sum).
- Text box: "Seeded defects were authored against the tool's own rules; this is a regression test, not independent accuracy."

## 4. Publish / share
- Save as `eCTD_Gap_Analyzer.pbix` and export pages to PDF (**File > Export > PDF**) for the repo.
- Take screenshots of each page into `docs/` and link them in the README. Keep the `Dashboard_Layout_Preview.png` label as "layout mock-up" if you use it instead of real screenshots.
- Do not commit any real company data.
