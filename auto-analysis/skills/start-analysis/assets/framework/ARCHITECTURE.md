# Architecture Documentation

## Markdown Building Blocks

The framework uses four types of Markdown documents as its core data structures:

| Block | Purpose | Typical Contents |
|-------|---------|------------------|
| **Context Markdown** | Supply background info | Business details, task brief, DB schema, historical performance |
| **Dataset Markdown** | Describe a table/CSV | Column definitions, stats, sample EDA results, **initial hypotheses** |
| **Experiment Markdown** | Log a modeling run | Model config, metrics, charts, observations, next steps |
| **Hypothesis Markdown** | Track analytical assumptions | Testable statements, validation methods, results, business implications. *Note: See `.auto-analysis/framework/HYPOTHESIS_DEFINITION.md` for our framework's definition of "hypothesis"* |

## Dataset-EDA Coupling Pattern

Every dataset is bundled with an auto-generated EDA Markdown file:

1. **Auto-generation**: A reusable Python script produces the EDA file
2. **Standard contents**:
   - Column descriptions & data types
   - Descriptive statistics (mean, std, uniques, missingness)
   - Basic visual summaries (e.g., histograms) or links to plots
   - Notable data-quality issues
3. **Purpose**: The EDA Markdown travels with the raw CSV/table so the LLM can reason about the data without loading the full file

## Human-in-the-Loop Interaction Patterns

Two checkpoint styles (configured per project):

1. **Full-stage validation**
   - Brief confirmation after every major stage
   - Stages: Context → Dataset → Features → Model → Eval
   
2. **Milestone validation**
   - Confirmation only after model-evaluation milestones
   - More autonomous execution between checkpoints

At each checkpoint:
- LLM presents a concise summary
- May ask: "Should I proceed with A, B, or C?"
- Can query for missing contextual info (e.g., business rules)

## Hypothesis-Driven Analysis Pattern

> **Definition Reference**: Our framework uses a broad definition of "hypothesis" - see `.auto-analysis/framework/HYPOTHESIS_DEFINITION.md` for details.

Every analysis follows a hypothesis-driven approach:

1. **Formulate**: Generate testable hypotheses from context and data (including assumptions, validation checks, and exploratory ideas)
2. **Document**: Record hypotheses before testing (prevents HARKing)
3. **Test**: Execute specific analyses to validate/refute
4. **Update**: Document results regardless of outcome
5. **Iterate**: Use results to generate follow-up hypotheses

This pattern ensures:
- Scientific rigor in decision-making
- Clear audit trail for stakeholders
- Learning from both successes and failures
- Business-relevant insights

## Canonical Workflow

The framework implements a 7-step iterative loop:

1. Select data & **formulate initial hypotheses**
2. Run basic EDA on selected data **& generate data hypotheses**
3. Engineer features **based on hypothesis insights**
4. Choose & train model **to test model hypotheses**
5. Evaluate model (metrics, charts) **& validate hypotheses**
6. Inspect results → refine **& create follow-up hypotheses**
7. Repeat steps 2-6 until satisfactory

All artifacts from each step are stored as Markdown files for traceability and reproducibility.