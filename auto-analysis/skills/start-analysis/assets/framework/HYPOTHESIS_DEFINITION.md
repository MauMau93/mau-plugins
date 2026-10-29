# Hypothesis Definition

## Purpose
The term **hypothesis** is used heavily in our modeling framework.  
To avoid confusion, this document defines exactly what we mean by *hypothesis* in our context, and how it differs from the strict scientific definition.

---

## Our Definition
A **hypothesis** in this framework is a **structured assumption or exploratory point** that we want to validate with data.  
It is broader than the classical scientific definition — it can include:

- **Scientific hypotheses**: Falsifiable statements that can be tested (e.g., "Customer LTV follows a Gompertz curve").
- **Assumption checks**: Things we need to verify before modeling (e.g., "Data from cohorts before 2018 is unreliable").
- **Validation points**: Criteria to confirm model performance or robustness (e.g., "MAPE should be <5% on holdout").
- **Exploratory ideas**: Potential business or feature relationships worth testing (e.g., "Retention differs by acquisition channel").

---

## Why We Use "Hypothesis"
- Keeps **scientific rigor**: everything we define must be testable or verifiable.  
- Encourages **iterative experimentation**: refine, reject, or confirm assumptions.  
- Ensures **business alignment**: each hypothesis ties directly to a business question or decision.  
- Provides a **unified language**: all agents (advisor, builder, explainer) speak in terms of hypotheses, so context is shared.

---

## Categories of Hypotheses
We organize hypotheses into categories for clarity:

1. **Data Pattern Hypotheses** – about distributions, seasonality, or feature relationships.  
2. **Model Performance Hypotheses** – about expected accuracy, generalization, or feature importance.  
3. **Business Logic Hypotheses** – about causal links, customer segments, or market effects.  
4. **Result-Based Hypotheses** – refinements or follow-ups based on prior results.  
5. **Integrity/Exclusion Hypotheses** – about whether certain cohorts, time periods, or datasets should be included/excluded.  
6. **Feature/Data Strategy Hypotheses** – about whether custom features or additional datasets improve performance.

---

## Documentation Standard
Every hypothesis must be written in a **clear, testable format**:

- **Statement** – Specific claim or assumption.  
- **Rationale** – Why it matters (EDA findings, business context).  
- **Test Design** – How it will be validated.  
- **Success Criteria** – What confirms it.  
- **Failure Criteria** – What refutes it.  
- **Business Impact** – Why it matters for decisions.  

---

## Key Takeaway
When we say **hypothesis**, we don’t just mean a narrow statistical claim.  
We mean **any structured, testable assumption, check, or exploratory idea** that guides our modeling and experimentation.

This flexible but rigorous use of the term ensures consistency across all agents and projects.
