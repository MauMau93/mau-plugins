# Hypothesis Tracking Framework

> **Definition Reference**: For our official definition of "hypothesis" in this framework, see [`.auto-analysis/framework/HYPOTHESIS_DEFINITION.md`](HYPOTHESIS_DEFINITION.md)

## Overview

This document defines the hypothesis tracking system for the LLM Automation Framework. Hypothesis tracking ensures scientific rigor, creates an audit trail for analytical decisions, and facilitates communication between agents, analysts, and stakeholders.

**Note**: In this framework, "hypothesis" has a broader meaning than the strict scientific definition - it encompasses structured assumptions, exploratory points, validation checks, and testable ideas that guide our analysis.

## Core Principles

1. **Hypothesis-Driven Analysis**: Every modeling decision should stem from a testable hypothesis
2. **Documentation First**: State hypotheses before testing, not after
3. **Transparent Validation**: Clear success criteria and honest result reporting
4. **Business Context**: Connect technical hypotheses to business implications
5. **Iterative Refinement**: Failed hypotheses inform new ones

## Hypothesis Categories

> **Reference**: These categories align with our official definition in `.auto-analysis/framework/HYPOTHESIS_DEFINITION.md`

### 1. Data Pattern Hypotheses
- Distribution assumptions (e.g., "Customer LTV follows Gompertz curve")
- Temporal patterns (e.g., "Seasonality affects customer behavior") 
- Feature relationships (e.g., "Geographic proximity affects purchase probability")
- Segment differences (e.g., "Premium customers have different retention curves")

### 2. Model Performance Hypotheses
- Accuracy expectations (e.g., "Model will achieve <5% MAPE on holdout")
- Feature importance (e.g., "Acquisition channel will be top predictor")
- Generalization (e.g., "Model parameters stable across cohorts")
- Validation performance (e.g., "Time-based split will show consistent performance")

### 3. Business Logic Hypotheses
- Causal relationships (e.g., "Marketing spend drives incremental acquisition")
- Parameter interpretations (e.g., "Model parameter 'a' correlates with channel quality")
- Segment behavior (e.g., "Mobile-first customers have faster early revenue curves")
- External factors (e.g., "Economic conditions affect parameter stability")

### 4. Integrity/Exclusion Hypotheses
- Data quality checks (e.g., "Data from cohorts before 2018 is unreliable")
- Completeness assumptions (e.g., "Missing data is random, not systematic")
- Consistency expectations (e.g., "Customer IDs are unique across systems")

### 5. Feature/Data Strategy Hypotheses
- Enhancement opportunities (e.g., "Adding interaction terms will improve performance")
- Data source value (e.g., "External weather data will improve seasonal predictions")
- Engineering decisions (e.g., "Custom features outperform raw features")

### 6. Result-Based Hypotheses (For Iterations)
- Refinement opportunities (e.g., "Adding interaction terms will improve partial hypothesis H-003")
- Alternative approaches (e.g., "Non-linear transformations will address H-001 failure")
- Deeper investigations (e.g., "Segment-specific modeling will resolve conflicting results")

## Standard Hypothesis Template

```markdown
## H-[ID]: [Short Descriptive Title]

**Date**: YYYY-MM-DD
**Author**: [Agent name or analyst]
**Category**: [Data Quality | Business Logic | Model Assumption | Parameter Relationship]
**Priority**: [High | Medium | Low]
**Status**: [🔄 Testing | ✅ Confirmed | ❌ Refuted | ⚠️ Partial | 🔍 Proposed]

### Hypothesis Statement
[Clear, specific, testable statement. Should be falsifiable.]

### Rationale
[Why we believe this might be true. Include prior evidence or domain knowledge.]

### Test Design
- **Required Data**: [Specific datasets and features needed]
- **Method**: [Statistical test, model comparison, or analysis approach]
- **Success Criteria**: [Specific thresholds or conditions for confirmation]
- **Failure Criteria**: [What would definitively refute this hypothesis]

### Results
- **Test Execution Date**: [When test was performed]
- **Evidence**: [Key metrics, statistics, visualizations]
- **Outcome**: [Clear statement of confirmation/refutation]
- **Confidence Level**: [Statistical significance or confidence measure]
- **Caveats**: [Limitations or assumptions in the test]

### Business Implications
- **If Confirmed**: [What this means for the business/model]
- **If Refuted**: [Alternative interpretations or approaches needed]
- **Action Items**: [Specific next steps based on result]

### Related Artifacts
- **Experiments**: [Links to experiment markdowns]
- **Data Sources**: [Links to dataset EDAs]
- **Visualizations**: [Links to supporting charts/plots]
- **Follow-up Hypotheses**: [New hypotheses generated from this result]
```

## Integration with Workflow

### Checkpoint Integration

