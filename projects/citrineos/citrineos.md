# CitrineOS

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

- LF Energy webpage: https://lfenergy.org/projects/citrineos/
- Website:
- Code: https://github.com/citrineos
- Documentation: https://citrineos.github.io/latest/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/citrineos?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
	- Discord: https://discord.gg/kkUxF7pRU7
- LFX Insights: https://insights.linuxfoundation.org/project/citrineos
- Other:

## Description

Modular charging station management system (CSMS) supporting both OCPP 1.6 and OCPP 2.0.1 for managing EV charging networks.

## Overview

CitrineOS is a charging station management system (CSMS) — the cloud-side software that manages a network of EV chargers. It communicates with charging stations via the Open Charge Point Protocol (OCPP) to handle station configuration, driver authorization, transaction tracking, smart charging profiles, and remote monitoring and control. CitrineOS supports both OCPP 1.6 and OCPP 2.0.1, allowing operators to manage mixed-protocol fleets of legacy and next-generation chargers from a single system.

Building a standards-compliant CSMS from scratch is a significant undertaking — OCPP alone involves hundreds of message types, security requirements, and edge cases, and each independent implementation introduces its own interoperability bugs. CitrineOS provides a shared foundation that dramatically accelerates CSMS deployment. Organizations building charging networks — whether CPOs, fleet operators, utilities, or technology vendors — can start from a production-grade OCPP implementation rather than building commodity protocol handling themselves, and focus their effort on the features and services that differentiate their offering.

CitrineOS is built as a modular TypeScript/Node.js application designed for cloud deployment. Each OCPP functional block (configuration, transactions, monitoring, smart charging, certificates) runs as an independent module, making it straightforward to extend, customize, or integrate into a larger platform alongside roaming (OCPI), payment, and fleet management systems. The project is OCA-certified for OCPP 2.0.1 Core and Advanced Security, and supports the OCPP 2.0.1 requirements for U.S. NEVI-funded deployments. S44 Energy initiated the project and offers a commercial distribution (TopazEV) with managed hosting and enterprise support.

## Technical Profile

### What It Does

Receives OCPP messages from EV charging stations over WebSocket, processes them through modular functional blocks (configuration, transactions, monitoring, smart charging, certificates, authorization), and exposes REST and GraphQL APIs for operator management and third-party integration.

### Problem(s) Solved

**For CPOs and fleet operators:** Provides a ready-to-deploy CSMS foundation that supports both OCPP 1.6 and 2.0.1, enabling rapid deployment of charging network management without building OCPP handling from scratch. Operators can be managing chargers in weeks rather than months.

**For CSMS solution builders:** Offers a certified, modular OCPP implementation that can be extended and embedded into commercial charging platforms, reducing development cost and improving interoperability through a shared standards implementation.

### Key Capabilities

- **Dual-protocol OCPP support**: Manages both OCPP 1.6 and OCPP 2.0.1 charging stations from a unified data model — one collection of locations, stations, authorizations, and transactions regardless of protocol version
- **Smart charging**: Supports charging profile management (SetChargingProfile, ReportChargingProfiles) for operator-directed load management across stations
- **Certificate management**: X.509 certificate handling for ISO 15118 Plug & Charge authorization, firmware signing, and secure WebSocket connections
- **Monitoring and remote control**: Real-time station monitoring (events, variables, security events), remote configuration, reset, and firmware update capabilities
- **OCPI roaming support**: Open Charge Point Interface implementation for EV roaming hub integration (available as a separate module, `citrineos-ocpi`)
- **Operator UI**: Web-based management interface for station monitoring, OCPP log inspection, configuration, and transaction management
- **Extensible module architecture**: Each OCPP functional block is an independent module with decorator-based message routing, allowing custom modules and overrides without modifying core code
- **OpenAPI and GraphQL APIs**: REST endpoints with auto-generated OpenAPI specification; GraphQL API for flexible data queries and integration with billing, fleet management, and other platform systems

### Relevant Standards

- **OCPP 1.6 / 2.0.1** (IEC 63584): Open Charge Point Protocol for charger-to-CSMS communication (certified for 2.0.1 Core and Advanced Security)
- **OCPI 2.2.1**: Open Charge Point Interface for EV roaming (via separate `citrineos-ocpi` module, not part of core)

## Grid Context

### Grid Segment

Behind the Meter

### Function

Flexibility & Markets — EV Charging

### Industry Solution Categories

#### Solution Type

- Charging Station Management System (CSMS): Provides the cloud-side management platform for EV charging networks, handling OCPP communication, station monitoring, driver authorization, and transaction management.

#### Component of

- EV Charging Management Software Platform: Serves as the OCPP-based station management core that integrates with roaming, payment, and fleet management systems to form a complete CPO operational platform.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **EVerest**: Complementary vertical integration. EVerest is the charger-side firmware stack; CitrineOS is the cloud-side management system. They connect via OCPP — chargers running EVerest communicate with a CitrineOS backend for remote management, session tracking, and configuration. CitrineOS documentation includes integration testing guidance with Dockerized EVerest simulators.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

Production

### Supporting / Adopting Organizations

- S44 Energy (project initiator, primary contributor; offers TopazEV commercial distribution built on CitrineOS)

## Learn More

- CitrineOS: Bridging the Past and Future of EV Charging with OCPP 1.6 & 2.x Support
	- Date: 2025-04-09
	- Type: Webinar

## Additional Notes

CitrineOS is, to our knowledge, the only OCA-certified open source CSMS. This positions it similarly to how EVerest commoditizes charging station firmware — providing shared infrastructure for standards-compliant OCPP communication so that companies building charging platforms can focus their development effort on differentiation (network services, driver experience, fleet integrations, energy management) rather than reimplementing commodity protocol handling.

The strategic timing is driven by the OCPP 1.6-to-2.0.1 transition. OCPP 2.0.1 was accepted by IEC as IEC 63584 in 2024 and is the target standard for U.S. NEVI-funded deployments, but the vast majority of deployed chargers still use OCPP 1.6. CitrineOS's dual-protocol support directly addresses this transition — operators can onboard new 2.0.1 chargers while continuing to manage their existing 1.6 fleet, with a unified data model that abstracts protocol differences.