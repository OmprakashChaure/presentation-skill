# Data Storytelling

## Purpose

Define the end-to-end process for turning data into communicated insight.

## Core Process

```
QUESTION → DATA → COMPARISON → INSIGHT → VISUAL → ANNOTATION → IMPLICATION
```

## Stage Rules

### 1. QUESTION

- **MUST** start with a specific question the audience needs answered
- **Format:** "How does X vary by Y?" "What drove change in Z?" "Is A better than B?"
- **Rule:** No "let's look at the data" — question first

### 2. DATA

- **MUST** define: Source, Scope, Timeframe, Granularity, Definitions, Limitations
- **Integrity checks:**
  - Completeness (missing data disclosed)
  - Consistency (definitions stable over time)
  - Validity (measures what it claims)
  - Currency (as-of date)
- **Rule:** No analysis without data provenance

### 3. COMPARISON

- **MUST** establish: What is being compared to what?
- **Comparison types:**
  - vs Target/Goal
  - vs Prior Period (YoY, QoQ, WoW)
  - vs Benchmark/Peer/Industry
  - vs Counterfactual (what if)
  - vs Segment (internal split)
- **Denominator:** MUST be explicit for rates

### 4. INSIGHT

- **Definition:** Non-obvious finding that answers the question
- **Test:** "Would the audience know this without this analysis?"
- **Format:** "[Finding] — driven by [Driver] — implying [Implication]"
- **Rule:** Insight ≠ Observation. "Revenue up 12%" = observation. "Revenue up 12% driven by APAC enterprise expansion, suggesting product-market fit in new segment" = insight.

### 5. VISUAL

- **Select** via chart-selection.md framework
- **Design** for the insight (not the data):
  - Highlight the comparison that reveals insight
  - Annotate the insight directly on chart
  - Remove noise (chartjunk, unnecessary series)

### 6. ANNOTATION

- **MUST** include: Insight callout, Driver labels, Context markers (events, changes)
- **Direct labels > Legends**
- **Callout style:** Accent colour, leader line, concise text
- **Placement:** Near the evidence, not floating

### 7. IMPLICATION

- **MUST** answer: "So what?" / "Now what?"
- **Types:** Decision, Action, Investigation, Monitoring, No action needed
- **Format:** "Implication: [Action/Decision] — Owner: [Who] — Timeline: [When]"

## Integrity Rules

### Data Integrity

- **No cherry-picking:** Show full range; disclose excluded data/why
- **No misleading scales:** Zero baseline for bars; proportional time axes
- **Correlation ≠ Causation:** Explicit language ("associated with," not "drives")
- **Uncertainty:** Show CI, error bars, ranges for estimates

### Context Rules

- **Absolute + Relative:** Show both (e.g., "+12% ($45M vs $40M)")
- **Denominator always:** "Conversion 3.2% (n=12,500 visits)"
- **Timeframe explicit:** "Q3 2024 vs Q3 2023"
- **Segmentation:** Show overall + key segments (Simpson's paradox guard)

### Annotation Rules

- **Every chart:** Title = Assertion (insight), not topic
- **Key data points:** Labelled (peaks, troughs, inflections, targets)
- **Events:** Marked (launches, outages, policy changes)
- **Source:** Bottom left, `caption` token

## Anti-Patterns (MUST PREVENT)

| Anti-Pattern | Detection | Correction |
|--------------|-----------|------------|
| Cherry-picking | Favorable period/subset only | Require full range + disclosure |
| Misleading scales | Truncated Y, non-proportional time | Enforce zero baseline, proportional time |
| Chart dumping | Multiple charts, no insight | One insight → one chart; appendix for rest |
| Unsupported conclusion | "Therefore X" without evidence | Require implication linked to insight |
| Correlation as causation | "X drives Y" from observational | Enforce language: "associated with" |
| Missing denominator | "30% increase" no base | Require absolute + relative |
| Insight-free chart | Title = "Revenue by Region" | Require assertion title |

## Handoff to Other Layers

- **Chart-selection:** Implements Visual stage
- **Reasoning:** Orchestrates full process
- **Charts generation:** Produces annotated chart specs
- **Slide-types:** Assertion-Evidence slide with data story
- **Evaluation:** Checks: Question defined, data sourced, comparison valid, insight non-obvious, visual supports insight, annotation present, implication actionable, integrity rules met