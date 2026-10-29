# Workflow Guide - Marketing Analytics Automation

This document describes the complete workflow for executing marketing analytics tasks. It serves as both framework documentation and execution instructions for the LLM.

---

## 1. Initialization & Context Understanding

**Input**: Context Markdown files

**Actions**:
1. Parse business context, objectives, and constraints
2. Identify available data sources and schemas
3. Understand success metrics and deliverables
4. Document any ambiguities or missing information

Context files to provide:
- **Business Context**: Company background, goals, KPIs
- **Task Description**: Specific analysis requested
- **Database Schema**: Table structures and relationships
- **Historical Context**: Previous analyses, known issues, business rules

**Output**: Summary of understanding with any clarification questions

---

## 2. Dataset Registration & EDA

Datasets can be processed in parallel, each following this flow:

**Input**: Raw dataset(s) in `data/raw/` (CSV or table export)

**Actions**:
1. Load and inspect the data structure
2. Generate descriptive statistics
3. Identify data quality issues (missing values, outliers, inconsistencies)
4. Create initial visualizations
5. Document key patterns and insights
6. Clean: Handle missing values, outliers, data type corrections
7. Explore: Deeper analysis, distributions, correlations

**Output**: `eda.md` file with comprehensive analysis (in `markdown/datasets/<dataset_name>/`)

**Checkpoint**: Present EDA findings and get approval to proceed

---

## 3. Feature Engineering

**Input**: Cleaned data + business context

**Actions**:
1. Create time-based features (if applicable)
2. Generate aggregations and ratios
3. Encode categorical variables
4. Handle missing values appropriately
5. Document feature rationale and transformations

**Output**: `features.md` with feature descriptions and code

**Optional Checkpoint**: Review features with human if complex

---

## 4. Hypothesis Generation & Tracking

Throughout the analysis, maintain rigorous hypothesis tracking.

> **Definition**: Our framework uses a broad definition of "hypothesis" encompassing structured assumptions, exploratory points, and validation checks. See `.auto-analysis/framework/HYPOTHESIS_DEFINITION.md` for details.

### Hypothesis Generation Points

1. **After Context Review**: Business assumptions and success metrics
2. **During EDA**: Data quality, patterns, and relationships
3. **Before Modeling**: Model selection and performance expectations
4. **After Evaluation**: Result interpretation and generalization

### Hypothesis Documentation

- Store in `<PROJECT_ROOT>/hypotheses/` folder
- Use standardized template from `HYPOTHESIS_TRACKING.md`
- Track status: Proposed → Testing → Confirmed / Refuted / Partial
- Link to supporting evidence and experiments

---

## 5. Model Development

**Input**: Feature set + task requirements + hypotheses

**Actions**:
1. Split data for training/validation/test
2. Select appropriate algorithm(s) based on task:
   - **EDA**: Statistical tests, clustering
   - **LTV**: Regression models, survival analysis
   - **MMM**: Time series models, causal inference
   - **Funnel**: Conversion rate analysis, path analysis
3. Train initial model(s)
4. Perform hyperparameter tuning

| LLM Action | Markdown Artifact | Checkpoint? |
|------------|-------------------|-------------|
| Select & Hypothesize | Updates Context Markdown, Creates Hypothesis Markdown | Yes |
| Feature Selection | Creates/updates Feature Markdown | Optional |
| Hypothesis Validation | Updates Hypothesis Markdown with results | Yes |
| Model Training | Creates Experiment Markdown | Optional |

**Output**: `experiment_YYYY-MM-DD.md` with model details

**Optional Checkpoint**: Confirm model approach if uncertain

---

## 6. Evaluation & Insights

**Input**: Trained model(s)

**Actions**:
1. Calculate relevant metrics:
   - **LTV**: MAE, RMSE, calibration plots
   - **MMM**: Attribution percentages, ROI by channel
   - **Funnel**: Conversion rates, drop-off analysis
2. Generate visualizations
3. Interpret results in business context
4. Identify limitations and caveats
5. Validate model hypotheses

**Output**: Updated experiment file with evaluation results, updated Hypothesis Markdown

**Checkpoint**: Present results and hypothesis validation outcomes, get feedback

---

## 7. Iteration Decision

**Input**: Evaluation results + human feedback

**Options**:
1. **Option A**: Accept results and finalize
2. **Option B**: Refine features and retrain
3. **Option C**: Try different modeling approach
4. **Option D**: Collect additional data/context

**Action**: Based on human selection, either iterate (go to relevant step) or proceed to completion

### Iteration Criteria

Continue the modeling loop until:
- Model performance meets requirements
- Business objectives are satisfied
- Human decides to conclude analysis

Each iteration creates new or updated markdown artifacts for full traceability.

---

## 8. Final Deliverables

**Input**: All artifacts from previous steps

**Actions**:
1. Create comprehensive final report
2. Link all relevant markdown files
3. Summarize key findings and recommendations
4. Document reproducibility instructions

**Output**:
- **Contextual Summary**: High-level findings and recommendations
- **Final Report Markdown** (`final_report.md`): Links all artifacts, summarizes methodology and results, provides actionable insights
- **Archive**: All markdown files preserved for reproducibility

---

## Appendix A: Checkpoint Guidelines

At each checkpoint (marked with "Checkpoint" above):
1. Summarize what was done
2. Present key findings or results
3. Show hypothesis validation results (confirmed/refuted/partial)
4. Offer 2-3 clear next step options
5. Wait for human approval before proceeding

---

## Appendix B: File Naming Conventions

| File Type | Naming Pattern |
|-----------|----------------|
| Context | `context.md` |
| EDA | `{dataset_name}_eda.md` |
| Features | `features.md` |
| Experiments | `experiment_YYYY-MM-DD_HH-MM.md` |
| Final Report | `final_report.md` |

All files should be saved in the project root (`<PROJECT_ROOT>/`) for the current execution.

---

## Appendix C: Validation Modes

The framework supports two human-in-the-loop patterns:

- **Full-stage validation**: Checkpoints after each major step
- **Milestone validation**: Checkpoints only after model evaluation

Choose based on project complexity and trust level.
