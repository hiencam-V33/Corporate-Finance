# Prompt Log — BUS 629 AI Project

This file records meaningful AI sessions used across the BUS 629 project stages, per Professor Stauffer's AI Use Policy. Format: date | stage | tool | brief description | what was kept/changed.

## Stage 2 — Sectra AB Company Selection Memo

**Date:** 2026-05-17
**Tool:** Claude (Anthropic)
**Session purpose:** Draft Stage 2 company selection memo for Sectra AB.

**Workflow:**
1. Discussed company shortlist with Claude (Vietnamese pharma, ASEAN healthcare, global medtech, Vietnamese non-healthcare). Selected Vietnamese healthcare first; later pivoted to international PACS/AI segment.
2. Compared Sectra AB vs Pro Medicus (ASX: PME) head-to-head on financial performance, business model maturity, and Vietnam-market fit. Selected Sectra over PME due to richer ratio dynamics from ongoing SaaS transition, broader customer tier suitability for Vietnam, and global expansion DNA.
3. Verified Sectra eligibility against four mandatory criteria from Stage 2 spec (publicly traded, annual report available, non-financial, ≥2 years comparable data) — all confirmed.
4. Searched Sectra FY2024/2025 financials, recent M&A (Oxipit acquisition, Paige.AI partnership), and KLAS PACS competitive positioning to gather evidence for hypothesis construction.
5. Drafted three hypotheses (Working Capital/DSO, Profitability/Operating Margin, Cash Conversion + FX) in "I expect X because Y" format with directional, falsifiable predictions tied to specific evidence (Québec deal, CEO guidance, SEK 110M patent settlement, cash conversion 1.64x).
6. Added emerging-market healthcare procurement perspective (CAPEX-to-OPEX shift; 12–24 month payment cycles in public hospitals) as comparative industry observation in H1.
7. Drafted Selection Rationale around three converging dimensions: industry alignment, analytical richness, international finance.
8. Generated full memo in the instructor-provided memo template format with YAML frontmatter intact; word count ~590 words (within 400–600 range).

**Verification steps:**
- Cross-checked FY2024/2025 figures (SEK 3,239.8M revenue, 18.9% underlying margin, SEK 110M patent settlement, SEK 922.4M CFO) against multiple sources: Sectra year-end press release, Year in Brief, third-party aggregators.
- Confirmed Pro Medicus FY2025 figures from Simply Wall St and PME investor announcements.
- Verified Nasdaq Stockholm Large Cap segment classification via Sectra IR listing data page.

**What I kept:** Three hypotheses, structure of Selection Rationale, all data points and references.
**What I changed:** Tone tuned from "due diligence intent" to neutral academic framing to preserve commercial confidentiality (public repo). Specific company and competitor brand names were anonymized to "Vietnam's medical equipment sector" and "legacy on-premise PACS vendors."

---

## Stage 4 — Technical Specification for Sectra Ratios Model

**Date:** 2026-05-30
**Tool:** Claude Code (Anthropic, claude-opus-4-7, 1M context) — Workflow B from the Stage 4 brief.
**Session purpose:** Draft a technical specification at `docs/specs/2026-05-30-cam-sectra-spec.md` that fully defines the Sectra ratio model (Part A) and the Stage 5 analytical work (Part B), precise enough that a fresh LLM given only the spec can reproduce a correct, comprehensive ratios analysis.

