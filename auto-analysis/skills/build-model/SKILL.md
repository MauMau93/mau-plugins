---
name: build-model
description: >
  Implement and validate models that test the active hypotheses of an autoAnalysis project (LTV, MMM, funnel, attribution, forecasting), writing code and technical results to src/ and moving hypotheses to validated/refuted. Use for "build the model", "test the hypotheses", "implement H-003", "run the next modeling iteration".
---

# build-model → model-builder agent

## 1. Locate the project
Find PROJECT_ROOT: the current folder or nearest parent containing `.auto-analysis/`
(legacy: `runs/PROJECT_NAME/` in the autoAnalysis repo). If none exists, offer to run
`start-analysis` first and stop.

## 2. Check inputs
- `hypotheses/active/` must contain hypotheses; if empty, suggest `advise-model` first.
- If the user named specific hypotheses (e.g. H-003), pass only those; otherwise pass the priority order from `hypotheses/hypothesis_log.md`.
- Check for a Python env (`.venv/` or `requirements.txt`); mention it to the agent.

## 3. Delegate
- **Preferred:** hand the task to the `model-builder` subagent from this plugin (it may appear as
  `auto-analysis:model-builder`). Pass PROJECT_ROOT as an absolute path plus everything gathered in step 2,
  and the checkpoint mode from `.auto-analysis/config.md`.
- **If subagents are not available in this environment** (some Cowork sessions): read
  `../../agents/model-builder.md` relative to this skill's base directory and follow those instructions
  yourself, exactly as written.

## 4. Report back
Summarise in a few lines what was produced and where, then present the next step as options A/B/C
(per the checkpoint mode) and wait for the user.
