# Stage 4 Spec — Retrospective

**Author:** Hien Cam
**Date:** 2026-05-31
**Company:** Sectra AB (publ) · SECT B · Nasdaq Stockholm
**Spec being evaluated:** `docs/specs/2026-05-30-cam-sectra-spec.md`
**Stage 5 LLM output:** `deliverables/2026-05-31-cam-sectra-llm-raw.md`
**LLM used:** Google Gemini 2.5 Pro
**Companion artifacts:** `analysis/validation/2026-05-31-cam-sectra-stage5-verification.md` · `deliverables/2026-05-31-cam-sectra-final-analysis.md`

---

## 1. Section-by-section verdict

| Spec section | Verdict | Symptom in Stage 5 output |
|---|---|---|
| Part A.1 — Scope & Objective | **Clear** | LLM correctly identified Sectra as a transition-stage SaaS company, used FY2024/2025 fiscal year, applied IFRS conventions, and targeted the multi-audience framing (Professor + EMBA peer + Sectra IR) without confusion. |
| Part A.2 — Model Architecture | **Clear** | LLM did not attempt to modify formulas on the Ratios tab and respected the read-only nature of computed cells; no architecture-related deviations observed. |
| Part A.3 — Data Inputs | **Vague** | LLM filled three "spec-silent" sub-components from the Annual Report rather than flagging the gap: `contract_liabilities_current` (SEK 974,935K, used in Adjusted Cash Ratio), the dividend per-share split (SEK 1.10 ordinary + SEK 1.00 extraordinary), and detail behind the SEK 110M patent settlement. Spec aggregated these into parent buckets without breaking out the sub-components the analysis needed. |
| Part A.4 — Named Range Conventions | **Clear** | LLM used the implemented `_curr` / `_prior` convention throughout — the Stage 4 HIL fix (calling out the Cover-sheet vs implementation deviation) worked as intended. No formulas attempted with `_2024` / `_2025` literals. |
| Part A.5 — Derived Inputs | **Clear** | LLM correctly constructed NOPAT = `INC_net + (1 − tax_rate) × INC_interest_expense` and used `startYear_total_capitalization` (not assets) for the EVA capital charge — both points where shortcuts would have been easy. |
| Part A.6 — Ratio Definitions & Formulas | **Clear** | All 26 ratios produced; verification table confirms 5/5 graded ratios tie to manual recompute. Du Pont 3-factor and 4-factor both produced with correct identities. |
| Part A.7 — Validation Rules | **Vague** | LLM explicitly cited 6 of 8 validation rules in its output (V-EBIT-1, V-CF-1, V-DP-1, V-DP-2, V-IS-1, V-IS-2). V-BS-1 (balance-sheet identity) was satisfied implicitly — the LLM did not surface the check, even though the rule asked it to. V-CF-2 (Dividends = 0 vs share-redemption tie) was addressed correctly in the cash-flow narrative, but the LLM also exceeded the rule's scope by sourcing the SEK 1.10 / SEK 1.00 dividend split from the Annual Report — a behavior the rule did not anticipate or prohibit. The Vague verdict therefore reflects both incomplete citation (V-BS-1) and unbounded scope (V-CF-2), not absence. |
| Part B.8 — Analysis Requirements | **Vague** | LLM hallucinated a historical DSO baseline of "45–50 days" to support Hypothesis H1's "DSO lengthening" claim. The spec asked for H1 testing but did not specify what to do when the underlying historical data was unavailable in the model — leaving the LLM with a choice between flagging the gap or fabricating a value. It chose fabrication. |
| Part B.9 — Du Pont Decomposition | **Clear** | Both three-factor and four-factor variants produced correctly. LLM correctly identified the 1.51 ppt mismatch between direct ROE and Du Pont ROE as a template time-mismatch artifact (per V-DP-2), not a model error. |
| Part B.10 — Strategic Recommendation Requirements | **Clear** | LLM produced three recommendations with the requested elements (addressee, evidence basis, action, timeline, counter-argument). Format conformed to spec. |
| Part B.11 — Output Format | **Vague** | Spec specified an 11-section output structure for Stage 5. The brief Stage 5 grading rubric specifies a *different* 6-section structure. The LLM followed the spec's 11-section structure faithfully, which then required restructuring in the evaluated final analysis. The spec author (me) failed to reconcile its own Section 11 with the upstream rubric. |

---

## 2. Top three gaps with evidence

### Gap 1: Spec did not prohibit external knowledge substitution when silent on a sub-component

