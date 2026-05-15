# Data

## Purpose

This directory contains source financial data, reference datasets, and complete provenance documentation for all data used in models and analysis.

## What Belongs Here

- Source financial data files (CSV, Excel, JSON)
- Reference data and lookup tables
- Data documentation and data dictionaries
- Provenance and source attribution notes
- Data extraction and transformation logs
- Change history and update records

## Naming Conventions

- **Source data files:** `[DataType]_[Source]_[Date].xlsx`
  - Example: `FinancialStatements_CompanyXYZ_2026-05-15.xlsx`
- **Reference data:** `REF_[Category].csv`
  - Example: `REF_ExchangeRates.csv`
- **Provenance notes:** `PROVENANCE_[DatasetName].md`
  - Example: `PROVENANCE_HistoricalRevenue.md`
- **Update logs:** `UPDATE_LOG_[DatasetName]_[Date].txt`
  - Example: `UPDATE_LOG_MarketData_2026-05-15.txt`

## Getting Started

1. Always include a PROVENANCE note with each new data file
2. Document the data source and extraction method
3. Note any transformations or calculations applied
4. Record the date of extraction and expected refresh date
5. Link to original source systems where applicable

## Guidelines

- Never modify source data files directly; create transformed versions instead
- Document all data transformations and business logic
- Maintain complete update history for audit purposes
- Include data quality notes and any known issues
- Keep file sizes reasonable; archive old versions
- Provide data dictionaries for complex datasets
