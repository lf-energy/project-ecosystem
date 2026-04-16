# Semantic Energy Framework

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

- LF Energy webpage: https://lfenergy.org/projects/semantic-energy-framework-sef/
- Website:
- Code: https://github.com/lfe-sef
- Documentation:
- Calendar:
- LinkedIn:
- Community:
	- Mailing List:
	- Slack: https://lfenergy.slack.com/archives/C07490HA2R1
- LFX Insights: https://insights.linuxfoundation.org/project/lfe-sef
- Other:

## Description

Semantic interoperability middleware that enables data exchange between heterogeneous energy platforms using ontology-based knowledge graphs, without requiring systems to agree on a single data model.

## Overview

The Semantic Energy Framework (SEF) provides middleware for connecting digital platforms that use different data models — such as a home energy management system, an EV charger, a building management system, and a DSO flexibility platform — without requiring each pair of systems to negotiate a shared data format. Each platform connects to SEF through an adapter that maps its native data model to a shared ontology (by default ETSI SAREF, though the framework is ontology-agnostic). The Knowledge Engine at the core handles discovery, translation, and routing: when one platform publishes or requests data, the engine matches it to other participants that can provide or consume that data based on the ontology, rather than through point-to-point API integration.

The interoperability problem SEF addresses is common at the customer-grid boundary, where DSOs need to coordinate with many types of customer-premises equipment and third-party platforms. Traditional approaches require either a centralized integration platform (creating vendor dependence) or bilateral data agreements between every pair of systems (creating an N-to-N mapping problem that doesn't scale). SEF's decentralized, ontology-based approach converts this to N-to-one: each system only needs one adapter to participate in the interoperable ecosystem.

SEF was developed and validated within the EU Horizon 2020 InterConnect project (2019–2024), a 50-partner consortium that ran seven large-scale pilots across Europe (Greece, France, Italy, Germany, the Netherlands, Belgium, Portugal). Pilot use cases included demand-side flexibility coordination, smart appliance scheduling, dynamic tariff optimization, and DSO-aggregator communication. The framework was tested with appliances from manufacturers including Whirlpool, Miele, BSH, Daikin, and Elli (EV charging), and with grid operator E-REDES (Portuguese DSO) in the Portuguese pilot. Following the completion of the InterConnect project, the three lead organizations — INESC TEC, TNO, and Vizlore Labs Foundation — proposed the project for inclusion in LF Energy in 2024.

## Technical Profile

### What It Does

Provides a decentralized semantic interoperability layer that connects heterogeneous digital platforms through ontology-based adapters and a knowledge engine that handles data discovery, translation, and routing using RDF knowledge graphs.

### Problem(s) Solved

Reduces the integration burden when a DSO or aggregator needs to exchange data with multiple customer-premises platforms (HEMS, BEMS, EV chargers, smart appliances) that each use proprietary data models. Replaces point-to-point bilateral integration with a shared semantic layer where each platform connects once through an adapter.

### Key Capabilities

- Decentralized architecture: no centralized broker or facilitating platform required — interoperability is established peer-to-peer between participants
- Ontology-agnostic Knowledge Engine: works with any ontology expressed in RDF/OWL, with ETSI SAREF as the default for energy applications
- Four knowledge interaction patterns: ASK/ANSWER for queries, POST/REACT for data dissemination — enabling both request-response and publish-subscribe styles
- Generic Adapter: REST API gateway that handles authentication, authorization, and communication between service-specific adapters and the Knowledge Engine
- Service Store: registry for discovering and certifying interoperable services within an ecosystem (described in project architecture; not yet migrated to LF Energy repositories)
- Graph pattern matching: the Knowledge Engine automatically matches data providers with data consumers based on overlapping ontology patterns, without manual configuration of data flows

### Relevant Standards

- ETSI SAREF (Smart Applications REFerence ontology) — the default ontology used for semantic data representation in energy applications; the framework is ontology-agnostic but SAREF is the primary validated ontology

<!-- SAREF is an ETSI standard (TS 103 264). SEF uses SAREF as its default ontology and the InterConnect project developed SAREF extensions for energy domain concepts. The framework works with any RDF/OWL ontology but SAREF is the only one validated in pilots. W3C RDF/OWL are foundational web standards used internally but are not energy industry standards per the template criteria. -->

## Grid Context

### Grid Segment

Behind the Meter (primary), Distribution (secondary)

### Function

Interoperability & Data

### Industry Solution Categories

#### Solution Type

- Semantic Interoperability Middleware: Provides an ontology-based integration layer that enables data exchange between heterogeneous digital platforms at the customer-grid boundary without requiring bilateral data model agreements.

#### Component of

None. SEF is a horizontal interoperability layer, not a component of a specific utility solution category. While it was demonstrated in demand-side flexibility and smart building scenarios, it does not serve as a recognized building block of any specific system (e.g., DERMS, HEMS) that a utility engineer would search for by category.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

None currently. While SEF's TAC proposal described potential for use as an interoperability layer between LF Energy projects, no direct technical integrations or shared data flows with other LF Energy projects have been established.

<!-- The TAC proposal suggested SEF could provide semantic interoperability between other LF Energy projects, but this remains aspirational. EVerest, Shapeshifter, and openLEADR all operate at the customer-grid boundary but use their own protocol-specific approaches (OCPP, USEF, OpenADR) rather than ontology-based semantic interoperability. "Both operate at the grid edge" is not a sufficient relationship per CLAUDE.md. -->

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- INESC TEC (co-developer; lead on Generic Adapter and pilot integration)
- TNO (co-developer; lead on Knowledge Engine)
- Vizlore Labs Foundation (co-developer; lead on Service Store and P2P marketplace enablers)

<!-- InterConnect pilot participants included E-REDES, Schneider Electric, Fraunhofer, and appliance manufacturers (Whirlpool, Miele, BSH, Daikin), but these were grant-funded pilot participants, not ongoing adopters of the LF Energy project. Listing them as adopters would overstate the current situation. -->

## Learn More

- [Collaborative Analytics and Semantic Interoperability for the Energy Sector](https://lfenergysummiteu2025.sched.com/event/26WnS/sponsored-session-collaborative-analytics-and-semantic-interoperability-for-the-energy-sector-jose-ricardo-andrade-fabio-coelho-inesc-tec)
	- Date: 2025-09-11
	- Type: Presentation
- [TAC proposal](https://github.com/lf-energy/tac/issues/132)
	- Date: 2024-03-29
	- Type: TAC proposal

## Additional Notes

SEF originated from the EU Horizon 2020 InterConnect project (grant agreement 857237, October 2019 – March 2024). The TAC proposal was filed as the grant project was concluding (March 2024), and the code was migrated from INESC TEC's GitLab to the LF Energy GitHub organization (`lfe-sef`) in late 2025. The LF Energy repositories (`knowledge-engine` at v1.2.5, `generic-adapter`) are snapshots from the InterConnect project and have not received commits since their initial import. The Service Store and P2P marketplace components described in the TAC proposal are not present in the LF Energy repositories.

All three contributing organizations are research institutes. The project self-assessed at Technology Readiness Level 6 (system demonstrated in a relevant environment) at the time of the TAC proposal. The TAC proposal explicitly identified "refactoring the code base towards production ready state" and "securing community contributions" as maturity goals within LF Energy. As of early 2026, the project remains in Sandbox stage with no visible community development activity in the LF Energy repositories.