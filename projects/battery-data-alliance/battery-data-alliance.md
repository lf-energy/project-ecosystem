# Battery Data Alliance

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

- LF Energy webpage: https://lfenergy.org/projects/battery-data-alliance/
- Website: https://batterydataalliance.energy/
- Code: https://github.com/battery-data-alliance
- Documentation:
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/battery-data-alliance?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
	- Discourse: https://bda.discourse.group/
- LFX Insights: https://insights.linuxfoundation.org/project/battery-data-alliance
- Other:

## Description

Shared software standards, data formats, and test equipment interfaces for the battery industry, enabling interoperability across laboratories, vendors, and analytical tools.

## Overview

The Battery Data Alliance (BDA) provides standardized tooling for battery data across the value chain — from cell design and testing through manufacturing and field telemetry. Its flagship deliverable is the Battery Data Format (BDF), an open standard that defines a fixed schema for battery cycling test data with ontology-aligned metadata. BDA also provides Python libraries for programmatic control of battery test cyclers (Maccor and Arbin), data ingestion pipelines for standardizing raw cycler output, and a formal ontology aligned with the BattINFO battery domain ontology.

Battery R&D and manufacturing are data-intensive, but the data ecosystem is fragmented. Each cycler manufacturer produces data in proprietary formats, each lab builds its own schemas and conversion pipelines, and each software tool expects a different input structure. The result is that organizations across the battery industry independently duplicate the same data engineering work — writing parsers, format converters, and equipment interfaces — rather than focusing on battery science and innovation. BDA eliminates this redundant effort by providing shared, vendor-neutral foundations that make battery datasets shareable, reproducible, and compatible across organizations.

BDA's tools are used by battery researchers, cell manufacturers, and testing laboratories. The cycler control libraries (PyMacNet for Maccor, PyCTIArbin for Arbin) enable automated test management and real-time monitoring without manual GUI interaction. The `batterydf` Python package reads raw cycler files, validates and cleans the data, and outputs BDF-compliant datasets. Per the BDF announcement (December 2025), the format is compatible with downstream modeling frameworks including PyBaMM and BattMo. The project has attracted contributions from battery companies and research institutions across North America and Europe.

## Technical Profile

### What It Does

Defines a standard data format for battery cycling test data and provides software libraries for controlling battery test equipment, ingesting raw test data, and producing standardized, ontology-aligned datasets.

### Problem(s) Solved

Eliminates redundant data engineering across the battery industry by providing shared data formats, equipment interfaces, and ingestion tooling. Enables battery R&D teams to focus on cell design and testing rather than building custom parsers and format converters for each combination of cycler, analysis tool, and modeling framework.

### Key Capabilities

- Battery Data Format (BDF): fixed table schema for time-series cycler data with required columns (test time, voltage, current), recommended columns (timestamp, cycle count, step count, temperature), and 20+ optional columns for capacity, energy, resistance, and multi-point temperature measurements
- Ontology alignment with BattINFO (extending Battery2030+ and BIG-MAP), enabling semantic interoperability and machine-readable metadata via JSON-LD context and CSVW table schemas
- Programmatic control of Maccor cyclers (PyMacNet) including real-time monitoring, direct current control, database logging, and batch test automation across multiple channels
- Programmatic control of Arbin cyclers (PyCTIArbin) via the Console TCP/IP Interface, with similar real-time monitoring and test management capabilities
- Data ingestion and validation via the `batterydf` Python package, which reads raw cycler files (including Neware `.nda/.ndax`), validates data quality, applies cleaning (time correction, outlier handling), and outputs BDF-compliant datasets
- Schema Management Service for standardizing raw battery cycling data from multiple sources into validated, schema-aligned dataframes
- Compatibility with downstream modeling frameworks including PyBaMM and BattMo, with conversion tooling (BDX) for PyProBE access (per BDF announcement, December 2025)
- AmpLabs (community-contributed): worked examples and how-to guides for battery data analysis, with a managed cloud version at amplabs.ai
- Mock test servers (MaccorSpoofer, ArbinSpoofer) for development and testing without physical hardware

