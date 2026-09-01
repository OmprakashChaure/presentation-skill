# Presentation Constitution

## Purpose

This document is the authoritative specification governing the presentation-skill project. It defines how an AI presentation system must think about and create professional PowerPoint presentations.

This constitution converts research and evidence synthesis into durable, implementation-independent rules. It governs all layers:

- knowledge/
- reasoning/
- generation/
- evaluation/

This is NOT a PowerPoint tutorial. It is NOT implementation code. It is the governing policy layer for an AI presentation skill.

---

## Priority Hierarchy

When requirements conflict, the higher-priority requirement wins unless the user explicitly changes the constraint and the resulting output remains technically and communicatively valid.

1. **Truthfulness and factual integrity**
2. **User objective and hard constraints**
3. **Audience comprehension and decision usefulness**
4. **Narrative coherence**
5. **Accessibility and readability**
6. **Visual hierarchy and information clarity**
7. **Brand/design consistency**
8. **Aesthetic enhancement**
9. **Decorative novelty**

---

## Non-Negotiable Principles

- **Audience before design** — Every decision must serve the audience's understanding and decision needs
- **Objective before layout** — Slide structure follows communication intent, not template availability
- **Semantic intent before visual styling** — Meaning determines form; styling never precedes semantic reasoning
- **Truth before persuasion** — Factual integrity supersedes persuasive technique
- **Evidence must support claims** — Every substantive assertion requires appropriate evidence
- **One dominant communication job per substantive slide** — A slide communicates one primary message
- **Visuals must communicate meaning** — Decorative elements that carry no information are prohibited
- **Accessibility is part of generation** — Not a post-generation checklist
- **Content density must be managed** — Cognitive load is a design constraint
- **Design consistency must be systematic** — Not achieved through manual repetition
- **Rendering must be inspected** — Generated PPTX quality is not determined merely by successful file export
- **Generated PPTX quality requires validation** — Export success ≠ communication success

---

## Canonical Pipeline

The AI must follow this process:

```
request
→ context
→ audience
→ objective
→ presentation classification
→ narrative
→ slide intent
→ assertion/message
→ evidence
→ visual representation
→ layout
→ styling
→ generation
→ rendering
→ evaluation
→ correction
```

Later repository layers implement this pipeline. Visual styling MUST NOT precede semantic reasoning.

---

## Input Contract

The AI must extract or infer the following from a presentation request:

### Required Information
- **topic** — Subject matter
- **audience** — Who will view this (role, expertise, context)
- **objective** — What the presentation must achieve
- **desired outcome** — Specific audience action or decision
- **presentation type** — Primary classification (educational, technical, research, executive, investor, sales, marketing)

### Contextual Information
- **delivery context** — Live, distributed, hybrid, recorded
- **duration** — Time available
- **slide-count constraint** — Hard or soft limit
- **aspect ratio** — 16:9, 4:3, custom
- **language** — Primary and any secondary languages
- **brand requirements** — Logo, colours, fonts, templates
- **available data** — Datasets, metrics, evidence sources
- **sources** — Citations, references, data provenance
- **supplied assets** — Images, diagrams, charts provided by user
- **output/editability requirements** — PPTX, PDF, editable vs locked

### Inference vs. Clarification
- **Infer** when context strongly implies a value (e.g., executive audience → executive presentation type)
- **Ask** when ambiguity materially affects narrative, evidence burden, or design decisions
- **Default** to conservative assumptions when user cannot clarify

---

## Presentation Classification

Classification is multi-dimensional. The AI must determine:

- **Primary presentation type** — Educational, technical, research, executive, investor, sales, marketing
- **Secondary purpose** — Additional goals (e.g., executive + decision)
- **Audience expertise** — Novice, practitioner, expert, mixed
- **Persuasion/information balance** — Pure information to pure persuasion
- **Evidence burden** — Low (opinion), medium (industry standard), high (scientific/regulatory)
- **Expected audience action** — Decide, learn, approve, invest, buy, align
- **Delivery mode** — Presented, read, hybrid

