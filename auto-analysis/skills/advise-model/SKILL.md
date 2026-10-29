---
name: advise-model
description: >
  Generate or refine testable modeling hypotheses and strategy (model family choice, features, validation/CV design, experiment plan) from EDA reports, business context and previous results in an autoAnalysis project. Use for "what hypotheses should I test", "how should I model this", "plan the LTV/MMM approach", "refine hypotheses after these results". Strategy only — not implementation.
---

# advise-model → model-advisor agent

## 1. Locate the project
Find PROJECT_ROOT: the current folder or nearest parent containing `.auto-analysis/`
(legacy: `runs/PROJECT_NAME/` in the autoAnalysis repo). If none exists, offer to run
`start-analysis` first and stop.

## 2. Check inputs
- At least one `data/*/eda_report.md` should exist; if not, suggest `run-eda` first.
- Read `context/business_context.md`; if it is mostly TODO, ask the user for the objective and key KPI before delegating.
- Note whether this is an initial cycle or a refinement (existing files in `hypotheses/validated|refuted/`).

## 3. Delegate
- **Preferred:** hand the task to the `model-advisor` subagent from this plugin (it may appear as
  `auto-analysis:model-advisor`). Pass PROJECT_ROOT as an absolute path plus everything gathered in step 2,
  and the checkpoint mode from `.auto-analysis/config.md`.
- **If subagents are not available in this environment** (some Cowork sessions): read
  `../../agents/model-advisor.md` relative to this skill's base directory and follow those instructions
  yourself, exactly as written.

## 4. Report back
Summarise in a few lines what was produced and where, then present the next step as options A/B/C
(per the checkpoint mode) and wait for the user.
