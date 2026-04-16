# Ecosystem

The LF Energy project ecosystem, including project overviews and the taxonomy that organizes them.

## Structure

- `taxonomy.md` — Defines how projects are categorized (Grid Segment, Function, Industry Solution Categories, Cross-Cutting Tags)
- `projects/` — Individual project knowledge bases and overviews
- `projects/_template/` — Template for new project overviews
- `projects/glossary.md` — Industry terms and acronyms used across overviews
- `projects/AGENTS.md` — Documentation process and editorial guidelines for project overviews

## Taxonomy

The taxonomy (`taxonomy.md`) is the authoritative reference for project categorization. Key principles that informed its design:

### Categorize by what a project does, not how it's built

Function categories describe the grid problem a project solves. AI/ML, specifications, and microservices are methods — they don't determine category. A load forecasting tool built with ML belongs in Grid Operations (because it supports operational decisions), not in an "AI" category. An API specification for ratings exchange belongs in Grid Operations (because it enables operations), not in a "Standards" category.

### Grid Segment is physical, not functional

Grid Segments (Generation, Transmission, Distribution, Behind the Meter) describe where on the energy system a project operates. Markets was deliberately excluded as a segment because it's an activity that cuts across physical locations, not a location itself. Market-facing functionality is captured by the Flexibility & Markets function category.

### Subcategories use em dash format

Two subcategories exist: `Grid Operations — Substation Digitalization` and `Flexibility & Markets — EV Charging`. These are called out because they represent distinct, recognized utility investment domains. The format in project overviews is the parent category, em dash, subcategory name.

### Multi-tagging is allowed but minimized

Projects can appear in multiple Grid Segments and (rarely) multiple Function categories. When multi-tagged, indicate primary vs. secondary. The goal is a taxonomy where most projects have one clear home — if too many projects need multi-tagging, the categories likely need revision.

### Industry Solution Categories are supplementary

Industry Solution Categories (EMS, ADMS, DERMS, etc.) provide an additional navigation path for utility engineers who think in terms of systems they buy and build. They are not the primary taxonomy — they supplement Grid Segment and Function. Not all projects map to one, and that's fine.

### Borderline decisions are documented

When a project could reasonably fit in more than one function category, the reasoning for the chosen placement is documented in taxonomy.md under "Notes on specific placements" within the relevant category. This preserves context for future reviewers. When new information arrives, these documented decisions can be revisited with full context.

### Cross-cutting tags supplement the primary taxonomy

Three cross-cutting tags (Project Intent, AI/ML, Deliverable Type) provide additional filtering dimensions that cut across Grid Segment and Function. These answer different questions: "Is this a research platform or something I can deploy?", "Is AI core to this project?", "Am I adopting a spec or running software?" See taxonomy.md for definitions, allowed values, and the full project mapping.

Key distinctions:
- **Project Intent (Applied/Research)** describes purpose, not maturity. A Research project can be mature software (Grid2Op); an Applied project can be early stage (GEISA). Research means the project exists to advance knowledge or enable experimentation, not that it's immature.
- **AI/ML** uses the test "Would this project exist without AI/ML?" Projects that use ML as one technique among many (e.g., FlexMeasures) don't qualify. Projects that provide environments for AI research but contain no AI themselves (e.g., Grid2Op) also don't qualify.
- **Deliverable Type** is based on primary output. Most specification projects ship code (reference implementations, conformance tests, client libraries) — the tag reflects what adopters are fundamentally adopting, not whether code exists.

### Some projects won't fit

The taxonomy doesn't need to accommodate every project perfectly. Energy-adjacent projects (covXtreme, Battery Data Alliance) may not map to a grid segment or function category. That's acceptable — forcing a fit would dilute the taxonomy's precision.