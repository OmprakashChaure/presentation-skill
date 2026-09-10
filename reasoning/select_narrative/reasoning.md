# Select Narrative — Reasoning Contract

## Purpose

Select the narrative structure that best serves the objective, audience, and content. Narrative is selected after context and classification, but before detailed slide planning.

## Input

```json
{
  "objective": { ... },
  "audience": { ... },
  "classification": { ... },
  "context": { ... },
  "available_evidence": ["string"]
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

## Available Narrative Structures

Per `knowledge/storytelling/narrative-patterns.md`:

| Structure | Best For | Organizing Principle |
|-----------|----------|---------------------|
| **Pyramid** | Executive, decision, recommendation, synthesis | Conclusion → Reasons → Evidence |
| **Assertion-Evidence** | Technical, scientific, educational, analytical | Claim → Evidence → Interpretation |
| **Problem-Solution** | Sales, proposals, strategy, product | Problem → Consequence → Solution → Evidence → Action |
| **Chronological** | History, milestones, incidents, roadmaps | Time-ordered sequence |
| **Comparison** | Evaluation, vendor selection, trade-off analysis | Criteria → Options → Trade-offs → Recommendation |
| **Research** | Academic, scientific, market research | Question → Method → Evidence → Findings → Uncertainty → Interpretation |
| **Educational Learning Journey** | Training, onboarding, skill building | Prior Knowledge → Concept → Explanation → Example → Application → Synthesis |
| **Executive Decision** | Board, steering committee, leadership | Decision Required → Context → Options → Evidence → Trade-offs → Recommendation |
| **Transformation/Change** | Reorg, migration, culture change, digital transformation | Current State → Reason for Change → Transition → Future State → Implementation |

## Selection Principle

The correct narrative is determined by:

```
audience
+ objective
+ desired outcome
+ presentation type
+ evidence structure
+ decision dependencies
```

**Rule:** No narrative structure should be forced merely because it is familiar.

## Narrative Selection Heuristics

### Pyramid
**Prefer when audience needs:** conclusion first, structured supporting reasons, executive synthesis, decision-oriented communication
**Typical flow:** answer/recommendation → key reasons → supporting evidence → detail

### Assertion-Evidence
**Prefer when:** individual claims require visible supporting evidence, evidence exists for analytical content
**Typical flow:** claim → evidence → interpretation
**Strong default for:** analytical, scientific, technical, educational communication

### Problem-Solution
**Prefer when:** establishing problem → consequences → solution → evidence → action
**Prevent:** manufactured urgency, unsupported claims, solution-first dumping

### Chronological
**Prefer when:** time order itself explains the subject (historical development, project progression, incident timeline, implementation journey)
**Do NOT use when:** another analytical structure communicates better

### Comparison
**Prefer when:** audience must understand meaningful alternatives or trade-offs
**Typical flow:** decision context → evaluation criteria → options → trade-offs → recommendation/conclusion

### Research
**Prefer when:** communicating a structured investigation
**Typical flow:** question → methodology → evidence → findings → limitations/uncertainty → interpretation → conclusion
**Prevent:** causal overclaiming, cherry-picking, omitted denominators, correlation≠causation

### Educational Learning Journey
**Prefer when:** progressive understanding is primary objective
**Typical flow:** prior knowledge → concept → explanation → example → application → synthesis
**Include:** misconception handling, signalling, segmentation, cognitive load management

### Executive Decision
**Prefer when:** audience must make or approve a decision
**Typical flow:** decision required → context → options → evidence → trade-offs → recommendation → decision/next step
**Prefer:** answer-first structure

### Transformation/Change
**Prefer when:** explaining movement from current state to desired future state
**Typical flow:** current state → reason for change → transition → future state → implementation

## Selection Procedure

1. **Identify dominant audience need** (decide, learn, understand, compare, act)
2. **Identify communication objective** (from objective.primary)
3. **Identify expected audience action** (from classification.expected_action)
4. **Identify evidence structure** (what evidence exists, what gaps)
5. **Determine dominant organizing relationship:**
   - Time → Chronological
   - Decision among options → Comparison / Executive Decision
   - Problem driving action → Problem-Solution
   - Synthesis to conclusion → Pyramid
   - Progressive understanding → Educational Journey
   - Structured investigation → Research
   - Claim + proof per slide → Assertion-Evidence
   - State change → Transformation/Change
6. **Select simplest narrative** that satisfies communication need
7. **Document rationale** in `narrative.rationale`

## Decision Tree (Enhanced)

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
  AND classification.info_persuasion_balance = primarily_informational
  AND context has strong temporal component (history, roadmap, incident)
  → chronological (confidence 0.85)

ELSE IF objective.primary = inform
  AND classification.evidence_burden = high
  AND context has methodology/data signals
  → research (confidence 0.8)

ELSE IF objective.primary = align
  AND classification.expected_action ∈ {compare, decide}
  → comparison (confidence 0.8)

ELSE IF objective.primary = align
  AND context has change/transformation signals
  → transformation_change (confidence 0.8)

ELSE IF objective.primary = explore
  → research OR chronological (confidence 0.7)

ELSE IF classification.primary_type = technical
  AND objective.primary ∈ {inform, explain}
  → assertion_evidence (confidence 0.8)

ELSE
  → assertion_evidence (confidence 0.6)  // Safe analytical default
```

