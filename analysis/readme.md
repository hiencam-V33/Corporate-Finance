# Analysis

## Purpose

This directory contains financial validation, self-audit, and review work for corporate finance models and datasets.

## What Belongs Here

- Model validation reports and test results
- Reconciliation notes and audit trails
- Self-audit documentation
- Data verification scripts and results
- Sensitivity analysis outputs
- Scenario testing reports

## Directory Structure

- `validation/` — Stage 3 validation reports, test results, and reconciliation notes

## Naming Conventions

- **Validation reports:** `VALIDATION_[ModelName]_[Date].md` (e.g., `VALIDATION_DCF_2026-05-15.md`)
- **Audit files:** `AUDIT_[Component]_[Date].xlsx` (e.g., `AUDIT_Assumptions_2026-05-15.xlsx`)
- **Test results:** `TEST_[Scenario]_[Date].csv` (e.g., `TEST_SensitivityAnalysis_2026-05-15.csv`)

## Getting Started

1. Review the subdirectory READMEs for specific naming and organizational patterns
2. Include test methodology and assumptions in all validation documents
3. Link validation reports back to the models they validate
4. Maintain clear audit trails for reproducibility

## Guidelines

- Document all test assumptions and methodologies
- Include timestamp and version references
- Keep validation notes linked to source data and models
- Archive completed validations by date or project phase