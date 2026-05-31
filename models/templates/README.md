# models/templates

The course-provided ratios template for BUS 629. **This file is unmodified** — the discipline is to keep the template intact as a reference, and to do all data entry and customization in [`models/builds/`](../builds) instead.

## What's in here

- **`performance-ratios-template.xlsx`** — Pre-built Excel workbook with:
  - Income Statement, Balance Sheet, and Cash Flow tabs (empty, ready to populate).
  - Ratios tab with formulas referencing named ranges (auto-computes once the statement tabs are filled).
  - Cover sheet documenting the naming convention.
  - Validation cells that flag balance-sheet mismatches and other consistency issues.

## Why unmodified

Two reasons:

1. **Auditability.** A reviewer can diff my build against the original template to see exactly what I added, removed, or changed.
2. **Reusability.** If I (or anyone else) re-runs this workflow for another company in the future, the clean template is here as the starting point.

## How to use

If you are reproducing this workflow:
1. Copy this file to `models/builds/YYYY-MM-DD-{lastname}-{company-slug}-financials.xlsx`.
2. Populate the Income Statement, Balance Sheet, and Cash Flow tabs from the company's audited filings.
3. The Ratios tab will compute automatically.
4. Do not edit anything in this `templates/` directory.

## Source

Course-provided file from Professor Stauffer's course materials at [`adamwstauffer/shidler/courses/BUS-629-VEMBA-International-Corporate-Finance`](https://github.com/adamwstauffer/shidler/tree/main/courses/BUS-629-VEMBA-International-Corporate-Finance).
