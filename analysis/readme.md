# analysis

This directory contains the analytical work that operates *on* the models and data: validation reports, reconciliations, sensitivity tests, scenario analyses, and any other quantitative work whose purpose is to verify, stress, or interrogate a model rather than to build one.

The folder is currently organized around `validation/`, which houses Stage 3 model-validation reports and self-audits. Additional sub-folders (e.g. `sensitivity/`, `scenarios/`) may be added as the project grows; when in doubt, put a new analytical sub-discipline under `analysis/` rather than scattering it across `models/` or `docs/`.

## Naming conventions

- Validation reports: `VALIDATION_[ModelName]_v[N]_[YYYY-MM-DD].md`.
- Reconciliation files: `RECONCILIATION_[Component]_[YYYY-MM-DD].xlsx`.
- Sensitivity tests: `SENSITIVITY_[ModelName]_[Driver]_[YYYY-MM-DD].xlsx`.
- Scenario analyses: `SCENARIO_[ModelName]_[ScenarioName]_[YYYY-MM-DD].md`.
- Always tie the filename to the model version being analyzed.

## What goes here

- Stage 3 validation reports and self-audit documents.
- Reconciliations between model outputs and source data.
- Sensitivity and scenario analyses on existing models.
- Quantitative quality-assurance notes and findings.
- Methodology notes specific to an analytical technique (e.g. how a sensitivity grid was set up).

## What does NOT go here

- The models themselves (use `models/builds/`).
- The data the models consume (use `data/`).
- General methodology specs that describe model construction (use `docs/specs/`).
- Final, polished analysis output prepared for an audience (use `deliverables/`).
- Decision memos about which methodology to use (use `docs/decisions/`).