Hypotheses should be generated and validated at specific workflow checkpoints:

#### After Context Review
- Business assumption hypotheses
- Data availability hypotheses
- Success metric hypotheses

#### After EDA
- Data quality hypotheses
- Pattern identification hypotheses
- Feature relevance hypotheses

#### Before Modeling
- Model selection hypotheses
- Parameter initialization hypotheses
- Performance expectation hypotheses

#### After Model Evaluation
- Result interpretation hypotheses
- Generalization hypotheses
- Improvement opportunity hypotheses

### TodoWrite Integration

When using the TodoWrite tool, include hypothesis-related tasks:
- `Generate hypotheses from EDA findings`
- `Test hypothesis H-001: [title]`
- `Document hypothesis validation results`
- `Create follow-up hypotheses from results`

## Project Structure

For each project, maintain hypothesis tracking in:

```
<PROJECT_ROOT>/
├── hypotheses/
│   ├── hypothesis_log.md          # Main tracking document
│   ├── active/                    # Currently being tested
│   │   └── H-XXX_title.md
│   ├── validated/                 # Confirmed hypotheses
│   │   └── H-XXX_title.md
│   └── refuted/                   # Failed hypotheses
│       └── H-XXX_title.md
```

### Getting Started
1. Create the hypothesis folder structure in your project
2. Copy templates from `.auto-analysis/framework/templates/`:
   - `hypothesis_log_template.md` → `hypothesis_log.md`
   - `hypothesis_template.md` → Use for each new hypothesis
3. Update the templates with your project information

## Hypothesis Log Format

The main `hypothesis_log.md` should maintain a summary table:

```markdown
# Hypothesis Log - [PROJECT_NAME]

## Summary Statistics
- Total Hypotheses: XX
- Confirmed: XX (XX%)
- Refuted: XX (XX%)
- Partial: XX (XX%)
- In Testing: XX

## Hypothesis Registry

| ID | Date | Category | Title | Status | Impact |
|----|------|----------|-------|---------|--------|
| H-001 | 2024-01-15 | Business Logic | Sunday Revenue Dominance | ✅ Confirmed | High |
| H-002 | 2024-01-16 | Model Assumption | Gompertz Curve Fit | ✅ Confirmed | High |
| H-003 | 2024-01-17 | Data Quality | Geographic Completeness | ⚠️ Partial | Medium |

## Key Insights from Validated Hypotheses
[Summary of major findings and their implications]

## Open Questions Requiring Hypotheses
[List of areas needing hypothesis formulation]
```

## Agent-Specific Guidelines

### For csv-data-explorer Agent
**Focus**: Pure technical exploration and documentation
- Provides comprehensive statistical analysis
- Documents data quality issues objectively
- Creates standardized technical documentation
- **Does NOT generate hypotheses** - just reports facts

### For model-builder Agent
Before modeling, formulate hypotheses about:
- Appropriate model families
- Feature importance expectations
- Performance benchmarks
- Parameter interpretations
- Generalization capability

## Best Practices

### DO:
- State hypotheses BEFORE testing
- Make hypotheses specific and measurable
- Include null hypotheses when appropriate
- Document failed hypotheses (they're valuable learning)
- Link hypotheses to business questions
- Update hypotheses based on new evidence

### DON'T:
- Create hypotheses after seeing results (HARKing)
- Make vague, untestable statements
- Ignore contradictory evidence
- Delete failed hypotheses
- Test multiple hypotheses without correction for multiple comparisons

## Communication Protocol

### Reporting to Stakeholders
When communicating hypothesis results:

1. **Lead with business impact**: Start with what it means, not technical details
2. **Show confidence levels**: Be transparent about uncertainty
3. **Visualize evidence**: Use charts/plots to support conclusions
4. **Propose next steps**: What actions should be taken based on results

### Example Communication:
```
"We tested whether Sunday drives disproportionate revenue (H-001). 
Confirmed: Sundays generate 26.9% of weekly revenue, 3.8x the daily average.
Implication: Concentrate marketing spend on Friday-Saturday for Sunday conversions.
Confidence: 99.9% statistical significance across all cohorts."
```

## Hypothesis Quality Metrics

Track the quality of hypothesis generation and testing:

- **Specificity Rate**: % of hypotheses with measurable criteria
- **Confirmation Rate**: % of hypotheses confirmed (should be 30-70% for good hypotheses)
- **Business Impact Rate**: % of hypotheses affecting decisions
- **Test Coverage**: % of model assumptions with corresponding hypotheses

## Version Control

- Hypotheses should be versioned if modified
- Keep original hypothesis even if refined
- Document why hypotheses were updated
- Track hypothesis evolution over project lifecycle

---

*This framework ensures scientific rigor and transparent communication in all analytical work. Every agent and analyst should follow these guidelines when working within the LLM Automation Framework.*