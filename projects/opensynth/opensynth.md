# OpenSynth

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

- LF Energy webpage: https://lfenergy.org/projects/opensynth/
- Website: https://www.centrefornetzero.org/impact/synthetic-smart-meter-data
- Code: https://github.com/OpenSynth-energy
- Documentation:
- Calendar: https://zoom-lfx.platform.linuxfoundation.org/meetings/opensynth?view=month
- LinkedIn:
- Community:
	- Mailing List:
	- Slack: https://lfenergy.slack.com/archives/C09SF8UBUE9
- LFX Insights: https://insights.linuxfoundation.org/project/opensynth
- Other:
	- HuggingFace: https://huggingface.co/OpenSynth
	- PyPi: https://pypi.org/project/opensynth-energy/

## Description

Community-driven repository of synthetic energy datasets, generative AI models, and grid topology data for power system research and planning.

## Overview

OpenSynth provides openly accessible energy datasets — both AI-generated synthetic data and grid topology data — along with the generative models and evaluation tools used to produce and validate them. The project has two workstreams. The first generates synthetic household-level electricity consumption profiles using generative AI models trained on real smart meter data, producing half-hourly load profiles conditioned on household attributes such as property type, energy efficiency rating, and low carbon technology ownership (heat pumps, EVs, solar PV). The second, D-GITT (Detailed Grid Inner Topology Time-series), publishes topology data from RTE's French transmission network — approximately 7,000 nodes covering 63 kV to 400 kV — at 5-minute intervals, in XIIDM format compatible with PowSyBl.

Granular household-level demand data is essential for grid planning, state estimation, and demand modeling, but access to real smart meter data is severely restricted by privacy regulations and consent requirements. Existing alternatives — aggregated datasets, anonymized samples, or standard load profiles — are either too coarse, too small, unrepresentative, or still carry re-identification risk. Synthetic smart meter data offers a privacy-preserving alternative: AI-generated profiles that replicate the statistical properties and consumption patterns of real data without being attributable to any individual. On the transmission side, realistic grid topology data at the node-breaker level has historically been unavailable for research — most publicly available test cases are simplified models that do not reflect the complexity of real networks. D-GITT addresses this by publishing detailed topology from the French transmission network.

OpenSynth is used by researchers, grid operators, and innovators who need realistic energy data for model development, scenario analysis, and algorithm validation. Liander (a Dutch DSO) is exploring how synthetic demand data could serve as pseudomeasurements in low-voltage state estimation, where grid measurements are sparse. Contributors from TU Delft have added cleaned historical consumption datasets covering the UK, Netherlands, Germany, and Australia. The D-GITT datasets are designed for developing AI and optimization models for power system analysis.

## Technical Profile

### What It Does

Provides generative AI models that produce synthetic household electricity consumption profiles, and hosts openly accessible grid topology and demand datasets.

### Problem(s) Solved

Gives grid planners and researchers access to granular, household-level demand data without the privacy restrictions, consent barriers, and access fees that limit use of real smart meter data. Provides realistic transmission grid topology data at the node-breaker level for power system research — replacing simplified test cases that do not reflect real-world network complexity.

### Key Capabilities

- Synthetic household load profile generation conditioned on user-specified attributes: property type, energy efficiency rating, LCT ownership (heat pump, EV, solar PV), day of week, month of year, and tariff type
- Multiple generative AI model architectures: Faraday (Variational Autoencoder with Gaussian Mixture Model), EnergyDiff (denoising diffusion probabilistic model), and FlowModel (flow-based model supporting weather-conditioned generation)
- Pre-built synthetic datasets available on HuggingFace for immediate use (10 million profiles in Faraday v4.0, per the white paper)
- D-GITT: three years (2021–2023) of 5-minute-interval topology snapshots from the French transmission network (~7,000 nodes, 4,800+ substations, 7,700+ lines) in XIIDM format
- Privacy attack implementations (membership inference, reconstruction attacks) for evaluating synthetic data privacy properties
- Curated historical consumption datasets from multiple countries (UK, Netherlands, Germany, Australia) for benchmarking and model training

### Relevant Standards

None. OpenSynth is a data and model repository. The D-GITT datasets use PowSyBl's XIIDM data format, but OpenSynth does not implement grid communication or data model standards.

## Grid Context

### Grid Segment

Distribution, Transmission

### Function

Grid Modeling & Simulation

### Industry Solution Categories

#### Solution Type

