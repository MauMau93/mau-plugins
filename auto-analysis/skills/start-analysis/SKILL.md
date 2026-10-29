---
name: start-analysis
description: >
  Set up a new folder as an autoAnalysis marketing-analytics project (EDA → hypotheses → models →
  stakeholder docs). Creates the standard folder structure, copies the framework docs and
  templates, and writes a project CLAUDE.md. Use when the user says "start an analysis project",
  "set up autoAnalysis here", "new analysis project", "bring the analysis framework to this folder",
  "initialize this project for EDA / LTV / MMM", or opens a new project folder and wants the
  csv-data-explorer / model-advisor / model-builder / model-explainer workflow available.
---

# Start an autoAnalysis project

Turns the current (or a user-chosen) folder into a project the four auto-analysis agents can work in.
The base directory of this skill is shown when it loads; `assets/` below is relative to it.

## 1. Pick the project root
- Default: the current working directory (in Cowork: the folder the user connected).
- If the folder already has `.auto-analysis/`, say it is already set up and offer to refresh the
  framework docs only (step 3) — never overwrite `context/`, `data/`, `hypotheses/` or `src/`.
- If the folder is the original autoAnalysis repo, create the project under `runs/<PROJECT_NAME>/`.

## 2. Ask (one AskUserQuestion call, skip what the user already said)
- Project name (UPPERCASE_WITH_UNDERSCORES, e.g. `ACME_MMM`)
- Task type: EDA only / LTV / MMM / Funnel / Attribution / Other
- Checkpoint mode: **Full-stage** (approve after every stage) or **Milestone** (approve after model evaluation)

## 3. Create the structure
```
<PROJECT_ROOT>/
├── .auto-analysis/
│   ├── config.md          # project name, task type, checkpoint mode, created date
│   └── framework/         # copy of assets/framework/ (docs, templates, instruction files)
├── context/business_context.md
├── data/                  # one subfolder per dataset: data/<DATASET_NAME>/<file>.csv
├── hypotheses/{active,validated,refuted}/ + hypothesis_log.md
├── src/
├── documentation/
└── visualizations/
```
- Copy `assets/framework/` recursively into `.auto-analysis/framework/` (use `cp -R`).
- Create `hypotheses/hypothesis_log.md` from `.auto-analysis/framework/templates/hypothesis_log_template.md`.
- Create `context/business_context.md` with headings: Business, Objective of this analysis,
  Key KPIs, Data sources, Constraints & known issues, Stakeholders, Timeline. Leave `TODO` under each.
- Write `.auto-analysis/config.md` with the answers from step 2.
- Add `*.csv` and `.venv/` to `.gitignore` if the folder is a git repo (client data stays local).

## 4. Write CLAUDE.md
If `CLAUDE.md` exists at the project root, append a section; otherwise create it with:

```markdown
# <PROJECT_NAME> — autoAnalysis project

Marketing-analytics project using the auto-analysis plugin. Task: <task type>. Checkpoints: <mode>.
Framework docs: `.auto-analysis/framework/` (read FOLDER_STRUCTURE.md and HYPOTHESIS_DEFINITION.md first).

## Workflow (hypothesis-driven, everything in Markdown)
1. `run-eda` → csv-data-explorer writes `data/<DATASET>/eda_report.md` + `eda_script.py`
2. `advise-model` → model-advisor writes hypotheses in `hypotheses/active/` + `documentation/hypothesis_strategy.md`
3. `build-model` → model-builder implements and tests hypotheses in `src/`, moves them to validated/refuted
4. `explain-model` → model-explainer writes executive/business/technical reports in `documentation/`
Repeat 2–4. At every checkpoint present options A/B/C and wait for the user.

## Rules
- Business context lives in `context/` — ask the user when it is missing, never invent it.
- Record hypotheses before testing them (no HARKing); log every result in `hypotheses/hypothesis_log.md`.
- Each dataset folder keeps its CSV, EDA report, script and plots together.
```

## 5. Finish
Show the created tree (`find . -maxdepth 2 -not -path './.git*'`) and tell the user the next steps:
1. Fill in `context/business_context.md` (or paste the context and you'll write it).
2. Drop each CSV in `data/<DATASET_NAME>/`.
3. Say "run EDA on <DATASET_NAME>".
