# covXtreme

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

- LF Energy webpage: https://lfenergy.org/projects/covxtreme/
- Website:
- Code: https://github.com/covXtreme
- Documentation: https://github.com/covXtreme/covXtreme/blob/main/covXtreme_UserGuide.pdf
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/covxtreme?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/covxtreme
- Other:

## Description

Statistical toolkit for modeling extreme environmental events — such as extreme wave heights, wind speeds, and temperatures — that vary with conditions like direction and season, producing return value estimates and design contours for infrastructure engineering.

## Overview

covXtreme is a MATLAB toolkit for extreme value analysis of environmental variables that change with conditions such as direction, season, or location. Given historical observations of storm peaks or other extreme events, it fits statistical models that capture how the severity and joint behavior of these extremes vary across different conditions, then uses those models to estimate rare event magnitudes (e.g., the 1,000-year maximum wave height from a given storm direction) and generate environmental design contours for pairs or triplets of variables. The software handles the full analysis workflow: peak extraction from time series, covariate binning, marginal distribution fitting, multivariate dependence modeling, and contour estimation — with uncertainty quantification throughout via bootstrap resampling.

The core problem covXtreme addresses is characterizing rare environmental extremes for infrastructure design. Engineers designing structures exposed to environmental loading — offshore platforms, coastal defenses, wind turbine foundations — must design for conditions far more severe than anything in the historical record. A 30-year wave measurement dataset must support design decisions for 100-year or 1,000-year return periods. Standard extreme value methods often assume environmental conditions are stationary (the same regardless of storm direction, season, or climate trend), which can lead to under- or over-design. covXtreme's non-stationary approach accounts for these variations, producing more realistic estimates of joint extreme conditions.

covXtreme was developed by statisticians at Shell and Lancaster University primarily for offshore metocean applications — characterizing joint extremes of wave height, wave period, wind speed, and structural loading for platform design. The methodology is general-purpose and applicable to any domain with non-stationary multivariate extremes, including extreme temperatures, rainfall, river levels, and wind speeds. Part-funded by the EU's ECSADES project, the software is provided as a set of MATLAB functions with two worked case studies and a comprehensive user guide.

## Technical Profile

### What It Does

Fits non-stationary extreme value models to multivariate environmental data that varies with covariates (direction, season, etc.), producing return value estimates at specified return periods and environmental design contours for infrastructure engineering.

### Problem(s) Solved

Enables engineers to estimate the severity of rare environmental events (beyond what historical records directly show) while accounting for how those extremes vary with conditions like storm direction and season. Replaces stationary assumptions that can lead to under- or over-design of infrastructure exposed to environmental loading.

### Key Capabilities

- Non-stationary marginal extreme value modeling using piecewise constant Generalized Pareto distributions with roughness-penalized maximum likelihood, allowing extreme value parameters to vary across covariate bins (e.g., by storm direction or season)
- Conditional dependence modeling using the Heffernan-Tawn framework, capturing how joint extremes of multiple variables (e.g., wave height and wave period) co-vary across conditions
- Environmental design contour estimation via three methods (constant exceedance, direct sampling, Heffernan-Tawn density), producing joint extreme envelopes at specified return periods
- Bootstrap uncertainty quantification for all model parameters, return values, and contours
- Storm peak extraction from time series with configurable threshold and storm separation criteria
- Multi-dimensional covariate binning with support for periodic covariates (e.g., 0–360° direction)
- Synthetic data generation for validation and testing of the statistical methodology

### Relevant Standards

None. covXtreme is a statistical analysis toolkit and does not directly implement grid communication or data model standards.

## Grid Context

covXtreme is a general-purpose statistical toolkit, not a grid-specific solution. Its primary documented applications are in offshore metocean engineering. The grid context below reflects potential applicability rather than current use.

### Grid Segment

Generation (secondary — applicable to offshore wind resource assessment and turbine foundation design, where characterizing joint extremes of wave height, wind speed, and structural loading is required)

### Function

Does not map to a function category. See taxonomy.md.

### Industry Solution Categories

#### Solution Type

- Extreme Event Hazard Analysis: Characterizes the statistical behavior of rare environmental events for infrastructure design, producing return value estimates and environmental design contours at specified return periods.

#### Component of

None. covXtreme is a standalone statistical analysis toolkit. It is not a component of a recognized utility system category.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

None. No LF Energy projects have documented technical integration points, shared data flows, or complementary workflows with covXtreme. While extreme value analysis outputs could theoretically serve as inputs to infrastructure planning or resilience modeling tools, no such integrations currently exist.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

Production (in offshore engineering; no known grid/utility deployments)

### Supporting / Adopting Organizations

- Shell (primary developer; production user for offshore metocean engineering)
- Lancaster University (co-developer; academic research partner)

## Learn More

- [covXtreme : MATLAB software for non-stationary penalised piecewise constant marginal and conditional extreme value models](https://www.sciencedirect.com/science/article/pii/S1364815224000963)
	- Date: 2024-04-13
	- Type: Journal article

## Additional Notes

covXtreme is unusual in the LF Energy portfolio: it is a domain-agnostic scientific computing tool rather than a grid digitalization solution. Its presence in the ecosystem reflects Shell's contribution of internal engineering software to the energy open source community, and the general applicability of extreme value statistics to energy infrastructure — particularly offshore wind, where metocean design criteria directly determine structural and foundation requirements. However, all documented case studies and production use to date are in offshore oil & gas engineering, not electricity grid applications.

The MATLAB-only implementation limits accessibility in modern data science environments. The project's contributing guidelines identify a Python reimplementation as a desired future enhancement, which would significantly broaden potential adoption. All components are licensed under Apache 2.0.