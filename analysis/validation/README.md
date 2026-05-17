# validation

This directory holds Stage 3 model validation artifacts: self-audit reports, reconciliations against source data, acceptance-criteria checks, and the supporting evidence behind each pass/fail conclusion. A model in `models/builds/` is not considered complete until it has a corresponding validation report here.

Each validation report should be reproducible. Anyone reading it should be able to point to the exact model version it covers, the data inputs that were used, the tests that were run, and the criteria the model was judged against.

## Naming conventions

- Validation reports: `VALIDATION_[ModelName]_v[N]_[YYYY-MM-DD].md` (e.g. `VALIDATION_DCF_v3_2026-05-15.md`).
- Reconciliation worksheets: `RECONCILIATION_[ModelName]_[Component]_[YYYY-MM-DD].xlsx`.
- Audit logs: `AUDITLOG_[Subject]_[YYYY-MM-DD]_to_[YYYY-MM-DD].md`.
- Sign-off records: `SIGNOFF_VALIDATION_[ModelName]_v[N]_[YYYY-MM-DD].md`.
- Always reference the specific model version (`v[N]`) being validated.

## What goes here

- Validation reports with methodology, test cases, results, and pass/fail conclusions.
- Reconciliations between model output and source data or independent calculations.
- Audit trails recording who reviewed what and when.
- Lists of known issues, deviations, and accepted limitations.
- Sign-off records confirming a model has been validated for use.

## What does NOT go here

- The model files being validated (use `models/builds/`).
- The data being reconciled against (use `data/`).
- The specification describing how the model should behave (use `docs/specs/`).
- Sensitivity or scenario analyses run on a validated model (use `analysis/` directly).
- Final externally-facing reports summarizing validation outcomes (use `deliverables/`).
