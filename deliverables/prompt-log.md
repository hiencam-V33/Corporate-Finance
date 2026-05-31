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

> **2026-05-31 reconciliation note (added at Stage 5):** The "~590 words" estimate above was the self-counted value at submission time and did not match what the grading rubric measured. The instructor's Stage 2 PR feedback (May 22, 2026) measured prose at approximately 1,153 words against the 400–600 target. A recount at Stage 5 using a standardized methodology (Executive Summary through Limitations, excluding YAML frontmatter, headers, bold markers, and References) found 868 prose words. The discrepancy between the original 590 self-count, the 868 standardized recount, and the 1,153 instructor measurement reflects different word-counting conventions (likely whether frontmatter, bullet content, blockquote content, and references are included). The instructor's count is the binding one for grading. The submission was over the senior-analyst memo target regardless of which count is used. Action taken at Stage 5: shipped a revised memo at 478 prose words at `docs/decisions/2026-05-31-cam-sectra-selection-revised.md`. See `docs/decisions/2026-05-31-cam-stage2-feedback-response.md` for the full feedback response.

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

---

## Stage 5 — Session 1: Spec execution against fresh LLM (Gemini 2.5 Pro)

**Date:** 2026-05-31
**Tool:** Google Gemini 2.5 Pro (web interface, no other context)
**Session purpose:** Execute the Stage 4 spec against a fresh LLM with no other context, per the Stage 5 brief's discipline requirement ("Paste your Stage 4 specification as the input — nothing else").

**Workflow:**

1. Opened a fresh Gemini 2.5 Pro chat with no prior context and pasted the full text of `docs/specs/2026-05-30-cam-sectra-spec.md` as the only input — no preamble, no system prompt additions, no "please also consider…" supplements.
2. Allowed the model to produce the analysis end-to-end without follow-up prompts or corrections during generation, so the raw output represents what the spec alone elicits.
3. Saved the complete unedited response to `deliverables/2026-05-31-cam-sectra-llm-raw.md` — 11 sections matching the spec's Section 11 Output Format requirement (Executive Summary, Company/Reporting Context, Performance/MVA, Profitability/H2, Efficiency/H1, Leverage/H3, Liquidity, Du Pont, Strategic Recommendations, Limitations, References).
4. Read the output once end-to-end before doing any verification work to form a first-impression read of where the LLM was confident vs hedged.

**Verification steps:**

All numerical and methodological verification was deferred to Stage 5 Session 2 (manual verification) — the discipline is to confront discrepancies in a separate pass rather than smooth them out in-line during reading. The raw output was not modified during or after this session.

**What I kept:** The entire raw output unedited as the Stage 5 artifact.
**What I changed:** Nothing in the raw output. All edits, corrections, and annotations live in the evaluated final analysis (`deliverables/2026-05-31-cam-sectra-final-analysis.md`).

**Observation on LLM behavior worth flagging here (before later annotation):** Gemini cited several values that were *not in the spec* — most notably the SEK 974,935K current contract-liabilities figure used in the Adjusted Cash Ratio, the SEK 1.10 + SEK 1.00 dividend split, and a historical DSO baseline of "45–50 days." The spec did not provide these values, did not prohibit external sourcing, and did not direct the model on how to handle a spec-silent input. The model defaulted to filling the gaps from the Annual Report (the first two) or fabricating outright (the third). This pattern is the central finding of the Stage 5 retrospective.

---

## Stage 5 — Session 2: Manual verification + final analysis + spec retrospective drafting

**Date:** 2026-05-31
**Tool:** Claude (Anthropic, claude-opus-4-7) via web chat
**Session purpose:** Verify Gemini's raw output against the Stage 3 workbook by hand, write the evaluated final analysis with corrections and executive voice, draft the spec retrospective using the instructor template, and incorporate Stage 2 + Stage 3 PR feedback.

**Workflow:**

