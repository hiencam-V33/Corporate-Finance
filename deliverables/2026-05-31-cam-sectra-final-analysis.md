# Sectra AB (publ) — Evaluated Final Analysis

**Author:** Hien Cam
**Date:** 2026-05-31
**Company:** Sectra AB (publ) · SECT B · Nasdaq Stockholm Mid Cap
**Fiscal year:** FY2024/2025 (May 1, 2024 – April 30, 2025), with comparatives for FY2023/2024
**Specification executed:** `docs/specs/2026-05-30-cam-sectra-spec.md`
**LLM used:** Google Gemini 2.5 Pro
**Source documents:** Sectra Annual Report 2024/2025 (pp. 92–94 for primary statements); Stage 3 workbook `models/builds/2026-05-17-cam-sectra-financials.xlsx`
**Related deliverables:** `deliverables/2026-05-31-cam-sectra-llm-raw.md` · `analysis/validation/2026-05-31-cam-sectra-stage5-verification.md` · `deliverables/2026-05-31-cam-sectra-spec-retrospective.md`

> **A note on how this analysis was produced.** The Stage 4 specification was executed by Google Gemini 2.5 Pro to produce a raw analysis (file linked above). I then manually recomputed seven ratios from the Stage 3 workbook (verification artifact linked above), evaluated where the LLM was correct and where it deviated, and rewrote the analysis with corrections, annotations, and executive judgment. Section 5 documents the LLM evaluation in full; Section 6 is my own investment thesis.

---

## 1. Company & Data Summary

Sectra AB (publ) is a Linköping, Sweden–headquartered medical-imaging IT and secure-communications group, listed on Nasdaq Stockholm Mid Cap (ticker SECT B). Its Medical IT segment is a global PACS / enterprise-imaging vendor and has held the #1 Best in KLAS award for US PACS for 13 consecutive years; its Secure Communications segment serves classified-government and defense customers across the EU and the United States.

The analysis covers fiscal year **FY2024/2025**, running May 1, 2024 through April 30, 2025, with comparative data for FY2023/2024 (ending April 30, 2024). All figures are reported in **Swedish krona** (SEK) and presented in **SEK thousand** unless otherwise stated.

**Reporting standard and IFRS-specific conventions.** Sectra reports under IFRS as adopted in the EU. Three structural conventions materially affect ratio interpretation in this analysis:

- **By-nature income statement.** Sectra presents operating expenses by nature (personnel costs, other external costs) rather than by function (cost of goods sold, SG&A). The line mapped to `INC_cost_goods_sold` in the model is "Goods for resale" only (SEK 441,712K) — primarily third-party hardware bundled into enterprise imaging contracts. Software-implementation and customer-support personnel are recorded inside `INC_sga`. Standard gross-margin calculations therefore yield an inflated, non-meaningful figure of ~86%, and standard inventory-turnover values reflect only hardware throughput, not software delivery. **Operating margin is the only reliable profitability baseline.**
- **Lease-only interest-bearing debt.** Sectra carries no traditional debt; the only interest-bearing liabilities are IFRS 16 lease liabilities (SEK 87,457K total between current and non-current). The model's `BAL_debt_short_term` and `BAL_debt_long_term` therefore map to lease liabilities.
- **Deferred revenue inflates current liabilities.** A material portion of current liabilities is contract liabilities (deferred revenue under IFRS 15). These are settled by future software delivery, not cash outflow, and should be excluded when evaluating cash-coverage and short-term solvency ratios.

**Key assumptions used in the model.**

| Assumption | Value | Source |
|---|---:|---|
| Share price at fiscal year-end (Apr 30, 2025) | SEK 296.60 | AR pp. 55–56 |
| Shares outstanding (ex-treasury) | 192,667.489 thousand | AR pp. 55, 122 |
| Weighted average cost of capital | 9.00% | CAPM build: Rf 2.76% (Swedish 10-yr govt bond) + Beta 1.15 (mean of three sources) × ERP 5.5% (Sweden mature-market, Damodaran) |
| Effective tax rate (input to NOPAT) | 20.6% | Sweden statutory rate; FY24/25 effective rate is 22.4% (`INC_taxes / INC_taxable_income`) |

