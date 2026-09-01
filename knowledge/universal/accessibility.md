# Accessibility

## Purpose

Define presentation accessibility requirements — integrated into generation, not post-hoc.

## Scope

All presentations; essential content MUST meet all requirements.

## Requirements

### 1. Meaningful Slide Titles

- **MUST:** Every slide has a unique, descriptive title
- **MUST:** Title communicates the slide's message (assertion), not just topic
- **Rule:** "Q3 Results" ❌ → "Q3 Revenue Exceeded Target by 12%" ✅
- **Evaluation:** Screen reader reads title first — must be informative

### 2. Logical Reading Order

- **MUST:** Z-order (tab order) matches visual/logical reading sequence
- **MUST:** Left-to-right, top-to-bottom for LTR languages
- **MUST:** Reading order validated after layout generation
- **Anti-pattern:** Visual position says A→B but tab order says B→A

### 3. Alternative Text

| Visual Type | Alt Text Requirement |
|-------------|---------------------|
| Meaningful chart | Full insight: "Bar chart: Revenue grew 12% YoY to $45M, driven by APAC (+28%)" |
| Meaningful diagram | Structure + key relationships: "Architecture: API Gateway routes to 3 microservices; Auth service handles 40% of traffic" |
| Meaningful image | Content description relevant to message |
| Decorative | Empty alt (alt="") — marked `role="presentation"` |
| Logo | "Company logo" (unless logo IS the message) |

**Rule:** Alt text MUST convey the same information a sighted user gets.

### 4. Decorative vs. Meaningful Visuals

- **MUST** explicitly classify every visual: `meaningful` or `decorative`
- **Default:** Assume meaningful — generator must justify decorative classification
- **Decorative examples:** Background textures, purely aesthetic icons, divider lines
- **Meaningful examples:** Charts, diagrams, product photos, screenshots, data tables

### 5. Contrast

- **MUST** meet WCAG AA for all text and meaningful graphics
- **Text:** 4.5:1 (normal), 3:1 (large ≥18pt/14pt bold)
- **Graphics:** 3:1 for essential visual elements (chart lines, diagram connectors, icons)
- **Validation:** Automated contrast check on rendered output

### 6. Non-Colour-Only Meaning

- **MUST NOT** use colour as sole carrier of essential information
- **Required redundant encodings:**
  - Status: Icon + text + colour
  - Chart series: Direct label + pattern + colour
  - Diagram state: Shape + label + colour
  - Table highlighting: Bold + background + text indicator

### 7. Readable Typography

- **MUST** follow typography.md rules (hierarchy, line length, contrast, size)
- **MUST NOT** go below `caption` token size (minimum readable)
- **MUST** support text resize up to 200% without horizontal scrolling or clipping

### 8. Captions/Transcripts

- **MUST** provide captions for embedded video
- **MUST** provide transcripts for embedded audio
- **SHOULD** provide speaker notes as transcript for recorded presentations

### 9. Focus Indicators (Interactive/Exported PDF)

- **MUST** have visible focus outline for interactive elements
- **MUST** meet 3:1 contrast for focus indicator

## Release Blockers

The following are **RELEASE-BLOCKING** — deck MUST NOT ship:

- Essential text below contrast threshold
- Essential content colour-only (no redundant encoding)
- Meaningful visual missing alt text
- Broken reading order for essential content
- Essential content clipped or outside safe area
- Slide without meaningful title

## Validation Process

1. **Automated:** Contrast, alt text presence, reading order, title uniqueness
2. **Semi-automated:** Alt text quality (semantic comparison to visual content)
3. **Manual:** Screen reader walkthrough (NVDA/JAWS/VoiceOver)

## Handoff to Other Layers

- **Generation:** Produces alt text, reading order, semantic markup
- **Typography:** Ensures minimum sizes, contrast tokens
- **Colour:** Ensures non-colour-only encodings, contrast
- **Layout:** Ensures safe margins, logical z-order
- **Evaluation:** Runs automated + semi-automated checks; flags release blockers