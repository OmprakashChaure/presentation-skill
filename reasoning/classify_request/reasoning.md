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
  },
  "normalized_input": {                // Intermediate representation
    "topic": "string|null",
    "audience": { "value": "string|null", "state": "explicit|inferred|unknown" },
    "objective": { "value": "string|null", "state": "explicit|inferred|unknown" },
    "desired_outcome": { "value": "string|null", "state": "explicit|inferred|unknown" },
    "presentation_type": { "value": "string|null", "state": "explicit|inferred|unknown" },
    "context": "object",
    "hard_constraints": "object",
    "supplied_evidence": "array",
    "supplied_assets": "array",
    "explicit_fields": ["string"],
    "inferred_fields": ["string"],
    "unknown_fields": ["string"]
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

### 6. Explicit / Inferred / Unknown Classification

For each required conceptual input, assign state:

| Input | Explicit If | Inferred If | Unknown If |
|-------|-------------|-------------|------------|
| `topic` | Directly stated | Clear noun phrase in request | Vague ("AI", "our project") |
| `audience` | "for [role]" | Strong role signals (see determine_audience) | No signals |
| `objective` | "to [verb]", "goal is" | Strong verb signals (see determine_objective) | Generic "present", "make" |
| `desired_outcome` | "so that", "we need", "approve" | Implied by objective + audience | Not stated |
| `presentation_type` | "investor deck", "training" | Classification hints + objective | Not classifiable |

**Inference Acceptability Criteria:**
1. Evidence strongly supports it (confidence ≥ 0.8)
2. Low downside if wrong (risk_if_wrong ≤ medium)
3. Does not materially change narrative/evidence/audience interpretation

If any criterion fails → State = `unknown`, generate clarification.

### 7. Hard Constraints Extraction

Parse and preserve as `request.constraints`:

| Constraint | Source | Example |
|------------|--------|---------|
| `max_slides` | "max 10 slides", "under 15" | 10 |
| `aspect_ratio` | "4:3", "16:9", "widescreen" | "16:9" |
| `duration_minutes` | "20 min", "half hour" | 20 |
| `language` | "in Spanish", "French version" | "es" |
| `brand_requirements` | "use our template", "brand guidelines" | { template: "corporate" } |
| `template_locked` | "don't change layout", "fixed template" | true |
| `output_format` | "PPTX only", "PDF export" | "pptx" |
| `required_sections` | "must include risks", "need appendix" | ["risks", "appendix"] |
| `required_sources` | "cite all data", "use Gartner" | ["Gartner"] |

**Rule:** Hard constraints take precedence over aesthetic preferences. Record in `normalized_input.hard_constraints`.

### 8. Conflict Handling

When inputs conflict, apply constitutional priority order (from `PRESENTATION_CONSTITUTION.md`):

```
1. Truthfulness / factual integrity
2. User objective and hard constraints
3. Audience comprehension / decision usefulness
4. Narrative coherence
5. Accessibility / readability
6. Visual hierarchy
7. Brand consistency
8. Aesthetic enhancement
9. Decorative novelty
```

**Procedure:**
- Detect contradictions (e.g., "max 5 slides" vs "cover all 20 topics")
- Resolve by priority: higher priority wins
- Record resolution in assumptions with rationale
- If hard constraint vs aesthetic preference → hard constraint wins

### 9. Ambiguous Request Handling

For underspecified requests (e.g., "Make me a professional PPT about AI"):

**Minimal Extraction:**
- `topic` = "AI" (explicit)
- All other required inputs = `unknown`

**Safe Defaults (Record as Assumptions):**
- `aspect_ratio` = "16:9" (inferred, confidence 0.95)
- `language` = request language (inferred, confidence 0.99)
- `delivery_mode` = "live" (inferred, confidence 0.5)

**Clarification Requirements Generated:**
```json
[
  { "question": "Who is the primary audience?", "domain": "audience", "impact_if_unresolved": "critical" },
  { "question": "What should this presentation achieve?", "domain": "objective", "impact_if_unresolved": "critical" },
  { "question": "What specific outcome indicates success?", "domain": "desired_outcome", "impact_if_unresolved": "high" },
  { "question": "What type of presentation: educational, technical, executive, investor, sales, marketing?", "domain": "presentation_type", "impact_if_unresolved": "high" },
  { "question": "How many slides needed?", "domain": "constraints", "impact_if_unresolved": "medium" }
]
```

**Rule:** Never silently select a highly specific narrative for ambiguous requests.

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