**Patent-settlement non-recurring item.** Reported FY2024/2025 operating profit of SEK 722,997K includes a SEK 110M patent-settlement gain disclosed in Sectra's administration report. Underlying EBIT is therefore approximately SEK 612,997K, and all trend commentary in this analysis is based on the underlying figure unless otherwise noted.

---

## 2. Ratio Results & Interpretation

All values are FY2024/2025 actuals computed from the Stage 3 workbook. Where the LLM output and the workbook diverge, I annotate the divergence and resolve to the workbook value. Each category opens with the headline metrics, then interprets them in business context.

### 2.1 Performance & Market Valuation

| Ratio | Value | Note |
|---|---:|---|
| Market value added (MVA) | SEK 55,228,352K | Market cap (57,145,177) less book equity (1,916,825) |
| Market-to-book ratio | 29.81× | Strong premium |
| Economic value added (EVA) | SEK 442,707K | NOPAT 585,698.28 less capital charge (9% × 1,588,795) |

The market places Sectra at a **29.81× book-equity multiple**, far above the 1–3× range typical of legacy hardware-heavy medical-imaging vendors (Agfa, Carestream) and well below the 80× and higher multiples paid for pure-play cloud-native peers like Pro Medicus (ASX:PME). Sectra sits in a transition band: priced as a high-quality SaaS company that has not yet fully completed its model conversion, with the market pricing in continued recurring-revenue mix growth.

The economic substance behind the multiple is sound. EVA of SEK 442,707K means that, after charging Sectra's start-of-year capital base (SEK 1,588,795K) at the 9% WACC, the company still generated SEK 442.7M of after-tax operating income above its cost of capital. This is genuine wealth creation, not multiple expansion alone.

### 2.2 Profitability

| Ratio | Start-of-year basis | Average basis | Note |
|---|---:|---:|---|
| Return on assets (ROA) | 18.24% | 16.81% | NOPAT / total assets |
| Return on capital (ROC) | 36.86% | 32.82% | NOPAT / total capitalization |
| Return on equity (ROE) | 35.89% | 32.32% | Net income / equity |
| Net profit margin | 17.39% | — | Net income / sales |
| Reported operating margin | 22.32% | — | Reported EBIT / sales |
| **Underlying operating margin** | **18.92%** | — | (Reported EBIT − SEK 110M patent settlement) / sales |

The reported 22.32% operating margin overstates underlying performance. Stripping the SEK 110M one-off patent settlement (per Validation Rule V-EBIT-1 in the spec) gives an underlying margin of 18.92%, which is consistent with Sectra's own multi-year communications. ROE of 35.89% — nearly double ROA — is driven not by financial leverage (Sectra carries effectively no interest-bearing debt) but by **operating leverage from non-interest-bearing contract liabilities**: deferred revenue and accrued obligations represent roughly half of total liabilities and finance a sizeable portion of the asset base at zero cost. This is a structural feature of the SaaS business model, not a credit risk.

### 2.3 Efficiency

| Ratio | Value | Note |
|---|---:|---|
| Asset turnover | 1.009× | Sales / start-of-year total assets |
| Receivables turnover | 5.67× | Sales / start-of-year receivables |
| Days sales outstanding (DSO, current) | 64.40 days | Start-of-year receivables / daily current sales |
| Inventory turnover | 12.07× | Goods for resale / start-of-year inventory |
| Days in inventory | 30.20 days | Inverse of inventory turnover |

**Asset turnover of 1.009× combined with an 18.92% underlying operating margin is the engine behind ROA.** The two multiply through to 19.1% (start-of-year basis), confirming the Du Pont identity holds on a single-year basis (see Section 3).

