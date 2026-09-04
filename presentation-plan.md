# PresentationPlan Contract

## Purpose

Define the structured output of Stage 5 reasoning — the semantic contract between reasoning and generation.

## Overview

```
PresentationPlan
├── request                    # Original user request (normalized)
├── context                    # Extracted + inferred context
├── audience                   # Audience model
├── objective                  # Presentation objective
├── classification             # Multi-dimensional classification
├── narrative                  # Selected narrative structure
├── global_strategy            # Cross-slide strategic decisions
├── slides[]                   # Ordered slide intents
├── assumptions[]              # Material assumptions made
└── clarification_requirements[] # Questions for user
```

---

## 1. Request

```json
{
  "raw": "string",                    // Original user input
  "normalized": "string",             // Cleaned, structured request
  "request_type": "enum",             // create | revise | extend | analyze
  "constraints": {                    // Hard constraints from request
    "max_slides": "integer|null",
    "aspect_ratio": "16:9 | 4:3 | custom",
    "duration_minutes": "integer|null",
    "language": "string",
    "brand_requirements": "object|null",
    "template_locked": "boolean"
  }
}
```

---

## 2. Context

```json
{
  "topic": "string",
  "delivery_mode": "live | distributed | hybrid | recorded",
  "venue": "conference | boardroom | virtual | email | unknown",
  "available_data": [
    {
      "description": "string",
      "format": "csv | json | spreadsheet | database | api | document",
      "access": "provided | referenced | needs_collection",
      "provenance": "string"
    }
  ],
  "supplied_assets": [
    {
      "type": "image | diagram | chart | document | video",
      "description": "string",
      "path_or_ref": "string"
    }
  ],
  "references": [
    {
      "citation": "string",
      "url_or_doi": "string|null",
      "access_date": "date"
    }
  ],
  "existing_deck": "object|null"      // If revising/extending
}
```

---

## 3. Audience

```json
{
  "primary": {
    "role": "string",                  // e.g., "C-Suite", "Engineering Leads", "Sales Team"
    "expertise_level": "novice | practitioner | expert | mixed",
    "domain_familiarity": "low | medium | high",
    "decision_authority": "decider | influencer | reviewer | learner"
  },
  "secondary": [
    {
      "role": "string",
      "expertise_level": "enum",
      "purpose": "alignment | awareness | approval"
    }
  ],
  "size": "individual | small_group | large_audience | unknown",
  "cultural_context": "string|null",
  "accessibility_needs": [
    "screen_reader | high_contrast | large_print | captions | translation | none"
  ],
  "expected_mindset": "skeptical | receptive | neutral | hostile | unknown",
  "prior_knowledge_assumed": [
    "string"  // Concepts, terms, context audience already knows
  ]
}
```

---

## 4. Objective

```json
{
  "primary": "enum",                   // decide | recommend | inform | teach | persuade | align | explore
  "secondary": ["enum"],               // Additional objectives
  "desired_outcome": "string",         // Concrete: "Approve $2M budget for Q3 initiative"
  "success_criteria": [
    "string"                           // Observable: "Board votes yes", "Team can implement design"
  ],
  "persuasion_vs_information": "float", // 0.0 = pure info, 1.0 = pure persuasion
  "evidence_burden": "low | medium | high | regulatory",
  "call_to_action": "string|null",     // Explicit ask
  "decision_deadline": "date|null"
}
```

---

## 5. Classification

```json
{
  "primary_type": "enum",              // educational | technical | research | executive | investor | sales | marketing
  "secondary_types": ["enum"],         // Additional applicable types
  "audience_expertise": "novice | practitioner | expert | mixed",
  "persuasion_balance": "float",       // 0.0–1.0 (from objective)
  "evidence_burden": "low | medium | high | regulatory",
  "expected_action": "decide | learn | approve | invest | buy | align | none",
  "delivery_mode": "presented | read | hybrid",
  "complexity": "simple | moderate | complex",
  "slide_count_estimate": "integer",   // Based on content scope
  "confidence": "float"                // 0.0–1.0 classification confidence
}
```

---

## 6. Narrative

```json
{
  "pattern": "enum",                   // pyramid | assertion_evidence | problem_solution | chronological | comparison | research | executive_decision | educational_journey | change_transformation
  "pattern_variant": "string|null",    // e.g., "compressed", "multi_problem"
  "rationale": "string",               // Why this pattern for this context
  "structure": [
    {
      "stage": "string",               // e.g., "answer", "argument_1", "evidence_1", "problem", "solution"
      "description": "string",
      "slide_count_estimate": "integer",
      "key_messages": ["string"]
    }
  ],
  "deck_level_assertion": "string|null" // Governing thought for pyramid/executive
}
```

