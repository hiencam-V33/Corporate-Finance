# analysis/validation

Manual verification artifacts that cross-check the model's and the LLM's outputs against hand-computed values. This is the discipline check that turns "the LLM said so" into "the LLM said so, and the arithmetic ties."

## What's in here

- **`2026-05-31-cam-sectra-stage5-verification.md`** — Stage 5 manual ratio verification table. Seven ratios across four of the six rubric categories (Performance, Profitability, Efficiency, Liquidity), biased toward ratios the LLM was most likely to get wrong (NOPAT-based ROA, start-of-year EVA, by-nature underlying operating margin, adjusted cash ratio with deferred-revenue strip-out, DSO historical baseline check). Six-column format: Ratio · Formula (named-range notation) · Manual value with arithmetic shown · LLM's value · Match? · One-line explanatory note.

## What the verification table caught

Five of seven ratios tied exactly to Gemini 2.5 Pro's stated values. Two failed:

1. **Adjusted Cash Ratio** — Arithmetic ties (1.847× = 1,341,871 / (1,701,450 − 974,935)), but the SEK 974,935K contract-liabilities figure used as the denominator adjustment was sourced from the Annual Report (p. 92), not from the spec. The spec only provided the aggregate `BAL_other_current_liabilities_curr` (1,570,554). A spec-discipline failure rather than an arithmetic one.

2. **DSO historical baseline** — The LLM claimed "DSO hovered around 45–50 days" historically, but no source document contains that range. Independent recompute using FY23/24 sales (2,963,607 from AR p. 92) gave a 70.4-day proxy, which is methodologically distinct from the workbook's DSO convention but in the same general range as the current 64.40 figure. The gap between 45–50 and 70.4 is too large to reconcile with any convention. **Hypothesis H1's predicted direction of DSO lengthening is therefore not supported** — DSO appears approximately stable in the 60–70-day band.

The full table with arithmetic shown is in the linked file.

## Why this is graded separately

The Stage 5 brief weights this artifact at 10% of the stage score independently of the final analysis. The reason is that verification is a transferable skill: any future LLM-assisted analysis you do in a corporate-finance, equity-research, or audit role will succeed or fail on whether you (a) recompute the numbers by hand before believing them, and (b) document the recompute in a way an auditor could reproduce.

## Naming convention

Files follow `YYYY-MM-DD-{lastname}-{company-slug}-stage5-verification.md` per the project-wide convention. If Stage 4 HIL iteration notes are present, they follow `YYYY-MM-DD-{lastname}-{company-slug}-stage4-iteration.md` — at this writing, no separate Stage 4 HIL file exists in this folder because the HIL fix (the `_curr` / `_prior` named-range convention deviation) is documented inline in the [Stage 4 prompt log entry](../../deliverables/prompt-log.md) and surfaced in the [Stage 5 spec retrospective](../../deliverables) Part A.4 verdict.

## How this folder fits the project

The verification table sits between [`models/builds/`](../../models/builds) (which it audits arithmetically) and [`deliverables/`](../../deliverables) (which it informs through the discrepancies it flags). The two failures it caught are the central evidence for the spec retrospective's three gaps and for the final analysis Section 5 (LLM Evaluation).
