# Corporate-Finance — BUS 629 Sectra AB Ratios Project

> A portfolio-grade financial analysis of **Sectra AB (publ)** — a Swedish medical-imaging IT and cybersecurity company listed on Nasdaq Stockholm — produced for the BUS 629 (VEMBA International Corporate Finance) capstone at Shidler College of Business, University of Hawaiʻi at Mānoa, under Professor Adam W. Stauffer. The work spans five staged deliverables: company selection memo, populated three-statement and ratios workbook, technical specification for LLM analysis, raw LLM execution against that spec, and an evaluated final analysis with manual verification and spec retrospective.

## What you'll find here

This repository is the auditable trail of one analyst's five-stage corporate-finance ratios project. If you are a manager, reviewer, or future employer arriving via my LinkedIn profile: start with [`deliverables/`](./deliverables) for the polished outputs (final analysis, spec retrospective, raw LLM output, prompt log). The [`docs/decisions/`](./docs/decisions) folder holds the original Stage 2 company-selection memo and its revised version after instructor PR feedback. [`docs/specs/`](./docs/specs) contains the Stage 4 technical specification that drove the Stage 5 LLM execution. [`models/`](./models) holds the Excel ratios template and the populated Sectra workbook. [`analysis/validation/`](./analysis/validation) contains the manual verification table that caught the LLM's hallucinations. [`data/`](./data) records source-document provenance.

For a project overview written for someone unfamiliar with the BUS 629 course: this repository documents how I selected a company, built a financial model, specified the analytical work for an LLM, executed the spec, and then evaluated and corrected the LLM's output — all with the audit trail an employer or reviewer would expect from real finance work.

## Project status

| Stage | Deliverable | Status | Score | Latest artifact |
| --- | --- | --- | --- | --- |
| Stage 0 | Repository + Resume + Bio | Complete | n/a | [`RESUME.md`](./RESUME.md), [`BIO.md`](./BIO.md) |
| Stage 1 | Ratios template populated structure | Complete | n/a | [`models/templates/performance-ratios-template.xlsx`](./models/templates/) |
| Stage 2 | Company selection memo | Complete | **97.11%** (4.37 / 4.5) | Original: [`2026-05-17-cam-sectra-selection.md`](./docs/decisions/2026-05-17-cam-sectra-selection.md) · Revised: [`2026-05-31-cam-sectra-selection-revised.md`](./docs/decisions/2026-05-31-cam-sectra-selection-revised.md) |
| Stage 3 | Populated financial workbook | Complete | **99%** (8.91 / 9) | [`models/builds/2026-05-17-cam-sectra-financials.xlsx`](./models/builds/) |
| Stage 4 | LLM technical specification | Complete | tba | [`docs/specs/2026-05-30-cam-sectra-spec.md`](./docs/specs/) |
| Stage 5 | LLM analysis, evaluation, repo polish | Complete | tba | [`deliverables/2026-05-31-cam-sectra-final-analysis.md`](./deliverables/) |

Commit hashes for each stage's primary commit can be found via the repo's [commit history](./commits/main). The "Latest artifact" column links directly to the canonical file for each stage.

## Repository structure

```
Corporate-Finance/
├── README.md                  # This file — project overview
├── RESUME.md                  # Resume (Stage 0)
├── BIO.md                     # Longer-form biography (Stage 0)
├── LICENSE                    # MIT
├── .gitignore                 # Excludes .DS_Store, ~$*.xlsx, *.tmp, etc.
│
├── docs/                      # Written deliverables
│   ├── decisions/             # Stage 2 selection memos + feedback responses
│   └── specs/                 # Stage 4 LLM specification
│
├── models/                    # Excel workbooks
│   ├── templates/             # Stage 1 ratios template (unmodified)
│   └── builds/                # Stage 3 populated Sectra workbook
│
├── data/                      # Source financial data + provenance
│
├── analysis/                  # Validation and review work
│   └── validation/            # Stage 5 manual ratio verification table
│
└── deliverables/              # Stage 5 final outputs
    ├── prompt-log.md          # AI session log across all stages
    ├── *-llm-raw.md           # Unedited LLM output from spec execution
    ├── *-final-analysis.md    # Evaluated, corrected analysis with executive voice
    └── *-spec-retrospective.md # Template-backed self-evaluation of Stage 4 spec
```

Each subdirectory has its own `README.md` explaining what belongs inside.

## Company subject

**Sectra AB (publ)** — Linköping, Sweden. Founded 1978. Ticker SECT B (Nasdaq Stockholm Large Cap). Three operating segments: Imaging IT Solutions (PACS, RIS, AI-enabled medical imaging; ranked #1 in PACS customer satisfaction by KLAS for 13 consecutive years in the U.S.), Secure Communications (encrypted defense and government systems), and Business Innovation (orthopedic and oncology). FY2024/2025 (year ending April 30, 2025): SEK 3,239.8M net sales (+9.3% YoY), underlying operating margin 18.92%, ROE 35.89%, CFO/Net Income 1.64×. IFRS reporter with by-nature income-statement presentation; majority of revenue earned in non-SEK currencies.

The selection rationale is detailed in the [Stage 2 memo](./docs/decisions/2026-05-31-cam-sectra-selection-revised.md). Briefly: I work as Vice President of the Ho Chi Minh City Medical Equipment Association with 23 years in Vietnam's medical-equipment sector, and Sectra's PACS-to-SaaS transition is directly relevant to PACS distribution decisions in the Vietnamese market — making this both a rigorous BUS 629 case study and applied market intelligence.

## About me

Hien Cam — VEMBA student, Shidler College of Business; VP of the Ho Chi Minh City Medical Equipment Association. See [`RESUME.md`](./RESUME.md) for full background and [`BIO.md`](./BIO.md) for a longer-form biography.

## License and reuse

This repository is released under the [MIT License](./LICENSE). The analytical work product is a portfolio artifact and may be referenced. Source documents from Sectra AB are publicly available from Sectra's investor relations site and remain copyright of their respective owners.

## Course context

- **Course:** BUS 629 — VEMBA International Corporate Finance
- **Institution:** Shidler College of Business, University of Hawaiʻi at Mānoa
- **Instructor:** Professor Adam W. Stauffer
- **Course materials and brief:** [adamwstauffer/shidler — courses/BUS-629-VEMBA-International-Corporate-Finance](https://github.com/adamwstauffer/shidler/tree/main/courses/BUS-629-VEMBA-International-Corporate-Finance)
