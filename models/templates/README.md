# Model Templates

This directory contains blank model frameworks provided by the instructor (Professor Adam Stauffer) for the BUS 629 - International Corporate Finance course at Shidler College of Business. Templates standardize architecture and named-range conventions across all students before company data is populated at Stage 3.

## Current Templates

### performance-ratios-template.xlsx

Stage 1 deliverable. Unmodified copy of the instructor's master template.

**6 Tabs:**
1. **Cover & Instructions** — Project overview and named-range key
2. **Legend** — Color-coding conventions
3. **Income Statement** — Skeleton with `INC_*` named-range placeholders
4. **Balance Sheet** — Skeleton with current and prior year columns (`BAL_*`, `startYear_*`)
5. **Cash Flow** — Operating, investing, financing activities (`CASH_*`)
6. **Ratios** — Six categories with named-range formulas (`RATIO_*`), auto-populates from financial statements

The Ratios tab is fully formulaic — no hardcoded numbers. Once Stage 3 financials are entered, ratios compute automatically.

## Color Conventions

| Color | Meaning |
|---|---|
| 🟡 Yellow | Inputs (raw financial data) |
| 🔵 Blue | Assumptions |
| 🟢 Green | Formulas |
| ⚪ Gray | Outputs |

## Usage Workflow

1. **Stage 1 (current):** Template is held here unmodified. Do NOT edit master templates.
2. **Stage 3:** Copy template from `models/templates/` to `models/builds/`, rename with company identifier, then populate with financial data.
3. **Stage 4:** Reference template structure when writing analytical specifications.
4. **Stage 5:** Use populated model from `models/builds/` for final deliverables.

## Source

Original template: [Professor Stauffer's course repo](https://github.com/adamwstauffer/shidler/blob/main/docs/templates/spreadsheets/performance-ratios-template.xlsx)

Course documentation: [Stage 1 instructions](https://github.com/adamwstauffer/shidler/blob/main/courses/BUS-629-VEMBA-International-Corporate-Finance/stage1-template-architecture.md)
