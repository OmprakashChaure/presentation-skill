# Tables

## Purpose

Define when tables are preferable and rules for table design in presentations.

## Scope

All presentation tables — data tables, comparison tables, specification tables, reference tables.

## When to Use Tables (MUST meet at least one)

| Use Case | Example |
|----------|---------|
| **Exact lookup** | Audience needs precise values (specs, pricing, config) |
| **Detailed comparison** | >3 items × >3 criteria with precise values |
| **Many categories** | >8 rows where chart would be cluttered |
| **Precise values required** | Financials, technical specs, regulatory data |
| **Mixed data types** | Text + Numbers + Status + Links in one view |
| **Appendix/reference** | Full data for verification |

## When NOT to Use Tables

| Situation | Better Alternative |
|-----------|-------------------|
| Showing trend | Line chart |
| Simple comparison (≤5 items) | Bar chart |
| Part-to-whole | Stacked bar / Treemap |
| Distribution | Histogram / Box plot |
| Relationship | Scatter plot |

## Table Design Rules

### Structure

- **Headers:** Clear, descriptive, include units
- **Header row:** Visually distinct (bold, background, border)
- **First column:** Row identifiers (what each row represents)
- **Alignment:** Numbers right-aligned; Text left-aligned; Headers match data

### Numeric Formatting

- **Consistent decimal precision:** Same decimals per column (not per cell)
- **Units in header:** Not in every cell
- **Thousands separators:** 1,234 (not 1234)
- **Negative:** Parentheses (1,234) or minus −1,234 — consistent
- **Missing data:** En dash (–) or "N/A" — not blank, not zero

### Selective Emphasis

- **Purpose:** Guide eye to key comparisons
- **Methods (max 1 per table):**
  - Bold: Top/bottom value per column
  - Background tint: Target met/missed (semantic colour)
  - Icon: ▲▼ for direction
- **Rule:** Emphasis MUST serve the slide assertion

### Density Variants

| Variant | Row Height | Font | Use Case |
|---------|------------|------|----------|
| **Comfortable** | 32px | `body` | Main deck, projected |
| **Compact** | 24px | `label` | Appendix, dense reference |
| **Minimal** | 20px | `caption` | Dense appendix only |

**Rule:** Default = Comfortable. Compact only when necessary.

### Pagination/Splitting

- **Max rows per slide:** 12–15 (comfortable), 20 (compact)
- **Split strategy:** Logical groups (by category, segment, time)
- **Continuation:** "Table 1 (cont.)" with repeated headers

## Comparison Table Specifics

- **Criteria as rows, Options as columns** (easier to scan down)
- **Checkmarks/Icons:** For boolean criteria (✓/✗/Partial)
- **Scoring:** Only if methodology disclosed
- **Highlight:** Recommended option (subtle background)

## Specification Table Specifics

- **Parameter | Value | Unit | Constraint/Note**
- **Group:** Related parameters with sub-headers
- **Links:** Reference to detailed doc (if digital)

## Anti-Patterns

- Spreadsheet dump (all columns, no curation)
- Left-aligned numbers (hard to compare magnitudes)
- Inconsistent decimals (1.2 vs 1.234 vs 1.200)
- Units in every cell (clutter)
- No header distinction
- Tiny font to fit (use split/appendix instead)
- Colour-only highlighting (accessibility)
- Merged cells (breaks sorting/accessibility)

## Handoff to Other Layers

- **Reasoning:** Chooses table when exact lookup/comparison needed
- **Chart-selection:** Tables for exact lookup; charts for relationships
- **Slide-types:** Table slide archetype
- **Responsive-layout:** Density variant selection
- **Evaluation:** Checks: Headers, alignment, precision, units, emphasis purpose, density, accessibility