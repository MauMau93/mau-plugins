---
name: explain-model
description: >
  Turn model results and validated/refuted hypotheses of an autoAnalysis project into stakeholder communication — executive summary, business report, technical documentation, explained visuals. Use for "explain the results", "write the executive summary", "prepare the client report", "document the model for stakeholders".
---

# explain-model → model-explainer agent

## 1. Locate the project
Find PROJECT_ROOT: the current folder or nearest parent containing `.auto-analysis/`
(legacy: `runs/PROJECT_NAME/` in the autoAnalysis repo). If none exists, offer to run
`start-analysis` first and stop.

## 2. Check inputs
- Results must exist in `src/` (e.g. `src/model_implementation_log.md`); if not, suggest `build-model` first.
- Ask which audience matters most if the user did not say (executive / business / technical / all).

## 3. Delegate
- **Preferred:** hand the task to the `model-explainer` subagent from this plugin (it may appear as
  `auto-analysis:model-explainer`). Pass PROJECT_ROOT as an absolute path plus everything gathered in step 2,
  and the checkpoint mode from `.auto-analysis/config.md`.
- **If subagents are not available in this environment** (some Cowork sessions): read
  `../../agents/model-explainer.md` relative to this skill's base directory and follow those instructions
  yourself, exactly as written.

## 4. Report back
Summarise in a few lines what was produced and where, then present the next step as options A/B/C
(per the checkpoint mode) and wait for the user.
