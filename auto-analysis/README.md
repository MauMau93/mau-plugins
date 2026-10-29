# auto-analysis plugin

Hypothesis-driven marketing analytics, packaged so it works in any project folder — in Claude Code and Cowork.

## Agents
| Agent | Role |
|---|---|
| `csv-data-explorer` | EDA on a CSV → `eda_report.md` + `eda_script.py` |
| `model-advisor` | Testable hypotheses + modeling strategy (no implementation) |
| `model-builder` | Implements models, tests hypotheses, moves them to validated/refuted |
| `model-explainer` | Executive / business / technical reports |

## Skills
| Skill | Say… |
|---|---|
| `start-analysis` | "start an analysis project here" — sets up folders, framework docs, CLAUDE.md |
| `run-eda` | "run EDA on transactions" |
| `advise-model` | "what hypotheses should we test?" |
| `build-model` | "build the model / test H-003" |
| `explain-model` | "write the executive summary" |

## Typical flow
1. New folder → `start-analysis`
2. Fill `context/business_context.md`, drop CSVs into `data/<DATASET>/`
3. `run-eda` → `advise-model` → `build-model` → `explain-model`, then iterate 2–4.

Framework docs are copied into each project at `.auto-analysis/framework/`; run `start-analysis` again in an existing project to refresh them.
