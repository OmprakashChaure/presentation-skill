# Classify Request — Reasoning Contract

## Purpose

Normalize the user request and extract structured context for downstream reasoning.

## Input

```json
{
  "raw_request": "string",
  "conversation_history": ["string"],  // Previous turns if multi-turn
  "supplied_context": {                // Optional pre-provided context
    "topic": "string|null",
    "audience": "string|null",
    "objective": "string|null",
    "constraints": "object|null",
    "assets": "object|null"
  }
}
```

## Output

```json
{
  "request": { ... },                  // Per PresentationPlan.request
  "context": { ... },                  // Per PresentationPlan.context
  "missing_context": ["string"],       // Context fields not inferrable
  "inferred_context": {                // Low-risk inferences made
    "field": "value",
    "confidence": "float",
    "reasoning": "string"
  }
}
```

## Procedure

### 1. Request Normalization

- Extract core topic from raw request
- Identify request type: `create | revise | extend | analyze`
- Parse explicit constraints (slide count, aspect ratio, duration, language, brand)
- Normalize to structured `request` object

### 2. Context Extraction

From request + supplied_context, populate:

| Field | Extraction Method |
|-------|-------------------|
| `topic` | Explicit in request or first noun phrase |
| `delivery_mode` | Keywords: "present", "send", "meeting", "email", "record" |
| `venue` | Keywords: "board", "conference", "zoom", "teams", "email" |
| `available_data` | References to "data", "metrics", "report", "dashboard", "file" |
| `supplied_assets` | References to "slides", "images", "charts", "diagrams", "documents" |
| `references` | Citations, URLs, DOIs mentioned |

### 3. Inference Rules (Low-Risk Only)

| Field | Inference Trigger | Inferred Value | Confidence |
|-------|-------------------|----------------|------------|
| `delivery_mode` | "board meeting", "steering committee" | `live` | 0.9 |
| `delivery_mode` | "send deck", "email", "pre-read" | `distributed` | 0.85 |
| `venue` | "board" | `boardroom` | 0.9 |
| `venue` | "conference", "keynote" | `conference` | 0.85 |
| `aspect_ratio` | Not specified | `16:9` | 0.95 |
| `language` | Not specified | Request language | 0.99 |
| `evidence_burden` | "investor", "board", "regulatory" | `high` | 0.8 |

### 4. Missing Context Identification

Flag as `missing_context` any field that:
- Materially affects downstream decisions (audience, objective, classification)
- Cannot be inferred with ≥0.8 confidence
- Is required for narrative/slide planning

### 5. Existing Deck Handling (Revise/Extend)

If `request_type` ∈ {revise, extend}:
- Parse `existing_deck` structure
- Identify: current narrative, slide count, archetypes used, evidence gaps
- Set `context.existing_deck` with parsed representation

## Decision Rules

- **MUST** extract explicit constraints before inferring defaults
- **MUST NOT** infer audience or objective — these go to dedicated modules
- **SHOULD** infer delivery_mode/venue from keywords with ≥0.8 confidence
- **MUST** record all inferences in `inferred_context` with confidence
- **MUST** flag missing context that blocks classification/narrative

## Knowledge Consumption

- `knowledge/universal/presentation-principles.md` — Input contract, canonical pipeline
- `knowledge/presentation_types/*.md` — Keywords for type hints

## Error Handling

- If raw_request is empty/vague → Return `missing_context: ["topic", "audience", "objective"]` with clarification requirements
- If contradictory constraints → Flag conflict, use most specific