- **Where it surfaced:**
  - Section 7 of the Gemini raw output (Liquidity Profile): the LLM computed an Adjusted Cash Ratio of 1.85× using SEK 974,935K for current contract liabilities. This value is not in the spec; it is in the Annual Report on page 92.
  - Section 6 of the Gemini raw output (Leverage): the LLM stated *"propose an extraordinary dividend of SEK 1.00/share alongside the SEK 1.10 ordinary dividend"*. The spec contains only the aggregate `INC_dividends = 404,602`; the 1.10 + 1.00 split is sourced from the AR.
  - Section 5 of the Gemini raw output (Hypothesis H1): the LLM stated *"supplementary data from the Annual Report indicates that historical collection cycles hovered around 45–50 days"*. This figure does not appear in the spec, the workbook, or — verified by manual recompute — the Annual Report itself.
- **Spec cause:** The spec aggregated contract liabilities into `BAL_other_current_liabilities_curr` (1,570,554) and aggregated the dividend into `INC_dividends` (404,602) without breaking out the sub-components the analysis in Section 8 of the spec asked for (specifically the "adjusted view excluding deferred revenue"). The spec also did not include a rule prohibiting external lookups when the spec is silent on a data point. The LLM was therefore given an unsolvable task with a default option (fabricate or pull from AR), and it chose the path of least resistance.
- **Fix (exact language):** Add to Part A.3 a new sub-section labeled "Data discipline boundary": *"The executor must use only the values provided in this specification. If a computation requires a value not in this spec (e.g., a sub-component of a named-range aggregate), the executor must flag the gap explicitly with the phrase 'Spec gap: [item] not available; computation deferred to manual analysis' rather than sourcing the value from the underlying filings."* Then add to Part A.3.1 a broken-out line: `contract_liabilities_current` (974,935) and `contract_liabilities_non_current` (26,342), with the sub-aggregation rule documented.

### Gap 2: Hypothesis H1 testing required data the model does not contain — the spec did not surface this dependency

- **Where it surfaced:** Section 5 of the Gemini raw output: the LLM produced a confident verdict on Hypothesis H1 ("DSO has lengthened, partially supporting H1") using a hallucinated 45–50-day historical baseline. The verdict appears authoritative because the supporting number is presented without qualification — but the underlying data point was not in the spec. When my manual recompute used FY23/24 sales (2,963,607) from the Annual Report as a denominator proxy, DSO came to 70.4 days, which contradicts the LLM's directional claim entirely. This is the single largest analytical error the LLM made, and it directly affects the H1 conclusion in the final analysis.
- **Spec cause:** Hypothesis H1 in Part B.8 (and inherited from Stage 2) called for a year-over-year DSO trend comparison. The single-period model contains current-year DSO (64.40 days) but not the prior-year DSO — because `INC_sales_prior` is not a named range in the spec (the workbook is structurally a single-period model). The spec asked for a test it did not provide the data for, and did not flag the gap.
- **Fix (exact language):** Add to Part B.8 (Analysis Requirements) under the Efficiency category: *"H1 testing requires a prior-year DSO baseline. The single-period model does not provide `INC_sales_prior` as a named range. If H1 must be tested, the executor should either (a) state explicitly that the spec lacks the data and defer the verdict, or (b) compute a year-prior proxy by treating `BAL_receivables_prior` as ending-of-FY23/24 receivables against FY23/24 sales — and disclose this convention. The executor must not fabricate a baseline value."* Then add `INC_sales_prior` (FY2023/2024 net sales: SEK 2,963,607K) to Part A.3.2 as an optional input for this specific test.

### Gap 3: Spec's Section 11 output structure conflicts with the brief Stage 5 grading rubric — LLM faithfully reproduced the misaligned structure

- **Where it surfaced:** Sections 1–11 of the Gemini raw output: the LLM produced exactly the 11-section structure the spec called for (Executive Summary, Company/Reporting Context, Performance/MVA, Profitability/H2, Efficiency/H1, Leverage/H3, Liquidity, Du Pont, Strategic Recommendations, Limitations, References) — including a separate "Limitations" section the brief Stage 5 rubric does not have, and *without* an "LLM Evaluation" section the brief rubric requires. The LLM's faithful execution of a misaligned spec is itself the surfaced behavior — when the spec and the grading criterion disagree, the LLM follows the spec, and the human reviewer is left with the restructuring work. In my case I had to reorganize the 11 sections into 6 in the evaluated final analysis, and the LLM Evaluation section had to be authored from scratch.
- **Spec cause:** I authored the spec's Section 11 (Output Format) based on what I thought the LLM should produce, without explicitly mapping it back to the Stage 5 grading rubric. The spec was internally consistent but externally misaligned with the assessment criterion. This is a different *category* of gap from Gaps 1 and 2 — it is a quality-of-specification issue, not a data-availability issue — but the symptom in the LLM output (an 11-section deliverable that needs reshaping before submission) is concrete and measurable.
- **Fix (exact language):** Replace Part B.11 (Output Format) opening paragraph with: *"The output must conform to the six-section structure mandated by the Stage 5 brief: (1) Company & Data Summary, (2) Ratio Results & Interpretation (covering Performance, Profitability, Efficiency, Leverage, Liquidity), (3) Du Pont Analysis, (4) Strategic Recommendations, (5) LLM Evaluation & Annotations (to be completed by the human reviewer, not the LLM), (6) Executive Justification (human voice required). Within Section 2 the LLM should follow the five-category internal structure below."* Then re-label the existing sub-section guidance as the internal structure of brief-Section 2.