---

## 7. Global Strategy

```json
{
  "design_system": {
    "theme": "string",                 // Theme name or "auto"
    "color_mode": "light | dark | auto",
    "font_stack": "system | brand | custom"
  },
  "density_target": "sparse | normal | dense",
  "signalling_strategy": "explicit | minimal", // Section dividers, progress indicators
  "build_strategy": "static | progressive | minimal",
  "appendix_strategy": "separate_section | inline | none",
  "localization": {
    "primary_language": "string",
    "secondary_languages": ["string"],
    "rtl_support": "boolean"
  },
  "accessibility_priority": "standard | high | maximum",
  "evidence_style": "integrated | referenced | appendix"
}
```

---

## 8. Slides (Ordered Array)

Each slide is a semantic intent — NOT a layout.

```json
{
  "slide_id": "string",                // Stable identifier: "slide_001"
  "sequence": "integer",               // 1-based order
  "archetype": "enum",                 // From knowledge/layout/slide-types.md
  "intent": {
    "purpose": "enum",                 // assert | compare | explain | decide | navigate | reference | orient
    "key_message": "string",           // The ONE thing audience must take away (declarative)
    "supporting_points": ["string"],   // 0–3 supporting points
    "audience_takeaway": "string"      // What changes in understanding
  },
  "evidence": {
    "required": "boolean",
    "type": "enum|null",               // data | diagram | case_study | authority | logical_proof | none
    "description": "string",           // What evidence should show
    "source_requirements": [
      {
        "claim": "string",
        "evidence_type": "primary_data | study | report | expert | benchmark",
        "citation_needed": "boolean",
        "data_provided": "boolean",
        "data_ref": "string|null"      // Links to context.available_data
      }
    ],
    "visual_representation": {
      "preferred": "enum|null",        // From visualization knowledge
      "alternatives": ["enum"],
      "rationale": "string",
      "annotation_requirements": ["string"]
    }
  },
  "relationships": {
    "previous": "string|null",         // How this connects to previous slide
    "next": "string|null",             // How this sets up next slide
    "narrative_stage": "string"        // From narrative.structure
  },
  "layout_hints": {
    "density_preference": "sparse | normal | dense",
    "emphasis": "assertion | evidence | balanced",
    "build_steps": "integer"           // If progressive reveal
  },
  "constraints": {
    "must_include": ["string"],        // Required elements
    "must_not_include": ["string"],    // Prohibited elements
    "max_content_units": "integer|null"
  },
  "confidence": "float"                // 0.0–1.0 confidence in this slide plan
}
```

---

## 9. Assumptions

```json
[
  {
    "id": "string",
    "assumption": "string",
    "domain": "audience | objective | data | classification | narrative | evidence | design",
    "risk_if_wrong": "low | medium | high | critical",
    "mitigation": "string",
    "clarification_id": "string|null"  // Links to clarification_requirements
  }
]
```

---

## 10. Clarification Requirements

```json
[
  {
    "id": "string",
    "question": "string",
    "domain": "audience | objective | data | classification | narrative | evidence | constraints",
    "impact_if_unresolved": "low | medium | high | critical",
    "suggested_options": ["string"],   // Options to help user answer
    "default_if_no_answer": "string|null",
    "blocks": ["slide_id"]             // Slides that cannot be finalized
  }
]
```

---

## Validation Rules

1. **Ordering:** `audience` → `objective` → `classification` → `narrative` → `slides`
2. **Completeness:** Every substantive slide has `intent.key_message` (declarative)
3. **Evidence:** Every assertion slide has `evidence.required: true` and at least one `source_requirements` entry
4. **Archetype:** `archetype` selected AFTER `intent` and `evidence.visual_representation`
4. **Traceability:** Each slide links to `narrative.structure` stage
5. **No Fabrication:** No invented data, citations, or evidence in `source_requirements.data_provided: false`
6. **Uncertainty:** All material unknowns captured in `assumptions` or `clarification_requirements`

---

## Handoff to Generation (Stage 6)

Generation receives `PresentationPlan` and produces:

- Physical slide instances with layout, typography, color
- Rendered charts, diagrams, tables
- PPTX file

Generation MUST NOT alter semantic intent (key_message, evidence requirements, narrative sequence).

---

## Handoff from Evaluation (Stage 7+)

Evaluation receives `PresentationPlan` + generated PPTX and validates:

- Content fidelity (key_message communicated?)
- Storytelling coherence (narrative followed?)
- Visual clarity (evidence readable?)
- Accessibility (requirements met?)
- Technical integrity (no overflow/clipping)