1. **Verification table first (brief's required discipline).** Selected seven ratios across four of the six rubric categories — Performance (EVA), Profitability (ROA, Underlying OM), Efficiency (Asset Turnover, DSO baseline check), and Liquidity (Cash Ratio standard, Adjusted Cash Ratio) — biased toward ratios the LLM is most likely to get wrong (NOPAT-based ROA, start-of-year EVA, by-nature underlying operating margin, adjusted cash ratio with deferred-revenue strip-out, DSO historical baseline check). Leverage and Du Pont were not separately re-verified in the table because the Du Pont decomposition is itself an identity check against the direct ratios already recomputed (ROA, ROE, NPM, AT), and Leverage's structural finding (LT debt 3.22% vs total 48.97%) was a categorical interpretation rather than a computation in dispute. Recomputed every value by hand from `models/builds/2026-05-17-cam-sectra-financials.xlsx` using the named-range notation from the spec. Built the six-column comparison table (Ratio · Formula · Manual · LLM · Match? · Note) at `analysis/validation/2026-05-31-cam-sectra-stage5-verification.md`.
2. **Confronted two discrepancies in the verification before writing anything else.** The Adjusted Cash Ratio used a SEK 974,935K input the spec did not provide. The DSO historical baseline of "45–50 days" did not appear in any input. Manual recompute using FY23/24 sales (2,963,607 from AR p. 92) gave a 70.4-day proxy — methodologically distinct from the workbook's DSO formula but in the same range as the current 64.40 figure. The LLM's claim that "DSO had lengthened" was therefore unsupported by data the spec contained.
3. **Authored the evaluated final analysis** (`deliverables/2026-05-31-cam-sectra-final-analysis.md`) restructured to the brief Stage 5's six-section format (not the spec's 11-section structure): Company & Data Summary, Ratio Results & Interpretation (sub-sectioned by the five non-Du-Pont categories), Du Pont Analysis, Strategic Recommendations, LLM Evaluation & Annotations, Executive Justification. Five strategic recommendations with distinct addressees (Sectra IR/CFO, Board, equity investor, CEO/CFO, Vietnam-market distributor team), each with addressee · evidence · action · timeline · counter-argument structure.
4. **Wrote Section 5 (LLM Evaluation) as a structured tri-pattern critique:** (5.1) what the LLM did correctly, (5.2a) external knowledge substitution where the spec was silent, (5.2b) output format drift between spec Section 11 and brief rubric, (5.2c) outright hallucination of the DSO baseline, (5.3) a summary table distinguishing spec gaps from LLM limitations.
5. **Wrote Section 6 (Executive Justification) in personal voice** anchored to my operator context — VEMBA student also evaluating PACS distribution in Vietnam, with first-hand market knowledge about cloud adoption barriers, on-premise dominance, and the 5-year finance-lease commercial structure that makes Vietnamese unit economics structurally different from Sectra's Swedish model. Included one original analytical insight not in any of the spec or LLM output: that Sectra's IFRS by-nature reporting *prevents* unit-economics disclosure at the product-mix level (the "Goods for resale" line of SEK 441,712K captures only third-party hardware; software-delivery costs are blended into Personnel costs), which means a Vietnamese distributor cannot extrapolate Sectra Sweden's 18.92% blended margin to a Vietnamese deal mix.
6. **Drafted the spec retrospective** (`deliverables/2026-05-31-cam-sectra-spec-retrospective.md`) using the instructor template at `docs/templates/spec-retrospective-template.md`. Eleven section-by-section verdicts (seven Clear, four Vague), three gaps with evidence-tied surface symptoms (the external-knowledge substitution, the H1 data dependency the spec did not surface, the spec Section 11 vs brief rubric structure mismatch), three revisions each addressing one gap, effectiveness rating of 3 with 165-word justification, forward link on data-discipline-boundary as a default spec section, Section 6 process feedback at 147 words proposing an "LLM behavior pattern" column for the Section 1 verdict table.
7. **Incorporated Stage 2 + Stage 3 PR feedback** (5% of Stage 5 rubric). Stage 2 received 97.11% with one critique: "prose ~1153 words, target 400–600, tighten repetitive sections." Drafted a revised memo at 478 prose words at `docs/decisions/2026-05-31-cam-sectra-selection-revised.md` (45% reduction; preserved all three hypotheses and the Selection Rationale structure). Stage 3 received 99% with no actionable critique — only forward guidance on Stage 4 named-range usage and HIL iteration, both of which were executed in the actual Stage 4 spec. Documented both feedback responses in `docs/decisions/2026-05-31-cam-stage2-feedback-response.md` and added a blockquote acknowledgment to the final analysis preamble.

**Verification steps:**

- Recomputed all seven ratios in the verification table by hand from the workbook data, with arithmetic shown in the Manual column. Five of seven tied exactly to Gemini's stated values; two failed but the arithmetic discrepancy was traceable to the LLM's external sourcing, not to computation error.
- Cross-checked every numerical claim in the final analysis (17 key values audited) against the Stage 3 workbook and the verification table. Caught and corrected one rounding error during audit (Equity Multiplier 2.044× → 2.046×, where 2.0457163... rounds to 2.046 at three decimals).
- Audited the spec retrospective for evidence-tied verdicts (all four Vague rows reference specific Gemini output symptoms — no "Part A.4 was OK" entries), word-count claims (Justification 165 words = actual; Section 6 147 words ≤ 150-word limit), and revision specificity (15 named-range / Part-section references in three revisions).
- Adversarial audit in the role of the grading instructor caught and fixed one logic inconsistency in the spec retrospective Section 1 verdict for Part A.7 ("LLM applied 6 of 8 rules… V-BS-1 implicitly assumed… V-CF-2 addressed correctly" was contradictory; rewritten to clarify that 6 rules were *explicitly cited* and 2 were *satisfied without explicit citation or with exceeded scope*).

**What I kept:** Five of seven ratios from Gemini's output unchanged (they tied to manual recompute); the structural framework of Gemini's 11-section output reorganized into the brief's six sections; my own Vietnam-market insights and the by-nature unit-economics observation as the distinctive contribution to Section 6.
**What I changed:** Reframed Hypothesis H1 from "DSO has lengthened" (LLM's conclusion based on the hallucinated baseline) to "DSO is approximately stable in the 60–70 day band — H1 not supported in the direction predicted." Stripped out the patent-settlement SEK 110M in every operating-margin discussion (per V-EBIT-1). Annotated the Adjusted Cash Ratio with a clear callout that the SEK 974,935K input was external to the spec. Restructured the entire LLM output from 11 sections into the brief's six sections.

### Closing observation on the workflow

The most valuable single artifact in this stage was the seven-row manual verification table. Without it, the LLM's confidently-stated DSO baseline of 45–50 days would have flowed through into the final analysis as fact, and Hypothesis H1 would have been "supported" on a number that does not exist. The discipline of computing five-to-seven ratios by hand before writing any narrative is the transferable skill this stage exists to teach — and it caught exactly the kind of hallucination the rubric is implicitly testing for.
