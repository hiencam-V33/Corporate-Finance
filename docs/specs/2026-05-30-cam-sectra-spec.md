---
template: spec
purpose: "Technical specification for Sectra AB (publ) accounting & performance ratios analysis — defines the Excel ratio model, populated FY2024/2025 inputs, derived inputs, ratio formulas in named-range notation, validation rules, and the analytical work an LLM is to produce at Stage 5."
audience: student
fields_required: [title, author, date, version, company, scope, model_architecture, data_inputs, derived_inputs, formulas, validation, analysis_requirements, output_format, references]
naming_convention: "YYYY-MM-DD-{slug}.md"
courses: [BUS-629]
stage: "Stage 4"
company: "Sectra AB (publ)"
ticker: "SECT B"
exchange: "Nasdaq Stockholm (Large Cap)"
reporting_standard: "IFRS (audited consolidated)"
reporting_currency: "SEK thousand"
fiscal_year_current: "FY2024/2025 (May 1, 2024 – April 30, 2025)"
fiscal_year_prior: "FY2023/2024 (May 1, 2023 – April 30, 2024)"
model_workbook: "models/builds/2026-05-17-cam-sectra-financials.xlsx"
template_workbook: "models/templates/performance-ratios-template.xlsx"
---

# Technical Specification — Sectra AB (publ) Accounting & Performance Ratios Analysis

**Author:** Hien Cam
**Date:** 2026-05-30
**Version:** 1.0
**Company:** Sectra AB (publ) · SECT B · Nasdaq Stockholm (Large Cap)

---

## 1. Scope & Objective

This specification defines (a) the Excel ratio model populated for Sectra AB in `models/builds/2026-05-17-cam-sectra-financials.xlsx` and (b) the analytical deliverable to be produced from that model at Stage 5. It is written to be self-contained: an LLM with no other context, given only this spec, must be able to verify the ratios and produce a substantively correct analysis.

- **Company:** Sectra AB (publ), Swedish medical-imaging IT and secure-communications vendor headquartered in Linköping.
- **Fiscal period:** Current = FY2024/2025 (year ending April 30, 2025). Prior = FY2023/2024 (year ending April 30, 2024). Sectra's fiscal year is May–April, not calendar.
- **Reporting standard:** IFRS, audited consolidated financial statements.
- **Reporting currency:** Swedish krona (SEK), all figures in **SEK thousand** unless otherwise stated. Market capitalization is computed in SEK thousand so it ties to the financial-statement tabs.
- **Analytical objective:** Compute and interpret 25+ performance, profitability, efficiency, leverage, liquidity, and Du Pont ratios; test the three Stage 2 hypotheses (working-capital reshape, profitability compression, cash-conversion strength); deliver 3–5 strategic recommendations.
- **Intended audience:** Professor Adam W. Stauffer (instructor, BUS-629) as primary; secondary audience is a corporate-finance peer reader (EMBA cohort) and Sectra's investor-relations team as the implied "executive" reader of the recommendations.

---

## Part A — Model Specification

### 2. Model Architecture

The workbook has **six tabs**, all single-currency (SEK thousand), built on the BUS-629 single-period (current vs prior) ratio template.

| # | Tab | Role | Contents |
|---|-----|------|----------|
| 1 | `Cover` | Reference | Brand header, usage instructions, color key, named-range convention table. Read-only. |
| 2 | `Balance Sheet` | Data input | Two-column layout (Assets left, Liabilities & Equity right). Columns C/D = FY Current / FY Prior assets; columns G/H = FY Current / FY Prior L&E. Yellow cells = inputs. |
| 3 | `Income Statement` | Data input | Single-year (current). Column C = SEK amount; column D = % of sales (formula-driven). Yellow cells = inputs. |
| 4 | `Cash Flow Statement` | Data input + derived | Indirect-method CFO built from Net Income + Depreciation ± Δ working capital; investing and financing as direct inputs. Some cells pull from named ranges. |
| 5 | `Ratios` | Calculation + output | Three sections: (a) four analyst assumptions and market cap at top, (b) derived inputs block (start-of-year, current-year, averages), (c) ratio outputs block by category. Gray cells = ratio outputs (do not overwrite). |
| 6 | `Notes` | Documentation | Company metadata, sources, IFRS-specific conventions, COGS-by-nature limitation, CFO method note, dividend note, Du Pont self-check explanation. |

**Color and style conventions** (Cover sheet R16–R22):
- **Yellow background** = DATA INPUT (overwrite with company figures).
- **Light-blue background + blue text** = ASSUMPTION (analyst inputs: share price, shares outstanding, WACC, tax rate, fiscal years).
- **Green text** = FORMULA (cross-sheet references, derived calculations; do not overwrite).
- **Gray background** = RATIO OUTPUT (computed; do not overwrite).

