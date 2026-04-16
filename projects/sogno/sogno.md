# SOGNO

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

- LF Energy webpage: https://lfenergy.org/projects/sogno/
- Website: https://sogno.energy/
- Code: https://github.com/sogno-platform
- Documentation: https://sogno.energy/docs/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/sogno?view=month
- LinkedIn:
- Community:
	- TSC Mailing List: https://lists.lfenergy.org/g/SOGNO-TSC
	- Discussion Mailing List: https://lists.lfenergy.org/g/sogno-discussion
	- Slack:
		- SOGNO: https://lfenergy.slack.com/archives/C01JBQ1F605
		- SOGNO DPSIM: https://lfenergy.slack.com/archives/C054GB551TL
- LFX Insights: https://insights.linuxfoundation.org/project/sogno
- Other:
	- TSC meeting minutes: https://lf-energy.atlassian.net/wiki/spaces/SOG/pages/31687247/SOGNO+TSC

## Description

Modular collection of microservices and libraries for distribution grid monitoring, simulation, and automation.

## Overview

SOGNO (Service-based Open-source Grid automation platform for Network Operation of the future) provides a set of cloud-native microservices and libraries for distribution grid automation. Its components address core DSO operational needs — state estimation, load forecasting, power system simulation, and grid data modeling — each deployable as an independent containerized service. The platform uses CIM/CGMES as its grid data model and communicates via message brokers (Kafka, MQTT), enabling integration with existing SCADA/DMS infrastructure without replacing it.

SOGNO addresses the challenge facing DSOs as distribution grids shift from passive to active networks. Growing penetrations of distributed generation, EVs, and flexible loads require levels of monitoring, automation, and coordination that traditional monolithic DMS platforms were not designed to support. Rather than replacing those systems wholesale, SOGNO offers a modular approach: a DSO can adopt individual capabilities (e.g., state estimation for low-voltage observability, or load forecasting) and integrate them incrementally into existing operations.

In practice, SOGNO functions more as a toolkit of related but loosely-coupled components than as a single integrated platform. Several components — particularly the DPsim real-time simulator and the CIM data modeling libraries — are widely used as standalone tools independent of the broader SOGNO platform. The project originated from EU Horizon 2020 research (the SOGNO and Platone projects) led by RWTH Aachen University and has been demonstrated in field trials with DSOs in Italy, Romania, Ireland, and Germany.

## Technical Profile

### What It Does

Provides a collection of microservices and libraries that perform distribution grid automation functions — including state estimation, power system simulation, load forecasting, and CIM-based grid data modeling.

### Problem(s) Solved

Enables DSOs to add advanced grid monitoring and automation capabilities to their existing operational systems incrementally, without replacing monolithic DMS platforms. Provides reusable, standards-based tools for distribution grid analysis and simulation that can be assembled according to each operator's needs.

### Key Capabilities

**Power System Simulation (DPsim)**
- Real-time and faster-than-real-time dynamic power system simulation
- Electromagnetic transient (EMT) and dynamic phasor simulation domains
- Supports real-time execution with timesteps down to 50 microseconds
- Available as a C++ library with Python bindings (pip-installable)

**CIM Grid Data Modeling (CIMpy, CIMgen, libcimpp, Pintura)**
- Import/export of CIM-CGMES (IEC 61970) grid data in XML/RDF format (CIMpy for Python, libcimpp for C++)
- Code generation from CIM data model definitions for multiple target languages (CIMgen)
- Web-based graphical CIM topology editor and viewer (Pintura)

**Distribution State Estimation (pyvolt)**
- State estimation and power flow algorithms for distribution networks
- Uses CIM-based grid models via CIMpy

**Load and Generation Forecasting (ProLoaF)**
- Probabilistic load forecasting using deep learning
- PV and wind generation forecasting

**DER and Flexibility Management (datafev, pymfm)**
- EV fleet charging optimization algorithms (datafev)
- Microgrid flexibility management for coordinating local DER dispatch (pymfm)

### Relevant Standards

- CIM-CGMES (IEC 61970) — Grid data model; directly implemented by CIMpy, libcimpp, and CIMgen for data import/export and code generation

## Grid Context

### Grid Segment

Distribution

### Function

Grid Operations (primary), Grid Modeling & Simulation (secondary)

### Industry Solution Categories

#### Solution Type

- Power System Simulation: DPsim provides real-time dynamic power system simulation, supporting EMT and dynamic phasor analysis.
- Grid Data Modeling: CIMpy, CIMgen, libcimpp, and Pintura provide CIM/CGMES data handling — import/export, code generation, and visual topology editing.
- Distribution State Estimation: pyvolt provides state estimation and power flow for distribution networks using CIM-based grid models.
- Load Forecasting: ProLoaF provides probabilistic load and PV generation forecasting.

#### Component of

- ADMS: SOGNO's monitoring and automation services (state estimation, forecasting, simulation) collectively serve as modular building blocks for an Advanced Distribution Management System.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **Power Grid Model**: Both provide distribution-level power system analysis. Power Grid Model is a high-performance calculation library (power flow, state estimation, short circuit) optimized for batch analysis at scale. SOGNO's pyvolt provides distribution state estimation with a CIM-native data model. Power Grid Model's calculation engine could serve as an alternative or complementary analytical backend within the SOGNO platform architecture.
- **OpenSTEF**: Complementary forecasting tools. OpenSTEF provides production-grade short-term energy load forecasting for operational use. SOGNO's ProLoaF provides probabilistic load forecasting with a research focus.

## Maturity & Adoption

### LF Energy Stage

Early Adoption

### Deployment Maturity

R&D

Component maturity varies significantly. DPsim and the CIM tooling are the most mature and actively maintained components, with broader use in research and academic settings. The integrated platform services (state estimation, forecasting APIs) were demonstrated in EU-funded field trials but have not reached production deployment at utilities.

### Supporting / Adopting Companies

- RWTH Aachen University (primary developer, project coordinator)
- Fraunhofer FIT — Digital Energy (active development, technical lead)
- areti (Acea group) — RomeFlex pilot deployment in Rome
- Avacon — Energieplattform Twistringen pilot (Kopernikus ENSURE project)
- Research Center Jülich (contributor)

**EU project field trial participants:**
- CEZ Distribution (Romania — state estimation and load forecasting)
- ESB Networks (Ireland)

## Learn More

- [RomeFlex: SOGNO Platform in Action](https://lfenergysummit2024.sched.com/event/1ehHe/romeflex-sogno-platform-in-action-antonello-monti-rwth-aachen-university)
	- Date: 2024-09-05
	- Type: Presentation

## Additional Notes

SOGNO is structurally different from most LF Energy projects. Rather than a single coherent codebase, it is an umbrella for ~34 repositories spanning several distinct functional domains. Some of these — particularly DPsim (the most popular component by GitHub stars and community engagement) and the CIM tooling suite — have independent value and user communities that extend well beyond the integrated platform vision. This creates an unusual dynamic where the umbrella project's identity is broader than any single component, but the components are often more practically useful than the integrated whole.

The platform integration layer — the service wrappers, APIs, and deployment tooling that would stitch individual components into a coherent DSO platform — is the least actively maintained part of the project. Several service repositories have not been updated since 2023. This suggests the project's near-term value lies more in its individual libraries and tools than in its platform-level integration, though the architectural vision of a modular, microservices-based DSO platform remains the project's stated direction.

The project's academic roots (RWTH Aachen, Fraunhofer FIT, EU research funding) are reflected in its contributor base, which is primarily researchers rather than utility software engineers. This distinguishes it from projects like Power Grid Model or PowSyBl, which have commercial utility adoption driving development priorities.