## Pattern Variant Selection

| Pattern | Variants | Selection Criteria |
|---------|----------|-------------------|
| pyramid | standard, inverted (rare) | Standard unless exploratory |
| problem_solution | standard, compressed, multi_problem, comparative | Time constraint → compressed; Multiple problems → multi_problem; Options comparison → comparative |
| chronological | standard, phase_focused, incident | Incident → incident; Roadmap → phase_focused |
| executive_decision | standard, options_focused | Multiple options → options_focused |
| educational_journey | standard, workshop, microlearning | Duration > 60min → workshop; < 15min → microlearning |
| investor | standard, traction_heavy, vision_heavy | Pre-revenue → vision_heavy; Series B+ → traction_heavy |
| comparison | standard, criteria_first, options_first | Criteria agreed → criteria_first; Options known → options_first |
| transformation_change | standard, phased, pilot_first | Large org → phased; Risk-averse → pilot_first |

## Structure Expansion

Expand selected pattern into `narrative.structure` array with stages:

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

**Example: executive_decision (options_focused)**
```json
[
  {"stage": "decision_required", "description": "What decision, by when", "slide_count_estimate": 1, "key_messages": ["Decision frame"]},
  {"stage": "context", "description": "Shared reality", "slide_count_estimate": 1, "key_messages": ["Current state"]},
  {"stage": "options", "description": "Alternatives with criteria", "slide_count_estimate": 2, "key_messages": ["Option A", "Option B", "Option C"]},
  {"stage": "evidence", "description": "Data per option", "slide_count_estimate": 2, "key_messages": ["Evidence A", "Evidence B"]},
  {"stage": "tradeoffs", "description": "Criteria comparison", "slide_count_estimate": 1, "key_messages": ["Trade-off summary"]},
  {"stage": "recommendation", "description": "Recommended option + rationale", "slide_count_estimate": 1, "key_messages": ["Recommendation"]},
  {"stage": "next_step", "description": "Decision / action", "slide_count_estimate": 1, "key_messages": ["Ask"]}
]
```

**Example: educational_journey (standard)**
```json
[
  {"stage": "objectives", "description": "Learning goals", "slide_count_estimate": 1, "key_messages": ["Objectives"]},
  {"stage": "prerequisites", "description": "Prior knowledge check", "slide_count_estimate": 1, "key_messages": ["Prerequisites"]},
  {"stage": "concept_1", "description": "Concept → Mechanism → Example → Application", "slide_count_estimate": 3, "key_messages": ["Concept 1"]},
  {"stage": "concept_2", "description": "Concept → Mechanism → Example → Application", "slide_count_estimate": 3, "key_messages": ["Concept 2"]},
  {"stage": "synthesis", "description": "Integration + Misconceptions", "slide_count_estimate": 2, "key_messages": ["Synthesis", "Misconceptions"]},
  {"stage": "assessment", "description": "Check understanding", "slide_count_estimate": 1, "key_messages": ["Assessment"]}
]
```

## Deck-Level Assertion (Pyramid/Executive)

If pattern ∈ {pyramid, executive_decision}:
- Extract/govern from `objective.desired_outcome`
- Formulate as single declarative sentence
- Set `narrative.deck_level_assertion`

