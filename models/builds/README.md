# models/builds

Populated Excel workbooks built from the course-provided template. This is where the Stage 3 data-entry work lives.

## What's in here

- **`2026-05-17-cam-sectra-financials.xlsx`** — Stage 3 populated workbook for Sectra AB (publ) FY2024/2025 with prior-year comparatives. Income Statement, Balance Sheet, and Cash Flow tabs sourced line-by-line from Sectra's Annual Report 2024/2025 (pp. 92–94 for primary statements). The Ratios tab auto-computes Performance, Profitability, Efficiency, Leverage, Liquidity, and Du Pont ratios via formulas referencing 79 named ranges defined on the Cover sheet.

## Key outputs from this workbook

The numbers downstream deliverables anchor to:

- **Performance:** EVA SEK 442,707K (at 9% WACC), MVA SEK 55,228,352K, M/B 29.81×
- **Profitability:** Reported operating margin 22.32% (incl. SEK 110M patent settlement), underlying 18.92%; ROA 18.24% (start-of-year basis); ROE 35.89%; Net Profit Margin 17.39%
- **Efficiency:** Asset Turnover 1.009× (start-of-year basis); DSO 64.40 days
- **Leverage:** Total Debt Ratio 48.97% (misleading — driven by deferred revenue); Long-term Debt Ratio 3.22% (the structural figure)
- **Liquidity:** Cash Ratio 0.79× (standard); Adjusted Cash Ratio 1.85× (excluding contract liabilities)
- **Du Pont:** 3-factor ROE 35.89% = 17.39% × 1.009 × 2.046; 4-factor 34.38% (template construction)
- **Cash conversion:** CFO / Net Income 1.64× (audited); template-computed CFO 839,295 reconciles to audited 922,364 by 83,069 unmapped working-capital items

## IFRS-specific conventions to be aware of

Sectra reports under IFRS as adopted in the EU. Three structural choices affect ratio interpretation:

1. **By-nature income statement** — Operating expenses presented by nature (personnel, other external costs) rather than by function (COGS, SG&A). The line mapped to `INC_cost_goods_sold` is "Goods for resale" only (SEK 441,712K, third-party hardware), not a full COGS. Standard gross-margin computations therefore yield an inflated, non-meaningful ~86%. Operating margin is the reliable profitability baseline.
2. **Deferred revenue / contract liabilities** — Current contract liabilities of SEK 974,935K (from AR p. 92) inflate the Total Debt Ratio and Current Liabilities denominators. The Adjusted Cash Ratio strips this out.
3. **Patent settlement non-recurring item** — Reported FY2024/2025 operating profit of SEK 722,997K includes a SEK 110M patent settlement gain. Underlying EBIT is SEK 612,997K. Trend commentary uses the underlying figure unless otherwise noted.

These are documented in detail in [`docs/specs/2026-05-30-cam-sectra-spec.md`](../../docs/specs) (Sections 2 and 4) and [`deliverables/2026-05-31-cam-sectra-final-analysis.md`](../../deliverables) (Section 1).

## Stage 3 PR review outcome

Scored 99% (8.91 / 9) with positive feedback across all four criteria: balance-sheet balance, named-range population, documentation completeness, and ratio resolution. No revisions required at Stage 5; see [`docs/decisions/2026-05-31-cam-stage2-feedback-response.md`](../../docs/decisions) for the documented response.

## Naming convention

Files follow `YYYY-MM-DD-{lastname}-{company-slug}-financials.xlsx` per the project-wide convention.

## How this folder fits the project

This workbook is the source-of-truth that every downstream artifact references. The Stage 4 spec quotes its formulas; the Stage 5 LLM execution computes against its named ranges; the Stage 5 verification table re-derives a subset of its ratios by hand. If any number in any downstream deliverable doesn't tie back to a cell in this workbook, that's a bug.
