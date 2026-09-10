# Classify Presentation — Reasoning Contract

## Purpose

Determine the multi-dimensional classification of the presentation before narrative and slide planning.

## Input

```json
{
  "audience": { ... },
  "objective": { ... },
  "context": { ... },
  "normalized_input": { ... }
}
```

## Output

```json
{
  "classification": { ... },           // Per PresentationPlan.classification
  "assumptions": [...],
  "clarification_requirements": [...]
}
```

## Procedure

### 1. Primary Type Classification

**Signal Sources (in priority order):**

| Signal | Weight | Types Indicated |
|--------|--------|-----------------|
| Explicit user label ("investor deck", "training") | 1.0 | Direct match |
| Objective.primary | 0.8 | decide→executive, teach→educational, persuade→sales/investor/marketing |
| Audience.primary.role | 0.7 | C-Suite→executive, Investor→investor, Customer→sales, Learner→educational |
| Context.venue | 0.5 | Boardroom→executive, Conference→marketing/technical |
| Available data type | 0.4 | Metrics/financials→investor/executive, Code/specs→technical |

**Decision Matrix:**

```
IF explicit label provided with confidence ≥0.8
  → Use explicit (confidence = 0.9)

ELSE IF objective.primary = teach
  → educational (confidence 0.85)

ELSE IF objective.primary = decide AND audience.primary.decision_authority = decider
  → executive (confidence 0.85)

ELSE IF objective.primary = persuade
  AND audience.primary.role = investor
  → investor (confidence 0.9)

ELSE IF objective.primary = persuade
  AND audience.primary.role = customer
  → sales (confidence 0.85)

ELSE IF objective.primary = persuade
  AND context has brand/campaign signals
  → marketing (confidence 0.8)

ELSE IF objective.primary ∈ {inform, explain} AND audience.expertise_level = expert
  → technical (confidence 0.8)

ELSE IF objective.primary = inform AND context has methodology/data signals
  → research (confidence 0.75)

ELSE
  → assertion_evidence (analytical default, confidence 0.6)
```

### 2. Secondary Types Detection

Scan for additional applicable types:

| Primary | Common Secondary | Trigger Signals |
|---------|------------------|-----------------|
| executive | technical, investor, sales | "technical details", "funding", "customer proof" |
| technical | educational, executive | "explain to leadership", "onboard team" |
| research | educational, technical | "teach method", "implementation details" |
| investor | executive, technical | "board summary", "technical moat" |
| sales | technical, marketing | "architecture", "campaign alignment" |
| marketing | sales, educational | "enable sales", "train partners" |
| educational | technical, research | "advanced concepts", "evidence base" |

**Rule:** Secondary types only added if explicit signals exist (confidence ≥0.7).

### 3. Audience Expertise Assessment

Map from `audience.primary.expertise_level` + domain signals:

| Audience Expertise | Classification Value |
|-------------------|---------------------|
| novice | novice |
| practitioner | intermediate |
| expert | expert |
| mixed | mixed |
| Not determined | unknown |

**Mixed Audience Rule:** If `mixed`, classification.expertise = `mixed` and global_strategy must address both levels.

### 4. Information / Persuasion Balance

Calculate from `objective.persuasion_vs_information` (0.0–1.0):

| Range | Classification |
|-------|----------------|
| 0.0–0.2 | primarily_informational |
| 0.2–0.4 | informational_with_recommendation |
| 0.4–0.6 | balanced_information_and_persuasion |
| 0.6–1.0 | primarily_persuasive |

**Rule:** Persuasion MUST NOT weaken factual integrity (constitutional priority).

### 5. Evidence Burden Assessment

**Per-Claim Assessment (Not Just Presentation Label):**

| Context Signal | Burden Level |
|----------------|--------------|
| Investor pitch, board decision, regulatory | high |
| Technical claims (performance, security, scalability) | high |
| Financial projections, market sizing | high |
| Sales claims (ROI, TCO, competitive) | high |
| Research findings, scientific claims | high |
| Educational concepts, established frameworks | moderate |
| Internal updates, status reports | low |
| Marketing positioning, brand | low/moderate |

**Overall Classification:** Maximum burden across all substantive claims.

### 6. Expected Audience Action

Map from `objective.primary` + `audience.primary.decision_authority`:

| Objective | Decision Authority | Action |
|-----------|-------------------|--------|
| decide | decider | decide |
| recommend | decider/influencer | approve |
| persuade (sales) | decider | purchase |
| persuade (investor) | decider | invest |
| teach | learner | learn |
| inform | reviewer | understand |
| align | influencer | align |
| explore | reviewer | investigate |

If no clear action → `none` (awareness only).

### 7. Delivery Mode Classification

From `context.delivery_mode` + signals:

| Signal | Mode |
|--------|------|
| "present", "meeting", "live", "speaker" | live_presentation |
| "send", "email", "pre-read", "distribute", "async" | self_guided_deck |
| "document", "report", "reference", "appendix" | document_like_deck |
| Both live and distribute | hybrid |
| Unknown | unknown |

**Implication for Reasoning:**
- `live_presentation` → Can rely on spoken explanation; slides can be sparser
- `self_guided_deck` → Slides must be self-explanatory; stronger signalling, more annotation
- `document_like_deck` → Dense, reference-oriented; appendix strategy important

### 8. Complexity & Slide Count Estimate

**Complexity Factors:**

| Factor | Weight |
|--------|--------|
| Number of distinct messages/arguments | +1 per |
| Evidence types required (data, diagram, case study) | +1 per type |
| Audience expertise = novice (needs more explanation) | +1 |
| Multiple secondary types | +1 per |
| Regulatory/high evidence burden | +1 |

**Complexity Bands:**
- 1–3 → simple
- 4–6 → moderate
- 7+ → complex

**Slide Count Estimate:**
- Simple: 8–12 slides
- Moderate: 12–20 slides
- Complex: 20–30 slides
- Cap at `request.constraints.max_slides` if set

### 9. Confidence Calculation

```
Base = Primary type confidence
+ 0.1 if secondary types have signals
+ 0.1 if expertise determined (not unknown)
+ 0.1 if evidence burden determined
+ 0.1 if delivery_mode determined (not unknown)
- 0.2 if any critical field = unknown
- 0.1 per assumption with risk_if_wrong ≥ high
Clamped to [0.0, 1.0]
```

## Decision Rules

- **MUST** classify after audience and objective are determined
- **MUST** produce multi-dimensional classification (not single label)
- **MUST** assess evidence burden per-claim, not just by type label
- **MUST** identify expected audience action
- **MUST** classify delivery_mode for downstream self-guided vs live decisions
- **SHOULD** use conservative classification when uncertain (assertion_evidence default)
- **MUST NOT** pretend certainty — if confidence < 0.6, record assumption and clarify

## Knowledge Consumption

- `knowledge/presentation_types/*.md` — Type profiles, defaults
- `knowledge/storytelling/narrative-patterns.md` — Type-narrative mapping
- `knowledge/universal/presentation-principles.md` — Classification pipeline step
- `PRESENTATION_CONSTITUTION.md` — Priority hierarchy for conflict resolution

## Clarification Triggers

Generate clarification when:
- Primary type confidence < 0.6 → "Is this primarily [A] or [B]?"
- Evidence burden ambiguous → "Do claims need high-evidence support (metrics, citations)?"
- Delivery mode unknown → "Will you present this live or send as a document?"
- Expected action unclear → "Should the audience decide, approve, learn, or just understand?"