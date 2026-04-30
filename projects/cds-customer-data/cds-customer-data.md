# CDS Customer Data

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

## Basic Info

- LF Energy webpage: https://lfenergy.org/projects/cds-customer-data/
- Website: https://daniel-roesler.github.io/CDS-Customer-Data/ <!-- note this is a development branch, but accurately reflects the direction of the working group -->
- Code: https://github.com/daniel-roesler/CDS-Customer-Data/tree/issue_29_updated_use_cases <!-- note this is a development branch, but accurately reflects the direction of the working group -->
- Documentation: https://daniel-roesler.github.io/CDS-Customer-Data/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/cds-customerdata-wg?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/cds-customer-data-wg
	- Slack:
- LFX Insights:
- Other:
	- Official repository: https://github.com/lfe-cds/CDS-Customer-Data
	- Specification website: https://cds-customerdata.lfenergy.org/

## Description

Specification defining standardized APIs for authorized third parties to access customer energy data — accounts, billing, usage, and meter metadata — from utilities via OAuth-based consent.

## Overview

CDS Customer Data is a specification that defines how utilities expose customer energy data to authorized third-party companies and applications through standardized REST/JSON APIs. The specification covers the full range of customer data: account information, service contracts, meter metadata, energy usage (interval data), billing statements and line-item details, aggregated portfolio data, and energy attribute certificates (EACs). Access is governed by OAuth 2.0, with fine-grained scopes that let customers control exactly what data they share — for example, a customer can authorize access to usage data without sharing billing details.

Today, every utility exposes customer data differently — different APIs, data formats, authentication methods, and consent flows. Third parties that need customer energy data (virtual power plants, carbon accounting platforms, solar installers, building energy auditors, demand response providers) must build and maintain custom integrations for each utility. This creates a significant barrier to scaling energy services: a company that works with 50 utilities needs 50 different integrations. CDS Customer Data addresses this by defining a single API specification that any utility can implement, reducing the integration problem from N custom connections to one shared standard.

The specification extends CDS-WG1-02 (Client Registration), which handles how third parties register with utilities and establish secure connections. CDS Customer Data adds customer-data-specific OAuth scopes and API endpoints to the client registration response defined by WG1-02. The specification is maintained by UtilityAPI with contributions from Flexidao.

## Technical Profile

### What It Does

Defines a set of REST/JSON APIs and OAuth 2.0 authorization scopes that standardize how utilities provide customer energy data (accounts, bills, usage, meters, EACs) to authorized third parties.

### Problem(s) Solved

Eliminates the need for third-party energy service providers to build custom data integrations with each utility. Gives utilities a standard API to implement for customer data access, and gives customers granular control over what data they share and with whom.

### Key Capabilities

- Customer account and service contract APIs providing account hierarchies, rate plans, service classes, and related entity information
- Meter metadata APIs covering service points (delivery locations with addresses and coordinates) and meter device information
- Energy usage API with configurable interval data supporting multiple measurement types (kWh forward/reverse/net, demand kW, gas, water)
- Bill statement and bill section APIs providing billing documents, amounts due, payment dates, and line-item breakdowns by service type and supplier
- Aggregation API for portfolio-level data groupings (buildings, regions, rate plans) with consent requirement handling
- Energy attribute certificate (EAC) API for renewable energy certificate data with beneficiary allocation
- Fine-grained OAuth 2.0 scopes allowing customers to authorize specific data categories (e.g., `cds_usage_detailed`, `cds_bill_amount_due`, `cds_accounts_basic`)
- Machine-to-machine scopes (client credentials grant) for aggregation queries that do not require individual customer consent
- Standardized pagination, filtering (date ranges, ID lists, text search), and ordering across all endpoints

### Relevant Standards

- IETF RFC 6749 / RFC 8414 (OAuth 2.0) — the specification builds its authorization and consent model on the OAuth 2.0 framework

<!-- The spec uses OAuth 2.0 as its core authorization mechanism, extending it with energy-specific scopes. This is a genuine implementation of OAuth patterns, not merely adjacent use. -->

## Grid Context

### Grid Segment

Distribution

### Function

Interoperability & Data

### Industry Solution Categories

#### Solution Type

- Customer Data Access Standard: Defines standardized APIs for utilities to provide customer energy data to authorized third parties with consent-based access control.

#### Component of

None — the specification defines an external API standard, not a building block inside a larger system.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Specification

## Related Projects

- **CDS Registration**: Builds on — CDS Customer Data extends CDS-WG1-02 (Client Registration) by adding customer-data-specific OAuth scopes and API endpoint URLs to the client registration response. CDS-WG1-02 handles third-party registration and secure connection establishment; Customer Data defines what data flows over those connections.
- **URPX**: Complementary — URPX defines a standardized format for utility rate plan data (structures, eligibility rules, charges). A third party using CDS Customer Data to pull customer usage data would need URPX-formatted rate plans to calculate bill impacts. URPX references CDS service accounts and aligns billing cycles with CDS billing periods.

## Maturity & Adoption

### LF Energy Stage

LFESS Working Group

### Deployment Maturity

R&D

<!-- The specification is in draft status. No known production implementations by utilities as of early 2026. -->

### Supporting / Adopting Organizations

- UtilityAPI (primary maintainer; customer data access platform provider)
- Flexidao (contributor; clean energy certificate and carbon accounting platform)

## Learn More

- [An Overview of the New Carbon Data Specification Discovery, Registration, and Customer Data Drafts](https://lfenergysummit2024.sched.com/event/1ehIt/an-overview-of-the-new-carbon-data-specification-consortium-cdsc-discovery-registration-and-customer-data-specification-drafts-daniel-roesler-utilityapi-eloi-fabrega-ferrer-flexidao)
	- Date: 2024-09-06
	- Type: Presentation

## Additional Notes

CDS Customer Data is a specification, not software. Like TROLIE, it defines an API contract that any party can implement — it does not ship a reference server or client library. The specification is licensed under the Joint Development Foundation (JDF) model; supporting documentation is Apache 2.0.

The incumbent standard in this space is Green Button (based on NAESB ESPI / OASIS Energy Interop), which has been the primary customer energy data access standard in North America since ~2012 and has regulatory mandates in several US states. Green Button uses XML/Atom feeds, while CDS Customer Data uses REST/JSON with OAuth 2.0 — a more modern web API architecture. CDS Customer Data also covers a broader data scope than Green Button's core energy usage focus, including bill line-item details, energy attribute certificates, and portfolio aggregations.

CDS Customer Data is closely related to but separate from CDS Registration. They share the same connectivity layer (the CDS Connectivity specifications from WG1) but address different data domains and can exist independently.