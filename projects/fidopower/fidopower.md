# FIDOpower

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

- LF Energy webpage: https://lfenergy.org/projects/fidopower/
- Website:
- Code: https://github.com/fidopower/
- Documentation:
- Calendar:
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/fidopower
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/fidopower
- Other:

## Description

Interactive notebook-based workflows for power system analysis, including optimal powerflow, capacity sizing, and network visualization.

## Overview

FIDOpower provides browser-based, interactive analysis workflows for power system studies. Built on Marimo — a reactive Python notebook environment — it packages common distribution planning analyses (optimal powerflow, generator and capacitor sizing and placement, network visualization) into self-contained notebooks that engineers can run without assembling custom scripts or managing complex toolchains. Analyses currently accept grid models in Arras (GridLAB-D) JSON format.

The project originated as a modernization of OpenFIDO, a data and model processing framework funded by the California Energy Commission (EPC 17-047) for facilitating power system data exchange across utilities and researchers. OpenFIDO ran analysis pipelines as containerized Docker workflows with a custom web UI and AWS backend. FIDOpower replaces that architecture with Marimo notebooks, which simplify deployment (no custom infrastructure required), provide reactive computation (results update automatically when inputs change), and use Python as the native development language.

FIDOpower is in early development with limited activity. Two analysis notebooks are currently available: an optimal sizing and placement tool and a grid model viewer. The OpenFIDO pipeline library (hosting capacity, electrification, tariff design, resilience, load shapes) has not yet been ported to the new platform.

## Technical Profile

### What It Does

Provides interactive notebook-based workflows for distribution system analysis, currently focused on optimal powerflow and capacity sizing/placement studies.

### Problem(s) Solved

Provides ready-to-use analysis workflows for common distribution planning studies, reducing the effort required to set up and run analyses like optimal capacity sizing without building custom toolchains.

### Key Capabilities

- **Optimal powerflow**: Computes economically optimal generation dispatch subject to power balance, voltage, and thermal constraints
- **Optimal sizing and placement**: Identifies lowest-cost configurations for generators, capacitors, and synchronous condensers to meet demand requirements
- **Network visualization**: Graphical display of grid models showing nodes, loads, generation, and current flows
- **Interactive parameter exploration**: Browser-based interface with adjustable inputs (voltage tolerances, cost parameters, demand safety margins) and reactive result updates

### Relevant Standards

None.

## Grid Context

### Grid Segment

Distribution

### Function

Grid Modeling & Simulation

### Industry Solution Categories

#### Solution Type

- Distribution Analysis Tool: Provides interactive, notebook-based workflows for distribution system analysis studies such as optimal powerflow and capacity planning.

#### Component of

- Distribution Planning: Supplies ready-to-use analysis workflows for distribution planners evaluating capacity adequacy and optimal equipment placement.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **Arras**: FIDOpower's analysis workflows consume grid models in Arras (GridLAB-D) JSON format as their primary input. Arras produces the distribution network models; FIDOpower provides interactive analysis workflows that operate on those models using its own analysis engine (PyPOWER).

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Companies

<!-- TODO: Confirm contributing organizations. The project shares lineage with Arras (same CEC/SLAC origins). Eudoxys Sciences may be involved but is not confirmed as a FIDOpower contributor. -->

## Learn More

<!-- TODO: No presentations or external content identified for FIDOpower specifically. Check future LF Energy Summit schedules. -->

## Additional Notes

FIDOpower is a modernization of OpenFIDO (https://github.com/openfido), which was originally funded by the California Energy Commission. The project has very low contributor activity — LFX Insights shows 0 active contributors in the most recent quarter with single-organization dependency. The OpenFIDO pipeline library has not yet been ported to the Marimo-based architecture, so the project's current scope is limited to two early-stage notebooks.