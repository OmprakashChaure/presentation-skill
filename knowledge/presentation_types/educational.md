# Educational Presentation Type

## Purpose

Define type-specific policies for educational/instructional presentations.

## Scope

Training, onboarding, workshops, tutorials, technical education, knowledge transfer.

## Core Policies

### Learning Objectives

- **MUST** state explicit, measurable learning objectives (slide 1 or 2)
- **Format:** "By the end of this session, you will be able to: [verb] [concept] [context]"
- **Bloom's taxonomy verbs:** Define, explain, apply, analyze, evaluate, create
- **SHOULD** limit to 3–5 objectives per session

### Prerequisite Knowledge

- **MUST** declare required prior knowledge
- **Format:** "This session assumes you know: [concept 1], [concept 2]"
- **SHOULD** provide pre-read/appendix for gaps
- **Anti-pattern:** Teaching prerequisites inside main flow (use pretraining principle)

### Progressive Explanation Structure

Per concept/module:

```
CONCEPT (what) → MECHANISM (how) → EXAMPLE (concrete) → APPLICATION (practice)
```

- **Concept:** Definition, mental model, analogy
- **Mechanism:** Process, rules, cause-effect, diagram
- **Example:** Worked case, walkthrough, demo
- **Application:** Exercise, quiz, scenario, "your turn"

### Misconception Handling

- **SHOULD** anticipate and address common misconceptions
- **Format:** "Common mistake: [wrong belief] → Reality: [correct model]"
- **Placement:** After mechanism, before example
- **Rule:** Don't introduce misconceptions not in audience's mind

### Signalling (Cognitive Load)

- **MUST** use explicit structural signals:
  - Module objectives slide
  - Section dividers with progress ("Module 2 of 4")
  - Summary slides per module
  - "Key takeaway" callout boxes
- **Rule:** Audience should always know: Where am I? What's the point?

### Segmentation (Cognitive Load)

- **MUST** segment into ≤15-minute modules
- **MUST** insert cognitive breaks: summary, question, activity
- **Rule:** No slide deck >60 min without major break

### Recap & Reinforcement

- **MUST** include spaced recap:
  - End of module: 3-bullet summary
  - End of session: Objective checklist + "What changed for you?"
- **SHOULD** provide reference sheet/appendix

## Slide Type Defaults

| Purpose | Slide Archetype |
|---------|-----------------|
| Learning objectives | Title/Objectives |
| Prerequisites | Reference/Checklist |
| Concept | Assertion-Evidence (diagram) |
| Mechanism | Process/Flow diagram |
| Example | Case Study / Walkthrough |
| Application | Activity / Exercise |
| Misconception | Comparison (Myth vs Reality) |
| Recap | KPI/Summary |
| Assessment | Question / Quiz |

## Design Adaptations

- **Density:** Lower — more whitespace, larger type, fewer concepts per slide
- **Builds:** Progressive reveal (assertion → evidence → implication)
- **Colour:** Category colours for concept families (consistent across deck)
- **Icons:** Consistent icon per concept type (definition, example, warning, tip)

## Anti-Patterns

- No learning objectives
- Assuming unknown prerequisites
- Concept without mechanism or example
- >20 min without interaction/break
- Dense text slides (violates coherence, segmenting)
- No recap or reinforcement
- Jargon without definition

## Handoff to Other Layers

- **Reasoning:** Selects educational pattern; enforces cognitive load principles
- **Narrative-patterns:** Educational learning journey is the default pattern
- **Slide-types:** Maps educational components to archetypes
- **Cognitive-load:** Strongest enforcement here (coherence, signalling, segmenting, pretraining)
- **Evaluation:** Checks objectives, prerequisites, progression, segmentation, recap