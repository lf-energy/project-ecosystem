# GEISA

**Last Updated:** 2026-04-20

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

- LF Energy webpage: https://lfenergy.org/projects/geisa/
- Website: https://geisa.lfenergy.org/
- Code: https://github.com/geisa
- Documentation: https://lf-energy.atlassian.net/wiki/spaces/GEISA/overview?homepageId=64946717
- Calendar: https://lf-energy.atlassian.net/wiki/spaces/GEISA/pages/66617382/Onboarding+New+Members#Meetings
- LinkedIn: https://www.linkedin.com/showcase/geisa-project
- Community:
	- Mailing List: https://lists.lfenergy.org/g/geisa-discussion
	- Slack: https://lfenergy.slack.com/archives/C07PULLH00P
- LFX Insights: https://insights.linuxfoundation.org/project/geisa
- Other:

## Description

Interoperability specification for running third-party applications on grid edge devices such as smart meters and distribution automation controllers.

## Overview

GEISA (Grid Edge Interoperability and Security Alliance) defines an open specification for grid edge computing environments. It standardizes how applications are deployed, managed, and executed on embedded devices at the grid edge — primarily smart meters, but also capacitor bank controllers, load tap changers, and other distribution automation devices. The specification covers four pillars: a standardized Application Programming Interface (API) for uniform access to device capabilities, an Application & Device Management (ADM) protocol for remote fleet management, and two execution environments — a Linux Execution Environment (LEE) for devices running Linux and a Virtual Execution Environment (VEE) for devices using virtual machines. Standard metering and billing functions are explicitly out of scope, as are standard SCADA operations for distribution automation; GEISA focuses on advanced capabilities beyond basic device functions.

The core problem GEISA addresses is vendor lock-in at the grid edge. Today, each device vendor ships its own proprietary application platform, APIs, and management interfaces. An application written for one vendor's meters or devices cannot run on another vendor's hardware, and a utility managing a multi-vendor fleet needs separate management systems for each manufacturer. As the role of the meter evolves — from periodic interval readings to one-second and waveform data capture, from a single-purpose measurement device to a multi-application computing platform serving as communications hub, consumer enabler, and grid sensor — this lack of interoperability becomes a bottleneck. GEISA enables utilities to deploy applications from any vendor onto devices from any vendor using a common management platform, decoupling application innovation from hardware procurement.

GEISA follows a "selection over invention" philosophy: rather than creating new technologies, it specifies the minimum set of choices needed for interoperability across the many options that already exist in the Linux and embedded computing ecosystems (C libraries, init systems, file system layouts, application management). Implementers are free to go beyond the specification. The project is utility-driven, with requirements defined by participating utilities and technical implementation developed collaboratively with device vendors and application providers.

## Technical Profile

### What It Does

Defines the interfaces and environment specifications that allow third-party applications to run portably across grid edge devices from different manufacturers, and allows those devices to be managed from a single platform regardless of vendor.

### Problem(s) Solved

Eliminates vendor lock-in for grid edge computing by enabling utilities to deploy and manage applications across multi-vendor device fleets (meters, DA controllers) through standardized interfaces, rather than being tied to each vendor's proprietary application platform and management system.

### Key Capabilities

- Standardized API providing uniform access to device capabilities (meter data, waveform readings, sensor inputs, actuator controls) via a message bus architecture
- Remote application and device management (ADM) protocol for deploying, updating, and managing applications across multi-vendor device fleets from a central management system
- Linux Execution Environment (LEE) specification for container-based application isolation on devices running embedded Linux
- Virtual Execution Environment (VEE) specification for application portability on more resource-constrained devices using virtual machines
- Manifest-based security model where applications declare required permissions, enforced by the runtime
- Conformance test framework for validating implementations against the specification

### Relevant Standards