A presentation MAY combine multiple types. The primary type governs default narrative and evidence policies; secondary types modify specific sections.

---

## Narrative Policy

Narrative selection is based on:

- **Objective** — What the presentation must achieve
- **Audience** — Expertise, expectations, decision context
- **Information dependency** — How ideas build on each other
- **Decision context** — Whether audience must decide, learn, or align

### Applicable Structures

| Structure | Best For |
|-----------|----------|
| Pyramid | Executive, decision, recommendation, synthesis |
| Assertion-Evidence | Technical, scientific, educational, analytical |
| Problem-Solution | Sales, technical proposals, strategy, product |
| Chronological | History, milestones, incidents, experiments, project phases |
| Comparison | Evaluation, vendor selection, trade-off analysis |
| Research | Academic, scientific, market research |
| Educational Learning Journey | Training, onboarding, skill building |
| Executive Decision | Board, steering committee, leadership |
| Transformation/Change | Change management, reorganization, migration |

**Rule:** Do not force one narrative structure onto every presentation. Match structure to communication job.

---

## Slide Policy

Before layout, each substantive slide MUST have:

- **purpose** — Communication job (assert, compare, explain, decide, navigate)
- **key message/assertion** — The one thing audience must take away
- **supporting evidence** — Data, reasoning, examples, authority
- **audience takeaway** — What changes in audience understanding
- **visual representation** — Chart, diagram, table, image, or text layout
- **source requirements** — Citations, data provenance, assumptions
- **relationship to neighbouring slides** — How it connects to previous/next

**Rule:** Slide titles SHOULD normally communicate the slide's message rather than merely naming its topic.

---

## Assertion-Evidence Policy

Assertion-evidence is a STRONG DEFAULT for substantive slides in:

- Technical presentations
- Scientific presentations
- Educational presentations
- Analytical presentations

When evidence exists.

### Structure

```
ASSERTION (declarative slide title)
+
EVIDENCE (visual + annotation)
+
IMPLICATION (so what?)
```

### Do NOT Force On

- Title slides
- Agenda slides
- Section dividers
- Navigation slides
- Reference/appendix slides

### Critical Distinction

**Decorative imagery is NOT evidence.** Evidence must directly support the assertion.

---

## Content Policy

### Prohibited

- Fabricated facts
- Fabricated statistics
- Fabricated sources
- Fabricated quotations
- Fabricated customer evidence
- Fabricated financial metrics
- Unsupported conclusions

### Must Preserve

- Dates
- Units
- Denominators
- Scope
- Uncertainty
- Distinctions between:
  - Fact
  - Inference
  - Recommendation
  - Assumption

### Source Integrity

Every claim requiring evidence MUST have a traceable source. If source is unavailable, the claim MUST be marked as assumption or removed.

---

## Visualization Policy

Visualization selection follows the information relationship the audience needs to understand.

### Default Mapping

| Relationship | Default Visualization |
|--------------|----------------------|
| Trend over time | Line chart, time-series |
| Comparison | Bar/column/dot chart |
| Ranking | Ordered bar/dot chart |
| Distribution | Histogram, box plot, violin plot |
| Relationship/correlation | Scatter plot, relational chart |
| Exact lookup | Table |
| Part-to-whole | Stacked bar, treemap, proportional area |
| Process/flow | Flow diagram, process diagram |
| Hierarchy | Tree diagram, org chart |
| Architecture | Architecture diagram, system diagram |
| Geography | Map, choropleth |

### Rules

- These are DEFAULTS, not absolute laws
- Context (audience, data scale, precision needs) may override
- **Prohibited:** Misleading visual encoding (truncated axes, 3D distortion, area encoding for 1D data, inverted scales)
- **Required:** Direct labelling over legends where feasible
- **Required:** Scale, units, denominator, timeframe, ordering, uncertainty disclosure
- **Prohibited:** Chart decoration that adds no information

---

## Layout Policy

### System Components

- **Grids** — Column/row structure with gutters
- **Safe areas** — Margins preventing clipping
- **Alignment anchors** — Consistent positioning references
- **Spacing tokens** — Systematic whitespace scale
- **Aspect ratio adaptation** — 16:9, 4:3, custom handling

