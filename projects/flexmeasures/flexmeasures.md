# FlexMeasures

**Last Updated:** 2026-03-13

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

- LF Energy webpage: https://lfenergy.org/projects/flexmeasures/
- Website: https://flexmeasures.io/
- Code: https://github.com/FlexMeasures
- Documentation: https://flexmeasures.readthedocs.io/stable/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/flexmeasures?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/flexmeasures
- Other:

## Description

Intelligent energy management system for optimizing flexible behind-the-meter assets.

## Overview

FlexMeasures is an energy management system (EMS) that determines optimal operating schedules for flexible energy assets. Given price signals, grid constraints, and device parameters, it computes when assets should consume, produce, or store energy to minimize costs or maximize value. Supported asset types include battery storage systems, EV chargers, heat pumps with thermal storage, and shiftable industrial processes. FlexMeasures runs as a web application with a REST API, enabling energy service companies and asset operators to integrate scheduling intelligence into their platforms without building optimization engines from scratch.

Behind-the-meter flexibility is increasingly valuable as energy markets, grid congestion, and variable renewable generation create opportunities to shift consumption in response to price signals and grid needs. However, building the optimization, forecasting, and data infrastructure required to exploit this flexibility is a significant engineering effort — one that each energy service company would otherwise need to develop independently. FlexMeasures provides this as a reusable backend: it ingests time series data (prices, weather, measurements), generates forecasts where needed, and produces device-level operating schedules via its API. The platform supports multi-tenancy and a plugin architecture, allowing different service providers to run customized applications on a shared platform.

FlexMeasures is developed by Seita BV, a Netherlands-based company that also uses FlexMeasures as the backend for its commercial energy flexibility services.

## Technical Profile

### What It Does

Computes cost-optimal operating schedules for flexible energy assets, with built-in forecasting, a REST API for integration, and a plugin architecture for customization.

### Problem(s) Solved

Enables energy service companies and asset operators to optimize the dispatch of behind-the-meter flexible assets (batteries, EV chargers, heat pumps, industrial processes) against energy prices and grid constraints, without building custom optimization and forecasting infrastructure. Replaces manual or rule-based scheduling with data-driven optimization that accounts for price signals, device constraints, and state-of-charge dynamics.

### Key Capabilities

- Storage device scheduling (batteries, EV chargers, thermal storage) that optimizes against consumption/production prices with state-of-charge constraints, round-trip efficiency modeling, and configurable soft constraints with breach pricing
- Process scheduling for shiftable, breakable, and inflexible industrial loads with time-window restrictions and duration requirements
- Multi-asset scheduling across sites with shared grid connection capacity constraints
- Built-in forecasting using LightGBM models, with support for weather and other external regressors; also accepts third-party forecast imports
- REST API (v3.0) for data ingestion, schedule retrieval, and sensor management, using USEF-aligned terminology
- Plugin architecture (Flask Blueprints) for extending schedulers, API endpoints, UI views, and CLI commands; available plugins include ENTSO-E market data integration and Home Assistant connectivity (both maintained by the core development team as separate packages)
- Multi-tenancy with role-based access control and per-account white-labeling
- Built-in web UI for asset visualization, schedule monitoring, and data exploration
- Probabilistic data model (timely-beliefs framework) that tracks data provenance, belief timing, and uncertainty

### Relevant Standards

None. FlexMeasures uses USEF terminology and concepts for its API and data model but does not implement the USEF Flex Trading Protocol (UFTP) — that function is served by the Shapeshifter project.

## Grid Context

### Grid Segment

Behind the Meter

### Function

Flexibility & Markets

### Industry Solution Categories

#### Solution Type

- Behind-the-Meter EMS: Computes optimized operating schedules for flexible behind-the-meter assets (batteries, EV chargers, heat pumps, industrial processes) using built-in forecasting and optimization.

#### Component of

- DERMS: Provides the scheduling and optimization engine that an aggregator or energy service company uses to determine optimal dispatch of flexible assets in response to market signals or grid constraints.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **Shapeshifter**: Complementary — an aggregator could use FlexMeasures to compute optimal dispatch schedules for its asset portfolio in response to flex requests received via Shapeshifter's UFTP protocol. FlexMeasures decides *what* each asset should do; Shapeshifter handles the *trading* of that flexibility with grid operators.
- **OpenSTEF**: Complementary — OpenSTEF forecasts energy load at grid locations, FlexMeasures optimizes flexible assets to manage consumption. In a congestion management workflow, OpenSTEF identifies where congestion will occur and FlexMeasures could determine how flexible assets should respond.
- **OpenLEADR**: Complementary — FlexMeasures computes optimal schedules, while OpenLEADR provides the OpenADR signaling layer to communicate demand response signals to devices. An aggregator could use FlexMeasures to determine the optimal charging profile and OpenLEADR to signal EV chargers to execute it.
- **RTC-Tools**: Overlapping scope — both can optimize energy storage dispatch. RTC-Tools is a lower-level optimization framework that supports broader problem classes (multi-market value stacking, stochastic optimization, Modelica-based physical modeling, hydropower) but requires more engineering effort to deploy. FlexMeasures is a higher-level application with a REST API, web UI, multi-tenancy, and built-in forecasting that is more turnkey for behind-the-meter flexibility.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

Production

### Supporting / Adopting Companies

- Seita BV (primary developer; uses FlexMeasures as backend for commercial energy flexibility services)
- Thiink Inc (early adopter — simulation and testing of energy management solutions)
- iRasus Technologies (early adopter — BESS scheduling and price-based optimization in India)

## Learn More

TODO: Identify and add key presentations, blog posts, and case studies with dates and local filepaths.

## Additional Notes

FlexMeasures is architecturally positioned as a backend platform rather than an end-user application. Energy service companies embed FlexMeasures into their own products via its API and plugin system, rather than deploying it as a standalone tool. The plugin architecture (based on Flask Blueprints) is the primary extension mechanism, allowing adopters to add custom schedulers, API endpoints, UI pages, and CLI commands without modifying the core codebase. This design reflects the project's target audience: developers building energy flexibility applications, not utility operators interacting directly with the system.

The platform is built on Python/Flask with PostgreSQL for persistence, Redis for task queues, and a mixed-integer linear optimization solver (HiGHS by default, Cbc as alternative) via Pyomo for schedule computation. It is deployable via Docker or as a standard WSGI application. All components are licensed under Apache 2.0.

The project's data model is built on the timely-beliefs framework, which records not just measurement values but *when* each value was believed to be true and *by whom*. This enables FlexMeasures to distinguish between forecasts made at different times, track data provenance across sources, and handle the inherent uncertainty in energy data — a design choice that supports audit trails and probabilistic decision-making.