### Relevant Standards

None. BDA defines its own data format standard (BDF) rather than implementing an existing industry standard. The BDF ontology extends the BattINFO domain ontology and uses IUPAC/SI notation conventions, but these are scientific naming conventions rather than formal standards in the IEC/IEEE/ISO sense.

## Grid Context

BDA targets the battery R&D and manufacturing value chain rather than grid operations. The categories below are adapted accordingly.

### Grid Segment

Not directly applicable. BDA operates upstream of grid deployment, in battery R&D, testing, and manufacturing. Batteries developed using BDA tooling may ultimately be deployed across all grid segments, but the project itself does not operate within any grid segment.

### Function

Interoperability & Data

### Industry Solution Categories

#### Solution Type

- Battery Test Data Platform: Provides a standardized data format, test equipment interfaces, and data ingestion tooling for battery cycling test data, enabling interoperability across laboratories, cycler vendors, and analytical tools.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Specification

## Related Projects

None currently identified within the LF Energy ecosystem. BDA operates in the battery R&D domain, which is distinct from the grid operations and planning focus of most LF Energy projects. While battery storage is a key grid asset, there is no direct technical integration between BDA's test data tooling and other LF Energy projects' grid management capabilities.

<!-- Future consideration: If FlexMeasures or other projects develop battery degradation modeling that consumes standardized cell test data, a genuine technical relationship could emerge. -->

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- AmpLabs (contributed battery data analysis examples and tooling; AmpLabs founder Gabe Hege serves as BDA chairperson)
- BattGenie (donated PyCTIArbin and PyMacNet cycler control libraries to BDA)
- Admiral Instruments (donated Squidstat Cycler test hardware)
- SINTEF (battery ontology work; BattINFO alignment)
- ionworks (battery simulation)
- M.A.P.L.E. Lab — Modeling, Analysis and Process control Laboratory for Electrochemical systems (donated lab space and volunteer access)
- Faraday Institution (PyProBE validation; funding PyProBE modification for BDF alignment; as of December 2025)
- Microsoft (contributing reference battery dataset in BDF format; as of December 2025)
- Ohm (YC W23) (free web-based converter for commercial cycler formats to BDF; as of December 2025)
- Empa, ETH Zurich, EPFL (contributed, with SINTEF, the largest open battery dataset: 199 coin cells, 1,000 cycles each; as of December 2025)
- Imperial College London (PyProBE development; as of December 2025)

## Learn More

- [Challenges and Opportunities Working with Battery Data](https://lfenergysummit2024.sched.com/event/1ehID/challenges-and-opportunities-working-with-battery-data-gabe-hege-amplabs)
	- Date: 2024-09-05
	- Type: Presentation
- [LF Energy Battery Data Alliance Announces the Battery Data Format (BDF): A New Open Standard for Battery Data Interoperability](https://batterydataalliance.energy/lf-energy-battery-data-alliance-announces-the-battery-data-format-bdf-a-new-open-standard-for-battery-data-interoperability/)
	- Date: 2025-12-22
	- Type: Press Release

## Additional Notes

BDA is unique within the LF Energy portfolio in that it does not target grid operations or planning. It addresses the battery value chain *upstream* of grid deployment — the R&D, testing, and manufacturing stages where cells are designed, characterized, and validated. The connection to the energy transition is indirect but fundamental: better battery data infrastructure accelerates the development of the storage technologies that the grid depends on.

The project is also structurally distinct from most LF Energy projects in that it combines a data standard (BDF) with software tooling in a single initiative. The standard defines how battery test data should be structured; the software tools implement it. This is more analogous to a standards body with a reference implementation than to a typical open source software project.

The competitive landscape is fragmented across proprietary solutions: each cycler manufacturer (Maccor, Arbin, Neware, etc.) ships its own data format and software. Commercial battery data platforms exist but use proprietary schemas. BDA provides the vendor-neutral alternative — shared data infrastructure that any organization can adopt and extend.