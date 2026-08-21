# OpenGridFM

**Last Updated:** 2026-08-21

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

- LF Energy webpage: https://lfenergy.org/projects/opengridfm/
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
- LFX Insights: https://insights.linuxfoundation.org/project/gridfm
- Other:
	- Published datasets: https://huggingface.co/gridfm

## Description

Foundation models for power system analysis, and the tooling to build and benchmark them.

## Overview

OpenGridFM builds AI foundation models trained on power grid data, along with the tooling needed to produce them. The approach follows the same pattern as large language models: pre-train a general-purpose model on large volumes of data, then fine-tune it for specific tasks. In OpenGridFM's case, the base data is solved power flow scenarios across diverse grid topologies and operating conditions, and the model architecture is a graph neural network that represents the grid's physical topology — buses as nodes, branches as edges. The fine-tuned model then handles downstream analysis tasks: power flow, optimal power flow, and state estimation.

The project addresses a computational challenge facing power system analysis: as grids grow more complex with distributed generation, variable renewables, and changing demand patterns, the number of scenarios that need to be analyzed grows faster than traditional numerical solvers can handle. Neural solvers offer a path to fast approximate solutions, which makes applications that require evaluating thousands of scenarios in near real time — security-constrained contingency screening being the clearest example — computationally tractable.

The framework is model-agnostic and supports more than one architecture, but the project's flagship model to date is GENCO (GEometric Neural Corrective Optimizer), which handles power flow, optimal power flow, and state estimation within a single architecture and shared grid representation rather than requiring a separate specialized solver for each. Published benchmarks report up to 30x speedups over Newton-Raphson for power flow and up to 85x over interior-point methods for optimal power flow, while recovering the full AC operating state at active power-balance residuals matching those of DC power flow. The project positions GENCO for a hybrid workflow rather than as a replacement for classical solvers: the neural solver evaluates scenarios in bulk and flags suspect cases via residual checks, and conventional solvers produce authoritative results for the cases that matter.

The codebase consists of four repositories: gridfm-datakit, which generates synthetic power flow and optimal power flow training datasets from standard test networks; gridfm-graphkit, which provides the model training, fine-tuning, evaluation, and inference pipeline; gridfm-app-distribution, which adapts the pipeline to distribution network applications; and gridfm-trustlayer, an early-stage uncertainty quantification layer. IBM Research, Hydro-Québec, and Artelys are the primary contributing organizations.

## Technical Profile

### What It Does

Develops graph neural network foundation models for power system analysis tasks such as power flow, optimal power flow, and state estimation, and provides the synthetic dataset generation, training, and benchmarking pipeline used to produce and compare them.

### Problem(s) Solved

Delivers fast approximate solutions to steady-state grid analysis problems, making it practical to evaluate large numbers of scenarios in the time available for operational decisions. Also lowers the barrier to applying modern AI techniques to power system problems by providing ready-made dataset generation and model training pipelines rather than requiring each organization to build this infrastructure independently.

### Key Capabilities

- Unified neural solver (GENCO) covering power flow, optimal power flow, and state estimation from a single architecture and shared grid representation
- Recovers the full AC operating state, including voltage magnitudes and reactive power that DC power flow cannot provide
- Synthetic dataset generation from MATPOWER/PGLib test networks, supporting grids up to 30,000 buses for power flow and 10,000 buses for optimal power flow
- Configurable data perturbations: load scenario variation (global scaling with localized per-bus noise), N-k topology and generator outages, generator cost permutation, and branch admittance scaling
- Data validation and benchmarking tooling, with pre-computed DC power flow and DC optimal power flow baselines and solver runtimes for comparison
- Model training with self-supervised pre-training (masked node feature reconstruction) and supervised fine-tuning for downstream tasks, using heterogeneous graph network and graph transformer architectures with physics-informed decoders
- Distribution network applications via a separate package (gridfm-app-distribution) built on the same training and inference pipeline
- CLI-based workflow for dataset generation, model training, fine-tuning, evaluation, and prediction with YAML configuration and MLflow experiment tracking
- Published open datasets of power flow and optimal power flow scenarios across a range of grid topologies

### Relevant Standards

None. OpenGridFM does not directly implement grid communication or data model standards. It consumes MATPOWER-format network data as input.

