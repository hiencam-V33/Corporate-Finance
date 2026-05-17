# templates (models)

This directory holds Stage 1 model templates: blank Excel frameworks with structure, formulas, and instructions but no live project data. Templates here are the starting point for any new model — pick the appropriate template, copy it, populate it, and promote the populated workbook to `models/builds/` once it is validated.

A good template is opinionated: it bakes in the layout (inputs / calculations / outputs as separate sheets), the formatting convention (input cells blue, formula cells black, links green), and the basic structure of the calculation, so each new build does not reinvent the wheel.

## Naming conventions

- Template workbooks: `TEMPLATE_[ModelType].xlsx` (e.g. `TEMPLATE_DCF_Valuation.xlsx`).
- Worked examples: `EXAMPLE_[ModelType]_[Scenario].xlsx` (e.g. `EXAMPLE_DCF_SampleCo.xlsx`).
- Build instructions: `GUIDE_[ModelType].md`.
- Best-practice notes: `BEST_PRACTICES_[Category].md`.
- Use PascalCase for the `[ModelType]` slug.

## What goes here

- Blank Excel templates for each canonical model type (DCF, ratio analysis, capital budgeting, etc.).
- Worked example workbooks demonstrating a template against fictional data.
- Build instructions and usage guides for each template.
- Best-practice notes on layout, formula conventions, and auditability.
- Reference parameter sheets reused across templates (e.g. tax rates, formatting standards).

## What does NOT go here

- Populated, project-specific models (use `models/builds/`).
- Real source data — examples should use clearly fictional values (use `data/` for real data).
- Validation reports for models built from these templates (use `analysis/validation/`).
- Document templates such as memos or spec scaffolds (use `docs/templates/`).
- Personal copies of templates that have been modified for one-off use.
