# Power Grid Model

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

- LF Energy webpage: https://lfenergy.org/projects/power-grid-model/
- Website:
- Code: https://github.com/PowerGridModel
- Documentation: https://power-grid-model.readthedocs.io/en/stable/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/powergridmodel?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/powergridmodel
	- Slack: https://lfenergy.slack.com/archives/C04UBM6S539
	- GitHub Discussions: https://github.com/orgs/PowerGridModel/discussions
- LFX Insights: https://insights.linuxfoundation.org/project/powergridmodel
- Other:

## Description

A high-performance library for steady-state distribution power system analysis.

## Overview

Power Grid Model (PGM) is a calculation library for distribution grid analysis, providing power flow, state estimation, and short circuit calculations. Built as a C++ core with a Python API, it is designed to be embedded into larger utility workflows — from grid planning tools to near-real-time operational systems. It supports both symmetric (balanced three-phase) and asymmetric (per-phase) calculations, making it applicable across medium-voltage and low-voltage distribution networks.

Distribution system operators face growing pressure from electrification, distributed generation, and grid congestion. Understanding the state of the network — where voltages are out of range, where cables are overloaded, where capacity exists — requires running power system calculations at scale, often across thousands of network scenarios or time steps. Traditional commercial tools were not designed for this kind of programmatic, high-volume analysis. PGM addresses this by providing a library that integrates directly into data pipelines and cloud-native applications, with native multi-threading for batch calculations and performance that is orders of magnitude faster than comparable open source alternatives.

PGM is deployed in production at multiple Dutch distribution system operators, where it underpins applications including grid planning, automatic network design, asset monitoring, and active congestion management. The project includes companion libraries for data format conversion (power-grid-model-io, with converters for Vision and PandaPower formats) and a higher-level data science interface (power-grid-model-ds) that simplifies common analysis workflows.

## Technical Profile

### What It Does

Performs steady-state power system calculations — power flow, state estimation, and short circuit analysis — for distribution networks.

### Problem(s) Solved

Enables utilities to run large-scale distribution network analysis programmatically, replacing manual workflows tied to commercial desktop tools. Supports operational use cases like near-real-time state estimation for congestion management, operational planning, grid connection planning as well as strategic and ivestment planning.

### Key Capabilities

- Power flow analysis with multiple algorithms (Newton-Raphson, iterative current, linear approximations)
- State estimation using weighted least squares methods (iterative linear and Newton-Raphson)
- Short circuit calculation
- Symmetric (balanced) and asymmetric (per-phase) calculation modes
- Native batch calculation with shared-memory multi-threading for time-series and scenario analysis
- High performance: orders of magnitude faster than comparable open source alternatives for batch and asymmetric calculations
- Cross-platform: available via PyPI and conda-forge for Windows, Linux, and macOS (x64 and ARM64)
- Data format converters for Vision and PandaPower (via power-grid-model-io)

### Relevant Standards

- CIM-CGMES — Common Grid Model Exchange Standard

## Grid Context

### Grid Segment

Distribution

### Function

Grid Modeling & Simulation

### Industry Solution Categories

#### Solution Type

- Network Analysis: Provides steady-state distribution grid calculations that can be embedded into larger utility workflows.

#### Component of

- ADMS: Supplies the power flow and state estimation engine that an ADMS needs for real-time network awareness and active congestion management.
- Network Planning: Enables large-scale scenario analysis for distribution grid reinforcement studies, running batch calculations across thousands of network configurations.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

### LF Energy Ecosystem

- **OpenSTEF**: Complementary — OpenSTEF produces energy load forecasts that feed into PGM power flow calculations for forward-looking congestion analysis.
- **Shapeshifter**: Complementary — within Alliander's Grid-as-a-Service architecture, PGM identifies congestion while Shapeshifter handles flexibility market coordination to resolve it.
- **PowSyBl**: Similar domain, different scope — PowSyBl focuses on transmission-level modeling (Java-based, used by TSOs like RTE), while PGM focuses on distribution-level analysis (C++/Python, used by DSOs). They are complementary across voltage levels rather than competing.
- **SOGNO**: Both provide distribution-level power system analysis. SOGNO's pyvolt provides distribution state estimation with a CIM-native data model. PGM's high-performance calculation engine could serve as an alternative or complementary analytical backend within the SOGNO platform architecture.
- **Arras**: Both address distribution system analysis. Arras (formerly GridLab-D) focuses on distribution system simulation and planning with agent-based modeling. PGM is a lower-level calculation library that can serve as a building block within planning tools.

### External

- **PandaPower**: PGM provides data format converters for PandaPower networks (via power-grid-model-io) and is validated against PandaPower results. PGM offers significantly higher performance for batch and asymmetric calculations.
- **GridCal**: Both are open source power system analysis tools. GridCal is research-oriented with a GUI; PGM is a headless calculation library optimized for high-performance programmatic use.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

Production

### Supporting / Adopting Organizations

- Alliander (production user)
- Enexis (production user)
- Stedin (production user)
- TU Delft
- TU Eindhoven
- RSE
- Soptim

## Learn More

- [Power Grid Model and DELVI integration case study](https://lfenergy.org/power-grid-model-delvi/)
	- Date: 2024-01-18
	- Type: Case Study
- [Power Grid Model: A High-Performance Distribution Grid Calculation Library](https://archive.fosdem.org/2024/events/attachments/fosdem-2024-2101-power-grid-model-open-source-high-performance-power-systems-analysis/slides/22163/PGM_FOSSDEM24_WPMoRII.pdf)
	- Date: 2024
	- Type: Presentation
- Network calculations for enhanced capacity management in distribution networks
	- Date: 2024-06-06
	- Type: Presentation
- [Distribution system analysis using Power Grid Model](https://lfenergysummit2024.sched.com/event/1ehHh/distribution-system-analysis-using-power-grid-model-peter-salemink-alliander)
	- Date: 2024-09-05
	- Type: Presentation
- [Lightning Talk: Integrating CGMES-Based Grid Model Using the Generic Branch in Power Grid Model](https://lfenergysummiteu2025.sched.com/event/26Iyc/lightning-talk-integrating-cgmes-based-grid-models-using-the-generic-branch-in-power-grid-model-udo-schmitz-soptim-ag)
	- Date: 2025-09-10
	- Type: Presentation
- [Power-Grid-Model-DS: simplifying data science for distribution system analysis](https://lfenergysummiteu2025.sched.com/event/26Iy8/power-grid-model-ds-simplifying-data-science-for-distribution-system-analysis-peter-salemink-jaap-schouten-alliander)
	- Date: 2025-09-10
	- Type: Presentation

## Additional Notes

PGM originated at Alliander, the largest Dutch DSO, where it serves as a foundational building block across multiple production applications — from long-term grid planning to active congestion management. This dual use (planning and operations) within a single DSO demonstrates the library's versatility and is relatively unusual for grid analysis tools, which tend to serve one domain or the other. The project's multi-stakeholder community now includes all three major Dutch DSOs, two Dutch technical universities, an Italian research institution (RSE), and a German energy software vendor (Soptim), who has built a CGMES-to-PGM conversion suite on top of the library.

**Technical architecture**: The project follows a layered design — the C++ calculation core (`power-grid-model`) provides maximum performance, the Python API provides accessibility for data scientists and engineers, `power-grid-model-io` handles data format conversion from various industry formats, and `power-grid-model-ds` provides a higher-level interface for common data science workflows. All components are licensed under MPL-2.0.
