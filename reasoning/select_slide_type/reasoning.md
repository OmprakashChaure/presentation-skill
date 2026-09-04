# Select Slide Type — Reasoning Contract

## Purpose

Select the semantic slide archetype for each slide intent after narrative structure is defined.

## Input

```json
{
  "narrative": { ... },
  "slides_intent": [                   // From narrative.structure expanded
    {
      "stage": "string",
      "description": "string",
      "key_messages": ["string"],
      "evidence_needed": "string",
      "visual_hint": "string|null"
    }
  ],
  "global_strategy": { ... }
}
```

## Output

```json
{
  "slides": [                          // Per PresentationPlan.slides (complete)
    { ... }
  ],
  "assumptions": [...],
  "clarification_requirements": [...]
}
```

## Procedure

### 1. Intent-to-Archetype Mapping

For each `slides_intent` entry, select archetype from `knowledge/layout/slide-types.md`:

| Narrative Stage | Intent Purpose | Default Archetype | Alternatives |
|-----------------|----------------|-------------------|--------------|
| context (pyramid/problem_solution) | orient | title (first) / agenda | section_divider |
| answer (pyramid) | assert | assertion_evidence | recommendation |
| argument (pyramid) | assert | assertion_evidence | comparison |
| evidence (pyramid) | assert | chart/data / table / diagram | case_study |
| problem | assert | assertion_evidence | comparison (problem vs target) |
| consequence | assert | assertion_evidence (KPI) | chart/data |
| root_cause | explain | process/flow / architecture | diagram |
| solution | assert | assertion_evidence | image_led (demo) |
| evidence (problem_solution) | assert | case_study / chart/data | assertion_evidence |
| implementation | explain | process/flow / timeline | table |
| next_step | decide | recommendation | assertion_evidence |
| methodology (research) | explain | process/flow / table | diagram |
| findings (research) | assert | chart/data / table | assertion_evidence |
| limitations (research) | inform | table / assertion_evidence | reference |
| concept (educational) | explain | assertion_evidence (diagram) | image_led |
| mechanism (educational) | explain | process/flow / architecture | diagram |
| example (educational) | assert | case_study / image_led | assertion_evidence |
| application (educational) | decide | assertion_evidence (exercise) | comparison |
| chronological phases | inform | timeline/milestone | process/flow |
| comparison criteria | compare | comparison | table |
| option profiles | inform | assertion_evidence / image_led | table |
| executive summary | assert | assertion_evidence (pyramid summary) | recommendation |
| risks | inform | table / comparison | assertion_evidence |

### 2. Archetype Selection Rules

**Primary Rule:** Archetype follows semantic intent, NOT visual preference.

**Decision Algorithm:**

```
FOR each slide_intent:
  1. Determine primary purpose: assert | compare | explain | decide | navigate | reference | orient
  2. Determine evidence type needed: data | diagram | case_study | authority | logical_proof | none
  3. Select archetype:
     IF purpose = navigate → agenda OR section_divider
     ELSE IF purpose = orient (first slide) → title
     ELSE IF purpose = orient (section) → section_divider
     ELSE IF purpose = reference → appendix/reference
     ELSE IF purpose = compare → comparison
     ELSE IF purpose = explain AND evidence_type = diagram → process/flow OR architecture
     ELSE IF purpose = explain AND evidence_type = data → chart/data
     ELSE IF purpose = assert AND evidence_type = case_study → case_study
     ELSE IF purpose = assert AND evidence_type = data → chart/data
     ELSE IF purpose = assert AND evidence_type = diagram → architecture
     ELSE IF purpose = assert AND evidence_type = authority → quote/testimonial
     ELSE IF purpose = decide → recommendation
     ELSE → assertion_evidence (default for assert with evidence)
```

### 3. Evidence & Visual Representation Binding

For each slide, populate `evidence.visual_representation`:

| Archetype | Preferred Visual | Annotation Requirements |
|-----------|------------------|------------------------|
| assertion_evidence | Per chart-selection.md | Direct labels, insight callout, source |
| comparison | Table / Grouped bar / Dot plot | Criteria labels, highlight recommended |
| process/flow | Flow diagram (orthogonal) | Step labels, decision logic, swimlanes |
| architecture | C4 diagram (level-appropriate) | Component names, protocols, boundaries |
| timeline/milestone | Horizontal timeline (proportional) | Phase bands, milestone labels, status |
| chart/data | Per chart-selection.md | Direct labels, uncertainty, source |
| table | Styled table | Headers, units, alignment, emphasis |
| case_study | KPI tiles + quote/logo | Metric labels, customer context |
| recommendation | Decision box + next step cards | Decision text, owner, date, success criteria |
| image_led | Annotated screenshot/photo | Callouts on image, assertion title |

### 4. Slide Relationships

Set `relationships` for each slide:

```json
{
  "previous": "Builds on [previous stage] by adding [specific element]",
  "next": "Sets up [next stage] by establishing [key premise]",
  "narrative_stage": "[stage from narrative.structure]"
}
```

### 5. Layout Hints

Set `layout_hints` per archetype + global_strategy.density_target:

| Archetype | Density Preference | Emphasis | Build Steps |
|-----------|-------------------|----------|-------------|
| title | sparse | balanced | 0 |
| section_divider | sparse | balanced | 0 |
| agenda | normal | balanced | 1 (progressive) |
| assertion_evidence | normal | assertion | 1–2 |
| comparison | normal | balanced | 1 |
| process/flow | normal | balanced | 2–4 |
| architecture | dense | balanced | 2–3 |
| timeline | normal | balanced | 1 |
| chart/data | normal | evidence | 1 |
| table | dense | balanced | 0 |
| KPI | sparse | balanced | 0 |
| case_study | normal | balanced | 0 |
| recommendation | sparse | assertion | 0 |
| conclusion | sparse | balanced | 0 |

### 6. Constraints

Set `constraints`:
- `must_include`: Required by archetype (e.g., source for evidence slides)
- `must_not_include`: Prohibited by archetype (e.g., no decoration on assertion_evidence)
- `max_content_units`: Based on density_target and archetype

## Decision Rules

- **MUST** select archetype AFTER intent and evidence type are known
- **MUST** use assertion_evidence as default for assert + evidence
- **MUST** use comparison for explicit compare purpose
- **MUST** use process/flow for explain + sequential logic
- **MUST** use architecture for explain + system structure
- **MUST** use timeline for inform + temporal sequence
- **MUST NOT** use title/agenda/section_divider for substantive content
- **SHOULD** prefer chart/data over table for trend/comparison/distribution
- **SHOULD** prefer table for exact lookup, many categories, precise values

## Knowledge Consumption

- `knowledge/layout/slide-types.md` — Archetype definitions, hierarchy, failure modes
- `knowledge/visualization/chart-selection.md` — Visual representation for data
- `knowledge/visualization/diagrams.md` — Diagram types for explain
- `knowledge/visualization/tables.md` — When to use tables
- `knowledge/storytelling/*.md` — Stage-to-purpose mapping

## Clarification Triggers

Generate clarification when:
- Intent purpose ambiguous → "Is this slide meant to [assert/compare/explain]?"
- Evidence type unknown → "What evidence supports this point? (data, diagram, case study)"
- Archetype conflict → "This could be [A] or [B]. Which better serves the message?"