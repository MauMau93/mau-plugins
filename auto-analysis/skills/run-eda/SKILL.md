---
name: run-eda
description: >
  Run exploratory data analysis (EDA) on a CSV in an autoAnalysis project — profiling, column stats, missingness, data quality, structure — producing eda_report.md + eda_script.py next to the data. Use for "run EDA", "explore/profile this CSV", "what is in this dataset", "data quality check", or any .csv under data/<DATASET>/.
---

# run-eda → csv-data-explorer agent

## 1. Locate the project
Find PROJECT_ROOT: the current folder or nearest parent containing `.auto-analysis/`
(legacy: `runs/PROJECT_NAME/` in the autoAnalysis repo). If none exists, offer to run
`start-analysis` first and stop.

## 2. Identify the dataset
- The CSV must be in `<PROJECT_ROOT>/data/<DATASET_NAME>/`. If the user points to a CSV elsewhere,
  offer to move/copy it there first.
- If several datasets exist and the user did not say which, ask once. Do not guess.
- Skip delegation for narrow one-off questions (a single pandas one-liner, one column count) — just answer.

## 3. Delegate
- **Preferred:** hand the task to the `csv-data-explorer` subagent from this plugin (it may appear as
  `auto-analysis:csv-data-explorer`). Pass PROJECT_ROOT as an absolute path plus everything gathered in step 2,
  and the checkpoint mode from `.auto-analysis/config.md`.
- **If subagents are not available in this environment** (some Cowork sessions): read
  `../../agents/csv-data-explorer.md` relative to this skill's base directory and follow those instructions
  yourself, exactly as written.

## 4. Report back
Summarise in a few lines what was produced and where, then present the next step as options A/B/C
(per the checkpoint mode) and wait for the user.
