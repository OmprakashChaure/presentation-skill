# Determine Audience — Reasoning Contract

## Purpose

Build a structured audience model that drives all downstream decisions.

## Input

```json
{
  "request": { ... },
  "context": { ... },
  "supplied_audience": "object|null",  // Explicit audience from request
  "classification_hint": "object|null" // From classify_request if available
}
```

## Output

```json
{
  "audience": { ... },                 // Per PresentationPlan.audience
  "assumptions": [...],                // Per PresentationPlan.assumptions
  "clarification_requirements": [...]  // Per PresentationPlan.clarification_requirements
}
```

## Procedure

### 1. Explicit Audience Parsing

If `supplied_audience` provided:
- Parse role, expertise, decision_authority from structured input
- Set confidence = 1.0 for explicit fields
- Proceed to validation

### 2. Audience Inference (When Not Explicit)

**Primary Role Inference:**

| Signal | Inferred Role | Confidence |
|--------|---------------|------------|
| "board", "directors", "C-suite", "executive", "leadership" | C-Suite / Board | 0.95 |
| "investor", "VC", "funding", "pitch", "raise" | Investor | 0.95 |
| "customer", "client", "prospect", "buyer", "sales" | Customer/Prospect | 0.9 |
| "team", "engineering", "developers", "technical" | Technical Practitioners | 0.85 |
| "management", "managers", "directors" (non-C) | Mid-level Management | 0.8 |
| "all-hands", "company", "organization", "everyone" | General Employee | 0.8 |
| "student", "trainee", "onboarding", "workshop", "training" | Learners | 0.9 |

**Expertise Level Inference:**

| Primary Role | Default Expertise | Adjustment Signals |
|--------------|-------------------|-------------------|
| C-Suite/Board | Mixed (business expert, domain novice) | "technical board" → practitioner |
| Investor | Practitioner (business) / Novice (technical) | "technical VC" → practitioner |
| Customer | Practitioner (domain) / Novice (your tech) | "technical buyer" → practitioner |
| Engineering | Expert | "junior" → practitioner |
| Management | Practitioner | — |
| General Employee | Novice | — |
| Learners | Novice | — |

**Decision Authority Inference:**

| Role | Default Authority | Signals for "decider" |
|------|-------------------|----------------------|
| C-Suite/Board | decider | "approval", "decision", "sign off" |
| Investor | decider | "term sheet", "investment committee" |
| Customer | decider | "purchase", "renewal", "vendor selection" |
| Management | influencer/decider | "recommend", "approve budget" |
| Engineering | reviewer/influencer | "implement", "technical review" |
| Learners | learner | — |

### 3. Secondary Audience Detection

Scan for signals of additional audiences:
- "also shared with..." → secondary
- "cc:", "forwarded to" → secondary
- "alignment with..." → secondary (alignment purpose)

### 4. Accessibility Needs

Default: `["none"]`
Signals for specific needs:
- "accessible", "508", "WCAG" → `["screen_reader", "high_contrast"]`
- "translated", "international", "global" → `["translation"]`
- "recorded", "async" → `["captions"]`

### 5. Mindset & Prior Knowledge

**Mindset Inference:**

| Signal | Mindset | Confidence |
|--------|---------|------------|
| "skeptical", "critical", "pushback", "concerns" | skeptical | 0.8 |
| "excited", "bought in", "supportive" | receptive | 0.75 |
| "hostile", "opposed", "resistant" | hostile | 0.7 |
| Default | neutral | 0.5 |

**Prior Knowledge:**
- Extract from request: "familiar with X", "knows Y", "background in Z"
- Infer from role: C-Suite knows business metrics, not implementation details
- Engineers know technical concepts, not business strategy

### 6. Validation & Assumptions

For each inferred field with confidence < 0.8:
- Create assumption entry
- Generate clarification requirement if risk_if_wrong ≥ medium

## Decision Rules

- **MUST** use explicit audience if provided
- **MUST** infer from role keywords when not explicit
- **MUST** set expertise_level based on role + domain signals
- **MUST** set decision_authority based on objective signals (decide → decider)
- **MUST NOT** assume expertise without signals
- **SHOULD** generate clarification for: primary role (if ambiguous), expertise_level (if mixed signals), decision_authority (if unclear)

## Knowledge Consumption

- `knowledge/universal/presentation-principles.md` — Audience-first principle
- `knowledge/presentation_types/*.md` — Audience profiles per type
- `knowledge/storytelling/narrative-patterns.md` — Audience-narrative fit

## Clarification Triggers

Generate clarification when:
- No role signals found → "Who is the primary audience?"
- Conflicting role signals → "Is the audience primarily [A] or [B]?"
- Expertise ambiguous for role → "What is the audience's familiarity with [domain]?"
- Decision authority unclear → "Will the audience make a decision or provide input?"