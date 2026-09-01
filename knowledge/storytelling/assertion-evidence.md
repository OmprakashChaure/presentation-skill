# Assertion-Evidence

## Purpose

Define the assertion-evidence slide structure — the strong default for technical, scientific, educational, and analytical substantive slides.

## Scope

**Strong default for:** Technical, scientific, educational, analytical presentations.

**Do NOT force onto:** Title, agenda, section divider, navigation, reference slides.

## Structure

```
ASSERTION (Declarative Slide Title)
    │
    ├── VISUAL EVIDENCE (Chart, Diagram, Table, Image)
    │       │
    │       └── ANNOTATION (Direct labels, callouts, highlights)
    │
    └── IMPLICATION (So what? / Takeaway / Next step)
```

## Component Rules

### Assertion (Slide Title)

- **MUST** be a complete declarative sentence
- **MUST** communicate the slide's key message
- **MUST NOT** be a topic label ("Revenue") — use claim ("Revenue grew 12% YoY")
- **SHOULD** be readable in <3 seconds
- **Font:** `h2` or `h3` token (assertion role)

### Visual Evidence

- **MUST** directly support the assertion
- **MUST** be the dominant visual element (secondary in hierarchy only to assertion)
- **Types by assertion type:**

| Assertion Type | Evidence Visual |
|----------------|-----------------|
| Trend | Time-series chart |
| Comparison | Bar/dot chart |
| Ranking | Ordered bar/dot |
| Distribution | Histogram/box plot |
| Relationship | Scatter plot |
| Composition | Stacked bar/treemap |
| Process | Flow diagram |
| Architecture | System diagram |
| Exact values | Table |

### Annotation

- **MUST** visually integrate with evidence (not separate text block)
- **Direct labels > Legends** — label data series directly on chart
- **Callouts** for: outliers, thresholds, targets, key data points
- **Highlight** the evidence that proves the assertion (colour, outline, arrow)

### Implication

- **SHOULD** be explicit: "So what?" / "Therefore..." / "Next: ..."
- **Placement:** Near evidence, visually distinct (accent colour, callout box)
- **Optional for:** Purely informational slides where implication is obvious

## Evidence Quality Rules

- **Source:** Every evidence visual MUST have source citation (bottom, `caption` token)
- **Recency:** Data MUST be dated; stale data flagged
- **Denominator:** Rates/percentages MUST show base (n=...)
- **Uncertainty:** Confidence intervals, error bars, ranges where applicable
- **No cherry-picking:** Full data range shown unless justified

## Decorative Imagery ≠ Evidence

| Decorative (NOT Evidence) | Evidence |
|---------------------------|----------|
| Stock photo of team | Customer quote with photo + name/role |
| Abstract background | Screenshot of product feature |
| Generic icon | Architecture diagram with labels |
| "Engagement" illustration | Usage funnel chart |

**Rule:** IF removing the image does not weaken the assertion → it is decorative → REMOVE or mark decorative.

## Slide Mapping

| Slide Purpose | Use Assertion-Evidence? |
|---------------|-------------------------|
| Make a claim with data | YES (default) |
| Explain a mechanism | YES (diagram as evidence) |
| Compare options | YES (comparison chart as evidence) |
| Show trend | YES (time-series as evidence) |
| Title slide | NO |
| Agenda | NO |
| Section divider | NO |
| Appendix/Reference | NO (use table/reference slide type) |

## Anti-Patterns

- **Topic title:** "Q3 Revenue" instead of "Q3 Revenue Exceeded Target by 12%"
- **Evidence without annotation:** Chart with no labels, no callout
- **Assertion without evidence:** Claim with no supporting visual
- **Evidence without assertion:** Chart with no message title
- **Decorative image as "evidence":** Stock photo labelled "evidence"
- **Legend-dependent chart:** Audience must cross-reference legend
- **Implication missing:** Evidence shown but no "so what?"

## Handoff to Other Layers

- **Slide-types:** Assertion-evidence is a slide archetype
- **Chart-selection:** Maps assertion type → evidence visual
- **Diagrams:** Process/architecture as evidence visuals
- **Visual-hierarchy:** Assertion = primary, Evidence = secondary, Annotation/Implication = tertiary
- **Evaluation:** Checks: declarative title, evidence supports assertion, annotation present, source cited