# Research Presentation Type

## Purpose

Define type-specific policies for research/analysis presentations.

## Scope

Academic presentations, scientific talks, market research, data analysis reports, analytical findings reviews.

## Core Policies

### Research Question

- **MUST** state explicit research question upfront (slide 1 or 2)
- **Format:** "Does X affect Y in context Z?" or "What is the relationship between X and Y?"
- **SHOULD** include: Hypothesis (if confirmatory), Exploratory scope (if exploratory)

### Motivation & Gap

- **MUST** explain: Why this question matters, What is already known, What gap this fills
- **Literature context:** 1–2 slides max; reference appendix for full review
- **Rule:** No literature dump — only what frames the gap

### Methodology Transparency

- **MUST** disclose: Design, sample, measures, analysis plan, limitations
- **Format:** "We [method] with [sample] measuring [variables] using [analysis]"
- **Pre-registration:** Reference if applicable
- **Anti-pattern:** "We analyzed the data" without design disclosure

### Data & Findings Separation

- **MUST** separate: Data (what the data shows) from Interpretation (what it means)
- **Data slides:** Descriptive statistics, visualizations, model outputs — no causal language
- **Interpretation slides:** Explicitly labelled "Interpretation" or "Discussion"
- **Rule:** No causal claims in data slides

### Uncertainty & Limitations

- **MUST** quantify uncertainty: Confidence intervals, standard errors, credible intervals
- **MUST** declare limitations: Sample constraints, measurement limits, design threats, generalizability
- **Format:** "Limitation: [specific] → Impact on inference: [direction/magnitude]"
- **Rule:** Limitations that could reverse conclusion = release blocker

### Interpretation vs. Data

| Data Language | Interpretation Language |
|---------------|------------------------|
| "Group A scored 12% higher (95% CI: 8–16%)" | "This suggests A may improve outcomes" |
| "Correlation r = 0.42, p < 0.01" | "Consistent with hypothesis that..." |
| "Model predicts 73% variance" | "Supports the mechanism, but..." |

### Causal Claims — Strict Rules

- **MUST NOT** claim causation from observational data without: Design justification (RCT, quasi-experiment, IV, DiD) + Assumption disclosure
- **MUST** use: "Associated with," "Predicts," "Consistent with" — not "Causes," "Drives," "Leads to" unless design warrants
- **MUST** disclose: Confounding, selection bias, reverse causality threats

### Anti-Patterns (MUST PREVENT)

| Anti-Pattern | Detection | Correction |
|--------------|-----------|------------|
| Causal overclaiming | "X causes Y" from correlation | Require design justification; rephrase to association |
| Cherry-picking | Only significant results shown | Require all pre-specified analyses; appendix for exploratory |
| Omitted denominators | "30% improvement" without base rate | Require absolute numbers, base rates, N |
| Correlation ≠ causation | Causal language without design | Enforce language rules; flag in evaluation |
| P-hacking disclosure | Many analyses, only significant shown | Require analysis plan or correction |

## Slide Type Defaults

| Purpose | Slide Archetype |
|---------|-----------------|
| Research question | Title/Objectives |
| Literature gap | Comparison (Gap analysis) |
| Methodology | Process diagram / Reference table |
| Data description | Chart/Data (descriptive) |
| Main findings | Assertion-Evidence (per finding) |
| Uncertainty | Chart (CI/error bars) |
| Limitations | Reference/List |
| Interpretation | Assertion-Evidence (qualitative) |
| Implications | Pyramid (Answer → Arguments) |

## Narrative Default

- **Primary:** Research pattern (Question → Method → Data → Findings → Uncertainty → Interpretation → Implications)
- **Executive summary:** Pyramid (for leadership audience)

## Design Adaptations

- **Density:** Higher — analytical audience expects detail
- **Charts:** Error bars, CIs, raw data points (not just aggregates)
- **Tables:** Preferred for exact statistics, model coefficients
- **Colour:** Sequential/diverging for continuous data; semantic for categories
- **Appendix:** Extensive — full tables, robustness checks, additional analyses

## Handoff to Other Layers

- **Reasoning:** Selects research pattern; enforces causal language rules
- **Visualization:** Charts with uncertainty; tables for exact values
- **Data-storytelling:** Question → Data → Comparison → Insight → Visual → Annotation → Implication
- **Evaluation:** Checks: Question stated, methodology transparent, data/interpretation separated, uncertainty quantified, causal language correct, limitations declared