# docs

This directory holds the written deliverables of the BUS 629 project: decision memos, technical specifications, and any plans or templates that are textual rather than computational. In the project's separation of concerns, `docs/` is where written reasoning lives, `models/` is where computations live, `analysis/` is where validation lives, and `deliverables/` is where the polished outputs live.

## Subdirectories

- [`decisions/`](./decisions) — Stage 2 company-selection memo (and any subsequent decision memos). The original 2026-05-17 memo and the revised 2026-05-31 version after instructor PR feedback both live here, alongside the Stage 5 feedback-response memo.
- [`specs/`](./specs) — Stage 4 technical specification that drives the Stage 5 LLM execution. Written in named-range notation so a fresh LLM with no other context can reproduce the analysis from the spec alone.

## What belongs here

- Memos addressed to the instructor or to a hypothetical stakeholder (selection rationale, decision documentation, response to PR feedback).
- Technical specifications describing how analytical work should be executed.
- Plans, schemas, or written templates that downstream code or models consume.

## What does NOT belong here

- Excel workbooks or models that compute values — use [`models/`](../models).
- Source financial data — use [`data/`](../data).
- Verification or validation outputs — use [`analysis/`](../analysis).
- Polished final outputs from Stage 5 — use [`deliverables/`](../deliverables).

## Naming convention

All files follow `YYYY-MM-DD-{lastname}-{company-slug}-{kind}.{ext}` per the project-wide convention. The only exception is the Stage 2 feedback-response memo, which omits the company slug because it documents process learning rather than company-specific analysis: `YYYY-MM-DD-{lastname}-stage2-feedback-response.md`.
