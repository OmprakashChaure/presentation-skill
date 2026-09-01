# Technical Presentation Type

## Purpose

Define type-specific policies for technical presentations.

## Scope

Architecture reviews, design docs, API presentations, system deep-dives, technical proposals, incident retrospectives, RFC presentations.

## Core Policies

### Technical Precision

- **MUST** use precise terminology — no hand-waving
- **MUST** define domain-specific terms on first use (or reference glossary)
- **MUST** distinguish: specification vs implementation vs behavior
- **Anti-pattern:** "Fast," "Scalable," "Robust" without metrics

### Terminology

- **Glossary slide** in appendix for >10 domain terms
- **Consistent naming:** Same component = same name everywhere
- **Acronyms:** Define on first use; avoid unexplained TLAs

### Architecture & Mechanisms

- **Default visual:** Architecture diagram (system context → container → component → code)
- **MUST** show: Components, relationships, data flows, boundaries, protocols
- **MUST** label: Responsibilities, interfaces, data contracts, SLAs
- **Anti-pattern:** Boxes without labels; arrows without protocol/direction

### Workflows & Processes

- **Default visual:** Sequence diagram or flow diagram
- **MUST** show: Actors, steps, decision points, error paths, timeouts, retries
- **MUST** distinguish: Happy path vs error handling vs compensation

### Evidence Standards

| Claim Type | Required Evidence |
|------------|-------------------|
| Performance | Benchmark methodology, hardware, workload, percentiles (p50/p95/p99) |
| Scalability | Load test config, bottleneck identification, scaling curve |
| Correctness | Test coverage, property-based tests, formal verification scope |
| Security | Threat model, attack surface, mitigations, audit results |
| Reliability | Failure modes, MTBF/MTTR, chaos experiment results |

### Constraints & Trade-offs

- **MUST** explicitly state: Constraints (hard limits), Trade-offs (design decisions), Assumptions
- **Format:** "We chose X over Y because [reason]; trade-off: [downside]"
- **Rule:** No design decision without documented trade-off

### Failure Modes

- **SHOULD** include: "What happens when..." slides
- **Cover:** Dependency failure, data corruption, network partition, overload, config error
- **Visual:** Failure mode → Detection → Mitigation → Recovery

### Implementation Details

- **Level:** Match audience (architects = interfaces/contracts; engineers = code patterns)
- **MUST** show: Key algorithms, data structures, config, deployment topology
- **Anti-pattern:** Code dumps without explanation

### Limitations

- **MUST** declare: Known limitations, unsolved problems, future work
- **Rule:** Honesty about limitations builds credibility

## Slide Type Defaults

| Purpose | Slide Archetype |
|---------|-----------------|
| System overview | Architecture diagram |
| Component detail | Assertion-Evidence (diagram + spec) |
| Data flow | Flow/Sequence diagram |
| API contract | Table (endpoint, method, params, response, errors) |
| Performance | Chart (benchmark results) |
| Trade-off | Comparison table |
| Failure mode | Process diagram (failure → detection → recovery) |
| Limitations | Reference/List |

## Narrative Default

- **Primary:** Assertion-Evidence (per slide)
- **Deck-level:** Problem-Solution (for proposals) or Chronological (for retrospectives)
- **Executive summary:** Pyramid (if leadership audience)

## Design Adaptations

- **Density:** Higher — technical audience tolerates detail
- **Diagrams:** Precise, labelled, consistent notation (C4, UML, Mermaid-style)
- **Tables:** Preferred for exact specs (APIs, configs, schemas)
- **Colour:** Semantic (not decorative) — protocol layers, service boundaries, data classification

## Anti-Patterns

- Marketing language in technical deck ("revolutionary," "seamless")
- Architecture diagram without labels/protocols
- Benchmark without methodology
- Trade-off not stated
- Failure modes ignored
- Code snippets without context
- Acronyms undefined
- "It works on my machine" as evidence

## Handoff to Other Layers

- **Reasoning:** Selects assertion-evidence as slide default; problem-solution for proposals
- **Visualization:** Architecture/flow diagrams as primary evidence visuals
- **Diagrams:** Strict notation standards (C4, sequence, deployment)
- **Charts:** Benchmarks, scaling curves, latency distributions
- **Evaluation:** Checks precision, evidence, trade-offs, failure modes, limitations