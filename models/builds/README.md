# builds (models)

This directory holds Stage 3 model builds: populated, versioned, and validated workbooks that represent the working artifacts of the BUS 629 portfolio. Anything in `builds/` should be auditable end-to-end — every input traceable to a file in `data/`, every methodology choice traceable to a document in `docs/specs/`, every validation traceable to a report in `analysis/validation/`.

Builds are versioned, not overwritten. When a model is materially revised, save a new version and update the change log; keep older versions in place so the project's history is preserved.

## Naming conventions

- Working builds: `[ModelName]_v[N]_[YYYY-MM-DD].xlsx` (e.g. `DCF_Valuation_v3_2026-05-15.xlsx`).
- Signed-off final builds: `[ModelName]_v[N]_FINAL_[YYYY-MM-DD].xlsx`.
- Change logs: `CHANGELOG_[ModelName].md`, one per model.
- Validation links: `VALIDATION_[ModelName]_v[N]_[YYYY-MM-DD].md` (the report itself lives in `analysis/validation/`; a pointer file may live here).
- Use PascalCase for `[ModelName]`; never embed spaces in filenames.

## What goes here

- Populated working models that have passed initial review.
- Final, signed-off model versions.
- Change logs documenting what changed between versions and why.
- Model-level README files describing sheet layout, inputs, and outputs.
- Pointers (short markdown files) linking each build to its spec, data sources, and validation report.

## What does NOT go here

- Blank or template workbooks (use `models/templates/`).
- Scratch / experimental workbooks not yet ready for review.
- Raw input data used by the models (use `data/`).
- The methodology spec or assumption documents themselves (use `docs/specs/`).
- The validation reports themselves (use `analysis/validation/`).
- Exported PDFs, slide decks, or presentation outputs (use `deliverables/`).
