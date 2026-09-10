# Stage 5 Reasoning Layer — Index

## Overview

This directory contains the six reasoning modules that transform a presentation request into a structured `PresentationPlan`.

## Module Execution Order

```text
1. classify_request      → request + context
2. determine_audience    → audience
3. determine_objective   → objective
4. classify_presentation → classification  (uses audience + objective)
5. select_narrative      → narrative       (uses classification + objective + audience)
6. select_slide_type     → slides[]        (uses narrative + global_strategy)
7. select_visualization  → slides[].evidence.visual_representation (refines slides)
```

## Module Contracts

| Module | Input | Output | Contract File |
|--------|-------|--------|---------------|
| classify_request | Raw request + supplied context | request, context, missing_context, normalized_input | `classify_request/reasoning.md` |
| determine_audience | Request, context, classification_hint | audience, assumptions, clarifications | `determine_audience/reasoning.md` |
| determine_objective | Request, context, audience | objective, assumptions, clarifications | `determine_objective/reasoning.md` |
| classify_presentation | Audience, objective, context, normalized_input | classification, assumptions, clarifications | `classify_presentation/reasoning.md` |
| select_narrative | Objective, audience, classification, context | narrative, assumptions, clarifications | `select_narrative/reasoning.md` |
| select_slide_type | Narrative, global_strategy | slides[], assumptions, clarifications | `select_slide_type/reasoning.md` |
| select_visualization | Slides, available_data, global_strategy | Updated slides[], assumptions, clarifications | `select_visualization/reasoning.md` |

## Shared Types

All modules reference types defined in `presentation-plan.md` at repository root.

## Knowledge Consumption

Each module consumes specific Stage 4 knowledge:

| Module | Knowledge Files |
|--------|----------------|
| classify_request | `knowledge/universal/presentation-principles.md` (input contract, pipeline) |
| determine_audience | `knowledge/universal/presentation-principles.md`, `knowledge/presentation_types/*.md`, `knowledge/storytelling/narrative-patterns.md` |
| determine_objective | `knowledge/universal/presentation-principles.md`, `knowledge/presentation_types/*.md`, `knowledge/storytelling/narrative-patterns.md` |
| classify_presentation | `knowledge/presentation_types/*.md`, `knowledge/storytelling/narrative-patterns.md`, `knowledge/universal/presentation-principles.md`, `PRESENTATION_CONSTITUTION.md` |
| select_narrative | `knowledge/storytelling/narrative-patterns.md`, `knowledge/storytelling/*.md`, `knowledge/presentation_types/*.md` |
| select_slide_type | `knowledge/layout/slide-types.md`, `knowledge/visualization/*.md`, `knowledge/storytelling/*.md` |
| select_visualization | `knowledge/visualization/chart-selection.md`, `knowledge/visualization/diagrams.md`, `knowledge/visualization/tables.md`, `knowledge/visualization/data-storytelling.md` |

## Integration Rules

1. **Sequential Dependency:** Each module receives outputs from previous modules
2. **No Backward Override:** Later modules MUST NOT silently override earlier semantic decisions
3. **Assumption Propagation:** Assumptions and clarifications accumulate across modules
4. **Confidence Tracking:** Each decision includes confidence; low confidence → clarification
5. **Conservative Defaults:** When uncertain, prefer safe defaults (assertion_evidence, normal density) and flag assumptions

## Output Aggregation

After all modules execute, the reasoning layer assembles the complete `PresentationPlan`:

```json
{
  "request": { ... },
  "context": { ... },
  "audience": { ... },
  "objective": { ... },
  "classification": { ... },
  "narrative": { ... },
  "global_strategy": { ... },
  "slides": [ ... ],
  "assumptions": [ ... ],           // Aggregated from all modules
  "clarification_requirements": [ ... ]  // Aggregated from all modules
}
```

## Validation Checklist

Before handing to Stage 6 Generation:

- [ ] `audience` and `objective` populated before `classification`
- [ ] `classification` before `narrative`
- [ ] `narrative` before `slides`
- [ ] Classification is multi-dimensional (primary_type + secondary_types + expertise + balance + evidence_burden + action + delivery_mode)
- [ ] Each slide has `intent.key_message` (declarative)
- [ ] Each substantive slide has `evidence.required: true`
- [ ] Each evidence slide has `visual_representation.preferred`
- [ ] `archetype` selected AFTER `intent` and `evidence.visual_representation`
- [ ] All assumptions recorded with risk_if_wrong
- [ ] All material unknowns in clarification_requirements
- [ ] No fabricated evidence in source_requirements
- [ ] Slide sequence matches narrative.structure

## Handoff to Generation (Stage 6)

Generation receives the complete `PresentationPlan` and is responsible for:
- Physical layout (grid, coordinates)
- Typography styling (font, size, weight, color)
- Chart/diagram rendering
- PPTX production

Generation MUST NOT alter semantic intent.

## Test Scenarios

Per `PRESENTATION_CONSTITUTION.md` Stage 5 validation:

1. **Executive Decision** — Board approval, pyramid/executive_decision, recommendation archetype
2. **Technical Architecture** — Engineering audience, assertion_evidence, architecture diagrams
3. **Educational Learning** — Novice audience, educational_journey, concept→mechanism→example→application
4. **Research with Uncertainty** — Research pattern, data/interpretation separation, uncertainty visualization
5. **Ambiguous Request** — "Make me a professional PPT about AI" → Clarifications for audience, objective, type