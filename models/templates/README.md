# Model Templates

This directory contains blank model frameworks provided by the course instructor (Professor Adam Stauffer), not student-built. These templates standardize the modeling architecture across the entire BUS 629 VEMBA class so every student works from the same structural foundation.

## Current Templates

- **performance-ratios-template.xlsx** — 6 tabs: `Cover & Instructions`, `Legend`, `Income Statement`, `Balance Sheet`, `Cash Flow`, `Ratios`. Uses named-range conventions for cross-sheet references:
  - `INC_*` — Income Statement line items
  - `BAL_*` — Balance Sheet line items
  - `CASH_*` — Cash Flow Statement line items
  - `RATIO_*` — calculated performance ratios

## Color Conventions

- **Yellow** — Inputs (raw financial data entered from source filings)
- **Blue** — Assumptions (driver values that can be flexed)
- **Green** — Formulas (calculated cells, do not overwrite)
- **Gray** — Outputs (final reported figures and ratio results)

## Usage

Templates in this directory are kept **unmodified** during Stage 1 — treat them as read-only reference copies. When Stage 3 begins, copy the relevant template into `models/builds/` and populate it with the data of your assigned company. Never edit the originals here; the integrity of the shared framework depends on them staying clean.

## Source

Original template authored by Professor Adam Stauffer:
https://github.com/adamwstauffer/shidler/blob/main/docs/templates/spreadsheets/performance-ratios-template.xlsx
