# OpenSTEF

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

- LF Energy webpage: https://lfenergy.org/projects/openstef/
- Website:
- Code: https://github.com/OpenSTEF
- Documentation:
	- Code: https://openstef.github.io/openstef/index.html
 	- Community: https://lf-energy.atlassian.net/wiki/spaces/OS/overview?homepageId=32276506
- Calendar:
	- Community meetings: https://lf-energy.atlassian.net/wiki/spaces/OS/pages/32278358/OpenSTEF+four-weekly+community+meeting
 	- Co-coding sessions: https://lf-energy.atlassian.net/wiki/spaces/OS/pages/919437342/OpenSTEF+Co-coding+Sessions
  	- TSC meetings: https://lf-energy.atlassian.net/wiki/spaces/OS/pages/32278002/OpenSTEF+Technical+Steering+Committee and https://zoom-lfx.platform.linuxfoundation.org/meetings/openstef?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack: https://lfenergy.slack.com/archives/C04P56MSM40
- LFX Insights: https://insights.linuxfoundation.org/project/openstef
- Other:

## Description

Automated machine learning pipelines for short-term (up to 48 hours ahead) energy load forecasting.

## Overview

OpenSTEF (Short-Term Energy Forecasting) provides automated machine learning pipelines that forecast energy load at specific locations up to 48 hours ahead. Given a time series of measured load, OpenSTEF combines it with external predictors — weather forecasts, market prices, and typical demand profiles — to produce probabilistic forecasts with confidence intervals. The system handles the full workflow from data validation through feature engineering, model training, forecasting, and evaluation, requiring minimal data science expertise to operate. For electricity grid applications, OpenSTEF includes dedicated solar and wind generation forecasting modules whose outputs feed into the load prediction pipeline as input features, accounting for behind-the-meter generation impact on net load.

Accurate short-term load forecasts are essential for managing congested distribution grids. As electrification and distributed generation push grid assets closer to their limits, operators need to anticipate overloads hours or days ahead to take preventive action — whether through flexibility markets, redispatch, or curtailment. Without reliable forecasts, operators must either over-build the grid or react to congestion after it occurs. OpenSTEF enables proactive congestion management by providing forecasts at individual substations and feeder routes, allowing operators to identify where and when capacity limits will be exceeded and initiate market-based responses in time.

OpenSTEF is deployed in production at Alliander (the largest Dutch DSO), where it delivers operational forecasts at hundreds of grid locations. At Alliander, OpenSTEF is part of the "Grid-as-a-Service" congestion management pipeline: OpenSTEF forecasts load, Power Grid Model performs network calculations to identify congestion, and Shapeshifter coordinates flexibility market responses to resolve it. Beyond electricity grids, Sigholm uses OpenSTEF as the forecasting engine for its Aurora by Sigholm platform, which optimizes district heating and combined heat and power production across Sweden, Norway, and Finland — demonstrating the framework's adaptability to thermal energy systems.

## Technical Profile

### What It Does

Produces automated short-term probabilistic forecasts of energy load at specific locations, using machine learning models trained on historical measurements and external predictors including weather, market prices, and (for electricity grids) behind-the-meter generation estimates.

### Problem(s) Solved

Enables grid operators to forecast load at substations and feeder routes without building custom ML pipelines, providing the forward-looking visibility needed for congestion management, flexibility market participation, and operational planning. Replaces manual or spreadsheet-based forecasting with automated, continuously retrained models that adapt as the grid evolves.

### Key Capabilities

- Probabilistic forecasts with configurable confidence intervals, enabling risk-based operational decisions
- Supports multiple ML model types (XGBoost, LightGBM, linear regression, ARIMA) — model selection can be tuned per use case (e.g., linear models for congestion peak detection, XGBoost for general accuracy)
- Solar and wind generation forecasting modules that feed into the load prediction pipeline, accounting for behind-the-meter generation impact on net load
- Energy splitting: decomposes net load forecasts into solar, wind, and demand components at locations lacking component-level historical data (DAZLS zero-shot learning technique)
- Automated model training, evaluation, and retraining with performance verification before deployment
- Input data validation with detection of flatliners, missing data, and anomalies
- Automated feature engineering from weather, market, calendar, and lagged load data
- Fallback forecast strategies ensuring a forecast is always available, with fallback status labeled for auditability
- Containerized, cloud-native architecture with a reference implementation for rapid deployment

