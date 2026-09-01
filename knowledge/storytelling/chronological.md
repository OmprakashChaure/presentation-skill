# Chronological Narrative

## Purpose

Define when and how to use chronological structure — and when NOT to.

## Scope

**Use for:** History, milestones, incidents, experiments, project phases, temporal change.

**Do NOT use when:** Another analytical structure communicates better.

## When to Use (MUST meet at least one)

| Situation | Example |
|-----------|---------|
| Audience needs to understand sequence | Project timeline, product roadmap |
| Causality depends on time order | Incident retrospective, root cause analysis |
| Change over time IS the message | Market evolution, technology adoption curve |
| Process has temporal dependencies | Clinical trial phases, regulatory approval steps |
| Milestones anchor the narrative | Company history, funding rounds |

## When NOT to Use

| Situation | Better Alternative |
|-----------|-------------------|
| Explaining a mechanism | Assertion-evidence (process diagram) |
| Making a recommendation | Pyramid or problem-solution |
| Comparing options | Comparison structure |
| Synthesizing findings | Pyramid or research pattern |
| Teaching a concept | Educational learning journey |
| Persuading to act | Problem-solution |

**Rule:** Chronology is a DEFAULT for time-dependent content, not a universal template.

## Structure

```
PHASE 1: ORIGIN / BASELINE
  ├─ Context
  ├─ Trigger event
  └─ Initial state
  ▼
PHASE 2: DEVELOPMENT / INTERVENTION
  ├─ Key actions/events (sequential)
  ├─ Decision points
  └─ Intermediate outcomes
  ▼
PHASE 3: CURRENT STATE / RESULT
  ├─ Measured outcomes
  ├─ Deviations from plan
  └─ Current status
  ▼
PHASE 4: FUTURE / NEXT PHASE (optional)
  ├─ Projected trajectory
  ├─ Planned actions
  └─ Decision needed
```

## Slide Rules

### Timeline Slides
- **Visual:** Horizontal timeline (left→right) or vertical (top→bottom)
- **Density:** Max 6–8 events per slide; split if more
- **Annotation:** Each event = date + label + significance (not just date+label)
- **Grouping:** Use phase bands/colour to show periods

### Phase Transition Slides
- **Purpose:** Mark major shifts (before/after)
- **Content:** What changed, why, impact
- **Visual:** Comparison (before vs after) or transition diagram

### Incident/Retrospective Specific
- **Must include:** Timeline → Root cause → Impact → Corrective actions → Prevention
- **Blame-free language:** "System allowed X" not "Team failed to Y"

## Anti-Patterns

- **Chronological resume:** "Jan: did X. Feb: did Y. Mar: did Z." (no synthesis)
- **Forced timeline:** Fitting non-temporal content into timeline
- **Event dump:** Dates without significance/insight
- **Missing causality:** Sequence shown but no "why" or "so what"
- **Present-only:** No future projection when decision needed

## Time Representation Rules

- **Scale:** Proportional time spacing (not equal spacing for unequal intervals)
- **Granularity:** Match audience need (quarters for business, sprints for dev, minutes for incident)
- **Relative time:** "Week 1, Week 2" for process; absolute dates for history
- **Uncertainty:** Dashed/faded for projected future events

## Handoff to Other Layers

- **Narrative-patterns:** Chronological is a pattern in the library
- **Reasoning (select_narrative):** Chooses when time-order is primary organizing principle
- **Slide-types:** Timeline, milestone, phase-transition slide archetypes
- **Charts:** Time-series, Gantt, roadmap visualizations
- **Evaluation:** Checks: temporal logic, proportional spacing, insight per event, not forced