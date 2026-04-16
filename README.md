# LF Energy Project Ecosystem

A centralized knowledge base for the LF Energy project ecosystem. Contains project overviews and a taxonomy for categorization.

## What's Here

- **`taxonomy.md`** — Defines how projects are categorized by Grid Segment, Function, Industry Solution Category, and Cross-Cutting Tags. This is the authoritative reference for project classification.
- **`projects/`** — Individual project directories, each containing an overview (`project-name.md`) and optionally a `context/` folder for local reference material used to produce and maintain the overview. Context folders are gitignored — see below.
- **`projects/_template/`** — Template and guidelines for creating new project overviews.
- **`projects/glossary.md`** — Industry terms and acronyms used across overviews.

## How to Use

Project overviews are written for engineers and are intended as source material — a shared factual foundation that feeds derivative works like website copy, presentations, and marketing collateral.

The taxonomy provides a structured way to navigate the ecosystem by where a project operates on the grid, what function it serves, and what industry solutions it relates to.

To use with AI tools, point them to `AGENTS.md` and `projects/AGENTS.md`. For example, for Claude, create `CLAUDE.md` and `projects/CLAUDE.md` files that says `See AGENTS.md`. Please do not commit agent-specific files to the repo.

## Maintenance

This knowledge base is owned and maintained by LF Energy staff. Updates are made on a regular cadence and at significant project milestones (e.g., major releases). Individual projects are consulted for review as part of the update process.

## Context Folders

Each project directory may contain a `context/` folder with reference material — presentation slides, case studies, code snapshots, and other source material used when creating and updating overviews. These folders are **gitignored** and not part of the public repository because the material is typically copyrighted by its respective authors.

If you're working on overviews locally, store relevant reference material in `projects/<project-name>/context/`. The folder structure mirrors the project directories.

## Contributing

Changes are made via pull request. For updates to a project overview, the relevant project TSC will be added as a reviewer. If you spot something that needs correcting, open a PR or an issue.
