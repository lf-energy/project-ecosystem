# CoMPAS

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

- LF Energy webpage: https://lfenergy.org/projects/compas/
- Website:
- Code: https://github.com/com-pas/
- Documentation: https://lf-energy.atlassian.net/wiki/spaces/SHP/overview
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/compas?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/CoMPAS
	- Slack: https://lfenergy.slack.com/archives/C01926K9D39
- LFX Insights: https://insights.linuxfoundation.org/project/compas
- Other:

## Description

Vendor-neutral tooling for IEC 61850 substation configuration.

## Overview

CoMPAS (Configuration Modules for Power industry Automation Systems) provides a web-based environment for engineering IEC 61850 substation automation systems. It combines a graphical SCL editor — built on the OpenSCD project — with a set of backend services for file storage, validation, CIM-to-SCL conversion, and automated SCD generation. Together, these components give protection and control engineers a vendor-neutral tool for the full IEC 61850 configuration workflow: from initial system specification through to configured device descriptions ready for deployment.

Today, IEC 61850 system configuration typically requires vendor-specific tools — each IED manufacturer provides their own engineering software. This creates fragmented workflows where engineers must use multiple proprietary tools, each with different interfaces and data handling. CoMPAS provides a single, vendor-neutral environment that can work with SCL files from any manufacturer, enabling utilities to own and control their configuration toolchain independently.

CoMPAS is deployed on-premise as a set of Docker containers. Engineers access the web-based editor through a browser, while backend services handle file persistence, versioning, and processing. The editor uses a plugin architecture, and the community has contributed plugins for guided engineering workflows and template generation that extend the core platform. The system supports all eight IEC 61850-6 SCL file types (SSD, SCD, ICD, IID, CID, SED, ISD, STD) with role-based access control. It is primarily developed by Alliander and BearingPoint, with contributions from RTE and TransnetBW.

![CoMPAS architecture overview](images/CoMPAS-architecture-overview-202320230912.avif)
*CoMPAS architecture overview*

## Technical Profile

### What It Does

Provides a web-based platform for creating, editing, validating, and managing IEC 61850 SCL (Substation Configuration Language) files used to configure substation protection, automation, and control systems.

### Problem(s) Solved

Enables utilities to engineer IEC 61850 substation configurations using a single vendor-neutral tool, eliminating dependence on manufacturer-specific configuration software for managing SCL files across multi-vendor substations.

### Key Capabilities

- **SCL editing**: Web-based graphical editor for IEC 61850 SCL files, with plugins for single-line diagrams, subscriber data binding (GOOSE/SMV), communication configuration, and template management
- **SCL file storage and versioning**: Centralized repository for all SCL file types with semantic versioning tracked through the IEC 61850-6 native History section
- **CIM-to-SCL mapping**: Converts CIM substation models to IEC 61850 SSD files, bridging enterprise grid models with substation configuration
- **SCD generation**: Automated generation of System Configuration Description files from SSD and STD inputs
- **Template generation**: Creation and management of IEC 61850 Logical Node type templates with drag-and-drop assignment of data types (available as a community-contributed plugin)
- **Guided engineering wizard**: Step-by-step workflow engine that sequences plugins into configurable engineering processes, with validation at each step (available as a community-contributed plugin)
- **SCL auto-alignment**: Automated graphical layout for SCL elements that lack coordinate data

### Relevant Standards

- IEC 61850-6 (Substation Configuration Language)
- IEC/TS 62361-102 (CIM-to-IEC 61850 mapping)

## Grid Context

### Grid Segment

Transmission, Distribution

### Function

Grid Operations — Substation Digitalization

### Industry Solution Categories

#### Solution Type

- System Configuration Tool: Provides a vendor-neutral environment for engineering IEC 61850 substation automation configurations (SCL files).

#### Component of

- Digital Substation: Serves as the configuration toolchain for IEC 61850-based digital substation programs, producing the SCL files that define how substation devices are configured and communicate.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **SEAPATH**: Complements CoMPAS in a digital substation architecture. CoMPAS produces the IEC 61850 configuration files (SCL); SEAPATH provides the real-time virtualization platform on which the configured PAC applications run.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- Alliander
- RTE
- BearingPoint
- TransnetBW

## Learn More

- [CoMPAS Essentials: Key to Simplicity](https://lfenergysummiteu2025.sched.com/event/26Izm/compas-essentials-key-to-simplicity-david-monichi-stefan-baumgartner-bearingpoint)
	- Date: 2025-09-11
	- Type: Presentation
- [CoMPAS and Beyond: Simplifying IEC 61850](https://lfenergysummit2024.sched.com/event/1ehIw/compas-and-beyond-simplifying-iec61850-pascal-wilbrink-openvalue-arnhem)
	- Date: 2024-09-06
	- Type: Presentation
- [LF Energy CoMPAS Cleans Up IEC 61850 Data Model](https://lfenergy.org/lf-energy-compas-cleans-up-iec-61850-data-model/)
	- Date: 2023-07-06
	- Type: Case Study

## Additional Notes

CoMPAS is, to our knowledge, the only vendor-neutral, open source IEC 61850 system configuration tool. The proprietary alternatives are vendor-specific: each major IED manufacturer ships their own configuration tool tied to their equipment. This means utilities with multi-vendor substations must maintain expertise across multiple proprietary tools. CoMPAS's vendor-neutral approach addresses this directly.

The project has a closely intertwined relationship with OpenSCD, an independent open source SCL editor. CoMPAS maintains a fork of OpenSCD (compas-open-scd) that extends it with backend service integration for file storage, CIM mapping, and validation. Multiple OpenSCD plugins are developed within the CoMPAS GitHub organization. The two projects share contributors and the codebases are being actively separated to clarify boundaries.