# docs/specs

Technical specifications written in a form precise enough that a fresh LLM, given only the spec as input, can reproduce the intended analysis without additional context. This is the "spec-driven design" discipline the course teaches: separate the specification of analytical work from its execution.

## What's in here

- **`2026-05-30-cam-sectra-spec.md`** — Stage 4 specification for the Sectra ratios analysis. Two parts: **Part A** (Architecture, Data Inputs, Named Range Conventions, Derived Inputs, Ratio Definitions, Validation Rules) defines the model the LLM reads; **Part B** (Analysis, Du Pont, Recommendations, Output Format) defines the analytical work the LLM produces. Forces every formula into named-range notation (e.g. `BAL_assets_total_curr`, `INC_sales`) so the LLM can locate cells unambiguously.

## How this folder fits the project

The Stage 4 spec is the input that drives Stage 5's automated ratio review. The Stage 5 LLM execution (`deliverables/*-llm-raw.md`) was produced by pasting this spec — and only this spec — into Google Gemini 2.5 Pro with no other context. The Stage 5 final analysis (`deliverables/*-final-analysis.md`) evaluated where that execution succeeded and where it deviated, and the Stage 5 spec retrospective (`deliverables/*-spec-retrospective.md`) graded the spec itself against that execution evidence.

## Spec quality discipline

A spec is "good" to the extent that an LLM given only the spec produces a correct, comprehensive analysis. The HIL iteration documented in [`deliverables/prompt-log.md`](../../deliverables/prompt-log.md) for Stage 4 captures one such gap caught before Stage 5: the workbook's Cover sheet documents `BAL_[item]_[yr]` naming with year literals, but the implementation uses `_curr` / `_prior` aliases. The first-draft spec inherited the Cover-sheet convention, which would have caused every Excel formula reference in the LLM output to fail silently. The fix — a dedicated Section 4 "Named Range Conventions" — converted a silent failure mode into a directive.

## Naming convention

Files follow `YYYY-MM-DD-{lastname}-{company-slug}-spec.md` per the project-wide convention.

## Where to look next

- The spec is executed at: [`deliverables/2026-05-31-cam-sectra-llm-raw.md`](../../deliverables) (raw output) and [`deliverables/2026-05-31-cam-sectra-final-analysis.md`](../../deliverables) (evaluated).
- The spec is critiqued at: [`deliverables/2026-05-31-cam-sectra-spec-retrospective.md`](../../deliverables) (Section-by-section verdict, top three gaps with evidence, three revisions, effectiveness rating).
