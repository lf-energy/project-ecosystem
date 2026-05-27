# LF Energy Project Taxonomy

**Last Updated:** 2026-05-27

## Contents

- [Purpose](#purpose)
- [Grid Segment](#grid-segment)
- [Function](#function)
  - [Planning & Analysis](#planning--analysis)
  - [Operations](#operations)
  - [Markets & Programs](#markets--programs)
  - [Outside the Grid Taxonomy](#outside-the-grid-taxonomy)
- [Placement Principles](#placement-principles)
- [Grid Segment x Function Matrix](#grid-segment-x-function-matrix)
- [Industry Solution Categories](#industry-solution-categories)
- [Cross-Cutting Tags](#cross-cutting-tags)
  - [Project Intent](#project-intent)
  - [AI/ML](#aiml)
  - [Modeling & Simulation](#modeling--simulation)
  - [Deliverable Type](#deliverable-type)
  - [Cross-Cutting Tag Summary](#cross-cutting-tag-summary)
- [Maintaining the Taxonomy](#maintaining-the-taxonomy)

## Purpose

This taxonomy provides a framework for categorizing and navigating LF Energy's project portfolio. It is designed for **discovery** — helping the LF Energy community (utility engineers, vendors, researchers) find relevant projects using vocabulary the industry already uses.

The taxonomy uses two primary dimensions (**Grid Segment** and **Function**) plus a supplementary navigation layer (**Industry Solution Categories**) and a set of **cross-cutting tags**. Together these provide multiple entry points into the portfolio depending on how a visitor thinks about the problem they're trying to solve.

## Grid Segment

Grid Segment describes **where on the energy system** a project operates. These are physical segments of the energy value chain, listed in order from power production to consumption.

| Segment | Description |
|---------|-------------|
| **Generation** | Power production assets and associated systems — power plants, wind farms, solar farms, hydropower facilities |
| **Transmission** | Bulk power delivery network — high-voltage lines, substations, and interconnections managed by TSOs, RCCs, and ISOs/RTOs |
| **Distribution** | Local power delivery network — medium- and low-voltage infrastructure managed by DSOs, delivering power to end customers, including utility-owned metering infrastructure |
| **Behind-the-meter** | Customer-sited and customer-facing systems on the customer side of the utility meter — DER, EV charging, microgrids, home/building energy management, aggregator platforms that orchestrate customer assets |

Projects may be tagged with multiple segments when they genuinely operate across boundaries; indicate primary vs. secondary where there is a clear distinction. Some projects sit outside the grid taxonomy entirely (see [Outside the Grid Taxonomy](#outside-the-grid-taxonomy)). For ambiguous placements, see [Placement Principles](#placement-principles).

## Function

Function describes **what kind of grid activity a project supports**. The discriminator is the *activity content* of the project — what the project IS, what work it enables — not the project's deployment maturity, deliverable format, or downstream consumer.

**Test:** "What kind of work does this project enable — operating the grid, analyzing it, or coordinating market/program participation?"

A project's deployment maturity (R&D, pilot, production) and its intent (Applied vs. Research) are captured separately as cross-cutting tags. A mature research platform whose content IS an operational system (e.g., a WAMPAC research testbed) is Operations + Research-intent, not P&A.

### Planning & Analysis

Software whose content supports analytical activities — modeling, simulation studies, forecasting, scenario analysis, risk and reliability modeling, data generation for study. These projects produce insight, models, forecasts, or data artifacts that humans or downstream systems consume to inform decisions. They do not act on real-time grid state.

| Project | Grid Segment | What it does |
|---------|-------------|-------------|
| PowSyBl | Transmission | Network modeling, power flow, contingency analysis, capacity calculation |
| Dynawo | Transmission | Dynamic and transient power system simulation |
| GridFM | Transmission, Distribution | Foundation models for power system analysis |
| Power Grid Model | Distribution | High-performance steady-state distribution network analysis |
| Arras | Distribution | Agent-based distribution system scenario planning |
| FIDOpower | Distribution | Interactive notebook-based distribution analysis workflows |
| OpenSynth | Transmission, Distribution | Synthetic grid topology and smart meter datasets for research and modeling |
| OpenSTEF | Distribution | Short-term (up to 48-hour) energy load forecasting |
| covXtreme | Generation | Statistical modeling of extreme environmental events for offshore wind and infrastructure design |

### Operations

Software whose content supports operating, controlling, monitoring, dispatching, or simulating-for-operational-purposes the grid or grid-edge assets. Includes applied operational systems (DERMS, ADMS, control room platforms, AMI head-ends, device firmware, semantic/data-carrying interoperability middleware) and research-grade platforms whose content IS an operational system (RL training environments, WAMPAC testbeds). Research intent is a separate cross-cutting tag.

**Subcategory: Substation Digitalization** — Tools for modernizing substation protection, automation, and control systems. In project overviews, indicated as `Operations — Substation Digitalization`.

**Subcategory: EV Charging** — Charging infrastructure firmware and management systems. In project overviews, indicated as `Operations — EV Charging`.

| Project | Subcategory | Grid Segment | What it does |
|---------|------------|-------------|-------------|
| RTDIP | | Generation | Cloud-native time-series data platform for sensor and meter data at scale |
| OperatorFabric | | Transmission, Distribution | Operator notification and coordination |
| SOGNO | | Distribution | Distribution grid monitoring, state estimation, and automation |
| GXF | | Distribution | IoT field device communication and management |
| TROLIE | | Transmission | Transmission facility ratings exchange (FERC Order 881) |
| SEF | | Distribution | Semantic interoperability middleware for DSO–DER/customer data exchange |
| Grid2Op | | Transmission | Simulation environment for developing automated grid control strategies |
| p-SWAMP | | Transmission | Wide-area monitoring, protection, and control R&D platform |
| Hyphae | | Behind-the-meter | DC microgrid autonomous energy sharing |
| ORES | | Behind-the-meter | Modular, plug-and-play residential DER systems |
| AINETUS | | Transmission | AI-based operator decision support: RL-based remedial action recommendations, explainability, and human-AI interaction |
| SEAPATH | Substation Digitalization | Transmission, Distribution | Virtualization platform for protection, automation, and control applications |
| CoMPAS | Substation Digitalization | Transmission, Distribution | Vendor-neutral IEC 61850 substation configuration tooling |
| GEISA | | Distribution | Grid edge application interoperability for smart meters and DA controllers |
| EVerest | EV Charging | Behind-the-meter | Standards-compliant EV charger firmware stack |
| CitrineOS | EV Charging | Behind-the-meter | OCPP-based charging station management system |

### Markets & Programs

Software that encodes market mechanisms, program structures, or commercial coordination — wholesale and ancillary markets, flexibility markets, demand response programs, customer enrollment, and the measurement & verification of program participation. "Markets" covers price-clearing mechanisms; "Programs" covers structured tariff-or-incentive-based participation mechanisms with defined enrollment, measurement, and settlement.

| Project | Grid Segment | What it does |
|---------|-------------|-------------|
| RTC-Tools | Generation | Multi-asset dispatch optimization (hydropower, BESS, multi-market) |
| Shapeshifter | Distribution | Flexibility trading protocol (USEF) between grid operators and aggregators |
| OpenLEADR | Distribution | Automated demand response communication (OpenADR) |
| CDS Customer Data | Distribution, Behind-the-meter | Standardized APIs for authorized third-party access to customer energy data |
| CDS Registration | Distribution | Utility API discovery, registration, and secure connectivity |
| URPX | Distribution, Behind-the-meter | Machine-readable format for utility rate plan data |
| FlexMeasures | Behind-the-meter | Aggregator-side optimization for customer-sited energy assets |
| OpenDSM | Behind-the-meter | Demand-side program measurement and verification |

### Outside the Grid Taxonomy

This taxonomy is organized around the grid value chain. Some LF Energy projects address energy industry problems that sit outside that value chain and are listed here rather than forced into ill-fitting grid categories.

| Project | Rationale |
|---------|-----------|
| Battery Data Alliance | Shared software standards and data formats for battery testing — addresses the battery R&D, manufacturing, and lab software ecosystem rather than grid operations |

**Watch:** An asset management function may emerge as anticipated 2026 project additions land (Raven, ReLife — reliability modeling, asset renewal optimization, LiDAR-based asset condition analytics). Revisit when the cluster has more than one inhabitant.

## Placement Principles

When a project could reasonably fit in more than one segment or function, these principles guide placement.

**Activity-content principle (function).** A project's function is determined by the kind of grid activity its content supports, not by its maturity or audience. A research-grade RL environment whose content is an operational decision-making system (Grid2Op) is Operations + Research-intent, not P&A. A forecasting tool that feeds operations (OpenSTEF) is still P&A — its activity content is analytical.

**Strategic-deployer principle (segment).** Place by the segment of the entity that *owns and deploys* the platform, not by where data flows or where code runs. A DSO-deployed DERMS that orchestrates BTM assets is Distribution; an aggregator platform that participates in DSO-run markets is BTM.

**Meter-data ownership (segment).** Smart meter data is utility-owned distribution infrastructure. Projects whose content is meter data (e.g., OpenSynth's synthetic meter datasets) sit in Distribution by ownership, not BTM. This distinguishes data products from BTM platforms that consume meter data (FlexMeasures, OpenDSM).

**Encoding-vs-carrying (Operations vs. M&P).** Protocols and middleware that *encode* market mechanisms or program structures (OpenADR, USEF/Shapeshifter, CDS family, URPX) belong to Markets & Programs. Protocols and middleware that *carry* operational data — even in market-adjacent contexts — belong to Operations (CUPID, SEF, GEISA).

### Notable borderline placements

- **SEF, CUPID, GEISA** — Operations (carry operational data) rather than M&P.
- **TROLIE** — Operations / Transmission. Ratings exchange feeds both reliability and market decisions, but the project's activity content is operational data exchange.
- **CDS family, URPX** — M&P / Distribution (with BTM secondary where customer access is part of the contract). Utilities operate the publishing platforms; the encoded content is program/tariff structure and customer enrollment.
- **OpenSynth** — P&A / Transmission, Distribution. Includes synthetic transmission topology and synthetic meter datasets; meter-data ownership keeps the meter side in Distribution.
- **FlexMeasures, OpenDSM** — M&P / BTM. Aggregator-deployed platforms that orchestrate or measure customer-side participation in DSO-run programs.
- **Hyphae, ORES, EVerest, CitrineOS** — Operations / BTM. Operational systems for BTM assets, not market participation platforms.
- **Grid2Op, p-SWAMP** — Operations / Transmission + Research-intent. Content is an operational system at research maturity.
- **OpenSTEF** — P&A / Distribution. Forecasting is analytical even when its output feeds operations.
- **SOGNO** — Operations / Distribution primary, with secondary value in P&A (DPsim, CIM tooling).

## Grid Segment x Function Matrix

|  | **Generation** | **Transmission** | **Distribution** | **Behind-the-meter** |
|---|---|---|---|---|
| **Planning & Analysis** | covXtreme | PowSyBl, Dynawo, GridFM, OpenSynth | Power Grid Model, Arras, FIDOpower, GridFM, OpenSynth, OpenSTEF | |
| **Operations** | RTDIP | OperatorFabric, SEAPATH⁺, CoMPAS⁺, TROLIE, Grid2Op°, p-SWAMP°, AINETUS | OperatorFabric, SOGNO, GXF, SEAPATH⁺, CoMPAS⁺, GEISA, SEF | Hyphae, ORES, EVerest⁺, CitrineOS⁺ |
| **Markets & Programs** | RTC-Tools | | Shapeshifter, OpenLEADR, CDS Registration, CDS Customer Data, URPX | FlexMeasures, OpenDSM |

⁺ = subcategory (Substation Digitalization or EV Charging)
° = Research intent

**Not shown:** Battery Data Alliance is listed in [Outside the Grid Taxonomy](#outside-the-grid-taxonomy).

## Industry Solution Categories

Industry Solution Categories describe the **recognized utility systems** that a project contributes to. These are supplementary to the primary taxonomy — they provide an additional navigation path for utility engineers who think in terms of the systems they buy and build.

Not all projects map to an Industry Solution Category, and that's fine. These categories work best for projects that are components of established utility systems.

### How to Use

Each project overview includes an "Industry Solution Categories" section with two subsections:
- **Solution Type:** What the project fundamentally IS as a solution category (e.g., "Network Analysis", "Load Forecasting", "Virtualization Platform")
- **Component of:** The broader utility systems where this project serves as a building block (e.g., EMS, ADMS, DERMS)

### Common Industry Solution Categories

| Industry Solution | Description | Projects |
|------------------|-------------|----------|
| **EMS** | Energy Management System — transmission grid operations | PowSyBl, Dynawo, TROLIE, AINETUS |
| **ADMS** | Advanced Distribution Management System — distribution grid operations | SOGNO, Power Grid Model, OpenSTEF |
| **DERMS** | Distributed Energy Resource Management System — DER coordination | FlexMeasures, OpenLEADR, Shapeshifter, SEF |
| **Digital Substation** | Digitalized protection, automation, and control | SEAPATH, CoMPAS |
| **EV Charging Infrastructure** | Charging hardware and management platforms | EVerest, CitrineOS |
| **AMI** | Advanced Metering Infrastructure — smart metering and edge | GXF, GEISA |
| **Distribution Automation** | Intelligent monitoring and control of distribution grid assets | GEISA |
| **Network Planning** | Grid reinforcement and capacity studies | Arras, Power Grid Model, PowSyBl |
| **WAMPAC** | Wide Area Monitoring, Protection, and Control | p-SWAMP |
| **Market Management** | Wholesale and flexibility market systems | Shapeshifter, RTC-Tools |

Not all projects appear in this table. Projects that are standalone tools or that occupy emerging categories without established utility system names may not have a Component of mapping.

## Cross-Cutting Tags

Cross-cutting tags provide additional dimensions for filtering and navigating the portfolio beyond Grid Segment and Function.

### Project Intent

Describes **why the project exists** — whether it produces outcomes that affect real grid decisions and infrastructure, or exists to advance knowledge and enable experimentation.

| Value | Description |
|-------|-------------|
| **Applied** | The project aims to be used in planning, operating, or managing real energy systems. Includes everything from control room tools to planning study software to device firmware. |
| **Research** | The project exists to advance knowledge, train models, or enable experimentation. It may be highly mature as software, but it is not heading toward direct grid deployment. |

Applied projects follow the normal deployment maturity arc (R&D → Piloting → Production). Research projects do not — their maturity is better measured by adoption within the research community.

| Project | Intent | Rationale |
|---------|--------|-----------|
| Grid2Op | Research | Simulation environment for grid control research and competitions |
| GridFM | Research | Foundation model research for power systems — may transition to Applied if it produces operational tools |
| OpenSynth | Research | Synthetic data generation for research and model training |
| p-SWAMP | Research | Wide-area monitoring R&D platform and testbed |
| *(all others)* | Applied | |

### AI/ML

Identifies projects where **AI or machine learning is core to the project's purpose**, not merely used as a peripheral technique. The test: "Would this project exist without AI/ML?"

| Project | Rationale |
|---------|-----------|
| AINETUS | Reinforcement learning agents, graph neural solver, and AI explainability ARE the project |
| GridFM | Foundation models ARE the project |
| OpenSTEF | ML forecasting pipeline is the core capability |
| OpenSynth | Generative AI models (VAE, diffusion) are the core |

### Modeling & Simulation

Identifies projects that provide **modeling or simulation capability**, regardless of their primary function placement. This cuts across the matrix because modeling and simulation tools serve P&A, Operations research, and operations training alike.

| Project | Rationale |
|---------|-----------|
| PowSyBl | Power system modeling and power flow simulation |
| Dynawo | Dynamic and transient simulation |
| Power Grid Model | Steady-state distribution simulation |
| GridFM | Foundation-model-based power system simulation |
| Arras | Agent-based distribution scenario simulation |
| SOGNO | DPsim simulation engine as a component |

### Deliverable Type

Describes **what you are adopting when you adopt this project**. Most projects have one primary deliverable type. Projects that genuinely ship in multiple modes (e.g., a specification with reference software and reference datasets) may be tagged with multiple values.

| Value | You're adopting... |
|-------|-------------------|
| **Specification** | A standard, protocol, API definition, or interoperability framework — you may implement it yourself or use provided tooling |
| **Software** | A tool, framework, platform, or library you run |
| **Data** | Datasets or data generation tools whose primary value is the data produced |

| Project | Deliverable Type |
|---------|-----------------|
| TROLIE | Specification |
| GEISA | Specification |
| CDS Customer Data | Specification |
| CDS Registration | Specification |
| URPX | Specification |
| Battery Data Alliance | Specification, Software, Data |
| ORES | Specification |
| OpenSynth | Data |
| *(all others)* | Software |

### Cross-Cutting Tag Summary

| Project | Intent | AI/ML | Modeling & Sim | Deliverable |
|---------|--------|-------|----------------|-------------|
| AINETUS | Applied | AI/ML | | Software |
| Arras | Applied | | Modeling & Sim | Software |
| Battery Data Alliance | Applied | | | Specification, Software, Data |
| CDS Customer Data | Applied | | | Specification |
| CDS Registration | Applied | | | Specification |
| CitrineOS | Applied | | | Software |
| CoMPAS | Applied | | | Software |
| covXtreme | Applied | | | Software |
| Dynawo | Applied | | Modeling & Sim | Software |
| EVerest | Applied | | | Software |
| FIDOpower | Applied | | | Software |
| FlexMeasures | Applied | | | Software |
| GEISA | Applied | | | Specification |
| Grid2Op | Research | | | Software |
| GridFM | Research | AI/ML | Modeling & Sim | Software |
| GXF | Applied | | | Software |
| Hyphae | Applied | | | Software |
| OpenDSM | Applied | | | Software |
| OpenLEADR | Applied | | | Software |
| OpenSTEF | Applied | AI/ML | | Software |
| OpenSynth | Research | AI/ML | | Data |
| OperatorFabric | Applied | | | Software |
| ORES | Applied | | | Specification |
| p-SWAMP | Research | | | Software |
| Power Grid Model | Applied | | Modeling & Sim | Software |
| PowSyBl | Applied | | Modeling & Sim | Software |
| RTC-Tools | Applied | | | Software |
| RTDIP | Applied | | | Software |
| SEAPATH | Applied | | | Software |
| SEF | Applied | | | Software |
| Shapeshifter | Applied | | | Software |
| SOGNO | Applied | | Modeling & Sim | Software |
| TROLIE | Applied | | | Specification |
| URPX | Applied | | | Specification |

## Maintaining the Taxonomy

### When to Update

- **New project joins LF Energy:** Assign Grid Segment(s) and Function using the criteria above. Add to the matrix. Assess Industry Solution Categories. Assign cross-cutting tags (Project Intent, AI/ML, Modeling & Simulation, Deliverable Type).
- **Project scope changes:** Review placement if a project's capabilities shift significantly.
- **Taxonomy itself needs revision:** If multiple projects don't fit, or a category grows beyond ~12 projects, revisit the category definitions.

### Conventions

- **Grid Segment** in project overviews: list applicable segments, with "(primary)" and "(secondary)" qualifiers when there is a genuine distinction.
- **Function** in project overviews: list the function category. For subcategories, use an em dash: `Operations — Substation Digitalization`. For multi-category projects, indicate primary and secondary: `Operations (primary), Planning & Analysis (secondary)`.
- **Industry Solution Categories** in project overviews: "Solution Type" describes what the project IS; "Component of" describes the broader utility system it fits into. Leave "Component of" blank rather than forcing a fit.
