# p-SWAMP

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

- LF Energy webpage: https://lfenergy.org/projects/p-swamp/
- Website:
- Code: https://github.com/p-swamp/P-SWAMP
- Documentation:
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/swamp?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/p-swamp-discussion
	- Slack: https://lfenergy.slack.com/archives/C09H29H24TX
- LFX Insights:
- Other:

## Description

R&D platform for developing and validating Wide Area Monitoring, Protection, and Control (WAMPAC).

## Overview

p-SWAMP (Power Stability Wide Area Monitoring and Protection) is a research and development platform for Wide Area Monitoring, Protection, and Control (WAMPAC). It ingests high-resolution synchrophasor data from Phasor Measurement Units (PMUs), distributes it to independent monitoring applications via a message bus, and provides real-time analysis of transmission grid stability — including electromechanical oscillation detection, islanding detection, voltage stability monitoring, and line outage detection. Results are displayed through interactive 2D and 3D geographic visualizations with an integrated alarm handling system.

As transmission grids absorb more inverter-based resources (wind, solar) and HVDC interconnections, they face new stability challenges: lower system inertia, faster frequency dynamics, and more complex oscillation patterns. Traditional SCADA monitoring operates at second-to-minute timescales and cannot capture these fast-moving phenomena. PMU-based wide-area monitoring provides the millisecond-resolution visibility needed to detect emerging stability issues — but the algorithms, visualization approaches, and architectural patterns for WAMPAC systems are still an active area of research. p-SWAMP provides a shared environment for developing and validating these capabilities before they are transferred to production systems.

p-SWAMP is explicitly a research sandbox, not a production deployment target. Algorithms and approaches validated in p-SWAMP are intended to flow into production tools built by vendors and utilities. The platform is developed by Statnett (the Norwegian TSO) together with research partners SINTEF Energy Research, NTNU, IFE, and Unicus+auticon. It builds on code from the NEWEPS (Nordic Early Warning Early Prevention System) research project (2020–2024). Statnett currently operates approximately 180 PMUs across its transmission grid and uses an existing commercial WAMS for back-office post-analysis; p-SWAMP aims to advance capabilities beyond what commercial systems provide today.

## Technical Profile

### What It Does

Provides a modular platform for developing and testing real-time monitoring applications that process PMU synchrophasor data to assess transmission grid stability, with interactive geographic visualization and alarm coordination.

### Problem(s) Solved

Gives TSO R&D teams and research partners a shared, vendor-independent environment for developing and validating WAMPAC algorithms and visualization approaches. Without a common platform, each research project builds its own ad-hoc infrastructure, limiting continuity between projects and making it harder to transfer results to production.

### Key Capabilities

- Microservice architecture where monitoring applications run as independent processes, communicating via a shared message bus (Apache Kafka, MQTT, or a lightweight built-in alternative) — new applications can be added without modifying existing ones
- Application framework with reusable templates for building real-time monitoring applications, handling data windowing, timing, status reporting, and alarm generation
- PMU data ingestion from Phasor Data Concentrators via IEEE C37.118, with support for additional data sources including real-time simulators and historical data playback
- Interactive 2D and 3D geographic grid visualization with configurable overlays (voltage phasors, frequency heatmaps, bus voltages, oscillation mode shapes) and drill-down into sub-grid regions
- Alarm handling system with cross-TSO coordination, context-specific diagnostic views, and operator acknowledgment workflow
- Sample monitoring applications included for oscillation detection (N4SID modal analysis), islanding detection, voltage stability assessment, and line outage detection

### Relevant Standards

- IEEE C37.118 (Synchrophasor): Receives and parses synchrophasor data frames from Phasor Data Concentrators as its primary data input interface.

## Grid Context

### Grid Segment

Transmission

### Function

Grid Operations

### Industry Solution Categories

#### Solution Type

- WAMPAC Research Platform: Provides a modular, vendor-independent environment for developing and validating wide-area monitoring, protection, and control applications using PMU synchrophasor data. Not intended for production deployment — validated algorithms and approaches are designed to transfer to production systems.

#### Component of

- WAMPAC: Develops and validates the monitoring algorithms and visualization approaches that form the monitoring layer of Wide Area Monitoring, Protection, and Control systems.

### Cross-Cutting Tags

- **Project Intent:** Research
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **dynaωo**: Potentially complementary — dynaωo performs dynamic simulation of transmission systems, which could generate synthetic PMU data streams for testing p-SWAMP monitoring applications. p-SWAMP's architecture accepts simulation data as input alongside real PMU streams. No current code integration exists; this is an identified area of interest from the p-SWAMP team.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Organizations

- Statnett (primary developer; Norwegian TSO)
- SINTEF Energy Research (research partner)
- NTNU (research partner)
- IFE — Institute for Energy Technology (research partner)
- Unicus+auticon Norway (research partner)

## Learn More

- [Wide Area Monitoring, Protection, and Control (WAMPAC)](https://lfenergysummiteu2025.sched.com/event/26J0S/wide-area-monitoring-protection-and-control-wampac-a-necessity-for-secure-monitoring-operation-kjell-petter-myhren-statnett-geir-borse-unicus+auticon-norway)
	- Date: 2025-09-11
	- Type: Presentation
- Statnett R&D WAMPAC power- Wide Area Monitoring Protection (p-SWAMP)
	- Date: 2025-09-02
	- Type: Presentation
- [TAC proposal: Power Stability Wide Area Monitoring Protection (p-SWAMP)](https://github.com/lf-energy/tac/issues/585)
	- Date: 2025-07-18
	- Type: TAC Proposal
- Code snapshot
	- Date: 2026-03-09
	- Type: Code

## Additional Notes

p-SWAMP is, to our knowledge, the only open source WAMS/WAMPAC research platform. Commercial WAMS products exist (e.g., Statnett currently uses one for back-office post-analysis), but they are proprietary, vendor-specific, and focused on operational use rather than R&D. p-SWAMP's value proposition is providing a vendor-independent, shared R&D environment where TSOs, research institutions, and vendors can collaboratively develop and validate next-generation WAMPAC capabilities — algorithms, visualizations, and architectural patterns — that then transfer into production tools.

A common misconception may be that p-SWAMP is a WAMS product at an early maturity stage that will eventually be deployed in production. This is not the case — it is by design a permanent R&D sandbox. The project's success is measured not by its own production deployment, but by the production impact of the capabilities developed within it.