**Data flow:** Inputs on `Balance Sheet` + `Income Statement` + `Cash Flow Statement` → named ranges → `Ratios` derived block (rows 14–38) → `Ratios` output block (rows 42–76). The Du Pont self-check on `Ratios!F75` confirms `Du Pont ROA = Direct ROA` at six-decimal precision.

### 3. Data Inputs

All values stated explicitly in SEK thousand. Year suffix convention in this workbook is `_curr` (FY2024/2025) and `_prior` (FY2023/2024); these aliases are driven by `yearCurrent = 2024` on `Ratios!C6` (interpreted by Sectra as "FY ending in 2024/25"). The current/prior aliases are used in all formulas below.

**Balance Sheet — Current Assets** (`'Balance Sheet'!C7:C11` curr; `D7:D11` prior)

| Named Range | Line Item | FY24/25 (curr) | FY23/24 (prior) |
|-------------|-----------|---------------:|----------------:|
| `BAL_cash_marketable_securities_curr` / `_prior` | Cash & marketable securities | 1,341,871 | 804,640 |
| `BAL_receivables_curr` / `_prior` | Receivables (trade) | 572,036 | 571,661 |
| `BAL_inventories_curr` / `_prior` | Inventories | 37,576 | 36,590 |
| `BAL_other_current_assets_curr` / `_prior` | Other current assets (contract assets, prepaid, derivatives, other receivables) | 1,007,648 | 1,109,257 |
| `BAL_assets_current_curr` / `_prior` | **Total current assets** (=SUM above) | **2,959,131** | **2,522,148** |

**Balance Sheet — Fixed & Other Assets** (`'Balance Sheet'!C14:C23` curr; `D14:D23` prior)

| Named Range | Line Item | FY24/25 | FY23/24 |
|-------------|-----------|---------:|---------:|
| `BAL_ppe_gross_curr` / `_prior` | Property, plant & equipment (net of accum. depreciation, already net per Sectra disclosure) | 220,654 | 227,040 |
| `BAL_accumulated_depreciation_curr` / `_prior` | Less accumulated depreciation (0 — already netted upstream) | 0 | 0 |
| `BAL_fixed_assets_net_curr` / `_prior` | Net tangible fixed assets (= ppe_gross − accum_dep) | 220,654 | 227,040 |
| `BAL_intangibles_curr` / `_prior` | Intangible assets (goodwill + capitalized R&D + customer relationships, IAS 38) | 283,063 | 262,330 |
| `BAL_other_assets_curr` / `_prior` | Other assets (deferred tax, lease ROU, financial assets, other LT) | 293,381 | 199,420 |
| `BAL_assets_total_curr` / `_prior` | **Total assets** | **3,756,229** | **3,210,938** |

**Balance Sheet — Current Liabilities** (`'Balance Sheet'!G7:G10` curr; `H7:H10` prior)

| Named Range | Line Item | FY24/25 | FY23/24 |
|-------------|-----------|---------:|---------:|
| `BAL_debt_short_term_curr` / `_prior` | Short-term debt (current portion of borrowings + lease) | 23,617 | 12,584 |
| `BAL_accounts_payable_curr` / `_prior` | Trade payables | 107,279 | 76,071 |
| `BAL_other_current_liabilities_curr` / `_prior` | Other current liabilities (contract liabilities = deferred revenue + accrued + tax payable + derivatives + other) | 1,570,554 | 1,500,108 |
| `BAL_liabilities_current_curr` / `_prior` | **Total current liabilities** (=SUM above) | **1,701,450** | **1,588,763** |

**Balance Sheet — Long-Term Liabilities** (`'Balance Sheet'!G12:G15` curr; `H12:H15` prior)

| Named Range | Line Item | FY24/25 | FY23/24 |
|-------------|-----------|---------:|---------:|
| `BAL_debt_long_term_curr` / `_prior` | Long-term debt (non-current borrowings + lease liability) | 63,840 | 19,204 |
| `BAL_other_long_term_liabilities_curr` / `_prior` | Other long-term liabilities (provisions, deferred tax, non-current contract liabilities) | 74,114 | 33,380 |
| `BAL_liabilities_total_curr` / `_prior` | **Total liabilities** (= current + LT debt + other LT) | **1,839,404** | **1,641,347** |

**Balance Sheet — Shareholders' Equity** (`'Balance Sheet'!G18:G23` curr; `H18:H23` prior)

| Named Range | Line Item | FY24/25 | FY23/24 |
|-------------|-----------|---------:|---------:|
| `BAL_common_stock_curr` / `_prior` | Common stock + paid-in capital | 400,495 | 400,295 |
| `BAL_retained_earnings_curr` / `_prior` | Retained earnings + reserves | 1,516,330 | 1,169,296 |
| `BAL_equity_shareholders_curr` / `_prior` | **Total shareholders' equity** | **1,916,825** | **1,569,591** |
| — | Total liabilities + equity (must equal total assets) | **3,756,229** | **3,210,938** |

**Income Statement — Current Year Only** (`'Income Statement'!C6:C19`)

