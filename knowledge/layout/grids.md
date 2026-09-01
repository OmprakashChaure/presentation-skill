# Grids

## Purpose

Define the grid system — safe area, margins, columns, rows, gutters, alignment anchors, spacing tokens, aspect ratio adaptation.

## Core Principle

Grid geometry is a SYSTEM, not arbitrary pixel placement. All layout decisions derive from grid.

## Safe Area & Margins

| Aspect Ratio | Slide Size | Safe Margin | Content Width | Content Height | Columns |
|--------------|------------|-------------|---------------|----------------|---------|
| **16:9** | 13.333" × 7.5" (1280×720) | 48px (space-2xl) | 1184px | 576px | 12 |
| **16:9 HD** | 1920×1080 | 72px | 1776px | 936px | 12 |
| **4:3** | 10" × 7.5" (960×720) | 48px | 864px | 624px | 8 |
| **Custom** | W × H | 5% min dimension | W - 2M | H - 2M | 8 or 12 |

**Rule:** Essential content MUST stay within safe area. Bleed elements (backgrounds) MAY extend to edge.

## Column Grid

### 12-Column (16:9 Default)

```
| Margin | C1 | G | C2 | G | C3 | G | C4 | G | C5 | G | C6 | G | C7 | G | C8 | G | C9 | G | C10 | G | C11 | G | C12 | Margin |
| 48px   | 64 |16| 64 |16| 64 |16| 64 |16| 64 |16| 64 |16| 64 |16| 64 |16| 64 |16| 64  |16| 64  |16| 64  | 48px  |
```

- **Column width:** 64px (1280px base)
- **Gutter:** 16px (space-md)
- **Margin:** 48px (space-2xl)

### 8-Column (4:3 / Dense)

```
| Margin | C1 | G | C2 | G | C3 | G | C4 | G | C5 | G | C6 | G | C7 | G | C8 | Margin |
| 48px   | 84 |16| 84 |16| 84 |16| 84 |16| 84 |16| 84 |16| 84 |16| 84 | 48px  |
```

- **Column width:** 84px (960px base)
- **Gutter:** 16px
- **Margin:** 48px

## Row Grid (Baseline Grid)

- **Base unit:** 8px (space-sm)
- **Row height:** 24px (3× base) for body text lines
- **Baseline alignment:** Text baselines snap to 8px grid
- **Vertical rhythm:** All vertical spacing = multiples of 8px

## Alignment Anchors

| Anchor | Use Case |
|--------|----------|
| **Left** | Primary (LTR) — strongest reading anchor |
| **Center** | Title slides, Section dividers, KPI tiles |
| **Right** | Annotations, Source lines, Secondary metrics |
| **Top** | Slide title, Section header |
| **Bottom** | Source, Footer, Page number |
| **Baseline** | Multi-column text, Label-value pairs |

**Rule:** Default = Left + Baseline. Center only for symmetric layouts (title, divider, KPI).

## Spacing Tokens (from spacing.md)

| Token | Value | Grid Multiple |
|-------|-------|---------------|
| space-xs | 4px | 0.5× |
| space-sm | 8px | 1× (base unit) |
| space-md | 16px | 2× (gutter) |
| space-lg | 24px | 3× (row) |
| space-xl | 32px | 4× |
| space-2xl | 48px | 6× (margin) |
| space-3xl | 64px | 8× |

**All positioning MUST use tokens.**

## Layout Zones (12-Col Grid)

| Zone | Columns | Typical Use |
|------|---------|-------------|
| **Full** | 1–12 | Title, Section divider, Full-width chart |
| **Two-thirds** | 1–8 | Assertion-Evidence (assertion + evidence) |
| **Half** | 1–6 / 7–12 | Comparison, Two-column content |
| **Third** | 1–4 / 5–8 / 9–12 | Three-column, KPI row |
| **Quarter** | 1–3 / 4–6 / 7–9 / 10–12 | Four-column, Metric tiles |
| **Sidebar** | 1–3 or 10–12 | Navigation, Annotations, Source column |

## Aspect Ratio Adaptation

| From → To | Strategy |
|-----------|----------|
| 16:9 → 4:3 | Reflow: 12-col → 8-col; stack horizontal zones vertically; reduce margins to space-xl |
| 4:3 → 16:9 | Expand: 8-col → 12-col; distribute horizontal; increase margins to space-2xl |
| Custom | Recalculate: Column count (8 or 12), Column width, Gutter (space-md), Margin (5%) |

**Rule:** Content reflows — never stretches. Typography tokens adapt per typography.md.

## Grid Validation Rules

- [ ] All elements align to column edges (start/end on column boundary)
- [ ] All vertical positions align to 8px baseline grid
- [ ] No element exceeds safe margins
- [ ] Gutters consistent (space-md) unless nested grid
- [ ] Nested grids inherit parent gutter or use space-sm
- [ ] Whitespace between zones = space-lg minimum

## Handoff to Other Layers

- **Composition:** Consumes grid for focal point, grouping, balance
- **Responsive-layout:** Selects column count, density variant
- **Slide-types:** Maps archetypes to grid zones
- **Generation:** Positions elements via grid coordinates
- **Evaluation:** Checks: Grid alignment, Safe margins, Token compliance, Baseline rhythm