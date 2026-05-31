# docs/decisions

Decision memos documenting the major choices made during the BUS 629 Sectra project. Each memo is written in the senior-analyst memo format the course teaches — short, structured, and traceable to specific evidence.

## What's in here

- **`2026-05-17-cam-sectra-selection.md`** — Stage 2 company-selection memo. The original submission. Scored 97.11% (4.37 / 4.5) by Professor Stauffer with one actionable critique: the prose exceeded the 400–600-word senior-analyst target.
- **`2026-05-31-cam-sectra-selection-revised.md`** — Revised Stage 2 memo at 478 prose words, addressing the length critique while preserving all three hypotheses (H1 working capital, H2 profitability, H3 cash conversion + FX) and the three-dimension selection rationale (industry alignment, analytical richness, international finance dimension).
- **`2026-05-31-cam-stage2-feedback-response.md`** — Documents both the Stage 2 PR feedback (97.11%, prose-length critique) and the Stage 3 PR feedback (99%, no actionable critique but forward guidance on named-range usage and HIL iteration that was executed in Stage 4). Explains what changed in the revised memo and what was learned.

## Why both Stage 2 versions are preserved

The original 2026-05-17 memo is preserved as the historical submission record — it is the version Professor Stauffer's PR review measured against. The revised 2026-05-31 version is the analytically anchored version that the downstream Stage 3 / 4 / 5 work builds on. Keeping both visible (rather than overwriting the original) maintains the audit trail that an academic or professional reviewer would expect.

## Naming convention

- Stage 2 selection memo: `YYYY-MM-DD-cam-sectra-selection[-revised].md`
- Stage 2 feedback response: `YYYY-MM-DD-cam-stage2-feedback-response.md` (no company slug — the document is about feedback process, not company analysis)

## How this relates to other folders

- The hypotheses introduced here (H1, H2, H3) are tested against computed ratios in [`models/builds/`](../../models/builds) (Stage 3 workbook) and discussed in detail in [`deliverables/2026-05-31-cam-sectra-final-analysis.md`](../../deliverables) (Stage 5 final analysis Section 2 and Section 6).
- The Stage 4 technical specification in [`docs/specs/`](../specs) operationalizes these hypotheses for LLM execution.
