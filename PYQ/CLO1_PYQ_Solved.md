# CLO 1 PYQ Solved - SoC Flow, ASIC Flow, Metrics, Chip Basics And System Introduction

## Clickable Index

- [Q1. Front-End Vs Back-End SoC Design](#q1-front-end-vs-back-end-soc-design)
- [Q2. Top-Down SoC Design Flow](#q2-top-down-soc-design-flow)
- [Q3. ASIC Design Flow And EDA Tools](#q3-asic-design-flow-and-eda-tools)
- [Q4. ASIC Vs SoC And EDA Tools](#q4-asic-vs-soc-and-eda-tools)
- [Q5. SoC Design Metrics And PDP](#q5-soc-design-metrics-and-pdp)
- [Q6. Five Chip Basics](#q6-five-chip-basics)
- [Q7. MST 2026 Brief Notes](#q7-mst-2026-brief-notes)

## CLO Mapping

This file maps to **CLO 1: Familiarize with Design Flow of SoC** and introductory SoC design concepts.

Use with:

- [CLO1.md](<../CLO1.md>)
- [PYQ Master Index](<PYQ_Master_Index.md>)

## Local PPT / Book References To Use

Use these while revising or writing this CLO1 PYQ answer:

- [SOC Design Flow.pdf, p.2](<../System on chip/SOC Design Flow.pdf#page=2>) supports design-flow pressure from design size, deep-submicron effects and predictable implementation time.
- [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) supports top-down design using system-level models, performance tradeoff analysis and partitioning.
- [SOC Design Flow.pdf, p.6](<../System on chip/SOC Design Flow.pdf#page=6>) supports top-down principles such as HDL/high-level models, early validation, reusable cores and verification environment.
- [module 1 part 1 introduction to system approach.pdf, p.2](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=2>) supports system architecture as processors, memories and interconnects.
- [module 1 part 1 introduction to system approach.pdf, p.3](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=3>) supports hardware/software implementation decisions.
- [module 1 part 1 introduction to system approach.pdf, p.4](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=4>) supports software programmability versus performance.
- [module 1 chip basics.pdf, p.1](<../System on chip/module 1 chip basics.pdf#page=1>) introduces chip basics: time, area, power, reliability and configurability.
- [module 1 chip basics.pdf, p.3](<../System on chip/module 1 chip basics.pdf#page=3>) supports design tradeoffs.
- [module 1 chip basics.pdf, p.13](<../System on chip/module 1 chip basics.pdf#page=13>) supports power as dynamic/switching and static/leakage.
- [Design_Metrics.pdf, p.2](<../System on chip/Design_Metrics.pdf#page=2>) supports deep-submicron issues such as power, interconnect, noise, crosstalk, reliability and clock distribution.
- [Design_Metrics.pdf, p.6](<../System on chip/Design_Metrics.pdf#page=6>) lists fundamental design metrics: functionality, cost, reliability, performance, power/energy, time-to-market and reusability.
- Detailed source maps: [CLO1_Topic1_sources.md](<../sources/CLO1_Topic1_sources.md>) and [CLO2_review_sources.md](<../sources/CLO2_review_sources.md>).

<a id="q1-front-end-vs-back-end-soc-design"></a>

## Q1. Differentiate Between Front-End And Back-End SoC Architecture Design

**PYQ source:** MST 2024 Q3.

### Core Difference

**Front-end design** defines and verifies what the chip should do.

**Back-end design** converts the verified logic into physical silicon layout that can be manufactured.

### Front-End Design

Front-end design works at specification, architecture, RTL and verification level.

Main activities:

- system specification,
- architecture design,
- hardware/software partitioning,
- RTL coding,
- IP integration,
- memory map definition,
- interface definition,
- functional verification,
- synthesis constraints,
- power intent definition.

Output:

```text
Verified RTL + constraints + design intent
```

### Back-End Design

Back-end design works at gate, layout and manufacturing level.

Main activities:

- synthesis to gate-level netlist,
- floorplanning,
- power planning,
- placement,
- clock tree synthesis,
- routing,
- timing closure,
- physical verification,
- DRC/LVS,
- parasitic extraction,
- sign-off,
- GDSII generation.

Output:

```text
Manufacturable layout / GDSII
```

### Comparison Table

| Point | Front-end | Back-end |
|---|---|---|
| Main question | Does the design function correctly? | Can it be physically manufactured and meet timing/power? |
| Abstraction | Specification, architecture, RTL | Gates, floorplan, layout, masks |
| Main tools | RTL simulator, lint, formal, synthesis | PnR, STA, DRC, LVS, extraction |
| Output | Verified RTL/netlist intent | Physical layout/GDSII |
| Main risk | Functional bug | Timing, congestion, power, manufacturability |

### Final Exam Answer

Front-end SoC design converts requirements into architecture, RTL and verified functionality. It includes specification, partitioning, IP selection, RTL design, memory-map definition and functional verification. Back-end SoC design converts the verified design into physical silicon. It includes synthesis, floorplanning, placement, clock tree synthesis, routing, static timing analysis, physical verification and GDSII generation. Front-end focuses on functional correctness and architecture; back-end focuses on timing, power, area, routing and manufacturability.

<a id="q2-top-down-soc-design-flow"></a>

## Q2. What Is The Top-Down SoC Design Flow? Discuss Its Significance And Stages

**PYQ source:** MST 2024 Q2, MST 2025 Q1, MST 2026 Q1(e).

### Definition

**Top-down SoC design flow** starts from system requirements and gradually refines the design into architecture, hardware/software partitioning, RTL, physical implementation and verification.

It is called top-down because the designer begins with the complete system goal before designing individual blocks.

### Why It Is Significant

Top-down flow is important because SoCs are too complex to build bottom-up without a system plan.

It helps with:

- requirement traceability,
- architecture exploration,
- early power/performance/area estimation,
- hardware/software partitioning,
- IP reuse,
- verification planning,
- reduced redesign,
- better time-to-market.

### Stages

```text
1. System requirements
2. System specification
3. Architecture exploration
4. Hardware/software partitioning
5. IP selection and platform definition
6. High-level modeling / ESL / TLM
7. RTL design and integration
8. Functional verification
9. Synthesis
10. Physical design
11. Timing/power/sign-off verification
12. Fabrication and post-silicon validation
```

### Stage Explanation

**System requirements:** decide what the product must do: performance, power, cost, interfaces, reliability and schedule.

**System specification:** convert requirements into precise functional and non-functional specifications.

**Architecture exploration:** compare processor choices, memory hierarchy, bus/NoC, accelerators and power domains.

**Hardware/software partitioning:** decide which functions run in software and which become hardware blocks.

**IP selection:** choose reusable cores such as CPU, DDR controller, USB, PCIe, DMA and peripherals.

**ESL/TLM modeling:** build fast executable models for early software and performance analysis.

**RTL implementation:** write or integrate synthesizable Verilog/VHDL/SystemVerilog.

**Verification:** check correctness using simulation, assertions, formal methods and coverage.

**Physical design:** convert logic into layout using synthesis, placement and routing.

**Sign-off:** check timing, power, DRC, LVS and equivalence.

**Post-silicon validation:** test real silicon using boards, testers and debug tools.

### Final Exam Answer

Top-down SoC design flow begins with system requirements and refines them into specification, architecture, hardware/software partitioning, IP selection, high-level models, RTL, verification, synthesis, physical design and silicon validation. Its significance is that it manages SoC complexity by considering system goals before individual implementation details. It supports early tradeoff analysis, IP reuse, verification planning, power/performance optimization and reduced redesign. In contrast to purely bottom-up design, top-down flow ensures that each block contributes to the final SoC requirements.

<a id="q3-asic-design-flow-and-eda-tools"></a>

## Q3. Write Brief Note On ASIC Design Flow And EDA Tools

**PYQ source:** MST 2024 Q1, MST 2025 Q4.

### ASIC Definition

**ASIC - Application-Specific Integrated Circuit** is a custom chip designed for a particular application.

### ASIC Design Flow

```text
Specification
     |
Architecture and microarchitecture
     |
RTL design
     |
Functional verification
     |
Logic synthesis
     |
DFT insertion
     |
Floorplanning and power planning
     |
Placement
     |
Clock tree synthesis
     |
Routing
     |
Static timing analysis
     |
Physical verification
     |
Equivalence checking
     |
GDSII tapeout
     |
Fabrication, packaging and test
```

### Important Stages

**Specification:** defines function, performance, power, area, interfaces and process node.

**RTL design:** describes hardware behavior using HDL.

**Functional verification:** checks RTL against specification.

**Synthesis:** converts RTL into gate-level netlist.

**DFT insertion:** adds scan chains, BIST and test structures.

**Floorplanning:** places major blocks and defines chip outline, power grid and IO placement.

**Placement:** places standard cells.

**CTS - Clock Tree Synthesis:** builds clock distribution network.

**Routing:** connects cells and blocks.

**STA - Static Timing Analysis:** checks timing without exhaustive simulation.

**DRC - Design Rule Check:** checks manufacturing design rules.

**LVS - Layout Versus Schematic:** checks layout matches netlist.

**GDSII:** final layout database sent for fabrication.

### EDA Tools

**EDA - Electronic Design Automation** tools automate chip design, verification and implementation.

EDA tool categories:

- HDL editors and simulators,
- lint tools,
- formal verification tools,
- synthesis tools,
- DFT tools,
- place-and-route tools,
- static timing tools,
- power analysis tools,
- physical verification tools,
- equivalence checkers.

### Final Exam Answer

ASIC design flow starts from specification and architecture, then proceeds to RTL design, functional verification, synthesis, DFT insertion, floorplanning, placement, clock tree synthesis, routing, timing analysis, physical verification and GDSII tapeout. EDA tools are essential because modern ASICs are too complex to design manually. They automate simulation, synthesis, timing analysis, power analysis, DFT, placement, routing, DRC, LVS and equivalence checking. The output of the flow is a manufacturable chip layout.

<a id="q4-asic-vs-soc-and-eda-tools"></a>

## Q4. What Is The Primary Distinction Between ASIC And SoC? Explain Role Of EDA Tools

**PYQ source:** MST 2025 Q3.

### ASIC Vs SoC

An ASIC is a custom chip designed for a specific application. An SoC is a complete system integrated on one chip.

An SoC can be an ASIC, but it is more system-oriented because it usually includes processors, memories, interconnect, peripherals, accelerators, debug/test logic and embedded software support.

### Comparison

| Point | ASIC | SoC |
|---|---|---|
| Meaning | Application-Specific Integrated Circuit | System on Chip |
| Scope | Custom chip/function | Complete system integrated on chip |
| Main focus | Dedicated hardware | Hardware + software + system integration |
| Components | Logic, memories, IO as needed | CPU, memory, bus/NoC, peripherals, accelerators |
| Software | May be absent | Usually essential |
| Example | Crypto chip, motor-control ASIC | Smartphone processor, automotive controller |

### Role Of EDA Tools

EDA tools enable:

- RTL simulation,
- synthesis,
- timing analysis,
- power analysis,
- physical design,
- DFT insertion,
- formal equivalence,
- DRC/LVS,
- sign-off verification.

### Final Exam Answer

The main distinction is that an ASIC is a custom integrated circuit for a particular application, while an SoC integrates a complete system on one chip, usually including processors, memory, interconnect, peripherals, accelerators and software support. Many SoCs are implemented as ASICs, but the term SoC emphasizes system integration. EDA tools are required to handle the complexity of both ASIC and SoC design by automating RTL verification, synthesis, timing analysis, power analysis, physical design, DFT and sign-off checks.

<a id="q5-soc-design-metrics-and-pdp"></a>

## Q5. What Are SoC Design Metrics? What Is The Significance Of PDP? Which Techniques Improve Metrics?

**PYQ source:** MST 2024 Q5, MST 2025 Q2, MST 2026 Q5.

### Definition

**SoC design metrics** are measurable criteria used to evaluate whether an SoC design is good for its target application.

### Main Metrics

**1. Performance:** speed, throughput, latency, clock frequency, instructions per second or frames per second.

**2. Power:** active power, leakage power, peak power and energy per operation.

**3. Area:** silicon area used by logic, memory, interconnect and IO.

**4. Cost:** die cost, packaging cost, test cost and NRE cost.

**5. Time-to-market:** time needed to complete and release the product.

**6. Reliability:** probability of correct operation over time under temperature, voltage and aging.

**7. Reusability:** ability to reuse IP, software, verification components and platform architecture.

**8. Portability:** ease of moving design/software to another process, platform or product.

**9. Functionality:** required features and correctness.

**10. Testability:** ease of manufacturing test and debug.

### PDP - Power Delay Product

**PDP - Power Delay Product** measures energy consumed per operation.

```text
PDP = Power x Delay
```

If delay is time per operation, then:

```text
Power x time = Energy
```

Significance:

- combines speed and power,
- lower PDP means less energy per operation,
- useful for comparing low-power designs,
- avoids optimizing only speed or only power.

### Techniques To Improve Metrics

| Metric | Improvement techniques |
|---|---|
| Performance | pipelining, parallelism, cache, accelerators, faster interconnect, better memory hierarchy |
| Power | clock gating, power gating, DVFS, multi-Vt cells, low-power modes, voltage scaling |
| Area | resource sharing, smaller memories, optimized datapaths, IP reuse |
| Cost | smaller die, better yield, fewer masks, lower test time |
| Reliability | ECC, redundancy, thermal management, voltage guardband, DFT |
| Time-to-market | IP reuse, platform-based design, automation, virtual platforms |
| Testability | scan, BIST, JTAG, ATPG, DFT planning |

### Final Exam Answer

SoC design metrics are criteria used to evaluate a design, including performance, power, area, cost, reliability, time-to-market, reusability, portability, functionality and testability. Power Delay Product is important because it combines power and delay into one energy-related metric. A design with low PDP performs an operation using less energy. SoC metrics can be improved using pipelining, parallelism, accelerators, cache optimization, clock gating, power gating, voltage/frequency scaling, resource sharing, IP reuse, DFT, platform-based design and efficient verification.

<a id="q6-five-chip-basics"></a>

## Q6. Explain In Detail The Five Chip Basics

**PYQ source:** MST 2026 Q4.

### The Five Chip Basics

In introductory SoC/chip design, the five basics can be written as:

1. **Time / performance**
2. **Area**
3. **Power**
4. **Reliability**
5. **Configurability**

### 1. Time / Performance

Performance measures how fast the chip completes work. It includes clock frequency, latency, throughput and response time.

Improved by:

- pipelining,
- parallelism,
- cache,
- accelerators,
- faster interconnect,
- better memory scheduling.

Tradeoff: higher performance often increases area and power.

### 2. Area

Area is the silicon space occupied by logic, memory, interconnect, IO and analog blocks.

Why it matters:

- larger die costs more,
- larger die may reduce yield,
- area affects package and routing.

Reduced by:

- resource sharing,
- optimized memories,
- smaller datapaths,
- IP reuse,
- careful floorplanning.

### 3. Power

Power includes dynamic power and leakage power. It affects battery life, heating, packaging and reliability.

Reduced by:

- clock gating,
- power gating,
- voltage scaling,
- DVFS,
- low-power memory modes,
- efficient accelerators.

### 4. Reliability

Reliability means correct operation over time under variations, temperature, aging and faults.

Improved by:

- ECC,
- redundancy,
- timing margins,
- thermal control,
- DFT,
- robust reset and clock design.

### 5. Configurability

Configurability means the ability to adapt the chip for different modes, products or applications.

Examples:

- programmable processor,
- configurable registers,
- firmware updates,
- reconfigurable accelerators,
- selectable clock and power modes.

Tradeoff: configurability improves flexibility but may increase area, verification effort and performance overhead.

### Final Exam Answer

The five chip basics are performance, area, power, reliability and configurability. Performance measures speed, latency and throughput. Area determines silicon cost and yield. Power affects energy consumption, heat and battery life. Reliability ensures correct operation under process, voltage, temperature, aging and fault conditions. Configurability allows the chip to support multiple modes, products or software-controlled behavior. Good SoC design balances these basics because improving one often worsens another.

<a id="q7-mst-2026-brief-notes"></a>

## Q7. Explain The Following In Brief: Deep Submicron Effects, SoC Components, Hardware Vs Software, Hardware/Software Co-Design, Top-Down Flow

**PYQ source:** MST 2026 Q1.

### (a) Deep Submicron Effects

Deep submicron effects are physical design problems that become serious when transistor dimensions become very small.

Important effects:

- interconnect delay becomes dominant,
- leakage power increases,
- crosstalk increases,
- signal integrity becomes difficult,
- process variation affects timing,
- electromigration affects reliability,
- clock skew becomes harder to control,
- power density and heating increase.

Exam line:

```text
In deep-submicron SoCs, wires, power, variation and reliability become as important as transistor logic.
```

### (b) Components Of An SoC System

An SoC contains:

- processors,
- memories,
- interconnect,
- peripherals,
- accelerators,
- DMA,
- interrupt controller,
- clock/reset/power management,
- debug and test logic,
- embedded software.

Exam line:

```text
An SoC integrates compute, storage, communication, control, I/O, test and software support on one chip.
```

### (c) Hardware Vs Software: Programmability Vs Performance

Software is programmable and flexible. It runs on processors and can be changed after fabrication. However, it may be slower for repetitive high-throughput tasks.

Hardware is less flexible but faster and more parallel. It is suitable for fixed high-performance functions such as encryption, video processing or signal processing.

Tradeoff:

```text
Software = flexibility
Hardware = performance and energy efficiency
```

### (d) Hardware/Software Co-Design

Hardware/software co-design jointly decides which functions should be software and which should be hardware.

It balances:

- performance,
- power,
- area,
- cost,
- flexibility,
- time-to-market.

Example: CPU runs control software, while a hardware accelerator performs repetitive video filtering.

### (e) Top-Down SoC Design Flow

Top-down flow starts from requirements, then refines to specification, architecture, partitioning, modeling, RTL, verification, physical design and silicon validation.

Memory line:

```text
Requirements -> Architecture -> Partitioning -> RTL -> Verification -> Physical design -> Silicon
```

### Combined Final Answer

Deep submicron effects make timing, leakage, crosstalk, variation and reliability critical in modern SoCs. A complete SoC contains processors, memories, interconnect, peripherals, accelerators, power/clock/reset logic, debug/test blocks and software. Hardware gives high performance and parallelism but is less flexible, while software gives programmability and easy updates but may be slower. Hardware/software co-design balances this by partitioning system functions between processors and hardware accelerators. A top-down SoC design flow begins with system requirements and refines them through architecture, partitioning, RTL, verification, physical design and silicon validation.