| Named Range | Line Item | FY24/25 | % of sales |
|-------------|-----------|---------:|----------:|
| `INC_sales` | Net sales | 3,239,811 | 100.00% |
| `INC_cost_goods_sold` | "Goods for resale" (sole IFRS-by-nature line mapping to COGS — see §6) | 441,712 | 13.63% |
| `INC_sga` | Selling, general & administrative (Personnel + Other external − D&A reclassed) | 1,963,572 | 60.61% |
| `INC_depreciation` | Depreciation & amortization (PP&E + intangibles + ROU) | 111,530 | 3.44% |
| `INC_ebit` | **EBIT (operating profit, reported)** | **722,997** | **22.32%** |
| `INC_other_income` | Other income (financial income) | 31,404 | 0.97% |
| `INC_interest_expense` | Interest expense (financial costs) | 28,120 | 0.87% |
| `INC_taxable_income` | Taxable income (= EBIT + Other inc − Int exp) | 726,281 | 22.42% |
| `INC_taxes` | Income tax | 162,910 | 5.03% |
| `INC_net` | **Net income** | **563,371** | **17.39%** |
| `INC_dividends` | Allocation: proposed dividend (board proposal to AGM 2025: SEK 1.10 ord + 1.00 extra = 2.10/share) | 404,602 | 12.49% |
| `INC_addition_retained_earnings` | Allocation: addition to retained earnings | 158,769 | 4.90% |

**Cash Flow Statement — Current Year** (`'Cash Flow Statement'!C7:C32`)

| Named Range | Line Item | FY24/25 |
|-------------|-----------|---------:|
| (pulls `INC_net`) | Net income | 563,371 |
| (pulls `INC_depreciation`) | Depreciation | 111,530 |
| — | Δ Receivables | −16,367 |
| — | Δ Inventories | −1,108 |
| — | Δ Other current assets | 0 |
| — | Δ Accounts payable | 0 |
| — | Δ Other current liabilities | 181,869 |
| — | Total change in working capital | 164,394 |
| `CASH_operating` | **Cash provided by operations (template, indirect)** | **839,295** |
| — | Capital expenditures | −109,992 |
| — | Sales (acquisitions) of long-term assets | −3,872 |
| `CASH_investments` | **Cash used for investments** | **−113,864** |
| — | Δ long-term debt | −39,950 |
| — | Share redemption (in lieu of cash dividend, prior cycle) | −211,935 |
| — | **Cash used for financing** | **−251,885** |
| — | Net increase in cash | 473,546 |

**Note on CFO:** This template's indirect-method CFO (`CASH_operating` = SEK 839,295K) differs from Sectra's audited Consolidated Cash-Flow Statement (SEK 922,364K) by SEK 83,069K because Sectra starts from Operating profit and includes broader non-cash adjustments (provisions, unrealized FX) of SEK 179,581K vs depreciation alone of SEK 111,530K, plus cash-basis interest and tax. All individual working-capital line items in the template tie exactly to Sectra's audited statement (Annual Report p.93). For ratio purposes use `CASH_operating` = 839,295. For "cash conversion" hypothesis testing, also reference Sectra's audited CFO of 922,364 explicitly.

**Analyst Assumptions** (`Ratios!C6:C11`, light-blue cells)

| Named Range | Item | Value | Source |
|-------------|------|------:|--------|
| `yearCurrent` | Current fiscal-year tag | 2024 | Stage-3 convention |
| `yearStart` | Prior fiscal-year tag | 2023 (=`yearCurrent` − 1) | Formula |
| `share_price` | Closing share price on balance-sheet date | SEK 296.60 | Annual Report p.55–56 (April 30, 2025) |
| `shares_outstanding` | Shares outstanding (thousands), ex-treasury | 192,667.489 | Annual Report p.55, p.122 |
| `cost_capital` | WACC (≈ cost of equity given minimal debt) | 0.09 (9.0%) | CAPM: Rf 2.76% + β 1.15 × ERP 5.5% = 9.09% |
| `tax_rate` | Statutory CIT (Sweden) | 0.206 (20.6%) | Skatteverket statutory rate |
| `market_capitalization` | (=`share_price`×`shares_outstanding`) | 57,145,177 | Derived |

### 4. Named Range Conventions

Every named range in this workbook follows the conventions on the Cover sheet (R23–R32). An LLM executing the analysis must use named-range notation in all formulas — not cell addresses.

