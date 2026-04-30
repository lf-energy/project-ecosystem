# Shapeshifter

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

- LF Energy webpage: https://lfenergy.org/projects/shapeshifter/
- Website:
- Code: https://github.com/shapeshifter
- Documentation: https://shapeshifter.github.io/shapeshifter-specification/development/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/shapeshifter?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/shapeshifter-discussion
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/uftp
- Other:

## Description

Communication protocol and reference implementations for flexibility trading between grid operators and aggregators, covering the full lifecycle from forecasting through offering, ordering, and settlement.

## Overview

Shapeshifter defines the USEF Flex Trading Protocol (UFTP), a standardized communication protocol that enables Distribution System Operators (DSOs) and Transmission System Operators (TSOs) to trade demand-side flexibility with Aggregators. The protocol specifies the XML message formats, signing mechanisms, and interaction sequences needed for two parties to negotiate, activate, and settle flexibility — the ability of grid-connected loads and generation to adjust their consumption or production on request. The project delivers the protocol specification with XSD schemas, plus reference implementations in Java (Spring Boot) and Python.

As distribution grids approach their physical capacity limits due to electrification, distributed generation, and increasing simultaneity of demand, grid operators face a choice: build more infrastructure, or make better use of existing capacity. Flexibility trading offers the latter — a DSO identifies an upcoming congestion point, requests load reduction or increase from an aggregator who controls flexible assets (industrial processes, EV chargers, heat pumps, battery storage), and pays for the delivered flexibility. Shapeshifter standardizes this exchange so that any DSO can trade with any aggregator using a common protocol, avoiding bilateral custom integrations. The protocol supports both bilateral trading (direct DSO-to-aggregator) and exchange-mediated trading through coordination platforms.

Shapeshifter is deployed in production by Dutch DSOs (Alliander/Liander, Enexis, Stedin) for congestion management, operating as the underlying protocol for the GOPACS (Grid Operators Platform for Congestion Solutions) platform. The protocol has also been implemented in the UK by SP Energy Networks in a demonstration project for local congestion management (Project Fusion). Contributors include Dutch DSOs, EDSN (the Dutch energy data services organization), and independent developers.

## Technical Profile

### What It Does

Defines a standardized protocol for grid operators and aggregators to exchange flexibility requests, offers, orders, and settlement data, with reference libraries that handle message construction, cryptographic signing, validation, and transport.

### Problem(s) Solved

Enables grid operators to procure demand-side flexibility from aggregators using a standard protocol, eliminating the need for custom point-to-point integrations between each DSO and each aggregator. Without a common protocol, each trading pair would need to negotiate its own message formats, security mechanisms, and settlement procedures — a barrier that limits market participation and prevents efficient flexibility markets from forming.

### Key Capabilities

- Full flexibility trading lifecycle: contract establishment, day-ahead prognosis, flex request/offer/order exchange, and financial settlement with penalty calculations
- Cryptographic message signing using NaCl (Ed25519) for authentication and tamper prevention
- XSD schema validation of all messages, ensuring protocol conformance
- Asynchronous message exchange over HTTP/TLS, with conversation-based correlation
- Support for multiple offer options per flex request, mutual exclusivity between offers, partial activation, and unsolicited offers
- Common Reference Operator (CRO) registry for managing which connections belong to which congestion points and which aggregator serves which prosumer
- Service discovery via DNS (TXT records for public keys, CNAME for endpoints) or centralized directory
- Java reference library (Spring Boot integration, Maven artifacts) and Python reference library (pip-installable)

### Relevant Standards

- USEF (Universal Smart Energy Framework) — UFTP is a subset of the USEF framework, specifically the market-based coordination mechanism for flexibility trading

## Grid Context

### Grid Segment

Transmission, Distribution

### Function

Flexibility & Markets

### Industry Solution Categories

#### Solution Type

- Flexibility Trading Protocol: Standardizes the communication between grid operators and aggregators for procuring, activating, and settling demand-side flexibility.

#### Component of

- DERMS: Provides the market-facing communication layer that a Distributed Energy Resource Management System uses to coordinate flexibility from aggregated DER portfolios.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **OpenSTEF**: Complementary — within Alliander's congestion management pipeline, OpenSTEF forecasts load to identify where congestion will occur, enabling DSOs to issue targeted flex requests via Shapeshifter.
- **Power Grid Model**: Complementary — within Alliander's Grid-as-a-Service architecture, Power Grid Model performs power flow calculations to identify congestion, and Shapeshifter coordinates the flexibility market response to resolve it.
- **OpenLEADR**: Adjacent protocol, different model — OpenLEADR implements OpenADR, a demand response signaling protocol where a utility sends price or event signals and devices respond. Shapeshifter is a flexibility *trading* protocol with bilateral negotiation, bidding, and financial settlement. OpenADR is command-and-control oriented (signal → response); Shapeshifter is market oriented (request → offer → order → settle). They can be complementary: an aggregator could receive a flex order via Shapeshifter and dispatch its devices via OpenADR.
- **FlexMeasures**: Potentially complementary — FlexMeasures optimizes scheduling of flexible energy assets (batteries, EV chargers, heat pumps, industrial processes). An aggregator could use FlexMeasures to compute optimal dispatch schedules in response to flex requests received via Shapeshifter.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

Production

### Supporting / Adopting Organizations

- Alliander (contributor; production user)
- Enexis (contributor; production user)
- Stedin (production user)
- EDSN (contributor — Dutch energy data services organization)
- SP Energy Networks (implemented in UK demonstration project)

## Learn More

- [Unleash the Power of Flexibility with Shapeshifter: A Universal Flex Trading Protocol](https://archive.fosdem.org/2024/schedule/event/fosdem-2024-2208-unleash-the-power-of-flexibility-with-shapeshifter-a-universal-flex-trading-protocol/)
	- Date: 2024-02-03
	- Type: Presentation

## Additional Notes

Shapeshifter originated from the USEF Foundation, a Dutch industry consortium founded in 2014 by ABB, Alliander, DNV, Essent, ICT Group, IBM, and Stedin to develop a common framework for smart energy systems. The USEF Flex Trading Protocol (UFTP) was extracted as the interoperability layer for flexibility trading and donated to LF Energy in 2021. The broader USEF framework covers additional energy market roles and interactions; Shapeshifter focuses specifically on the AGR-DSO (and AGR-TSO) trading subset.

The protocol is technology-neutral at its core — it defines XML message schemas and signing conventions, not a specific software stack. The Java and Python reference libraries handle boilerplate (XML marshalling, cryptographic signing, schema validation, HTTP transport) but leave business logic, persistence, and integration to the implementer. This design allows organizations to embed UFTP into their existing systems architecture rather than adopting a standalone platform.

The Netherlands is the primary adoption context, where grid congestion has become acute — most of the country faces constraints on both consumption and generation connections. Dutch regulators require market-based congestion management, creating a structural demand for standardized flexibility trading. GOPACS, the national congestion management platform operated jointly by the Dutch grid operators, uses Shapeshifter as its trading protocol. While the protocol is geography-neutral, its current adoption is concentrated in the Netherlands and to a lesser extent the UK.
