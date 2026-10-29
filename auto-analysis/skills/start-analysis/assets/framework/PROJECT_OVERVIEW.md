# LLM Automation Framework Overview

## Project Goal

Create a **framework that lets an LLM run common marketing-analytics tasks autonomously** (EDA, LTV models, MMM, funnel analysis, etc.) while keeping a **human-in-the-loop** for key decisions and contextual knowledge.

## Supported Tasks

| Category | Examples |
|----------|----------|
| Exploratory & Diagnostic | Exploratory Data Analysis (EDA) |
| Predictive / Modeling | Lifetime-Value models (cohort-level & user-level) |
| Attribution / Optimization | Marketing-Mix Modeling (MMM) |
| Behavioral / Funnel | Funnel analysis |

## Core Design Principle

**Everything flows through Markdown.**  
Markdown is the lingua‑franca for passing context, logging results, and guiding the LLM.

## High-Level Vision

- **Standard prompt templates** orchestrate each building block.  
- The framework stitches blocks into an end‑to‑end automated flow, yet surfaces **clear checkpoints** for human judgment.  
- Result: faster, reproducible analyses with just‑enough human guidance.