| Pattern | Meaning | Example |
|---------|---------|---------|
| `BAL_[item]_curr` | Balance-sheet line item, current fiscal year (FY24/25) | `BAL_assets_total_curr` = 3,756,229 |
| `BAL_[item]_prior` | Balance-sheet line item, prior fiscal year (FY23/24) | `BAL_equity_shareholders_prior` = 1,569,591 |
| `INC_[item]` | Income-statement item, current year only | `INC_sales`, `INC_ebit`, `INC_net` |
| `CASH_[item]` | Cash-flow item, current year only | `CASH_operating`, `CASH_investments` |
| `share_price`, `shares_outstanding`, `cost_capital`, `tax_rate`, `market_capitalization` | Analyst assumptions / market data (no prefix) | — |
| `yearCurrent`, `yearStart` | Year tags (driven by `Ratios!C6`) | 2024, 2023 |
| `startYear_[item]` | Alias for prior-year balance, used in turnover/return formulas where opening balance is correct | `startYear_equity` ≡ `BAL_equity_shareholders_prior` |
| `currentYear_[item]` | Alias for current-year balance or current-year derived figure | `currentYear_assets_total` ≡ `BAL_assets_total_curr` |
| `avg_[item]` | Mean of start-of-year and current-year balances | `avg_equity` = AVERAGE(`startYear_equity`, `currentYear_equity`) |
| `RATIO_[name]` | Key intermediate ratios reused inside the Du Pont decomposition | `RATIO_asset_turnover`, `RATIO_operating_profit_margin`, `RATIO_leverage`, `RATIO_debt_burden` |

**Convention deviation to be aware of.** The Cover sheet documents the pattern as `BAL_[item]_[yr]` with a literal year suffix (e.g., `BAL_assets_total_2024`). The workbook actually implements `_curr` / `_prior` aliases instead, driven by the `yearCurrent` cell. This is functionally equivalent for a single-period model but should be called out explicitly so a Stage 5 LLM does not search for non-existent `_2024` / `_2025` named ranges. The analysis writer must use the `_curr` / `_prior` form.

### 5. Derived Inputs

All derived inputs live on the `Ratios` tab and are computed by Excel formulas in named-range notation. They are listed here with formula and FY24/25 value so any executor can re-derive them.

**Start-of-Year (prior-year balance sheet) block** (`Ratios!C15:C19`)

| Named Range | Formula | Value (SEK thousand) |
|-------------|---------|---------------------:|
| `startYear_equity` | `= BAL_equity_shareholders_prior` | 1,569,591 |
| `startYear_inventory` | `= BAL_inventories_prior` | 36,590 |
| `startYear_receivables` | `= BAL_receivables_prior` | 571,661 |
| `startYear_total_assets` | `= BAL_assets_total_prior` | 3,210,938 |
| `startYear_total_capitalization` | `= BAL_debt_long_term_prior + BAL_equity_shareholders_prior` | 1,588,795 |

**Current-Year derived block** (`Ratios!C22:C33`)

| Named Range | Formula | Value |
|-------------|---------|------:|
| `currentYear_after_tax_operating_income` | `= INC_net + (1 − tax_rate) × INC_interest_expense` | 585,698.28 |
| `currentYear_daily_sales_average` | `= INC_sales / 365` | 8,876.19 |
| `currentYear_equity` | `= BAL_equity_shareholders_curr` | 1,916,825 |
| `currentYear_cash_marketable_securities` | `= BAL_cash_marketable_securities_curr` | 1,341,871 |
| `currentYear_assets_current` | `= BAL_assets_current_curr` | 2,959,131 |
| `currentYear_liabilities_current` | `= BAL_liabilities_current_curr` | 1,701,450 |
| `currentYear_cost_goods_sold_daily` | `= INC_cost_goods_sold / 365` | 1,210.17 |
| `currentYear_debt_long_term` | `= BAL_debt_long_term_curr` | 63,840 |
| `currentYear_working_capital_net` | `= BAL_assets_current_curr − BAL_liabilities_current_curr` | 1,257,681 |
| `currentYear_assets_total` | `= BAL_assets_total_curr` | 3,756,229 |
| `currentYear_total_capitalization` | `= currentYear_debt_long_term + currentYear_equity` | 1,980,665 |
| `currentYear_liabilities_total` | `= BAL_liabilities_total_curr` | 1,839,404 |

**Average (mixed-year) block** (`Ratios!C36:C38`)

| Named Range | Formula | Value |
|-------------|---------|------:|
| `avg_equity` | `= AVERAGE(startYear_equity, currentYear_equity)` | 1,743,208 |
| `avg_total_assets` | `= AVERAGE(startYear_total_assets, currentYear_assets_total)` | 3,483,583.5 |
| `avg_total_capitalization` | `= AVERAGE(startYear_total_capitalization, currentYear_total_capitalization)` | 1,784,730 |

### 6. Ratio Definitions & Formulas

All ratios are stated in named-range notation. The FY24/25 computed value is from the populated workbook so any LLM can verify rather than recompute. Where the ratio has an interpretation caveat under IFRS-by-nature reporting or Sectra-specific items, the caveat is noted.

**Performance** (`Ratios!C43:C45`)

