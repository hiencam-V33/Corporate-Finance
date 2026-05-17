# data

This directory holds every dataset used in the BUS 629 portfolio: source financial statements, reference tables, downloaded extracts, and any transformed copies needed by the models. The non-negotiable rule for this folder is provenance — every file must have a PROVENANCE note explaining where it came from, when it was pulled, and how (if at all) it was transformed.

Source files are treated as immutable. If a dataset needs cleaning or reshaping, save the transformed version as a new file with a clear suffix and document the transformation, rather than editing the original.

## Naming conventions

- Source files: `[DataType]_[Source]_[YYYY-MM-DD].xlsx` (e.g. `FinancialStatements_CompanyXYZ_2026-05-15.xlsx`).
- Reference tables: `REF_[Category].csv` (e.g. `REF_ExchangeRates.csv`).
- Transformed copies: append `_clean`, `_normalized`, or `_v[N]` before the date.
- Provenance notes: `PROVENANCE_[DatasetName].md`, one per dataset.
- Update logs: `UPDATE_LOG_[DatasetName]_[YYYY-MM-DD].md`.

## What goes here

- Original source data files downloaded or exported from external systems.
- Reference tables and lookups (currencies, tax rates, industry codes).
- Transformed / cleaned versions of source data, clearly labeled.
- Provenance notes documenting source, retrieval method, retrieval date, and transformations.
- Data dictionaries for non-trivial schemas (paired with `SPEC_DataSchema_*` in `docs/specs/`).

## What does NOT go here

- Excel models or workbooks that compute on the data (use `models/`).
- Analysis or validation outputs computed from the data (use `analysis/`).
- Specifications describing the schema (use `docs/specs/`).
- Confidential or proprietary data without explicit authorization to commit.
- Personal scratch CSVs, throwaway exports, or files without a PROVENANCE note.
