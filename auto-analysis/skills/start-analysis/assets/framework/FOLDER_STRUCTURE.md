# Folder Structure Guide

> **Plugin note:** examples below show the original multi-project layout `runs/PROJECT_NAME/`. When this framework is set up with the `start-analysis` skill, the project folder itself is the project root (`<PROJECT_ROOT>/`), so read `runs/PROJECT_NAME/` as `<PROJECT_ROOT>/`.

## Overview

This document defines the standard folder structure for all projects and experiments in the LLM Marketing Analytics Framework. Every project should follow this structure to ensure consistency and enable all agents to work effectively.

## Standard Project Structure

```
runs/
└── PROJECT_NAME/              # Use UPPERCASE_WITH_UNDERSCORES
    ├── data/                  
    ├── context/               
    ├── documentation/         
    ├── src/                   
    └── visualizations/        
```

## Folder Descriptions

### `/<PROJECT_ROOT>/`
The root folder for each project. Use descriptive names in UPPERCASE with underscores.
- Examples: `ACME_LTV`, `NEW_PARTNER`, `Q4_MMM_ANALYSIS`

### `/<PROJECT_ROOT>/data/`
Contains all datasets used in the project. Each dataset gets its own subfolder.

```
data/
└── DATASET_NAME/          # e.g., customers, transactions, campaigns
    ├── dataset.csv        # The actual data file (can be any name)
    ├── eda_report.md      # Exploratory Data Analysis report
    ├── eda_script.py      # Generated EDA Python script
    ├── data_profile.html  # Optional: pandas profiling report
    └── *.png/jpg          # Any visualizations from the EDA
```

**Important for Agents:**
- CSV Explorer Agent: Always save EDA outputs in `data/DATASET_NAME/`
- Model Builder Agent: Read data from `data/DATASET_NAME/dataset.csv`
- All dataset-specific analysis stays within its folder

### `/<PROJECT_ROOT>/context/`
Business context and requirements for the project.

```
context/
├── business_context.md    # Business background and goals
├── task_requirements.md   # Specific task requirements
├── constraints.md         # Any limitations or constraints
├── kpis.md               # Key performance indicators
└── *.md                  # Any other context documents
```

**Files typically include:**
- Business objectives
- Data sources and definitions
- Success criteria
- Stakeholder requirements
- Timeline and milestones

### `/<PROJECT_ROOT>/documentation/`
Project-specific documentation created during analysis.

```
documentation/
├── data_dictionary.md     # Definitions of all fields
├── methodology.md         # Approach and methods used
├── decisions_log.md       # Key decisions and rationale
├── findings.md           # Key insights and discoveries
└── final_report.md       # Executive summary
```

### `/<PROJECT_ROOT>/src/`
All source code and scripts for the project.

```
src/
├── data_preprocessing.py  # Data cleaning and preparation
├── feature_engineering.py # Feature creation scripts
├── model_training.py      # Model training code
├── evaluation.py          # Model evaluation scripts
├── utils.py              # Helper functions
├── main.ipynb            # Main analysis notebook
└── *.py / *.ipynb        # Any other code files
```

**Important for Agents:**
- Model Builder Agent: Save all model code here
- Keep files flat - no subdirectories needed
- Use descriptive filenames

### `/<PROJECT_ROOT>/visualizations/`
All visualizations for user communication and reporting.

```
visualizations/
├── model_performance.png  # Model metrics charts
├── feature_importance.png # Feature importance plots
├── predictions_vs_actual.png
├── dashboard.html        # Interactive dashboards
└── *.png/jpg/html        # All other visualizations
```

**Important:**
- This folder is for **final visualizations** shown to users
- Dataset-specific exploratory plots stay in `data/DATASET_NAME/`
- Use descriptive filenames for easy reference

## Example: ACME_LTV Project

