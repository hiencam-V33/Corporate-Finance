# Specs

## Purpose

This directory contains technical specifications, model assumptions, data schemas, and design documentation that define how systems and models are built and operated.

## What Belongs Here

- Model architecture and assumptions documentation
- Data schema and structure specifications
- Technical interface and API specifications
- Input and output specifications
- Calculation methodologies and formulae
- System design and integration notes
- Business logic specifications

## Naming Conventions

- **Model specs:** `SPEC_[ModelName]_[Component]_v[Version].md`
  - Example: `SPEC_DCF_Assumptions_v2.md`
- **Data specs:** `SPEC_DataSchema_[Entity]_v[Version].md`
  - Example: `SPEC_DataSchema_FinancialStatements_v1.md`
- **Interface specs:** `SPEC_Interface_[SystemName]_v[Version].md`
  - Example: `SPEC_Interface_DataImport_v1.md`
- **Methodology docs:** `METHODOLOGY_[Process]_v[Version].md`
  - Example: `METHODOLOGY_CashFlowCalculation_v1.md`

## Getting Started

1. Document all assumptions in model specifications
2. Include calculations and formulae explicitly
3. Define data inputs, outputs, and validation rules
4. Version all specifications
5. Update when assumptions or methodology changes

## Guidelines

- Be precise and explicit; avoid ambiguity
- Include worked examples for complex calculations
- Document dependencies between specifications
- Link to related plans and decisions
- Maintain version control; archive superseded specs
- Keep specifications current with actual implementations
- Include acceptance criteria for testing
