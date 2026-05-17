# specs

This directory holds technical and analytical specifications: the documents that define *how* models, datasets, and calculations are constructed. Specs are the contract between a decision and an implementation — they translate "we chose DCF" into "here are the assumptions, inputs, formulas, and outputs."

Specs are versioned because methodology evolves. When a spec changes materially, bump the version rather than overwriting, and link the new version back to the decision record that authorized the change.

## Naming conventions

- Model specs: `SPEC_[ModelName]_[Component]_v[N].md` (e.g. `SPEC_DCF_Assumptions_v2.md`).
- Data schema specs: `SPEC_DataSchema_[Entity]_v[N].md` (e.g. `SPEC_DataSchema_FinancialStatements_v1.md`).
- Methodology documents: `METHODOLOGY_[Process]_v[N].md`.
- Interface or integration specs: `SPEC_Interface_[System]_v[N].md`.
- Always use `v1`, `v2`, … (no leading zeros, no `v1.0`).

## What goes here

- Model architecture documents: assumptions, inputs, calculation flow, outputs.
- Data dictionaries and schema definitions for datasets in `data/`.
- Methodology write-ups (e.g. how WACC is calculated, how comps are selected).
- Acceptance criteria and validation rules for models and data.
- Worked numerical examples that anchor a calculation.

## What does NOT go here

- The Excel models themselves (use `models/builds/` or `models/templates/`).
- The raw data being described (use `data/`).
- The reason a methodology was chosen (use `docs/decisions/`).
- Project timelines or owner assignments (use `docs/plans/`).
- Validation results showing the spec was met (use `analysis/validation/`).