```
runs/
└── ACME_LTV/
    ├── data/
    │   ├── customers/
    │   │   ├── acme_customers.csv
    │   │   ├── eda_report.md
    │   │   ├── eda_customers.py
    │   │   └── distribution_plots.png
    │   └── transactions/
    │       ├── transactions.csv
    │       ├── eda_report.md
    │       └── monthly_trends.png
    ├── context/
    │   ├── business_context.md
    │   ├── ltv_requirements.md
    │   └── acme_background.md
    ├── hypotheses/
    │   ├── hypothesis_log.md
    │   ├── validated/
    │   │   └── H-001_gompertz_curves.md
    │   └── refuted/
    │       └── H-002_linear_growth.md
    ├── documentation/
    │   ├── executive/
    │   │   └── executive_summary.md
    │   ├── business/
    │   │   ├── business_report.md
    │   │   └── implementation_guide.md
    │   ├── technical/
    │   │   ├── technical_specifications.md
    │   │   └── methodology_details.md
    │   └── methods/
    │       └── ltv_model_explanation.md
    ├── src/
    │   ├── models/
    │   │   └── ltv_model.py
    │   ├── validation/
    │   │   └── model_validation.py
    │   ├── tests/
    │   │   └── hypothesis_tests.py
    │   ├── results/
    │   │   └── validation_metrics.json
    │   └── model_implementation_log.md
    └── visualizations/
        ├── explained/
        │   ├── ltv_curves_annotated.png
        │   └── business_impact_chart.png
        ├── technical/
        │   ├── model_diagnostics.png
        │   └── residual_analysis.png
        └── business_metrics/
            └── cohort_retention_dashboard.html
```

## Guidelines for Agents

### For CSV Explorer Agent (`@agent-csv-data-explorer`)
1. Always work within `<PROJECT_ROOT>/data/DATASET_NAME/`
2. Save EDA report as `eda_report.md`
3. Save EDA script as `eda_script.py` or `eda_[dataset].py`
4. Save all exploratory visualizations in the same folder
5. Create data quality assessments and statistical summaries

### For Model Builder Agent (`@agent-model-builder`)
1. Read data from `<PROJECT_ROOT>/data/DATASET_NAME/`
2. Save all model code in `<PROJECT_ROOT>/src/`
3. Save model outputs and predictions in `<PROJECT_ROOT>/src/`
4. Save final model visualizations in `<PROJECT_ROOT>/visualizations/`
5. Document model decisions in `<PROJECT_ROOT>/documentation/`

### For All Agents
1. **Never create nested subdirectories** unless absolutely necessary
2. **Keep folder structure flat and simple**
3. **Always check if folders exist** before creating files
4. **Use descriptive filenames** that indicate content
5. **Follow the naming convention**: UPPERCASE for project names, lowercase for files

## Creating a New Project

When starting a new project, create this structure:

```bash
runs/NEW_PROJECT/
├── data/
├── context/
├── documentation/
├── src/
└── visualizations/
```

Then add datasets as needed:
```bash
runs/NEW_PROJECT/data/DATASET_NAME/
```

## File Naming Conventions

- **Project folders**: `UPPERCASE_WITH_UNDERSCORES`
- **Dataset folders**: `lowercase_with_underscores`
- **Python files**: `lowercase_with_underscores.py`
- **Markdown files**: `lowercase_with_underscores.md`
- **Visualizations**: `descriptive_name.png/jpg/html`

## Common Patterns

### Multiple Datasets
When working with multiple datasets:
```
data/
├── customers/
│   └── [eda files]
├── transactions/
│   └── [eda files]
└── products/
    └── [eda files]
```

### Time-Series Experiments
For experiments over time, use timestamps in filenames:
```
src/
├── model_v1_2024_01_15.py
├── model_v2_2024_01_20.py
└── final_model.py
```

### Model Iterations
Track model versions in src/:
```
src/
├── baseline_model.py
├── improved_model_v1.py
├── improved_model_v2.py
└── final_model.py
```

## Important Notes

1. **Simplicity is key** - Don't create complex nested structures
2. **Consistency matters** - All projects should follow this structure
3. **Documentation is critical** - Always update markdown files
4. **Agents must be aware** - All agents should know where to read/write files
5. **User communication** - Use visualizations/ for final outputs shown to users

This structure ensures that all agents can work together effectively and users can easily navigate and understand project outputs.