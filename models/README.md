# Models

## Purpose

This directory contains Excel financial models, analytical frameworks, and model-related documentation organized into templates (stage 1) and builds (stage 3).

## Directory Structure

- `templates/` — Blank model frameworks and starter workbooks (Stage 1)
- `builds/` — Populated, versioned, and audited working models (Stage 3)

## What Belongs Here

- Financial modeling workbooks (Excel, Google Sheets)
- Blank model templates and frameworks
- Working, production models with full documentation
- Model change logs and version history
- Model specifications and assumptions
- Supporting calculation guides

## Naming Conventions

- **Model files:** `[ModelName]_[Version]_[Date].xlsx`
  - Example: `DCF_Valuation_v3_2026-05-15.xlsx`
- **Template files:** `TEMPLATE_[ModelType].xlsx`
  - Example: `TEMPLATE_CashFlow_Projection.xlsx`
- **Build archives:** `[ModelName]_v[Version]_FINAL_[Date].xlsx`
  - Example: `DCF_v3_FINAL_2026-05-15.xlsx`
- **Change logs:** `CHANGELOG_[ModelName].txt`
  - Example: `CHANGELOG_DCF.txt`

## Getting Started

1. Start with a template from `templates/` for new models
2. Read the template documentation before building
3. Document assumptions as you build
4. Validate results before moving to builds/
5. Archive completed models with version numbers

## Guidelines

- Keep model structure clean and auditable
- Separate inputs, calculations, and outputs
- Document all assumptions and methodologies
- Version control all models
- Maintain change logs for tracking updates
- Test models thoroughly before archiving
- Keep templates up-to-date with best practices