| Ratio | Formula (named-range) | Unit | FY24/25 value | Interpretation |
|-------|----------------------|------|--------------:|----------------|
| Market Value Added (MVA) | `market_capitalization − currentYear_equity` | SEK thousand | 55,228,352 | Wealth created above book equity. Positive and very large reflects SaaS-style premium pricing. |
| Market-to-Book | `market_capitalization / currentYear_equity` | × | 29.81× | Equity multiple. Compare to Pro Medicus (≈80×+, pure SaaS) and Agfa Healthcare (asset-heavy <2×). |
| Economic Value Added (EVA) | `currentYear_after_tax_operating_income − (cost_capital × startYear_total_capitalization)` | SEK thousand | 442,707 | Operating profit in excess of cost of capital on opening capital. Positive = value creation. |

**Profitability** (`Ratios!C47:C52`) — both start-of-year and average-balance variants are reported.

| Ratio | Formula | Unit | FY24/25 |
|-------|---------|------|--------:|
| ROA (start-of-year) | `currentYear_after_tax_operating_income / startYear_total_assets` | % | 18.24% |
| ROC (start-of-year) | `currentYear_after_tax_operating_income / startYear_total_capitalization` | % | 36.86% |
| ROE (start-of-year) | `INC_net / startYear_equity` | % | 35.89% |
| ROA (avg) | `currentYear_after_tax_operating_income / avg_total_assets` | % | 16.81% |
| ROC (avg) | `currentYear_after_tax_operating_income / avg_total_capitalization` | % | 32.82% |
| ROE (avg) | `INC_net / avg_equity` | % | 32.32% |

**Efficiency** (`Ratios!C54:C60`)

| Ratio | Formula | Unit | FY24/25 |
|-------|---------|------|--------:|
| Asset turnover | `INC_sales / startYear_total_assets` | × | 1.009× |
| Receivables turnover | `INC_sales / startYear_receivables` | × | 5.67× |
| Average collection period (DSO) | `startYear_receivables / currentYear_daily_sales_average` | days | 64.4 |
| Inventory turnover | `INC_cost_goods_sold / startYear_inventory` | × | 12.07× |
| Days in inventory | `startYear_inventory / currentYear_cost_goods_sold_daily` | days | 30.2 |
| Profit margin | `INC_net / INC_sales` | % | 17.39% |
| Operating profit margin (`RATIO_operating_profit_margin`) | `currentYear_after_tax_operating_income / INC_sales` | % | 18.08% |

**Caveat — Inventory turnover & gross margin under IFRS-by-nature reporting (Notes R47–R67).** Sectra reports income by nature (IFRS), not by function (US GAAP). `INC_cost_goods_sold` here is **only** "Goods for resale" (the hardware Sectra resells), the sole line that maps cleanly. Personnel costs (SEK 1,598,697K) contain the implementation/support effort that would sit in COGS under by-function reporting, but Sectra does not disclose the split. Consequently: (a) Inventory turnover is reliable but reflects only hardware throughput; (b) any computed "Gross Margin" would appear unrealistically high (~86%) and is **not** meaningful for Sectra. **Operating profit margin is the reliable profitability gauge for this company.**

**Leverage** (`Ratios!C62:C68`)

| Ratio | Formula | Unit | FY24/25 |
|-------|---------|------|--------:|
| Long-term debt ratio | `currentYear_debt_long_term / (currentYear_debt_long_term + currentYear_equity)` | % | 3.22% |
| Long-term debt-equity ratio | `currentYear_debt_long_term / currentYear_equity` | × | 0.033× |
| Total debt ratio | `currentYear_liabilities_total / currentYear_assets_total` | % | 48.97% |
| Times interest earned | `INC_ebit / INC_interest_expense` | × | 25.71× |
| Cash coverage | `(INC_ebit + INC_depreciation) / INC_interest_expense` | × | 29.68× |
| Debt burden (`RATIO_debt_burden`) | `INC_net / currentYear_after_tax_operating_income` | × | 0.962 |
| Leverage (`RATIO_leverage`) | `currentYear_assets_total / currentYear_equity` | × | 1.96× |

**Caveat.** The high Total-debt ratio (48.97%) is misleading: only SEK 87,457K of liabilities is interest-bearing debt (short + long term); the rest is non-interest-bearing operating liabilities, dominated by **contract liabilities (deferred revenue)** of SEK 974,935K (current) + SEK 26,342K (non-current). For Sectra, long-term debt ratio (3.22%) is the correct gauge of financial leverage.

**Liquidity** (`Ratios!C70:C73`)

| Ratio | Formula | Unit | FY24/25 |
|-------|---------|------|--------:|
| Net working capital to assets | `currentYear_working_capital_net / currentYear_assets_total` | % | 33.48% |
| Current ratio | `currentYear_assets_current / currentYear_liabilities_current` | × | 1.74 |
| Quick ratio | `(currentYear_cash_marketable_securities + BAL_receivables_curr) / currentYear_liabilities_current` | × | 1.12 |
| Cash ratio | `currentYear_cash_marketable_securities / currentYear_liabilities_current` | × | 0.79 |

