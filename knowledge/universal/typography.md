# Typography

## Purpose

Define the typography system for presentation slides — semantic roles, hierarchy, readability rules, and overflow handling.

## Scope

All text elements in all presentations.

## Semantic Roles

| Role | Purpose | Typical Usage |
|------|---------|---------------|
| Title | Presentation title, major section | Slide 1, section dividers |
| Section Title | Major division within deck | Section divider slides |
| Assertion | Slide key message (declarative) | Substantive slide titles |
| Body | Supporting text, explanation | Bullet points, paragraphs |
| Label | Axis labels, callouts, annotations | Chart axes, diagram labels |
| Annotation | Evidence labels, data point callouts | Direct labels on charts, callout boxes |
| Source/Note | Citations, assumptions, methodology | Bottom of slide, footnotes |

## Hierarchy Rules

### Visual Hierarchy (MUST be distinguishable)

1. **Title** > **Section Title** > **Assertion** > **Body** > **Label** ≥ **Annotation** > **Source/Note**
2. Differentiation via: size, weight, colour, case (Title Case vs. Sentence case)
3. **Minimum 3 distinct levels** between Title and Source/Note

### Sizing (NO Universal Fixed Sizes)

- Sizes are **relative tokens** in the design system: `display`, `h1`, `h2`, `h3`, `body`, `label`, `annotation`, `caption`
- Actual point values adapt to: aspect ratio, delivery context, language, content density
- **Example token mapping (16:9, projected):**
  - display: 44pt, h1: 36pt, h2: 28pt, h3: 24pt, body: 18pt, label: 14pt, annotation: 12pt, caption: 11pt
- **Example token mapping (16:9, dense/read):**
  - display: 36pt, h1: 28pt, h2: 22pt, h3: 18pt, body: 14pt, label: 11pt, annotation: 10pt, caption: 9pt

## Readability Rules

- **Line length:** 45–75 characters (including spaces) for body text
- **Line height:** 1.3–1.5 for body; 1.1–1.2 for headings
- **Paragraph spacing:** 0.5–1.0 line height between paragraphs
- **Contrast:** Text MUST meet WCAG AA (4.5:1 normal, 3:1 large)
- **Font choice:** Maximum 2 font families per deck (heading + body)
- **Font availability:** Prefer system fonts or embedded web-safe fonts; MUST verify rendering

## Font Consistency

- **MUST** use design system tokens — no manual per-slide font sizing
- **MUST NOT** mix more than 2 font families
- **SHOULD** use same font family for all body text across deck
- **SHOULD** use weight variants (Regular, Medium, Semibold, Bold) not different fonts for hierarchy

## Multilingual Considerations

- **Text expansion:** Plan for +20–40% character count for non-Latin scripts (CJK, Arabic, Devanagari)
- **Line height:** Increase for complex scripts
- **Font fallback:** Define fallback stacks per script
- **Direction:** Support RTL (Arabic, Hebrew) — mirror layout, not just text
- **Token adaptation:** Design system provides per-script size adjustments

## Overflow Handling

### Repair Order (MUST follow sequence)

1. **Remove unnecessary content** — Cut fluff, redundant words, decorative text
2. **Rewrite for conciseness** — Active voice, shorter sentences, eliminate hedging
3. **Restructure** — Split message across 2+ slides (e.g., assertion + evidence separate)
4. **Split slide** — One message → two slides with clear continuation
5. **Change layout variant** — Switch to dense-content layout (smaller margins, tighter spacing)
6. **Controlled typography reduction** — Reduce by MAX 1 token step (e.g., body → label)

**NEVER** reduce below `caption` (minimum readable size).
**NEVER** reduce assertion/title size — rewrite or split instead.

## Anti-Patterns

- Shrinking text to fit (without trying steps 1–5 first)
- Mixing 3+ font families
- Using decorative/script fonts for body text
- All-caps for body text (reduces readability)
- Justified text (creates rivers, hurts readability)
- Font sizes below 9pt (projected) / 11pt (read)

## Handoff to Other Layers

- **Design system** defines token values per context
- **Responsive-layout** selects variant and applies token scaling
- **Composition** uses typography hierarchy for visual weight
- **Evaluation** checks: hierarchy distinguishable, contrast, overflow, readability