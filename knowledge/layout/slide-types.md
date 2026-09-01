# Slide Types — Semantic Archetypes

## Purpose

Define semantic slide archetypes. Slide type MUST be selected AFTER semantic intent is determined.

## Slide Archetypes

### 1. Title Slide
| Aspect | Detail |
|--------|--------|
| **Purpose** | Identify presentation, presenter, context |
| **Content** | Title, Subtitle, Presenter, Role, Date, Event, Confidentiality |
| **Hierarchy** | Title (display) > Subtitle (h1) > Meta (body) |
| **Visual** | Minimal — logo, background image (meaningful only) |
| **Narrative Role** | Orientation |
| **Failure Modes** | Cluttered, missing metadata, generic title |

### 2. Section Divider
| Aspect | Detail |
|--------|--------|
| **Purpose** | Signal major narrative transition |
| **Content** | Section title, Optional: Section number, Progress indicator |
| **Hierarchy** | Section title (h1) centered |
| **Visual** | High whitespace, brand colour block, optional thematic image |
| **Narrative Role** | Segmentation, cognitive break |
| **Failure Modes** | Used as content slide, no progress context |

### 3. Agenda / Roadmap
| Aspect | Detail |
|--------|--------|
| **Purpose** | Set expectations, show structure |
| **Content** | Ordered sections, Time allocations, Current indicator |
| **Hierarchy** | Section titles (h2), Times (label), Current (accent) |
| **Visual** | Numbered list, Timeline, or Progress bar |
| **Narrative Role** | Navigation, Pretraining |
| **Failure Modes** | Too detailed, vague items, no timeboxes |

### 4. Assertion-Evidence
| Aspect | Detail |
|--------|--------|
| **Purpose** | Make claim + show proof |
| **Content** | Assertion (title), Evidence visual, Annotation, Implication, Source |
| **Hierarchy** | Assertion (h2) > Evidence (visual) > Annotation/Implication (label/accent) > Source (caption) |
| **Visual** | Chart, Diagram, Table, or Annotated image |
| **Narrative Role** | Core argument unit |
| **Failure Modes** | Topic title, No evidence, Evidence ≠ assertion, No implication |

### 5. Comparison
| Aspect | Detail |
|--------|--------|
| **Purpose** | Contrast items on criteria |
| **Content** | Criteria (rows), Options (columns), Values/Scores, Highlight |
| **Hierarchy** | Criteria (label) > Values (body) > Highlight (accent) |
| **Visual** | Table, Grouped bar, Dot plot, Radar (avoid) |
| **Narrative Role** | Decision support |
| **Failure Modes** | Biased criteria, Missing options, No recommendation |

### 6. Process / Flow
| Aspect | Detail |
|--------|--------|
| **Purpose** | Show sequential logic, decisions, branches |
| **Content** | Steps, Decisions, Swimlanes, Inputs/Outputs |
| **Hierarchy** | Flow direction (primary) > Step labels (label) > Decision logic (annotation) |
| **Visual** | Flow diagram (orthogonal, swimlanes) |
| **Narrative Role** | Mechanism explanation |
| **Failure Modes** | Spaghetti, Unexplained decisions, No start/end |

### 7. Architecture
| Aspect | Detail |
|--------|--------|
| **Purpose** | Show system structure, components, interfaces |
| **Content** | Components, Boundaries, Protocols, Data flows, External deps |
| **Hierarchy** | Container/Component (primary) > Interfaces (label) > Protocols (annotation) |
| **Visual** | C4-style architecture diagram (level-appropriate) |
| **Narrative Role** | Technical structure |
| **Failure Modes** | Mixed levels, Unexplained boxes, Missing protocols |

### 8. Timeline / Milestone
| Aspect | Detail |
|--------|--------|
| **Purpose** | Show temporal sequence, phases, key dates |
| **Content** | Time axis, Events/Milestones, Phases, Status |
| **Hierarchy** | Time axis (primary) > Milestones (label) > Phase bands (background) |
| **Visual** | Horizontal timeline (proportional), Phase swimlanes |
| **Narrative Role** | Chronological narrative |
| **Failure Modes** | Equal spacing for unequal intervals, Event dump, No insight |

### 9. Chart / Data
| Aspect | Detail |
|--------|--------|
| **Purpose** | Show data relationship (trend, comparison, distribution, etc.) |
| **Content** | Chart + Assertion title + Annotation + Source |
| **Hierarchy** | Assertion (h2) > Chart (visual) > Annotations (label/accent) > Source (caption) |
| **Visual** | Per chart-selection.md |
| **Narrative Role** | Evidence for claim |
| **Failure Modes** | Chart without assertion, Legend-dependent, No uncertainty |

