# models

This directory contains all financial models built for the BUS 629 portfolio: Excel workbooks, supporting calculation files, and their accompanying documentation. Models are organized along the course's two-stage flow — `templates/` for blank, Stage 1 starter frameworks, and `builds/` for populated, validated, Stage 3 working models.

Every working model should be reproducible from its inputs and its spec. If a reader cannot rebuild the model from the documents in `docs/specs/` and the data in `data/`, the model is undocumented and not ready for `builds/`.

## Naming conventions

- Working model files: `[ModelName]_v[N]_[YYYY-MM-DD].xlsx` (e.g. `DCF_Valuation_v3_2026-05-15.xlsx`).
- Final / signed-off builds: `[ModelName]_v[N]_FINAL_[YYYY-MM-DD].xlsx`.
- Template files: `TEMPLATE_[ModelType].xlsx`.
- Change logs: `CHANGELOG_[ModelName].md`, kept beside the model.
- Use PascalCase for `[ModelName]`; do not use spaces in filenames.

## What goes here

- Stage 1 blank template workbooks (in `templates/`).
- Stage 3 populated, audited working models (in `builds/`).
- Change logs and version histories for each model.
- Model-level README files explaining inputs, sheet structure, and outputs.
- Lightweight calculation helpers (lookup tables, parameter sheets) used by the models.

## What does NOT go here

- Specifications describing the model's methodology (use `docs/specs/`).
- Raw or reference data that feeds the model (use `data/`).
- Validation reports and audit results for the model (use `analysis/validation/`).
- Final exported PDFs or presentations of model output (use `deliverables/`).
- Personal scratch workbooks or experiments not intended to be shared.