---

## 3. Revisions

1. **Add a "Data discipline boundary" sub-section to Part A.3 with the explicit prohibition language above, and break out `contract_liabilities_current` (974,935) and `contract_liabilities_non_current` (26,342) as their own named ranges** — addresses **Gap 1**. This single change would have prevented all three of the LLM's external-source incidents (Adjusted Cash Ratio input, dividend split, and arguably reduced the temptation that led to the H1 fabrication).

2. **Add `INC_sales_prior` (2,963,607) to Part A.3.2 as an optional input plus an explicit instruction in Part B.8 on what to do when H1 prior-year data is unavailable** — addresses **Gap 2**. This converts H1 from a test the LLM was forced to guess at into a test the LLM can either complete or defer with disclosure — eliminating the hallucination pathway entirely.

3. **Rewrite Part B.11 (Output Format) to mirror the Stage 5 grading rubric's six-section structure rather than the spec's own 11-section instinct, with sub-section internal structure within brief-Section 2** — addresses **Gap 3**. This aligns the LLM's output with the structure that will be graded, eliminating the restructuring overhead in the evaluated final analysis.

---

## 4. Effectiveness rating

| Rating | Anchor |
|---|---|
| 5 | I would hand this spec to a junior analyst and trust their output without re-checking. |
| 4 | Solid overall; one section needs sharpening before I'd ship it. |
| **3** | **Workable with revisions; spec has gaps the LLM had to guess around.** |
| 2 | Substantial rework needed; LLM output diverged in meaningful ways traceable to the spec. |
| 1 | Spec is not yet usable as a standalone artifact. |

**My rating: 3**

**Justification (165 words):**

I rate this spec a 3 because two of the eleven sections (Part A.3 Data Inputs and Part B.8 Analysis Requirements) had gaps the LLM had to guess around, and those gaps produced one substantive analytical error — the H1 hallucination — that affected a hypothesis conclusion in the final analysis. A 4 rating would require that only one section needed sharpening; mine had two, plus a third structural mismatch (Part B.11 vs the Stage 5 rubric) that did not affect analytical correctness but did force reorganization downstream. A 2 rating would require that LLM output diverged in meaningful ways across multiple sections — but in fact the spec performed strongly on numerical correctness (5 of 7 graded ratios tied exactly to manual recompute), on the Du Pont decomposition (both variants produced correctly with V-DP-2 acknowledged), and on the strategic recommendation structure. The gaps are concentrated, identifiable, and fixable with the three revisions in Section 3 — which is the textbook definition of a 3.

---

## 5. Forward link

For the next spec I write — for Sectra a year from now, for a different company, or for a non-finance domain like a product-launch plan — I will add a "Data discipline boundary" section as a default part of every spec template, treating the prohibition against external substitution as a first-class requirement rather than an unstated assumption.

---

## 6. Retrospective process feedback (≤150 words)

Filling out Section 1 (the section-by-section verdict table) surfaced something a free-form write-up would have hidden: I had to **rate** Validation Rules as "Vague" even though all eight rules were syntactically present, because the LLM's behavior showed the rules did not anticipate the external-substitution pattern. The act of forcing a Clear/Vague/Missing verdict revealed that "complete on paper" and "complete in practice" are different standards — I would not have caught this with a freeform reflection. (147 words)

**One structural change I would suggest to the template:** add a column to the Section 1 table labeled *"LLM behavior pattern"* with a small fixed vocabulary (Followed-verbatim / Substituted-from-external / Fabricated / Restructured / Skipped). Forcing a categorical pattern alongside the Clear/Vague/Missing verdict would make it harder to give a Clear rating to a section the LLM technically followed but practically circumvented — exactly the failure mode my Validation Rules section exhibited.
