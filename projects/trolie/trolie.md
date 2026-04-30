# TROLIE

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

- LF Energy webpage: https://lfenergy.org/projects/trolie/
- Website: https://trolie.energy/
- Code: https://github.com/trolie
- Documentation: https://trolie.energy/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/trolie?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/trolie-general
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/trolie
- Other:

## Description

API specification for exchanging transmission facility ratings between Transmission Owners and ISOs/RTOs, enabling FERC Order 881 ambient-adjusted ratings compliance.

## Overview

TROLIE (Transmission Ratings and Operating Limits Information Exchange) is an OpenAPI specification that defines how Transmission Owners (TOs) and ISOs/RTOs exchange transmission line ratings data. It was created to solve an interoperability problem introduced by FERC Order 881, which requires the use of ambient-adjusted ratings (AARs) for transmission lines instead of static seasonal ratings. The order mandates that TOs produce a new 240-hour-ahead forecast for each applicable transmission facility every hour and transmit those ratings to their ISO/RTO — a volume of data that traditional ICCP/SCADA-based exchange methods cannot handle.

TROLIE uses a "Clearinghouse" model: the ISO/RTO hosts a TROLIE server that collects rating proposals from multiple TOs, applies its internal logic, and produces limits snapshots representing the in-use operating limits for each transmission facility. TOs run TROLIE clients that submit forecast and real-time rating proposals to the Clearinghouse. The specification covers the full lifecycle of ratings exchange — forecast proposals (240-hour ahead), real-time ratings, seasonal ratings, temporary AAR exceptions, and cross-regional reconciliation for tie-lines between Reliability Coordinators. It also provides limit provenance, allowing TOs to see how the Clearinghouse determined the in-use rating for their facilities.

Beyond the specification itself, the TROLIE project includes a conformance test suite for validating server implementations and a Java client SDK for building TROLIE clients. MISO and GE Vernova co-originated the project. GE Vernova has adopted the TROLIE specification in its Limit Exchange Portal product for both ISOs and TOs (as of June 2025).

## Technical Profile

### What It Does

Defines a REST/JSON API for Transmission Owners to submit transmission line rating proposals to ISOs/RTOs and for ISOs/RTOs to publish the resulting operating limits back to stakeholders.

### Problem(s) Solved

FERC Order 881 requires TOs and ISOs/RTOs to exchange ambient-adjusted ratings at a scale that existing ICCP/SCADA infrastructure cannot support — a single transmission line would need over 1,400 SCADA points to exchange 240-hour forecasts in both directions. TROLIE provides a standard data exchange protocol that replaces ad-hoc, point-to-point integration between each TO and ISO, reducing the implementation burden from N custom integrations to one shared specification.

### Key Capabilities

- Forecast ratings exchange: TOs submit 240-hour-ahead rating forecasts; the Clearinghouse produces forecast limits snapshots
- Real-time ratings exchange: TOs submit current-hour ratings based on actual ambient conditions
- Seasonal ratings management: exchange of recourse ratings that apply when AARs are unavailable
- Temporary AAR exceptions: handling of facilities that temporarily cannot receive ambient-adjusted ratings due to outages or clearance concerns
- Limit provenance: detailed snapshots showing which proposals the Clearinghouse considered, any AAR exceptions, and any operator overrides for each in-use limit
- Monitoring sets: named collections of power system resources enabling filtered API queries (e.g., per-TO or per-region)
- Segment-based model: supports jointly-owned facilities and tie-lines where different entities submit separate proposals for different segments of the same transmission facility
- Cross-regional reconciliation: RC-to-RC peering for coordinating ratings on tie-lines between Reliability Coordinators
- Efficient polling via Conditional GET: uses HTTP ETag/If-None-Match headers to avoid transferring unchanged data
- Conformance test suite: BDD-style test suite (Gherkin/pytest-bdd) for validating server implementations against the specification
- Java client SDK: framework-agnostic client library with built-in compression, retries, and Conditional GET support

### Relevant Standards

- FERC Order 881 — requires ambient-adjusted ratings for transmission lines and defines the regulatory framework that TROLIE implements the data exchange for

<!-- TROLIE does not implement FERC Order 881 itself (which is a regulatory order, not a technical standard), but it is purpose-built to enable compliance. No IEC/IEEE standards are directly implemented. -->

## Grid Context

### Grid Segment

Transmission

### Function

Grid Operations

### Industry Solution Categories

#### Solution Type

- Transmission Ratings Exchange: Defines a standard API for exchanging transmission line ratings between Transmission Owners and ISOs/RTOs.

#### Component of

- EMS: Provides the data exchange layer that delivers ambient-adjusted ratings into the Energy Management System for use in real-time operations and security analysis.
- Market Management System: FERC Order 881 requires AARs in day-ahead and real-time market models; TROLIE delivers the ratings data that defines transmission constraints used in market dispatch and pricing.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Specification

## Related Projects

None currently. TROLIE's scope — FERC Order 881 transmission ratings exchange between TOs and ISOs/RTOs — is specialized and does not have direct technical integration points with other LF Energy projects.

<!-- PowSyBl performs transmission security analysis that uses line ratings as inputs, but there is no direct code integration or shared data flow with TROLIE. -->

## Maturity & Adoption

### LF Energy Stage

LFESS Working Group

### Deployment Maturity

Production

### Supporting / Adopting Organizations

- MISO (co-originator)
- GE Vernova (co-originator; lead maintainer; adopted TROLIE specification in its Limit Exchange Portal product for ISOs and TOs, as of June 2025)
- ISO New England (TROLIE installation referenced in project materials, as of November 2024)
- SPP (TROLIE installation referenced in project materials, as of November 2024)

<!-- ISO-NE and SPP are referenced in the Nov 2024 presentation in the context of Java client authentication support for their TROLIE installations. This suggests they have or are building TROLIE servers but should be verified against primary sources. -->

## Learn More

- A Lap around TROLIE 1.0
	- Date: 2024-11-20
	- Type: Webinar
- [Introduction to TROLIE](https://community.linuxfoundation.org/events/details/lfhq-lf-energy-presents-webinar-introduction-to-trolie/)
	- Date: 2024-02-21
	- Type: Webinar
- [Meeting the challenge of FERC Order 881: Why open source matters for AAR implementation](https://www.utilitydive.com/news/ferc-order-881-aar-ambient-adjusted-rating-trolie/750604/)
	- Date: 2025-06-13
	- Type: Article

## Additional Notes

TROLIE is unique in the LF Energy portfolio as a **regulation-driven, North America-specific** specification. FERC Order 881 creates mandatory compliance demand — every FERC-jurisdictional TO and ISO/RTO must implement ambient-adjusted ratings exchange. This regulatory driver means adoption is not optional for the target audience, which is a fundamentally different adoption dynamic than technology-driven projects.

The project is a specification first and a software project second. The OpenAPI specification is licensed under the Community Specification License 1.0 (providing IP clarity essential for critical infrastructure); supporting tools (Java client SDK, conformance suite) are licensed under Apache 2.0. This structure — open specification with open tooling — allows any vendor to build conformant implementations while the shared spec ensures interoperability.

Before TROLIE, each TO-to-ISO integration was a custom point-to-point implementation. With multiple TOs per ISO footprint and TOs potentially operating across multiple ISO regions, this created an N-to-M integration problem. TROLIE reduces this to a single shared interface, analogous to how OpenADR standardized demand response signaling.