**DSO at 64.40 days, and the H1 caveat.** The LLM's analysis claimed DSO had "lengthened" from a historical baseline of 45–50 days to the current 64.40 days. **This claim is not supported by data.** The 45–50-day figure does not appear in the Stage 4 spec, the workbook, or the Annual Report. My manual recompute using FY23/24 sales of SEK 2,963,607K (from AR p. 92) as a proxy denominator — `BAL_receivables_prior (571,661) / (FY23/24 sales (2,963,607) / 365)` = 571,661 / 8,119.47 = **70.4 days** — is methodologically distinct from the workbook's DSO formula but in the same range as the current 64.40 figure. Hypothesis H1 (formulated in Stage 2 as *"DSO should lengthen 15–25 days as SaaS transition shifts revenue-recognition timing"*) is **not supported in the direction claimed.** Sectra's collection cycle, viewed across the two-year window available, is approximately stable in the 60–70 day band — neither dramatically lengthening (as H1 predicted) nor shortening enough to call it a directional win. This nuance is preserved here rather than papered over because the integrity of the hypothesis-testing matters more than the appearance of a clean directional answer.

**Inventory turnover of 12.07× reflects hardware-only turnover.** Per Section 1 conventions, Sectra's "inventory" is third-party hardware bundled into enterprise contracts. Software delivery, which generates the majority of revenue, does not pass through this account. This ratio is therefore not a meaningful measure of overall operational efficiency.

### 2.4 Leverage

| Ratio | Value | Note |
|---|---:|---|
| Long-term debt ratio | 3.22% | LT debt / (LT debt + equity) |
| LT debt / equity | 0.033× | — |
| **Total debt ratio** | **48.97%** | Total liabilities / total assets — see caveat |
| Times interest earned | 25.71× | EBIT / interest expense |
| Cash coverage ratio | 29.68× | (EBIT + D&A) / interest expense |

**The 48.97% total debt ratio is misleading and the long-term debt ratio of 3.22% is the truer measure.** Of the SEK 1,839,404K total liabilities, only SEK 87,457K is interest-bearing (IFRS 16 lease liabilities); the remainder is operating liabilities, dominated by SEK 974,935K of current contract liabilities (deferred revenue per AR p. 92) plus accruals and trade payables. Deferred revenue represents pre-paid software services, not financial debt — settling it requires delivering software, not cash.

Interest cover at 25.71× and cash cover at 29.68× confirm that, even on the reported leverage, financial fragility is not a concern. The proposed FY2025 capital return — comprising a SEK 1.10/share ordinary dividend, a SEK 1.00/share extraordinary dividend, and continued share-redemption program — is consistent with management's communicated policy of preventing equity bloat in a low-reinvestment-need business.

### 2.5 Liquidity

| Ratio | Standard value | Adjusted value | Note |
|---|---:|---:|---|
| Net working capital / total assets | 33.48% | — | NWC 1,257,681 / TA 3,756,229 |
| Current ratio | 1.74× | — | — |
| Quick ratio | 1.12× | — | (Cash + receivables) / CL |
| Cash ratio | 0.79× | **~1.85×** | See note |

The headline cash ratio of 0.79× understates Sectra's actual short-term liquid strength because deferred revenue (which is settled by service delivery, not cash) is included in the current-liabilities denominator. **Removing current contract liabilities of SEK 974,935K (sourced from the Annual Report — this value is not in the model spec)** gives an adjusted cash ratio of approximately 1.85×, meaning Sectra holds nearly twice the cash needed to clear all near-term financial obligations.

I flag the data-source issue here because it is the cleanest example of a spec gap: the model spec aggregates contract liabilities into the broader `BAL_other_current_liabilities_curr` (1,570,554) without breaking them out, so the LLM had no choice but to pull from the Annual Report. The adjusted ratio is directionally correct but is not strictly an in-spec computation. See the spec retrospective for the remediation I would make if I re-ran Stage 4.

---

## 3. Du Pont Analysis