### 10. Table
| Aspect | Detail |
|--------|--------|
| **Purpose** | Exact lookup, detailed comparison, precise values |
| **Content** | Headers, Rows, Selective emphasis, Source |
| **Hierarchy** | Headers (label) > Data (body) > Emphasis (accent) |
| **Visual** | Styled table (per tables.md) |
| **Narrative Role** | Reference, Decision detail |
| **Failure Modes** | Spreadsheet dump, Misaligned numbers, No units |

### 11. KPI / Metric Tile
| Aspect | Detail |
|--------|--------|
| **Purpose** | Show single metric status at a glance |
| **Content** | Metric name, Current value, Status (RAG), Trend sparkline, Target, Period |
| **Hierarchy** | Value (display/h1) > Status (accent) > Trend (label) > Context (caption) |
| **Visual** | Tile/card layout, Sparkline, Status indicator |
| **Narrative Role** | Health monitoring, Executive scan |
| **Failure Modes** | No target/context, Status colour-only, Cluttered |

### 12. Case Study / Proof
| Aspect | Detail |
|--------|--------|
| **Purpose** | Demonstrate outcome via customer/example |
| **Content** | Customer context, Problem, Solution, Results (metrics), Quote |
| **Hierarchy** | Outcome metric (h2) > Customer context (body) > Results (KPI tiles) > Quote (annotation) |
| **Visual** | Customer logo, Result metrics, Quote card |
| **Narrative Role** | Social proof, Evidence |
| **Failure Modes** | Generic/no metrics, Irrelevant segment, No permission |

### 13. Quote / Testimonial
| Aspect | Detail |
|--------|--------|
| **Purpose** | Authority/voice of customer |
| **Content** | Quote, Attribution (Name, Role, Company), Photo (optional) |
| **Hierarchy** | Quote (h2/body, italic) > Attribution (label) |
| **Visual** | Quote marks, Photo, Clean typography |
| **Narrative Role** | Credibility, Emotional connection |
| **Failure Modes** | Generic quote, No attribution, Fake/embellished |

### 14. Image-Led
| Aspect | Detail |
|--------|--------|
| **Purpose** | Visual as primary evidence (screenshot, photo, render) |
| **Content** | Image, Assertion title, Annotations/Callouts, Source |
| **Hierarchy** | Assertion (h2) > Image (visual) > Callouts (label/accent) |
| **Visual** | Full-bleed or framed image, Direct callouts |
| **Narrative Role** | Visual proof |
| **Failure Modes** | Decorative image, No callouts, Low quality |

### 15. Recommendation / Decision
| Aspect | Detail |
|--------|--------|
| **Purpose** | Drive specific decision |
| **Content** | Decision needed, Recommendation, Rationale (3 bullets), Risks, Next steps (Owner/Date) |
| **Hierarchy** | Decision (h2) > Recommendation (h3) > Rationale (body) > Next steps (label/accent) |
| **Visual** | Decision box, Risk table, Next step cards |
| **Narrative Role** | Decision point |
| **Failure Modes** | No clear ask, Buried recommendation, Vague next steps |

### 16. Conclusion / Summary
| Aspect | Detail |
|--------|--------|
| **Purpose** | Reinforce key messages, close |
| **Content** | 3–5 Key takeaways (aligned to objectives), Next steps, Thank you / Contact |
| **Hierarchy** | Takeaways (h3) > Next steps (label) > Contact (caption) |
| **Visual** | Numbered list, Callback to objective |
| **Narrative Role** | Closure, Reinforcement |
| **Failure Modes** | New information, Generic "thank you," No callback |

### 17. Appendix / Reference
| Aspect | Detail |
|--------|--------|
| **Purpose** | Backup detail, not presented live |
| **Content** | Detailed tables, Full methodology, Extended charts, Glossary, Sources |
| **Hierarchy** | Section label (h2) > Content (body/label) |
| **Visual** | Dense but structured, Clear section tabs |
| **Narrative Role** | Reference, Verification |
| **Failure Modes** | Presented as main content, Disorganized, Not referenced |

## Type Selection Rules

1. **Determine slide intent** (assert, compare, explain, decide, navigate, reference)
2. **Select archetype** matching intent
3. **Populate required content** per archetype
4. **Apply hierarchy** per archetype
5. **Validate** against failure modes

## Handoff to Other Layers

- **Reasoning (select_slide_type):** Implements selection rules
- **Narrative-patterns:** Maps pattern steps to archetypes
- **Composition:** Implements layout per archetype
- **Generation:** Produces PPTX slide from archetype spec
- **Evaluation:** Checks: Archetype match, Required content, Hierarchy, Failure modes