### Overflow Repair Order (MUST follow sequence)

1. Remove unnecessary content
2. Rewrite for conciseness
3. Restructure (split message across slides)
4. Split slide
5. Change layout variant
6. Controlled typography reduction (last resort)

**NEVER** solve overflow by making text unreadable.

---

## Typography Policy

### Semantic Roles

| Role | Purpose |
|------|---------|
| Title | Presentation title, major section |
| Section Title | Major division within deck |
| Assertion | Slide key message (declarative) |
| Body | Supporting text, explanation |
| Label | Axis labels, callouts, annotations |
| Annotation | Evidence labels, data point callouts |
| Source/Note | Citations, assumptions, methodology |

### Rules

- **NO universal font-size number** — Sizes adapt to context
- Typography adapts to: delivery context, aspect ratio, language, font availability, content density
- Hierarchy must be visually clear (size, weight, colour, position)
- Font consistency: maximum 2 font families per deck (heading + body)
- Font availability: prefer system fonts or embedded web-safe fonts
- Multilingual: account for text expansion (typically +20-40% for non-Latin scripts)

---

## Colour Policy

### Semantic Colour Roles

| Role | Purpose |
|------|---------|
| Background | Canvas, slide background |
| Primary Text | Highest readability text |
| Secondary Text | Supporting, less prominent text |
| Accent | Primary brand/action colour |
| Status | Informational states |
| Warning | Caution, attention needed |
| Success | Positive completion/state |
| Category Colours | Distinguishing series/groups |

### Rules

- Colour MUST NOT be the sole carrier of essential meaning (redundant encoding required)
- Accessibility contrast ratios take priority over brand colour preferences
- Minimum 4.5:1 for text, 3:1 for large text and UI components (WCAG AA)
- Semantic meaning consistency: same meaning = same colour across deck
- Maximum 6-8 categorical colours (discrimination limit)
- Brand colours are subordinate to accessibility and communication clarity

---

## Accessibility Policy

### Required Where Supported

- **Meaningful slide titles** — Every slide has unique, descriptive title
- **Logical reading order** — Z-order matches visual/logical sequence
- **Useful alternative text** — Meaningful images described; decorative marked as such
- **Non-colour-only meaning** — Colour never sole carrier of essential information
- **Applicable contrast** — Text and meaningful graphics meet WCAG AA
- **Readable typography** — Sizes, spacing, fonts support readability
- **Captions/transcripts** — For embedded audio/video
- **Decorative vs. meaningful distinction** — Explicit marking

### Release Blockers

Accessibility failures affecting essential information are **release-blocking issues**. Deck must not ship with:

- Unreadable essential text
- Colour-only critical meaning
- Missing alt text on meaningful visuals
- Broken reading order for essential content

---

## Presentation Type Policy

High-level defaults that SPECIALIZE universal principles rather than contradict them.

### Educational
- Learning objectives explicit
- Prerequisite knowledge acknowledged
- Progressive explanation (concept → mechanism → example → application)
- Signalling and segmentation for cognitive load management
- Misconception handling
- Recap and reinforcement

### Technical
- Technical precision in terminology
- Architecture, mechanisms, workflows
- System diagrams with clear relationships
- Evidence for claims
- Constraints, trade-offs, failure modes
- Implementation details where relevant
- Limitations acknowledged

### Research
- Research question explicit
- Motivation and gap
- Methodology transparency
- Data and findings separated
- Uncertainty and limitations stated
- Interpretation distinguished from data
- **Prohibited:** Causal overclaiming, cherry-picking, omitted denominators, correlation≠causation confusion

### Executive
- Answer-first (pyramid)
- Implications and decision focus
- Recommendation with options and trade-offs
- Business impact quantified
- Risks acknowledged
- Next steps concrete

### Investor
- Problem → Customer → Solution → Market → Traction → Business Model → Economics → Differentiation → Risks → Projections → Ask
- **Strict distinction:** Actual metrics vs. projections vs. assumptions
- **Prohibited:** Invented traction or market data

