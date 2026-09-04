# Determine Objective — Reasoning Contract

## Purpose

Establish the presentation objective that governs all structural decisions.

## Input

```json
{
  "request": { ... },
  "context": { ... },
  "audience": { ... },
  "supplied_objective": "object|null"  // Explicit objective from request
}
```

## Output

```json
{
  "objective": { ... },                // Per PresentationPlan.objective
  "assumptions": [...],
  "clarification_requirements": [...]
}
```

## Procedure

### 1. Explicit Objective Parsing

If `supplied_objective` provided:
- Map to `primary` enum: `decide | recommend | inform | teach | persuade | align | explore`
- Extract `desired_outcome` as concrete, measurable statement
- Parse `success_criteria` from "success means..." / "we'll know it worked when..."
- Set `persuasion_vs_information` from language signals
- Set `evidence_burden` from context (regulatory, investor, board → high)

### 2. Objective Inference (When Not Explicit)

**Primary Objective Mapping:**

| Request Language | Primary Objective | Confidence |
|------------------|-------------------|------------|
| "decide", "approval", "vote", "sign off", "greenlight" | decide | 0.95 |
| "recommend", "proposal", "suggest", "option" | recommend | 0.9 |
| "pitch", "sell", "convince", "win", "convert" | persuade | 0.9 |
| "teach", "train", "onboard", "educate", "workshop" | teach | 0.95 |
| "inform", "update", "brief", "status", "report" | inform | 0.85 |
| "align", "sync", "shared understanding", "get on same page" | align | 0.85 |
| "explore", "investigate", "research", "analyze" | explore | 0.8 |
| "present", "show", "demo" | inform | 0.6 (ambiguous) |

**Secondary Objectives:**
- Often multiple: e.g., `persuade` + `inform`, `teach` + `align`
- Extract from conjunctions: "inform and persuade", "teach so they can decide"

### 3. Desired Outcome Formulation

**Rules:**
- **MUST** be concrete and observable
- **MUST** be expressed in audience's terms
- **FORMAT:** "[Audience] [action] [target] by [timeframe]"

| Weak | Strong |
|------|--------|
| "Understand our strategy" | "Leadership approves Q3 strategy by Friday" |
| "Know the architecture" | "Engineering team can implement auth service by sprint end" |
| "See the results" | "Board votes to fund Phase 2 ($2M) at next meeting" |

If user provides vague outcome → Generate clarification requirement.

### 4. Success Criteria

Derive from desired_outcome:
- Binary: Decision made (yes/no)
- Continuous: Metric threshold achieved
- Behavioral: Audience takes specific action

### 5. Persuasion vs. Information Balance

Calculate 0.0–1.0:

| Factor | Weight |
|--------|--------|
| Primary = persuade | +0.4 |
| Primary = recommend | +0.3 |
| Primary = decide | +0.2 |
| Primary = teach/inform | -0.3 |
| Audience = skeptical | +0.2 |
| Audience = receptive | -0.1 |
| High evidence burden | +0.1 |
| Clamped to [0.0, 1.0] | |

### 6. Evidence Burden

| Context | Burden |
|---------|--------|
| Investor pitch | high |
| Board decision | high |
| Regulatory/compliance | regulatory |
| Technical proposal | high |
| Sales (enterprise) | high |
| Sales (SMB) | medium |
| Internal update | low |
| Training | low |
| Research | high |
| Marketing | medium |

### 7. Call to Action & Deadline

- Extract explicit: "We need X by Y"
- Infer from objective: `decide` → decision deadline; `persuade` → next meeting; `teach` → assessment date

## Decision Rules

- **MUST** have concrete `desired_outcome` — if vague, generate clarification
- **MUST** set `evidence_burden` per context table
- **MUST** align `primary` with audience `decision_authority`:
  - Audience = decider → primary ∈ {decide, recommend, persuade}
  - Audience = learner → primary = teach
  - Audience = reviewer → primary ∈ {inform, align, explore}
- **MUST NOT** set `persuade` as primary if audience is learner
- **SHOULD** generate clarification if `desired_outcome` not measurable

## Knowledge Consumption

- `knowledge/universal/presentation-principles.md` — Objective-first principle
- `knowledge/presentation_types/*.md` — Objective-type mapping
- `knowledge/storytelling/narrative-patterns.md` — Objective-narrative fit

## Clarification Triggers

Generate clarification when:
- No objective signals → "What should this presentation achieve?"
- `desired_outcome` vague → "What specific outcome indicates success? (e.g., 'Board approves budget')"
- Primary objective conflicts with audience authority → "Audience is [role]; is the goal to [decide/recommend/learn]?"
- Multiple conflicting objectives → "Which is primary: [A] or [B]?"