**Workflow:**
1. Pointed Claude Code at the four required inputs: the Stage 4 brief (raw URL), the spec template (raw URL), `models/templates/performance-ratios-template.xlsx`, and the populated Stage 3 workbook `models/builds/2026-05-17-cam-sectra-financials.xlsx`. Read the existing Stage 2 selection memo for hypothesis context.
2. Extracted the workbook structure two ways: (a) parsed `xl/workbook.xml` after unzipping the `.xlsx` to enumerate all 79 named ranges; (b) opened both workbooks via Excel COM (PowerShell) to dump every populated cell with value **and** formula, so the spec could quote real numbers, real formulas, and verify each ratio output rather than re-derive.
3. Drafted Part A item-by-item against the Stage 4 component list (1 Scope · 2 Architecture · 3 Data Inputs · 4 Named Range Conventions · 5 Derived Inputs · 6 Ratio Definitions · 7 Validation Rules), preserving the spec-template numbering for Part B (Analysis · Du Pont · Recommendations · Output Format).
4. Forced every data value in the spec to come **numerically** from the Sectra workbook — no "TBD" placeholders. Included unit notes (SEK thousand), the `yearCurrent = 2024` driver semantics, and explicit formulas in named-range notation.
5. Built validation rules from material I'd already discovered while reading the Notes tab: BS-balance ✓, Du Pont ROA = Direct ROA ✓, Du Pont ROE ≠ Direct ROE (time-mismatch, explain), reported-vs-underlying EBIT (722,997 vs 612,997 after stripping the SEK 110M patent settlement), template CFO 839,295 vs audited CFO 922,364 reconciliation, dividend-proposal vs share-redemption tie, EPS sanity check (SEK 2.92).
6. Wrote Part B by hanging each subsection on a Stage 2 hypothesis (H1 working capital ↔ Efficiency; H2 profitability ↔ Profitability; H3 cash conversion ↔ Cash flow) so the Stage 5 analysis has a built-in scaffold to test against.
7. Defined the Stage 5 output format down to section count (11), word target per section, decimal precision (two for %, three for ×), and citation discipline ("no unsourced numbers").

**Verification steps:**
- Cross-checked the spec's quoted ratio outputs against `Ratios!C43:C76` cell values (MVA 55,228,352; ROA 18.24%; ROE 35.89%; current ratio 1.74; cash ratio 0.79; Du Pont ROA match ✓). All tie.
- Re-derived the underlying operating margin (612,997 / 3,239,811 = 18.92%) and confirmed it matches the 18.9% figure used throughout the Stage 2 memo.
- Confirmed `shares_outstanding` unit convention (entered as thousand-shares) by recomputing EPS = 563,371 / 192,667 = SEK 2.92 against Sectra's reported figure.

**What I kept:** Entire spec structure, all 25 ratio definitions, validation rules, Stage 5 output format.
**What I changed:** See HIL note below.

### HIL iteration — named-range convention gap (before/after)

**Gap identified.** My first-draft spec wrote ratio formulas using the convention the Cover sheet **documents** — `BAL_[item]_[yr]` with a literal year suffix, e.g. `BAL_assets_total_2025 / BAL_assets_total_2024`. When I cross-checked against the actual `definedName` entries parsed out of `xl/workbook.xml`, the workbook implements `_curr` / `_prior` aliases instead (`BAL_assets_total_curr`, `BAL_assets_total_prior`), driven by a `yearCurrent = 2024` cell on `Ratios!C6`. None of the `_[yr]` named ranges exist. A Stage 5 LLM fed the first-draft spec would have written formulas like `BAL_assets_total_2025` that Excel could not resolve, and would either (a) silently produce zeros, or (b) hallucinate a corrected naming and then drift from the model. Worse, the spec inherited a real ambiguity from the Cover sheet itself, so the gap was *baked into the documentation* and would have propagated.

**Fix.** I added a dedicated Section 4 "Named Range Conventions" that states the implemented `_curr` / `_prior` pattern explicitly, lists the aliases alongside their start-of-year / current-year `startYear_*` / `currentYear_*` derived equivalents, and ends with a one-paragraph "Convention deviation to be aware of" footnote that quotes the Cover-sheet documentation, names the implementation difference, and tells the analysis writer to use the `_curr` / `_prior` form. All subsequent Part-A formulas were rewritten in the implemented convention. I also propagated the same convention into the Validation Rules (rule 8, unit consistency) and the Output Format (style requirement: "use named ranges in inline math"). This converts a silent failure mode into a directive, which is exactly the kind of gap the Stage 4 rubric is asking us to surface.