**Du Pont System** (`Ratios!C75:C76`)

| Ratio | Formula | Unit | FY24/25 |
|-------|---------|------|--------:|
| Du Pont ROA | `RATIO_asset_turnover × RATIO_operating_profit_margin` | % | 18.24% (✓ matches direct ROA) |
| Du Pont ROE | `RATIO_leverage × RATIO_asset_turnover × RATIO_operating_profit_margin × RATIO_debt_burden` | % | 34.38% |

### 7. Validation Rules

Any executor must verify the following before publishing the analysis. Any failure is a stop-the-line condition.

1. **Balance-sheet balance.** `BAL_assets_total_curr` must equal `BAL_liabilities_total_curr + BAL_equity_shareholders_curr`. Workbook: 3,756,229 = 1,839,404 + 1,916,825 ✓. Prior year: 3,210,938 = 1,641,347 + 1,569,591 ✓.
2. **Du Pont ROA self-check.** `Ratios!F75` displays `✓ matches direct ROA` when ROUND(Du Pont ROA, 6) = ROUND(Direct ROA, 6). Workbook returns ✓ — Du Pont ROA = Direct ROA = 18.2407%.
3. **Du Pont ROE time-mismatch (acceptable, explain).** Du Pont ROE (34.38%) will NOT equal Direct ROE (35.89%). This is by design of the template: `RATIO_leverage` uses current-year balances (`currentYear_assets_total / currentYear_equity`) while `RATIO_asset_turnover` uses start-of-year assets. The Stage 5 narrative must explain the time-mismatch in one sentence rather than treat it as an error.
4. **Income-statement subtotals.** `INC_ebit` = `INC_sales − INC_cost_goods_sold − INC_sga − INC_depreciation`; `INC_taxable_income` = `INC_ebit + INC_other_income − INC_interest_expense`; `INC_net` = `INC_taxable_income − INC_taxes`. All three formula-driven and must reconcile.
5. **CFO method footnote.** Template indirect-method `CASH_operating` (839,295) is **not** Sectra's audited CFO (922,364). The 83,069 gap is explained on Notes R69–R91 and arises from broader non-cash adjustments + cash-basis interest/tax. Stage 5 must use the template value for ratios but cite the audited figure when discussing "cash-conversion strength" (Hypothesis H3).
6. **Operating profit underlying vs reported.** Reported EBIT (`INC_ebit` = 722,997) includes a SEK 110,000K non-recurring patent settlement. Underlying EBIT = 612,997. For like-for-like vs FY23/24 and vs peers, Stage 5 must compute and present **both** reported and underlying operating margin: Reported = 22.32%; Underlying = 18.92% (= 612,997 / 3,239,811).
7. **Dividend vs cash outflow tie.** Income-statement Dividends (SEK 404,602K) is the **proposed** AGM 2025 dividend (1.10 ord + 1.00 extra = 2.10/share). The Cash Flow Statement shows Dividends paid = 0 and instead a Share-redemption outflow of SEK −211,935K (financing). Stage 5 must not double-count.
8. **Unit consistency.** All financial-statement tabs are in SEK thousand; `shares_outstanding` is entered as thousand-shares (192,667.489) so that `market_capitalization` = SEK 57,145,177 thousand ≈ SEK 57.1 billion ties to consensus market-cap. EPS cross-check: `INC_net / shares_outstanding` = 563,371 / 192,667 = SEK 2.92, matching Sectra's reported EPS.

---

## Part B — Analysis Specification

### 8. Analysis Requirements

The Stage 5 deliverable must interpret each ratio category in the order below, applying the named benchmarks. Treat all FY24/25 values above as inputs — do **not** recompute them; flag any discrepancy as a spec defect.

**8.1 Performance.** Interpret MVA, M/B, and EVA together. The narrative must answer: is Sectra creating economic value above its cost of capital? Anchor M/B against three peer points — (a) Pro Medicus (ASX:PME) as a pure-play SaaS PACS upper bound, (b) Agfa Healthcare / Carestream as legacy on-premise lower bound, (c) Sectra's own FY23/24 M/B as the self-trend. Comment on whether the 29.8× M/B is consistent with a successful SaaS transition or signals over-pricing.

**8.2 Profitability.** Compare reported vs underlying operating margin (per §7 rule 6). Test **Hypothesis H2** from the Stage 2 memo (`docs/decisions/2026-05-17-cam-sectra-selection.md`): "underlying operating margin should compress 100–200 bps FY24/25 → FY25/26 from 18.9% toward 17–18%." Use the underlying 18.92% as the starting point and note the CEO's June 2025 forward guidance. Discuss the ROE-vs-ROA gap: which is the larger driver — operating efficiency, leverage, or both? Use **start-of-year** ratios for the primary narrative (more conservative for a growing company) and **average** ratios as a cross-check.

