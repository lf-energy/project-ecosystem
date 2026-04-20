# EVerest

**Last Updated:** 2026-03-17

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

- LF Energy webpage: https://lfenergy.org/projects/everest/
- Website:
- Code: https://github.com/EVerest
- Documentation: https://everest.github.io/nightly/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/everest?view=month
- LinkedIn: https://www.linkedin.com/showcase/everest-project
- Community:
	- Mailing List: https://lists.lfenergy.org/g/everest
	- Zulip: https://lfenergy.zulipchat.com/
- LFX Insights: https://insights.linuxfoundation.org/project/everest
- Other:
	- Roadmap: https://github.com/EVerest/everest/blob/main/tsc/ROADMAP.md

## Description

Complete firmware stack for standards-compliant, interoperable, and secure EV chargers.

## Overview

EVerest is a complete software stack that runs on EV charging station hardware, handling everything from low-level hardware control to cloud communication. It implements the protocols a charging station needs to communicate with vehicles (ISO 15118, IEC 61851), with back-office management systems (OCPP), and with energy management systems. EVerest's modular architecture allows it to be configured for any charging use case — an unmanaged single-port AC wallbox, a managed workplace charger with authentication and smart charging, or a multi-port public DC fast charging station with integrated payment, metering, and power distribution.

The core problem EVerest solves is interoperability. EV charging involves a combinatorial explosion of standards, vehicle models, charging apps, and back-office systems that must all work together. Industry data shows 10–25% of charging sessions fail, primarily due to connectivity and software errors. Each charging station OEM implementing these standards independently produces different interpretations and bugs, compounding the problem as the ecosystem grows. EVerest addresses this by providing a single, shared implementation of charging protocols that the entire industry can test against, fix, and improve. This is the same approach that made Linux successful: commoditize the shared infrastructure so that companies compete on their unique value rather than duplicating commodity plumbing.

EVerest is deployed as embedded firmware on charging station controllers. Charger OEMs integrate EVerest into their products, typically on ARM-based Linux boards (e.g., PHYTEC phyVERSO, NXP i.MX-based controllers). Charge point operators (CPOs) benefit from cross-vendor consistency and reduced stranded-asset risk when chargers run on open, maintainable software. For utilities, EVerest's energy management capabilities and growing support for grid integration protocols make EV chargers controllable grid-edge assets rather than unmanaged loads — enabling smart charging, demand response, and emerging vehicle-to-grid (V2G) use cases. Grid protocol support (OpenADR, EEBus) is under active development, with integration modules on feature branches.

![Simplified EVerest context](images/everest_simplified_context.avif)
*Simplified EVerest context*

![Simplified EVerest architecture](images/everest_simplified_achitecture.avif)
*Simplified EVerest architecture*

## Technical Profile

### What It Does

Provides the full software stack for EV charging stations: vehicle communication, back-office integration, authentication, energy management, and hardware abstraction — running on embedded Linux controllers inside the charger.

### Problem(s) Solved

**For charger OEMs and CPOs:** Eliminates the need to independently implement dozens of charging standards, reducing development cost and time-to-market while improving interoperability across the fragmented EV charging ecosystem.

**For utilities and DSOs:** Provides a standardized, controllable interface to EV chargers as grid-edge assets, enabling smart charging, demand response, and V2G to manage the grid impact of growing EV loads.

### Key Capabilities

- **AC and DC charging support**: Configurable for any charging use case from simple home wallboxes to complex multi-port public DC fast chargers with centralized power architecture
- **Vehicle communication**: ISO 15118-2, ISO 15118-3, ISO 15118-20, and DIN 70121 for vehicle-to-charger communication, including Plug & Charge with full PKI support
- **Back-office integration**: OCPP 1.6 and OCPP 2.0.1 (production-ready, OCA-certified) for charger-to-cloud management system communication; OCPP 2.1 under active development
- **Energy management**: Hierarchical energy tree that distributes available power across multiple charging ports, with automatic phase switching optimization (1-phase/3-phase) and support for external limits from OCPP or energy management systems
- **Grid integration protocols**: OpenADR 3.0 (via OpenLEADR, draft PR) and EEBus (on feature branch) for demand response and energy management; Modbus/SunSpec for direct metering and control (shipped)
- **Authentication**: RFID/NFC readers, ISO 15118 Plug & Charge certificate-based authentication, and OCPP-based authorization
- **Payment terminal integration**: ZVT protocol support for credit card payment terminals
- **Metering and calibration law compliance**: Support for Eichrecht-compliant DC power meters (LEM DCBM, DZG GSH01) for legally accurate billing
- **Hardware abstraction**: Pre-built drivers for DC power supplies (Huawei, InfyPower, UUGreenPower), power meters, isolation monitors, PLC modems, and NFC readers
- **Modular architecture**: ~90+ modules communicating via MQTT, each configurable independently; language bindings for C++, Rust, Python, and JavaScript
- **Software-in-the-loop simulation**: Full charging simulation without hardware for development, testing, and research
- **Bidirectional charging (emerging)**: V2G and V2H support through bidirectional power supply drivers; full protocol support depends on ISO 15118-20 and OCPP 2.1, both under active development

### Relevant Standards

- **ISO 15118** (Parts -2, -3, -20): Vehicle-to-grid communication for EV charging, including Plug & Charge
- **IEC 61851**: Electric vehicle conductive charging system — physical signaling and safety
- **DIN SPEC 70121**: DC charging communication (predecessor to ISO 15118 for DC)
- **OCPP 1.6 / 2.0.1** (IEC 63584): Open Charge Point Protocol for charger-to-back-office communication (OCPP 2.1 in development)

