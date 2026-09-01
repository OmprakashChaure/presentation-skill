# Chart Selection Decision Framework

## Purpose

Decision framework for selecting chart types based on the information relationship the audience needs to understand.

## Core Principle

**Start with:** "What relationship does the audience need to understand?"
**Then map:** Relationship → Default chart type → Refine by context

## Relationship → Chart Mapping (Defaults, Not Laws)

| Relationship | Question | Default Chart | Alternatives |
|--------------|----------|---------------|--------------|
| **Trend over time** | How does X change over time? | Line chart | Area, Connected scatter, Horizon |
| **Comparison** | How do A, B, C compare on X? | Bar/Column chart | Dot plot, Slope chart (2 timepoints) |
| **Ranking** | What is the order from highest to lowest? | Ordered bar/dot | Lollipop, Barcode |
| **Distribution** | What is the shape/spread of values? | Histogram | Box plot, Violin, Density, Ridgeline |
| **Relationship** | How does X relate to Y? | Scatter plot | Bubble (3rd var), Heatmap (binned), Connected scatter |
| **Exact lookup** | What is the precise value for X? | Table | Annotated bar (few values) |
| **Composition (part-to-whole)** | How do parts contribute to total? | Stacked bar (100%) | Treemap, Sunburst, Waffle, Pie (≤5 parts) |
| **Flow/Process** | What are the steps/transitions? | Sankey / Flow diagram | Process diagram, Chord |
| **Hierarchy** | What is the parent-child structure? | Tree map / Icicle | Org chart, Dendrogram |
| **Geospatial** | Where does X occur? | Choropleth / Symbol map | Cartogram, Dot density |

## Contextual Refinement Rules

### Scale & Units
- **MUST** show: Axis scale, Units, Zero baseline (for bar/area)
- **Log scale:** Only when multiplicative relationships; label clearly
- **Dual axis:** AVOID — use indexed lines or separate charts

### Denominator & Rate
- **MUST** disclose: Denominator for rates/percentages (n=...)
- **Rule:** Never show % without base

### Timeframe & Granularity
- **Match** granularity to decision cycle (daily for ops, quarterly for board)
- **Proportional spacing:** Time intervals proportional on axis

### Ordering
- **Categorical:** Order by value (not alphabet) unless natural order exists
- **Time:** Chronological always

### Uncertainty
- **MUST** show: Confidence intervals, Error bars, Prediction intervals
- **Default:** 95% CI; label level

### Labels & Direct Labelling
- **MUST prefer:** Direct labels on elements over legends
- **Legend:** Only when direct labelling impossible (too many series, space)
- **Data labels:** Show values when precision needed; omit when trend is message

### Misleading Encodings (MUST NOT)

| Forbidden | Why | Alternative |
|-----------|-----|-------------|
| Truncated Y-axis (bar) | Exaggerates differences | Start at zero; use dot plot if small differences |
| 3D charts | Distorts perception | 2D only |
| Area encoding for 1D data | Area ∝ value² misleads | Bar/line for 1D |
| Inverted axis (no reason) | Confounds intuition | Standard orientation |
| Pie >5 slices | Angle discrimination fails | Stacked bar, treemap |
| Radar/spider | Angle/area distortion | Parallel coordinates, grouped bar |
| Gauge/meter | Low data density | KPI tile + sparkline |

## Chart Quality Checklist (Per Chart)

- [ ] Title = Assertion (declarative message)
- [ ] Axes labelled with units
- [ ] Scale appropriate (zero baseline for bars)
- [ ] Direct labels on series/elements
- [ ] Uncertainty shown if applicable
- [ ] Source cited
- [ ] Colour accessible (contrast, colourblind-safe)
- [ ] No chartjunk (3D, gradients, shadows, decorations)
- [ ] Aspect ratio supports comparison (wider for time, taller for ranking)

## Anti-Patterns

- Chart type chosen for aesthetics not relationship
- Defaulting to pie/bar without relationship reasoning
- Legend-dependent charts (audience cross-references)
- Missing uncertainty on estimates
- Truncated axes on bar charts
- 3D or decorative effects
- Too many series (>6 lines, >8 bars)

## Handoff to Other Layers

- **Data-storytelling:** Implements Question → Data → Comparison → Insight → Visual → Annotation → Implication
- **Reasoning (select_visualization):** Implements this decision framework
- **Charts generation:** Produces chart specs from selected type
- **Evaluation:** Checks: Relationship match, labelling, uncertainty, source, accessibility, no misleading encodings