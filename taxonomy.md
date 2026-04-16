# LF Energy Project Taxonomy

**Last Updated:** 2026-03-18

## Contents

- [Purpose](#purpose)
- [Grid Segment](#grid-segment)
- [Function](#function)
  - [Grid Modeling & Simulation](#grid-modeling--simulation)
  - [Grid Operations](#grid-operations)
  - [Flexibility & Markets](#flexibility--markets)
  - [Interoperability & Data](#interoperability--data)
  - [Projects That Don't Fit Cleanly](#projects-that-dont-fit-cleanly)
  - [Borderline Placement Decisions](#borderline-placement-decisions)
- [Grid Segment x Function Matrix](#grid-segment-x-function-matrix)
- [Industry Solution Categories](#industry-solution-categories)
- [Cross-Cutting Tags](#cross-cutting-tags)
  - [Project Intent](#project-intent)
  - [AI/ML](#aiml)
  - [Deliverable Type](#deliverable-type)
  - [Cross-Cutting Tag Summary](#cross-cutting-tag-summary)
- [Maintaining the Taxonomy](#maintaining-the-taxonomy)

## Purpose

This taxonomy provides a framework for categorizing and navigating LF Energy's project portfolio. It is designed for **discovery** — helping website visitors, potential members, and utility engineers find relevant projects and understand how they fit together.

The taxonomy uses two primary dimensions (**Grid Segment** and **Function**) plus a supplementary navigation layer (**Industry Solution Categories**). Together, these provide multiple entry points into the portfolio depending on how the visitor thinks about the problem they're trying to solve.

## Grid Segment

Grid Segment describes **where on the energy system** a project operates. These are physical segments of the energy value chain, listed in order from power production to consumption.

| Segment | Description |
|---------|-------------|
| **Generation** | Power production assets and associated systems — power plants, wind farms, solar farms, hydropower facilities |
| **Transmission** | Bulk power delivery network — high-voltage lines, substations, and interconnections managed by TSOs, RCCs, and ISOs/RTOs |
| **Distribution** | Local power delivery network — medium- and low-voltage infrastructure managed by DSOs, delivering power to end customers |
| **Behind the Meter** | Customer-sited systems — DER, EV charging, microgrids, home/building energy management, and other assets on the customer side of the utility meter |

### Usage

- Projects may be tagged with multiple segments where they genuinely operate across boundaries (e.g., a protection platform deployed in both transmission and distribution substations).
- When a project has a primary and secondary segment, indicate this (e.g., "Distribution (primary), Transmission (secondary)").
- Some projects are energy-adjacent but do not map to a specific grid segment (e.g., battery R&D data standards, extreme weather hazard analysis). These do not require a Grid Segment tag.

## Function

Function describes **what a project does for the energy system**. Categories are defined by the grid problem a project solves, not by its technology approach (AI/ML), deliverable format (specification), or architecture (microservices).

**Test:** "If a utility engineer asks 'what does this project do?', which category does the answer fall into?"

### Categories

#### Grid Modeling & Simulation

Computational tools for representing, analyzing, and simulating grid behavior — whether for network planning, operational studies, research, or training AI models.

Projects in this category create computational representations of the grid. They may serve long-term planning, near-term operational analysis, or research, but they are united by the core activity of modeling how the grid behaves.

| Project | Grid Segment | What it does |
|---------|-------------|-------------|
| PowSyBl | Transmission | Network modeling, power flow, contingency analysis, capacity calculation |
| Dynawo | Transmission | Dynamic and transient power system simulation |
| Power Grid Model | Distribution | High-performance steady-state distribution network analysis |
| Arras | Distribution | Agent-based distribution system scenario planning |
| FIDOpower | Distribution | Interactive notebook-based distribution analysis workflows |
| GridFM | Transmission, Distribution | Foundation models for power system analysis |
| OpenSynth | Transmission, Distribution | Synthetic grid datasets and topologies for research and planning |

#### Grid Operations

Tools that support grid monitoring, control, coordination, and operational decision-making. This includes near-term operational forecasting and operations-focused research platforms, not only real-time systems.

Projects in this category help grid operators manage the operating grid — from real-time monitoring through short-term operational planning. The defining characteristic is that the project's purpose is to support operational decisions and actions.

**Subcategory: Substation Digitalization** — Tools for modernizing substation protection, automation, and control systems. Called out as a subcategory because digital substations represent a distinct, recognized utility investment domain. In project overviews, indicated as `Grid Operations — Substation Digitalization`.

| Project | Subcategory | Grid Segment | What it does |
|---------|------------|-------------|-------------|
| OperatorFabric | | Transmission, Distribution | Operator notification and coordination |
| SOGNO | | Distribution | Distribution grid monitoring, state estimation, and automation |
| OpenSTEF | | Distribution | Short-term (up to 48-hour) energy load forecasting for operational congestion management |
| GXF | | Distribution | IoT field device communication and management |
| TROLIE | | Transmission | Transmission facility ratings exchange (FERC Order 881) |
| Grid2Op | | Transmission | Simulation environment for developing automated grid control strategies |
| p-SWAMP | | Transmission | Wide-area monitoring, protection, and control R&D platform |
| SEAPATH | Substation Digitalization | Transmission, Distribution | Virtualization platform for protection, automation, and control applications |
| CoMPAS | Substation Digitalization | Transmission, Distribution | Vendor-neutral IEC 61850 substation configuration tooling |

**Notes on specific placements:**
- **SOGNO** is also tagged as a secondary category in Grid Modeling & Simulation, due to its DPsim simulation engine and CIM data modeling libraries which have independent value as modeling tools.
- **OpenSTEF** produces 48-hour-ahead forecasts — not "real-time" in the SCADA sense, but its purpose is operational congestion management, and it is a component of ADMS (an operational system).
- **Grid2Op** and **p-SWAMP** are research platforms, not production operations tools. They are categorized here because their purpose is specifically to advance grid operations capabilities (RL-based control strategies and WAMPAC, respectively). Their research nature should be noted in project descriptions and can be captured through future cross-cutting tags.
- **TROLIE** is an API specification, but its function is enabling operational ratings exchange. Could alternatively be categorized under Interoperability & Data; placed here because its purpose is tightly coupled to transmission operations (FERC Order 881 compliance).

#### Flexibility & Markets

Tools for managing distributed energy resources, demand-side programs, and market participation — including the optimization intelligence, communication protocols, and physical integration infrastructure that enable flexible resource coordination.

This category covers the full stack of flexibility management, from the firmware running on devices (EVerest) to the optimization engines that coordinate them (FlexMeasures, RTC-Tools) to the market protocols that trade their output (Shapeshifter). The unifying thread is that these projects enable the grid to use flexible, distributed resources.

**Subcategory: EV Charging** — Charging infrastructure firmware and management systems. Called out as a subcategory because EV charging is a distinct, high-visibility domain with its own standards ecosystem (OCPP, ISO 15118). In project overviews, indicated as `Flexibility & Markets — EV Charging`.

| Project | Subcategory | Grid Segment | What it does |
|---------|------------|-------------|-------------|
| FlexMeasures | | Behind the Meter | Behind-the-meter energy asset optimization |
| RTC-Tools | | Generation | Multi-asset dispatch optimization (hydropower, BESS, multi-market) |
| Shapeshifter | | Transmission, Distribution | Flexibility trading protocol between grid operators and aggregators |
| OpenLEADR | | Distribution, Behind the Meter | Automated demand response communication (OpenADR) |
| OpenDSM | | Distribution, Behind the Meter | Demand-side program measurement and verification |
| Hyphae | | Behind the Meter | DC microgrid autonomous energy sharing |
| ORES | | Behind the Meter | Modular, plug-and-play residential DER systems |
| GEISA | | Distribution | Grid edge application interoperability for smart meters and DA controllers |
| EVerest | EV Charging | Behind the Meter | Standards-compliant EV charger firmware stack |
| CitrineOS | EV Charging | Behind the Meter | OCPP-based charging station management system |

**Notes on specific placements:**
- **GEISA** defines application interoperability on grid edge devices — it enables DER and AMI applications to run on distribution-level hardware, making it a better fit here than in Interoperability & Data (which focuses on data exchange).
- **RTC-Tools** is tagged with Generation (its primary use case is hydropower scheduling) but also serves market optimization for BESS and multi-energy systems.

#### Interoperability & Data

Standards and platforms that enable energy systems to exchange and use each other's data.

Projects in this category exist specifically to solve the interoperability problem — making it possible for different utility systems, third-party platforms, or industry tools to share information. Their primary function is enabling data flow, not making operational decisions or modeling the grid.

| Project | Grid Segment | What it does |
|---------|-------------|-------------|
| CDS Customer Data | Distribution | Standardized APIs for authorized third-party access to customer energy data |
| CDS Registration | Distribution | Utility API discovery, registration, and secure connectivity |
| URPX | Distribution | Machine-readable format for utility rate plan data |
| SEF | Distribution, Behind the Meter | Semantic interoperability middleware using ontology-based knowledge graphs |
| RTDIP | Generation | Cloud-native time-series data platform for sensor and meter data at scale |
| Battery Data Alliance | *(none)* | Shared software standards and data formats for battery testing |

### Subcategory Format

When a project belongs to a subcategory, its Function field in the project overview uses an em dash to indicate the relationship:

```
Grid Operations — Substation Digitalization
Flexibility & Markets — EV Charging
```

Projects that belong to the parent category without a subcategory simply list the parent:

```
Grid Operations
Flexibility & Markets
```

### Projects That Don't Fit Cleanly

| Project | Why it doesn't fit | Grid Segment |
|---------|-------------------|-------------|
| covXtreme | Extreme weather hazard analysis — energy-adjacent (offshore wind, infrastructure design) but not grid-specific | *(none)* |

covXtreme provides statistical tools for modeling extreme environmental events. While relevant to energy infrastructure planning (particularly offshore wind), it is a general-purpose hazard analysis toolkit rather than a grid-specific tool.

### Borderline Placement Decisions

When a project could reasonably fit in more than one function category, the reasoning for the chosen placement is documented in the "Notes on specific placements" section within the relevant category above. This preserves context for future reviewers and enables informed updates if new information emerges.

Summary of current borderline placements:

- **TROLIE:** Grid Operations (operational purpose) vs. Interoperability & Data (API specification deliverable)
- **SOGNO:** Primary Grid Operations (DSO automation mission), secondary Grid Modeling & Simulation (DPsim and CIM tooling)
- **GEISA:** Flexibility & Markets (enables DER/AMI edge applications) vs. Interoperability & Data (interoperability specification, but for applications not data)
- **OpenSynth:** Grid Modeling & Simulation (feeds modeling tools) vs. Interoperability & Data (data commons, but users are modelers not integrators)
- **Grid2Op, p-SWAMP:** Grid Operations (purpose: advancing grid control) vs. Grid Modeling & Simulation (method: simulation/research)

## Grid Segment x Function Matrix

|  | **Generation** | **Transmission** | **Distribution** | **Behind the Meter** |
|---|---|---|---|---|
| **Grid Modeling & Simulation** | | PowSyBl, Dynawo, GridFM, OpenSynth | Power Grid Model, Arras, FIDOpower, GridFM, OpenSynth, SOGNO* | |
| **Grid Operations** | | OperatorFabric, TROLIE, Grid2Op, p-SWAMP, SEAPATH+, CoMPAS+ | OperatorFabric*, SOGNO, OpenSTEF, GXF, SEAPATH+, CoMPAS+ | |
| **Flexibility & Markets** | RTC-Tools | Shapeshifter | Shapeshifter, OpenLEADR, OpenDSM, GEISA | FlexMeasures, OpenLEADR*, OpenDSM, Hyphae, ORES, EVerest+, CitrineOS+ |
| **Interoperability & Data** | RTDIP | | CDS Customer Data, CDS Registration, URPX, SEF | SEF* |

\* = secondary segment or secondary function category
\+ = subcategory (Substation Digitalization or EV Charging)

**Not shown:** Battery Data Alliance (Interoperability & Data, no grid segment), covXtreme (no function category, no grid segment)

## Industry Solution Categories

Industry Solution Categories describe the **recognized utility systems** that a project contributes to. These are supplementary to the primary taxonomy — they provide an additional navigation path for utility engineers who think in terms of the systems they buy and build.

Not all projects map to an Industry Solution Category, and that's fine. These categories work best for projects that are components of established utility systems.

### How to Use

Each project overview includes an "Industry Solution Categories" section with two subsections:
- **Solution Type:** What the project fundamentally IS as a solution category (e.g., "Network Analysis", "Load Forecasting", "Virtualization Platform")
- **Component of:** The broader utility systems where this project serves as a building block (e.g., EMS, ADMS, DERMS)

### Common Industry Solution Categories

These are the utility system categories that appear across the portfolio. A visitor filtering by one of these categories would find the listed projects.

| Industry Solution | Description | Projects |
|------------------|-------------|----------|
| **EMS** | Energy Management System — transmission grid operations | PowSyBl, Dynawo, TROLIE |
| **ADMS** | Advanced Distribution Management System — distribution grid operations | SOGNO, Power Grid Model, OpenSTEF |
| **DERMS** | Distributed Energy Resource Management System — DER coordination | FlexMeasures, OpenLEADR, Shapeshifter |
| **Digital Substation** | Digitalized protection, automation, and control | SEAPATH, CoMPAS |
| **EV Charging Infrastructure** | Charging hardware and management platforms | EVerest, CitrineOS |
| **AMI** | Advanced Metering Infrastructure — smart metering and edge | GXF, GEISA |
| **Network Planning** | Grid reinforcement and capacity studies | Arras, Power Grid Model, PowSyBl |
| **WAMPAC** | Wide Area Monitoring, Protection, and Control | p-SWAMP |
| **Market Management** | Wholesale and flexibility market systems | TROLIE, Shapeshifter |

Not all projects appear in this table. Projects that are standalone tools (Grid2Op, OpenSynth, covXtreme), emerging categories without established utility system names (CDS family, URPX, SEF), or adjacent to the grid (Battery Data Alliance) may not have a Component of mapping.

## Cross-Cutting Tags

Cross-cutting tags provide additional dimensions for filtering and navigating the portfolio beyond Grid Segment and Function. They answer questions that cut across the primary taxonomy: "Is this an AI project?", "Am I adopting a spec or running software?", "Is this a research tool or something I can deploy?"

### Project Intent

Describes **why the project exists** — whether it produces outcomes that affect real grid decisions and infrastructure, or exists to advance knowledge and enable experimentation.

| Value | Description |
|-------|-------------|
| **Applied** | The project aims to be used in planning, operating, or managing real energy systems. Includes everything from control room tools to planning study software to device firmware. |
| **Research** | The project exists to advance knowledge, train models, or enable experimentation. It may be highly mature as software, but it is not heading toward direct grid deployment. |

Applied projects follow the normal deployment maturity arc (R&D → Piloting → Production). Research projects do not — their maturity is better measured by adoption within the research community, not by grid deployment.

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
| GridFM | Foundation models ARE the project |
| OpenSTEF | ML forecasting pipeline is the core capability |
| OpenSynth | Generative AI models (VAE, diffusion) are the core |

Projects that use ML as one technique among many (e.g., FlexMeasures uses ML forecasting to support its optimization core) do not carry this tag. Similarly, projects that provide environments where AI is commonly applied but are not themselves AI (e.g., Grid2Op is a simulation environment used for RL research, but the platform itself contains no AI) do not carry this tag. The AI SIG may still engage with these projects, but the tag is reserved for AI-native projects.

### Deliverable Type

Describes **what you are adopting when you adopt this project**. Single-select based on primary output — many specification projects ship reference implementations, client libraries, or conformance tests, but the primary thing being adopted is the specification itself.

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
| Battery Data Alliance | Specification |
| ORES | Specification |
| OpenSynth | Data |
| *(all others)* | Software |

### Cross-Cutting Tag Summary

| Project | Intent | AI/ML | Deliverable |
|---------|--------|-------|-------------|
| Arras | Applied | | Software |
| Battery Data Alliance | Applied | | Specification |
| CDS Customer Data | Applied | | Specification |
| CDS Registration | Applied | | Specification |
| CitrineOS | Applied | | Software |
| CoMPAS | Applied | | Software |
| covXtreme | Applied | | Software |
| Dynawo | Applied | | Software |
| EVerest | Applied | | Software |
| FIDOpower | Applied | | Software |
| FlexMeasures | Applied | | Software |
| GEISA | Applied | | Specification |
| Grid2Op | Research | | Software |
| GridFM | Research | AI/ML | Software |
| GXF | Applied | | Software |
| Hyphae | Applied | | Software |
| OpenDSM | Applied | | Software |
| OpenLEADR | Applied | | Software |
| OpenSTEF | Applied | AI/ML | Software |
| OpenSynth | Research | AI/ML | Data |
| OperatorFabric | Applied | | Software |
| ORES | Applied | | Specification |
| p-SWAMP | Research | | Software |
| Power Grid Model | Applied | | Software |
| PowSyBl | Applied | | Software |
| RTC-Tools | Applied | | Software |
| RTDIP | Applied | | Software |
| SEAPATH | Applied | | Software |
| SEF | Applied | | Software |
| Shapeshifter | Applied | | Software |
| SOGNO | Applied | | Software |
| TROLIE | Applied | | Specification |
| URPX | Applied | | Specification |

## Maintaining the Taxonomy

### When to Update

- **New project joins LF Energy:** Assign Grid Segment(s) and Function using the criteria above. Add to the matrix. Assess Industry Solution Categories. Assign cross-cutting tags (Project Intent, AI/ML, Deliverable Type).
- **Project scope changes:** Review placement if a project's capabilities shift significantly.
- **Taxonomy itself needs revision:** If multiple projects don't fit, or a category grows beyond ~12 projects, revisit the category definitions.

### Conventions

- **Grid Segment** in project overviews: list applicable segments, with "(primary)" and "(secondary)" qualifiers when there is a genuine distinction.
- **Function** in project overviews: list the function category. For subcategories, use an em dash: `Grid Operations — Substation Digitalization`. For multi-category projects, indicate primary and secondary: `Grid Operations (primary), Grid Modeling & Simulation (secondary)`.
- **Industry Solution Categories** in project overviews: "Solution Type" describes what the project IS; "Component of" describes the broader utility system it fits into. Leave "Component of" blank rather than forcing a fit.