The Du Pont decomposition isolates which structural drivers produce Sectra's elite ROE. I present both the standard three-factor identity and the four-factor variant used in the model.

**Three-factor decomposition (direct, start-of-year basis):**

ROE 35.89% = Profit Margin 17.39% × Asset Turnover 1.009× × Equity Multiplier 2.044×

Where equity multiplier = start-of-year total assets / start-of-year equity = 3,210,938 / 1,569,591 = 2.044×.

**Four-factor decomposition (workbook variant, mixed-basis):**

Du Pont ROE 34.38% = Leverage 1.96× × Asset Turnover 1.009× × Operating Profit Margin 18.08% × Debt Burden 0.962

The 1.51 percentage-point gap between direct ROE (35.89%) and four-factor Du Pont ROE (34.38%) is **a structural artifact of the template**, not a computation error: the leverage component uses current-year terminal balances while asset turnover uses start-of-year asset denominators. This is documented as Validation Rule V-DP-2 in the spec and was correctly handled by the LLM.

**Primary driver.** Asset turnover (~1×) and equity multiplier (~2×) are stable structural anchors of the business model — neither is changing meaningfully year-over-year. **The variable that moves ROE is the operating margin.** This is exactly why Hypothesis H2 (margin compression during cloud-transition) is the key risk to the near-term ROE trajectory, and why the patent-settlement strip-out matters: the 22.32% reported margin in the four-factor identity is partly a non-recurring inflation, and the underlying 18.92% is what feeds into the sustained run-rate.

If the underlying margin compresses by 100–200 bps over FY2025/2026 (as H2 predicts and as management has guided), holding asset turnover and the multiplier constant, ROE would re-rate from the current ~32–36% range down to approximately **28–32% on the same basis**. This is still an elite return profile, but the headline number will look weaker.

---

## 4. Strategic Recommendations

> **Author's note on this section.** The recommendations below were drafted from ratio evidence and the audited Annual Report. Section 6 contains the integrating "so what?" thesis. Voice in this section is intentionally directive — each recommendation is written as guidance to a named decision-maker, with the evidence anchor and counter-argument disclosed.

### Recommendation 1 — IR: institute a "SaaS transition" disclosure overlay

