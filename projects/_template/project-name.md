<!-- Filename: use the project name in kebab-case, e.g. power-grid-model.md, powsybl.md -->

# PROJECT NAME

**Last Updated:** YYYY-MM-DD

## Table of Contents

<!-- Create and update table of contents from headers below -->

## Basic Info

- LF Energy webpage:
- Website:
- Code:
- Documentation:
- Calendar:
- LinkedIn:
- Community:
	- Mailing List:
	- Slack: 
- LFX Insights:
- Other:

## Description

Short 1 sentence description of the project

<!-- Keep it simple, no jargon. Think "elevator pitch" for utility engineers. "Open source" is redundant, no need to emphasize that.
Describe what the project DOES, not where it's currently adopted. Don't scope by geography or current user base.
Example: "Production-grade machine learning system for automated short-term energy load forecasting."
NOT: "Open source ML-based forecasting solution leveraging XGBoost for predictive analytics."
NOT: "Framework for European grid modeling" (when the technology is general-purpose) -->

## Overview

2-3 paragraph overview in plain language for utility engineers. What is this project? What problem does it solve? Who uses it?

<!--
Paragraph 1: What is it? (technology + use case)
Paragraph 2: Why does it matter? (problem solved, value proposition)
Paragraph 3: How is it used? (deployment model, who uses it)
Write for operations engineers, not software developers.
Include any relevant diagrams to aid understanding.
-->

## Technical Profile

### What It Does

Brief description of technical function

<!-- 1-2 sentences max. Focus on WHAT it does, not HOW it works technically. -->

### Problem(s) Solved

The specific operational/technical problem(s) this addresses from a utility perspective

<!-- Frame from utility operator perspective, not technology perspective.
Example: "Enables utilities to forecast load without data science expertise"
NOT: "Provides ML pipeline for time-series prediction" -->

### Key Capabilities

- Capability 1
- Capability 2
- Capability 3

<!-- List key technical capabilities. Focus on outcomes/features, not implementation details. -->

### Relevant Standards

- Standard A
- Standard B

<!-- Only list standards the project directly implements or supports as a core feature.
Do NOT list standards that are merely adjacent, upstream, or used by dependencies.
Test: Could this project appear in a compliance or conformance discussion for this standard?
Important distinction: hosting, configuring, or requiring a standard is NOT the same as implementing it.
Example: A virtualization platform that hosts IEC 61850 applications does not implement IEC 61850.
Example: A platform that configures PTP (IEEE 1588) for time sync does not implement IEEE 1588.
When in doubt, omit — it's better to undercount than to overclaim.
Limit to major, industry-recognized standards (IEC, IEEE, ISO, IETF, etc.) -->

## Grid Context

### Grid Segment

Generation, Transmission, Distribution, Behind the Meter

<!-- Where on the energy system does this project operate? List all applicable segments.
Indicate primary vs. secondary if relevant (e.g., "Distribution (primary), Transmission (secondary)").
Some projects are energy-adjacent and don't map to a grid segment — that's fine.
See taxonomy.md for full definitions. -->

### Function

Grid Modeling & Simulation | Grid Operations | Flexibility & Markets | Interoperability & Data

<!-- What does this project do for the energy system? Most projects have one primary function.
Multi-tagging is allowed but should be minimized — indicate primary vs. secondary when used.

Subcategories are indicated with an em dash:
  Grid Operations — Substation Digitalization
  Flexibility & Markets — EV Charging

See taxonomy.md for full definitions, allowed values, and placement rationale. -->

### Industry Solution Categories

#### Solution Type

- Category: Brief description of how the project serves this solution type.

<!-- What the project fundamentally IS as a solution category. Most projects will have one. -->

#### Component of

- Category: Brief description of how the project fits into this broader solution.

<!-- Broader utility solution categories where this project could be used as a building block. These help utility engineers understand positioning — e.g., a DSO looking for ADMS-related projects would find this. -->

### Cross-Cutting Tags

- **Project Intent:** Applied | Research
- **AI/ML:** Yes | No
- **Deliverable Type:** Specification | Software | Data

<!-- See taxonomy.md "Cross-Cutting Tags" section for definitions and the test for each tag.
- Project Intent: Applied = aims to be used in real energy systems; Research = exists to advance knowledge or enable experimentation
- AI/ML: Yes only if AI/ML is core to the project's purpose ("Would this project exist without AI/ML?")
- Deliverable Type: Based on primary output — what you're adopting when you adopt this project -->

## Related Projects

- **Project A**: How they complement each other
- **Project B**: Integration relationship
- **Project C**: Depends on Project X for Y functionality (if applicable)
- **Project D**: How they differ or overlap

<!-- 
Related Projects entries should reflect genuine technical relationships (integration points, complementary functions, shared data flows) — not merely shared adopters or co-location within the same organization.

Be specific about relationships:
- "Works with": Technical integration (APIs, data exchange)
- "Similar to": Overlapping scope—explain the difference
- "Builds on": Dependency relationship
- "Complements": Use together for fuller solution
Examples:
- "FlexMeasures: OpenSTEF predicts load, FlexMeasures optimizes flexibility to manage it"
- "GridFM: Both use ML for grid; OpenSTEF is specialized forecasting, GridFM is general foundation models"
-->

## Maturity & Adoption

### LF Energy Stage

Sandbox | Incubation | Early Adoption | Graduated | Emeritus

<!-- Check LF Energy project page or TAC records for official stage. -->

### Deployment Maturity

R&D | Piloting | Production

<!--
- R&D: Pre-production; not yet deployed in any utility production environment
- Piloting: Deployed in production by utilities, but limited in scale or scope (e.g., single region, specific use case, trial basis)
- Production: One or more utilities running in production to plan or operate the grid
-->

### Supporting / Adopting Organizations

## Learn More

- [Title](URL)
	- Date: YYYY-MM-DD
	- Type: Case Study | Presentation | Blog Post | Webinar

<!-- Curated list of the best external links to share for this project.
Include case studies, blog posts, webinars, conference talks, and other shareable content. -->

## Additional Notes

<!--
Non-obvious context that affects how this project should be understood or positioned.
This is NOT for information that fits in sections above.

Good examples:
- Strategic positioning (e.g., "only open source implementation of X")
- Structural adoption factors (e.g., regulatory drivers, skill availability)
- Geographic relevance differences
- Common misconceptions about scope

Avoid:
- Development history or roadmap
- Information that duplicates Overview, Technical Profile, or Grid Context
- Time-sensitive content (events, upcoming releases)
- Detailed competitive analysis (brief strategic positioning that references proprietary alternatives is OK — e.g., identifying the incumbent solution the project replaces — but avoid feature-by-feature comparisons)
-->