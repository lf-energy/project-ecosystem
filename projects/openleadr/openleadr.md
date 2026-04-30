# OpenLEADR

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

- LF Energy webpage: https://lfenergy.org/projects/openleadr/
- Website:
- Code: https://github.com/openleadr
- Documentation:
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/openleadr?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/openleadr
	- Slack: https://lfenergy.slack.com/archives/C045K9YGX52
- LFX Insights: https://insights.linuxfoundation.org/project/openleadr
- Other:

## Description

Reference implementations of the OpenADR standard for automated demand response communication between utilities and grid-connected devices.

## Overview

OpenLEADR provides implementations of the OpenADR (Open Automated Demand Response) standard, which defines how a grid operator or aggregator communicates demand response signals to devices and systems that can adjust their energy consumption. The standard uses a client-server model: a Virtual Top Node (VTN) operated by the utility or aggregator publishes demand response programs containing price signals, usage limits, or event notifications, and Virtual End Nodes (VENs) on the device or aggregator side receive those signals and report back on their response. OpenLEADR's active implementation, openleadr-rs, is a Rust-based OpenADR 3.0 VTN server and VEN client library.

Demand response is a key tool for managing grid congestion without building new infrastructure. When a distribution grid approaches capacity limits — due to electrification, EV charging coincidence, or distributed generation — the operator needs a standardized way to signal devices to reduce or shift their consumption. Without a common protocol, each utility-device integration requires custom development. OpenADR provides that common protocol, and OpenLEADR provides an implementation that any party can deploy, avoiding dependence on proprietary demand response platforms.

The primary use case driving OpenLEADR development is Grid Aware Charging (GAC) in the Netherlands, where Dutch DSOs use OpenADR to signal EV charge point operators (CPOs) to adjust charging behavior during grid congestion. OpenLEADR is developed jointly by ElaadNL (the Dutch knowledge and innovation center for charging infrastructure) and Tweede Golf (a Rust software consultancy).

## Technical Profile

### What It Does

Provides an OpenADR 3.0 VTN server and VEN client library that enable automated demand response communication — the VTN publishes programs and events (price signals, usage limits), and VENs poll for those events and submit reports on their response.

### Problem(s) Solved

Gives utilities and aggregators a standards-based way to signal demand response to grid-connected devices without proprietary platforms or custom integrations. Enables CPOs, building management systems, and other load controllers to receive and act on grid operator signals through a common protocol.

### Key Capabilities

- OpenADR 3.0 VTN server with REST API, deployable as a single binary or via Docker
- VEN client library for integrating demand response signal reception into devices or aggregator platforms
- CRUD operations for programs, events, reports, VENs, and resources
- Authentication and authorization via built-in OAuth provider, with support for third-party OAuth
- Fine-grained access control for multi-tenant deployments
- PostgreSQL backend for data persistence
- Passes 128 of 168 OpenADR Alliance test cases; 38 failures relate to the unimplemented subscription (webhook) feature, and 2 to access control granularity differences
- CLI tool for testing and prototyping (in progress)

### Relevant Standards

- OpenADR 3.0 (OpenADR Alliance) — the project implements the OpenADR 3.0 specification for demand response communication

## Grid Context

### Grid Segment

Distribution (primary), Behind the Meter (secondary)

### Function

Flexibility & Markets

### Industry Solution Categories

#### Solution Type

- Demand Response Communication Platform: Provides VTN and VEN implementations for automated demand response signaling per the OpenADR standard.

#### Component of

- DERMS: Provides the demand response signaling layer that a DERMS uses to communicate price signals and usage limits to distributed energy resources.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **Shapeshifter**: Adjacent protocol, different model — Shapeshifter implements UFTP, a flexibility *trading* protocol with bilateral negotiation, bidding, and financial settlement. OpenLEADR implements OpenADR, a demand response *signaling* protocol where a utility sends signals and devices respond. They can be complementary: an aggregator could receive a flex order via Shapeshifter and dispatch its devices via OpenADR signals delivered through OpenLEADR.
- **EVerest**: Complementary for EV charging — EVerest manages charge point operations (OCPP, ISO 15118), while OpenLEADR provides the grid signal interface. An experimental EVerest module (RsOpenADR3) uses openleadr-rs to receive demand response signals from a VTN and translate them into EVerest energy limits, enabling grid operators to manage EV charging load via OpenADR. Not yet merged to the EVerest main branch.
- **FlexMeasures**: Complementary — FlexMeasures computes optimal schedules for flexible assets, while OpenLEADR provides the OpenADR signaling layer to communicate demand response signals to devices. An aggregator could use FlexMeasures to determine the optimal charging profile and OpenLEADR to signal EV chargers to execute it.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

R&D

### Supporting / Adopting Organizations

- ElaadNL (primary developer/sponsor — Dutch knowledge and innovation center for charging infrastructure)
- Tweede Golf (primary developer — Rust software consultancy)

## Learn More

- [Rust Meets the Grid: Building openleadr-rs for Real-World Demand Response](https://lfenergysummiteu2025.sched.com/event/26Iyx/rust-meets-the-grid-building-openleadr-rs-for-real-world-demand-response-hugo-van-de-pol-tweede-golf-ton-smets-elaadnl)
	- Date: 2025-09-11
	- Type: Presentation

## Additional Notes

OpenLEADR was revived with an OpenADR 3.0 implementation (openleadr-rs) after the original maintainer of the OpenADR 2.0b Python implementation stepped away. The Python library (openleadr-python) remains available but is no longer actively developed. The openleadr-rs implementation joined the existing LF Energy OpenLEADR project in fall 2024.

The OpenADR standard originated at Lawrence Berkeley National Laboratory in 2009 and is managed by the OpenADR Alliance. Version 3.0 (released 2024) provides a simplified REST/JSON API as an alternative to the XML-based 2.0b specification (2015). OpenADR 3.1 was released in August 2025; openleadr-rs has a 3.1 implementation branch in development.

The Dutch Grid Aware Charging (GAC) initiative — based on the Dutch National Charging Infrastructure Agenda — is the primary adoption context. Dutch DSOs (Alliander, Enexis, Stedin) and CPOs are using OpenADR profiles to coordinate EV charging with grid capacity, addressing nationwide grid congestion. ElaadNL's involvement as both a domain expert in charging infrastructure and a primary developer of openleadr-rs positions the project at the intersection of the EV charging and grid operations domains.

The project is dual-licensed under Apache 2.0 and MIT.