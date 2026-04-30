# RTC-Tools

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

- LF Energy webpage: https://lfenergy.org/projects/rtc-tools/
- Website:
- Code: https://github.com/rtc-tools/
- Documentation: https://rtc-tools.readthedocs.io/en/stable/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/rtc-tools?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/rtc-tools-discussion
	- Slack: https://lfenergy.slack.com/archives/C09H4UHQ4P4
- LFX Insights: https://insights.linuxfoundation.org/project/rtc-tools
- Other:

## Description

Optimization framework for dispatch of energy assets including hydropower, battery storage, and multi-energy systems.

## Overview

RTC-Tools is a solver-agnostic mathematical optimization framework for time-dependent systems. Users define physical asset models — either in Python or using the Modelica modeling language — and RTC-Tools translates these into optimization problems that are solved by pluggable open source or commercial solvers (HiGHS, CBC, IPOPT, Gurobi, CPLEX). The framework supports linear and nonlinear optimization, multi-objective goal programming via lexicographic ordering, and stochastic optimization using ensemble forecasts with automatic control tree generation for decision-making under uncertainty. This makes it applicable to a broad range of asset optimization problems where operators must balance competing objectives under uncertainty.

In the energy sector, RTC-Tools addresses two primary use cases. For hydropower, it optimizes reservoir operations and generation schedules across competing objectives — maximizing power revenue while respecting flood control limits, environmental flow requirements, and water supply obligations. Planning horizons range from days (operational scheduling) to years (strategic planning). For battery energy storage systems (BESS), it optimizes dispatch across multiple electricity markets simultaneously — day-ahead, intraday, and ancillary services — performing value stacking to maximize total revenue while managing battery degradation and operational constraints. In both cases, the core challenge is the same: finding the best operating strategy for a complex physical asset participating in markets with uncertain future prices and conditions.

RTC-Tools originated at Deltares, the Dutch research institute for water and subsurface, where it has been deployed in production since 2017 for hydropower scheduling at utilities including Ontario Power Generation (Canada), HydroTasmania (Australia), and Verbund (Austria). PortfolioEnergy, founded in 2025, uses the framework as the optimization core of its commercial BESS trading platform. PortfolioEnergy co-maintains the project alongside Deltares.

## Technical Profile

### What It Does

Solves constrained optimization problems for energy asset dispatch, taking physical asset models and market/operational constraints as inputs and producing optimal operating schedules as output.

### Problem(s) Solved

Enables hydropower operators and battery storage traders to compute optimal asset dispatch strategies that balance multiple competing objectives (revenue, safety constraints, equipment longevity) across multiple markets and uncertain future conditions — without building custom optimization infrastructure. Replaces manual scheduling rules or proprietary black-box optimization tools with a transparent, extensible framework where operators can inspect and modify the underlying models.

### Key Capabilities

- Multi-objective goal programming via lexicographic ordering, allowing operators to define priority-ranked objectives (e.g., safety constraints first, revenue maximization second)
- Stochastic optimization using ensemble forecasts with automatic control tree generation for decision-making under uncertainty
- Modelica-based physical modeling, enabling engineers to define asset physics (reservoirs, batteries, heat networks) in a standard systems modeling language and automatically derive optimization formulations
- Multi-market value stacking for BESS: simultaneous optimization across day-ahead, intraday, and ancillary service markets
- Model predictive control (MPC) for rolling-horizon operational optimization that re-optimizes as new forecasts and measurements arrive
- Solver-agnostic architecture: supports open source solvers (HiGHS, CBC, IPOPT) and commercial solvers (Gurobi, CPLEX, Knitro) via CasADi
- Delft-FEWS integration for embedding optimization into existing operational decision support systems

### Relevant Standards

None. RTC-Tools is a mathematical optimization framework and does not directly implement grid communication or data model standards. It uses Modelica as a modeling language (not a grid standard) and the Delft-FEWS PI file format for operational system integration (a Deltares-specific interface, not an industry standard).

## Grid Context

### Grid Segment

Generation

### Function

Flexibility & Markets

### Industry Solution Categories

#### Solution Type

- Asset Optimization Engine: Computes optimal dispatch schedules for energy assets using mathematical optimization with physics-based modeling, supporting multiple objectives, uncertainty, and multi-market participation.

#### Component of

- Hydropower Scheduling System: Serves as the optimization core for hydropower generation scheduling, balancing power revenue against water management constraints across planning horizons from days to years.
- BESS Trading Platform: Serves as the optimization core for battery storage dispatch, computing value-stacked schedules across energy and ancillary service markets.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **FlexMeasures**: Overlapping scope — both can optimize energy storage dispatch. RTC-Tools is a lower-level optimization framework that supports broader problem classes (multi-market value stacking, stochastic optimization, Modelica-based physical modeling, hydropower) but requires more engineering effort to deploy. FlexMeasures is a higher-level application with a REST API, web UI, multi-tenancy, and built-in forecasting that is more turnkey for behind-the-meter flexibility. RTC-Tools is a tool for building optimization solutions; FlexMeasures is an optimization solution you deploy.
- **OpenSTEF**: Complementary — OpenSTEF can provide load and price forecasts as inputs to RTC-Tools optimization models. RTC-Tools consumes forecast time series to optimize asset dispatch against expected market conditions.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

Production

### Supporting / Adopting Organizations

- Deltares (primary developer; production deployments for hydropower scheduling worldwide)
- PortfolioEnergy (co-maintainer; commercial BESS trading platform built on RTC-Tools)
- Shell (historical contributor)
- Kisters (contributor)
- Ontario Power Generation (production user — hydropower scheduling, Canada)
- HydroTasmania (production user — hydropower scheduling, Australia)
- Verbund (production user — hydropower scheduling, Austria)

## Learn More

- [RTC-Tools for Energy Trading](https://lfenergysummiteu2025.sched.com/event/26IzO/rtc-tools-integration-energy-trading-use-cases-overview-jorn-baayen-portfolioenergy)
	- Date: 2025-09-11
	- Type: Presentation
- [TAC issue](https://github.com/lf-energy/tac/issues/344)
	- Date: 2024-11-27
	- Type: Issue

## Additional Notes

RTC-Tools originated in water management — canal control, reservoir operations, flood management — and maintains a large user base in that sector (Rijkswaterstaat, Bundesanstalt für Gewässerkunde, US National Weather Service, among others). The water use cases are omitted from the grid-focused categories above but explain the project's maturity: the optimization framework has been in production use since 2017 and has accumulated significant real-world validation. The energy applications (hydropower, BESS) build on the same core engine that manages critical water infrastructure.

The project follows an open-core model for BESS trading. The core RTC-Tools optimization framework and a BESS example implementation are open source (LGPL-3.0). PortfolioEnergy adds proprietary value stack optimization, market models, and a low-level solver layer on top of the open source core for its commercial BESS trading platform. This is analogous to how other LF Energy projects (e.g., Sigholm building on OpenSTEF) have commercial extensions built on the open source base.

RTC-Tools competes with proprietary solutions in both its domains: in hydropower scheduling, with Riverware (CADSWES) and Kisters' Real Time Optimisation package; in energy asset optimization, with commercial Modelica-based optimization tools. The project maintainers position RTC-Tools as an alternative to "black box" vendor solutions, where operators cannot inspect or modify the optimization models driving their asset dispatch decisions.