- Synthetic Load Profile Generation: Provides generative AI models and pre-built datasets of household-level electricity consumption profiles for use in grid planning, state estimation, and demand modeling.
- Grid Test Case / Reference Dataset: Publishes openly accessible grid topology and demand datasets for power system research, model validation, and AI training.

#### Component of

None. OpenSynth provides data resources that feed into planning, forecasting, and state estimation workflows, but is not itself a component of those systems.

### Cross-Cutting Tags

- **Project Intent:** Research
- **AI/ML:** Yes
- **Deliverable Type:** Data

## Related Projects

- **PowSyBl**: Integration — D-GITT datasets use PowSyBl's XIIDM format and are loaded using pypowsybl. PowSyBl is the primary tool for working with D-GITT's transmission topology data.
- **GridFM**: Complementary — GridFM builds AI foundation models for power system analysis and needs large-scale, realistic grid data for training. OpenSynth's D-GITT datasets provide transmission topology at the scale and fidelity needed for foundation model development.

## Maturity & Adoption

### LF Energy Stage

Sandbox

### Deployment Maturity

R&D

### Supporting / Adopting Companies

- Centre for Net Zero (primary developer of Faraday synthetic smart meter model; funded by Octopus Energy Group)
- RTE (French TSO; data provider for D-GITT transmission topology datasets)
- CRESYM (initiated D-GITT workstream)
- Alliander / Liander (exploring synthetic data for distribution state estimation; contributor of EnergyDiff model)
- TU Delft (contributor of cleaned consumption datasets and EnergyDiff model)
- eRoots Analytics (D-GITT contributor)
- Hydro-Québec (community participant)
- University of Oxford (co-author of associated evaluation framework paper)

## Learn More

- [Synthetic Data for Smart Energy](https://cdn.sanity.io/files/lrxd4jqj/production/5e309155a488a8ef5d4e20660e1699440f197744.pdf)
	- Date: 2025-04
	- Type: White Paper
- [Defining 'Good': Evaluation Framework for Synthetic Smart Meter Data](https://arxiv.org/pdf/2407.11785)
	- Date: 2024-07-16
	- Type: Article
- [OpenSynth Expands with D-GITT & RTE7000](https://lfenergysummiteu2025.sched.com/event/26Iyu/opensynth-expands-with-d-gitt-rte7000-open-transmission-system-data-for-grid-aware-innovation-geethu-joseph-cresym-josep-fanals-batllori-eroots-analytics)
	- Date: 2025-09-11
	- Type: Presentation

## Additional Notes

OpenSynth is fundamentally a **data and models** project rather than a software tool — it provides resources that other tools and workflows consume, more analogous to ImageNet for computer vision than to a forecasting engine or planning tool. This distinguishes it from most other LF Energy projects and is important for setting expectations: OpenSynth does not run in a utility's production environment, but its outputs feed into tools that do.

A common misconception is that "synthetic" means "fake" or "less useful than real data." For demand scenario modeling — where the goal is to predict possible future consumption patterns under varying assumptions about LCT adoption, tariffs, and building stock — synthetic data can be more useful than real data because it can be generated at arbitrary scale, conditioned on specific attributes, and shared freely. Synthetic data is not suitable where actual household-specific events need to be understood (e.g., real-time operations, individual billing). The white paper summarizes this distinction: "when seeking to predict possible demand scenarios, synthetic smart meter data will be suitable. However, when seeking to understand actual, household-specific events, only real data will suffice."

The D-GITT workstream represents a significant expansion of OpenSynth's scope from demand-side synthetic data into grid topology data, signaling an ambition to become a broader open data commons for the energy sector. The D-GITT datasets contain topology and structural parameters only — load and generator locations are present but without power flow or injection values — so users must combine them with external sources (Eco2mix, ENTSO-E Transparency Platform) to reconstruct full power flow scenarios.

Privacy is not a theoretical concern for synthetic smart meter data. Even short sequences of half-hourly readings can uniquely identify a household, and household characteristics (income, occupancy, appliances) can be inferred from consumption patterns. An associated academic paper (["Defining 'Good': Evaluation Framework for Synthetic Smart Meter Data,"](https://arxiv.org/pdf/2407.11785) co-authored by Centre for Net Zero with MIT, Oxford, and Georgia Tech) proposes a three-pillar evaluation framework covering fidelity, utility, and privacy. The paper demonstrates that standard privacy tests can give overly optimistic results for smart meter data and recommends explicit privacy attacks on outlier data as a more robust evaluation method. The OpenSynth repository includes implementations of the paper's privacy attack methods (membership inference and reconstruction attacks), though the broader fidelity and utility evaluation framework described in the paper is not implemented in the codebase.
