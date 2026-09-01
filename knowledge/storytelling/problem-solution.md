# Problem-Solution Narrative

## Purpose

Define the problem-solution narrative structure for presentations where the objective is to drive action on a defined problem.

## Scope

Appropriate for: Sales, technical proposals, strategy, executive, product presentations.

**Not for:** Pure learning, exploration, chronological reporting, open-ended research.

## Structure

```
CONTEXT
  │  (Shared understanding — "Where we are")
  ▼
PROBLEM
  │  (Specific, quantified pain — "What's wrong")
  ▼
CONSEQUENCE
  │  (Impact if unsolved — "Why it matters")
  ▼
ROOT CAUSE
  │  (Why problem exists — "Why it's happening")
  ▼
SOLUTION
  │  (Proposed answer — "What we do")
  ▼
EVIDENCE
  │  (Proof it works — "Why believe us")
  ▼
IMPLEMENTATION
  │  (How it works — "What it takes")
  ▼
NEXT STEP
     (Clear action — "What we need from you")
```

## Component Rules

### Context
- **MUST** establish shared reality audience agrees with
- **SHOULD** be 1 slide maximum
- **Rule:** No controversial claims in context

### Problem
- **MUST** be specific and quantified
- **MUST** be audience's problem (not presenter's)
- **Format:** "[Metric] is [current state] vs [target/benchmark]"
- **Anti-pattern:** "We need better tools" → "Deployments take 4hrs (target: 15min)"

### Consequence
- **MUST** quantify impact: cost, risk, lost opportunity, competitive disadvantage
- **SHOULD** use audience's metrics (revenue, churn, cost, compliance)
- **Anti-pattern:** Manufactured urgency without evidence

### Root Cause
- **MUST** be evidence-based (data, analysis, not opinion)
- **SHOULD** distinguish symptoms from causes
- **Rule:** If multiple causes, prioritize by impact

### Solution
- **MUST** directly address root cause(s)
- **MUST** be specific (not "improve process" → "automate deploy pipeline")
- **SHOULD** acknowledge alternatives considered

### Evidence
- **MUST** prove solution works: pilot data, case study, benchmark, logical proof
- **SHOULD** distinguish: proven (done) vs projected (modelled)
- **Anti-pattern:** "Trust us" without evidence

### Implementation
- **SHOULD** include: timeline, resources, owners, milestones, risks
- **Level of detail:** Match audience (executive = high-level; technical = detailed)

### Next Step
- **MUST** be specific, time-bound, assigned
- **Format:** "Decision needed: Approve $X budget by [date] → [Owner]"

## Anti-Patterns (MUST PREVENT)

| Anti-Pattern | Detection | Correction |
|--------------|-----------|------------|
| Manufactured urgency | Consequence not quantified; "urgent" without data | Require quantified impact; remove urgency language |
| Unsupported claims | Solution stated without evidence | Require evidence slide per solution claim |
| Solution-first dumping | Solution appears before problem/root cause | Enforce sequence: Context → Problem → Cause → Solution |
| Feature dumping (sales) | Solution = feature list without problem mapping | Map each feature to specific problem/root cause |
| Vague next step | "Let's discuss" / "Follow up" | Require: Decision/Action + Owner + Deadline |

## When to Use

| Presentation Type | Use Problem-Solution? |
|-------------------|----------------------|
| Sales pitch | YES (default) |
| Technical proposal | YES |
| Strategy review | YES |
| Executive decision | YES (often combined with pyramid) |
| Product launch | YES |
| Investor pitch | PARTIAL (use investor pattern) |
| Technical training | NO (use educational) |
| Incident retrospective | NO (use chronological) |
| Research presentation | NO (use research pattern) |

## Variants

### Problem-Solution-Evidence (Compressed)
For time-constrained: Context+Problem → Solution → Evidence → Next Step (4 slides)

### Multi-Problem
One deck, multiple problem-solution threads → Use section dividers per thread

### Comparative Solution
Problem → Option A → Option B → Recommendation → Evidence → Next Step

## Handoff to Other Layers

- **Narrative-patterns:** Problem-solution is a pattern in the library
- **Reasoning (select_narrative):** Chooses when objective=persuade/decide, audience has defined problem
- **Slide-types:** Maps each component to slide archetypes
- **Evaluation:** Checks sequence, quantification, evidence, next-step specificity