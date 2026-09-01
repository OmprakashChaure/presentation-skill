# Narrative Patterns Library

## Purpose

Catalog of narrative patterns with decision criteria for selection.

## Pattern Library

### 1. Problem-Solution

| Aspect | Detail |
|--------|--------|
| **Purpose** | Drive action on a defined problem |
| **Best Use Case** | Sales, proposals, strategy, product, executive decision |
| **Sequence** | Context → Problem → Consequence → Root Cause → Solution → Evidence → Implementation → Next Step |
| **Strengths** | Clear motivation, logical flow, action-oriented |
| **Limitations** | Assumes problem is agreed; weak for exploration |
| **Anti-Patterns** | Manufactured urgency, solution-first, feature dumping |

### 2. Pyramid

| Aspect | Detail |
|--------|--------|
| **Purpose** | Synthesize to a governing answer; support decision |
| **Best Use Case** | Executive, board, recommendation, strategy synthesis |
| **Sequence** | Answer → 3–5 Key Arguments (MECE) → Evidence per Argument |
| **Strengths** | Answer-first, scannable, logical rigor (MECE) |
| **Limitations** | Requires known answer; not for discovery |
| **Anti-Patterns** | Inverted pyramid, non-MECE, >5 arguments, mixed logic types |

### 3. Assertion-Evidence

| Aspect | Detail |
|--------|--------|
| **Purpose** | Communicate claims with integrated visual proof |
| **Best Use Case** | Technical, scientific, educational, analytical slides |
| **Sequence** | Assertion (title) + Visual Evidence + Annotation + Implication |
| **Strengths** | High retention, evidence-integrated, scannable |
| **Limitations** | Not for navigation/reference slides; requires evidence |
| **Anti-Patterns** | Topic titles, evidence without assertion, decorative "evidence" |

### 4. Chronological

| Aspect | Detail |
|--------|--------|
| **Purpose** | Explain sequence where time-order is causal/organizing |
| **Best Use Case** | History, milestones, incidents, experiments, roadmaps |
| **Sequence** | Phase 1 (Origin) → Phase 2 (Development) → Phase 3 (Result) → Phase 4 (Future) |
| **Strengths** | Intuitive for temporal content, shows causality over time |
| **Limitations** | Weak for synthesis, recommendation, mechanism explanation |
| **Anti-Patterns** | Event dump, forced timeline, missing insight, no synthesis |

### 5. Research

| Aspect | Detail |
|--------|--------|
| **Purpose** | Communicate inquiry: question → method → findings → implications |
| **Best Use Case** | Academic, scientific, market research, analysis reports |
| **Sequence** | Research Question → Motivation/Gap → Methodology → Data → Findings → Uncertainty/Limitations → Interpretation → Implications |
| **Strengths** | Rigorous, transparent, separates finding from interpretation |
| **Limitations** | Dense; not for persuasion or decision-driven decks |
| **Anti-Patterns** | Causal overclaiming, cherry-picking, omitted denominators, correlation≠causation |

### 6. Comparison

| Aspect | Detail |
|--------|--------|
| **Purpose** | Enable choice between options on defined criteria |
| **Best Use Case** | Vendor selection, build vs buy, technology evaluation, trade-off analysis |
| **Sequence** | Decision Context → Criteria Definition → Option Profiles → Side-by-Side Comparison → Recommendation → Next Step |
| **Strengths** | Structured decision support, transparent criteria |
| **Limitations** | Requires agreed criteria; can oversimplify complex choices |
| **Anti-Patterns** | Criteria biased to favorite, missing options, no recommendation |

### 7. Executive Decision

| Aspect | Detail |
|--------|--------|
| **Purpose** | Enable leadership decision with minimal time |
| **Best Use Case** | Board, steering committee, leadership reviews |
| **Sequence** | Decision Required → Executive Answer → Implications → Options + Trade-offs → Recommendation → Risks/Mitigation → Next Steps (Owner/Date) |
| **Strengths** | Answer-first, decision-focused, risk-aware |
| **Limitations** | Requires pre-alignment; not for deep technical debate |
| **Anti-Patterns** | Buried lead, no clear ask, risks minimized, no owner/date |

### 8. Educational Learning Journey

| Aspect | Detail |
|--------|--------|
| **Purpose** | Build capability: novice → competent |
| **Best Use Case** | Training, onboarding, workshops, technical tutorials |
| **Sequence** | Learning Objectives → Prerequisites → Concept → Mechanism → Example → Practice/Application → Misconception Check → Recap → Assessment/Next Steps |
| **Strengths** | Cognitive-load aware, progressive, reinforces |
| **Limitations** | Time-intensive; not for decision or persuasion |
| **Anti-Patterns** | No prerequisites check, no practice, cognitive overload, no recap |

### 9. Change/Transformation

| Aspect | Detail |
|--------|--------|
| **Purpose** | Drive organizational/behavioral change |
| **Best Use Case** | Reorg, migration, culture change, digital transformation |
| **Sequence** | Burning Platform (Why) → Vision (Where) → Current State → Gap Analysis → Roadmap (Phases) → Quick Wins → Capability Building → Measurement → Commitment |
| **Strengths** | Addresses emotion + logic, phased, measurable |
| **Limitations** | Complex; requires sponsorship; long timeline |
| **Anti-Patterns** | Vision without roadmap, no quick wins, no measurement, top-down only |

## Selection Decision Tree

```
START: What is the PRIMARY OBJECTIVE?
│
├─ DECIDE / RECOMMEND / ALIGN LEADERSHIP
│   ├─ Audience = Executive/Board → EXECUTIVE DECISION
│   ├─ Problem agreed, need solution → PROBLEM-SOLUTION
│   ├─ Synthesizing multiple analyses → PYRAMID
│   └─ Choosing between options → COMPARISON
│
├─ PERSUADE / SELL
│   ├─ External buyer → PROBLEM-SOLUTION (sales variant)
│   ├─ Investor → INVESTOR PATTERN (see investor.md)
│   └─ Internal stakeholder → PROBLEM-SOLUTION or CHANGE/TRANSFORMATION
│
├─ TEACH / TRAIN / ONBOARD
│   └─ EDUCATIONAL LEARNING JOURNEY
│
├─ EXPLAIN MECHANISM / PROCESS / TECHNICAL DETAIL
│   └─ ASSERTION-EVIDENCE (per slide) + CHRONOLOGICAL (if temporal)
│
├─ REPORT RESEARCH / ANALYSIS
│   └─ RESEARCH
│
├─ SHOW HISTORY / TIMELINE / INCIDENT / ROADMAP
│   └─ CHRONOLOGICAL
│
└─ DRIVE ORGANIZATIONAL CHANGE
    └─ CHANGE/TRANSFORMATION
```

## Multi-Pattern Decks

A deck MAY combine patterns:

| Combination | Structure |
|-------------|-----------|
| Executive + Problem-Solution | Pyramid at deck level; Problem-Solution per major section |
| Sales + Assertion-Evidence | Problem-Solution narrative; each proof slide = Assertion-Evidence |
| Change + Educational | Change narrative; training modules = Educational Journey |
| Research + Pyramid | Research narrative; executive summary = Pyramid |

**Rule:** One PRIMARY pattern governs deck-level structure; secondary patterns operate at section/slide level.

## Handoff to Other Layers

- **Reasoning (select_narrative):** Implements decision tree
- **Slide-types:** Maps pattern sequences to slide archetypes
- **Presentation-types:** Default pattern per type (e.g., sales → problem-solution)
- **Evaluation:** Checks pattern adherence, anti-patterns, pattern mixing validity