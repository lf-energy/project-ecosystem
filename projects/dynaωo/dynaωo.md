# Dynaωo

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

- LF Energy webpage: https://lfenergy.org/projects/dyna%cf%89o/
- Website: https://dynawo.github.io/ <!-- note: appears ~3 years stale, limited credibility -->
- Code: https://github.com/dynawo
- Documentation: https://github.com/dynawo/dynawo/releases/download/nightly/DynawoDocumentation.pdf
- Calendar:
- LinkedIn:
- Community:
	- Mailing List: https://lists.lfenergy.org/g/dynawo
	- Slack:
- LFX Insights: https://insights.linuxfoundation.org/project/dynawo
- Other:

## Description

Suite of dynamic simulation tools for power system analysis, built on transparent Modelica models.

## Overview

Dynaωo is a suite of simulation tools for power system dynamic analysis. It provides steady-state calculation (DynaFlow), long-term stability simulation (DynaWaltz), and transient stability simulation (DynaSwing) — with short-circuit calculation (DySym) and quasi-EMT analysis (DynaWave) under development. All tools share a common architecture, model library, and compiler, meaning the same equipment models can be reused across different types of studies. Dynaωo models power system components using the Modelica language, an equation-based modeling language where the mathematics are written in a form that engineers can read and verify, rather than being hidden inside compiled code.

Grid operators need dynamic simulation to ensure the power system remains stable under disturbances — generator trips, line faults, load changes, and the growing complexity introduced by renewable energy and power-electronic devices. Traditional simulation tools use simplified models with implementations hidden inside compiled code, making it difficult to share, compare, or modify analysis assumptions across organizations. Dynaωo addresses this by providing transparent, open models that operators can inspect and customize, paired with solvers that are interchangeable without affecting the models. This enables collaborative studies where multiple TSOs can agree on shared modeling and solving choices.

Dynaωo is developed and maintained by RTE (the French TSO), which uses the DynaWaltz tool operationally on a daily basis in its national control center for voltage stability analysis, including contingency analysis and voltage margin calculations. The simulation engine has been validated on the full French EHV-HV network (in the range of 100,000 continuous variables and 150,000 discrete variables after simplifications). Dynaωo integrates with PowSyBl through the powsybl-dynawo wrapper, which allows DynaFlow and DynaWaltz to be invoked from within PowSyBl workflows. The project is primarily written in C++ with Modelica for component models, and is built on the OpenModelica compiler.

## Technical Profile

### What It Does

Simulates power system behavior over time — from steady-state equilibrium calculations to transient and long-term stability analysis — using transparent Modelica-based equipment models with interchangeable numerical solvers.

### Problem(s) Solved

Enables TSOs to perform dynamic stability studies — voltage stability, transient stability, and steady-state calculations — using open, transparent models that can be shared and validated across organizations, replacing proprietary black-box simulation tools where modeling choices are hidden and difficult to compare.

### Key Capabilities

- **Steady-state calculation (DynaFlow)**: Computes system equilibrium following events using a simplified time-domain simulation, correctly capturing the influence of control speeds and regulation dynamics on the final operating point — unlike traditional power flow tools that ignore these temporal effects
- **Long-term stability simulation (DynaWaltz)**: Simulates long-term dynamics (seconds to minutes) to verify voltage stability and detect slow collapse scenarios, using a simplified solver that filters fast dynamics while retaining detailed models
- **Transient stability simulation (DynaSwing)**: Simulates short-term dynamics (milliseconds to seconds) to assess system response to faults, using the variable time-step IDA solver for high accuracy
- **Contingency analysis and margin calculation**: The dynawo-algorithms repository provides systematic contingency analysis and voltage margin computation
- **Modelica-based model library**: Includes synchronous generators (with configurable windings and transformer models), loads, transformers, HVDCs, SVCs, wind turbines and PV (WECC standard models), protection automata (under-voltage, current limiting), and grid-forming controllers
- **Model reuse across study types**: The same equipment models serve multiple simulation tools — only the solver and its configuration change between steady-state, long-term, and transient studies
- **Separation of modeling and solving**: Models expose standard interfaces (residual, Jacobian, zero-crossing functions) to solvers, allowing solvers to be swapped without modifying models
- **Large-scale network simulation**: Validated on networks with 100,000+ continuous variables, with pre-compilation of models enabling performance comparable to existing commercial tools
- **Grid compliance verification**: Dedicated tool (dyn-grid-compliance-verification) for automatic verification of grid-code compliance on dynamic behavior for generators and renewable energy farms

### Relevant Standards

None directly implemented. Dynaωo includes equipment models that follow WECC standard model specifications for wind turbines and PV, but these are modeling conventions rather than communication or data exchange standards that the tool itself implements.

## Grid Context

### Grid Segment

Transmission

### Function

Grid Modeling & Simulation

### Industry Solution Categories

#### Solution Type

- Dynamic Simulation: Provides time-domain simulation for power system stability analysis, spanning steady-state, long-term, and transient studies.

#### Component of

- EMS: Serves as the dynamic simulation engine within energy management systems, providing the stability analysis capabilities needed for real-time grid operations and planning.

### Cross-Cutting Tags

- **Project Intent:** Applied
- **AI/ML:** No
- **Deliverable Type:** Software

## Related Projects

- **PowSyBl**: PowSyBl provides a wrapper (powsybl-dynawo) that enables Dynaωo's DynaFlow and DynaWaltz simulators to be invoked from within PowSyBl workflows, extending PowSyBl's steady-state network analysis capabilities with dynamic simulation. Both are used in production at RTE.

## Maturity & Adoption

### LF Energy Stage

Incubation

### Deployment Maturity

Production

### Supporting / Adopting Companies

- RTE (primary developer; production user — DynaWaltz used daily in national control center for voltage stability analysis)

## Learn More

TODO: Add presentations and case studies

## Additional Notes

Dynaωo's central design choice — using the Modelica language for power system component modeling — is strategically significant. In proprietary simulation tools, equipment models are typically embedded in compiled code that users cannot inspect or modify. Dynaωo's Modelica models are readable equation-based descriptions, enabling multiple organizations to share, review, and agree on modeling assumptions. This transparency is particularly valuable in the European context, where TSOs and RCCs must coordinate cross-border stability studies and agree on how equipment behaves under disturbances.

The project originated from two European R&D projects — Pegase and iTesla — which demonstrated the viability of using Modelica for industrial-scale power system simulation and developed the numerical methods integrated into Dynaωo. The current release (v1.7.0, July 2025) includes validated models and solvers for DynaFlow, DynaWaltz, and DynaSwing. DySym (short-circuit) remains at research stage, and DynaWave (quasi-EMT for high-penetration power electronics) is in early development. The project is licensed under MPL-2.0.
