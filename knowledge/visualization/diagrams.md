# Diagrams

## Purpose

Define diagram types, creation rules, and quality standards for presentation diagrams.

## Scope

Process, flow, architecture, hierarchy, relationship, system diagrams.

## Diagram Type Taxonomy

| Type | Purpose | Core Elements |
|------|---------|---------------|
| **Process** | Sequential steps, decisions, branches | Steps, Decisions, Start/End, Swimlanes |
| **Flow** | Data/material/information movement | Nodes (processes/stores), Flows, External entities |
| **Architecture** | System structure, components, interfaces | Components, Relationships, Boundaries, Protocols |
| **Hierarchy** | Parent-child, classification, org | Nodes, Links, Levels, Grouping |
| **Relationship** | Entity connections, networks | Nodes, Edges, Attributes, Clusters |
| **System** | Holistic view: context, containers, components, code | Context, Containers, Components, Code (C4) |

## Creation Rules (MUST Follow Sequence)

```
1. RELATIONSHIP FIRST
   Define: What relationships must the audience understand?
   (Not: "I need a flowchart" — but "Audience must see how data flows from A to B")

2. DIAGRAM TYPE
   Select type based on relationship:
   - Sequential logic → Process
   - Data movement → Flow
   - System structure → Architecture (C4 level appropriate)
   - Classification → Hierarchy
   - Network effects → Relationship
   - Multi-level system → System (C4)

3. STRUCTURE
   - Define nodes (entities) and edges (relationships)
   - Group by: Layer, Domain, Swimlane, Cluster
   - Limit: ≤7±2 nodes per level (cognitive load)
   - Hierarchy: Max 3 levels visible; detail in appendix

4. LABELS
   - Every node: Name + Type (Service, DB, Queue, Actor)
   - Every edge: Protocol / Data / Trigger / Frequency
   - No acronyms without legend/definition
   - Label placement: Adjacent, not overlapping, readable

5. CONNECTORS
   - Style: Solid (sync), Dashed (async), Dotted (dependency)
   - Arrow: Direction of flow/control
   - Routing: Orthogonal, minimal crossings
   - Crossings: Bridge/hop if unavoidable

6. HIERARCHY & SIMPLIFICATION
   - Show: Level appropriate to audience (exec=context, eng=component)
   - Hide: Internal details not relevant to message
   - Abstract: Group related nodes into super-nodes
   - Consistency: Same notation across all diagrams in deck
```

## Notation Standards

### Architecture (C4-Inspired)

| Level | Scope | Audience | Notation |
|-------|-------|----------|----------|
| **Context** | System + External actors | Executive, Stakeholder | Box (system) + Stick figures (actors) + Lines |
| **Container** | Deployable units (API, DB, Frontend) | Architect, Tech Lead | Boxes (containers) + Labels (tech) + Lines (protocols) |
| **Component** | Internal modules | Engineer | Boxes (components) + Interfaces + Lines |
| **Code** | Classes, functions | Developer | UML class / Sequence |

**Rule:** One level per diagram. Cross-level = separate diagrams.

### Process/Flow

- **Start/End:** Rounded rectangle (terminal)
- **Step:** Rectangle
- **Decision:** Diamond (Yes/No labelled)
- **Swimlane:** Horizontal/vertical bands (Actor/System)
- **Connector:** Solid arrow (flow), Dashed (info flow)

## Quality Rules

### MUST HAVE

- [ ] Title = Assertion (what this diagram shows)
- [ ] Every node labelled (Name + Type)
- [ ] Every connector labelled (Protocol/Data/Direction)
- [ ] Legend if >3 node types or connector styles
- [ ] Source/version/date (bottom, caption)
- [ ] Fits safe margins (no clipping)

### MUST NOT HAVE

- [ ] Unexplained boxes (mystery shapes)
- [ ] Spaghetti connectors (excessive crossings, no routing)
- [ ] Decorative elements (gradients, shadows, 3D, clip art)
- [ ] Paragraphs reproduced as diagram text
- [ ] Inconsistent notation within deck
- [ ] Acronyms without definition

## Simplification Techniques

| Technique | When |
|-----------|------|
| Group into super-nodes | >7 nodes at same level |
| Hide internal edges | Audience needs structure not wiring |
| Use appendix for detail | Main deck shows context; detail in backup |
| Abstract repeated patterns | "3× Worker" not 3 separate boxes |
| Elide trivial nodes | Load balancer, API gateway if not the point |

## Anti-Patterns

- Diagrams that merely reproduce paragraphs (text in boxes)
- Unexplained notation (audience guesses meaning)
- Mixed abstraction levels (context + code in one diagram)
- Connector spaghetti (no routing, many crossings)
- Decorative styling (gradients, shadows, 3D)
- Missing protocol/data labels on connectors
- No title/assertion

## Handoff to Other Layers

- **Reasoning (select_visualization):** Chooses diagram type from relationship
- **Diagrams generation:** Produces diagram specs (Mermaid/PlantUML/Draw.io XML)
- **Visual-hierarchy:** Diagram = secondary (evidence); assertion = primary
- **Composition:** Diagram placement, sizing, whitespace
- **Evaluation:** Checks: Assertion title, labels, connectors, notation consistency, simplification, safe margins