- **Addressee:** Sectra Investor Relations and CFO function.
- **Evidence:** Reported operating margin 22.32% vs. underlying 18.92% (Section 2.2); the SEK 110M patent settlement is fully disclosed in the administration report but is not surfaced in the headline P&L presentation. Non-current contract liabilities expanded from prior-year levels (per AR — exact figures depend on note breakouts).
- **Action:** Publish a quarterly KPI overlay alongside the standard income statement, disclosing (a) recurring versus non-recurring profit, (b) annual recurring revenue (ARR) and net retention rate, and (c) the rolling Total Contract Value backlog. The objective is to anchor sell-side and buy-side models on the recurring base, so that during cloud-investment quarters (H2's predicted margin dip) the market understands the structural quality rather than re-rating downward on a single weak headline.
- **Timeline:** Implement in the FY2025/2026 Q1 reporting cycle.
- **Counter-argument:** Disclosing TCV backlog at high granularity gives commercial intelligence to pure-play competitors (e.g., Pro Medicus) during multi-hospital RFP bidding. Mitigation: report at a portfolio level (e.g., total subscription-revenue backlog), not customer-level.

### Recommendation 2 — Board: codify the capital-return waterfall

- **Addressee:** Sectra Board of Directors.
- **Evidence:** EVA SEK 442,707K (Section 2.1); long-term debt ratio 3.22% (Section 2.4); cash and marketable securities SEK 1,341,871K (Section 2.5); proposed AGM 2025 capital return of SEK 2.10/share total dividend plus continued share-redemption program.
- **Action:** Adopt a written capital-return policy stating that any free cash above an SEK 1.0B liquidity floor will be returned to shareholders through the redemption mechanism in addition to the ordinary dividend. The structural rationale is that an asset-light SaaS business does not require heavy reinvestment, and retaining cash beyond a working buffer compresses ROE through equity bloat — exactly what the share-redemption mechanism is designed to prevent.
- **Timeline:** Codify at the 2026 AGM.
- **Counter-argument:** A formal policy reduces flexibility for opportunistic M&A — for instance, a bolt-on AI-pathology acquisition in the SEK 500M–1B range (cf. Sectra's prior Oxipit acquisition pattern). Mitigation: include a written exception for board-approved strategic transactions above SEK 250M.

### Recommendation 3 — Equity investor: accumulate through the cloud-investment trough

- **Addressee:** Long-only equity investors (institutional, EMBA portfolio peers considering SECT B).
- **Evidence:** Adjusted cash ratio ~1.85× (Section 2.5); CFO/Net Income ratio of 1.64× on the audited basis (the simplified-indirect template figure is 1.49× per Validation Rule V-CF-1); H2 margin compression is signaled, time-limited, and already partially priced in.
- **Action:** Build a core position in SECT B, accumulating on margin-driven drawdowns over FY2025/2026 rather than chasing entry at current levels. The investment case rests on three legs: (a) the cash-generation engine remains intact through the transition (audited CFO conversion of 1.64×); (b) the underlying margin floor at ~18% is well above the cost of capital (9%); (c) the M/B premium (29.81×) is justified by EVA performance rather than speculative growth alone.
- **Timeline:** 12–18 month accumulation window.
- **Counter-argument:** A broader healthcare-IT cybersecurity breach (e.g., major US PACS-vendor incident) could compress sector multiples by 30%+ regardless of Sectra's individual performance. Mitigation: size the position with sector-event tail risk in mind; do not exceed standard healthcare-IT allocation limits.

### Recommendation 4 — Management: time the dilutive transition cost transparently

- **Addressee:** Sectra CEO and CFO.
- **Evidence:** Hypothesis H2 (margin compression 100–200 bps in FY2025/2026); Du Pont primary-driver analysis (Section 3) showing margin as the variable; non-current contract liabilities trend (Section 2.4) showing multi-year cloud commitments accumulating.
- **Action:** Provide explicit, dated guidance on the cloud-investment cost arc — for example, "Operating-margin trough in H2 FY2025/2026 at 17.0–17.5%, with recovery to 19%+ by FY2026/2027 as Azure-migration costs amortize against expanded recurring base." Anchoring an expected trough and recovery date prevents the market from extrapolating the dip into a structural impairment.
- **Timeline:** At the FY2024/2025 year-end results presentation (June 2025) and again at each interim update.
- **Counter-argument:** Specific margin guidance creates a stick for the share price if delivery slips even modestly — a "missed your own forecast" narrative is harder to manage than a vague qualitative caution. Mitigation: provide ranges, not point estimates, and tie the recovery date to a published technical milestone (e.g., percent of accounts migrated).

### Recommendation 5 — Sectra International Business Development: design a Vietnam-fit "hybrid on-premise finance-lease" package

- **Addressee:** Sectra International Business Development and the Vietnamese-market PACS distributor management team.
- **Evidence:** Vietnamese hospital procurement convention is a 5-year finance-lease structure with 100% upfront distributor investment, fixed monthly payments, end-of-term ownership transfer (see Section 6 paragraph 4); Sectra's by-nature reporting blends hardware, software, and services costs into a single 18.92% underlying margin (Section 1, Section 6 paragraph 3) — meaning a Vietnamese distributor cannot directly extrapolate which product-mix configuration is most margin-defensible without primary-source cost reconstruction; Vietnamese capital cost is 9–10% floating (per local operator input), comparable to the 9.00% WACC used in this analysis but exposed to floating-rate risk; data-sovereignty considerations make pure-cloud SaaS deployment non-viable for public and large private hospitals in Vietnam over the next 3–5 years.
- **Action:** Sectra HQ should design and license a "hybrid on-premise + perpetual-licence-with-maintenance" package specifically adapted to the Vietnamese finance-lease distribution model. Three concrete elements: (a) a documented commitment to support on-premise PACS product configurations through at least FY2034/2035 — long enough to cover one full 5-year lease cycle plus a post-transfer maintenance phase — to give distributors and hospital customers a credible product-lifecycle guarantee; (b) a transparent unit-cost breakdown specifically for the Vietnamese deal mix (hardware integration, software licence, on-site service costs separated), provided under NDA to distributor partners, so that distributor IRR per deal can be modelled with real cost inputs rather than blended by-nature estimates; (c) a structured early-termination clause framework that aligns Sectra's exposure with the distributor's hospital-side credit risk (e.g., software-licence reactivation rights if a hospital terminates before year 5, so the distributor can recover residual value through redeployment).
- **Timeline:** Negotiated and codified during FY2026/2027 distribution-agreement discussions; implementation in any Vietnamese deals signed from FY2027/2028 onwards.
- **Counter-argument:** Providing per-line cost transparency to a single regional distributor risks setting a precedent that other distributors will demand (and may leak to competitors). Mitigation: cost-disclosure under tiered NDA tied to minimum annual deal-volume commitments from the distributor, so the disclosure is mutual rather than one-sided. Additionally, an explicit on-premise-lifecycle commitment to 2034/2035 may slow Sectra's internal cloud-migration roadmap by preserving on-premise engineering resources longer than HQ would prefer; mitigation here is to scope the commitment to specifically the product configurations already deployed in Vietnam, not to a wholesale on-premise product line, so HQ retains the option to discontinue parallel on-premise SKUs in mature cloud markets while preserving the Vietnamese configuration.

---

## 5. LLM Evaluation & Annotations

The LLM (Gemini 2.5 Pro) executed the Stage 4 specification competently but exhibited four distinct behavioral patterns that materially affect how the output should be used. I document each below with the implication for the spec and for the final analysis.

### 5.1 What the LLM executed correctly

- **Named-range convention.** The LLM used the implemented `_curr` / `_prior` aliases throughout, not the literal `_2024` / `_2025` convention documented (but not implemented) in the Cover sheet. This validates the HIL fix made during Stage 4.
- **Validation rules from spec Section 7.** Six of the eight validation rules were applied without prompting: BS balance, by-nature EBIT integrity, gross-margin non-meaningfulness, CF reconciliation, Du Pont ROA = direct ROA, and Du Pont ROE time-mismatch. Both were correctly explained as structural rather than as model errors.
- **Underlying vs reported EBIT.** The LLM correctly applied Validation Rule V-EBIT-1, stripping the SEK 110M patent settlement and reporting both reported (22.32%) and underlying (18.92%) operating margins.
- **Du Pont decomposition.** Both three-factor and four-factor variants were produced with the correct identities and the explained 1.51 ppt mismatch.
- **NOPAT and start-of-year basis.** Verification on ROA, Asset Turnover, EVA, and Underlying Operating Margin (verification artifact) all returned exact matches against manual recomputation — the LLM did not take shortcuts on NOPAT construction or denominator basis.

### 5.2 Where the LLM deviated — three distinct failure modes

**5.2a — External-knowledge substitution where the spec was silent.** The LLM filled three spec-silent fields with values from the Annual Report rather than flagging the gap:

- Adjusted Cash Ratio: used SEK 974,935K for current contract liabilities (the value is correct against AR p. 92 but is not in the spec; the spec only provides the aggregate `BAL_other_current_liabilities_curr` of 1,570,554).
- Dividend split: "SEK 1.10 ordinary + SEK 1.00 extraordinary" (matches AR p. 73 and p. 120 but spec only provides the aggregate `INC_dividends` of 404,602).
- Historical DSO baseline of "45–50 days" — see 5.2c below.

This is a spec gap, not an LLM error. The spec did not explicitly prohibit external lookups, and the missing sub-component breakouts forced the LLM into either silence (which it did not choose) or external sourcing (which it did). Section 6 of the spec retrospective documents the remediation.

**5.2b — Output formatting drift relative to spec Section 11.** The spec's Section 11 specified an 11-section structure for the Stage 5 output. The LLM produced an 11-section output (1. Executive Summary through 11. References), which matches the spec's count but not the brief Stage 5 grading rubric (which calls for 6 specific sections). This evaluated final analysis re-organizes the content into the rubric's six-section structure. No analytical content was lost in the reorganization.

**5.2c — One outright hallucination affecting a hypothesis test.** The LLM stated *"supplementary data from the Annual Report indicates that historical collection cycles hovered around 45–50 days"* (Section 5 of the raw output) and used this to support Hypothesis H1's "DSO lengthening" claim. **There is no such 45–50-day figure in the Annual Report.** A manual proxy computation using the prior-year sales and prior-year receivables yields approximately 70.4 days — methodologically distinct from the workbook's DSO formula, but in the same range as the current 64.4 days, and dramatically inconsistent with the LLM's claim. The LLM hallucinated the historical baseline. This affected the conclusion on Hypothesis H1, which has been corrected in Section 2.3 of this final analysis.

### 5.3 Spec gaps vs LLM limitations

| Pattern | Spec gap | LLM limitation |
|---|:---:|:---:|
| External-knowledge substitution (5.2a) | ✓ — spec did not direct refusal | — |
| Output structure drift (5.2b) | ✓ — spec Section 11 conflicted with brief | — |
| Hallucinated baseline (5.2c) | — | ✓ — LLM should have flagged the gap, not invented a value |

Two of three failure modes are spec gaps. One is a true LLM limitation (hallucination). The spec retrospective addresses both gaps directly; the LLM limitation is a reminder that even a well-specified analysis requires human verification, which is precisely what this stage tests.

---

## 6. Executive Justification

I came to Sectra because two questions were converging in my own work. As a VEMBA student, I needed a company financially transparent enough to test the spec-driven analysis discipline this course is teaching. As an operator evaluating whether to distribute enterprise-imaging solutions in Vietnam, I needed a vendor whose product, brand, and balance-sheet stability would actually justify the long commitment a Vietnamese distribution arrangement requires. Sectra was one of a small handful of global PACS vendors that passed both screens — technically credible for Vietnamese hospital deployment, priced at a level the market can absorb, and listed on Nasdaq Stockholm with publicly audited statements. I picked it because I wanted the analysis to do real work for me, not just earn a grade.

What the ratios say about Sectra as a company is, on the headline, very positive. Underlying operating margin near 19% (after stripping the SEK 110M patent settlement per V-EBIT-1), EVA of SEK 442,707K against a 9% cost of capital, and a cash-conversion ratio of 1.64× on the audited basis are not accidental. They are the signature of a company that has converted a meaningful share of its revenue base from hardware-bundled enterprise sales to recurring software subscriptions, and the operating leverage of that conversion is what produces the 35.89% ROE despite Sectra carrying effectively no interest-bearing debt. Du Pont decomposition makes the source of returns explicit — leverage contributes a 2.04× multiplier, but the dominant lever is the 17.39% net profit margin. Sectra is a **pricing-power business**, not a **leverage business** — and that is the structural fact that matters when projecting its trajectory.

There is one significant transparency limitation I would not have appreciated before working through this analysis: **Sectra does not, and structurally cannot under IFRS by-nature presentation, disclose unit economics by product line.** The "Goods for resale" line of SEK 441,712K captures only third-party hardware bundled into enterprise contracts; software-implementation engineers, cloud-infrastructure operations, customer-success personnel — all the cost of actually delivering the Sectra product — sit inside Personnel costs and Other external costs, blended across software licenses, hardware integration, professional services, and maintenance. The headline 19% operating margin is a **blended margin** across all of these. There is no audited line that says "Sectra's software gross margin is X% and its hardware-integration margin is Y%." For a distributor evaluating which mix of products to push in a new market, this opacity matters more than the headline number, because the Vietnamese deal mix will not be the same as the Stockholm deal mix.

The contrarian view I take from this analysis is that **Sectra's headline financial story does not transfer to Vietnam — and the transfer gap is larger than most institutional analysts would estimate.** Three reasons. First, the Vietnamese hospital market remains predominantly on-premise; cloud deployment is constrained by data-sovereignty concerns, network reliability in regional hospitals, and a deep cultural preference against patient-data leaving national jurisdiction with a foreign vendor. Cloud-subscription model — the very transition Sectra's narrative depends on — is for the next three to five years viable in Vietnam only for small private hospitals and clinics, not the public-hospital and large private-hospital segments that drive PACS volume. Second, the commercial structure for selling PACS in Vietnam is not subscription: it is a 5-year financed-lease arrangement in which the distributor takes 100% upfront investment in hardware and software, collects fixed monthly payments, and transfers ownership at end of term. This is, structurally, a finance lease, not a service contract — the distributor functions as an equipment financier as much as a technology vendor. Third, Vietnamese capital cost (9–10%, floating) combined with hospital-side risks (leadership transitions, policy shifts, early-termination risk, payment delays) means the working-capital and credit-risk profile of a Vietnamese Sectra distributor looks nothing like Sectra Sweden's 64-day DSO and SEK 1.34B cash buffer.

The methodological lesson I take from running Stage 5 was sharper than I expected. The Gemini output was professional, used correct ratios, and produced a confident verdict on Hypothesis H1 — DSO had "lengthened" from a historical 45–50-day baseline. That baseline did not exist anywhere in the Annual Report. The seven-row manual verification table is what caught it; without that discipline, a board memo built on the LLM's number would have presented a counterfactual narrative as fact. The transferable habit I am keeping is this: any LLM-generated financial analysis I consume, including ones I commission, gets manual recompute on at least five anchor numbers before any conclusion is allowed to move my decision. That habit is more durable than any individual ratio formula in this course.

The integrated thesis is therefore not "Sectra is a great company" — that part is well-established. The integrated thesis is that **Sectra is the right vendor to evaluate for Vietnam, but the right way to evaluate it is not by extrapolating its Swedish unit economics**. The Sectra financial story tells me the vendor has pricing power, a clean balance sheet, and durable cash generation — these are the qualifications I need from a partner I am proposing to commit five-year contracts under. The Vietnamese commercial model, however, must be analyzed on its own terms — finance-lease IRR per deal, default-risk-adjusted payment streams, blended hardware-plus-software cost structure that I must rebuild from primary sources because Sectra's by-nature reporting cannot supply it. The ratio analysis above is the necessary first half of that work; the second half is operator-level due diligence that no public filing can substitute for.

---

## References

- Sectra AB (publ) Annual Report and Sustainability Report 2024/2025: Consolidated income statements (p. 92), consolidated balance sheets (p. 92), consolidated cash-flow statements (p. 93), consolidated statement of changes in equity (p. 94), share data (pp. 55–56, 122), dividend proposal (pp. 73, 120). Available at investor.sectra.com.
- Sectra AB Year-End Press Release, June 5, 2025.
- KLAS Research PACS 2025 Report (US PACS Best in KLAS award).
- Damodaran, A. — Country Risk Premiums and Equity Risk Premiums (Sweden ERP input).
- Sveriges Riksbank — Swedish 10-year government bond yield (risk-free rate input).
- Stage 3 workbook: `models/builds/2026-05-17-cam-sectra-financials.xlsx`.
- Stage 4 specification: `docs/specs/2026-05-30-cam-sectra-spec.md`.
- Stage 5 raw LLM output: `deliverables/2026-05-31-cam-sectra-llm-raw.md`.
- Stage 5 manual verification: `analysis/validation/2026-05-31-cam-sectra-stage5-verification.md`.
- Stage 5 spec retrospective: `deliverables/2026-05-31-cam-sectra-spec-retrospective.md`.