### Relevant Standards

None. OpenSTEF is an ML forecasting framework and does not directly implement grid communication or data model standards.

## Grid Context

### Grid Segment

Distribution (primary), Transmission (secondary — transport forecasts at DSO-to-TSO coupling points)

### Function

Grid Operations

### Industry Solution Categories

#### Solution Type

- Load Forecasting: Provides automated short-term energy load forecasting using machine learning, with probabilistic output for risk-based decision making.

#### Component of

- ADMS: Supplies the forecasting capability needed for forward-looking congestion management within distribution grid operations.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** Yes
- **Deliverable Type:** Software

## Related Projects

- **Power Grid Model**: Complementary — OpenSTEF produces load forecasts that feed into Power Grid Model power flow calculations for forward-looking congestion analysis. At Alliander, OpenSTEF forecasts at MV feeder routes are combined with PGM network calculations for congestion management.
- **Shapeshifter**: Complementary — within Alliander's Grid-as-a-Service congestion management pipeline, OpenSTEF forecasts load, Power Grid Model identifies congestion, and Shapeshifter handles flexibility market coordination to resolve it.
- **SOGNO**: SOGNO's ProLoaF provides probabilistic load forecasting with a research focus, while OpenSTEF provides production-grade operational forecasting.
- **FlexMeasures**: Complementary — OpenSTEF forecasts energy load at grid locations, FlexMeasures optimizes flexible assets to manage consumption in response. In a congestion management workflow, OpenSTEF identifies where congestion will occur and FlexMeasures could determine how flexible assets should respond.
- **RTC-Tools**: Complementary — OpenSTEF can provide load and price forecasts as inputs to RTC-Tools asset optimization models for hydropower scheduling and BESS trading.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

Production

### Supporting / Adopting Companies

- Alliander (primary developer; production user — operational forecasts at hundreds of grid locations)
- Sigholm (production user — forecasting engine for Aurora by Sigholm district heating optimization platform; as of December 2025, serving ~40% of Sweden's district heating production)
- RTE (French TSO; active contributor)
- RTE International (contributor)
- Firan (contributor)
- Shell (community participant)

## Learn More

- [OpenSTEF Delivers Operational Forecasts at Hundreds of Grid Locations for Alliander](https://lfenergy.org/openstef-delivers-operational-forecasts-at-hundreds-of-grid-locations-for-alliander/)
	- Date: 2022-12-19
	- Type: Case Study
- [Net Congestion Forecasting at Liander](https://lfenergysummit2024.sched.com/event/1ehJO/net-congestion-forecasting-daan-van-es-alliander)
	- Date: 2024-09-06
	- Type: Presentation
- [The Value of Open Source Short-term Energy Forecasting Demonstrated Through Real-world Use Cases](https://lfenergysummiteu2025.sched.com/event/26Ixh/the-value-of-open-source-short-term-energy-forecasting-demonstrated-through-real-world-use-cases-bart-pleiter-alliander-jan-maarten-van-doorn-sigholm)
	- Date: 2025-09-10
	- Type: Presentation
- [Optimizing Nordic District Heating: How OpenSTEF Powers 40% of Sweden's Heat Production](https://lfenergy.org/openstef-sigholm-nordic-heating-case-study/)
	- Date: 2025-12-16
	- Type: Case Study

## Additional Notes

OpenSTEF originated at Alliander to address an acute operational need: the Netherlands faces severe grid congestion, with transmission capacity unavailable or under congestion management across most of the country for both consumption and generation connections. Forecasting is the prerequisite for all market-based congestion management approaches — operators must predict overloads before they occur to activate flexibility through bilateral agreements, redispatch markets, or curtailment. This regulatory and operational context (particularly relevant in the Netherlands but increasingly across Europe) is the primary adoption driver.

The project's architecture separates the core ML library (`openstef`) from the database connector (`openstef-dbc`) and a reference implementation (`openstef-reference`) that includes database schemas, a Grafana dashboard, and deployment tooling. This modularity allows adopters like Sigholm to embed OpenSTEF's forecasting engine into their own platforms while using entirely different data infrastructure and domain applications. All components are licensed under MPL-2.0.
