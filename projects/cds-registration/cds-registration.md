# CDS Registration

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

- LF Energy webpage: https://lfenergy.org/projects/cds-registration/
- Website: https://cds-registration.lfenergy.org/
- Code: https://github.com/lfe-cds/CDS-Registration
- Documentation: https://cds-registration.lfenergy.org/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/cds-registration-wg?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/cds-registration-wg
	- Slack:
- LFX Insights:
- Other:

## Description

Specifications standardizing how utilities publish their API capabilities and how third parties discover, register with, and establish secure connections to those utilities.
## Overview

CDS Registration is a pair of specifications that define the connectivity layer between utilities and third-party companies. CDS-WG1-01 (Server Metadata) standardizes how utilities publish what data and services they offer via a well-known JSON endpoint (`/.well-known/cds-server-metadata.json`), including their service territory, infrastructure types, and supported capabilities. CDS-WG1-02 (Client Registration) standardizes how third parties register with those utilities, obtain OAuth 2.0 credentials, manage their client profiles, and handle authorization grants — providing the secure identity and access management foundation that data-specific specifications build on.

Today, each utility that offers API access to third parties implements its own discovery mechanism, registration process, and authentication scheme. A third-party company wanting to connect to multiple utilities must learn and implement each utility's proprietary onboarding flow. CDS Registration solves this by defining a single, predictable process: discover the utility's capabilities via Server Metadata, register programmatically via Dynamic Client Registration, and manage the ongoing connection through standardized client management, messaging, and credential APIs.

The specifications are designed as a shared foundation layer. Other CDS specifications (such as CDS Customer Data) extend CDS Registration by adding domain-specific OAuth scopes and API endpoints to the connectivity framework. The specifications are maintained by UtilityAPI with contributions from Flexidao.
## Technical Profile

### What It Does

Defines how utilities publish their capabilities via a standardized metadata endpoint (WG1-01) and how third parties programmatically register, authenticate, and manage secure API connections with those utilities via OAuth 2.0 (WG1-02).
### Problem(s) Solved

Gives utilities a standard way to publish what API capabilities they offer, and gives third-party companies a single, predictable process for discovering utilities, registering for access, and managing credentials — replacing utility-by-utility custom onboarding.
### Key Capabilities

- Server Metadata endpoint at a well-known URL providing utility name, description, service territory coverage, infrastructure types (distribution utility, DSO, TSO, metering provider, etc.), and supported capabilities
- Coverage API with geographic and logical coverage entries, including GeoJSON boundaries and commodity types (electricity, natural gas, water, distributed energy)
- OAuth 2.0 Dynamic Client Registration (based on RFC 7591) extended with CDS-specific registration fields and scope descriptions
- Authorization Server Metadata (based on RFC 8414) extended with CDS-specific endpoints for client management, messaging, credentials, and grants
- Client management APIs for listing, retrieving, and modifying client profiles, with sandbox and production status separation
- Grants API with rich lifecycle management — active, pending, future, suspended, revoked, and other statuses — supporting both machine-to-machine and user-authorized access
- Messages API for structured communication between clients and servers (update requests, grant requests, status notifications)
- Credentials API for managing OAuth client secrets with expiration and rotation
- Server-Provided Files API for secure ad-hoc file sharing (configuration files, certificates, manual backfill data)
- Extensible design: object formats and enumerated lists can be extended by downstream specifications without breaking existing clients
### Relevant Standards

- IETF RFC 6749 (OAuth 2.0) — core authorization framework
- IETF RFC 7591 (OAuth 2.0 Dynamic Client Registration) — the specification extends this for programmatic client registration
- IETF RFC 8414 (OAuth 2.0 Authorization Server Metadata) — the specification extends this for capability discovery
- IETF RFC 9126 (Pushed Authorization Requests) — required for user-authorization flows
- IETF RFC 9396 (Rich Authorization Requests) — used for fine-grained access control on grants
## Grid Context

### Grid Segment

Distribution

### Function

Interoperability & Data

### Industry Solution Categories

#### Solution Type

- Utility Data Connectivity Standard: Defines standardized protocols for third parties to discover utility API capabilities, register for access, and manage secure connections.

#### Component of

None — the specification defines connectivity infrastructure, not a building block inside a larger system.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Specification

## Related Projects

- **CDS Customer Data**: Foundation for — CDS Customer Data extends CDS-WG1-02 by adding customer-data-specific OAuth scopes and API endpoint URLs. CDS Registration provides the discovery, registration, and authentication layer; CDS Customer Data defines what customer data flows over those connections.
- **URPX**: Complementary — URPX leverages CDS Registration's Server Metadata for geographic territory mapping and utility capability discovery, providing the upstream connectivity layer needed to access URPX-formatted rate plan data from utilities.

## Maturity & Adoption

### LF Energy Stage

LFESS Working Group

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- UtilityAPI (primary maintainer; customer data access platform provider)
- Flexidao (contributor; clean energy certificate and carbon accounting platform)

## Learn More

- [An Overview of the New Carbon Data Specification Discovery, Registration, and Customer Data Drafts](https://lfenergysummit2024.sched.com/event/1ehIt/an-overview-of-the-new-carbon-data-specification-consortium-cdsc-discovery-registration-and-customer-data-specification-drafts-daniel-roesler-utilityapi-eloi-fabrega-ferrer-flexidao)
	- Date: 2024-09-06
	- Type: Presentation

## Additional Notes

CDS Registration is a specification, not software. Like TROLIE and CDS Customer Data, it defines API contracts that any party can implement — it does not ship a reference server or client library. The specifications are licensed under the Joint Development Foundation (JDF) model; supporting documentation is Apache 2.0.

The two specs serve distinct but complementary roles. CDS-WG1-01 (Server Metadata) is the discovery layer — a lightweight, publicly accessible endpoint that lets anyone find out what a utility offers. CDS-WG1-02 (Client Registration) is the identity and access management layer — a comprehensive OAuth-based system for establishing and maintaining secure API connections. Together they form a reusable connectivity foundation that is intentionally domain-agnostic, designed to be extended by data-specific specifications rather than tied to any particular data domain.

CDS Registration is closely related to but separate from CDS Customer Data. CDS Customer Data is the first (and currently only) specification to extend the CDS Registration connectivity layer, but the design intent is for other specifications to reuse the same foundation.