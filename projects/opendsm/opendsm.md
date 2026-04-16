# OpenDSM

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

- LF Energy webpage: https://lfenergy.org/projects/opendsm/
- Website: https://opendsm.energy/
- Code: https://github.com/opendsm/opendsm
- Documentation: https://opendsm.energy/documentation/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/opendsm?view=month
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/opendsm-discussion/
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/opendsm
- Other:
	- PyPI package: https://pypi.org/project/opendsm/
	- Related package — EEweather (weather data): https://github.com/opendsm/eeweather
	- Related package — CalTRACK (methodology docs & tests): https://github.com/opendsm/caltrack

## Description

Measurement and verification (M&V) of energy impacts for demand-side programs, including energy efficiency, demand response, electrification, and load shifting.

## Overview

OpenDSM is a Python library for measuring the energy impacts of demand-side programs. Given historical meter data and weather observations, it builds statistical baseline models of a building's expected consumption, then compares that baseline to actual post-intervention consumption to quantify avoided energy use (AEU). This counterfactual approach — modeling what consumption *would have been* without the program — is the standard method for measuring savings from energy efficiency retrofits, demand response events, electrification conversions, and load-shifting programs. OpenDSM implements the CalTRACK methodology, with uncertainty quantification based on ASHRAE Guideline 14.

Measuring the impact of demand-side programs is a longstanding challenge for utilities. Savings are invisible by definition — you cannot directly meter energy that was not consumed. Without rigorous, transparent M&V, utilities cannot demonstrate program effectiveness to regulators, settle performance-based incentive contracts, or compare the cost-effectiveness of different interventions. Proprietary M&V approaches also create inconsistency across programs and jurisdictions. OpenDSM addresses this by providing a standardized, auditable implementation designed for the scale of an entire utility meter portfolio, with built-in data sufficiency checks to ensure methodology compliance before model fitting.

According to Recurve Analytics, OpenDSM has been used to measure hundreds of energy efficiency, demand response, and electrification programs since 2016. In January 2025, the U.S. Department of Energy approved OpenDSM (then OpenEEMeter) as the first M&V solution for the measured pathway under the IRA HOMES rebate program. The project is primarily developed by Recurve Analytics, which also offers a commercial platform (FLEX) built on OpenDSM.

## Technical Profile

### What It Does

Builds statistical baseline models from historical meter and weather data, generates counterfactual consumption predictions, and quantifies avoided energy use from demand-side interventions at individual building and portfolio levels.

### Problem(s) Solved

Enables utilities and program administrators to measure savings from demand-side programs (energy efficiency, demand response, electrification, load shifting) using a standardized, transparent methodology that scales to millions of meters — replacing inconsistent proprietary approaches and enabling performance-based program evaluation and regulatory reporting.

### Key Capabilities

- Multiple model types at billing, daily, and hourly resolution — including a solar-aware hourly model that integrates Global Horizontal Irradiance (GHI) data to account for behind-the-meter PV generation
- Demand response hourly model for measuring short-term building-level impacts from DR events
- Built-in data sufficiency validation to verify compliance with CalTRACK methodology requirements before model fitting
- Fractional savings uncertainty (FSU) calculations based on ASHRAE Guideline 14
- Model serialization to JSON for persistence and portability across systems
- Designed for the scale of an entire utility meter portfolio
- Companion EEweather package for automated weather station matching and data retrieval

### Relevant Standards

- ASHRAE Guideline 14 — used for site-level fractional savings uncertainty calculations

## Grid Context

### Grid Segment

Distribution, Behind the Meter

### Function

Flexibility & Markets

### Industry Solution Categories

#### Solution Type

- M&V Calculation Engine: Provides the statistical baseline modeling and avoided energy use quantification that underpins measurement and verification of demand-side programs.

#### Component of

- M&V Platform: Serves as the core calculation engine within a broader M&V platform that adds data management, reporting, and program workflow.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

None currently identified. While OpenDSM operates in the demand-side domain alongside projects like OpenLEADR (demand response signaling) and Shapeshifter (flexibility trading), there are no direct code integrations, shared data flows, or complementary workflow connections with other LF Energy projects at this time.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

Production

### Supporting / Adopting Companies

- Recurve Analytics (primary developer; provides commercial FLEX platform built on OpenDSM)

## Learn More

- [Reliably Measuring Demand-Side Interventions in a Solar PV World with OpenDSM](https://community.linuxfoundation.org/events/details/lfhq-lf-energy-presents-reliably-measuring-demand-side-interventions-in-a-solar-pv-world-with-opendsm/)
	- Date: 2025-09-24
	- Type: Presentation
	- Slideshare link: https://www.slideshare.net/slideshow/lf-energy-webinar-reliably-measuring-demand-side-interventions-in-a-solar-pv-world-with-opendsm/283441261
- [U.S. Department of Energy Validates Open Source Approach for IRA HOMES Programs](https://lfenergy.org/us-department-of-energy-validates-open-source-approach-for-ira-homes-programs/)
	- Date: 2025-01-17
	- Type: Blog Post

## Additional Notes

OpenDSM was formerly called OpenEEMeter. References to OpenEEMeter in external sources (documentation, blog posts, DOE filings) refer to the same project and codebase.

OpenDSM's methodology is rooted in CalTRACK, a specification developed through a California Public Utilities Commission (CPUC) working group starting in 2015 to standardize metered savings calculations for pay-for-performance energy efficiency programs. Models run with default settings produce OpenDSM compliant measurements. This regulatory origin — and the DOE approval for IRA HOMES — positions OpenDSM as particularly relevant in U.S. jurisdictions with performance-based energy efficiency and electrification programs, though the statistical methods are general-purpose.

The project is the only open source implementation of CalTRACK-based M&V at production scale, providing a transparent alternative to proprietary M&V platforms where methodology details are often opaque. This transparency is a key value proposition for regulators and program evaluators who need to audit savings claims.