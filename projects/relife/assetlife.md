<!-- Filename: use the project name in kebab-case, e.g. power-grid-model.md, powsybl.md -->

# AssetLife

**Last Updated:** 2026-09-04

## Table of Contents

- [Basic Info](#basic-info)
- [Description](#description)
- [Overview](#overview)
- [Technical Profile](#technical-profile)
- [Grid Context](#grid-context)
- [Related Projects](#related-projects)
- [Maturity & Adoption](#maturity--adoption)
- [Learn More](#learn-more)
- [Additional Notes](#additional-notes)

## Basic Info

- LF Energy webpage: TODO: page in progress, not yet published
- Website: https://opensource.rte-france.com/AssetLife/
- Code: https://github.com/AssetLife-project
- Documentation: https://opensource.rte-france.com/AssetLife/
- Calendar:
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
- LFX Insights:
- Other:
	- PyPI: https://pypi.org/project/AssetLife/
	- TAC proposal: https://github.com/lf-energy/tac/issues/762

## Description

Built on reliability theory, AssetLife helps infrastructure managers select maintenance policies that minimize socio-economic costs and justify investment decisions.

## Overview

In the context of aging infrastructures and climate change, asset managers face critical investment decisions. AssetLife helps asset managers perform quantitative risk analysis to evaluate and compare risk control options over large asset populations based on probability models along with socio-economic criteria. Quantitative risk analysis is highly desirable for justifying investment decisions, maximizing asset value and anticipating stocks and budgets.

AssetLife analyzes historical asset data — failures, repairs, service duration, deterioration measurements, and contextual factors like location or corrosion levels — to build statistical models for lifetime distributions and failure behavior. These models are then used to compare maintenance strategies and determine when to maintain, repair, or replace assets by balancing preventive and corrective costs. It identifies optimal maintenance policies, and projects the expected total cost and replacement count over a planned horizon. Cost calculations include direct replacement expenses and societal costs, such as carbon shadow pricing, which strengthens the economic justification for renewal investments.

AssetLife is used internally at RTE, the French transmission system operator, and by a growing set of other infrastructure operators. Its outputs feed the asset-renewal and capital-planning decisions that asset managers and investors make. Although it originates in grid asset management, the methods are general and apply to any aging asset population.

The library is built on NumPy and SciPy and distributed as a Python package.

## Technical Profile

### What It Does

Depending on the event of interest, fits statistical distributions or stochastic processes to model asset aging or behavior over time, then uses renewal theory and socioeconomic engineering to compare maintenance policies and compute the expected replacement and discounted costs of each.

### Problem(s) Solved

Gives infrastructure operators (TSOs, railway operators, etc.) a quantitative, defensible basis for asset-renewal investment decisions — when to repair, replace, or run an asset to failure, at what budget, and how to manage spare-parts stock — replacing rule-of-thumb or purely age-based replacement with data-driven reliability modeling. It also narrows the research-to-industry gap by packaging peer-reviewed reliability methods in accessible open-source form.

### Key Capabilities

- **Lifetime modeling**: non-parametric estimators, parametric lifetime distributions with or without covariates, and semi-parametric Cox regression for the influence of asset conditions (location, corrosion, temperature, etc.) on failure
- **Recurrent-event modeling**: non-homogeneous Poisson processes for recurrent minimal repairs
- **Maintenance policy evaluation**: corrective replacement (run-to-failure) and preventive age-based replacement policies, with computation of expected discounted annual costs
- **Socioeconomic cost evaluation**: costs can incorporate societal factors such as the shadow price of carbon, not just direct replacement cost
- **Renewal-theory projection**: forecasts the expected number of replacements and associated budgets that a given maintenance policy implies over a planning horizon, using renewal processes with or without rewards, a renewal equation solver, and N-dimensional Lebesgue-Stieltjes integration
- **Simulation**: can generate simulated data to study the influence of data changes and test functionality (though simulation is not its primary purpose)

### Relevant Standards

None directly implemented. The project describes its risk-informed decision-making approach as aligned with IEC 63223-2 (risk analysis for asset management), but this is a methodological reference rather than a standard the library implements or conforms to.

## Grid Context

### Grid Segment

Cross-cutting (grid segment is not a meaningful axis — AssetLife operates on asset failure/repair statistics, not on a physical location of the energy system, and applies to asset populations across all segments and beyond the grid)

<!-- Per taxonomy.md, "Cross-cutting" applies when grid segment is not a meaningful descriptor of where a project operates. AssetLife is a horizontal reliability/renewal method library. This is distinct from multi-segment grid tools (which are multi-tagged by physical segment) and from "Outside the Grid Taxonomy" (off-grid, no Function). Lead/primary documented deployers are TSOs (RTE, TenneT), but the methods are asset-type-agnostic. -->

### Function

Planning & Analysis

<!-- Reliability/risk modeling that produces insight (policy comparisons, replacement/budget projections) to inform investment decisions; does not act on real-time grid state. The taxonomy "Watch" note tracks whether a dedicated Asset Management function should emerge once a second such project (e.g., Raven) is active. -->

### Industry Solution Categories

#### Solution Type

- Reliability & Maintenance Policy Modeling: Fits statistical models of asset aging and behavior over time, then uses those models to compare different maintenance strategies.

#### Component of

- Asset Investment Planning (AIP): Provides quantitative approaches to justify investment decisions for renewal of aging asset populations — the analytical core of an asset investment planning workflow.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

None. No LF Energy projects currently have documented technical integration, shared data flows, or complementary workflows with AssetLife. (covXtreme is also a statistical toolkit, but shared statistical character is not a sufficient relationship — there is no integration or shared workflow.)

## Maturity & Adoption

### LF Energy Stage

Sandbox (proposed)

<!-- TAC issue #762 proposes AssetLife at Sandbox stage. -->

### Deployment Maturity

Production (in transmission asset management at RTE; other operators at earlier stages of adoption)

### Supporting / Adopting Organizations

- RTE (project lead and primary developer; production user for transmission asset management)
- Artelys (supports research and development)
- TenneT, AusNet, GRTgaz (infrastructure operators using the library)
- CentraleSupélec, Sorbonne Université (academic partners; AssetLife is part of the CentraleSupélec engineering training program)

## Learn More

<!-- TODO: add curated external links (e.g., MIMAR 2025 conference material, LF Energy Europe Summit 2025 presentation) when shareable URLs are available. -->

## Additional Notes

AssetLife occupies an emerging asset-management niche in the LF Energy portfolio rather than a settled one. The taxonomy currently has no Asset Management function category; AssetLife is classified under Planning & Analysis with a Cross-cutting grid segment (it shares this segment designation with covXtreme, the portfolio's other horizontal statistical method library). The taxonomy's watch note tracks whether a dedicated Asset Management function should emerge as related projects (e.g., reliability modeling, asset-condition analytics such as Raven) join.

The maintainers emphasize that AssetLife is a statistical toolbox rather than a simulator — a distinction worth preserving in any positioning. Its differentiator is bringing open, peer-reviewed reliability and renewal-theory methods, plus socioeconomic cost evaluation (including the shadow price of carbon), to asset-renewal decisions that are often made today with proprietary tools or simple age-based rules.

The package API is still evolving (the maintainers note significant changes are ongoing despite a 1.0.0+ release history), so specific module and class names should be verified against current documentation before being cited externally.

As of the TAC submission, the project's main acknowledged gaps are limited external contributors and limited visibility — both motivations for joining LF Energy.