**8.3 Efficiency.** Test **Hypothesis H1** from Stage 2: "DSO should lengthen 15–25 days and deferred revenue should expand 25–40% as SaaS transition shifts revenue-recognition timing." The model gives DSO = 64.4 days FY24/25; the Stage 5 narrative must situate this against FY23/24's implied DSO (calculate from prior-year receivables / prior-year sales — note this requires the prior-year sales figure, which is **not** in the model; the analysis must either retrieve it from the Annual Report or state explicitly that the FY-on-FY DSO comparison cannot be computed from this spec alone). For deferred-revenue expansion, compare contract liabilities current (974,935 vs 946,263 = +3.0%) and non-current (26,342 vs 10,907 from disclosures — to confirm at Stage 5). Where this spec lacks prior-year P&L data, say so in the deliverable rather than guess.

**8.4 Leverage.** Lead with the long-term debt ratio (3.22%), not the total-debt ratio. Explain why the total-debt ratio is misleading for Sectra (per §6 caveat). Connect to the AGM 2025 extraordinary dividend (SEK 1.00/share on top of SEK 1.10 ordinary) as evidence that management views capital structure as over-equity-weighted.

**8.5 Liquidity.** Cash ratio 0.79× is the most informative — current ratio is inflated by contract assets and other current assets. Note that Sectra holds SEK 1.34B of cash against SEK 1.7B current liabilities, of which ~SEK 975M is deferred revenue (services owed, not cash owed). Effective cash position vs **non-deferred** current liabilities is much stronger than the headline cash ratio suggests; compute and present this adjusted view.

**8.6 Cash flow strength (Hypothesis H3).** Confirm CFO / Net income > 1.5×. Template: 839,295 / 563,371 = 1.49× (just under). Sectra's audited statement: 922,364 / 563,371 = 1.64× (clears the 1.5× threshold and ties to the Stage 2 memo). State the audited figure as the headline number and the template figure as the model-based cross-check, with the §7-rule-5 reconciliation in a footnote.

