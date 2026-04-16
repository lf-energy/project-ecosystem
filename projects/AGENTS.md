## Project Name Aliases

Some project names contain special characters. When searching, always check both forms:

- **dynaωo** (omega symbol) — also written as **dynawo** in plain ASCII. Directory: `dynaωo/`, overview: `dynaωo.md`. File system searches for "dynawo" will not match — always use the omega variant `dynaωo` when globbing or grepping. dynaωo / dynawo are often used interchangeable in project material.

## Overview

- The directories here represent knowledge bases for each project in the LF Energy ecosystem.
- The `PROJECT-NAME.md` (with PROJECT-NAME replaced with the actual project name) is the synthesized overview that includes references to relevant information, and a summary of what the project is, does, and how it fits within LF Energy and the broader digital energy landscape.
- Each project directory may contain a `context/` folder with reference material (presentations, case studies, code snapshots, etc.) used to produce the overview. **When creating or updating a project overview, always check for a `context/` folder and read any relevant material there first.** These files are gitignored and not part of the public repository, but they are valuable primary and secondary sources.
- This is technical information on each project and the project ecosystem as a whole.
- Target audience are utility engineers, not software developers.
- Assume a base level of expertise of utility digital systems
- Prioritize quality and accuracy. Do not guess to fill in gaps or missing info.
- Double check your work to ensure high quality information.
- Different sources of information have different levels of quality and therefore receive different levels of trust and credibility
	- Source code and the technical standards are primary sources that defines what the project actually does. High credibility.
	- Documentation, if well maintained, is also a high quality and credibility source
	- Marketing websites, presentations, case studies, white papers, etc are usually derivative works that are useful for understanding how to message and talk about a project, but are not always factually correct. These should be trusted less than source code and documentation.

## Documentation Process

Document creation is human-led, agent-assisted. The agent is meant to be an assistant through editing, researching, fact-checking, and critiquing, not by being the primary author.

### Workflow

Do not skip steps, go in the order defined below.

1. **Human creates skeleton**: Fill in links to source material, rough entries, and any known details. This will usually be an unpolished, incomplete first draft.
2. **Agent researches and drafts**: Fill in details, edit and polish text, ask questions for clarification, and serve as a thought partner. Research code, documentation, presentations, and project pages — in parallel where possible. Use the **cto** skill as a thought partner for technical framing, Grid Segment and Function classification, Industry Solution Category decisions, and cross-cutting tag assignments. Refer to `ecosystem/taxonomy.md` for allowed values and placement rationale.
	1. Always review the code and documentation to ensure they are in context. Remember that they are considered the highest quality sources of information unless indicated otherwise.
	2. **Inaccessible sources**: If a provided data source cannot be accessed (private repository, JavaScript-rendered page, authentication-required URL, etc.), stop and ask the user for help rather than silently proceeding without it. These sources were provided for a reason and may contain key information. The user can provide a local copy, screenshot, or alternative access path.
	3. **Before drafting**, read `_template/project-name.md` for understanding the whole template and `ecosystem/taxonomy.md` for the project taxonomy (Grid Segment, Function, Industry Solution Categories). Also read at least two existing completed overviews for precedent on how fields are used in practice. Grid Segment and Function are distinct axes with specific allowed values defined in the taxonomy — do not invent new options without discussion.
3. **Human reviews draft**: Flag what to keep, cut, or reframe. Agent adjusts.
4. **QA review**: Use the **technical-qa** skill. Systematically fact-check claims against primary sources. Flag unverified, inaccurate, inconsistent, or misleading items. Check that secondary-source claims (presentations, marketing) are appropriately contextualized (e.g., "as of September 2024") and not presented as verified fact.
5. **Cross-overview consistency review**: Compare formatting, conventions, terminology, and structure against existing completed overviews. Check for reciprocal cross-references in Related Projects. Related Projects entries should reflect genuine technical relationships (integration points, complementary functions, shared data flows) — not merely shared adopters or co-location within the same organization.
6. **Pressure-test Industry Solution Categories**: Use the **cto** skill to verify each category passes the tests described below.
7. Update `glossary.md` in the parent directory with any new industry terms or standards.
8. Update the table of contents and update timestamp for the document.
9. Review this project overview in the context of all project overviews to ensure consistency and accuracy across all of them. This may require updating other project overviews.

