# RTDIP

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

- LF Energy webpage: https://lfenergy.org/projects/real-time-data-ingestion-platform-rtdip/
- Website: https://www.rtdip.io/
- Code: https://github.com/rtdip
- Documentation: https://www.rtdip.io/
- Calendar:
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/rtdip
- Other:

## Description

Cloud-native time-series data platform for ingesting, transforming, and querying high-volume sensor and meter data at scale.

## Overview

RTDIP (Real-Time Data Ingestion Platform) is a time-series data platform that ingests, transforms, and serves high-volume operational data from sensors, meters, and external sources. It addresses similar use cases to traditional industrial data historians but with a modern, cloud-native architecture built on Apache Spark and Delta Lake. RTDIP provides a Python SDK, REST APIs, and ODBC connectors for querying data, making it accessible from common analytics tools such as Power BI, Grafana, and Jupyter notebooks.

Energy companies managing large fleets of generation assets face a common data infrastructure challenge: plant instrumentation, environmental monitoring, and performance tracking systems produce massive volumes of time-series data that must be collected, quality-checked, and made available for analysis. Traditional on-premises data historians handle this at individual plant or site level, but struggle with cloud-scale aggregation across geographically distributed assets. RTDIP provides a cloud-native alternative that can consolidate time-series data from multiple sources — plant control systems (via OPC UA), smart meters, weather services, and wholesale market feeds — into a unified data layer with built-in data quality checks and standardized query interfaces.

RTDIP originated at Shell, where it manages time-series data from over 3 million sensors across global operations. The platform's energy-specific data models for process control data (PCDM), meter data (MDM), and weather data reflect this industrial energy heritage.

## Technical Profile

### What It Does

Ingests time-series data from industrial sensors, meters, weather services, and market data feeds; applies data quality transformations; and provides a unified query layer for analytics and operational applications.

### Problem(s) Solved

Enables energy companies to consolidate high-volume time-series data from distributed generation assets and external sources into a single cloud-based platform, replacing the need for site-by-site on-premises data historians. Provides standardized data quality processing (validation, anomaly detection, gap filling) and query interfaces that allow operations and analytics teams to access clean, consistent data without building custom data pipelines.

### Key Capabilities

- Scalable ingestion from streaming and batch sources including OPC UA/Publisher, IoT Hub, Kafka, EventHub, and cloud storage
- Energy-specific data source connectors for US ISO market data (MISO, PJM, CAISO, ERCOT), ENTSO-E, ECMWF weather, and The Weather Company
- Three standardized domain data models: Process Control (PCDM) for sensor data, Meters (MDM) for smart meter and market data, and Weather for forecast data
- Data quality pipeline with validation, duplicate detection, flatline filtering, K-sigma anomaly detection, and missing value imputation
- Time-series query engine with resampling, interpolation, time-weighted averages, circular averages (for directional data), and aggregations
- Multiple access methods: Python SDK, REST APIs, ODBC connectors (via pyodbc and turbodbc) for integration with BI and analytics tools
- Pipeline framework (Jobs → Tasks → Steps) with configurable sources, transformers, and destinations
- Multiple runtime environments: Databricks (primary), Apache Spark (PySpark), and pure Python

### Relevant Standards

None. RTDIP parses OPC UA data formats as an ingestion source but does not implement the OPC UA protocol itself. It does not directly implement grid communication or data model standards.

## Grid Context

### Grid Segment

Generation

### Function

Interoperability & Data

### Industry Solution Categories

#### Solution Type

- Process Data Platform: Provides cloud-native infrastructure for ingesting, quality-checking, and serving high-volume process and sensor data from generation assets and energy data sources, addressing similar use cases to traditional industrial data historians.

#### Component of

- Industrial Data Historian: Provides the cloud-native data ingestion, storage, and query layers of a modern historian architecture, replacing the data collection and retrieval functions of traditional on-premises historians.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

None identified. RTDIP operates as data infrastructure that does not have direct code-level integration points with other LF Energy projects. While RTDIP includes parsers for data formats used by other platforms (e.g., EdgeX, Fledge), these are format-level compatibility, not coordinated integration.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

Production (in industrial energy operations; no confirmed utility grid deployments)

### Supporting / Adopting Companies

- Shell (primary developer; production deployment managing 3M+ sensors across global operations)
- Databricks (technology partner and backer)
- Innowatts (backer)

## Learn More

- [Beyond the Traditional Data Historian](https://www.rtdip.io/blog/2023/11/27/beyond-the-traditional-data-historian/)
	- Date: 2023-11-27
	- Type: Blog Post
- [RTDIP Ingestion Pipelines](https://www.rtdip.io/blog/2023/02/24/rtdip-ingestion-pipelines/)
	- Date: 2023-02-24
	- Type: Blog Post
- [Energy Forecasting: Utilising the Power of Tomorrow's Data](https://www.rtdip.io/blog/2024/04/08/energy-forecasting-utilising-the-power-of-tomorrows-data/)
	- Date: 2024-04-08
	- Type: Blog Post
- [Enhancing Data Quality in Real-Time: Our Experience with RTDIP and the AMOS Project](https://www.rtdip.io/blog/2025/02/05/enhancing-data-quality-in-real-time-our-experience-with-rtdip-and-the-amos-project/)
	- Date: 2025-02-05
	- Type: Blog Post

## Additional Notes

RTDIP originated in the oil and gas industry, where the operational data challenges — high-volume sensor ingestion, data quality at scale, multi-source data consolidation — are directly analogous to those faced in power generation operations. The platform's process control data model (PCDM) reflects this industrial heritage, targeting sensor types (temperature, pressure, flow) common to both thermal generation and upstream energy operations. The meter data model (MDM) and market data connectors extend RTDIP's relevance to the electricity sector, though the primary production deployment remains in industrial energy operations.

While RTDIP supports multiple runtime environments (Databricks, Apache Spark, pure Python), the primary deployment target and most mature integration path is Databricks. The deep Databricks integration — Delta Lake storage, Databricks SQL connectors, Databricks Workflows orchestration — means that adopters not already using Databricks would face additional platform adoption considerations. Apache Airflow and Dagster are supported as alternative orchestration options, though the Airflow integration is specifically designed to trigger Databricks-deployed jobs rather than orchestrating non-Databricks runtimes. Energy companies evaluating RTDIP should consider alignment with their existing cloud data platform strategy.

The project is licensed under Apache 2.0 and distributed as the `rtdip-sdk` package on PyPI.