# docs

This directory is the written-word layer of the BUS 629 portfolio. It holds every artifact whose primary purpose is to explain, decide, plan, or standardize — not to compute. Anything a reader (Prof. Stauffer, a teammate, a future employer) would read to understand *why* something was built or *how* it should be used belongs here.

The folder is organized into four sub-areas: `decisions/` for decision records, `specs/` for technical and analytical specifications, `plans/` for project plans and timelines, and `templates/` for the canonical Stage 0 course templates supplied by the instructor.

## Naming conventions

- General documents: `[TYPE]_[Topic]_[YYYY-MM-DD].md` (e.g. `DECISION_ModelingApproach_2026-05-15.md`).
- Versioned documents: append `_v[N]` before the date (e.g. `SPEC_DCF_Assumptions_v2.md`).
- Use kebab-case for multi-word topics inside the slug; never use spaces.
- All dates are ISO-8601 (`YYYY-MM-DD`), not US-style.

## What goes here

- Index/landing READMEs that route the reader to the right sub-folder.
- Cross-cutting documentation that spans multiple sub-areas.
- Top-level reference pages and glossaries used across the project.

## What does NOT go here

- Excel models or workbooks (use `models/`).
- Raw data files, CSVs, or extracts (use `data/`).
- Validation reports or audit outputs (use `analysis/validation/`).
- Final presentation-ready deliverables (use `deliverables/`).
- Working notes or scratch files that are not intended to be read by anyone else.
