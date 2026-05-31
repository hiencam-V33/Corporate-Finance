# models

Excel workbooks: the templates the course provides and the populated models I built from them. The discipline this folder enforces is the separation between **template** (unmodified course-provided structure) and **build** (my populated workbook with the company's data).

## Subdirectories

- [`templates/`](./templates) — Stage 1 ratios template, unmodified. The course-provided starting point with named ranges, ratio formulas, and validation tabs pre-defined.
- [`builds/`](./builds) — Stage 3 populated Sectra workbook. Income Statement, Balance Sheet, and Cash Flow tabs filled with Sectra's FY2024/2025 audited financials and prior-year comparatives, sourced from the Annual Report. The Ratios tab auto-computes once the statement tabs are populated.

## Naming convention

- Templates: keep the course-provided filename (`performance-ratios-template.xlsx`).
- Builds: `YYYY-MM-DD-{lastname}-{company-slug}-financials.xlsx` per the project-wide convention.

## How this folder fits the project

The Stage 3 workbook is the data foundation everything downstream consumes:
- The Stage 4 spec quotes specific cell values and formulas from this workbook.
- The Stage 5 LLM execution operates on the model's named ranges.
- The Stage 5 manual verification table re-derives ratios by hand from this workbook to cross-check the LLM's output.

If a number in any downstream deliverable doesn't tie to this workbook, that's a bug worth tracking down — by design.

## Validation

The Stage 3 workbook passed all four BUS 629 Stage 3 criteria per the instructor's PR review: balance sheet balances both years, named ranges populated, documentation complete, and ratios resolve cleanly. The eight validation rules used during Stage 4 spec writing are documented in [`docs/specs/2026-05-30-cam-sectra-spec.md`](../docs/specs) Section 7.