## Narrative Rationale

**MUST** include concise rationale in `narrative.rationale`:

> **Example:**
> Structure: Executive Decision
> Rationale: The audience must approve one of three architecture options. The narrative therefore moves from the decision context through criteria and evidence to trade-offs and a recommendation.

## Narrative and Slide Types

Narrative determines logical progression; slide archetype determines semantic form per slide.

**Example: Executive Decision narrative may contain:**
```
Title → orient
Decision/Recommendation → recommendation
Context → assertion_evidence
Comparison → comparison
Evidence → chart/data / case_study
Trade-offs → comparison
Recommendation → recommendation
Next Steps → recommendation
Appendix → appendix/reference
```

**Rule:** Narrative structure does not determine every slide archetype.

## Avoid Narrative Overfitting

**MUST NOT** force every presentation into fixed number of stages or slides.

- Narrative structures are adaptive
- Short presentation → complete narrative in few slides
- Research presentation → more evidence/methodological detail
- Slide count follows communication requirements and constraints, not arbitrary template

## Narrative Dependencies

**MUST** record meaningful dependencies between sections in `narrative.structure` stage descriptions:

```json
{
  "stage": "tradeoffs",
  "description": "Criteria comparison",
  "dependencies": ["options", "evidence"],
  "dependents": ["recommendation"]
}
```

**Purpose:** Prevents slide sequencing from becoming disconnected collection.

Example dependencies:
- "Section A establishes the problem"
- "Section B evaluates alternatives"
- "Section C depends on criteria established in Section B"
- "Section D presents recommendation derived from Sections B and C"

## Evidence-Narrative Fit Check

Verify available evidence supports pattern:

| Pattern | Required Evidence Stages |
|---------|-------------------------|
| problem_solution | problem data, solution evidence, implementation plan |
| pyramid | evidence for each argument |
| research | methodology, data, uncertainty quantification |
| educational_journey | examples, exercises, assessments |
| comparison | criteria definitions, option data, trade-off analysis |
| transformation_change | current state data, change rationale, transition plan |

If gaps → Record assumptions, generate clarification for critical missing evidence.

## Confidence Calculation

```
Base = Decision tree confidence
+ 0.1 if classification.primary_type matches pattern default
+ 0.1 if objective.primary strongly signals pattern
+ 0.1 if dominant organizing relationship clear
- 0.2 if evidence gaps for required stages
- 0.1 if audience expertise mismatches pattern assumption
- 0.1 if slide count constraint forces overfitting
Clamped to [0.0, 1.0]
```

## Decision Rules

- **MUST** follow decision tree order (objective → audience → classification → context)
- **MUST** select pattern before defining slide intents
- **MUST** expand pattern into structure with slide_count_estimate
- **MUST** verify evidence availability for required stages
- **MUST** document rationale in `narrative.rationale`
- **MUST** record narrative dependencies between stages
- **MUST NOT** force pattern — if confidence < 0.6, use assertion_evidence with recorded assumption
- **MUST NOT** overfit — adapt structure to communication needs, not template
- **SHOULD** prefer problem_solution for persuade + sales/investor/marketing
- **SHOULD** prefer pyramid for decide/recommend + executive
- **SHOULD** prefer educational_journey for teach

## Knowledge Consumption

- `knowledge/storytelling/narrative-patterns.md` — Pattern library, decision tree, variants
- `knowledge/storytelling/pyramid.md` — MECE, vertical/horizontal logic
- `knowledge/storytelling/assertion-evidence.md` — Default for analytical
- `knowledge/storytelling/problem-solution.md` — Structure, anti-patterns
- `knowledge/storytelling/chronological.md` — When to use/not use
- `knowledge/storytelling/comparison.md` — Comparison pattern (if exists)
- `knowledge/presentation_types/*.md` — Type-default patterns

## Clarification Triggers

Generate clarification when:
- Confidence < 0.6 → "Multiple structures could work. Should we lead with [A] or [B]?"
- Critical evidence missing for pattern → "This structure needs [evidence type]. Do you have it?"
- Pattern variant ambiguous → "Should we use the standard or compressed version?"
- Dominant organizing relationship unclear → "Is the core structure a decision, a problem, a timeline, or a comparison?"