### Sales
- Customer problem → Desired outcome → Value proposition → Solution → Evidence → Proof → Differentiation → Objections → Next action
- **Prohibited:** Feature dumping without customer value framing

### Marketing
- Target audience → Insight → Positioning → Message → Creative concept → Evidence → Channels → Call to action
- Brand constraints respected
- **Prohibited:** Disconnected creative decoration

---

## Design System Policy

Centralized design tokens for systematic consistency:

- **Typography** — Font families, sizes, weights, line heights per semantic role
- **Colours** — Semantic palette with accessibility-verified values
- **Spacing** — Token scale (xs, sm, md, lg, xl, 2xl, 3xl)
- **Margins** — Safe area definitions per aspect ratio
- **Grids** — Column counts, gutter widths, alignment anchors
- **Charts** — Default encodings, colour sequences, label styles
- **Diagrams** — Connector styles, shape conventions, label placement
- **Image treatment** — Cropping, framing, opacity, caption style
- **Source/footer conventions** — Placement, format, required fields

Slides MUST inherit the design system. Manual per-slide styling is prohibited for systematic properties.

---

## Evaluation Policy

Every generated deck MUST be evaluated across six dimensions:

1. **Content** — Factual accuracy, source integrity, claim support
2. **Storytelling** — Narrative coherence, slide-to-slide flow, objective achievement
3. **Visual Design** — Hierarchy, layout, typography, colour, clutter
4. **Accessibility** — Titles, reading order, alt text, contrast, non-colour meaning
5. **Technical/Rendering Integrity** — No clipping, overflow, font substitution issues, corruption
6. **Deck-Level Coherence** — Consistent style, narrative arc, repetition for reinforcement

### Release Blockers

- Factual integrity failures
- Severe overflow/clipping
- Inaccessible essential information
- Materially misleading visualizations
- Broken reading order for critical content

---

## Revision Policy

### Cycle

```
generate
→ render
→ evaluate
→ identify highest-impact defect
→ revise
→ render again
→ evaluate again
```

### Fix Priority Order

1. Truth/content integrity
2. Objective/narrative coherence
3. Readability/accessibility
4. Visual clarity
5. Aesthetics

**Rule:** Never regenerate without evaluation. Endless regeneration without evaluation is prohibited.

---

## Anti-Patterns (Explicitly Prohibited)

- Template-first generation (layout before semantic intent)
- Bullet dumping (slides as document dumps)
- Decorative image filling (images without communication purpose)
- Random chart selection (without relationship reasoning)
- Misleading chart decoration (3D, gradients, chartjunk)
- Unsupported claims (assertions without evidence)
- Invented sources (fabricated citations)
- Tiny text (below readability threshold)
- Alignment drift (inconsistent positioning)
- Clipping (content outside safe area)
- Colour-only meaning (no redundant encoding)
- Identical layouts for unrelated purposes
- Excessive layout novelty (cognitive overhead)
- Endless regeneration without evaluation

---

## Rule Language

This constitution uses explicit operational language:

- **MUST** — Mandatory, no exceptions unless explicitly stated
- **MUST NOT** — Prohibited, no exceptions unless explicitly stated
- **SHOULD** — Strongly recommended, deviation requires justification
- **SHOULD NOT** — Strongly discouraged, deviation requires justification
- **MAY** — Permitted, optional
- **IF ... THEN** — Conditional requirement
- **EXCEPTION** — Explicitly documented exception to a rule

Vague statements that cannot guide an AI decision are prohibited.

---

## Stage Boundary

This constitution governs Stages 4-8:

- **Stage 4 (Knowledge)** — Operationalizes these principles into decision-ready knowledge files
- **Stage 5 (Reasoning)** — Implements decision procedures following this pipeline
- **Stage 6 (Generation)** — Produces PPTX following these policies
- **Stage 7 (Evaluation)** — Validates against these criteria
- **Stage 8 (Testing)** — End-to-end verification

No layer may contradict this constitution. Conflicts are resolved in favour of this document.

---

## Version

1.0 — Initial constitution