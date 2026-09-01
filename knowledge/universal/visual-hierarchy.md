# Visual Hierarchy

## Purpose

Define how the system creates and controls visual hierarchy to guide audience attention and comprehension.

## Scope

All substantive slides in all presentations.

## Core Concepts

### Information Tiers

| Tier | Role | Visual Treatment |
|------|------|------------------|
| Primary (Focal Point) | The ONE thing audience must see first | Largest, highest contrast, top/left position, most whitespace |
| Secondary | Supporting evidence, key details | Medium size, medium contrast, grouped near primary |
| Tertiary | Context, sources, annotations | Smallest, lowest contrast, consistent position (bottom/right) |

### Visual Weight Variables

- **Size** — Larger = more important
- **Position** — Top-left (Western reading) = first attention
- **Contrast** — High contrast (colour, weight) = emphasis
- **Whitespace** — Isolation = importance
- **Alignment** — Breaking alignment = attention
- **Grouping/Proximity** — Related items close; unrelated separated
- **Visual Weight** — Bold, colour, icon, shape, whitespace

## Decision Rules

### Default Hierarchy for Assertion-Evidence Slides

1. **Assertion (slide title)** — Primary focal point
2. **Evidence visual** — Secondary (chart/diagram/table)
3. **Annotation/Implication** — Tertiary (callouts, takeaway)
4. **Source** — Tertiary (bottom, muted)

### Hierarchy by Slide Purpose

| Slide Purpose | Primary | Secondary | Tertiary |
|---------------|---------|-----------|----------|
| Assertion-Evidence | Assertion title | Evidence visual + annotation | Source, assumptions |
| Comparison | Comparison criteria | Items being compared | Detail values, notes |
| Process/Flow | Flow direction + key steps | Decision points, branches | Timing, owners, exceptions |
| Architecture | Major components + relationships | Data flows, interfaces | Technologies, protocols |
| KPI/Metric | The metric value + status | Trend, target, variance | Period, definition, source |
| Timeline | Time axis + milestone events | Phase grouping | Details, dependencies |

## Exceptions (Where Default Hierarchy Changes)

### Comparison Slides
- **Primary:** Comparison criteria (what is being compared)
- **Secondary:** The items side-by-side
- **Rationale:** Audience needs criteria first to evaluate items

### Dashboard/KPI Slides
- **Primary:** Current status (value + health indicator)
- **Secondary:** Trend sparkline
- **Tertiary:** Target, variance, period
- **Rationale:** Executive scan: "Is it good or bad?" first

### Multi-Panel Analytical Slides
- **Primary:** Panel titles (each panel has its own assertion)
- **Secondary:** Panel evidence
- **Rationale:** Each panel is a mini assertion-evidence unit

## Anti-Patterns (MUST AVOID)

| Anti-Pattern | Problem | Correction |
|--------------|---------|------------|
| Everything emphasized | No focal point; cognitive overload | Apply 1 primary, 2 secondary max |
| Equal visual weight | Audience doesn't know where to look | Create clear size/contrast/position differential |
| Random bolding | False emphasis; looks unprofessional | Bold only for semantic emphasis (assertion, key metric) |
| Competing titles | Two large text blocks fighting for attention | One assertion title; others as labels/annotations |
| Excessive contrast | Visual fatigue; accessibility risk | Use contrast purposefully; meet WCAG, don't exceed needlessly |
| Centre-everything | No reading path; weak hierarchy | Left-align; use grid alignment anchors |

## Reading Order Rules

- **MUST** follow Z-pattern (top-left → top-right → bottom-left → bottom-right) for Western audiences
- **MUST** ensure logical reading order matches visual order (z-index = reading order)
- **SHOULD** use numbering/arrows for non-linear flows (process, decision trees)

## Handoff to Other Layers

- **Composition layer** implements hierarchy through layout grids and spacing tokens
- **Typography layer** provides size/weight scale for hierarchy tiers
- **Colour layer** provides contrast tokens for emphasis
- **Evaluation layer** checks: single focal point, reading order, contrast ratios