# Composition

## Purpose

Define composition principles — focal point, visual weight, grouping, balance, alignment, whitespace, reading path, evidence placement, hierarchy.

## Core Principles

### 1. Focal Point

- **MUST** have exactly ONE primary focal point per substantive slide
- **Location:** Top-left quadrant (Z-pattern entry) for assertion slides
- **Creation:** Size + Contrast + Whitespace isolation + Position
- **Rule:** Focal point = Slide assertion (title) for assertion-evidence slides

### 2. Visual Weight Distribution

| Element | Weight Factors | Typical Weight |
|---------|----------------|----------------|
| Assertion title | Size (h2), Bold, Position (top), Isolation | HIGH |
| Chart/Diagram | Area, Contrast, Detail density | HIGH |
| KPI Value | Size (display/h1), Bold, Colour | HIGH |
| Body text | Size (body), Regular, Density | MEDIUM |
| Labels/Annotations | Size (label), Accent colour | MEDIUM-LOW |
| Source/Footer | Size (caption), Muted colour | LOW |

**Rule:** No more than 2 HIGH-weight elements. If 2, they must be assertion + evidence (intended pairing).

### 3. Grouping & Proximity

- **Gestalt Law:** Elements close together = perceived as related
- **Grid enforcement:** Related elements share column span; unrelated separated by ≥space-lg
- **Explicit grouping:** Background tint, Border, Connector line, Shared alignment
- **Rule:** Grouping MUST reflect semantic relationship

### 4. Balance

| Type | Rule | Use Case |
|------|------|----------|
| **Asymmetric (Default)** | Visual weight balanced across vertical axis; not mirror | Assertion-Evidence, Comparison, Most slides |
| **Symmetric** | Mirror left/right or top/bottom | Title, Section divider, KPI row |
| **Radial** | Elements around center | Rare — only for hub-and-spoke diagrams |

**Rule:** Asymmetric balance = professional, dynamic. Symmetric = formal, static.

### 5. Alignment

- **Grid alignment:** All elements snap to column edges + baseline grid
- **Optical alignment:** Visual centers align (not just bounding boxes)
- **Edge alignment:** Related elements share left/right/top/bottom edges
- **Rule:** Alignment drift (1–2px off) = unprofessional — grid prevents this

### 6. Whitespace

- **Active, not empty:** Whitespace creates hierarchy, grouping, breathing room
- **Macro:** Safe margins, Zone gaps (space-lg to space-2xl)
- **Micro:** Element padding (space-sm), Line height, Paragraph spacing
- **Rule:** Generous whitespace around focal point increases perceived importance

### 7. Reading Path

- **Default (LTR):** Z-pattern — Top-left → Top-right → Bottom-left → Bottom-right
- **Guided:** Numbered steps, Arrows, Connector lines, Progressive builds
- **Rule:** Reading path MUST match logical argument flow

### 8. Evidence Placement (Assertion-Evidence Slides)

| Layout | Assertion | Evidence | Annotation | Implication | Source |
|--------|-----------|----------|------------|-------------|--------|
| **Standard** | Top (cols 1–12) | Middle (cols 1–8 or 1–12) | On evidence | Right of evidence (cols 9–12) or below | Bottom (caption) |
| **Vertical** | Top | Below (full width) | On evidence | Below evidence | Bottom |
| **Sidebar** | Top (cols 1–8) | Right (cols 9–12) | On evidence | Below evidence | Bottom |

**Selection:** Based on evidence aspect ratio (wide → standard/vertical; tall → sidebar)

## Anti-Patterns (MUST PREVENT)

| Anti-Pattern | Detection | Correction |
|--------------|-----------|------------|
| Centred-everything | All elements centered | Default left-align; center only for symmetric archetypes |
| Equal-weight layouts | Multiple HIGH-weight elements competing | Enforce 1 focal point; demote others |
| Accidental overlaps | Elements intersect unintentionally | Grid validation; z-order check |
| Decorative clutter | Non-semantic lines, shapes, icons | Remove; every element must have semantic role |
| Floating elements | Not aligned to grid or group | Snap to grid; assign to zone |
| Weak focal point | No clear entry point | Boost assertion size/isolation; reduce competitors |

## Composition by Archetype

| Archetype | Focal Point | Balance | Reading Path |
|-----------|-------------|---------|--------------|
| Title | Title (center) | Symmetric | Center → Meta |
| Section Divider | Section title (center) | Symmetric | Center |
| Assertion-Evidence | Assertion (top-left) | Asymmetric | Assertion → Evidence → Annotation → Implication |
| Comparison | Criteria (left) | Asymmetric | Criteria → Option A → Option B → Highlight |
| Process | Flow start (top-left) | Asymmetric | Follow flow arrows |
| Architecture | Primary component (center-left) | Asymmetric | Center → Outward |
| Timeline | Time axis (left) | Asymmetric | Left → Right |
| KPI Tile | Value (center) | Symmetric (per tile) | Value → Status → Trend |
| Recommendation | Decision (top) | Asymmetric | Decision → Rec → Rationale → Next Steps |

## Handoff to Other Layers

- **Grids:** Consumes grid zones, alignment anchors, spacing tokens
- **Visual-hierarchy:** Implements tier weights (primary/secondary/tertiary)
- **Slide-types:** Defines composition per archetype
- **Responsive-layout:** Adapts composition for density variants
- **Generation:** Positions elements per composition spec
- **Evaluation:** Checks: Single focal point, Grid alignment, Balance, Reading path, Whitespace, Anti-patterns