## Grid Context

### Grid Segment

Transmission (primary), Distribution (secondary)

### Function

Planning & Analysis

### Industry Solution Categories

#### Solution Type

- Network Analysis: Produces models that solve power flow, optimal power flow, and state estimation, the core computations that network analysis tools perform, using learned models in place of classical numerical methods.

#### Component of

- EMS: Power flow, optimal power flow, and state estimation are the computations an EMS network analysis suite performs, and the project targets contingency screening as a near-term application.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** Yes
- **Modeling & Simulation:** Yes
- **Deliverable Type:** Software, Data

## Related Projects

- **Grid2Op**: Both apply ML to power grid operations but with fundamentally different approaches. Grid2Op provides a simulation environment for developing reinforcement learning control strategies (sequential decision-making); OpenGridFM develops neural solvers for power system analysis tasks (scenario evaluation). They address different aspects of AI for grids and do not directly integrate.
- **OpenSynth**: Complementary — OpenSynth's D-GITT datasets provide transmission topology from the French network at the scale and fidelity needed for foundation model training. OpenGridFM needs large-scale, realistic grid data; OpenSynth publishes it.
- **EnerGNN**: Similar approach, different scope — both are open source toolkits for building GNN models of power grids. OpenGridFM pre-trains and fine-tunes foundation models for power system analysis; EnerGNN is a general-purpose GNN library emphasizing the hyper-heterogeneous multi-graph (H2MG) representation and amortized optimization across analysis and control use cases. They do not directly integrate.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

R&D

### Supporting / Adopting Organizations

- IBM Research
- Hydro-Québec
- Artelys

## Learn More

- [GridFM: enable the emergence of foundation models for power grids](https://tac.lfenergy.org/meetings/2024-10-29/GridFM%20proposal.pdf) (TAC proposal submitted under the project's former name, GridFM)
	- Date: 2024-10-29
	- Type: Presentation
- [A Perspective on Foundation Models for the Electric Power Grid](https://arxiv.org/abs/2407.09434)
	- Date: 2024-12-16
	- Type: Research Paper (published in Joule, Vol. 8, No. 12)
- [gridfm-datakit-v1: A Python Library for Scalable and Realistic Power Flow and Optimal Power Flow Data Generation](https://arxiv.org/abs/2512.14658)
	- Date: 2025-12
	- Type: Research Paper (preprint)
- [OpenGridFM — Incubation stage request](https://github.com/lf-energy/tac/blob/main/meetings/2026/2026-07-21/GridFM%20-%20LFE%20incubation%20request.pdf)
	- Date: 2026-06
	- Type: Presentation (LF Energy TAC)
- [GENCO — A Unified Neural Solver Embedded in a Development Framework for Steady-State Grid Analysis](https://arxiv.org/abs/2608.09921)
	- Date: 2026-08-10
	- Type: Research Paper (preprint)
- [A neural solver for the power grid](https://research.ibm.com/blog/gridfm-neural-solver-power-grid)
	- Date: 2026-08-11
	- Type: Blog Post (IBM Research)

## Additional Notes

**Project rename**: The LF Energy project was renamed from GridFM to OpenGridFM in 2026. Existing repository URLs (github.com/gridfm, gridfm-datakit, gridfm-graphkit) and documentation sites have not yet been migrated and continue to use the original name. Historical materials (the TAC proposal, the Joule paper, and prior presentations) reference the project as GridFM.

**Validation on operational data**: GENCO was evaluated against a full year of SCADA data from Hydro-Québec's 1,200-bus transmission network, in addition to the synthetic PFDelta and OPFData benchmarks. Published benchmark figures (30x over Newton-Raphson for power flow, 85x over interior-point methods for optimal power flow) come from the project's own arXiv preprint and have not been independently reproduced.

**gridfm-trustlayer** applies conformal prediction to produce statistically valid uncertainty intervals on model outputs such as voltage magnitude, voltage angle, and line loading. Its README carries an explicit warning against production use; treat it as early-stage.

All project components are licensed under Apache-2.0. The TAC proposal originally envisioned MPL-2.0 for the model training pipeline (to require contributions back to the core encoder), but the project shipped with Apache-2.0 across all repositories.