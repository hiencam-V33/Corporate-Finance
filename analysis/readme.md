# analysis

Validation, self-audit, and review work. The discipline this folder enforces is that **verification is a separate artifact from analysis** — you don't smuggle the check into the conclusion; you write it down where someone can audit your audit.

## Subdirectories

- [`validation/`](./validation) — Stage 5 manual ratio verification (re-deriving ratios by hand from the Stage 3 workbook to cross-check the LLM's output), plus any HIL (human-in-the-loop) iteration notes from Stage 4 that document spec gaps caught before Stage 5.

## What belongs here

- Manual recomputations and arithmetic checks against the model's computed values.
- Side-by-side comparisons of expected vs. actual outputs.
- Self-audit notes documenting what was checked, what was found, and what was decided.
- HIL iteration logs explaining gaps caught and the fixes applied.

## What does NOT belong here

- The Excel workbook itself — use [`models/`](../models).
- The final analysis or strategic recommendations — use [`deliverables/`](../deliverables).
- The specification being validated — use [`docs/specs/`](../docs/specs).

## How this folder fits the project

The Stage 5 manual verification table in [`validation/`](./validation) was the discipline that caught the LLM's hallucinated DSO baseline ("45–50 days" — a value not present in any spec or source document). Without the manual recompute, the LLM's claim that "DSO had lengthened" would have flowed through into the final analysis as fact, and Hypothesis H1 would have been "supported" on a number that does not exist. The seven-row table is the most important artifact in this folder.
