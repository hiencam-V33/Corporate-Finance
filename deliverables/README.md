# deliverables

The Stage 5 outputs — the polished, presentation-ready end products of the BUS 629 project. If a reviewer reads only one folder in this repo, this is the one.

## What's in here

- **`prompt-log.md`** — Chronological log of every meaningful AI session across the project (Stage 2, Stage 4, Stage 5 Sessions 1 and 2). Each entry documents tool used, date, session purpose, workflow steps, verification, what was kept, what was changed. Includes the Stage 4 HIL iteration note about the named-range convention gap, and the Stage 5 reconciliation note for the Stage 2 word-count discrepancy.

- **`2026-05-31-cam-sectra-llm-raw.md`** — Unedited Google Gemini 2.5 Pro output from feeding only the Stage 4 spec (no other context) into the model. Saved as the historical record of what the spec alone elicited. Eleven sections matching the spec's Section 11 Output Format.

- **`2026-05-31-cam-sectra-final-analysis.md`** — The evaluated, corrected, annotated final analysis. Six sections matching the Stage 5 brief: Company & Data Summary, Ratio Results & Interpretation, Du Pont Analysis, Strategic Recommendations (five recommendations with distinct addressees, evidence, action, timeline, and counter-argument), LLM Evaluation & Annotations, Executive Justification (in personal voice with the by-nature unit-economics observation as the distinctive contribution).

- **`2026-05-31-cam-sectra-spec-retrospective.md`** — Template-backed self-evaluation of the Stage 4 spec, using the instructor's spec retrospective template. Six sections: section-by-section verdict (eleven Clear/Vague/Missing entries with evidence-tied symptoms), top three gaps with where/cause/fix structure, three revisions each addressing one gap, effectiveness rating of 3 with a 165-word justification, forward link, and process feedback at 147 words.

## How to read this folder

The recommended reading order for a reviewer:

1. Start with the **final analysis** for the substantive output and the strategic recommendations.
2. Then read the **spec retrospective** to see how I graded my own spec against what the LLM produced.
3. Then read the **raw LLM output** alongside the [`analysis/validation/`](../analysis/validation) verification table to see exactly which parts the LLM got right and which it didn't.
4. Then read the **prompt log** for the full process audit trail.

## Naming convention

Files follow `YYYY-MM-DD-{lastname}-{company-slug}-{kind}.{ext}` per the project-wide convention. The exception is `prompt-log.md`, which is a continuously updated single-file log spanning multiple stages rather than a dated artifact.

## How this folder fits the project

This folder is the output side of the project. The inputs are: the Stage 2 memo in [`docs/decisions/`](../docs/decisions), the Stage 3 workbook in [`models/builds/`](../models/builds), and the Stage 4 spec in [`docs/specs/`](../docs/specs). The verification artifact in [`analysis/validation/`](../analysis/validation) is what makes the final analysis defensible — without that table, the LLM's claims would be unaudited assertions rather than verified outputs.

## Stage 5 brief rubric this folder addresses

- Analytical correctness (25%) — final analysis Section 2 & 3
- Manual verification artifact (10%) — lives in [`analysis/validation/`](../analysis/validation) but referenced extensively here
- LLM evaluation + spec retrospective (25%) — final analysis Section 5 + spec retrospective file
- Strategic recommendations + executive voice (20%) — final analysis Section 4 & 6
- Stage 2 feedback incorporation (5%) — addressed in [`docs/decisions/2026-05-31-cam-stage2-feedback-response.md`](../docs/decisions) with cross-reference in this folder's final-analysis preamble
- Repo polish (15%) — the structure of this repo overall, with this folder as one of the polished destinations