**8.7 Cross-category connections.** At minimum, the Stage 5 deliverable must link: (a) profitability ↔ efficiency (asset turnover holds steady at ~1.0×, so margin is the swing variable for ROA); (b) leverage ↔ liquidity (low interest-bearing debt + high deferred revenue means Sectra's "liabilities" are operating, not financial); (c) cash flow ↔ working capital (deferred-revenue build is the mechanical reason CFO > Net income).

### 9. Du Pont Decomposition

Decompose ROE into the three-factor (margin × turnover × leverage) and the four-factor (operating margin × asset turnover × leverage × debt burden) forms.

- **Three-factor (Direct ROE = 35.89%):**
  Profit margin (17.39%) × Asset turnover (1.009×) × Equity multiplier (2.044× start-of-year, = 3,210,938 / 1,569,591) = 35.89%.
  Drivers: profit margin is the largest contributor; turnover is unremarkable (asset-light software business); leverage adds a multiplier ≈ 2× because half of liabilities is deferred revenue, not debt.
- **Four-factor (Du Pont ROE in workbook = 34.38%):**
  `RATIO_leverage` (1.96 current-year) × `RATIO_asset_turnover` (1.009, start-of-year) × `RATIO_operating_profit_margin` (18.08%) × `RATIO_debt_burden` (0.962) = 34.38%.
  Du Pont ROE ≠ Direct ROE by 1.51pp purely from the leverage component's current-year basis vs the rest's start-of-year basis (see §7 rule 3). Explain — do not "correct."
- **Primary driver question.** State explicitly which factor is the primary driver of Sectra's ROE: operating margin. Asset turnover and leverage are both stable; margin is what moves with the SaaS transition. Therefore Hypothesis H2 (margin compression) is also the key ROE-trajectory risk.
- **Sustainability.** Comment on whether the current ROE is sustainable through the SaaS transition. Use the CEO's June 2025 guidance and the underlying 18.9% margin as the anchor. Sustainability test = does CFO continue to exceed Net income? If yes, the headline margin compression is a recognition-timing artefact, not value destruction.

### 10. Strategic Recommendations

Produce **3–5 recommendations** for Sectra's management or for an equity investor. Each must:

1. Name a specific addressee — "management" or "an institutional investor evaluating Sectra at the current SEK 296.60 share price." (No vague "the company should...")
2. Be evidence-anchored — cite at least one specific computed ratio from §6 above, plus one qualitative factor (CEO guidance, AGM proposal, IFRS-15 contract-liability dynamic, etc.). No recommendation may stand on a single ratio in isolation.
3. Be actionable and specific — a recommendation that says "improve margins" is not actionable; "accept margin compression through FY25/26 and communicate the SaaS deferred-revenue mechanic to investors" is.
4. Be time-bound — name the horizon (next quarter, next fiscal year, by AGM 2026).
5. Acknowledge a counter-argument or risk — what would falsify this recommendation?

**Suggested recommendation slots** (not mandatory, but the writer must cover at least 3 of these 5 angles):
- A capital-return recommendation tied to the AGM 2025 extraordinary dividend pattern.
- A margin-communication recommendation tied to Hypothesis H2 and the CEO's guidance.
- A working-capital-disclosure recommendation tied to contract-liability dynamics (Hypothesis H1).
- A peer-benchmarking recommendation tied to M/B vs Pro Medicus and Agfa.
- An investor-positioning recommendation: hold / accumulate / trim, with the EVA (SEK +443M) and current 9% cost-of-capital assumption as anchors.

### 11. Output Format

The Stage 5 deliverable is a single Markdown file at `analysis/2026-XX-XX-cam-sectra-ratios-analysis.md` (date set at execution time), 6–10 pages printed (≈3,500–5,500 words), structured in the order below.

| § | Section | Length target | Tone |
|---|---------|--------------|------|
| 1 | Executive summary | 200–300 words | One-screen elevator: company, fiscal period, headline ROA/ROE/margin numbers, one-line headline recommendation. |
| 2 | Company and reporting context | 150–250 words | Sectra's segments, fiscal-year quirk, IFRS-by-nature reporting limitation. |
| 3 | Performance & EVA | 300–450 words | MVA, M/B, EVA with peer anchoring. |
| 4 | Profitability (reported vs underlying) | 400–600 words | Reported vs underlying operating margin; H2 test; ROE/ROA gap. |
| 5 | Efficiency & working capital | 400–600 words | DSO, inventory turnover, H1 test on contract liabilities. Acknowledge data gap on prior-year sales. |
| 6 | Leverage & cash flow | 300–500 words | Long-term debt ratio leads; interest coverage; cash conversion (template vs audited). |
| 7 | Liquidity | 200–300 words | Cash ratio adjusted view for deferred-revenue load. |
| 8 | Du Pont decomposition | 400–500 words | Three-factor + four-factor; primary driver; sustainability. |
| 9 | Strategic recommendations | 600–900 words | 3–5 recs per §10 requirements. |
| 10 | Limitations & data gaps | 150–250 words | Single-period model, IFRS-by-nature ceiling on COGS analysis, prior-year P&L not in spec, peer ratios not in spec. |
| 11 | References | — | Annual Reports, KLAS, Yahoo Finance, Riksbank, Damodaran ERP. |

**Style requirements:**
- All currency in SEK with explicit unit ("SEK 563.4M" not "563M"). Convert any USD comparison to SEK at the FY24/25 average rate (state the rate used).
- All ratios stated to **two decimals for %, three for ×** (e.g., 18.24%, 1.009×).
- Every numerical claim must trace to either (a) a named range in §3–§5, (b) a derived calculation shown inline, or (c) a cited Annual Report page. No unsourced numbers.
- One sentence per ratio interpretation; do not pad. Use named ranges in inline math (e.g., "Operating margin = `currentYear_after_tax_operating_income` / `INC_sales` = 18.08%").
- Hypothesis-testing language ("H1 supported", "H2 supported with caveat", "H3 confirmed by audited CFO") rather than rhetorical hedging.
- US business English; second person never; first person only in the limitations section.

---

## References

- Sectra AB Investor Relations: https://investor.sectra.com — Annual Reports FY2022/2023, FY2023/2024, FY2024/2025 (IFRS-audited).
- Sectra Annual Report FY2024/2025 — Consolidated Balance Sheet p.92, Income Statement p.91, Cash-Flow Statement p.93, share data p.55–56, p.122, dividend proposal p.73 & p.120.
- Sectra FY24/25 Year-End Press Release, June 5, 2025: https://sectra.com/news-and-press-releases/news-item/B25E9F6BE58D2EAB/
- Sectra Year in Brief 2024/2025: https://investor.sectra.com/financial-reports/the-year-in-brief-2024-2025/
- BUS-629 Stage 4 brief: https://github.com/adamwstauffer/shidler/blob/main/courses/BUS-629-VEMBA-International-Corporate-Finance/stage4-technical-specification.md
- BUS-629 spec template: https://github.com/adamwstauffer/shidler/blob/main/docs/templates/spec-template.md
- Stage 2 selection memo (this repo): `docs/decisions/2026-05-17-cam-sectra-selection.md` — three hypotheses (H1 working capital, H2 profitability, H3 cash conversion & FX) tested in Part B.
- Stage 3 populated workbook (this repo): `models/builds/2026-05-17-cam-sectra-financials.xlsx` — source of every numerical input above.
- KLAS PACS 2025 report: https://klasresearch.com/report/pacs-2025-consistent-support-and-ongoing-product-development-are-key-to-customer-success/3159 — Sectra ranked #1 PACS in US, 13 consecutive years.
- Riksbank.se — SEK/USD, SEK/GBP, SEK/EUR period-average rates for FY24/25.
- Damodaran — Sweden mature-market equity risk premium 5.5% (cost-of-capital input).
