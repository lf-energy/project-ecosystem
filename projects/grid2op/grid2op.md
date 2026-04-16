# Grid2Op

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

- LF Energy webpage: https://lfenergy.org/projects/grid2op/
- Website:
- Code: https://github.com/Grid2op
- Documentation: https://grid2op.readthedocs.io/en/latest/
- Calendar:
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
	- Discord: https://discord.com/invite/cYsYrPT
- LFX Insights: https://insights.linuxfoundation.org/project/grid2op
- Other:

## Description

Simulation environment for developing and benchmarking automated control strategies for power grid operations.

## Overview

Grid2Op is a simulation environment for modeling sequential decision-making in power grid operations. It presents a realistic power grid as an interactive environment where automated agents — whether AI-based, optimization-based, or rule-based — can take the same control actions a transmission operator would: reconfiguring substation topology, redispatching generators, curtailing renewable generation, and managing maintenance outages. The environment enforces physics-based AC power flow, thermal line limits, and protection system behavior, so agents must learn to operate the grid within real operational constraints.

Testing new control strategies on a live grid is not an option — the consequences of failure are too severe. Grid2Op provides a safe, repeatable sandbox where control approaches can be developed, stress-tested against thousands of scenarios (variable renewables, demand changes, contingencies, cascading failures), and benchmarked against each other before any consideration of real-world deployment. As grids become more complex with high renewable penetration and tighter operating margins, the operational decisions facing control room operators increasingly exceed what manual or simple rule-based approaches can handle. Grid2Op enables the development of advanced decision support tools that could help operators manage this complexity.

Grid2Op is developed and maintained by RTE, the French transmission system operator. It serves as the platform for the Learning to Run a Power Network (L2RPN) competition series, including events hosted at NeurIPS, where the NeurIPS 2020 edition attracted over 300 international participants from both academia and industry. The project is used by power systems researchers and AI/ML teams developing control algorithms, rather than by grid operators directly. The ecosystem includes companion tools: lightsim2grid (a high-performance C++ power flow backend), chronix2grid (synthetic power grid scenario generation), grid2viz (agent behavior visualization), and grid2game (interactive human-in-the-loop simulation).

## Technical Profile

### What It Does

Simulates power grid operations as an interactive environment where automated agents make sequential control decisions (topology switching, redispatching, curtailment) against realistic physics-based power flow and operational constraints.

### Problem(s) Solved

Provides a safe testing ground for developing automated grid control strategies, eliminating the need to test on live grids. Enables systematic benchmarking of different control approaches (AI, optimization, heuristic) against identical scenarios, accelerating the development of decision support tools for grid operators facing increasingly complex operating conditions.

### Key Capabilities

- Realistic simulation of transmission grid operations with AC power flow, thermal limits, and protection system behavior
- Full range of operator control actions: substation topology reconfiguration, generator redispatching, renewable curtailment, and maintenance scheduling
- Pluggable power flow backends: PandaPower (default), lightsim2grid (high-performance C++ backend), and pypowsybl2grid (PowSyBl integration)
- Standard test environments based on IEEE bus systems and competition-specific networks
- Gymnasium-compatible reinforcement learning interface for integration with standard ML frameworks
- Scenario-based simulation with variable load, generation, and contingency profiles for stress-testing control strategies
- Observation model providing agents with line flows, topology state, generator/load injections, forecasts, and thermal limit data
- Configurable operational rules and constraints to model different grid codes and operating procedures

### Relevant Standards

None. Grid2Op is a simulation environment that uses power flow physics but does not directly implement grid communication or data model standards.

## Grid Context

### Grid Segment

Transmission

### Function

Grid Operations

### Industry Solution Categories

#### Solution Type

- Grid Operations Simulation Environment: Provides a realistic, physics-based simulation environment for developing and benchmarking automated control strategies for power grid operations.

#### Component of

None. Grid2Op is a standalone research and development tool, not a component of a broader operational system. The control strategies developed using Grid2Op could eventually be deployed within an EMS, but Grid2Op itself is not an EMS component.

### Cross-Cutting Tags

- **Project Intent:** Research
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **PowSyBl**: Integration — a backend (pypowsybl2grid) enables PowSyBl's power flow engine to serve as the simulation backend for Grid2Op environments, bringing PowSyBl's transmission-grade modeling capabilities into the training loop.
- **dynaωo**: Both are RTE-developed projects for power system simulation. Dynaωo provides dynamic (time-domain) simulation for transient stability analysis; Grid2Op provides sequential decision-making simulation for control strategy development. They address different simulation needs and do not directly integrate.
- **GridFM**: Both apply ML to power grid operations but with fundamentally different approaches. Grid2Op provides a simulation environment for reinforcement learning control strategies (sequential decision-making); GridFM develops pre-trained foundation models for power system analysis tasks (scenario evaluation). They do not directly integrate.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- RTE (primary developer and maintainer; uses Grid2Op for internal research on grid operations)

## Learn More

TODO: Identify and add key presentations, blog posts, and competition results with dates and local filepaths.

## Additional Notes

Grid2Op occupies a unique position in the LF Energy ecosystem as a tool primarily aimed at AI/ML researchers and algorithm developers rather than grid operators directly. Its value to utilities is indirect but strategic: it accelerates the development and validation of advanced control strategies that utilities may eventually deploy in their control rooms. The L2RPN competition series (hosted at venues including NeurIPS 2020, with 300+ participants) demonstrated that reinforcement learning agents can achieve competitive performance on grid operation tasks.

A common misconception is that Grid2Op is a power system simulator in the traditional sense (like PowSyBl or dynaωo). It is better understood as a *decision-making environment* that wraps a power flow simulator — the simulation serves the RL training loop, not the other way around. The modular backend architecture reflects this: Grid2Op delegates the actual power flow computation to pluggable solvers (PandaPower, lightsim2grid, PowSyBl) and focuses on modeling the decision space, observation space, and operational rules that define the control problem.

All components are licensed under MPL-2.0.