## Grid Context

### Grid Segment

Behind the Meter (primary), Distribution (secondary)

### Function

Flexibility & Markets — EV Charging

### Industry Solution Categories

#### Solution Type

- EV Charging Station Firmware: Provides the complete software stack that runs inside EV charging hardware, managing all aspects of a charging session from vehicle communication to energy delivery.

#### Component of

- EV Charging Infrastructure: Serves as the embedded intelligence layer in charging stations deployed by CPOs and fleet operators, enabling standards-compliant public and private charging networks.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **CitrineOS**: Complementary vertical integration. CitrineOS is an open source charging station management system (CSMS) — the cloud-side software that manages a network of chargers. EVerest is the charger-side firmware. They connect via OCPP: chargers running EVerest communicate with a CitrineOS backend for remote management, session tracking, and configuration.
- **OpenLEADR**: OpenLEADR provides an OpenADR 3.0 implementation in Rust (openleadr-rs). An experimental EVerest module (RsOpenADR3) uses OpenLEADR to receive demand response signals from a Virtual Top Node and translate them into EVerest energy limits, enabling grid operators to manage EV charging load via OpenADR. Not yet merged to the main branch.

## Maturity & Adoption

### LF Energy Stage

Early Adoption

### Deployment Maturity

Production

### Supporting / Adopting Companies

**Charger OEMs with known EVerest-based products:**
- Mahle (chargeBIG)
- Qwello (CP21, CP22)
- Pod Point (Solo 3s)
- Enteligent (TLCEV)
- Voltpost

**Component suppliers with EVerest-compatible hardware:**
- chargebyte
- PHYTEC
- Texas Instruments
- Seeed Studio
- Advantech
- NXP
- Analog Devices
- Renesas
- FEIG

**Other contributing/supporting organizations:**
- Pionix (project initiator, primary contributor)
- U.S. Joint Office of Energy and Transportation (dedicated resources, TSC member)
- Hubject
- Fraunhofer ISE
- RWTH Aachen

## Learn More

- [From Ambition to Reality: How We Built the Global Open Source Community Around EVerest](https://lfenergysummiteu2025.sched.com/event/27TaN/keynote-from-ambition-to-reality-how-we-built-the-global-open-source-community-around-everest-marco-moller-co-founder-and-ceo-pionix-gmbh)
	- Date: 2025-09-11
	- Type: Presentation
- [Emerging Energy Management Use Cases for Car Charging](https://lfenergysummiteu2025.sched.com/event/26IzI/emerging-energy-management-use-cases-for-car-charging-hauke-feiertag-simon-seres-chargebyte-gmbh)
	- Date: 2025-09-11
	- Type: Presentation
- [EVerest: Current Status and How It Can Help Stabilize the Grid](https://lfenergysummit2024.sched.com/event/1ehHV/everest-current-status-and-how-it-can-help-stabilize-the-grid-robert-de-leeuw-pionix-gmbh)
	- Date: 2024-09-05
	- Type: Presentation
- [Park&Charge and Qwello Revitalize EV Chargers with LF Energy EVerest](https://lfenergy.org/parkcharge-and-qwello-revitalize-ev-chargers-with-lf-energy-everest/)
	- Date: 2025-01-25
	- Type: Case Study
- [Seeed Studio Develops Open Source EV Charging Product Thanks to Zephyr RTOS and LF Energy EVerest](https://lfenergy.org/seeed-studio-develops-open-source-ev-charging-product-thanks-to-zephyr-rtos-and-lf-energy-everest/)
	- Date: 2024-05-13
	- Type: Case Study
- [Real World Interoperability in EV Charging: The Tooling Stack Behind the EVerest Ecosystem](https://www.youtube.com/watch?v=0cjevmsFhAA)
	- Date: 2026-01-31
	- Type: Presentation

## Additional Notes

EVerest is the largest project in the LF Energy ecosystem by contributor count and development activity. As of September 2025, the project reported over 70 contributing organizations and more than 900 individual contributors. The project has four technical working groups (Car Communication, Cloud Communication, Energy Management, and Megawatt Charging System (MCS)).

The EV charging firmware market has historically been entirely proprietary, with each OEM building and maintaining its own full stack. EVerest is, to our knowledge, the only open source project offering a production-grade, full-stack alternative. This positions it similarly to how Android commoditized mobile device operating systems or how Linux commoditized server infrastructure — providing a shared foundation that enables competition on differentiation rather than duplicated commodity code. The Apache 2.0 license was chosen specifically to enable commercial adoption without requiring companies to publish proprietary extensions.

From a utility perspective, the grid relevance of EVerest increases as EV penetration grows. Unmanaged EV charging concentrates new load at evening peaks, potentially requiring costly grid reinforcement. EVerest's on-device energy management already enables smart charging (local power distribution, phase switching, external limit enforcement). Grid integration protocols for demand response (OpenADR, EEBus) and bidirectional charging (V2G via ISO 15118-20) are under active development, with integration modules on feature branches. The BiFlex-Industrie R&D project in Germany (funded by the German Federal Ministry for Economic Affairs, ending September 2026) is exploring bidirectional flexibility using company fleets, with chargebyte contributing EVerest-based implementations.

The project launched the EVerest CPO Forum in early 2026, a user group aligning charge point operators and vendors on requirements, interoperability KPIs, and roadmap priorities.

The U.S. Joint Office of Energy and Transportation (a partnership between the U.S. Department of Energy and Department of Transportation) actively supports EVerest, reflecting growing government interest in open standards for EV charging infrastructure.