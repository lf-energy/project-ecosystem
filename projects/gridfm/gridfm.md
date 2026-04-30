# GridFM

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

- LF Energy webpage: https://lfenergy.org/projects/gridfm/
- Website:
- Code: https://github.com/gridfm
- Documentation:
	- gridfm-datakit: https://gridfm.github.io/gridfm-datakit/
	- gridfm-graphkit: https://gridfm.github.io/gridfm-graphkit/
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/gridfm?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack: https://lfenergy.slack.com/archives/C07U2PCSBN1
	- GridFM Community (independent research forum): https://gridfm.org/
- LFX Insights: https://insights.linuxfoundation.org/project/gridfm
- Other:

## Description

Tooling and infrastructure for developing foundation models for power system analysis.

## Overview

GridFM provides tools for building AI foundation models trained on power grid data. The approach follows the same pattern as large language models in AI: pre-train a general-purpose model on large volumes of data, then fine-tune it for specific tasks. In GridFM's case, the base data is solved power flow scenarios across diverse grid topologies and operating conditions, and the model architecture is a graph neural network that represents the grid's physical topology — buses as nodes, branches as edges. Once pre-trained, the model can be fine-tuned for downstream power system analysis tasks such as approximating power flow solutions, assessing contingencies, and evaluating optimal power flow scenarios.

The project addresses a computational challenge facing power system analysis: as grids grow more complex with distributed generation, variable renewables, and changing demand patterns, the number of scenarios that need to be analyzed grows faster than traditional numerical solvers can handle. Foundation models offer a potential path to fast approximate solutions — once trained, inference is orders of magnitude faster than running a full AC power flow solver — which could enable applications that require evaluating thousands of scenarios in near real time, such as security-constrained contingency screening.

The LF Energy GridFM project originated from the broader GridFM community (gridfm.org), an independent research collaboration spanning utilities, technology companies, national laboratories, and universities — studying the potential of foundation models for the electric grid. The LF Energy project serves as the destination for the community's open source technical outputs. The project currently consists of two components: gridfm-datakit, which generates synthetic power flow training datasets from standard test networks, and gridfm-graphkit, which provides the model training, fine-tuning, and inference pipeline. Hydro-Québec and IBM Research are the founding contributors.

## Technical Profile

### What It Does

Generates synthetic power flow datasets from standard grid test cases and provides tools to pre-train, fine-tune, and run inference with graph neural network foundation models on that data for power system analysis tasks.

### Problem(s) Solved

Provides shared infrastructure for developing AI models that can approximate power system analysis computations, potentially enabling faster-than-real-time evaluation of large numbers of grid scenarios. Lowers the barrier to applying modern AI techniques to power system problems by providing ready-made dataset generation and model training pipelines rather than requiring each organization to build this infrastructure independently.

### Key Capabilities

- Synthetic power flow dataset generation from MATPOWER/PGLib test networks, supporting grids up to 30,000 buses for power flow and 10,000 buses for optimal power flow
- Configurable data perturbations: load scenario variation (global scaling with localized per-bus noise), N-k topology outages, generator cost permutation, and branch impedance scaling
- Graph neural network model training with self-supervised pre-training (masked node feature reconstruction) and supervised fine-tuning for downstream tasks
- Two GNN architectures: GPSTransformer (graph convolution with transformer-style attention) and GNN_TransformerConv (stacked multi-head attention layers)
- CLI-based workflow for dataset generation, model training, fine-tuning, evaluation, and prediction with YAML configuration and MLflow experiment tracking
- Federated learning support planned to enable utilities to contribute to model training without sharing sensitive grid data

### Relevant Standards

None. GridFM is an AI/ML research platform and does not directly implement grid communication or data model standards. It consumes MATPOWER-format network data as input.

## Grid Context

### Grid Segment

Transmission, Distribution

### Function

Grid Modeling & Simulation

### Industry Solution Categories

#### Solution Type

- Power System AI Research Platform: Provides infrastructure for generating synthetic power flow training data and developing graph neural network foundation models that can be fine-tuned for power system analysis tasks.

#### Component of

None. GridFM is a standalone research and development platform. Foundation models developed using GridFM could eventually be embedded within EMS, ADMS, or planning tools, but GridFM itself is not a component of those systems.

### Cross-Cutting Tags

- **Project Intent:** Research
- **AI/ML:** Yes
- **Deliverable Type:** Software

## Related Projects

- **Grid2Op**: Both apply ML to power grid operations but with fundamentally different approaches. Grid2Op provides a simulation environment for developing reinforcement learning control strategies (sequential decision-making); GridFM develops pre-trained foundation models for power system analysis tasks (scenario evaluation). They address different aspects of AI for grids and do not directly integrate.
- **OpenSynth**: Complementary — OpenSynth's D-GITT datasets provide transmission topology from the French network at the scale and fidelity needed for foundation model training. GridFM needs large-scale, realistic grid data; OpenSynth publishes it.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Organizations

- Hydro-Québec
- IBM

## Learn More

- [GridFM: enable the emergence of foundation models for power grids](https://tac.lfenergy.org/meetings/2024-10-29/GridFM%20proposal.pdf)
	- Date: 2024-10-29
	- Type: Presentation
- [A Perspective on Foundation Models for the Electric Power Grid](https://arxiv.org/abs/2407.09434)
	- Date: 2024-12-16
	- Type: Research Paper (published in Joule, Vol. 8, No. 12)

## Additional Notes

**Disambiguating the GridFM community and the LF Energy GridFM project**: "GridFM" refers to two related but distinct entities. The **GridFM community** (gridfm.org) is an independent, IBM-initiated research collaboration that brings together stakeholders from industry, academia, and government to study the potential and impact of foundation models for the electric grid. The community is structured into governance, collaboration, and technology working groups and holds regular workshops. The **LF Energy GridFM project** is the open source code and infrastructure that serves as the destination for the community's technical outputs. The community participant list should not be conflated with the LF Energy project's contributor base — the code repositories are primarily developed by researchers from Hydro-Québec and IBM Research, with a small number of additional contributors.

All project components are licensed under Apache-2.0. The TAC proposal originally envisioned MPL-2.0 for the model training pipeline (to require contributions back to the core encoder), but the project shipped with Apache-2.0 across all repositories.