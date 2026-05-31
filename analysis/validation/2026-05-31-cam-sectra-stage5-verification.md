# Stage 5 — Manual Ratio Verification Table

**Author:** Hien Cam
**Date:** 2026-05-31
**Company:** Sectra AB (publ)
**Fiscal year:** FY2024/2025 (ending April 30, 2025)
**Source data:** `models/builds/2026-05-17-cam-sectra-financials.xlsx` (Stage 3 workbook) + Sectra Annual Report FY2024/2025 (pp. 92–94)
**LLM evaluated:** Google Gemini 2.5 Pro, executed against `docs/specs/2026-05-30-cam-sectra-spec.md`
**LLM output verified:** `deliverables/2026-05-31-cam-sectra-llm-raw.md`

## Purpose and method

This artifact recomputes seven ratios by hand from the Stage 3 financial-statement data and compares the manual values to the LLM's stated values. The Stage 3 workbook's auto-computed Ratios tab was used as a side sanity check on both columns during preparation, but the grading comparison shown in the table below is strictly **manual vs. LLM**.

Ratios are chosen across categories (Performance, Profitability, Efficiency, Liquidity, Du Pont input) and intentionally include ratios the LLM is most likely to get wrong: those involving start-of-year values, after-tax operating income (NOPAT), non-recurring strip-outs, adjusted-view sub-components, and data points the spec does not provide directly.

All figures in SEK thousand unless stated. Named-range notation follows the implemented `_curr` / `_prior` convention from Stage 4 spec Section 4.

## Verification table

| Ratio | Formula (named-range notation) | Manual value (show arithmetic) | LLM's value | Match? | One-line note |
|---|---|---|---:|:---:|---|
| **ROA (start-of-year)** | `currentYear_after_tax_operating_income / startYear_total_assets` | NOPAT = 563,371 + (1−0.206) × 28,120 = 585,698.28; ROA = 585,698.28 ÷ 3,210,938 = **18.24%** | 18.24% | ✓ | LLM correctly used NOPAT numerator and start-of-year denominator |
| **Asset Turnover** | `INC_sales / startYear_total_assets` | 3,239,811 ÷ 3,210,938 = **1.009×** | 1.009× | ✓ | Start-of-year denominator basis preserved; matches Du Pont input |
| **Economic Value Added (EVA)** | `currentYear_after_tax_operating_income − (cost_capital × startYear_total_capitalization)` | startYear_total_cap = 19,204 + 1,569,591 = 1,588,795. EVA = 585,698.28 − (0.09 × 1,588,795) = 585,698.28 − 142,991.55 = **442,706.73 (≈ 442,707)** | 442,707 | ✓ | LLM avoided averaging shortcut on capitalization base |
| **Underlying Operating Margin** | `(INC_ebit − non_recurring_patent_settlement) / INC_sales` | (722,997 − 110,000) ÷ 3,239,811 = 612,997 ÷ 3,239,811 = **18.92%** | 18.92% | ✓ | LLM correctly applied Validation Rule V-EBIT-1 strip-out; reported (22.32%) and underlying (18.92%) both disclosed |
| **Cash Ratio (standard)** | `currentYear_cash_marketable_securities / currentYear_liabilities_current` | 1,341,871 ÷ 1,701,450 = 0.7887 = **0.79×** | 0.79× | ✓ | — |
| **Adjusted Cash Ratio (excl. deferred revenue)** | `currentYear_cash_marketable_securities / (currentYear_liabilities_current − contract_liabilities_current)` *— `contract_liabilities_current` is NOT a named range in the spec* | LLM-used denominator 974,935 (from AR p. 92, not spec): 1,341,871 ÷ (1,701,450 − 974,935) = 1,341,871 ÷ 726,515 = **1.847×** | 1.85× | ✗ | Arithmetic ties, but LLM sourced the SEK 974,935 contract-liabilities figure from outside the spec — the spec only provides the aggregate `BAL_other_current_liabilities_curr` (1,570,554). Spec-discipline failure. |
| **DSO historical baseline check** | LLM-claimed "45–50 days" — no formula shown. Independent reference check from AR p. 92: `BAL_receivables_prior / (FY23/24_sales / 365)` *— FY23/24 sales is not in the spec or workbook; only available in AR* | FY23/24 daily sales = 2,963,607 ÷ 365 = 8,119.47. Proxy = 571,661 ÷ 8,119.47 = **70.4 days** | "45–50 days" (no formula) | ✗ | LLM hallucinated the historical baseline. The proxy uses a different convention (own-year sales) than the workbook's DSO formula (current-year sales × prior-year AR), so the two are **not strictly apples-to-apples** for trend computation — but the gap between 45–50 and 70.4 is too large to reconcile with any convention. Conclusion: the LLM's narrative that DSO "lengthened" is unsupported, and Hypothesis H1's direction must be re-examined in the final analysis. |

## Summary

| Outcome | Count | Implication |
|---|:---:|---|
| Arithmetic matches between manual and LLM | 5 of 7 graded comparisons | High analytical correctness when the spec provided complete input data |
| Discrepancy — LLM sourced input outside the spec | 2 of 7 (Adjusted Cash Ratio and DSO historical baseline) | Spec gap, not LLM error: spec did not break out `contract_liabilities` and did not prohibit external lookups |
| Hypothesis affected by external-sourcing | Hypothesis H1 (DSO trend direction) | Final analysis cannot rely on the LLM's H1 conclusion; must reframe using either workbook-only data or AR data with disclosed convention |

## Conclusions for downstream work

1. **Analytical correctness is high** for the five "in-spec" ratios (ROA, Asset Turnover, EVA, Underlying Operating Margin, Cash Ratio): every value ties to manual arithmetic and to the workbook's auto-computed Ratios tab.
2. **Spec discipline failures on the Adjusted Cash Ratio and the DSO historical baseline** are *spec gaps*, not LLM errors. The spec failed to (a) break out `contract_liabilities` as its own named range, and (b) explicitly direct the LLM to refuse external lookups when the spec is silent on a data point. Both gaps are documented in `deliverables/2026-05-31-cam-sectra-spec-retrospective.md`.
3. **Hypothesis H1 (DSO lengthening) is not supported by the data the spec contains.** The LLM's claim of a 45–50-day historical baseline does not appear in the spec or the workbook. An AR-based proxy (70.4 days) is methodologically distinct from the workbook's DSO formula and is presented in the DSO baseline-check row only as a falsification check on the LLM's hallucinated number, not as a definitive trend value. The final analysis (`deliverables/2026-05-31-cam-sectra-final-analysis.md`) reframes H1 around this finding rather than carrying the LLM's directional claim forward.
