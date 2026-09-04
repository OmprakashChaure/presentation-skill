# Select Visualization — Reasoning Contract

## Purpose

Select the appropriate visual representation for evidence on each slide.

## Input

```json
{
  "slides": [                          // From select_slide_type output
    {
      "slide_id": "string",
      "intent": { ... },
      "evidence": {
        "required": "boolean",
        "type": "enum|null",
        "description": "string",
        "visual_representation": { ... }  // To be refined
      }
    }
  ],
  "available_data": [...],             // From context.available_data
  "global_strategy": { ... }
}
```

## Output

```json
{
  "slides": [                          // Updated with refined visual_representation
    {
      ...
      "evidence": {
        ...
        "visual_representation": {
          "preferred": "enum",
          "alternatives": ["enum"],
          "rationale": "string",
          "annotation_requirements": ["string"],
          "data_mapping": {            // How data maps to visual
            "x": "field|null",
            "y": "field|null",
            "series": "field|null",
            "size": "field|null",
            "color": "field|null",
            "facet": "field|null"
          },
          "encoding_requirements": {   // Per chart-selection.md
            "zero_baseline": "boolean",
            "direct_labels": "boolean",
            "uncertainty": "boolean",
            "proportional_time": "boolean"
          }
        }
      }
    }
  ],
  "assumptions": [...],
  "clarification_requirements": [...]
}
```

## Procedure

### 1. Visual Representation Selection

For each slide with `evidence.required = true`, apply decision framework from `knowledge/visualization/chart-selection.md`:

**Core Question:** "What relationship does the audience need to understand?"

| Evidence Description | Relationship | Preferred Visual |
|---------------------|--------------|------------------|
| "Trend over time", "How X changed", "Growth trajectory" | Trend | line_chart |
| "Compare A vs B vs C", "Which is higher", "Performance by segment" | Comparison | bar_chart / dot_plot |
| "Rank from highest to lowest", "Top 10", "Leaderboard" | Ranking | ordered_bar / ordered_dot |
| "Distribution of values", "Spread", "Variation", "Outliers" | Distribution | histogram / box_plot / violin |
| "Relationship between X and Y", "Correlation", "Driver analysis" | Relationship | scatter_plot / bubble_chart |
| "Exact values for lookup", "Specifications", "Detailed comparison" | Exact Lookup | table |
| "Part of whole", "Composition", "Breakdown", "Market share" | Composition | stacked_bar_100 / treemap / waffle |
| "Process steps", "Flow", "Decision logic", "User journey" | Process | flow_diagram / process_diagram |
| "System components", "Architecture", "Dependencies", "Data flow" | System Structure | architecture_diagram (C4) |
| "Hierarchy", "Org chart", "Classification", "Taxonomy" | Hierarchy | tree_map / icicle / org_chart |
| "Geographic distribution", "Regional performance", "Location data" | Geospatial | choropleth / symbol_map |

### 2. Contextual Refinement

Apply modifiers from `knowledge/visualization/chart-selection.md`:

**Scale & Units:**
- If values span orders of magnitude → Consider log scale (label clearly)
- If comparing parts of whole → stacked_bar_100 or treemap
- If small differences matter → dot_plot over bar_chart

**Denominator:**
- If rates/percentages → MUST show denominator (n=...) in annotation_requirements

**Timeframe:**
- If time series → proportional_time: true
- If irregular intervals → Note in annotation_requirements

**Ordering:**
- Categorical → Order by value (not alphabet) unless natural order
- Time → Chronological

**Uncertainty:**
- If estimates/projections → uncertainty: true, show CI/error bars
- If survey/sample → uncertainty: true

**Labels:**
- direct_labels: true (prefer over legend)
- legend only if >6 series or space constrained

### 3. Data Mapping

For each visual, define `data_mapping` from available data fields:

```json
{
  "x": "time_period",
  "y": "revenue_usd",
  "series": "region",
  "size": "null",
  "color": "region",
  "facet": "product_line"
}
```

If data not yet available → Set fields to `null`, add clarification requirement.

### 4. Encoding Requirements

Set per chart-selection.md rules:

| Visual | zero_baseline | direct_labels | uncertainty | proportional_time |
|--------|---------------|---------------|-------------|-------------------|
| bar_chart | true | true | if estimates | false |
| line_chart | false | true | if estimates | true |
| dot_plot | false | true | if estimates | false |
| ordered_bar | true | true | if estimates | false |
| histogram | true | false | false | false |
| box_plot | false | false | true | false |
| scatter_plot | false | true | if estimates | false |
| stacked_bar_100 | true | true | false | false |
| treemap | N/A | true | false | false |
| table | N/A | N/A | N/A | N/A |

### 5. Annotation Requirements

Generate specific annotation requirements:

| Visual | Required Annotations |
|--------|---------------------|
| All charts | Title = assertion, Axis labels + units, Source |
| Trend | Key inflection points, Target line, Period markers |
| Comparison | Highlight (target/best), Value labels on bars |
| Ranking | Rank numbers, Cutoff line if top-N |
| Distribution | Median/mean line, Outlier labels |
| Relationship | Trend line, R², Quadrant labels if meaningful |
| Composition | Segment labels + %, "Other" if aggregated |
| Process | Step numbers, Decision labels (Y/N), Swimlane headers |
| Architecture | Component types, Protocol labels, Boundary names |
| Timeline | Phase bands, Milestone markers, Today line |

### 6. Diagram-Specific Selection (Non-Chart)

If `evidence.type = diagram`:

| Description | Diagram Type | Level |
|-------------|--------------|-------|
| "How data flows", "User journey", "Process steps" | flow_diagram | — |
| "System architecture", "Components", "Microservices" | architecture_diagram | context / container / component |
| "Org structure", "Classification", "Taxonomy" | hierarchy_diagram | — |
| "Entity relationships", "Network", "Dependencies" | relationship_diagram | — |
| "Full system view" | system_diagram | C4 multi-level |

## Decision Rules

- **MUST** start with relationship question, not chart preference
- **MUST** apply chart-selection.md framework
- **MUST** set direct_labels: true unless >6 series
- **MUST** set zero_baseline: true for bar/area charts
- **MUST** include uncertainty for estimates/projections
- **MUST** define data_mapping fields or flag as clarification
- **MUST NOT** use 3D charts, pie >5 slices, radar/spider, gauges
- **SHOULD** prefer dot_plot over bar for small differences
- **SHOULD** prefer treemap over pie for composition >5 parts

## Knowledge Consumption

- `knowledge/visualization/chart-selection.md` — Decision framework, forbidden encodings
- `knowledge/visualization/diagrams.md` — Diagram types, notation standards
- `knowledge/visualization/tables.md` — When to use tables
- `knowledge/visualization/data-storytelling.md` — Question→Data→Comparison→Insight flow

## Clarification Triggers

Generate clarification when:
- Relationship ambiguous → "What relationship should the audience see? (trend, comparison, distribution...)"
- Data fields unknown → "What data fields map to X/Y/Series for this chart?"
- Evidence type unclear → "Is this evidence quantitative (chart), structural (diagram), or narrative (case study)?"
- Uncertainty not quantified → "Do you have confidence intervals/error bars for these estimates?"