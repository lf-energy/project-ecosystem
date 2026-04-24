# PowSyBl

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

- LF Energy webpage: https://lfenergy.org/projects/powsybl/
- Website: https://powsybl.org/
- Code: https://github.com/powsybl
- Documentation: https://powsybl.readthedocs.io/en/latest/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/powsybl?view=month
- LinkedIn: N/A
- Community: https://www.powsybl.org/pages/community/contact.html
	- Mailing List:
		- General: https://lists.lfenergy.org/g/powsybl
		- Developers: https://lists.lfenergy.org/g/powsybl-dev
		- Technical Steering Committee: https://lists.lfenergy.org/g/powsybl-tsc
	- Slack: https://join.slack.com/t/powsybl/shared_invite/zt-36jvd725u-cnquPgZb6kpjH8SKh~FWHQ (note: this gets stale. Look at https://www.powsybl.org/pages/community/contact.html for updated version.)
- LFX Insights: https://insights.linuxfoundation.org/project/powsybl
- Other:
	- Roadmap: https://github.com/powsybl/.github/wiki/Roadmap
	- Maintainers: https://github.com/powsybl/.github/blob/main/MAINTAINERS.md

## Description

Modular framework for electrical grid modeling, simulation, and visualization.

## Overview

PowSyBl ("Power System Blocks") is a modular framework for electrical grid modeling and simulation. It provides the computational building blocks for grid planning and real-time operations of transmission grids — including load flow analysis, security analysis, sensitivity analysis, remedial action optimization, and network visualization. PowSyBl reads and writes industry-standard grid data formats such as CIM-CGMES, as well as vendor formats like Siemens PSS®E, enabling it to work with existing utility data infrastructure.

Grid operators face growing complexity from renewable integration, cross-border power flows, and tighter coordination requirements. PowSyBl is built for high-performance, cloud-native deployment, enabling the kind of large-scale analysis that modern grid operations demand. As open source software, it offers complete transparency — operators can inspect exactly how every calculation is performed, rather than relying on black-box solutions. And because the framework is modular, users can customize and extend it for their specific needs.

PowSyBl is used in production by grid operators. RTE (the French TSO) maintains the project and uses it across its grid operations. BalticRCC and Coreso — two of Europe's Regional Coordination Centers — use PowSyBl in production for functions including the European Merging Function, coordinated security analysis, and capacity calculation. Adoption extends beyond Europe, with broad format support enabling use across different grid modeling ecosystems. The framework is primarily written in Java with a Python binding (PyPowSyBl) for scripting and analysis workflows.

## Technical Profile

### What It Does

Provides grid modeling, power flow computation, security analysis, remedial action optimization, and network visualization for transmission-level power systems.
### Problem(s) Solved

Enables TSOs and RCCs to model, analyze, and coordinate transmission grids using a shared, standards-based framework — replacing fragmented proprietary tools with modular components that can be assembled for specific operational needs.

### Key Capabilities

- **Grid modeling and data exchange**: Import/export support for CIM-CGMES, UCTE-DEF, PSS®E, IEEE-CDF, Matpower, PowerFactory, and AMPL formats
- **Load flow analysis**: AC and DC load flow computation
- **Security analysis**: N-k contingency analysis with pre- and post-contingency remedial actions
- **Sensitivity analysis**: PTDF and PSDF calculations on network elements
- **Remedial action optimization**: Coordinated optimization of topological actions, PST regulation, HVDC setpoints, and redispatching
- **Grid reinforcement studies**: Multi-variant time-series simulation for planning studies
- **Network visualization**: Automated generation of network-area diagrams and single-line diagrams
- **Python interface**: PyPowSyBl binding for scripting, analysis, and Jupyter notebook integration
- **High-performance computing**: HPC support for large-scale parallel simulations

### Relevant Standards

- CIM-CGMES — Common Grid Model Exchange Standard
- UCTE-DEF (legacy European grid exchange format)

## Grid Context

### Grid Segment

Transmission

### Function

Grid Modeling, Simulation & Visualization

### Industry Solution Categories

#### Solution Type

- Network Analysis: Provides the core computational capabilities for transmission grid analysis

#### Component of

