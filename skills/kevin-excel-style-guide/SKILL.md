---
name: kevin-excel-style-guide
description: Apply Kevin's formatting, formula, and source-documentation standards whenever a spreadsheet file is the primary input or requested output. Use for .xlsx, .xlsm, .csv, and .tsv work; do not use when the primary deliverable is a document, web page, standalone script, database workflow, or Google Sheets API integration.
---

# Kevin's Excel Style Guide

Apply these preferences alongside the standard spreadsheet-authoring workflow. User instructions and established workbook or template conventions take precedence.

## All Excel Workbooks

### Font

- Use Aptos Display throughout Excel workbooks.
- If Aptos Display is unavailable, use one consistent professional sans-serif font, such as Open Sans or Arial.
- CSV and TSV files cannot retain visual formatting; apply only the relevant data- and formula-quality requirements to those formats.

### Formula Quality

- Deliver workbooks with no formula errors, including `#REF!`, `#DIV/0!`, `#VALUE!`, `#N/A`, and `#NAME?`.
- Use spreadsheet formulas for calculations rather than externally calculated values hardcoded into result cells.
- Verify references, copied ranges, and cross-sheet links. Check for off-by-one errors and unintended circular references.
- Test relevant edge cases, including zero and negative values.

### Existing Workbooks and Templates

- Match the workbook's existing format, style, structure, and conventions when modifying it.
- Do not restyle or reorganize unrelated content to impose these defaults.

## Financial Models

Apply the following conventions unless the user instructs otherwise or an existing workbook establishes another standard.

### Text and Fill Colors

- **Blue text (`RGB 0,112,192`)**: Hardcoded inputs and scenario values users may change.
- **Black text (`RGB 26,26,26`)**: Formulas and calculations.
- **Green text (`RGB 0,176,80`)**: Links to other worksheets in the same workbook.
- **Red text (`RGB 192,0,0`)**: External workbook links.
- **Yellow fill (`RGB 255,255,192`) with red text**: Key assumptions needing attention or updates.
- **Orange text (`RGB 233,113,50`)** and **purple text (`RGB 112,48,160`)**: Distinct callouts when the primary colors already carry other meanings.

### Number Formats

- **Years**: Store or display as text strings, such as `2024`, without thousands separators.
- **Currency**: Use `$#,##0` conventions and state units in headers, such as `Revenue ($mm)`.
- **Zeros**: Display as `-`, including currency and percentages; for example, `$#,##0;($#,##0);-`.
- **Percentages**: Default to `0.00%`.
- **Valuation multiples**: Use `0.0x`.
- **Negative numbers**: Display in parentheses rather than with a minus sign.

### Assumptions and Formulas

- Put assumptions such as growth rates, margins, and multiples in separate assumption cells.
- Reference those cells in formulas instead of embedding assumption values. Use `=B5*(1+$B$6)` rather than `=B5*1.05`.
- Keep formulas consistent across comparable projection periods.

### Sources for Hardcoded Inputs

- Document material hardcoded inputs in a cell note or adjacent source cell.
- Use this format: `Source: [System/Document], [Date], [Specific Reference], [URL if applicable]`.
- Examples:
  - `Source: Company 10-K, FY2024, Page 45, Revenue Note, [SEC EDGAR URL]`
  - `Source: Company 10-Q, Q2 2025, Exhibit 99.1, [SEC EDGAR URL]`
  - `Source: Bloomberg Terminal, 8/15/2025, AAPL US Equity`
  - `Source: FactSet, 8/20/2025, Consensus Estimates Screen`
