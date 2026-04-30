# GXF (Grid eXchange Fabric)

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

- LF Energy webpage: https://lfenergy.org/projects/gxf/
- Website:
- Code: https://github.com/OSGP
- Documentation: https://grid-exchange-fabric.gitbook.io/gxf/ <!-- note that the documentation appears to be fairly stale and may not be entirely accurate -->
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/grid-exchange-fabric?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/gxf
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/grid-exchange-fabric
- Other:

## Description

IoT device management platform for communication between utility applications and grid field devices.

## Overview

GXF is a middleware platform that sits between utility business applications and the diverse field devices deployed across a distribution grid. It provides a single, protocol-neutral interface through which applications can monitor and control devices — regardless of the underlying communication protocol each device uses. GXF handles the translation between functional requests (e.g., "read this meter" or "set this lighting schedule") and the specific wire protocol required by each device type, including DLMS/COSEM for smart meters, IEC 61850 and IEC 60870-5-104 for distribution automation equipment, and MQTT.

The core problem GXF solves is device fleet management at scale across a heterogeneous field device landscape. Distribution operators deploy hundreds of thousands to millions of devices from multiple vendors, each speaking different protocols. Without a middleware layer, every business application needs to understand every protocol — creating integration complexity that grows multiplicatively. GXF centralizes protocol handling, device lifecycle management, security (key management, authentication, authorization), and command scheduling into a shared platform, so business applications can focus on their domain logic rather than device communication.

GXF was developed by Alliander starting in 2012 and contributed to LF Energy in 2020. As of September 2024, Alliander reports managing approximately 6 million smart meters, 20,000 public lighting switching devices, and 8,000 low-voltage measurement devices in production, processing over 10 million events per day including 5 million+ meter readouts. Newer use cases include battery-powered RTUs for cable oil pressure monitoring, cathodic protection, and fault detection, as well as MSR Gateway RTU Edge devices for substation monitoring.

## Technical Profile

### What It Does

Provides a protocol-abstraction layer and device management platform that enables utility applications to communicate with and control heterogeneous field devices through a single unified interface.

### Problem(s) Solved

Enables utilities to manage large fleets of field devices from multiple vendors and protocols through a single platform, eliminating the need for each business application to implement device-specific protocol handling. Centralizes security, scheduling, firmware management, and device lifecycle operations that would otherwise be duplicated across applications.

### Key Capabilities

- **Multi-protocol device communication**: Protocol adapters for DLMS/COSEM (smart metering), IEC 61850 (distribution automation), IEC 60870-5-104 (SCADA/RTU), MQTT, and OSLP (public lighting). New protocol adapters can be added without changes to the application layer.
- **Device lifecycle management**: Registration, configuration, firmware updates, key rotation, and decommissioning of field devices.
- **Smart metering head-end**: Meter data retrieval (daily/interval/monthly for electricity and gas), power quality monitoring, outage detection, M-Bus sub-meter coupling, and alarm management. Supports meters from Kaifa, Landis+Gyr, Iskra, and Itron.
- **Public lighting management**: Switching schedules (astronomical time and fixed-time), dimming control, relay management, burn-hours reporting, and batch operations across device groups.
- **Low-voltage grid monitoring**: Measurement of outgoing LV fields and transformer conditions using Rogowski coils, supporting congestion detection and energy fraud identification.
- **Scheduling and batch operations**: Time-based command scheduling for recurring operations like tariff switching and lighting schedules.
- **Security and key management**: End-to-end message signing, multi-level encryption (DLMS HLS3/4/5), organizational authorization per device per function, and credential lifecycle management with HSM integration.
- **Multi-tenant authorization**: Multiple organizations and applications can share the platform with scoped access control per device function.
- **Scalability**: Designed and load-tested for millions of concurrent devices with asynchronous request/response handling.

### Relevant Standards

- IEC 62056 (DLMS/COSEM) — Smart meter communication protocol, directly implemented as a protocol adapter for reading and managing electricity and gas meters.
- IEC 61850 — Substation and distribution automation communication protocol, directly implemented as a protocol adapter (specifically IEC 61850-8-1 / MMS).
- IEC 60870-5-104 — Telecontrol protocol for SCADA/RTU communication, directly implemented as a protocol adapter.

## Grid Context

### Grid Segment

Distribution

### Function

Grid Operations

### Industry Solution Categories

#### Solution Type

- IoT Device Management Platform: Provides centralized communication, control, and lifecycle management for grid-connected field devices across multiple protocols.

#### Component of

- Advanced Metering Infrastructure (AMI): Serves as the smart meter head-end system, managing meter communication, data retrieval, firmware updates, and key management.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **GEISA**: Both address the grid edge, but with different approaches. GEISA defines a runtime environment and app ecosystem for edge devices. GXF manages those devices from a central platform. A GEISA-compliant device could potentially be managed through a GXF protocol adapter.

## Maturity & Adoption

### LF Energy Stage

Early Adoption

### Deployment Maturity

Production

### Supporting / Adopting Organizations

- Alliander (founding contributor and primary maintainer)

## Learn More

- [Physical and Digital Worlds Come Together in GXF](https://lfenergysummit2024.sched.com/event/1ehIY/physical-and-digital-worlds-come-together-in-gxf-grid-exchange-fabric-maarten-mulder-jelle-hoffman-alliander)
	- Date: 2024-09-05
	- Type: Presentation

## Additional Notes

GXF was formerly known as "Open Smart Grid Platform" (OSGP). The names are used interchangeably through code and marketing material. The GitHub organization remains `OSGP` and the primary repository is `open-smart-grid-platform`.

GXF is undergoing a significant architectural evolution. The original platform (GXF 1.0) uses a layered Java architecture with SOAP APIs and ActiveMQ messaging. Newer use cases are being built on a GXF 2.0 architecture that uses Kotlin, Kafka (event-driven), REST APIs, and Gradle. As of the September 2024 presentation, some GXF 2.0 use cases (FlexOVL frontend, low-voltage measurements) remain closed-source, with plans to open-source connected applications over time.

GXF is predominantly an Alliander project — all governance council members and named maintainers are Alliander-affiliated, and no other adopting organizations are publicly documented. This is notable context for assessing community breadth and reusability, though the platform's protocol-neutral design and multi-tenant architecture suggest it was built with broader applicability in mind. The Dutch smart metering regulatory framework (a government mandate for smart meter rollout) has been a key driver of GXF's development and scale.