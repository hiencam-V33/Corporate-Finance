# Builds

## Purpose

This directory contains populated, production-ready, and audited working models in their final or near-final state (Stage 3). All models here should be versioned, documented, and validated.

## What Belongs Here

- Completed, working financial models
- Models that have passed validation and audit
- Versioned model files with change history
- Model documentation and assumption summaries
- Model testing and validation records
- Change logs and version notes
- Supporting documentation and methodologies

## Naming Conventions

- **Build files:** `[ModelName]_v[Version]_[Date].xlsx`
  - Example: `DCF_Valuation_v3_2026-05-15.xlsx`
- **Final builds:** `[ModelName]_v[Version]_FINAL_[Date].xlsx`
  - Example: `DCF_v3_FINAL_2026-05-15.xlsx`
- **Change logs:** `CHANGELOG_[ModelName].md`
  - Example: `CHANGELOG_DCF.md`
- **Validation records:** `VALIDATION_[ModelName]_v[Version]_[Date].md`
  - Example: `VALIDATION_DCF_v3_2026-05-15.md`

## Getting Started

1. Ensure models are fully validated before placing here
2. Include complete change log with version history
3. Document model assumptions and methodologies
4. Link to validation reports in `/analysis/validation/`
5. Maintain version numbers for traceability

## Guidelines

- Only place audited, working models here
- Always include version number and date in file name
- Maintain complete change logs for each model
- Archive older versions rather than deleting
- Include README or documentation file for each major model
- Update change log when modifications are made
- Link to related specifications in `/docs/Specs/`
- Document any known limitations or assumptions
- Store supporting data files in `/data/`
