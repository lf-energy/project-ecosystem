# OperatorFabric

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

- LF Energy webpage: https://lfenergy.org/projects/operatorfabric/
- Website: https://opfab.github.io/
- Code: https://github.com/opfab
- Documentation: https://opfab.github.io/documentation/current/getting_started/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/operator-fabric?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/opfab
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/operator-fabric
- Other:
	- Releases: https://github.com/opfab/operatorfabric-core/releases
	- Roadmap: https://opfab.github.io/pages/roadmap.html

## Description

Notification and coordination platform for utility control room operators.

## Overview

OperatorFabric is a platform that centralizes operational event notifications and enables structured communication between control centers. It aggregates real-time alerts and events from multiple business applications — SCADA, EMS, network analysis tools, maintenance systems — into a single operator interface, replacing the need to monitor numerous screens and software simultaneously. Events are delivered as "cards": structured notifications that operators can filter by severity, process, and date, and act on directly within the platform.

Beyond notification aggregation, OperatorFabric provides a formal coordination workflow between control centers. Operators can exchange structured question-and-response messages with configurable deadlines, replacing ad-hoc phone calls and emails with traceable, auditable digital processes. This is particularly valuable for coordination between TSOs and DSOs, or between neighboring TSOs, where multiple organizations need to align on operational decisions under time pressure.

OperatorFabric was created by RTE (the French TSO) and contributed to LF Energy in 2018. RTE uses it in production across its 8 control centers for crisis management and inter-center coordination. Alliander (Dutch DSO) contributes to the project, particularly on geographic map features for incident visualization. The platform is deployed via Docker containers and integrates with existing operational systems through REST APIs and Kafka.

![OperatorFabric UI](images/opfab.avif)
*OperatorFabric UI*

## Technical Profile

### What It Does

Centralizes operational event notifications from upstream systems into a unified operator interface and provides structured, time-bounded coordination workflows between control centers.

### Problem(s) Solved

Control room operators monitor multiple applications simultaneously, each with its own alerts and notification system. Cross-center coordination happens through unstructured channels (phone, email) with no traceability or enforced deadlines. OperatorFabric consolidates notifications into a single feed and replaces ad-hoc communication with formal, auditable workflows — reducing cognitive overload and improving coordination reliability.

### Key Capabilities

- **Card-based notification feed**: Events from any upstream system delivered as structured "cards" with four severity levels (alarm, action, compliant, information), filterable by process, date, and severity
- **Structured coordination workflows**: Question-and-response exchanges between control centers with configurable deadlines ("last time to decide") and response tracking across entities
- **Customizable card templates**: HTML/Handlebars-based templates allow each business process to define its own card layout and interaction logic without modifying platform code
- **Timeline and calendar views**: Temporal visualization of events for operational planning and shift awareness
- **Geographic map display**: Cards can carry geographic coordinates for map-based incident visualization (supports WMTS layers and ArcGIS)
- **Real-time operator supervision**: Monitoring of which operators and organizational entities are connected, with card acknowledgment tracking
- **Email notification integration**: Optional email diffusion of card notifications with customizable templates
- **External device alarming**: Physical alarm signals via Modbus protocol for critical notifications
- **Card reminders and task tracking**: Configurable reminders with recurrence rules to support shift handovers and ongoing operational tasks
- **Archive and audit**: Historical card search and operator action logging

### Relevant Standards

None. OperatorFabric is standards-agnostic — it is a general-purpose notification and coordination platform that carries arbitrary business data. Standards compliance resides in the upstream systems that publish cards to OperatorFabric.

## Grid Context

### Grid Segment

Transmission (primary), Distribution (secondary)

### Function

Grid Operations

### Industry Solution Categories

#### Solution Type

- Operator Notification & Coordination Platform: Centralizes operational event notifications and provides structured inter-center coordination workflows. This is not a widely standardized product category — OperatorFabric occupies a relatively novel space, sitting alongside (not inside) traditional control center systems like EMS, SCADA, and DMS.

#### Component of

- Control Room Systems: Serves as a complementary notification and coordination layer within a control center technology stack, integrating with EMS, SCADA, DMS, and other operational applications via REST API and Kafka.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

None at this time.

## Maturity & Adoption

### LF Energy Stage

Early Adoption

### Deployment Maturity

Production

### Supporting / Adopting Organizations

- RTE (production user, primary developer)
- Alliander (contributor — geographic map visualization features)

## Learn More

- [FOSDEM Energy Devroom: Control Room Management with OperatorFabric](https://lfenergy.org/fosdem-energy-devroom-control-room-management-with-operatorfabric/)
	- Date: 2025-02-01
	- Type: Presentation
- [TSO-DSO Coordination using OperatorFabric](https://lfenergysummiteu2025.sched.com/event/26Izv/tso-dso-coordination-using-operatorfabric-sascha-eschmann-rte-international)
	- Date: 2025-09-11
	- Type: Presentation
- [OperatorFabric: Field-Tested Platform For Utility Systems Operators](https://tfir.io/operatorfabric-field-tested-platform-for-utility-systems-operators/)
	- Date: 2023-10-11
	- Type: Interview
- [LF Energy OperatorFabric Project Completes Security Audit and Threat Model](https://lfenergy.org/lf-energy-operatorfabric-project-completes-security-audit-and-threat-model/)
	- Date: 2024-08-22
	- Type: Announcement

## Additional Notes

OperatorFabric is one of the few LF Energy projects with confirmed production deployment at a major TSO. RTE's use across 8 control centers for crisis management and operational coordination represents meaningful operational validation.

The project has a small contributor base (primarily RTE developers), which is both a strength (deep domain expertise from actual control center operators) and a risk (limited community breadth). The MPL v2 license is commercial-friendly, allowing proprietary extensions while requiring modifications to OperatorFabric itself to remain open.

A common misconception is that OperatorFabric is a SCADA or EMS replacement. It is not — it is a notification and coordination layer that sits above and alongside these systems, aggregating their outputs for operator consumption and enabling structured communication that these systems do not provide natively.