GEISA is a specification that defines interoperability interfaces for grid edge computing environments. It does not implement existing grid communication or data model standards; however, it does specify the use of some industry-standard protocols. MQTT (https://mqtt.org), LwM2M (https://www.openmobilealliance.org/specifications/lwm2m), and CoAP (https://www.rfc-editor.org/rfc/rfc7252) are all required to develop a GEISA-conformant solution. Beyond this, applications running on GEISA-conformant platforms may implement standards such as OCPP, Matter, Modbus, IEEE 2030.5, or IEC 62056 (DLMS/COSEM), but the GEISA specification defines the platform layer beneath those applications.

## Grid Context

### Grid Segment

Distribution

### Function

Flexibility & Markets

### Industry Solution Categories

#### Solution Type

- Edge Application Platform: Defines the interoperability specification for running third-party applications on grid edge devices, enabling multi-vendor application deployment and fleet management.

#### Component of

- AMI: Provides the application platform specification for next-generation AMI, enabling utilities to deploy advanced analytics, DER orchestration, and grid monitoring applications on smart meters independent of the meter vendor.
- Distribution Automation: Provides the application platform specification for intelligent DA, enabling utilities to deploy advanced analytics, grid monitoring, and control applications on DA controllers independent of the device vendor.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Specification

## Related Projects

- **GXF**: Complementary — GXF manages grid edge devices from a central platform (protocol translation, device lifecycle, command scheduling), while GEISA defines the on-device application runtime environment. A GEISA-conformant device could potentially be managed through a GXF protocol adapter.
- **SEAPATH**: Both address edge computing for grid infrastructure, but for different deployment profiles. SEAPATH targets substation servers running clustered VMs for protection and control applications, while GEISA targets lower-power, higher-quantity distributed devices (meters, DA controllers) running lightweight applications.

## Maturity & Adoption

### LF Energy Stage

Sandbox

<!-- Check LF Energy project page or TAC records for official stage. -->

### Deployment Maturity

R&D

<!--
- R&D: Pre-production; not yet deployed in any utility production environment
- Piloting: Deployed in production by utilities, but limited in scale or scope (e.g., single region, specific use case, trial basis)
- Production: One or more utilities running in production to plan or operate the grid
-->

### Supporting / Adopting Organizations

#### Utilities

- Southern California Edison
- National Grid
- Duquesne Light
- Portland General Electric

#### Vendors

- Aetheros
- EDMI
- Honeywell
- Itron
- Kalkitech
- Landis+Gyr
- Sagemcom
- Savoir-faire Linux
- Span
- Sense
- Utilidata

## Learn More

- [Introduction to GEISA](https://lfenergysummiteu2025.sched.com/event/26Iyf/introduction-to-geisa-michael-stuber-southern-california-edison)
	- Date: 2025-09-10
	- Type: Presentation
- Achieving Interoperability at the Grid Edge
	- Date: 2026-02-05
	- Type: Presentation

## Additional Notes

GEISA is a specification project, not a software product. The primary deliverable is the GEISA Specification document (v0.1.8 as of January 2026), with reference implementations and a conformance test framework supporting validation. The specification is the authoritative artifact; the code repositories serve as reference and testing tools.

The project's governance separates utility-driven requirements from vendor-led technical implementation. This structure reflects the nature of the problem: utilities define what interoperability means for their procurement and operational needs, while device vendors and application developers determine how to achieve it. Southern California Edison initiated the project and remains the primary utility driver.

There is no established open standard for grid edge computing interoperability today. Each meter and DA device vendor provides its own proprietary application environment, APIs, and management interfaces. GEISA aims to fill this gap in the same way that OCPP standardized charger-to-back-office communication for EV charging — by defining the minimum interoperability interfaces that allow the ecosystem to decouple application innovation from hardware procurement. The "selection over invention" approach (choosing from existing Linux/embedded technologies rather than creating new ones) is a deliberate design philosophy to minimize the specification's footprint and maximize implementer flexibility.
