<!-- Filename: use the project name in kebab-case, e.g. power-grid-model.md, powsybl.md -->

# ReLife

**Last Updated:** 2026-06-23

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
- Website: https://opensource.rte-france.com/relife/
- Code: https://github.com/rte-france/relife
- Documentation: https://opensource.rte-france.com/relife/
- Calendar:
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
- LFX Insights:
- Other:
	- PyPI: https://pypi.org/project/relife/
	- TAC proposal: https://github.com/lf-energy/tac/issues/762

## Description

Python library that models how assets age and fail using reliability and survival statistics, then compares maintenance, replacement, and run-to-failure strategies by cost and risk.

## Overview

ReLife is a statistical toolbox for asset management decisions. Given records of how assets have behaved over time — failures, repairs, time in service, and conditions such as location or corrosion level — it fits statistical models of asset lifetime and failure behavior, then uses those models to compare maintenance strategies and project the replacements and budgets each strategy implies. It is built on NumPy and SciPy and distributed as a Python package.

Network operators face a recurring capital question: a large population of assets installed decades ago is aging at once, and replacing everything at once is neither affordable nor necessary. ReLife brings a quantitative, peer-reviewed basis to that question. It answers when to maintain, replace, or repair an asset, on what criteria, and at what budget — for example, comparing a run-to-failure policy against a preventive age-based replacement policy and showing the expected total cost, risk, and number of replacements of each over a planning horizon. Costs can include not only direct replacement cost but societal costs such as the shadow price of carbon, supporting socioeconomic justification of renewal investment.

ReLife is used internally at RTE, the French transmission system operator, and by a growing set of other infrastructure operators. Its outputs feed the asset-renewal and capital-planning decisions that asset managers and investors make. Although it originates in grid asset management, the methods are general and apply to any aging asset population.

## Technical Profile

### What It Does

Fits statistical lifetime and recurrent-event models to asset failure/repair data, then uses renewal theory to compare maintenance policies and project the expected replacements and discounted costs of each.

### Problem(s) Solved

Gives network operators a quantitative, defensible basis for asset-renewal investment decisions — when to repair, replace, or run an asset to failure, and at what budget — replacing rule-of-thumb or purely age-based replacement with data-driven reliability modeling. It also narrows the research-to-industry gap by packaging peer-reviewed reliability methods in accessible open-source form.

### Key Capabilities

- **Lifetime modeling** (`lifetime_models` module): non-parametric estimators, parametric lifetime distributions with or without covariates, and semi-parametric Cox regression for the influence of asset conditions (location, corrosion, temperature, etc.) on failure
- **Recurrent-event modeling** (`stochastic_processes` module): non-homogeneous Poisson processes for recurrent minimal repairs
- **Maintenance policy evaluation** (`policies` module): corrective replacement (run-to-failure) and preventive age-based replacement policies, with computation of expected discounted annual costs
- **Socioeconomic cost evaluation**: costs can incorporate societal factors such as the shadow price of carbon, not just direct replacement cost
- **Renewal-theory projection**: forecasts the expected number of replacements and associated budgets that a given maintenance policy implies over a planning horizon
- **Renewal processes** with or without rewards, a renewal equation solver, and N-dimensional Lebesgue-Stieltjes integration
- Can generate simulated data to study the influence of data changes and test functionality (though simulation is not its primary purpose)

### Relevant Standards

None directly implemented. The project describes its risk-informed decision-making approach as aligned with IEC 63223-2 (risk analysis for asset management), but this is a methodological reference rather than a standard the library implements or conforms to.

## Grid Context

### Grid Segment

Cross-cutting (grid segment is not a meaningful axis — ReLife operates on asset failure/repair statistics, not on a physical location of the energy system, and applies to asset populations across all segments and beyond the grid)

<!-- Per taxonomy.md, "Cross-cutting" applies when grid segment is not a meaningful descriptor of where a project operates. ReLife is a horizontal reliability/renewal method library. This is distinct from multi-segment grid tools (which are multi-tagged by physical segment) and from "Outside the Grid Taxonomy" (off-grid, no Function). Lead/primary documented deployers are TSOs (RTE, TenneT), but the methods are asset-type-agnostic. -->

### Function

Planning & Analysis

<!-- Reliability/risk modeling that produces insight (policy comparisons, replacement/budget projections) to inform investment decisions; does not act on real-time grid state. The taxonomy "Watch" note tracks whether a dedicated Asset Management function should emerge once a second such project (e.g., Raven) is active. -->

### Industry Solution Categories

#### Solution Type

- Reliability & Maintenance Policy Modeling: Fits statistical models of asset lifetime and failure behavior and evaluates maintenance strategies on expected cost, risk, and number of replacements.

#### Component of

- Asset Investment Planning (AIP): Provides the quantitative reliability-and-cost engine that justifies and prioritizes capital renewal of aging asset populations — the analytical core of an asset investment planning workflow.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

None. No LF Energy projects currently have documented technical integration, shared data flows, or complementary workflows with ReLife. (covXtreme is also a statistical toolkit, but shared statistical character is not a sufficient relationship — there is no integration or shared workflow.)

## Maturity & Adoption

### LF Energy Stage

Sandbox (proposed)

<!-- TAC issue #762 proposes ReLife at Sandbox stage. -->

### Deployment Maturity

Production (in transmission asset management at RTE; other operators at earlier stages of adoption)

### Supporting / Adopting Organizations

- RTE (project lead and primary developer; production user for transmission asset management)
- Artelys (supports research and development)
- TenneT, AusNet, GRTgaz (infrastructure operators using the library)
- CentraleSupélec, Sorbonne Université (academic partners; ReLife is part of the CentraleSupélec engineering training program)

## Learn More

<!-- TODO: add curated external links (e.g., MIMAR 2025 conference material, LF Energy Europe Summit 2025 presentation) when shareable URLs are available. -->

## Additional Notes

ReLife occupies an emerging asset-management niche in the LF Energy portfolio rather than a settled one. The taxonomy currently has no Asset Management function category; ReLife is classified under Planning & Analysis with a Cross-cutting grid segment (it shares this segment designation with covXtreme, the portfolio's other horizontal statistical method library). The taxonomy's watch note tracks whether a dedicated Asset Management function should emerge as related projects (e.g., reliability modeling, asset-condition analytics such as Raven) join.

The maintainers emphasize that ReLife is a statistical toolbox rather than a simulator — a distinction worth preserving in any positioning. Its differentiator is bringing open, peer-reviewed reliability and renewal-theory methods, plus socioeconomic cost evaluation (including the shadow price of carbon), to asset-renewal decisions that are often made today with proprietary tools or simple age-based rules.

The package API is still evolving (the maintainers note significant changes are ongoing despite a 1.0.0+ release history), so specific module and class names should be verified against current documentation before being cited externally.

As of the TAC submission, the project's main acknowledged gaps are limited external contributors and limited visibility — both motivations for joining LF Energy.
