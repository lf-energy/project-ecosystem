# VAREN

**Last Updated:** 2026-09-22

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

- LF Energy webpage: TODO: not yet published
- Website: TODO: none yet
- Code: TODO: not yet public; initial release planned following Sandbox acceptance
- Documentation: TODO: none yet
- Calendar:
- LinkedIn:
- Community:
	- Mailing List:
	- Slack:
- LFX Insights:
- Other:
	- TAC proposal: https://github.com/lf-energy/tac/issues/764

## Description

Python library to extract actionable intelligence from mobile LiDAR point clouds for distribution networks.

## Overview

Many utilities already collect mobile LiDAR (laser scans from vehicle-mounted survey units) of their distribution networks, but turning raw point clouds into usable asset and vegetation data is still largely manual. VAREN (Vegetation and Asset Recognition for Electrical Network) automates that interpretation. Its initial use case is vegetation management: per the project's TAC presentation, vegetation accounts for 45% of outages on the Hydro-Québec network.

VAREN is organized as four algorithms that run in sequence. A neural network labels each point in the cloud as a pole, wire, transformer, vegetation, building, or other object, and distinguishes medium-voltage, low-voltage, and telecom lines. A reconstruction algorithm models power line geometry across gaps where obstructions or low point density leave the scan incomplete. A third algorithm extracts poles and spans to rebuild the physical network layout from the labeled scan, without relying on existing GIS records. The fourth detects vegetation encroaching on spans and produces risk zones and pruning work orders. Outputs are intended to feed GIS and enterprise asset management systems.

The project was developed by the Hydro-Québec research institute. The open source code has not yet been released; the project plans to publish the four algorithms, documentation, and a sample LiDAR dataset in stages through 2027.

## Technical Profile

### What It Does

Classifies distribution assets and vegetation in mobile LiDAR point clouds, reconstructs overhead line geometry and the physical network layout (poles and spans), and identifies vegetation encroachment on spans.

### Problem(s) Solved

Replaces manual interpretation of mobile LiDAR with an automated pipeline, giving distribution utilities current asset inventories, corrected GIS data, and prioritized vegetation work from scans they may already be collecting.

### Key Capabilities

- Point-level classification of distribution assets (poles, wires, transformers), vegetation, and other objects, including separation of medium-voltage, low-voltage, and telecom lines
- Reconstruction of overhead line geometry where the scan is obstructed or sparse
- Pole and span extraction to rebuild the physical network layout without prior GIS data
- Vegetation encroachment detection with risk-zone identification and automated pruning work orders

### Relevant Standards

None identified.

## Grid Context

### Grid Segment

Distribution

### Function

Planning & Analysis

### Industry Solution Categories

#### Solution Type

- LiDAR Point Cloud Analytics: Classifies mobile LiDAR point clouds into distribution assets and vegetation, and derives line geometry, poles and spans, and vegetation encroachment from the labeled data.

#### Component of

- Vegetation Management System: Provides the encroachment detection, risk-zone identification, and pruning work orders that a utility vegetation management program plans and schedules work from.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** Yes
- **Deliverable Type:** Software

## Related Projects

None. No LF Energy projects currently have documented technical integration, shared data flows, or complementary workflows with VAREN. Revisit once code is released.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Organizations

- Hydro-Québec (utility, Canada; project lead and sole contributor to date)

## Learn More

- [VAREN TAC proposal (lf-energy/tac#764)](https://github.com/lf-energy/tac/issues/764) (submitted under the project's former name, RAVEN)
	- Date: 2026-03-03
	- Type: TAC Proposal
- [VAREN: Vegetation and Asset Recognition for Electrical Network (LF Energy TAC presentation)](https://github.com/lf-energy/tac/blob/main/meetings/2026/2026-07-21/RAVEN_TAC_Project_Contribution_Proposal.pdf)
	- Date: 2026-07-21
	- Type: Presentation

## Additional Notes


