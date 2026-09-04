# Select Narrative — Reasoning Contract

## Purpose

Select the narrative structure that best serves the objective, audience, and content.

## Input

```json
{
  "objective": { ... },
  "audience": { ... },
  "classification": { ... },
  "context": { ... },
  "available_evidence": ["string"]  // Types of evidence available
}
```

## Output

```json
{
  "narrative": { ... },                // Per PresentationPlan.narrative
  "assumptions": [...],
  "clarification_requirements": [...]
}
```

## Procedure

### 1. Narrative Pattern Selection (Decision Tree)

**Start with Objective + Audience:**

```
IF objective.primary = decide AND audience.primary.decision_authority = decider
  AND classification.primary_type = executive
  → executive_decision (confidence 0.95)

ELSE IF objective.primary = decide AND audience.primary.decision_authority = decider
  → pyramid (confidence 0.9)

ELSE IF objective.primary = recommend
  → pyramid (confidence 0.85)

ELSE IF objective.primary = persuade
  AND classification.primary_type = sales
  → problem_solution (confidence 0.95)

ELSE IF objective.primary = persuade
  AND classification.primary_type = investor
  → investor (confidence 0.95)

ELSE IF objective.primary = persuade
  AND classification.primary_type = marketing
  → marketing (confidence 0.9)

ELSE IF objective.primary = teach
  → educational_journey (confidence 0.95)

ELSE IF objective.primary = inform
  AND classification.primary_type = research
  → research (confidence 0.9)

ELSE IF objective.primary = inform
  AND context has strong temporal component (history, roadmap, incident)
  → chronological (confidence 0.85)

ELSE IF objective.primary = align
  → problem_solution OR comparison (confidence 0.8)

ELSE IF objective.primary = explore
  → research OR chronological (confidence 0.7)

ELSE
  → assertion_evidence (confidence 0.6)  // Safe default for analytical
```

### 2. Pattern Variant Selection

| Pattern | Variants | Selection Criteria |
|---------|----------|-------------------|
| pyramid | standard, inverted (rare) | Standard unless exploratory |
| problem_solution | standard, compressed, multi_problem, comparative | Time constraint → compressed; Multiple problems → multi_problem; Options comparison → comparative |
| chronological | standard, phase_focused, incident | Incident → incident; Roadmap → phase_focused |
| executive_decision | standard, options_focused | Multiple options → options_focused |
| educational_journey | standard, workshop, microlearning | Duration > 60min → workshop; < 15min → microlearning |
| investor | standard, traction_heavy, vision_heavy | Pre-revenue → vision_heavy; Series B+ → traction_heavy |

### 3. Structure Expansion

Expand selected pattern into `narrative.structure` array:

**Example: problem_solution (standard)**
```json
[
  {"stage": "context", "description": "Shared reality", "slide_count_estimate": 1, "key_messages": ["Current state"]},
  {"stage": "problem", "description": "Quantified pain", "slide_count_estimate": 1, "key_messages": ["Problem statement"]},
  {"stage": "consequence", "description": "Impact if unsolved", "slide_count_estimate": 1, "key_messages": ["Cost of inaction"]},
  {"stage": "root_cause", "description": "Why it exists", "slide_count_estimate": 1, "key_messages": ["Root cause"]},
  {"stage": "solution", "description": "Proposed answer", "slide_count_estimate": 1, "key_messages": ["Solution overview"]},
  {"stage": "evidence", "description": "Proof it works", "slide_count_estimate": 2, "key_messages": ["Pilot results", "Case study"]},
  {"stage": "implementation", "description": "What it takes", "slide_count_estimate": 1, "key_messages": ["Timeline, resources"]},
  {"stage": "next_step", "description": "Decision needed", "slide_count_estimate": 1, "key_messages": ["Ask"]}
]
```

### 4. Deck-Level Assertion (Pyramid/Executive)

If pattern ∈ {pyramid, executive_decision}:
- Extract/govern from objective.desired_outcome
- Formulate as single declarative sentence
- Set `narrative.deck_level_assertion`

### 5. Evidence-Narrative Fit Check

Verify available evidence supports pattern:
- `problem_solution` → Needs: problem data, solution evidence, implementation plan
- `pyramid` → Needs: evidence for each argument
- `research` → Needs: methodology, data, uncertainty quantification
- `educational_journey` → Needs: examples, exercises, assessments

If gaps → Record assumptions, generate clarification for critical missing evidence.

### 6. Confidence Calculation

Base confidence from decision tree + modifiers:
- +0.1 if classification.primary_type matches pattern default
- +0.1 if objective.primary strongly signals pattern
- -0.2 if evidence gaps for required stages
- -0.1 if audience expertise mismatches pattern assumption

## Decision Rules

- **MUST** follow decision tree order (objective → audience → classification → context)
- **MUST** select pattern before defining slide intents
- **MUST** expand pattern into structure with slide_count_estimate
- **MUST** verify evidence availability for required stages
- **MUST NOT** force pattern — if confidence < 0.6, use assertion_evidence with recorded assumption
- **SHOULD** prefer problem_solution for persuade + sales/investor/marketing
- **SHOULD** prefer pyramid for decide/recommend + executive
- **SHOULD** prefer educational_journey for teach

## Knowledge Consumption

- `knowledge/storytelling/narrative-patterns.md` — Pattern library, decision tree, variants
- `knowledge/storytelling/pyramid.md` — MECE, vertical/horizontal logic
- `knowledge/storytelling/assertion-evidence.md` — Default for analytical
- `knowledge/storytelling/problem-solution.md` — Structure, anti-patterns
- `knowledge/storytelling/chronological.md` — When to use/not use
- `knowledge/presentation_types/*.md` — Type-default patterns

## Clarification Triggers

Generate clarification when:
- Confidence < 0.6 → "Multiple structures could work. Should we lead with [A] or [B]?"
- Critical evidence missing for pattern → "This structure needs [evidence type]. Do you have it?"
- Pattern variant ambiguous → "Should we use the standard or compressed version?"