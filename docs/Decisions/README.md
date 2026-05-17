# decisions

This directory stores formal decision records (ADR-style memos) that document choices made during the BUS 629 project: methodology selections, scoping calls, trade-offs between alternatives, and approvals. Every non-trivial decision that future readers might second-guess should have a memo here.

Each memo should make the decision auditable: state the question, the alternatives considered, the choice, and the reasoning. Once written, decision records are immutable — if a decision is later reversed, write a new record that supersedes the old one rather than editing history.

## Naming conventions

- Decision memos: `DECISION_[Topic]_[YYYY-MM-DD].md` (e.g. `DECISION_ModelingApproach_2026-05-15.md`).
- Trade-off analyses: `TRADEOFF_[OptionA-vs-OptionB]_[YYYY-MM-DD].md`.
- Meeting notes that produced a decision: `NOTES_[MeetingType]_[YYYY-MM-DD].md`.
- Sign-off artifacts: `SIGNOFF_[Decision]_[YYYY-MM-DD].pdf`.
- Use kebab-case in the `[Topic]` slug; spell out the topic, do not abbreviate.

## What goes here

- Decision memos with context, options, choice, and rationale.
- Side-by-side trade-off analyses comparing two or more options.
- Meeting notes whose primary output is a decision or commitment.
- Approval records, sign-offs, and stakeholder confirmations.
- Records of reversed or superseded decisions (kept for the audit trail).

## What does NOT go here

- Technical specifications describing *how* something is built (use `docs/specs/`).
- Project plans, schedules, or milestones (use `docs/plans/`).
- General meeting notes with no decision attached (keep locally or in `docs/`).
- Drafts of decisions that have not yet been made — keep in scratch until finalized.
- Anything that would need to be edited regularly; decision records should be immutable.
