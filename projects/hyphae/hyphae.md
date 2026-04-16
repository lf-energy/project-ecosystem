# Hyphae

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

- LF Energy webpage: https://lfenergy.org/projects/hyphae/
- Website: https://github.com/hyphae
- Code: https://github.com/hyphae
- Documentation: https://lf-energy.atlassian.net/wiki/spaces/HYP/overview
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/hyphae?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/hyphae
- Other:

## Description

Microgrid controller that enables autonomous peer-to-peer energy sharing between distributed battery systems on DC microgrids.

## Overview

Hyphae provides software for controlling microgrids, with its core component being APIS (Autonomous Power Interchange System). APIS manages power flows between distributed battery systems connected on a DC microgrid, enabling peer-to-peer energy sharing between participants. Each battery node runs identical APIS software that autonomously negotiates energy transfers with other nodes based on its battery state of charge and configured rules, using bidirectional DC/DC converters to execute the physical power transfers. The system uses no permanent central coordinator — nodes self-organize and dynamically elect a Grid Master role within each cluster to facilitate coordination.

The core problem Hyphae addresses is the control complexity of community microgrids. In a neighborhood or campus with multiple solar-plus-storage systems, energy produced at one site may exceed local demand while a nearby site has depleted batteries. Without a microgrid controller, this surplus is either wasted or exported to the main grid at unfavorable rates. APIS enables these systems to share energy directly with each other on a local DC grid, improving collective self-consumption of locally generated renewable energy and providing community-level resilience.

APIS was originally developed by Sony Computer Science Laboratories (Sony CSL) and contributed to LF Energy in 2021. The software runs on embedded controllers alongside battery systems and DC/DC converters. It includes a hardware emulator for development and testing without physical equipment, a web-based service center for monitoring cluster status and energy sharing history, and a configuration management client for distributing settings across nodes.

## Technical Profile

### What It Does

Manages autonomous peer-to-peer energy transfers between distributed battery systems on a DC microgrid, with the system using constant current control through bidirectional DC/DC converters to execute precise power transfers.

### Problem(s) Solved

Enables communities with distributed solar-plus-storage systems to share locally generated energy between participants on a DC microgrid, without requiring a permanent centralized controller or manual coordination. Improves collective self-consumption of renewable generation and provides local energy resilience.

### Key Capabilities

- Autonomous peer-to-peer energy negotiation and transfer between battery nodes on a DC microgrid, with nodes self-organizing and dynamically electing a Grid Master role within each cluster
- Constant current control at the system level (software + DC/DC converter hardware) for precise energy sharing between specific battery systems, enabling fixed-amount power transfers based on energy amounts and pricing conditions
- Fully distributed architecture where identical software runs on every node, allowing heterogeneous behavior policies based on individual battery capacity thresholds
- Web-based service center for real-time monitoring of unit status, energy sharing history, abnormality notifications, and per-unit availability metrics, with clusters organized into communities for centralized management
- Scenario management for configuring energy sharing rules per node
- Configuration management client (apis-ccc) for uploading energy sharing data to external services and downloading node configuration files across the network
- Hardware emulator that simulates battery systems, DC/DC converters, solar generation, and residential consumption patterns for development and testing without physical equipment

### Relevant Standards

None. APIS uses a proprietary peer-to-peer negotiation protocol over TCP/IP. The broader Hyphae program vision references integration with devices using SunSpec (for PV and storage) and OCPP (for EV chargers), but APIS itself does not implement these standards.

## Grid Context

### Grid Segment

Behind the Meter

### Function

Flexibility & Markets

### Industry Solution Categories

#### Solution Type

- DC Microgrid Power Sharing Controller: Manages autonomous power flows between distributed battery systems on a DC microgrid through peer-to-peer negotiation and bidirectional DC/DC converter control.

#### Component of

- Microgrid Controller: Provides the DC-bus power sharing layer within a broader microgrid controller, handling autonomous energy transfers between distributed battery nodes.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **OpenLEADR**: Complementary — the Hyphae program envisions using OpenLEADR as a VEN (Virtual End Node) alongside the Hyphae site EMS to receive utility demand response signals via OpenADR, enabling the microgrid to participate in utility DR programs. This integration has been demonstrated in reference architectures (as of September 2024 presentation) but should be verified in code.
- **EVerest**: Complementary — in the broader Hyphae program vision (as of September 2024 presentation), the site EMS manages EV charging stations via OCPP. EVerest is the firmware stack running inside those chargers. In a Hyphae-managed microgrid with solar, storage, and EV charging, EVerest-equipped chargers would be the grid-edge devices receiving charging commands from the Hyphae site EMS over OCPP. This integration is aspirational and not yet reflected in the current codebase.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- Sony Computer Science Laboratories (Sony CSL) — original developer of APIS; contributed the codebase to LF Energy in 2021
- Energy IoT Open Source (Arila Barnes, TSC as of September 2024)
- RWTH Aachen University (Asimenia Korompili, TSC as of September 2024)
- Kaleidoscope (Suparna Pal, TSC as of September 2024)

## Learn More

- [How open source can enable your next microgrid community project?](https://lfenergysummit2024.sched.com/event/1h5g1/how-open-source-can-enable-your-next-microgrid-community-project-arila-barnes-energy-iot-open-source)
	- Date: 2024-09-06
	- Type: Presentation

## Additional Notes

The name "Hyphae" is a biological metaphor: hyphae are the filament-like threads that transport resources between fungi, plants, and trees in forest ecosystems — analogous to how the software transfers energy between nodes in a microgrid.

It is important to distinguish between the APIS codebase and the broader Hyphae program vision. The actual code in the `hyphae` GitHub organization is specifically the APIS DC microgrid peer-to-peer energy sharing system. The broader Hyphae program, as presented at LF Energy Summit 2024, envisions a wider scope that includes DC/AC microgrid energy management (integrating PV, battery storage, and EV chargers via external tools like OpenEMS and Odoo) and demand response support via OpenLEADR. These broader integrations are aspirational and reference external projects that are not part of Hyphae itself. This overview describes what APIS currently delivers based on the code.

The project is at an early stage with a small contributor community. The APIS codebase was originally developed by Sony CSL for research purposes and is being adapted for broader use through the Hyphae project. The emulator component enables experimentation and development without physical DC microgrid hardware, which lowers the barrier to entry for potential contributors and evaluators.