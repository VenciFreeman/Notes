# 纳米级CMOS的可制造性设计

> Design for Manufacturability (DFM) for Nani-scale CMOS

**主讲**：李永福

[TOC]

## Understanding Moore's Law and its impact

- 1971：4004
- Moore's law: Enables innovation and cost reductions
  - ​     Same circuitry ~ half the space
  - or Twice the circuitry in the ~ same space
  - =  Optimized by design for best performance / cost
  - e. g. Chip Layout Complexity in iPhone
    - A4 (53mm<sup>2</sup> 45nm)
    - A13 (98mm<sup>2</sup> 7nm)
- Market continue to grow
- steady market expansion
  - Increasing semiconductor penetration in electronics
  - Increasing functionalities and performance
  - New applications
  - 
- China market continues to grow
- EDA Companies
  - R&D Centre
  - Regional Office

## Importance of EDA

- Trend between # transistors vs EDA
  - EDA is the backbone of the entire semiconductor industry
- Is EDA research easy
  - Go: number of State 10<sup>360</sup>
  - Chip Placement: number of State 10<sup>9000</sup>
- Google Research in ISSCC 2020
  - Human Expert: ~6-8 person weeks
  - ML Placer: 24 hours
- Why EDA is important in China
- Who else has this problem
  - What do I benefit from EDA course if I am not into EDA research or industry

## What's EDA and its history

- Time Period

  - 1950-1965: manual design only.
  - 1965-1975: layout editors, e. g. place and route tools
  - 1975-1985: more advanced tools for ICs and PCBs
  - 1985-1990: First performance-driven tools and parallel optimization algorithms for layout
  - 1990-2000: First over-the-cell routing, first 3D multilayer placement and routing technique developed
  - 2000-now: design for manufacturability, optical proximity correction and other techniques emerge at the design-manufacturing interface.

- Common EDA terminology

  > System Specification ==> Arch

  - Logic design: mapping the  VHDL / Verilog code to circuit gates / netlist
  - Physical design: geometrical arrangement of cells and their connections within the IC layout
  - Physical verification: checks the correctness of the layout design
    - DRC: Design Rule Checking
    - LV: Layout vs. Schematic
    - ERC: Electrical Rule Checking

- Simple concept: schematic to layout

  > Standard cells ==>

- How does things get complicated

- How to draw the layout

- VLSI design flow

## What's DFM and its capabilities

Challenges in Semiconductor Industry

#### Economy

- Huge Capex

  - Financing & Profitability of a new fab?

- ROI Risk

  - Increasing R&D costs
  - Increasing time & investment to ramp up yield

  > Costs are now prohibitive for many companies to continue to invest

#### Technology

- Manufacturing
- Design
  - Increasing process steps & design rules
  - Increasing yield loss due to process variation

### Define the type of yields?

### What cause poor functional yields?

#### Fab

- Random effects
  - Misalignment
  - Impurities / dust particles (Outside the die)
  - Defects (Within the die)
- Systematic effects
  - Human Errors
  - Equipment Errors
  - Limitation of lithography
  - Planarity issues

#### Design

- Physical effects
  - Fabrication accuracy
- Electrical & Parasitic effects
  - Modelling accuracy
- Thermal effects
  - Thermal gradients
  - Layout

### Yield Loss Mechanisms

### Root Causes?

#### Foundries

- More complex process
  - e. g. Strain engineering
    - Well proximity effects
    - Unforeseen mismatch
- More complex design rules

#### IC Design Companies / Product

- Circuits are sensitive to layout, matching, proximity and stress
  - e. g. It may not b possible for an unaided human to estimate the actual strain on a given transistor
- Harder to get skillful & experienced design engineers
- Reduce the design time cycle
  - maximize profit

#### Software design tool

- Lack of proper design-layout guided tools to ensure robust layout
- Lack of comprehensive verification tools for design sign-off

## What's DFM & it's capabilities?

### Characteristics of DFM

- Manufacturing yield
  - Root Cause: Global | Local (~1μm)
  - Variation: Systematic | Random
- Type of DFM
  - Physical DFM ==> Functional
- Research / Implementation Techniques

### Industrial DFM Applications

- Systematic
- Printability
- Random
- Parametric

## Why CMOS Technology requires DFM

## My past works in GLOBALFOUNDRIES

## University Program & Design Contest