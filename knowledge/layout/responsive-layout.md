# Responsive Layout

## Purpose

Define how layouts respond to content length, language, multilingual expansion, aspect ratio, font substitution, dense/sparse content.

## Content Density Variants

| Variant | Trigger | Margins | Gutters | Block Gap | Typography | Max Content |
|---------|---------|---------|---------|-----------|------------|-------------|
| **Sparse** | <30% content fill | space-2xl | space-md | space-xl | Normal tokens | Minimal — title + 1 visual |
| **Normal** | 30–70% fill | space-2xl | space-md | space-lg | Normal tokens | Standard — assertion + evidence |
| **Dense** | >70% fill | space-xl | space-sm | space-md | Compact tokens (↓1 step) | Heavy — comparison table, detailed diagram |

**Selection:** Automatic based on content volume analysis per slide.

## Overflow Repair Sequence (MUST Follow Order)

```
1. REMOVE unnecessary content
   - Cut fluff, redundant words, decorative elements
   - Merge duplicate information
   
2. REWRITE for conciseness
   - Active voice, eliminate hedging, combine sentences
   - "In order to" → "To"; "Due to the fact that" → "Because"
   
3. RESTRUCTURE (split message)
   - One assertion → Two slides (assertion + evidence separate)
   - Complex comparison → Criteria slide + Detail slide
   
4. SPLIT slide
   - Duplicate slide, divide content logically
   - Add "(cont.)" or part numbers
   
5. CHANGE layout variant
   - Normal → Dense (smaller margins, tighter gutters)
   - Two-column → Single-column stack
   - Side-by-side → Tabbed/Accordion (if interactive)
   
6. CONTROLLED TYPOGRAPHY REDUCTION (LAST RESORT)
   - Reduce by MAX 1 token step (body → label, h2 → h3)
   - NEVER below caption token
   - NEVER reduce assertion/title — rewrite or split instead
```

**NEVER** allow automatic expansion to create collisions or clipping.

## Multilingual Expansion

| Script | Expansion Factor | Adaptations |
|--------|------------------|-------------|
| **Latin (EN, ES, FR, DE)** | 1.0× (baseline) | Normal tokens |
| **CJK (ZH, JA, KO)** | 1.2–1.5× chars, same width | Line height +20%; font fallback; same token sizes |
| **Arabic/Hebrew (RTL)** | 1.2–1.3× | Mirror layout (not just text); RTL grid; font fallback |
| **Devanagari/Indic** | 1.3–1.5× | Line height +30%; conjunct handling; font fallback |
| **Thai/Vietnamese** | 1.2× | Line height +20%; tone marks; font fallback |

### RTL Layout Mirroring

- **Grid:** Columns mirror (Col 1 ↔ Col 12)
- **Alignment:** Left ↔ Right, Start ↔ End
- **Reading Path:** Top-right → Top-left → Bottom-right → Bottom-left
- **Icons/Arrows:** Directional icons mirrored (→ becomes ←)
- **Numbers:** Stay LTR (Arabic-Indic digits if locale)

## Aspect Ratio Adaptation

| Change | Strategy |
|--------|----------|
| **16:9 → 4:3** | Stack horizontal zones vertically; 12-col → 8-col; margins space-2xl → space-xl |
| **4:3 → 16:9** | Distribute horizontal; 8-col → 12-col; margins space-xl → space-2xl |
| **Custom → Standard** | Recalculate grid; preserve relative proportions; reflow zones |

**Rule:** Content reflows — never stretches. Aspect ratio change triggers layout variant recalculation.

## Font Substitution Handling

| Scenario | Response |
|----------|----------|
| **Primary font unavailable** | Fallback to system font stack (defined in design system) |
| **Fallback changes metrics** | Recalculate layout: measure text bounds → reflow if overflow |
| **Embedded font fails** | Use system fallback; log warning; validate readability |
| **Variable font unsupported** | Use static weight instances; same token sizes |

**Rule:** Design system defines font stacks per script with measured fallbacks.

## Density Variant Details

### Sparse Variant
- **Use:** Title slides, Section dividers, KPI dashboard (few metrics)
- **Whitespace:** Generous — focal point isolation
- **Typography:** Normal or display tokens
- **Risk:** Can feel empty — add meaningful visual or increase focal size

### Normal Variant
- **Use:** Standard assertion-evidence, Comparison, Process
- **Whitespace:** Balanced — rhythm and grouping clear
- **Typography:** Normal tokens
- **Default:** Target for most slides

### Dense Variant
- **Use:** Detailed tables, Complex diagrams, Appendix, Technical specs
- **Whitespace:** Compressed — space-sm gutters, space-md block gaps
- **Typography:** Compact tokens (body→label, h3→body, etc.)
- **Limit:** Not for projected slides; readable only at close range

## Collision Prevention

- **Pre-layout validation:** Measure all content bounds before placement
- **Constraint solver:** If collision detected → escalate repair sequence
- **Minimum clearances:** space-xs (4px) between unrelated elements
- **Safe zone enforcement:** Hard constraint — no essential content outside

## Handoff to Other Layers

- **Typography:** Provides token scaling per density variant
- **Grids:** Provides margin/gutter adjustments per variant
- **Composition:** Adapts focal point, grouping, balance per variant
- **Slide-types:** Defines density thresholds per archetype
- **Generation:** Executes repair sequence; produces variant-specific PPTX
- **Evaluation:** Checks: No collisions, No clipping, Token compliance, Readable at target density, RTL correctness