### Industry Solution Categories

- **Solution Type** should map to a recognized product/platform category (e.g., "Network Analysis", "Virtualization Platform", "IoT Device Management Platform").
- **Component of** entries must be genuine industry solution categories that a utility engineer would search for (e.g., AMI, ADMS, EMS, Digital Substation). These are the broader systems where this project serves as a building block. Use cases and workflows (e.g., "Congestion Management") are not product categories — they describe *how* a project is used, not *what* it is a component of.
- Prefer fewer, accurate categories over comprehensive but stretched ones.
- Test: Would a utility engineer shopping for this category expect to find this project? If not, drop it.
- Non-grid use cases (e.g., public lighting) that are factually correct but outside the target audience's frame of reference should generally be omitted from categories, even if they are a major use case of the project.
- **Component of Nesting**: If categories form a chain (e.g., project → M&V Platform → DSM Program Management), list only the immediate parent. Listing the full chain overstates the project's scope and dilutes discoverability.

### Describing Capabilities

Describe what a project delivers as its output, not its internal processing steps. Intermediate computations that feed into the primary output are implementation details, not independent capabilities. For example, if a forecasting project runs solar generation models as an input to its load forecast, the capability is "load forecasting that accounts for behind-the-meter generation" — not "load forecasting and generation forecasting."

### Standards Conformance Language

When a project partially implements a standard, use "based on" rather than "per" or "implements." "Per" and "implements" imply full conformance; "based on" accurately reflects partial or in-progress implementation.

### Plugin and Extension Provenance

When a project uses a plugin architecture, distinguish core capabilities from community-contributed extensions. Presenting contributed plugins as core capabilities overstates what a generic deployment includes out of the box. Use qualifiers like "(available as a community-contributed plugin)" in Key Capabilities.

### Competitor Product Naming

Do not name specific proprietary competitor products (e.g., "ABB ITT600", "Siemens DIGSI") unless the names are verified from primary sources. Product names change, and inaccuracies undermine credibility with utility engineers who know the tools. Instead, describe the competitive landscape generically (e.g., "each IED manufacturer ships their own configuration tool").

### Archived Repositories

If a project contains components with archived GitHub repositories, those components should be excluded from the overview entirely — not mentioned with a caveat. Archived repos represent abandoned code that creates a misleading impression of active capability if included.

### Related Projects Threshold

"Both projects use the same standard/format" (e.g., both handle CIM data) is not a sufficient relationship for a Related Projects entry. There must be a genuine technical relationship: direct code integration, complementary functions in the same workflow, or shared data flows. Merely operating in adjacent domains or using common standards does not qualify.

### Avoiding Time-Sensitive Content

- Focus on durable facts: technical capabilities, production deployments, company participation, specification versions
- For milestones, reference the outcome rather than the future event (e.g., "launched Q1 2026" vs "launching at DistribuTech Feb 2026")
- Assume 3-6 month refresh cycle when deciding what to include

### Handling Missing Information

- Leave fields blank rather than guessing
- Mark with "TODO: [what's needed]" for follow-up

### Versioning

  - Each `project-name.md` file includes a **Last Updated** field at the top in format YYYY-MM-DD
  - Update this date whenever ANY edit is made to the file (no judgment calls about materiality)
  - This provides a simple audit trail and freshness indicator for internal use

### Emeritus Projects

Some projects have been archived to "Emeritus" because they are no longer active. These should generally be ignored. If mentioned, it should be clarified that they are no longer active. These projects include but are not limited to:

- FledgePOWER
- Grid Capacity Map

Some projects are not officially Emeritus yet but they are dormant and can be ignored:

- GridVantage
- SCDH
- Node Collective
