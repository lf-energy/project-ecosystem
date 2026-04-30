# Arras

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

- LF Energy webpage: https://lfenergy.org/projects/arras/
- Website: https://www.arras.energy/
- Code: https://github.com/arras-energy
- Documentation: https://docs.arras.energy/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/arras?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/arras-discussion
	- Slack: https://lfenergy.slack.com/archives/C03P2MYBDPG
- LFX Insights: https://insights.linuxfoundation.org/project/gridlabd
- Other:

## Description

Agent-based simulation platform for distribution system planning, modeling loads, generation, storage, and markets over time to evaluate grid scenarios like electrification, hosting capacity, and resilience.

## Overview

Arras Energy is a distribution system simulation platform that models electric grids as collections of interacting agents — where each load, generator, transformer, and other grid object operates independently and advances through simulated time. Unlike traditional power flow tools that analyze a single operating condition at a time, Arras runs time-series simulations where devices respond dynamically to changing weather, prices, and grid conditions at each time step. This agent-based approach captures the temporal complexity of modern distribution grids — particularly the interactions between customer-side technologies (rooftop solar, EV chargers, heat pumps, battery storage) and grid infrastructure.

Utility planners face questions that snapshot analysis struggles to answer: What happens to a feeder when 30% of customers adopt EVs and charge on a time-of-use tariff? How does a distribution system perform during a multi-day extreme heat event when solar generation, air conditioning load, and battery dispatch all interact simultaneously? Arras addresses these by simulating realistic device behavior over days, weeks, or years, using physics-based and data-driven load models at the appliance level, integrated weather data, and tariff/market models. This enables planners to evaluate scenarios like deep electrification impact, DER hosting capacity, extreme event resilience, and tariff design with a level of temporal and behavioral fidelity that static analysis cannot provide.

Arras originated as HiPAS GridLAB-D, a high-performance variant of the U.S. Department of Energy's GridLAB-D simulation tool, developed at SLAC National Accelerator Laboratory with funding from the California Energy Commission. It was adopted by LF Energy in 2022. The project is primarily used by national laboratories, universities, and utilities for distribution planning studies. It includes a library of IEEE, DOE, and PG&E test/taxonomy feeders, converters for importing CYME distribution models, and Python integration for custom analysis workflows. Deployment options include Docker containers, cloud (AWS), and native Linux/macOS installations.

## Technical Profile

### What It Does

Performs agent-based time-series simulation of distribution systems, solving power flow at each time step while individual loads, generators, storage, and market objects interact dynamically based on weather, price signals, and physical state.

### Problem(s) Solved

Enables utility planners to evaluate how distribution systems will perform under future scenarios — electrification, DER growth, tariff changes, extreme weather — where the time-varying interactions between customer devices and grid infrastructure matter. Replaces the need to build custom simulation environments for studies that require temporal and behavioral fidelity beyond what snapshot power flow analysis provides.

### Key Capabilities

- Time-series distribution power flow simulation with 3-phase unbalanced solvers (Newton-Raphson and forward-backward sweep methods)
- Physics-based residential load models at the appliance level (HVAC, water heater, EV charger, etc.) and data-driven load models for all sectors (residential, commercial, industrial, agricultural)
- Distributed generation and storage modeling (solar, wind, battery)
- Integrated weather data: TMY files for planning studies, NOAA real-time forecasts (North America), NREL historical data
- Retail market simulation including transactive energy, with access to the OpenEI tariff database
- Reliability and resilience analysis: fault simulation, pole failure modeling from wind/ice/vegetation, extreme event scenarios
- Optimization capabilities (convex optimization, particle swarm optimization)
- CYME distribution model converter for importing utility network models
- IEEE, DOE, and PG&E test/taxonomy feeders included for benchmarking and validation
- Python integration for extending simulations with custom modules and analysis workflows

### Relevant Standards

None. Arras is a simulation platform; it does not directly implement grid communication or data model standards. It provides a format converter for importing CYME distribution models.

## Grid Context

### Grid Segment

Distribution

### Function

Grid Modeling & Simulation

### Industry Solution Categories

#### Solution Type

- Distribution System Simulation Platform: Provides agent-based time-series simulation for distribution system planning studies, modeling the dynamic interaction of loads, generation, storage, weather, and markets over time.

#### Component of

- Network Planning: Supplies the simulation engine for distribution network planning studies — evaluating capacity, assessing infrastructure alternatives, and modeling the impact of load growth, electrification, and DER penetration on distribution feeders.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **Power Grid Model**: Both address distribution system analysis but at different levels. PGM is a high-performance calculation library for steady-state power flow (snapshot analysis at scale). Arras is a simulation platform that models dynamic device behavior over time. PGM is suited for batch calculations across thousands of scenarios; Arras is suited for detailed time-series studies where temporal interactions between devices matter.
- **PowSyBl**: Both are grid simulation projects. PowSyBl focuses on transmission-level modeling (Java, used by TSOs); Arras focuses on distribution-level simulation (C++, used for utility planning). No direct technical integration.
- **FIDOpower**: FIDOpower's analysis workflows consume Arras (GridLAB-D) JSON model files as their primary input format. FIDOpower provides interactive notebook-based analyses (optimal powerflow, capacity sizing) that operate on Arras network models.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

<!-- TODO: Verify deployment maturity. The CEC project involved California utility engagement (Southern California Edison, PG&E feeder models), but it's unclear whether any utility has deployed Arras in a production planning workflow vs. R&D/evaluation use. If utility production use can be confirmed, this should be upgraded to Piloting. -->

### Supporting / Adopting Organizations

- Eudoxys Sciences (David P. Chassin, project lead)
- SLAC National Accelerator Laboratory (original HiPAS GridLAB-D developer; Stanford University)
- Pacific Northwest National Laboratory (original GridLAB-D developer)
- California Energy Commission (funder of HiPAS GridLAB-D development)
- U.S. Department of Energy (original GridLAB-D funder)
- Hitachi America (developer of GLOW web-based GUI)
- NRECA (contributor)
- Southern California Edison (contributor)
- NREL (contributor)
- Post Road Foundation (contributor)
- AWS (contributor)

## Learn More

- [Arras: Status and Challenges](https://lfenergysummit2024.sched.com/event/1ehJT/update-on-arras-energy-david-p-chassin-eudoxys-sciences-llc)
	- Date: 2024-09-06
	- Type: Presentation

## Additional Notes

Arras originated from GridLAB-D, an agent-based distribution system simulator developed at Pacific Northwest National Laboratory (PNNL) starting in 2007, funded by the U.S. Department of Energy. In 2018, the California Energy Commission funded SLAC National Accelerator Laboratory to develop HiPAS GridLAB-D — a high-performance variant optimized for California utility use cases (hosting capacity, electrification, resilience, tariff design). HiPAS GridLAB-D was adopted by LF Energy in 2022 and renamed Arras Energy. The original PNNL GridLAB-D (https://www.gridlabd.org/) continues as a separate project; the two codebases have diverged significantly.

The agent-based architecture is Arras's key differentiator relative to traditional distribution analysis tools. Where conventional tools perform snapshot power flow calculations, Arras simulates each grid object as an independent agent that responds to its environment at each time step. This enables studies where temporal interactions matter — for example, simultaneous modeling of how weather drives both load (air conditioning) and hazards (pole failure from wind), or how customer response to price signals changes aggregate feeder load profiles over a season. This approach is computationally more expensive than snapshot analysis but provides a level of behavioral fidelity that planning studies for electrification and DER integration increasingly require.

Licensed under BSD-3-Clause.