- EMS: Serves as the analytical engine for energy management systems, providing the computational capabilities that underpin real-time grid operations.
- Grid Planning: Enables transmission planning studies through multi-variant scenario analysis, sensitivity calculations, and network reinforcement evaluation.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **Dynaωo**: Tool for dynamic simulation (time-domain, transient stability). PowSyBl provides a wrapper (powsybl-dynawo) that enables Dynaωo's DynaFlow and DynaWaltz simulators to be invoked from within PowSyBl workflows, extending PowSyBl's steady-state capabilities with dynamic analysis.
- **Power Grid Model**: Both provide grid modeling and power flow analysis. PowSyBl focuses on transmission-level systems with CIM-CGMES support and TSO coordination workflows; Power Grid Model focuses on distribution-level analysis with a high-performance C++ core.
- **Arras**: Both are grid simulation projects. PowSyBl focuses on transmission; Arras focuses on distribution planning and DER integration. No direct technical integration.
- **FIDOpower**: FIDOpower provides cross-tool data exchange for power systems analysis. PowSyBl is a potential consumer/producer of data within such exchange workflows. No direct technical integration currently.
- **Grid2Op**: A backend (pypowsybl2grid) enables PowSyBl to serve as the power flow engine within Grid2Op's simulation environment for developing automated grid control strategies.
- **OpenSynth**: Integration — OpenSynth's D-GITT datasets publish transmission topology from the French network in PowSyBl's XIIDM format, loaded using pypowsybl. PowSyBl is the primary tool for working with D-GITT data.

## Maturity & Adoption

### LF Energy Stage

Early Adoption

### Deployment Maturity

Production

### Supporting / Adopting Companies

- RTE (production user, TSC member)
- BalticRCC (production user)
- Coreso (production user)
- Artelys (contributor, TSC member)
- Grupo AIA (contributor, TSC member)
- TenneT (production user)

## Learn More

- [GridSuite and PowSyBl: an Open Source approach to develop advanced tools for grid analysis and simulation of power systems](https://archive.fosdem.org/2024/schedule/event/fosdem-2024-1918-gridsuite-and-powsybl-an-open-source-approach-to-develop-advanced-tools-for-grid-analysis-and-simulation-of-power-systems-/)
	- Date: 2024-02-03
	- Type: Presentation
- [Sharing the operational cost of Europe's electricity grid: optimization and transparency through open source](https://archive.fosdem.org/2024/schedule/event/fosdem-2024-2640-sharing-the-operational-cost-of-europe-s-electricity-grid-optimization-and-transparency-through-open-source/)
	- Date: 2024-02-03
	- Type: Presentation
- PowSyBl: [Electrical Grid Modelling and Simulation Through PowSyBl - A Hands-On Approach](https://community.linuxfoundation.org/events/details/lfhq-lf-energy-presents-electrical-grid-modelling-and-simulation-through-powsybl-a-hands-on-approach/)
	- Date: 2024-06-03
	- Type: Presentation
- [European Merging Function made open source](https://lfenergysummit2024.sched.com/event/1ehIZ/european-merging-function-made-open-source-kristjan-vilgo-baltic-rcc-elering)
	- Date: 2024-09-05
	- Type: Presentation
- [Non-linear Optimal Power Flows in PowSyBl](https://lfenergysummit2024.sched.com/event/1ehI5/powsybl-ac-optimal-power-flows-nicolas-omont-artelys) 
	- Date: 2024-09-05
	- Type: Presentation
- [Baltic RCC's use of open source technology to meet energy transition challenges](https://lfenergy.org/baltic-rccs-use-of-open-source-technology-to-meet-energy-transition-challenges/)
	- Date: 2024-10-07
	- Type: Case Study
- [LFE project PowSyBl: Grid Modeling at the core of Europe’s power grid planning and operation](https://lfenergysummiteu2025.sched.com/event/26J6V/lfe-project-powsybl-grid-modeling-at-the-core-of-europes-power-grid-planification-and-operation-nicolas-omont-artelys)
	- Date: 2025-09-10
	- Type: Presentation
- [PowSyBl: A community-led open source project for European grid sovereignty](https://lfenergy.org/powsybl-a-community-led-open-source-project-for-european-grid-sovereignty/)
	- Date: 2025-10-21
	- Type: Case Study
- [Grid Security at Scale: How TenneT Built a 10× Faster Analysis Platform on PowSyBl](https://lfenergy.org/grid-security-at-scale-tennet-powsybl/)
    - Date: 2026-04-02
    - Type: Case Study

## Additional Notes

PowSyBl is one of the most operationally significant projects in the LF Energy ecosystem. Its use in production by multiple RCCs for pan-European coordination functions — including the European Merging Function, coordinated security analysis, and capacity calculation — represents a level of real-world deployment that few open source grid projects have achieved.

The project benefits from a healthy commercial ecosystem. Artelys builds and sells commercial products and services on top of PowSyBl, demonstrating that the open source model can sustain vendor businesses while keeping the core framework open. The MPL v2 license (weakly copyleft) is commercial-friendly, allowing proprietary extensions while requiring modifications to PowSyBl itself to remain open.

PowSyBl has strong adoption in Europe, driven by the ENTSO-E coordination framework that requires TSOs and RCCs to exchange grid models and coordinate operations using common standards (particularly CIM-CGMES). European public procurement practices that allow or encourage open source software further support adoption. The framework's support for widely-used formats like PSS/E, Matpower, and IEEE-CDF reflects its applicability beyond European markets.
