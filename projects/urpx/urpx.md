# Utility Rate Plan Exchange (URPX)

**Last Updated:** 2026-03-18

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
- [Language & Attribution Guidelines](#language--attribution-guidelines)

## Basic Info

- LF Energy webpage: https://lfenergy.org/projects/utility-rate-plan-exchange-urpx/
- Website:
- Code: https://github.com/urpx-org
- Documentation: https://github.com/urpx-org/urpx-website/blob/main/introduction/what-is-urpx.md
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/utility-rate-plan-exchange?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/urpx-wg
	- Slack: https://lfenergy.slack.com/archives/C09NTF8PZTJ
- LFX Insights:
- Other:
	- Working Group Admin Repo: https://github.com/urpx-org/urpx-wg

## Description

A standardized, machine-accessible format and Common Service API specification for representing and exchanging utility rate plan data.

## Overview

URPX (Utility Rate Plan Exchange) is an open semantic standard that provides a comprehensive, standardized method for representing rate plan data from distribution, retail, and other utility service providers — including energy, water, and other utilities — in machine-accessible format. The standard defines a modular ontology — covering rate plan structures, charge classifications, eligibility rules, applicability conditions, geographic territories, and temporal versioning — and a Common Service API specification, enabling governments, utilities, vendors, and technology companies to exchange rate plan information in a consistent, interoperable way.

While standards exist for customer usage data (Green Button / NAESB REQ.21 Energy Services Provider Interface (ESPI)) and grid operations (CIM), no comprehensive standard exists for the rate plan data that determines how customers are charged. Today, vendors handling rate plan calculations work in silos using custom logic and proprietary data structures. There is no standard format for representing the logic and customer profile attributes needed to compute costs accurately, and no integration with emissions or renewable energy credit data. In deregulated markets, this problem compounds: retail energy suppliers must represent and compare rate plans across multiple distribution utilities, each with its own proprietary format, making it difficult to offer transparent pricing to customers. This fragmentation creates barriers to innovation, competition, and transparency in energy markets: customers cannot easily compare rate plans, vendors must build custom integrations for each utility territory, and those tasked with cost data ingest and cost estimation struggle with data quality across territories. URPX addresses this by defining a single semantic model and API specification that any party can implement, reducing the integration problem from N proprietary formats to one shared standard.

Initiated by Flux Tailor with collaboration from the National Laboratory of the Rockies (NLR), URPX was contributed to LF Energy in 2025 to ensure open, vendor-neutral governance. Flux Tailor serves as working group chair, guiding the specification's development within LF Energy's collaborative standards ecosystem. NLR maintains the Utility Rate Database (URDB), and a formal MOU governs the collaboration between the two organizations on open standard development. While the URPX ontology can reference URDB data, the two formats serve different purposes: URDB contains summary-level pricing data, whereas URPX defines structured rate plan representations with executable cost modeling logic, eligibility criteria, and applicability conditions that go well beyond what URDB captures. The standard is built on W3C semantic web technologies (RDF, OWL, SHACL) with data instances in JSON-LD, made available through GraphQL or REST APIs. From simple flat-rate plans to complex ratchet and time-of-use structures and highly dynamic pricing, URPX provides the shared language required to compute costs accurately and consistently.

## Technical Profile

### What It Does

Defines a standardized ontology, exchange format, and Common Service API specification for utility rate plan data, including rate structures, charge types, eligibility rules, applicability conditions, and temporal versioning, enabling machine-readable representation and programmatic exchange of rate plan information across utility territories.

### Problem(s) Solved

Eliminates the need for vendors and technology companies to reverse-engineer each utility's proprietary rate plan data structures. Provides a common semantic model and API that enables consistent rate plan representation across utilities, allowing customers to compare rate plans, retail energy suppliers in deregulated markets to offer transparent pricing across distribution territories, vendors to scale across territories without custom integrations, DER developers to integrate structured pricing signals into optimization and control systems, and regulators to perform reliable analysis with lower data integration costs.

### Key Capabilities

- Comprehensive rate plan ontology in RDF/OWL covering core rate plan structure and cost model, charge classifications and calculation logic, geographic applicability and jurisdiction, and organizational and regulatory metadata — representing everything from simple flat-rate plans to complex ratchet and time-of-use structures and highly dynamic pricing
- Common Service API specification (REST and GraphQL) for programmatic discovery, retrieval, and querying of published rate plan data, with SPARQL endpoint for advanced semantic queries
- Multiple document types: rate plans, rate plan modifiers (add-on pricing that layers onto a base rate plan), tariff book documents, tariff statement documents (PSC filings), supply prices documents (competitive market pricing), real-time prices documents, and DER export prices
- Rich eligibility rules that define who qualifies for a rate plan, evaluating customer profile attributes (customer class, entity type, tax status, income level) and service point attributes (connection type, voltage level, service territory, DER capability)
- Applicability conditions that define when charges apply, evaluating usage conditions (thresholds, demand levels, power factor), time conditions (TOU periods, seasons, billing cycles, day types), and other conditions (service territory, voltage level)
- Rule evaluation logic with Boolean operators (AND, OR, NOT), comparison operators, and multiple condition types (customer-based, usage-based, time-based, geographic, measurement)
- Temporal versioning and regulatory tracking of rate plan definitions, including full version history and structured tracking of proposed, approved, and retired plans
- Standards alignment with formal SKOS-based mappings to Green Button / NAESB REQ.21 ESPI (rate plan context for usage data), LF Energy CDS (account and billing data alignment), CIM (grid operations), and OpenADR (demand response); interoperability with M2M communication standards including IEEE 2030.5 (SEP) and Matter
- Data validation and conformance using SHACL constraints for schema validation, conformance testing, and data quality enforcement
- Data instances in JSON-LD, accessible through GraphQL or REST APIs
- Reference implementation (planned)
- Test data repository for implementation validation (planned)

### Relevant Standards

URPX is itself an emerging standard — a new open semantic standard for rate plan data exchange. It does not implement an existing industry standard; it aims to become one. URPX is built on W3C semantic web standards (RDF, OWL, SHACL, JSON-LD) and provides formal semantic mappings to related industry standards including Green Button (NAESB REQ.21 ESPI), CIM, LF Energy CDS, and OpenADR. The URPX specification will be released under a W3C license.

## Grid Context

### Grid Segment

Distribution

### Function

Interoperability & Data

### Industry Solution Categories

#### Solution Type

- Rate Plan Data Standard: Provides a standardized ontology, exchange format, and Common Service API specification for utility rate plan data, enabling machine-readable representation, programmatic access, and interoperable exchange across utilities and vendors.

#### Component of

- Customer Information System (CIS): Standardizes the rate plan data object that CIS platforms manage, enabling interoperable exchange of rate structures, eligibility rules, and charge conditions between CIS and downstream systems.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Specification

## Related Projects

- **CDS Customer Data**: Complementary — CDS Customer Data defines how authorized third parties access customer energy data (accounts, billing, usage) from utilities via standardized APIs. URPX defines the standardized format for rate plan data that applies to those customers. A third party using CDS Customer Data to pull customer usage data would need URPX-formatted rate plans to calculate bill impacts. Specific integration points include service account references, billing cycle synchronization, and service agreement attributes used in URPX eligibility rules.
- **CDS Registration**: Complementary — CDS Registration defines how third parties discover utility API capabilities and establish secure connections. URPX leverages CDS Registration's Server Metadata for geographic territory mapping and utility capability discovery, providing the upstream connectivity layer needed to access URPX-formatted rate plan data from utilities.

## Maturity & Adoption

### LF Energy Stage

LFESS Working Group

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- [Flux Tailor](https://fluxtailor.com/) (initiating sponsor, technical lead, and working group chair)
- National Laboratory of the Rockies (NLR) (formal MOU partnership for open standard development; maintains the Utility Rate Database)

## Learn More

- [TAC proposal](https://github.com/lf-energy/tac/issues/600)
	- Date: 2025-08-03
	- Type: TAC proposal
- URPX: Utility Rate Plan Exchange Standard
	- Date: 2025-10-09
	- Type: Presentation
- [LF Energy webpage snapshot](https://lfenergy.org/projects/utility-rate-plan-exchange-urpx/)
	- Date: 2026-03-11
	- Type: Webpage
- URPX code snapshot
	- Date: 2026-03-11
	- Type: Code

## Additional Notes

URPX is positioned as an interoperability standard that complements — rather than competes with — existing vendor solutions and data sources. The standard aims to provide a common data layer that enables the broader ecosystem, including CIS vendors, customer engagement platforms, DER optimization tools, and energy service providers. NLR's existing URDB provides a substantial foundation of rate plan data that can be expressed in URPX format, giving the standard an existing data corpus to build against.

Standardized, machine-readable access to rate plan data is an emerging regulatory topic. Regulators are increasingly referencing standards like Green Button (Connect) for customer data access; URPX positions itself as the analogous standard for rate plan data, which regulators could reference for rate plan publication requirements.

## Language & Attribution Guidelines

This section provides guidance for anyone creating derived works (slide decks, webpage blurbs, press releases, social media) from this document.

### Tagline

> The semantic switchboard for utility rate plan data

### Mission Statement

> Promote market competition, affordability, transparency, and innovation in the energy sector by introducing an open standard for the exchange and publication of machine-readable utility rate plan data from distribution, retail, and other utility service providers.

### Terminology

Always use "rate plan" — not "rate," "tariff," or "rate schedule" — when referring to the pricing structures URPX represents. "Rate plan" is the standard URPX term and should be used consistently across all materials.

Additional terminology standards:

| Use | Avoid | Notes |
|-----|-------|-------|
| Rate plan | Rate, tariff, rate schedule | Complete pricing structure |
| Rate plan data | Rate data, tariff data | The information URPX exchanges |
| Charge | Fee, cost component | Specific billable element |
| Customer profile | Customer type, customer class | Set of attributes describing a customer |
| Service point profile | Meter profile, usage profile | Physical connection characteristics |
| Eligibility rule | Qualification, requirement | Conditions for rate plan access |
| Applicability rule | Condition, trigger | Conditions for when a charge applies |
| Time-of-use period | TOU period, time block | Abbreviation "TOU period" is acceptable |

### Organization Names & Ordering

| Correct | Incorrect |
|---------|-----------|
| NLR (National Laboratory of the Rockies) | NREL |
| Flux Tailor | FluxTailor, Flux-Tailor |
| LF Energy | Linux Foundation Energy |
| LFESS (spell out on first use) | LF Energy Standards and Specifications (without abbreviation after first use) |

When listing project contributors, Flux Tailor is always listed first as the initiating sponsor and working group chair, with a link to https://fluxtailor.com/ where format allows. NLR is listed second as a collaboration partner. Example: "Initiated by [Flux Tailor](https://fluxtailor.com/) with collaboration from the National Laboratory of the Rockies (NLR)."

### Attribution in Derived Works

All derived materials should include:

- Flux Tailor as initiating sponsor and working group chair (listed first, with website link where format allows)
- NLR as collaboration partner (listed second)
- LF Energy / LFESS as the host organization and governance framework
- Link to the canonical version of this document at https://github.com/urpx-org/urpx-wg when practical

### Key Messages by Audience

**Regulators:** URPX provides standardized, AI-ready access to rate plan data. With machine-readable rate plans, regulatory analysis that once took weeks can happen in hours. Market transparency improves when rate plan structures are consistently documented and comparable across utilities.

**Developers:** Stop building custom parsers for every utility. URPX gives you consistent APIs and data structures across territories. The semantic model means your code understands rate plan relationships, not just data fields.

**Utilities:** Publish rate plans once, serve them everywhere. URPX reduces customer service calls by making rate plan information self-documenting. Standardized formats lower vendor integration costs and improve data quality.

**Retail Suppliers:** In deregulated markets, URPX gives competitive energy suppliers a standard format for representing and comparing rate plans across distribution territories. Structured supply price data and eligibility rules enable transparent customer-facing pricing, streamline market entry into new territories, and support automated rate plan comparison tools.

**Customers:** Understand your energy costs. URPX-powered tools let you compare rate plans, see what you qualify for, and model how changes affect your bill — without calling your utility.

**Researchers:** Analyze rate plan structures across markets with consistent data. URPX provides the standardized format needed for large-scale pricing pattern analysis and policy impact studies.

### Voice & Tone

URPX communications should be clear (no jargon without explanation), direct (say what needs to be said), confident (we know this problem well), collaborative (community-first), and pragmatic (focus on real problems).

**Embrace:** transparent, open, accessible, standardized, consistent, reliable, machine-readable, semantic, structured, interoperable, connected, integrated, community, collaboration.

**Avoid:** proprietary, closed, siloed, revolutionary, disruptive (too hyperbolic), simple (rate plans are not simple — URPX makes them manageable).

### Boilerplate Text

**One-liner (25 words):**
URPX is an open standard for exchanging machine-readable utility rate plan data, enabling transparent energy pricing across the industry.

**Short description (50 words):**
URPX (Utility Rate Plan Exchange) is an open standard for machine-readable utility rate plan data. Built on semantic web technologies, URPX acts as the switchboard for transforming flat rate plan data into structured formats with executable cost modeling instructions. Hosted by LF Energy Standards and Specifications.

**Medium description (100 words):**
URPX (Utility Rate Plan Exchange) is an open standard that enables transparent, machine-readable utility rate plan data exchange. While standards exist for customer usage data and grid operations, no comprehensive standard previously existed for the rate plan data that determines how customers are charged. Built on W3C semantic web technologies (RDF, OWL, SHACL), URPX provides a rich ontology and Common Service API for representing everything from simple flat-rate plans to complex time-of-use structures with dynamic pricing. Initiated by Flux Tailor with NLR collaboration, URPX is hosted by LF Energy Standards and Specifications (LFESS).

**Full description (200 words):**
URPX (Utility Rate Plan Exchange) addresses a critical gap in energy data infrastructure. While standards exist for customer usage data (Green Button / NAESB REQ.21 ESPI) and grid operations (CIM), no comprehensive standard existed for the rate plan data that determines how customers are charged for energy.

Today's utility rate plan landscape is fragmented. Each vendor uses proprietary systems for cost calculations. Rate plan data in machine-accessible form is rarely available from utilities. When it is available, there is no standard format for the logic, eligibility rules, or customer profile attributes needed to compute costs accurately.

URPX acts as the semantic switchboard for transforming flat rate plan data into structured rate plans with executable cost modeling instructions. Built on W3C semantic web technologies (RDF, OWL, SHACL), the standard provides a modular ontology for rate plan structures, machine-readable eligibility and applicability rules, temporal versioning with regulatory approval tracking, formal mappings to Green Button, LF Energy CDS, and other standards, and a Common Service API specification for programmatic access.

Initiated by Flux Tailor with formal NLR collaboration, URPX is developed through open collaboration under LF Energy Standards and Specifications (LFESS) governance.

### Social Media

**Hashtags:** #URPX, #LFEnergy, #OpenEnergy, #EnergyData, #RatePlans

**Handle:** @urpx_org (when established)

### Co-branding

When URPX appears alongside LF Energy / LFESS, the URPX logo should be equal or smaller in size. Note "Initiated by Flux Tailor" in text, not as a logo lockup. Note "In collaboration with NLR" in text.

### Visual Identity

For logo usage, color palette, and typography, refer to the URPX Brand Guidelines document maintained at https://github.com/urpx-org/urpx-wg.

### Review Process

This document is maintained by the URPX working group at https://github.com/urpx-org/urpx-wg. Updates should be submitted as pull requests to ensure change tracking and working group review. The working group chair reviews and approves changes before they are merged.
