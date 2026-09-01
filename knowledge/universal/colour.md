# Colour

## Purpose

Define the semantic colour system — roles, contrast, accessibility, consistency, and brand subordination rules.

## Scope

All visual elements in all presentations.

## Semantic Colour Roles

| Role | Purpose | Usage | Accessibility |
|------|---------|-------|---------------|
| `background` | Slide canvas | Slide background, card backgrounds | N/A (contrast tested against text) |
| `text-primary` | Highest readability text | Assertions, body, headings | 4.5:1 vs background (WCAG AA) |
| `text-secondary` | Supporting text | Labels, annotations, metadata | 4.5:1 vs background |
| `text-muted` | Low-priority text | Sources, timestamps, assumptions | 3:1 vs background (large text) |
| `accent` | Primary brand/action | Primary buttons, key highlights, links | 3:1 vs background (UI) |
| `accent-hover` | Interactive state | Hover/focus on accent elements | 3:1 vs background |
| `status-info` | Informational | Neutral callouts, progress | 3:1 vs background |
| `status-warning` | Caution/attention | At-risk metrics, pending items | 3:1 vs background + icon |
| `status-success` | Positive completion | Achieved targets, completed steps | 3:1 vs background + icon |
| `status-error` | Critical failure | Failed metrics, blockers | 3:1 vs background + icon |
| `category-1`..`category-8` | Data series discrimination | Chart lines, bars, diagram groups | 3:1 vs background; pairwise distinguishable |

## Colour Palette Structure

```
semantic-colour = {
  light: { background, text-primary, text-secondary, text-muted, accent, status-*, category-* },
  dark:  { background, text-primary, text-secondary, text-muted, accent, status-*, category-* }
}
```

**MUST** provide both light and dark mode palettes.

## Contrast Rules

- **Text (normal):** 4.5:1 minimum (WCAG AA)
- **Text (large ≥18pt/14pt bold):** 3:1 minimum
- **UI components / graphics:** 3:1 minimum
- **Category colours:** 3:1 vs background; MUST be distinguishable from each other (simulate deuteranopia/protanopia)

## Accessibility Rules

1. **Colour MUST NOT be sole carrier of essential meaning** — redundant encoding required (icon, pattern, label, position)
2. **Brand colours are SUBORDINATE to accessibility** — if brand colour fails contrast, use accessible variant
3. **Category palette limited to 8 hues** — human discrimination limit; use sequential/diverging for >8
4. **Status colours MUST include icon/text** — never colour-only for warning/success/error

## Consistency Rules

- **Semantic meaning = same colour everywhere** — `status-warning` always same hue
- **Design system tokens ONLY** — no hex/rgb in slide logic
- **Chart category order fixed** — category-1, category-2... consistent across all charts in deck
- **Diagram convention:** Process flow = accent; Decision = warning; Data store = info; External = muted

## Colour-Only Encoding Prohibition

| Forbidden | Required Redundant Encoding |
|-----------|----------------------------|
| Red/green only for good/bad | Add ✓/✗ icons or "Good"/"Bad" labels |
| Colour-only chart legend | Direct labelling on chart elements |
| Colour-only diagram status | Shape + colour (▲ warning, ● error, ■ success) |
| Colour-only table highlighting | Bold + background + text label |

## Brand Colour Handling

- Brand colours mapped to semantic roles where they meet contrast
- **IF** brand primary fails contrast on brand background → use `accent` for UI, keep brand for logo only
- **IF** brand palette lacks accessible status colours → use system status colours
- **NEVER** compromise readability for brand compliance

## Anti-Patterns

- Using brand colours directly without semantic mapping
- >8 categorical colours in one chart
- Red/green as only distinction (colourblind unsafe)
- Decorative gradients on charts (reduces readability)
- Low-contrast "subtle" text (fails WCAG)
- Different hues for same meaning across slides

## Handoff to Other Layers

- **Design system** defines exact colour values per theme (light/dark)
- **Charts/diagrams** consume category/status tokens
- **Typography** consumes text-* tokens
- **Evaluation** checks: contrast ratios, redundant encoding, token compliance, colourblind simulation