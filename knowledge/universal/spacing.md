# Spacing

## Purpose

Define the spacing system — safe margins, spacing scale, padding, grouping, proximity, alignment, gutters, and whitespace rules.

## Scope

All slide layouts in all presentations.

## Spacing Tokens (Design System)

| Token | Value (16:9 base) | Usage |
|-------|-------------------|-------|
| `space-0` | 0 | No gap |
| `space-xs` | 4px | Tight related elements (icon+label) |
| `space-sm` | 8px | Related elements (label+value, bullet+text) |
| `space-md` | 16px | Standard paragraph/group gap |
| `space-lg` | 24px | Section separation within slide |
| `space-xl` | 32px | Major block separation |
| `space-2xl` | 48px | Slide-level margins (with safe area) |
| `space-3xl` | 64px | Section divider breathing room |

**Rule:** All spacing MUST use tokens — no arbitrary pixel values.

## Safe Margins

| Aspect Ratio | Safe Margin (all sides) | Content Width | Content Height |
|--------------|------------------------|---------------|----------------|
| 16:9 | 48px (space-2xl) | 1200px | 675px |
| 4:3 | 48px (space-2xl) | 960px | 720px |
| Custom | 5% of shorter dimension | Calculated | Calculated |

**MUST NOT** place essential content outside safe margins.

## Grid Gutters

- **Column gutter:** `space-md` (16px) default
- **Row gutter:** `space-md` (16px) default
- **Nested grids:** Inherit parent gutter or `space-sm`

## Proximity & Grouping Rules

### Small Gap = Related Elements
- Label + value: `space-xs` (4px)
- Bullet + text: `space-sm` (8px)
- Chart axis label + axis: `space-sm` (8px)
- Diagram box + label: `space-xs` (4px)

### Large Gap = Separate Groups
- Unrelated content blocks: `space-lg` (24px) minimum
- Section header + content: `space-md` (16px)
- Multiple charts on one slide: `space-xl` (32px)

## Alignment Rules

- **MUST** align to grid columns/rows — no arbitrary positioning
- **MUST** use alignment anchors: left, center, right, top, bottom, baseline
- **SHOULD** default to left-align for LTR languages (strongest reading anchor)
- **MUST** maintain consistent baseline alignment for text in same row

## Anti-Patterns (MUST PREVENT)

| Anti-Pattern | Detection | Correction |
|--------------|-----------|------------|
| Accidental tangencies | Elements touch or near-touch without intent | Enforce minimum `space-xs` between unrelated |
| Overlaps | z-order collision, clipping | Layout engine validates no overlaps in safe area |
| Floating labels | Label not visually connected to element | Enforce proximity: label within `space-sm` of target |
| Inconsistent margins | Left margin varies across slides | Grid system enforces consistent safe margins |
| Alignment drift | Elements visually "off" by few pixels | Snap-to-grid; design system tokens only |

## Whitespace Principles

- **Whitespace is active design** — not empty space
- **Generous whitespace** around primary focal point increases perceived importance
- **Consistent whitespace** creates rhythm and professionalism
- **MUST NOT** fill whitespace decoratively

## Responsive Spacing

| Content Density | Margin | Gutter | Block Gap |
|-----------------|--------|--------|-----------|
| Sparse | `space-2xl` | `space-md` | `space-xl` |
| Normal | `space-2xl` | `space-md` | `space-lg` |
| Dense | `space-xl` | `space-sm` | `space-md` |

**Rule:** Density variant selected by responsive-layout layer based on content volume.

## Handoff to Other Layers

- **Grids layer** consumes spacing tokens for column/row/gutter definitions
- **Composition layer** uses proximity rules for grouping
- **Responsive-layout** selects density variant
- **Evaluation** checks: token compliance, safe margins, no overlaps, consistent alignment