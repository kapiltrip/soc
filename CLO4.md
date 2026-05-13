# CLO 4 - SoC Design Essentials and Design Methodologies

## Clickable Index

- [CLO 4 Master Definitions](#clo4-master-definitions)
- [CLO 4 Full-Form Review Addendum](#clo4-full-form-review)
- [Topic 1: SoC Design Essentials - Design Methodologies: TDD, BBD and PBD](#topic-1)
  - [Question](#topic-1-question)
  - [Main Explanation](#topic-1-explanation)
  - [Design Methodology Mental Model](#topic-1-mental-model)
  - [Why Methodology Is Needed](#topic-1-why-methodology)
  - [Evolution Of Methodologies](#topic-1-evolution)
  - [TDD - Timing Driven Design](#topic-1-tdd)
  - [BBD - Block Based Design](#topic-1-bbd)
  - [PBD - Platform Based Design](#topic-1-pbd)
  - [Which Methodology To Choose](#topic-1-selection-guide)
  - [Comparison Table](#topic-1-comparison)
  - [Final Exam-Ready Answer](#topic-1-final-answer)
  - [Technical Words](#topic-1-technical-words)
  - [Images / Diagrams](#topic-1-diagrams)
- [Topic 2: Hardware-Software Co-Design](#topic-2)
  - [Question](#topic-2-question)
  - [Main Explanation](#topic-2-explanation)
  - [Hardware Vs Software Implementation](#topic-2-hw-vs-sw)
  - [HW/SW Partitioning](#topic-2-partitioning)
  - [Co-Design Flow](#topic-2-flow)
  - [ESL And TLM Models](#topic-2-esl-tlm)
  - [Interfaces Between Hardware And Software](#topic-2-interfaces)
  - [Final Exam-Ready Answer](#topic-2-final-answer)
  - [Technical Words](#topic-2-technical-words)
  - [Images / Diagrams](#topic-2-diagrams)
- [Topic 3: Co-Design Vs Co-Simulation](#topic-3)
  - [Question](#topic-3-question)
  - [Main Explanation](#topic-3-explanation)
  - [Comparison Table](#topic-3-comparison)
  - [How Co-Simulation Works](#topic-3-how-cosim-works)
  - [Final Exam-Ready Answer](#topic-3-final-answer)
  - [Technical Words](#topic-3-technical-words)
  - [Images / Diagrams](#topic-3-diagrams)
- [Topic 4: Architectural Models](#topic-4)
  - [Question](#topic-4-question)
  - [Main Explanation](#topic-4-explanation)
  - [Types Of Architectural Models](#topic-4-types)
  - [Function-Architecture Mapping](#topic-4-mapping)
  - [TLM And Abstraction Levels](#topic-4-tlm)
  - [Final Exam-Ready Answer](#topic-4-final-answer)
  - [Technical Words](#topic-4-technical-words)
  - [Images / Diagrams](#topic-4-diagrams)

<a id="clo4-master-definitions"></a>

## CLO 4 Master Definitions

Use this section before revising CLO 4 answers. For this CLO, always learn the **full form**, **what it means**, and **why it appears in an SoC design answer**.

| Term | Full Form / Meaning | Definition / Why It Matters |
|---|---|---|
| CLO | Course Learning Outcome | The syllabus outcome used to group topics and expected exam answers. |
| SoC | System on Chip | Complete system integrated on one chip, including processor, memory, interconnect, IP blocks, peripherals and often embedded software. |
| Methodology | Organized design approach | A planned way of designing a chip so that complexity, timing, area, power, verification and time-to-market are controlled. |
| TDD | Timing Driven Design | Design methodology where timing closure and delay minimization strongly guide synthesis, floorplanning and physical design. |
| BBD | Block Based Design | Hierarchical design methodology where the SoC is divided into functional blocks with timing, power and area budgets. |
| PBD | Platform Based Design | Design methodology based on planned reuse of preverified blocks, standard interfaces and reusable platform architecture. |
| ADD | Area Driven Design | Older methodology where reducing chip area was the main goal. It became insufficient when timing/performance became dominant. |
| ASIC | Application-Specific Integrated Circuit | Custom chip designed for a specific application; often the target of SoC methodologies. |
| DSM | Deep Sub-Micron | Very small semiconductor technology generation where wire delays, timing closure, power and physical effects become difficult. |
| EDA | Electronic Design Automation | Software tools for synthesis, simulation, floorplanning, place-and-route, STA, verification and sign-off. |
| RTL | Register Transfer Level | Hardware design abstraction written in Verilog, SystemVerilog or VHDL before synthesis. |
| HDL | Hardware Description Language | Language such as Verilog or VHDL used to describe hardware behavior/structure. |
| IP | Intellectual Property | Reusable design block such as CPU, memory controller, USB, UART, DSP, PLL or accelerator. |
| VC | Virtual Component | Reusable design component/IP block used in SoC design methodology discussions. |
| TTM | Time To Market | Time required to bring a product from concept to market; a major reason for reuse and platform-based design. |
| Linchpin technology | Indispensable enabling technology | Key procedure/tool capability required for a design methodology to work effectively. |
| Floorplanning | Early physical placement planning | Decides approximate block placement and chip organization to estimate area, wire length and timing. |
| STA | Static Timing Analysis | Timing verification technique that checks paths without exhaustive simulation. Crucial in TDD. |
| Synthesis | RTL-to-gate transformation | Converts RTL/behavioral descriptions into gate-level logic while optimizing timing, area and power. |
| Place and Route / P&R | Physical implementation step | Places standard cells/macros and routes wires; strongly affects timing and power. |
| Timing closure | Meeting all timing constraints | Process of ensuring all paths satisfy required clock timing after synthesis/physical design. |
| Timing budget | Allocated timing target | Timing limit assigned to a block or interface so the whole chip can meet its clock target. |
| Power budget | Allocated power target | Power limit assigned to a block/subsystem to control total SoC power. |
| Area budget | Allocated silicon-area target | Area limit assigned to a block/subsystem to control die size and cost. |
| Critical path | Slowest timing path | Path with the least timing margin; it usually decides whether the design can meet the target clock period. |
| Slack | Timing margin | Positive slack means timing is met; negative slack means the path is too slow and timing fails. |
| Setup time | Data-before-clock requirement | Minimum time data must be stable before the capturing clock edge at a flip-flop. |
| Hold time | Data-after-clock requirement | Minimum time data must remain stable after the capturing clock edge at a flip-flop. |
| Clock skew | Difference in clock arrival time | Clock reaches different flip-flops at slightly different times, affecting setup and hold margins. |
| ECO | Engineering Change Order | Late design change used to fix bugs or timing issues with minimum disruption. |
| Hierarchical design | Divide-and-integrate approach | Large design is divided into blocks/subsystems to reduce complexity and allow parallel team work. |
| Design reuse | Reusing existing blocks or platforms | Reduces design effort, verification effort and time-to-market. |
| Standard interface | Agreed communication boundary | Interface such as AMBA AXI/APB or a documented block protocol that enables reuse and integration. |
| IP-XACT | IEEE 1685 IP metadata standard | Standard structure for packaging, integrating and reusing IP within tool flows. |
| AMBA | Advanced Microcontroller Bus Architecture | Arm bus/interconnect family commonly used in SoCs. |
| AXI | Advanced eXtensible Interface | High-performance AMBA interface often used for memory-mapped SoC blocks. |
| APB | Advanced Peripheral Bus | Simpler AMBA peripheral interface used for low-bandwidth register/peripheral access. |
| Top-down design | System-first design approach | Start from requirements/specification and refine down to architecture, blocks, RTL and physical implementation. |
| Bottom-up design | Block-first design approach | Start by designing lower-level blocks and integrate them later; can expose system errors late. |
| Platform | Reusable architecture base | Predefined architecture, interfaces, software layers and verified IP blocks used to build related products. |
| Platform stack | Layered platform abstraction | Hardware architecture platform plus software/API platform that hides lower-level details and enables reuse. |
| Derivative product | Product variant | New SoC created by modifying a reusable platform rather than starting from scratch. |
| NRE | Non-Recurring Engineering cost | One-time engineering cost of designing, verifying and taping out a chip. Reuse reduces this cost across products. |
| Block authoring | Creating reusable blocks | Designing IP blocks with clean interfaces and deliverables so they can be reused across systems. |
| System-chip integration | SoC-level integration | Combining blocks, interfaces, software and verification into a complete chip. |
| Co-design | Joint hardware/software design | Hardware and software are designed together, with partitioning and tradeoffs considered early. |
| Co-simulation | Joint simulation of models | Hardware and software models are simulated together to check behavior before final implementation. |
| ESL | Electronic System Level | System-design abstraction above RTL where designers model whole-system behavior, hardware/software partitioning, architecture choices and performance before detailed RTL exists. |
| TLM | Transaction-Level Modeling | Modeling style where communication is represented as abstract transactions such as read, write or burst transfer instead of pin-level signal toggles. |
| HW/SW partitioning | Hardware/software partitioning | Decision process that assigns each system function either to hardware or to software based on performance, power, cost, flexibility and real-time constraints. |
| Functional model | What the system does | Executable or descriptive model of required behavior before deciding the final hardware/software architecture. |
| Architectural model | How the system is organized | Abstract model of processors, memories, buses, accelerators, peripherals, RTOS and communication used to evaluate design alternatives. |
| Virtual platform | Executable system model | Software-runnable model of an SoC platform, often built with SystemC/TLM, used for early software development and architecture exploration before silicon. |
| Transaction | Abstract communication operation | High-level operation such as read, write, burst, interrupt or DMA transfer, carrying fields like address, data, command, response and timing delay. |
| Initiator | TLM transaction starter | Component such as CPU, DMA or accelerator that starts a transaction. Similar to a bus master. |
| Target | TLM transaction receiver | Component such as memory, peripheral or register block that responds to a transaction. Similar to a bus slave. |
| LT | Loosely Timed | TLM style that prioritizes fast simulation with limited timing detail, useful for early software development and virtual platforms. |
| AT | Approximately Timed | TLM style with more timing/resource-ordering detail than LT, useful for architecture/performance analysis. |
| Temporal decoupling | Fast TLM simulation technique | Allows a model to run ahead of global simulation time and synchronize later, reducing simulation overhead. |
| DMI | Direct Memory Interface | TLM speed feature allowing a model to access modeled memory directly, bypassing normal interconnect calls when safe. |
| Cycle-accurate model | Cycle-by-cycle model | Model that represents behavior at each clock cycle; more accurate than TLM but usually slower. |
| Bit-accurate model | Exact data-value model | Model that produces exact bit-level values even if timing is abstract. |
| Timed model | Model with timing annotation | Model that includes delays/latencies so performance can be estimated. |
| Untimed model | Model without timing detail | Model that checks functional behavior only, usually fastest but not useful for timing/performance conclusions. |
| Model of computation / MoC | Execution and communication rule | Defines how functional blocks execute and communicate, such as sequential execution, dataflow, finite-state machines or concurrent tasks. |
| DSE | Design Space Exploration | Comparing architecture alternatives, partitioning choices and parameters before final RTL/software implementation. |
| Performance model | Timing/throughput estimate model | Model used to estimate latency, throughput, bandwidth, utilization and bottlenecks before detailed implementation. |
| ISS | Instruction Set Simulator | Simulator that runs processor instructions in software to model how embedded code behaves on a target CPU. |
| SystemC | C++ based system modeling language | Commonly used for ESL and TLM modeling of hardware/software systems at high abstraction levels. |
| RTOS | Real-Time Operating System | Operating system used in embedded systems where task scheduling, interrupts and timing deadlines matter. |
| HAL | Hardware Abstraction Layer | Low-level software layer that hides hardware details from OS/application software and improves portability. |
| BSP | Board Support Package | Hardware-dependent software package that initializes board/SoC hardware and adapts an operating system to a platform. |
| API | Application Programming Interface | Defined software interface used by upper software layers to access services without knowing implementation details. |
| Device driver | Hardware-control software | Software that controls a hardware peripheral through registers, interrupts, DMA and protocol-specific operations. |
| Memory-mapped I/O | Register access through address map | Technique where hardware registers are accessed by software using normal load/store instructions to specific addresses. |
| Interrupt | Hardware event signal | Signal/event that tells the processor that a peripheral or hardware block needs service. |
| ISR | Interrupt Service Routine | Software routine executed when an interrupt occurs. |
| DMA | Direct Memory Access | Hardware engine that transfers data between memory and peripherals/accelerators without the CPU copying every word. |
| Accelerator | Dedicated hardware engine | Physical hardware block inside the SoC that performs one specific heavy task faster, with lower latency or with lower energy than running the same task as software on a general CPU. |
| MMU | Memory Management Unit | Hardware block that translates virtual addresses to physical addresses and enforces memory protection. |
| Bus bridge | Interconnect adapter | Hardware block that connects two bus protocols, widths, speeds or clock domains. |
| CPU | Central Processing Unit | Main processor that runs software and starts transactions in architectural/co-design models. |
| SRAM | Static Random Access Memory | Fast on-chip memory used for caches, buffers, scratchpads and local storage. |
| DRAM | Dynamic Random Access Memory | Dense main memory technology usually reached through a memory controller. |
| Cache | Hardware-managed fast copy memory | Reduces average instruction/data access time and affects hardware/software performance tradeoffs. |
| Memory controller | Memory protocol controller | Hardware that converts SoC memory requests into legal external memory commands and timing. |
| HLS | High-Level Synthesis | Tool flow that can generate RTL hardware from higher-level algorithmic descriptions. |
| QoS | Quality of Service | Policy support for latency, bandwidth, priority or fairness in interconnect/memory systems. |
| HW | Hardware | Physical circuits such as processors, memories, buses, accelerators and peripherals. |
| SW | Software | Program code running on processors, including firmware, drivers, RTOS and applications. |

Memory line for CLO 4:

```text
TDD controls timing closure.
BBD controls complexity using hierarchical blocks and budgets.
PBD controls time-to-market using planned reuse and standardized platforms.
```

<a id="clo4-full-form-review"></a>

## CLO 4 Full-Form Review Addendum

For CLO 4, the full forms are not enough. You must explain why each method/model exists.

**TDD - Timing Driven Design** exists because delay and timing closure became dominant SoC problems. In this method, timing constraints influence synthesis, floorplanning, placement, routing and static timing analysis from the beginning.

**BBD - Block Based Design** exists because one huge flat SoC is too complex for one team to design and close at once. The chip is divided into blocks with timing, area and power budgets, then integrated hierarchically.

**PBD - Platform Based Design** exists because repeated redesign wastes time. A reusable platform gives preverified processors, interconnects, memories, software layers and interfaces so derivative products can be made faster.

**ESL - Electronic System Level** and **TLM - Transaction-Level Modeling** exist because RTL - Register Transfer Level simulation is too slow for early architecture exploration. ESL/TLM models let designers test hardware/software partitioning, bus traffic, memory bottlenecks and software boot behavior before detailed RTL is complete.

**HW/SW - Hardware/Software partitioning** is the decision of which functions become physical hardware and which remain software. Put repeated, parallel, deadline-critical work into hardware accelerators; keep control, configuration and changing behavior in software.

<a id="topic-1"></a>

## Topic 1: SoC Design Essentials - Design Methodologies: TDD, BBD and PBD

<a id="topic-1-question"></a>

### Question

**Explain SoC design methodologies: TDD, BBD and PBD.**

### CLO Mapping

This topic belongs to **CLO 4: Analyze the Design Methodologies of SoC; TLM and its need in SoC Design**.

Reason: The syllabus lists **SoC Design Essentials: Design Methodologies - TDD, BBD, PBD** under the design-essentials part of the course. The CLO also explicitly says students must analyze SoC design methodologies.

### What The Question Is Asking

The examiner is not asking for only the full forms of TDD, BBD and PBD. A full answer must explain why design methodology changed as SoCs became more complex.

For full marks, answer in this order:

1. Define design methodology in SoC.
2. Explain why SoC design needs methodology.
3. Show the evolution from ADD to TDD to BBD to PBD.
4. Explain TDD with linchpin technologies, benefits and limitations.
5. Explain BBD with block partitioning, budgets, floorplanning and integration.
6. Explain PBD with planned reuse, standardized interfaces and platform architecture.
7. Compare TDD, BBD and PBD.
8. Draw a methodology evolution diagram or comparison table.

<a id="topic-1-explanation"></a>

### Main Explanation

**SoC design methodology** means the organized process used to convert requirements into a working System on Chip while controlling complexity, timing, area, power, verification effort and time-to-market.

An SoC is not just random logic. It may contain CPUs, DSPs, memory controllers, buses, Network-on-Chip interconnect, accelerators, analog blocks, embedded software, third-party IP and test structures. If each part is designed independently without a methodology, the chip may fail because of timing violations, interface mismatches, excessive power, integration errors or late verification failures.

So design methodology answers:

```text
How should the SoC be planned, partitioned, implemented, verified and integrated
so that timing, area, power, cost and schedule targets are met?
```

The three important methodologies in this topic are:

- **TDD - Timing Driven Design**.
- **BBD - Block Based Design**.
- **PBD - Platform Based Design**.

These methodologies evolved because design problems changed over time. Early designs were limited mainly by chip area. Later, timing and performance became harder. Then chip complexity and integration became the bigger problem. Finally, time-to-market and reuse became central.

### PPT / Book Citation

The direct PPT source is [14-SOC Design Methodologies.pdf](<System on chip/14-SOC Design Methodologies.pdf>). Page 3 explains the evolution from area-driven design to TDD, BBD and PBD. Page 5 lists the three primary methods: Timing Driven Design, Block Based Design and Platform Based Design. Pages 7-10 explain TDD, pages 11-15 explain BBD, and pages 16-20 explain PBD and their comparison. For design-flow context, [SOC Design Flow.pdf, p.2](<System on chip/SOC Design Flow.pdf#page=2>) and p.3 discuss top-down/bottom-up design flow. For system-level design context, [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.44](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=44>) and p.45 explain requirements, specifications and design iteration.

Detailed source notes, including web references for AMBA, IP-XACT and platform-based design, are kept in [sources/CLO4_Topic1_sources.md](<sources/CLO4_Topic1_sources.md>).

<a id="topic-1-mental-model"></a>

### Design Methodology Mental Model

Think of an SoC design methodology as a **control system for chip development**. The input is a product requirement. The output is a manufacturable, verified SoC. The methodology controls the steps in between so that the final chip does not fail due to timing, area, power, verification, integration or schedule problems.

```text
Requirements
    |
    v
System architecture
    |
    v
Partitioning into hardware, software and blocks
    |
    v
RTL / IP / software development
    |
    v
Verification and physical implementation
    |
    v
Tapeout-ready SoC
```

The word **methodology** is important because designing an SoC is not just writing Verilog or connecting IP blocks. It includes decisions about:

- **abstraction level**: system model, architectural model, RTL, gate level or physical layout,
- **partitioning**: deciding blocks, subsystems and hardware/software split,
- **constraints**: timing, area, power, test, cost and packaging limits,
- **reuse**: choosing whether to create new logic or reuse existing IP/platforms,
- **integration**: connecting blocks with compatible interfaces and protocols,
- **verification**: proving that each block and the complete SoC behave correctly,
- **iteration**: going back when performance, timing or power targets are not met.

The Flynn/Luk textbook supports this way of thinking by treating SoC design as an iterative process: requirements lead to specifications, an initial design is evaluated, and the design is improved until it meets the required constraints. The course design-flow PPT also supports this because top-down flow starts with system-level models and a verification environment so that major issues are found early.

#### The Three Levels Of The Topic

This topic is easier if you remember that TDD, BBD and PBD solve **different dominant problems**.

| Methodology | Dominant Problem | What The Methodology Controls |
|---|---|---|
| TDD - Timing Driven Design | The chip may not meet speed/timing | Critical paths, constraints, floorplan, STA, timing closure |
| BBD - Block Based Design | The chip is too complex to design flat | Block partitioning, budgets, interfaces, integration |
| PBD - Platform Based Design | Product must be built quickly with reuse | Reusable platform, standard interfaces, IP reuse, derivative products |

This is why your answer should not treat them as unrelated definitions. They are an evolution of design thinking:

```text
When area was the main problem -> ADD
When timing became the main problem -> TDD
When complexity became the main problem -> BBD
When reuse and time-to-market became the main problem -> PBD
```

#### Constraints That Drive Methodology

Every SoC methodology exists because of constraints.

| Constraint | Meaning | Methodology Connection |
|---|---|---|
| Functional correctness | SoC must implement required behavior | All methodologies need verification |
| Timing | Signals must arrive within clock period | TDD is mainly about timing closure |
| Area | Silicon size must be controlled | ADD and block budgets address this |
| Power | Dynamic/leakage power must fit limits | BBD/PBD use power budgets and reusable low-power structures |
| Performance | System must meet throughput/latency targets | TDD checks paths; BBD/PBD check system architecture |
| Integration | Blocks must connect correctly | BBD and PBD strongly focus on interfaces |
| Reuse | Existing verified work should be reused | PBD is built around planned reuse |
| TTM - Time To Market | Product must finish on schedule | BBD improves parallel work; PBD improves reuse speed |
| NRE - Non-Recurring Engineering cost | One-time design cost must be controlled | PBD spreads platform cost across many derivative products |

Exam line: **TDD, BBD and PBD are not only implementation flows; they are ways of controlling the dominant SoC design risk at that stage of design evolution.**

<a id="topic-1-why-methodology"></a>

### Why Methodology Is Needed

SoC design needs methodology because SoC design has many competing constraints:

- **Functionality**: the chip must implement the required behavior.
- **Timing**: the chip must meet clock frequency and path delays.
- **Area**: the chip must fit in acceptable silicon area.
- **Power**: dynamic and leakage power must be within limits.
- **Cost**: die size, mask cost, verification effort and engineering effort must be controlled.
- **Verification**: hardware and software must be checked before fabrication.
- **Reuse**: existing IP should be reused safely to reduce time and risk.
- **Integration**: blocks must communicate correctly through standard interfaces.
- **TTM - Time To Market**: product must be finished fast enough to be commercially useful.

Without methodology:

- timing closure may fail late,
- interfaces may not match,
- blocks may not meet system budgets,
- verification may become unmanageable,
- physical design may require many iterations,
- design teams may duplicate work,
- product release may be delayed.

The Flynn/Luk book supports this general idea by emphasizing requirements, specifications and design iteration. The designer starts with requirements, converts them into specifications, studies alternatives, and iterates toward an efficient design. That is exactly what a methodology organizes.

Exam line: **A design methodology is needed because SoC design is too complex to be handled as one flat RTL design; methodology controls timing, hierarchy, reuse, verification and time-to-market.**

<a id="topic-1-evolution"></a>

### Evolution Of SoC Design Methodologies

The PPT explains this evolution:

```text
1980s: ADD - Area Driven Design
       Main goal: minimize silicon area

1990s: TDD - Timing Driven Design
       Main goal: meet performance/timing constraints

2000s: BBD - Block Based Design
       Main goal: manage larger design complexity using reusable blocks

Later: PBD - Platform Based Design
       Main goal: planned reuse and faster derivative products
```

#### ADD - Area Driven Design

**ADD - Area Driven Design** is the older methodology where the main objective was to reduce chip area. This made sense when fabrication processes had large feature sizes and area was the dominant limitation.

Why ADD became insufficient:

- clock frequencies increased,
- wire delays became important,
- performance became a key product goal,
- area minimization alone could not guarantee timing closure.

This led to **TDD - Timing Driven Design**.

#### Linchpin Technology

The PPT uses the term **linchpin technology**. A linchpin is something indispensable. In design methodology, a linchpin technology is the tool/procedure without which that methodology cannot work well.

Example:

```text
TDD needs static timing analysis and floorplanning.
BBD needs block-level planning, budgeting and block integration.
PBD needs planned reuse, standard interfaces and reusable platforms.
```

Exam line: **Linchpin technologies are the enabling procedures/tools that make a design methodology practical and successful.**

<a id="topic-1-tdd"></a>

### TDD - Timing Driven Design

**TDD** means **Timing Driven Design**. It is a methodology where timing constraints and delay minimization guide the design flow from RTL through synthesis and physical design.

TDD became important when designers could no longer optimize only for area. In deep sub-micron technologies, wire delay, gate delay, clock frequency and timing closure became critical. The design had to be optimized so that signals reached their destinations within the clock period.

Important definition:

```text
TDD = design methodology where timing closure is the main driver
for synthesis, floorplanning, static timing analysis and physical design.
```

#### Where TDD Fits

TDD is suitable for:

- moderately sized ASICs,
- designs with mostly new logic,
- designs with limited reuse,
- designs where timing closure is difficult but hierarchy is still manageable,
- designs where a floorplan-centric method can control delay.

The PPT states that TDD is suitable for moderately sized and complex ASICs, especially when the design consists mainly of new logic and has little reuse.

#### How TDD Works

Typical TDD flow:

```text
Specification
      |
      v
RTL design
      |
      v
Timing constraints
      |
      v
Synthesis with timing goals
      |
      v
Floorplanning and delay estimation
      |
      v
Static timing analysis
      |
      v
Timing optimization
      |
      v
Place and route
      |
      v
Timing closure/sign-off
```

TDD tries to avoid discovering timing problems too late. Timing is checked and optimized repeatedly.

#### What Timing Closure Actually Means

**Timing closure** means all timing paths in the design meet the required timing constraints after synthesis, placement and routing.

In a synchronous digital chip, data usually moves like this:

```text
launch flip-flop -> combinational logic + wires -> capture flip-flop
```

For correct operation, data must arrive at the capture flip-flop before the next clock edge with enough setup margin, and it must not change too soon after the capture clock edge.

The basic idea is:

```text
available clock time >= data path delay + setup time + clock uncertainty
```

If the data path is too slow, the design has a **setup violation**. If data changes too quickly after the clock edge, the design has a **hold violation**.

Key timing terms:

| Term | Meaning | Why It Matters In TDD |
|---|---|---|
| Clock period | Time available for one cycle | Smaller clock period means harder timing closure |
| Critical path | Slowest or most timing-limited path | Optimization focuses first on critical paths |
| Setup violation | Data arrives too late before clock edge | Chip may sample wrong value at high frequency |
| Hold violation | Data changes too soon after clock edge | Chip may sample new data when old data was expected |
| Slack | Timing margin | Negative slack means timing fails |
| Clock skew | Difference in clock arrival times | Can help or hurt setup/hold timing |
| Wire delay | Delay due to interconnect wires | Becomes very important in DSM technologies |

This is why TDD cannot be only a logic-level method. It must care about physical design, because wire length, block placement and routing congestion affect timing.

#### TDD Optimization Actions

When TDD finds timing problems, designers may fix them using:

- **logic optimization**: simplifying logic on the critical path,
- **gate sizing**: using stronger cells to drive signals faster,
- **buffer insertion**: adding buffers to drive long wires,
- **pipelining**: adding registers so a long operation is split across cycles,
- **retiming**: moving registers to balance delay,
- **floorplan change**: moving communicating blocks closer,
- **clock-tree adjustment**: reducing harmful skew and uncertainty,
- **constraint correction**: declaring false paths or multicycle paths when valid,
- **ECO - Engineering Change Order**: late localized fix after implementation.

Be careful: not all timing fixes are free. Gate sizing and buffering may increase area and power. Pipelining can change latency and may require RTL changes. Floorplan changes may affect routing and integration. Therefore TDD is about balancing timing with area, power and schedule.

#### TDD Example

Suppose a block must run at 500 MHz.

```text
Clock period = 1 / 500 MHz = 2 ns
```

If a path has:

```text
combinational logic delay = 1.4 ns
wire delay                = 0.5 ns
setup + uncertainty       = 0.3 ns
total needed              = 2.2 ns
```

The path fails because it needs 2.2 ns but only 2.0 ns is available.

TDD may fix this by:

- shortening wire delay through better floorplanning,
- optimizing logic gates,
- inserting a pipeline register,
- reducing clock uncertainty,
- changing constraints if the path is truly multicycle.

Exam line: **TDD means timing is not checked only at the end; timing constraints guide synthesis, floorplanning, physical design and optimization throughout the flow.**

#### TDD Linchpin Technologies

The PPT lists key linchpin technologies for TDD.

##### 1. Interactive Floorplanning Tools

**Floorplanning** decides approximate placement of major blocks and estimates wire delays early. This matters because in modern chips, wire delay can dominate timing. If blocks are placed too far apart, timing may fail even if logic gates are fast.

Why needed:

- gives early area and delay estimates,
- reduces mismatch between synthesis and place-and-route,
- helps timing convergence,
- shows whether the physical layout is realistic.

##### 2. Static Timing Analysis

**STA - Static Timing Analysis** checks whether timing paths meet clock constraints without simulating all input patterns. It identifies setup/hold violations and critical paths.

Why needed:

- quickly finds timing problems,
- avoids relying only on slow gate-level timing simulation,
- supports full-chip timing checks,
- guides optimization.

##### 3. Behavioral Synthesis / Datapath Compilers

Behavioral synthesis and datapath compilers move design to a higher abstraction while preserving timing predictability for datapath-heavy blocks.

Why needed:

- improves designer productivity,
- enables faster datapath exploration,
- supports better timing/performance tradeoffs at a higher level.

#### Benefits Of TDD

- Good for timing-focused ASIC design.
- Floorplan-centric approach reduces timing surprises.
- STA makes timing checking faster and more systematic.
- Netlist handoff is well understood.
- RAM/ROM blocks can be included as cells/macros.
- Test generation can be more uniform and automatic.
- Suitable for small soft VC/IP blocks.

#### Challenges Of TDD

- Flat design begins to fail as complexity grows.
- Large designs may need many loops between synthesis, timing analysis and place-and-route.
- RTL changes late in the flow are hard to incorporate.
- Wire-load models may be inaccurate for high-performance or low-power designs.
- It does not fully solve integration and reuse problems.
- It is less suitable for very large SoCs with many IP blocks and teams.

#### Why TDD Alone Is Not Enough For Large SoCs

TDD is strong when timing is the main difficulty, but a modern SoC also has system-level problems that timing tools cannot solve alone.

Examples:

- STA can tell that a path meets timing, but it cannot prove the CPU programmed a DMA register correctly.
- Floorplanning can reduce wire delay, but it cannot guarantee two third-party IP blocks follow the same bus protocol assumptions.
- Synthesis can optimize a datapath, but it cannot decide whether a video function should be hardware or software.
- Timing closure can pass, but the full-chip may still fail because of memory bandwidth, interrupt routing, reset sequencing or software-driver bugs.

So TDD is necessary inside blocks, but SoC design also needs BBD for hierarchy and PBD for reuse/platform integration.

Exam line: **TDD is timing-closure focused; it is strong for moderately complex ASICs but becomes insufficient when SoC complexity, reuse and integration dominate.**

<a id="topic-1-bbd"></a>

### BBD - Block Based Design

**BBD** means **Block Based Design**. It is a hierarchical methodology where the SoC is divided into functional blocks or subsystems. Each block is designed, verified and optimized under assigned timing, area and power budgets.

Important definition:

```text
BBD = hierarchical SoC design methodology where the system is partitioned
into functional blocks, and each block is designed to timing, power and area budgets.
```

#### Why BBD Was Needed

TDD works well when a design can still be treated mostly as one timing-driven design. But as SoCs became larger, this became difficult. More blocks, more teams, more interfaces, more software and more verification complexity required a hierarchical method.

BBD became necessary because:

- design size increased,
- system-level functions became more complex,
- multiple teams worked on different parts,
- interface timing errors increased,
- testbench complexity increased,
- reuse of existing blocks became attractive,
- flat timing-driven design did not scale.

The PPT specifically says BBD is appropriate when subsystems such as embedded processing, compression and error correction are required and multiple teams work on specific parts of the design.

#### How BBD Works

Typical BBD flow:

```text
System specification
      |
      v
System-level behavioral model
      |
      v
Partition into functional blocks
      |
      v
Assign timing / power / area budgets
      |
      v
Design each block at RTL or lower level
      |
      v
Verify each block
      |
      v
Integrate blocks at SoC level
      |
      v
Verify interfaces and full system
```

#### What Is A Block?

A **block** is a meaningful subsystem or IP region inside the SoC. Examples:

- CPU subsystem,
- memory controller,
- video decoder,
- image processor,
- DSP subsystem,
- bus/interconnect block,
- DMA controller,
- security engine,
- error-correction block.

BBD does not mean randomly cutting the chip into pieces. Blocks must be partitioned according to function, interfaces, timing, physical placement and team ownership.

#### Budgets In BBD

BBD depends heavily on budgets.

| Budget | Meaning | Why It Matters |
|---|---|---|
| Timing budget | Allowed delay for block/internal paths/interfaces | Prevents late timing failure |
| Area budget | Allowed silicon area for the block | Controls die size and cost |
| Power budget | Allowed power consumption for the block | Controls thermal and battery limits |
| Interface budget | Timing/protocol assumptions at block boundary | Prevents integration mismatch |
| Verification budget | Required tests/coverage for the block | Prevents unverified integration |

If budgets are unrealistic, integration fails. For example, if one block consumes too much timing margin, another block may not meet full-chip frequency.

#### Why BBD Is More Than Dividing RTL Files

In exams, do not write BBD as only "divide the design into blocks." That is too shallow. BBD is a complete management method for a large chip.

In a real SoC, a block boundary becomes a contract. The block owner must know:

- what function the block performs,
- what input/output interface it exposes,
- what clock and reset it uses,
- what protocol timing it follows,
- what latency and bandwidth it must support,
- how much area and power it may consume,
- what timing delay it is allowed at its boundary,
- what verification evidence must be delivered.

This contract matters because different teams may design different blocks at the same time. If the CPU subsystem team assumes a 2-cycle memory response and the memory-controller team delivers a 10-cycle response, both blocks may be individually correct but the SoC may miss performance. If a bus interface assumes active-low reset while another block assumes active-high reset, integration can fail. BBD tries to prevent this by making block boundaries, budgets and interface assumptions explicit early.

#### Example Of BBD In An SoC

Suppose the SoC is a multimedia SoC. It may be divided into these blocks:

| Block | Responsibility | Example Budget / Interface Concern |
|---|---|---|
| CPU subsystem | Runs control software and operating system | Clock frequency, cache size, interrupt lines |
| Memory subsystem | Connects to SRAM/DRAM and handles memory traffic | Bandwidth, latency, refresh timing |
| Video accelerator | Performs video decoding/encoding | Throughput, input/output buffer rate |
| DMA controller | Moves data between memory and peripherals | Bus-master behavior, priority, address range |
| Interconnect | Connects masters and slaves | Arbitration, bandwidth, protocol compliance |
| Peripheral subsystem | UART, SPI, I2C, timers and GPIO | Register map, interrupts, low power behavior |

BBD allows each block team to work separately, but the SoC team must still verify the combined behavior. This is why BBD always has two levels of verification:

1. **Block-level verification**: checks whether each block works by itself.
2. **Integration/system verification**: checks whether the blocks work correctly together.

Exam line: **In BBD, a block is not just a piece of code; it is a planned subsystem with functional responsibility, interface contract, timing budget, area budget, power budget and verification responsibility.**

#### How Block Budgets Are Created

Block budgets are not guessed randomly. They are derived from full-chip goals.

Example:

```text
Full-chip clock target = 1 GHz
Clock period           = 1 ns
```

If a signal path crosses from Block A to Block B, the SoC team may divide the available time:

```text
Block A output delay      = 0.35 ns
Top-level routing delay   = 0.20 ns
Block B input/setup time  = 0.25 ns
Margin                    = 0.20 ns
Total                     = 1.00 ns
```

This becomes a timing contract. Block A must deliver its output within its assigned budget. Block B must accept input within its assigned budget. The top-level integrator must keep routing delay within the assigned budget.

The same idea applies to power and area:

```text
Full SoC power budget = 2 W
CPU subsystem         = 600 mW
GPU/video block       = 500 mW
Memory subsystem      = 400 mW
Peripherals           = 200 mW
Interconnect/others   = 300 mW
```

If one block exceeds its budget, the full chip may exceed the thermal or battery limit. This is why BBD is deeply connected to system planning.

#### Block Handoff Package

In BBD, a block team should deliver more than RTL. A proper block handoff package may include:

- RTL source code,
- block specification,
- interface/protocol document,
- timing constraints,
- area and power estimates,
- clock and reset description,
- register map if software-visible,
- verification plan and coverage report,
- testbench or verification components,
- synthesis scripts,
- physical abstract or floorplan view,
- integration guide,
- known limitations and assumptions.

This is important because the SoC integration team cannot safely integrate a block if it only receives code without constraints and assumptions.

#### Interface Contract In BBD

An **interface contract** describes exactly how one block communicates with another block.

It should define:

- signal names and directions,
- clock and reset behavior,
- valid/ready handshake rules,
- data width and byte ordering,
- burst length rules,
- latency assumptions,
- error response behavior,
- backpressure behavior,
- power-state behavior,
- test/debug access.

Many SoC bugs happen at interfaces, not inside the main datapath. A block may be correct internally but fail because the other block interprets the interface differently.

Exam line: **BBD succeeds only when block boundaries are treated as engineering contracts, not informal connections.**

#### BBD Linchpin Technologies

##### 1. High-Level System Algorithmic Analysis

Before committing to RTL, designers model algorithms and system behavior. This helps evaluate hardware/software tradeoffs and functional partitioning.

##### 2. Integrated Synthesis And Physical Design

As physical effects become important, synthesis cannot be completely separated from placement and routing. BBD benefits from tools that consider physical design while optimizing logic.

##### 3. Block-Level Floorplanning

BBD needs floorplanning that estimates block sizes, placement, routing and interface feasibility. This helps create realistic budgets.

#### Benefits Of BBD

- Scales better than flat TDD.
- Allows multiple teams to work in parallel.
- Makes complex systems manageable.
- Supports subsystem-level verification.
- Allows reuse of some existing blocks.
- Controls timing/power/area through budgets.
- Helps integration by defining clear block interfaces.

#### Challenges Of BBD

- Budget creation is difficult.
- Interface timing errors can still occur.
- System-level verification becomes important.
- Blocks may individually pass but fail together.
- Reuse is opportunistic rather than fully planned.
- Integration can become a major schedule risk.

Exam line: **BBD manages SoC complexity by partitioning the design into blocks with budgets, but it still needs careful integration and interface verification.**

<a id="topic-1-pbd"></a>

### PBD - Platform Based Design

**PBD** means **Platform Based Design**. It is a methodology where SoCs are built using a reusable platform architecture, preverified IP blocks and standardized interfaces.

Important definition:

```text
PBD = design methodology based on planned reuse of verified blocks,
standard interfaces and reusable platform architecture to reduce time-to-market.
```

#### What Is A Platform?

A **platform** is a reusable base for a family of SoCs. It may include:

- processor subsystem,
- memory subsystem,
- interconnect architecture,
- standard buses/interfaces,
- reusable IP blocks,
- verification environment,
- software layers,
- device drivers,
- RTOS/OS support,
- power-management framework,
- test and debug infrastructure.

The platform is not a single chip copied blindly. It is a reusable architecture that can be configured or extended for related products.

#### Platform Vs Block Vs Product

These three words are different and should not be mixed:

| Term | Meaning | Example |
|---|---|---|
| Block | One reusable functional unit | UART IP, DMA controller, memory controller |
| Platform | Reusable architecture base made of many blocks plus interfaces and software support | Processor subsystem + AMBA interconnect + memory subsystem + drivers |
| Product | Final SoC built for a market/customer using the platform | Mobile camera SoC, IoT controller, media processor |

PBD is powerful because the platform is reused across many products. For example, a company may reuse the same CPU subsystem, bus architecture, boot software, debug logic and peripheral framework in several SoCs, while changing only the accelerator blocks or memory size. This reduces design time because the reused part has already been integrated and verified.

#### What Gets Reused In PBD

PBD is not only hardware reuse. A strong platform can reuse many things:

- **Hardware IP**: CPU core, DSP, memory controller, DMA, peripheral controllers.
- **Interconnect architecture**: AMBA AXI bus, bridges, arbitration policy, address map style.
- **Software**: boot code, device drivers, HAL, RTOS port, middleware.
- **Verification environment**: testbench components, verification IP, assertions, scoreboards and tests.
- **Physical-design knowledge**: floorplan templates, clocking style, power-domain strategy.
- **DFT/debug logic**: scan access, JTAG access, trace/debug blocks and test controllers.

This is why PBD reduces time-to-market more strongly than ordinary block reuse. The team is not only reusing a single block; it is reusing an already understood design ecosystem.

#### Platform Stack In PBD

A platform is often better understood as a stack of reusable layers.

```text
Application / product-specific features
        |
Software platform: APIs, drivers, RTOS/OS, middleware
        |
Hardware architecture platform: CPU, interconnect, memory subsystem, accelerators
        |
Physical/test platform: floorplan style, power domains, DFT, debug, timing strategy
```

The platform-based design literature describes a platform as an abstraction layer that hides details of lower-level implementation choices. That idea is useful for exams: the platform gives designers a stable base and hides unnecessary detail, so new products can be built faster.

#### Why Standard Interfaces Matter In PBD

PBD depends on reusable IP. But IP can only be reused easily if its interfaces are standard and well described.

Examples:

- **AMBA - Advanced Microcontroller Bus Architecture** provides standard SoC interface/protocol families such as AXI, AHB and APB.
- **AXI - Advanced eXtensible Interface** is often used for high-performance memory-mapped masters/slaves.
- **APB - Advanced Peripheral Bus** is often used for simpler low-bandwidth peripherals.
- **IP-XACT / IEEE 1685** provides a standard way to describe IP metadata, interfaces, memory maps and integration information for tool flows.

Why this matters:

- the integrator can connect blocks more predictably,
- tools can understand IP interfaces and memory maps,
- verification IP can be reused,
- software register maps can be generated or checked more consistently,
- integration errors reduce because interfaces are documented and standardized.

Without standard interfaces, PBD becomes weak because every reused block needs custom glue logic, custom verification and custom documentation.

#### Hard, Firm And Soft IP In PBD

PBD often reuses IP in different forms.

| IP Type | Meaning | Advantage | Limitation |
|---|---|---|---|
| Soft IP | RTL source such as Verilog/VHDL/SystemVerilog | Flexible and portable across technologies | Timing/area not fully fixed until implementation |
| Firm IP | Partly implemented or constrained IP | Better predictability than soft IP | Less flexible than pure RTL |
| Hard IP | Physical layout/macros already implemented | Predictable timing, power and area | Less portable and harder to modify |

Example:

- CPU core may be delivered as soft or hard IP.
- SRAM/PLL/analog blocks are usually hard macros.
- USB or PCIe controller may include soft controller logic plus hard PHY.

Why this matters in PBD:

- soft IP supports configurability,
- hard IP improves predictability,
- firm IP balances reuse and predictability,
- the platform integrator must know the form of each IP to plan timing, area, power and verification.

#### PBD And Derivative Products

A **derivative product** is a new product based on an existing platform.

Example:

```text
Base platform:
CPU + AXI interconnect + DDR controller + DMA + security + boot software

Product 1:
Base platform + camera image accelerator

Product 2:
Base platform + AI accelerator

Product 3:
Base platform + wireless communication subsystem
```

The first platform may take longer to create because the team must design it for reuse. But later derivative products become faster because the base architecture, software, verification and integration flow already exist.

This is why the PPT says PBD can reduce time-to-market for first products and increase the speed of derivative products.

Exam line: **PBD is not just copying old blocks; it is planned reuse of a complete hardware/software/verification platform with standardized interfaces.**

#### Why PBD Was Needed

BBD still has high integration effort if every chip uses different blocks and interfaces. PBD reduces effort by planning reuse in advance.

PBD was needed because:

- time-to-market became critical,
- SoC complexity increased,
- verification effort became too large,
- derivative products had to be delivered quickly,
- standardized interfaces made reuse more practical,
- preverified IP reduced risk.

The PPT says PBD uses extensive design reuse and design hierarchy, and productivity improves through predictable, preverified blocks with standardized interfaces.

#### PBD Has Two Main Focus Areas

##### 1. Block Authoring / Creation

In PBD, blocks are created to be reusable in multiple target designs. This requires:

- clean interfaces,
- documentation,
- verification collateral,
- configurable parameters,
- timing/power/area information,
- standard deliverables.

The block author does not design only for one chip. The block is designed so future SoCs can reuse it.

##### 2. System-Chip Integration

The system integrator assembles the SoC using platform blocks and standard interfaces. The focus shifts from designing every block from scratch to:

- selecting blocks,
- configuring blocks,
- connecting interfaces,
- verifying integration,
- checking performance and power,
- validating software interaction.

#### PBD Linchpin Technologies

The PPT lists important PBD enablers:

- high-level system-level algorithmic and architectural design tools,
- hardware/software co-design technologies,
- physical layout tools focused on bus planning and block integration,
- VC/IP authoring verification tools.

These matter because PBD succeeds only when reused blocks can be integrated predictably.

#### Benefits Of PBD

- Reduces time-to-market.
- Supports derivative products quickly.
- Improves productivity through planned reuse.
- Reduces verification risk using preverified blocks.
- Encourages standardized interfaces.
- Supports hierarchical design.
- Allows software and hardware reuse together.

#### Challenges Of PBD

- Platform creation requires high initial investment.
- The platform must be designed carefully for reuse.
- Standard interfaces may reduce freedom in some designs.
- Reused blocks may not perfectly match new requirements.
- Integration and system-level validation are still necessary.
- Platform-based products can become less optimized than fully custom designs.

#### Example Of PBD

Assume a company builds a family of smart-camera SoCs. The reusable platform may contain:

- Arm CPU subsystem,
- AMBA AXI/APB interconnect,
- DDR memory controller,
- boot ROM,
- interrupt controller,
- DMA controller,
- debug/JTAG block,
- power-management unit,
- Linux or RTOS software layer,
- reusable drivers for timers, UART, SPI and I2C.

For Product A, the company adds an image-signal-processing accelerator. For Product B, it adds an AI accelerator. For Product C, it adds a video encoder. Because the base platform is already verified, the new product team focuses mainly on the new accelerator, integration performance and software support.

Exam line: **PBD is valuable when many related SoCs are built from the same reusable architecture, because hardware, software, verification and integration knowledge are reused together.**

Exam line: **PBD is the most reuse-oriented methodology; it improves productivity and time-to-market by using preverified platform blocks and standardized interfaces.**

<a id="topic-1-selection-guide"></a>

### Which Methodology To Choose

In exams, you may be asked indirectly which methodology fits a situation. Use this guide.

#### Choose TDD When

- the design is not extremely large,
- most logic is new,
- timing/performance is the main risk,
- block reuse is limited,
- the team needs strong floorplan and STA-driven closure.

Example: a custom ASIC datapath block that must run at a high clock frequency.

#### Choose BBD When

- the design has many functional subsystems,
- different teams own different parts,
- block-level timing/power/area budgets are needed,
- integration complexity is high,
- some block reuse exists but not a full reusable platform.

Example: a multimedia SoC with CPU subsystem, memory subsystem, video block, DMA, interconnect and peripherals.

#### Choose PBD When

- many related products must be built,
- reuse is planned from the beginning,
- standard interfaces can be enforced,
- hardware and software platform layers can be reused,
- derivative products must be delivered quickly.

Example: an IoT SoC family using the same CPU, bus, memory subsystem, drivers and debug framework, while changing sensor or wireless blocks.

#### How They Combine In Modern SoC Design

Real companies do not always use only one methodology. They combine them:

```text
PBD at product-family level:
    reuse a platform architecture

BBD at SoC integration level:
    divide the SoC into subsystems and budgets

TDD inside blocks and physical implementation:
    close timing using constraints, STA and floorplanning
```

So the best exam statement is:

```text
Modern SoC methodology is layered:
PBD provides reuse, BBD provides hierarchy, and TDD provides timing closure.
```

<a id="topic-1-comparison"></a>

### Comparison Table

| Point | TDD - Timing Driven Design | BBD - Block Based Design | PBD - Platform Based Design |
|---|---|---|---|
| Main goal | Meet timing/performance | Manage complexity through blocks | Reduce time-to-market through planned reuse |
| Main design style | Mostly timing-driven RTL/physical flow | Hierarchical block partitioning | Reusable platform architecture |
| Best suited for | Moderately complex ASICs with mostly new logic | Large SoCs with multiple functional blocks | Product families and derivative SoCs |
| Reuse level | Low or limited | Opportunistic reuse | Planned extensive reuse |
| Key concern | Timing closure | Block budgets and integration | Standard interfaces and platform reuse |
| Important tools | Floorplanning, STA, synthesis, P&R | System modeling, block floorplanning, integrated synthesis/physical design | ESL tools, co-design tools, platform integration, VC verification |
| Team style | Smaller homogeneous teams | Multiple block teams | Block authors + system integrators |
| Main risk | Timing closure loops and late RTL changes | Interface and integration errors | Platform mismatch or high initial platform cost |
| Exam keyword | Timing closure | Hierarchical budgets | Planned reuse |

### Common Confusions To Avoid

| Confusion | Correct Understanding |
|---|---|
| TDD means only checking timing at the end | TDD means timing constraints guide the whole flow from synthesis to physical design. |
| BBD means only splitting Verilog into modules | BBD means hierarchical design with block contracts, budgets, floorplanning, verification and integration. |
| PBD means copying an old chip | PBD means planned reuse of a configurable platform, including hardware, software, interfaces and verification. |
| Reuse always reduces effort automatically | Reuse helps only when the IP is documented, verified, configurable and interface-compatible. |
| A block that passes alone will pass in the SoC | Integration can still fail because of timing, protocol, reset, clock, power or software assumptions. |
| Standard interfaces remove all integration work | They reduce custom work, but configuration, verification and performance validation are still required. |

### One-Line Memory

```text
TDD: Can the design meet the clock?
BBD: Can the large design be divided and integrated safely?
PBD: Can we reuse a verified platform to build products faster?
```

### Figure To Remember

Draw this in the exam:

```text
Design methodology evolution

ADD             TDD             BBD             PBD
Area-driven ->  Timing-driven -> Block-based -> Platform-based
1980s           1990s           2000s          reuse/product-family era

Main concern:
Area       ->    Timing      ->  Complexity  ->  Time-to-market + reuse
```

Also draw this comparison triangle:

```text
                 PBD
         planned reuse + platform
              /          \
             /            \
          BBD ------------ TDD
  hierarchy + budgets     timing closure
```

<a id="topic-1-final-answer"></a>

### Final Exam-Ready Answer

SoC design methodology is the organized process used to design a System on Chip while controlling functionality, timing, area, power, verification effort, integration risk and time-to-market. It is needed because an SoC contains many interacting hardware and software components such as processors, memories, interconnects, IP blocks, accelerators and peripherals. A flat unplanned design flow cannot handle such complexity reliably.

The evolution of SoC design methodologies can be understood as a shift in dominant design problems. In early IC design, area was the major concern, so Area Driven Design was used. With technology scaling and higher clock frequencies, timing and delay became more important, leading to **TDD - Timing Driven Design**. As chip complexity increased, flat timing-driven design became insufficient, so **BBD - Block Based Design** evolved. Later, market competition and time-to-market pressure required planned reuse, leading to **PBD - Platform Based Design**.

**TDD - Timing Driven Design** is a methodology where timing closure is the main driver of the design process. Timing constraints guide synthesis, floorplanning, static timing analysis and physical implementation. TDD uses linchpin technologies such as interactive floorplanning tools, **STA - Static Timing Analysis**, timing-driven synthesis and datapath compilers. It is suitable for moderately complex ASICs with mostly new logic and limited reuse. Its advantage is strong timing control, but it becomes weak when designs become too large, hierarchical and reuse-heavy.

**BBD - Block Based Design** is a hierarchical methodology where the SoC is divided into functional blocks. Each block is designed according to timing, area and power budgets. It is useful when the design contains subsystems such as embedded processors, compression engines, error-correction blocks, memory controllers and accelerators. BBD allows multiple teams to work in parallel and makes large designs manageable. However, block budgets must be realistic, and interface verification becomes critical because blocks that work individually may fail after integration.

**PBD - Platform Based Design** is a reuse-oriented methodology where SoCs are built from preverified blocks, standard interfaces and reusable platform architecture. A platform may include processors, interconnects, memory subsystem, software layers, verification environment and reusable IP blocks. PBD separates block authoring from system-chip integration. It reduces time-to-market and supports derivative products, but it requires large initial investment and careful platform planning.

Thus, TDD focuses on timing closure, BBD focuses on hierarchical complexity management and PBD focuses on planned reuse and fast product development. A modern SoC may combine all three ideas: timing-driven implementation inside blocks, block-based hierarchy for integration and platform-based reuse for product families.

In deeper terms, TDD controls the physical timing risk of the design. It asks whether every register-to-register path, input path, output path and clock-domain-related timing path can meet the clock constraints after synthesis and layout. BBD controls the system organization risk. It asks whether a large design can be partitioned into blocks with realistic timing, power, area and interface contracts. PBD controls the product-development risk. It asks whether a family of SoCs can be created by reusing a stable platform containing hardware IP, standard interfaces, software layers, verification components and physical-design knowledge.

Therefore, the evolution from TDD to BBD to PBD is not the replacement of one idea by another. It is the addition of higher-level control. TDD remains necessary inside blocks, BBD is needed to manage SoC hierarchy, and PBD is needed when companies must build multiple related products quickly with predictable reuse.

### Short 10-Mark Exam Answer

SoC design methodology is a planned approach for designing a System on Chip while meeting functionality, timing, area, power, verification and time-to-market goals. The major methodologies are **TDD - Timing Driven Design**, **BBD - Block Based Design** and **PBD - Platform Based Design**.

TDD focuses on timing closure. It uses floorplanning, timing-driven synthesis and **STA - Static Timing Analysis** to reduce delay and meet clock constraints. It is suitable for moderately complex ASICs but does not scale well for very large reusable SoCs.

BBD divides the SoC into functional blocks. Each block is assigned timing, area and power budgets and can be designed by separate teams. This improves scalability and supports partial reuse, but block interfaces and system integration must be verified carefully.

PBD uses reusable platforms, preverified IP blocks and standardized interfaces. It improves productivity and reduces time-to-market, especially for derivative products. Its challenge is the initial platform investment and possible mismatch between reused blocks and new requirements.

Therefore, TDD solves timing problems, BBD solves complexity problems and PBD solves reuse and time-to-market problems.

<a id="topic-1-technical-words"></a>

### Technical Words To Use For Marks

- **SoC design methodology** (write this because the question asks about organized SoC design approaches.)
- **TDD - Timing Driven Design** (write this because it is the first named methodology in the topic.)
- **BBD - Block Based Design** (write this because it explains hierarchy and block budgets.)
- **PBD - Platform Based Design** (write this because it explains planned reuse and platform architecture.)
- **ADD - Area Driven Design** (write this because it explains the historical evolution before TDD.)
- **Linchpin technology** (write this because the PPT uses it for enabling methodology tools/procedures.)
- **Timing closure** (write this because TDD is built around meeting timing constraints.)
- **STA - Static Timing Analysis** (write this because TDD depends on fast timing checking.)
- **Floorplanning** (write this because physical placement affects delay and area.)
- **Synthesis** (write this because RTL is converted into gates while optimizing constraints.)
- **Place and route / P&R** (write this because physical implementation affects timing closure.)
- **RTL - Register Transfer Level** (write this because TDD and BBD often begin from RTL block descriptions.)
- **ASIC - Application-Specific Integrated Circuit** (write this because TDD is often discussed for ASIC design.)
- **DSM - Deep Sub-Micron** (write this because timing/wire delay problems increased in DSM technologies.)
- **Timing budget** (write this because BBD assigns timing constraints to blocks.)
- **Power budget** (write this because blocks must fit total power limits.)
- **Area budget** (write this because block area controls die size and cost.)
- **Hierarchical design** (write this because BBD and PBD divide a large SoC into manageable levels.)
- **IP - Intellectual Property** (write this because PBD relies on reusable design blocks.)
- **VC - Virtual Component** (write this because the PPT uses VC-style reusable block language.)
- **Standard interface** (write this because PBD needs predictable block integration.)
- **Design reuse** (write this because reuse is the core productivity driver of PBD.)
- **TTM - Time To Market** (write this because BBD/PBD evolved to reduce product development time.)
- **NRE - Non-Recurring Engineering cost** (write this because platform reuse spreads one-time design cost over many products.)
- **Block authoring** (write this because PBD separates reusable block creation from integration.)
- **System-chip integration** (write this because PBD focuses on integrating platform blocks.)
- **Critical path** (write this because timing closure is usually limited by the slowest path.)
- **Slack** (write this because positive/negative slack tells whether timing passes or fails.)
- **Setup violation** (write this because data arriving late can break synchronous operation.)
- **Hold violation** (write this because data changing too early can also break synchronous operation.)
- **Clock skew** (write this because clock arrival differences affect setup and hold timing.)
- **Wire delay / interconnect delay** (write this because DSM designs are strongly affected by routing delay.)
- **Pipelining** (write this because it is a common way to split a long timing path across cycles.)
- **Retiming** (write this because moving registers can balance timing paths.)
- **ECO - Engineering Change Order** (write this because late fixes are often needed during timing closure.)
- **Interface contract** (write this because BBD depends on clear block-boundary rules.)
- **Register map** (write this because software-visible blocks must define addresses and fields.)
- **Integration verification** (write this because blocks that pass alone can still fail together.)
- **Hard IP / firm IP / soft IP** (write these because PBD reuse depends on the form of reusable IP.)
- **Derivative product** (write this because PBD is especially useful for product families.)
- **Platform stack** (write this because PBD reuses hardware architecture, software/API and physical/test layers.)
- **IP-XACT / IEEE 1685** (write this because standard IP metadata supports packaging, integration and reuse.)
- **AMBA AXI/APB** (write this because standard SoC bus interfaces make platform integration more predictable.)
- **Verification collateral** (write this because reusable IP must include tests, assertions, coverage and documentation, not only RTL.)

<a id="topic-1-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 174644.png](<images/Screenshot 2026-05-12 174644.png>) contains the exact syllabus headline **SoC Design Essentials: Design Methodologies - TDD**.
2. **Related topic image**: [Screenshot 2026-05-12 174710.png](<images/Screenshot 2026-05-12 174710.png>) contains **BBD, PBD**.
3. **Methodology evolution diagram**: Draw `ADD -> TDD -> BBD -> PBD` with area, timing, complexity and reuse/time-to-market.
4. **Comparison table**: Draw TDD vs BBD vs PBD with goal, use case, tools, benefits and challenges.
5. **PPT source to cite**: [14-SOC Design Methodologies.pdf, p.5](<System on chip/14-SOC Design Methodologies.pdf#page=5>) lists TDD, BBD and PBD as primary design methods.
6. **PPT source to cite**: [14-SOC Design Methodologies.pdf, p.20](<System on chip/14-SOC Design Methodologies.pdf#page=20>) gives the difference between TDD, BBD and PBD.

#### Figure 1: TDD Timing Closure Loop

Draw this when explaining Timing Driven Design:

```text
RTL + timing constraints
        |
        v
Timing-driven synthesis
        |
        v
Floorplanning and placement
        |
        v
Static timing analysis
        |
        v
Timing optimization
        |
        +---- if timing fails ----+
        |                         |
        v                         |
Place and route                   |
        |                         |
        v                         |
Timing sign-off <-----------------+
```

Why this figure is useful: it shows that TDD is iterative. Timing is checked, optimized and rechecked until timing closure is achieved.

#### Figure 2: BBD Block Budget Diagram

Draw this when explaining Block Based Design:

```text
                 SoC specification
                         |
                         v
        +----------------+----------------+
        |                |                |
    CPU block       Memory block     Accelerator block
 timing/power/area timing/power/area timing/power/area
    budget             budget             budget
        |                |                |
        +----------------+----------------+
                         |
                         v
              SoC integration + verification
```

Why this figure is useful: it shows that BBD is about block partitioning plus budgets plus integration, not just separate module design.

#### Figure 3: PBD Platform Reuse Diagram

Draw this when explaining Platform Based Design:

```text
Reusable platform
CPU + interconnect + memory + drivers + debug + verification
        |
        +----------------+----------------+----------------+
        |                |                |                |
 Product A          Product B          Product C       Product D
 camera SoC         AI SoC             IoT SoC         media SoC
```

Why this figure is useful: it shows how PBD reduces time-to-market by using one verified platform for many derivative products.

#### Figure 4: Layered Modern SoC Methodology

Draw this if the question asks for analysis:

```text
Product family level:     PBD -> platform reuse
SoC organization level:   BBD -> blocks, budgets, interfaces
Implementation level:     TDD -> timing closure inside blocks
```

Why this figure is useful: it shows that modern SoC design often uses all three methodologies together.

---

<a id="topic-2"></a>

## Topic 2: Hardware-Software Co-Design

<a id="topic-2-question"></a>

### Question

**Explain Hardware-Software Co-Design in SoC design.**

### CLO Mapping

This topic belongs to **CLO 4: Analyze the Design Methodologies of SoC; TLM and its need in SoC Design**.

Reason: Hardware-software co-design is listed in the SoC Design Essentials part of the syllabus. It is also directly connected to ESL, TLM, architectural modeling, partitioning and design methodology.

### What The Question Is Asking

The examiner is asking how an SoC is designed when part of the system is implemented as hardware and part is implemented as software.

For full marks, answer in this order:

1. Define hardware-software co-design.
2. Explain why it is needed in SoC.
3. Explain hardware implementation and software implementation.
4. Explain hardware/software partitioning.
5. Explain the co-design flow.
6. Explain hardware/software interfaces such as registers, drivers, interrupts and DMA.
7. Explain benefits and challenges.
8. Draw a flow diagram.

<a id="topic-2-explanation"></a>

### Main Explanation

**Hardware-software co-design** is a system-level design methodology in which the hardware part and the software part of an SoC are designed together from the beginning. It is not correct to design hardware fully first and then think about software at the end. In a real SoC, hardware and software depend on each other.

Important definition:

```text
Hardware-software co-design is the integrated design of a system using both
hardware and software components, where functions are partitioned between
hardware and software according to performance, power, cost, flexibility and
implementation constraints.
```

An SoC usually contains:

- processors or microcontrollers that execute software,
- memories that store code and data,
- interconnects or buses that connect blocks,
- hardware accelerators for performance-critical functions, meaning physical SoC blocks that speed up specific heavy tasks such as AI inference, video processing, encryption or compression,
- peripherals such as UART, SPI, I2C, timers, USB or Ethernet,
- DMA engines for data movement,
- interrupt controllers,
- embedded software such as boot code, drivers, RTOS and application software.

Because all these components interact, the designer must decide early:

```text
Which functions should be hardware?
Which functions should be software?
How will hardware and software communicate?
Will the final system meet performance, power, area, cost and schedule targets?
```

The course PPT on Functional Architecture Co-Design states that co-design is needed because systems contain large amounts of both hardware and software. It defines co-design as an integrated methodology for systems implemented using both hardware and software components, with performance goals and implementation technology in mind.

Detailed source notes are kept in [sources/CLO4_Topic2_sources.md](<sources/CLO4_Topic2_sources.md>).

#### Why Co-Design Is Needed

Co-design is needed because an SoC is not only a circuit. It is a hardware platform plus software running on that platform.

If the hardware team works alone, they may build registers, interrupts or accelerators that are difficult for software to use. If the software team works alone, they may assume features, timing or memory behavior that the hardware cannot support. Co-design avoids this gap.

Main reasons:

- **Performance**: some functions are too slow in software and need hardware acceleration.
- **Power**: dedicated hardware may consume less energy per operation than a CPU executing many instructions.
- **Flexibility**: software is easier to update than fixed hardware.
- **Cost and area**: hardware accelerators increase silicon area, so only important functions should be moved to hardware.
- **Real-time deadlines**: some functions must complete within strict time limits.
- **Software dependency**: boot code, drivers and RTOS behavior depend on hardware registers, interrupts and memory map.
- **Early validation**: system-level models allow performance and partitioning problems to be found before RTL is complete.

Exam line: **Co-design is needed because SoC behavior is produced by both hardware and software, so partitioning, interfaces and performance must be decided at system level.**

<a id="topic-2-hw-vs-sw"></a>

### Hardware Vs Software Implementation

In co-design, the designer compares two implementation styles.

#### 1. Hardware Implementation

**Hardware implementation** means implementing a function as a dedicated circuit or hardware block, usually described later in RTL.

Examples:

- video encoder,
- image-signal processor,
- AI accelerator,
- encryption engine,
- memory controller,
- packet-processing engine,
- motor-control PWM block.

Hardware is suitable when:

- the function is performance-critical,
- the function must process many data items per second,
- the function has strict latency or real-time requirements,
- the function is repeated frequently,
- energy per operation must be low,
- direct interaction with external signals is required.

Why hardware can be faster:

Software executes instructions sequentially or with limited parallelism on a processor. Here, **parallelism** means doing more than one operation at the same time.

The limited processor parallelism can be:

- **ILP - Instruction-Level Parallelism**: a pipelined or superscalar CPU may overlap/fetch/decode/execute multiple instructions, but only within the limits of its pipeline and issue width.
- **DLP - Data-Level Parallelism**: SIMD/vector instructions may process multiple data items with one instruction, but only for operations supported by the CPU/DSP instruction set.
- **TLP - Thread-Level Parallelism**: a multi-core processor or RTOS may run multiple tasks/threads, but this depends on number of cores, scheduling and shared-memory contention.
- **Memory-level parallelism**: the processor may keep multiple cache misses or memory requests outstanding, but it is still limited by cache, interconnect and memory-controller bandwidth.

Even with these forms of parallelism, a general CPU is still designed to run many different programs. It must fetch instructions, decode them, check dependencies, access registers/cache and handle branches. A dedicated accelerator is designed for one job, so it can build many datapaths exactly for that job.

Example:

```text
CPU software image filtering:
one instruction stream processes pixels step by step,
possibly helped by SIMD, cache and multiple cores.

Hardware image accelerator:
many pixel operations are wired as parallel datapaths,
and a pipeline can process a new pixel/block every cycle.
```

Dedicated hardware can build many parallel datapaths and pipelines for one specific job. For example, a video accelerator can process many pixels in a pipeline, while software may need many instruction cycles per pixel.

Tradeoff:

- hardware is fast and energy-efficient for fixed tasks,
- but hardware costs silicon area,
- hardware is harder to change after fabrication,
- hardware needs deep verification.

#### 2. Software Implementation

**Software implementation** means implementing a function as code running on a processor, microcontroller, DSP or embedded CPU.

Examples:

- device driver,
- bootloader,
- control algorithm,
- protocol stack,
- user application,
- RTOS task,
- error-handling routine.

Software is suitable when:

- the function may change after deployment,
- flexibility is more important than maximum speed,
- the task is control-oriented rather than data-heavy,
- development time must be reduced,
- the function interacts heavily with the operating system,
- the task does not require special hardware throughput.

Tradeoff:

- software is flexible and easier to update,
- but software may be slower,
- it consumes CPU cycles,
- it depends on memory latency, caches and interrupts,
- it may miss real-time deadlines if scheduling is poor.

#### Hardware And Software Tradeoff

| Point | Hardware Implementation | Software Implementation |
|---|---|---|
| Speed | Usually faster for fixed data-path work | Usually slower for heavy computation |
| Flexibility | Hard to change after chip fabrication | Easy to update by changing code |
| Area | Uses extra silicon area | Reuses existing processor |
| Power per operation | Often lower for repeated compute-heavy tasks | Can be higher due to instruction fetch/decode/control overhead |
| Development | Needs RTL design and hardware verification | Needs compiler, drivers and software testing |
| Best for | acceleration, interfaces, timing-critical tasks | control, configuration, protocol changes, application logic |

Exam line: **Co-design is mainly the art of choosing the correct hardware/software boundary.**

<a id="topic-2-partitioning"></a>

### HW/SW Partitioning

**HW/SW partitioning** means deciding which system functions will run as software and which functions will be implemented as hardware.

Important definition:

```text
HW/SW partitioning is the allocation of system tasks to hardware resources
or software resources based on performance, power, cost, area, flexibility,
communication and real-time requirements.
```

The co-design PPT states that a task may be placed in software if it interacts closely with the operating system, while a task may need hardware if it interacts closely with external signals. It also gives criteria such as dynamic system behavior, execution-time difference between hardware and software and hardware cost.

#### Partitioning Criteria

| Criterion | Meaning | Partitioning Decision |
|---|---|---|
| Execution time | How long the task takes in hardware vs software | Put in hardware if software is too slow |
| Real-time deadline | Maximum allowed response time | Put in hardware or high-priority software if deadline is strict |
| Throughput | Amount of data processed per second | Put streaming/high-data-rate tasks in hardware |
| Power | Energy used for the function | Use hardware if it reduces energy significantly |
| Area cost | Silicon area required for custom hardware | Keep in software if hardware cost is too high |
| Flexibility | Need to update function after release | Keep in software if function may change |
| OS interaction | Dependency on files, tasks, scheduling or protocols | Keep in software when OS services are needed |
| External signal timing | Direct timing with pins, sensors or high-speed I/O | Use hardware when precise timing is required |
| Communication cost | Data movement between CPU, memory and accelerator | Avoid hardware if data-transfer overhead is bigger than compute gain |

#### Simple Example

Consider a camera SoC.

Software may handle:

- user settings,
- camera mode control,
- file-system interaction,
- network upload,
- error handling,
- driver configuration.

Hardware may handle:

- pixel filtering,
- image compression,
- face-detection acceleration,
- sensor timing,
- high-speed DMA transfers.

Why this split makes sense:

- software is good for control and changing product features,
- hardware is good for high-throughput pixel processing,
- DMA moves frames without making the CPU copy every byte,
- drivers connect software to hardware registers and interrupts.

#### Common Partitioning Mistake

A beginner may think "put everything in hardware because hardware is faster." That is not correct. Hardware is not free. It costs area, verification effort, power leakage, design time and risk. Also, a hardware accelerator may be useless if the CPU spends too much time moving data to and from it.

Exam line: **A good partition is not the fastest hardware-only design; it is the best balance of performance, power, area, cost, flexibility and software complexity.**

<a id="topic-2-flow"></a>

### Co-Design Flow

A typical hardware-software co-design flow is:

```text
System requirements
      |
      v
Functional specification / executable model
      |
      v
Architecture exploration
      |
      v
HW/SW partitioning
      |
      v
Interface definition
      |
      +--------------------+
      |                    |
      v                    v
Hardware design        Software design
RTL / accelerator      boot code / drivers / RTOS / application
      |                    |
      +---------+----------+
                v
       Co-simulation / co-verification
                |
                v
       Integration and validation
```

#### Step 1: System Requirements

The design starts from requirements: what the product must do, performance targets, power limits, cost limits, I/O requirements and real-time deadlines.

Example requirements:

- process 4K video at 60 frames per second,
- boot in less than 2 seconds,
- support low-power standby,
- encrypt packets at required throughput,
- meet battery-power budget.

#### Step 2: Functional Specification

The **functional specification** describes what the system must do without fixing the final hardware/software implementation.

For example:

```text
Input camera frame -> noise reduction -> color correction -> compression -> memory/network output
```

At this stage, the designer focuses on behavior and algorithms.

#### Step 3: Architecture Exploration

**Architecture exploration** means trying possible system organizations:

- one CPU vs multiple CPUs,
- CPU plus DSP,
- CPU plus hardware accelerator,
- shared memory vs local memory,
- bus-based interconnect vs NoC,
- different cache/memory sizes,
- different accelerator speeds.

This is where ESL and TLM models are useful because they run faster than RTL and allow many design alternatives to be tested early.

<a id="topic-2-esl-tlm"></a>

### ESL And TLM Models In Co-Design

#### What Is ESL?

**ESL** means **Electronic System Level**. It is a high-level design stage above RTL where the designer thinks about the complete system rather than individual flip-flops and signals.

Important definition:

```text
ESL = Electronic System Level design, where the SoC is modeled at a high
abstraction level to explore architecture, hardware/software partitioning,
performance and system behavior before detailed RTL implementation.
```

At ESL, the designer may model:

- algorithms,
- software tasks,
- processor choices,
- memory hierarchy,
- bus/interconnect behavior,
- accelerators,
- DMA transfers,
- interrupts,
- power/performance estimates,
- hardware/software communication.

The course PPT says ESL is needed because modern SoCs are too complex to design only at RTL. It says designers reason at an abstract functional level, then refine the model toward RTL. This is exactly why ESL is used in hardware-software co-design.

#### What Is TLM?

**TLM** means **Transaction-Level Modeling**. It is a modeling method where communication is represented as high-level transactions instead of individual wires toggling cycle by cycle.

Important definition:

```text
TLM = Transaction-Level Modeling, where communication between SoC components
is modeled using abstract operations such as read, write, burst transfer,
interrupt or DMA transaction instead of pin-level bus signals.
```

A **transaction** is one complete communication operation.

Examples:

```text
read(address)
write(address, data)
burst_read(start_address, length)
dma_transfer(source, destination, size)
interrupt(event_id)
```

At RTL, an AXI/APB/AHB bus transfer may require many signals and clock cycles. At TLM, the same transfer can be represented as one function call or one transaction object carrying address, data, command, response and timing delay.

#### Why ESL/TLM Runs Faster Than RTL

RTL simulation is slow because it simulates:

- every clock edge,
- every signal transition,
- every flip-flop update,
- every handshake signal,
- every bit-level bus event,
- every delta-cycle/event in the simulator.

TLM simulation is faster because it abstracts many low-level events into one transaction.

Example:

```text
RTL bus write:
cycle 1: address valid
cycle 2: ready handshake
cycle 3: data phase
cycle 4: response phase
many signal toggles are evaluated

TLM bus write:
write(address, data, delay)
one high-level transaction is evaluated
```

So TLM reduces simulation work. It does not simulate every pin toggle unless the model is refined to a lower level. This makes it possible to test many architectural choices early.

#### Why ESL/TLM Is Useful In Hardware-Software Co-Design

ESL/TLM helps answer system-level questions before RTL exists:

- Should a function run on CPU, DSP or accelerator?
- How many processors are needed?
- Is the bus/interconnect bandwidth enough?
- Is memory latency too high?
- Does DMA reduce CPU load?
- Does software meet real-time deadlines?
- Does the accelerator provide enough speedup to justify area?
- Will the driver/register interface be convenient for software?
- Does the boot or interrupt flow work?

Without ESL/TLM, designers may wait until RTL is available to test these questions. That is risky because architecture changes are expensive after RTL and physical design have started.

#### TLM Initiator And Target

In TLM, communication usually has an **initiator** and a **target**.

| Term | Meaning | SoC Example |
|---|---|---|
| Initiator | Component that starts a transaction | CPU, DMA controller, accelerator bus master |
| Target | Component that receives/responds to a transaction | memory, peripheral register block, accelerator control registers |

Example:

```text
CPU model = initiator
Accelerator register model = target

CPU sends write(ACCEL_CONTROL, START)
Accelerator target receives transaction and starts processing
```

#### Loosely Timed And Approximately Timed TLM

Accellera/SystemC TLM commonly distinguishes two useful modeling styles.

| Style | Full Form | Meaning | Best Use |
|---|---|---|---|
| LT | Loosely Timed | Fast model with limited timing detail | early software development, booting OS, functional platform testing |
| AT | Approximately Timed | More detailed timing/resource behavior | architecture performance analysis, contention, arbitration, latency studies |

**Loosely timed models** are very fast because they do not model every timing dependency or resource conflict. They are useful when software behavior is more important than detailed hardware timing.

**Approximately timed models** are slower but more informative because they can model ordering, delays, contention and arbitration. They are useful when the designer wants to know whether the architecture can meet bandwidth and latency requirements.

Exam line: **LT is faster and better for early software; AT is more timing-aware and better for architecture/performance analysis.**

#### Virtual Platform

A **virtual platform** is an executable model of the SoC that can run software before the real chip exists.

It may include:

- CPU model or ISS,
- memory model,
- interrupt controller model,
- peripheral models,
- bus/interconnect model,
- accelerator models,
- TLM register models,
- software image or driver code.

Why it matters:

- software teams can develop boot code and drivers early,
- architecture teams can estimate performance early,
- hardware/software interface bugs can be found before silicon,
- product development can start before RTL is complete.

#### ESL/TLM Example

Assume a camera SoC has a CPU, DMA, memory and image accelerator.

RTL-level thinking:

```text
Track AXI valid/ready signals, address channel, data channel,
response channel, burst lengths, clock cycles and signal transitions.
```

TLM-level thinking:

```text
CPU writes accelerator configuration register.
DMA transaction moves frame buffer to accelerator.
Accelerator transaction processes frame.
DMA transaction writes output frame to memory.
Interrupt transaction notifies CPU.
```

This TLM model is not final silicon implementation. It is an early system model used to check architecture and software interaction.

#### What ESL/TLM Cannot Replace

ESL/TLM is powerful, but it does not replace lower-level verification.

It cannot fully replace:

- RTL verification,
- protocol signal-level checks,
- gate-level timing simulation,
- static timing analysis,
- physical design sign-off,
- DFT and manufacturing test.

Reason: TLM abstracts away many low-level details. A TLM model can prove that the architecture idea is reasonable, but RTL is still needed to implement exact cycle behavior and hardware signals.

Exam line: **ESL/TLM is used for early exploration and fast system modeling; RTL is still needed for detailed implementation and sign-off.**

#### Step 4: HW/SW Partitioning

The team assigns functions to hardware or software. Performance-critical data-path tasks may become hardware accelerators, while control tasks may remain software.

#### Step 5: Interface Definition

This step defines how software controls hardware and how hardware reports status. Interfaces include:

- memory-mapped registers,
- interrupts,
- DMA descriptors,
- shared buffers,
- device drivers,
- HAL/BSP functions,
- bus protocols,
- reset and clock control.

#### Step 6: Hardware And Software Development

Hardware designers develop RTL for hardware blocks. Software designers develop boot code, drivers, RTOS configuration and applications. Co-design allows both to proceed concurrently using models.

#### Step 7: Co-Simulation / Co-Verification

The software and hardware models are run together to check real interaction. This can find bugs such as:

- wrong register programming sequence,
- missing interrupt clear,
- incorrect DMA buffer address,
- performance bottleneck,
- software expecting a hardware response too early,
- hardware status bit behaving differently from software assumptions.

<a id="topic-2-interfaces"></a>

### Interfaces Between Hardware And Software

The most important part of co-design is the hardware/software boundary. The hardware is useless if software cannot control it correctly.

#### 1. Register Interface

A **register interface** is a set of hardware control/status registers visible to software.

Example:

```text
CONTROL register: start, stop, reset
STATUS register: busy, done, error
CONFIG register: mode, size, priority
ADDRESS register: input/output buffer address
```

Software writes control/configuration registers and reads status registers.

#### 2. Memory-Mapped I/O

**Memory-mapped I/O** means hardware registers are placed in the processor address map. Software uses normal load/store instructions to access them.

Example:

```text
0x4000_0000 = UART control register
0x4000_0004 = UART status register
0x5000_0000 = DMA control register
```

Why it matters: software can control hardware using addresses, but the register map must be correct and documented.

#### 3. Device Driver

A **device driver** is software that controls a hardware peripheral or accelerator. It hides hardware details from higher-level software.

A driver usually:

- configures registers,
- starts and stops hardware,
- handles interrupts,
- sets up DMA,
- checks error/status bits,
- exposes an API to application software or the operating system.

#### 4. HAL - Hardware Abstraction Layer

**HAL** means **Hardware Abstraction Layer**. It is the low-level software layer directly dependent on the hardware. The software-design PPT defines HAL as software directly dependent on the underlying hardware, such as boot code, context switch code, configuration code and access to resources like MMU, on-chip bus, bus bridge and timers.

Why it matters: HAL helps upper software layers run on different hardware with fewer changes.

#### 5. RTOS - Real-Time Operating System

**RTOS** means **Real-Time Operating System**. It schedules tasks and handles timing-sensitive embedded software.

An RTOS may provide:

- task scheduling,
- interrupt management,
- timers,
- inter-task communication,
- memory management,
- synchronization.

Why it matters: if the SoC has real-time deadlines, the software scheduler must work with hardware timing.

#### 6. Interrupt

An **interrupt** is a hardware event that tells the processor a device needs service.

Example:

```text
Accelerator finishes processing -> raises interrupt -> CPU runs ISR -> driver reads status -> software continues
```

Interrupt design must define:

- interrupt source,
- priority,
- mask/unmask behavior,
- status bits,
- clear mechanism,
- edge-triggered or level-triggered behavior.

#### 7. DMA - Direct Memory Access

**DMA** means **Direct Memory Access**. It is a hardware engine that transfers data between memory and a peripheral/accelerator without the CPU copying every word.

Why DMA is used:

- reduces CPU workload,
- improves bandwidth for large data transfers,
- allows CPU and hardware accelerator to work in parallel,
- supports streaming data such as audio, video and network packets.

Example:

```text
CPU programs DMA source address, destination address and length.
DMA moves data from memory to accelerator.
Accelerator processes data.
DMA moves result back to memory.
DMA/accelerator raises interrupt when done.
```

DMA is a physical hardware block inside the SoC. Software controls it through registers and descriptors.

#### 8. Accelerator

An **accelerator** is a dedicated hardware engine used to speed up a specific function. It is a real hardware block inside the SoC, not just software. It is designed for one narrow class of operations and therefore can be faster or more power-efficient than a general-purpose CPU.

Important definition:

```text
Accelerator = specialized hardware block inside an SoC that performs a
performance-critical or energy-critical task faster than software running on
a general processor.
```

#### Why It Is Called An Accelerator

It is called an accelerator because it **accelerates** a workload. The CPU can usually perform the same task in software, but it may take many instructions, many clock cycles and more energy. The accelerator uses dedicated datapaths, parallelism and pipelining to perform the same work more efficiently.

Example:

```text
CPU doing image filtering in software:
fetch instruction -> decode -> load pixel -> calculate -> store result
repeat for millions of pixels

Image accelerator:
stream pixels through dedicated filter pipeline
many pixels processed continuously with less CPU involvement
```

#### What Is Inside An Accelerator

An accelerator may contain:

- **datapath**: arithmetic units, multipliers, adders, comparators or logic specific to the function,
- **control logic**: finite-state machine that sequences operations,
- **local buffers**: small SRAM/register storage for temporary data,
- **register interface**: control/status registers visible to software,
- **DMA interface**: connection for moving large data blocks to/from memory,
- **interrupt output**: signal to notify the CPU when work is complete,
- **bus interface**: AXI/AHB/APB or another SoC interface for communication.

So, an accelerator is usually connected to the SoC interconnect and controlled by software.

Important clarification:

```text
The driver is not a physical part of the accelerator hardware.
The driver is software that runs on the CPU and controls the accelerator.
```

The accelerator hardware contains registers, datapath, control logic, bus interface and interrupt/DMA support. The **driver** is a software layer that knows how to use those hardware features correctly.

#### How Software Uses An Accelerator

Software does not usually execute instructions inside the accelerator like a CPU. Instead, software controls the accelerator through registers and memory buffers.

Typical sequence:

```text
1. CPU/driver writes configuration registers.
2. CPU/driver gives input-buffer and output-buffer addresses.
3. CPU/driver starts the accelerator.
4. DMA or bus interface moves data.
5. Accelerator processes the data.
6. Accelerator sets a done/status bit or raises an interrupt.
7. CPU/driver reads status and uses the result.
```

This is why accelerators are important in hardware-software co-design. The hardware part gives performance, but the software part must configure and control it correctly.

Examples:

- AI inference accelerator,
- video encoder/decoder,
- cryptographic engine,
- image processing engine,
- compression engine.

#### CPU Vs Accelerator

| Point | CPU - Central Processing Unit | Accelerator |
|---|---|---|
| Purpose | General-purpose instruction execution | Specific function acceleration |
| Flexibility | Very flexible because software can change | Less flexible because hardware is fixed |
| Performance for one heavy task | May be slower | Often much faster |
| Energy per operation | Often higher for repeated heavy tasks | Often lower for the target task |
| Control | Runs software instructions | Controlled by software through registers |
| Examples | Arm Cortex-A, RISC-V core, microcontroller | AI engine, crypto engine, video codec, image processor |

#### Why Not Make Everything An Accelerator?

Accelerators are useful, but they are not free:

- they increase silicon area,
- they need verification,
- they may increase leakage power,
- they add software-driver complexity, because a driver must be written to configure the accelerator, program its registers, set up buffers/DMA, handle interrupts and report errors,
- they are harder to change after fabrication,
- they may sit idle if the workload is not used,
- data movement overhead can reduce the benefit.

Therefore, only performance-critical, repeated or energy-critical functions should become accelerators.

Exam line: **An accelerator is a physical SoC hardware block controlled by software to execute a specific heavy function faster or more efficiently than a CPU.**

<a id="topic-2-final-answer"></a>

### Final Exam-Ready Answer

Hardware-software co-design is a system-level methodology in which the hardware and software parts of an SoC are designed together. It is required because modern SoCs contain processors, memories, interconnects, peripherals, accelerators and embedded software. The final behavior of the SoC depends on both the hardware implementation and the software running on it.

The main task in co-design is hardware/software partitioning. In partitioning, system functions are assigned either to hardware or to software. Performance-critical, high-throughput or strict real-time functions are often implemented in hardware. Flexible, control-oriented or operating-system-dependent functions are often implemented in software. The decision depends on execution time, throughput, power, area, cost, flexibility, communication overhead and real-time constraints.

The co-design flow begins with system requirements and a functional specification. Designers then explore candidate architectures, perform hardware/software partitioning, define interfaces, develop hardware and software in parallel and verify the complete system using co-simulation or co-verification. Hardware may be developed as RTL blocks or accelerators, while software may include boot code, device drivers, HAL, RTOS and application software.

The hardware/software interface is very important. Software controls hardware through memory-mapped registers, device drivers, interrupts, DMA descriptors, shared memory and HAL APIs. For example, a CPU may configure a DMA engine and accelerator using registers, the DMA transfers data to the accelerator, and the accelerator raises an interrupt when processing is complete.

The advantage of co-design is that it exposes performance, partitioning and interface problems early. It improves system-level tradeoffs and allows hardware and software to be developed concurrently. Its challenge is that accurate models, good partitioning decisions and careful interface specifications are required. Thus, hardware-software co-design is essential for modern SoCs because the chip is a combined hardware and software system, not hardware alone.

### Short 10-Mark Exam Answer

Hardware-software co-design is the integrated design of an SoC using both hardware and software components. It decides which functions should be implemented as dedicated hardware and which should run as software on processors. This decision is called hardware/software partitioning.

Hardware is used for high-speed, low-latency, compute-heavy or real-time functions. Software is used for flexible control, configuration, protocol handling, drivers and application behavior. Partitioning depends on performance, power, area, cost, flexibility, communication cost and deadlines.

The co-design flow starts with requirements, creates a functional model, explores architecture alternatives, partitions functions, defines interfaces, develops hardware and software, and verifies them together. Interfaces include memory-mapped registers, interrupts, DMA, device drivers, HAL and RTOS services. Co-design is important because SoC behavior depends on both hardware and software, and late discovery of interface or performance errors is costly.

<a id="topic-2-technical-words"></a>

### Technical Words To Use For Marks

- **Hardware-software co-design** (write this because it is the exact topic and shows joint design of hardware and software.)
- **HW/SW partitioning** (write this because co-design mainly decides which functions go to hardware and which go to software.)
- **Functional specification** (write this because co-design begins with what the system must do.)
- **Architecture exploration** (write this because designers compare possible processors, accelerators, memories and buses.)
- **ESL - Electronic System Level** (write this because co-design begins above RTL and C-code level.)
- **TLM - Transaction-Level Modeling** (write this because fast architectural communication modeling supports co-design.)
- **RTL - Register Transfer Level** (write this because hardware partition is eventually refined into RTL.)
- **RTOS - Real-Time Operating System** (write this because embedded software may require task scheduling and timing guarantees.)
- **HAL - Hardware Abstraction Layer** (write this because software portability depends on hiding hardware details.)
- **BSP - Board Support Package** (write this because it adapts OS/software to the hardware platform.)
- **Device driver** (write this because software controls SoC peripherals through drivers.)
- **Memory-mapped I/O** (write this because software accesses hardware registers through the address map.)
- **Interrupt** (write this because hardware reports events to software using interrupts.)
- **ISR - Interrupt Service Routine** (write this because software responds to hardware events through ISR code.)
- **DMA - Direct Memory Access** (write this because high-speed data movement is central in SoC hardware/software interaction.)
- **Accelerator** (write this because performance-critical functions are often moved from software to dedicated hardware.)
- **Performance, power, area, cost, flexibility** (write these because they are the main partitioning tradeoffs.)

<a id="topic-2-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 174733.png](<images/Screenshot 2026-05-12 174733.png>) contains the exact syllabus headline **Hardware-Software Co-Design**.
2. **Draw this co-design flow**:

```text
Requirements
    |
Functional model
    |
Architecture exploration
    |
HW/SW partitioning
    |
Interface definition
    |
+------------------+------------------+
|                                     |
Hardware design                       Software design
RTL / accelerator                     boot / driver / HAL / RTOS / app
|                                     |
+------------------+------------------+
    |
Co-simulation and co-verification
    |
Final SoC integration
```

3. **Draw this hardware/software boundary**:

```text
Software side                         Hardware side

Application
RTOS / OS
Device driver
HAL / BSP
        | memory-mapped registers, interrupts, DMA descriptors
        v
Peripheral / DMA / Accelerator / Interrupt controller
```

Why this figure is useful: it helps you explain where software ends, where hardware begins and how they communicate.

<a id="topic-3"></a>

## Topic 3: Co-Design Vs Co-Simulation

<a id="topic-3-question"></a>

### Question

**Differentiate between co-design and co-simulation in SoC design.**

### CLO Mapping

This topic belongs to **CLO 4: Analyze the Design Methodologies of SoC; TLM and its need in SoC Design**.

Reason: Co-design and co-simulation are part of system-level SoC methodology. Co-design is the design decision process; co-simulation is a verification/modeling activity used during co-design.

### What The Question Is Asking

The examiner wants you to avoid mixing two terms:

```text
Co-design = deciding and developing hardware/software together.
Co-simulation = simulating hardware/software models together.
```

For full marks, define both, compare them and explain their relationship.

<a id="topic-3-explanation"></a>

### Main Explanation

**Co-design** and **co-simulation** are related but not the same.

**Co-design** is a methodology. It covers system requirements, architecture exploration, hardware/software partitioning, interface definition, hardware development, software development and system optimization.

**Co-simulation** is a simulation technique. It runs hardware and software models together so the designer can observe interaction before final silicon.

Important definitions:

```text
Co-design = joint design and partitioning of hardware and software.
Co-simulation = joint execution/simulation of hardware and software models.
```

So, co-simulation is one activity inside the larger co-design process.

Detailed source notes are kept in [sources/CLO4_Topic3_sources.md](<sources/CLO4_Topic3_sources.md>).

#### Co-Design

Co-design asks:

```text
What should be implemented in hardware?
What should be implemented in software?
Which architecture should be used?
How should hardware and software communicate?
Will the design meet performance, power, area and flexibility goals?
```

Co-design includes:

- requirement analysis,
- functional modeling,
- architecture exploration,
- hardware/software partitioning,
- interface specification,
- hardware RTL design,
- software driver/application development,
- co-verification,
- system integration.

Co-design is about **making design decisions**.

#### Co-Simulation

Co-simulation asks:

```text
When hardware and software execute together, do they behave correctly?
```

It checks whether software correctly controls hardware and whether hardware responds as expected.

Co-simulation may connect:

- C/SystemC model of hardware with embedded software,
- TLM platform model with software,
- RTL simulator with processor instruction-set simulator,
- RTL hardware model with C driver model,
- emulator/FPGA prototype with real software.

Co-simulation is about **checking interaction**.

#### Simple Example

Suppose an SoC has a video accelerator.

During **co-design**, the team decides:

- video filtering should be hardware,
- user settings and mode control should be software,
- CPU will configure accelerator registers,
- DMA will move frames,
- interrupt will signal completion,
- memory bandwidth must support frame rate.

During **co-simulation**, the team runs:

- software driver,
- CPU/ISS or platform model,
- DMA model,
- accelerator model,
- memory/interconnect model.

Then the team checks:

- Did software program the correct registers?
- Did DMA fetch the correct buffer?
- Did the accelerator produce the expected result?
- Did interrupt occur at the correct time?
- Did total latency meet the frame deadline?

<a id="topic-3-comparison"></a>

### Comparison Table

| Point | Co-Design | Co-Simulation |
|---|---|---|
| Meaning | Joint hardware/software design methodology | Joint simulation of hardware/software models |
| Main question | What should hardware and software do? | Do hardware and software work together correctly? |
| Stage | Starts early at system-level design | Used during modeling, verification and integration |
| Main output | Partition, architecture, interfaces, implementation plan | Simulation results, bugs, traces, performance observations |
| Focus | Design decision and optimization | Verification and validation |
| Uses | HW/SW partitioning, architecture exploration, tradeoff analysis | Driver testing, register checking, interrupt/DMA behavior, timing validation |
| Models used | Functional models, architectural models, TLM, cost/performance models | ISS, RTL simulator, TLM platform, SystemC model, software simulator |
| Example question | Should encryption be hardware or software? | Does software correctly program the encryption hardware? |
| Relation | Larger process | Tool/activity inside co-design |

Exam line: **Co-design decides the hardware/software split; co-simulation checks whether the selected hardware and software models work together.**

<a id="topic-3-how-cosim-works"></a>

### How Co-Simulation Works

Co-simulation usually connects two or more simulators/models so they move forward in a coordinated way.

Example setup:

```text
Embedded software
      |
      v
Instruction Set Simulator / CPU model
      |
      v
Bus or TLM interconnect model
      |
      v
RTL or high-level hardware model
      |
      v
Memory / peripheral / accelerator model
```

#### What Happens During Co-Simulation

1. Software executes on a CPU model or instruction set simulator.
2. Software writes a memory-mapped register.
3. The bus/TLM model transfers this register write to the hardware model.
4. The hardware model changes state or starts processing.
5. Hardware may access memory or use DMA.
6. Hardware sets status bits or raises an interrupt.
7. Software reads status or enters an interrupt service routine.
8. The simulation trace shows whether the interaction was correct.

#### What Co-Simulation Can Find

Co-simulation can find errors such as:

- wrong register address,
- wrong register bit field,
- wrong initialization order,
- driver waits for a status bit that hardware never sets,
- hardware interrupt is not cleared correctly,
- DMA uses wrong address or buffer length,
- software assumes zero latency but hardware has delay,
- hardware and software disagree on data format,
- bus bandwidth is too low,
- real-time deadline is missed.

#### Levels Of Co-Simulation

| Level | Meaning | Use |
|---|---|---|
| Algorithm/C co-simulation | Software-like functional models run together | Early behavior checking |
| TLM co-simulation | Transaction-level platform and software model | Fast architecture/performance exploration |
| RTL plus ISS co-simulation | RTL hardware with processor instruction simulator | Detailed driver and hardware interaction |
| Emulation/prototyping | Hardware mapped to emulator or FPGA with software | Faster pre-silicon software validation |

#### Why Co-Simulation Is Not Enough Alone

Co-simulation checks behavior for simulated scenarios, but it does not automatically choose the best architecture or partition. Co-design is still needed to decide the system structure and tradeoffs. Co-simulation supports co-design by giving feedback.

Exam line: **Co-simulation is evidence for co-design decisions, but it is not the whole co-design methodology.**

<a id="topic-3-final-answer"></a>

### Final Exam-Ready Answer

Co-design and co-simulation are related concepts in SoC design, but they are different. Hardware-software co-design is the complete methodology used to design hardware and software together. It starts from system requirements, builds functional and architectural models, performs hardware/software partitioning, defines interfaces, develops hardware and software and optimizes the complete system.

Co-simulation is a verification and modeling technique used within co-design. It runs hardware and software models together to check whether they interact correctly. For example, software may run on an instruction set simulator while hardware is represented by a TLM or RTL model. Register writes, interrupts, DMA transfers and memory accesses can be observed during simulation.

The difference is that co-design asks what should be implemented in hardware and software, while co-simulation checks whether the selected hardware and software models work together. Co-design produces architecture, partitioning and interface decisions. Co-simulation produces traces, performance results and bug reports.

For example, in a camera SoC, co-design decides that pixel filtering should be implemented in hardware and camera mode control should be software. Co-simulation then runs the driver, DMA model, accelerator model and memory model together to verify register programming, frame transfer, interrupt behavior and latency. Thus, co-simulation supports co-design, but co-design is the larger methodology.

<a id="topic-3-technical-words"></a>

### Technical Words To Use For Marks

- **Co-design** (write this because it means joint hardware/software design.)
- **Co-simulation** (write this because it means joint simulation of hardware/software models.)
- **HW/SW partitioning** (write this because co-design decides the hardware/software split.)
- **Architecture exploration** (write this because co-design compares design alternatives.)
- **TLM - Transaction-Level Modeling** (write this because co-simulation often uses transaction-level platform models.)
- **ISS - Instruction Set Simulator** (write this because software may run on an ISS during co-simulation.)
- **RTL - Register Transfer Level** (write this because detailed hardware models may be RTL in co-simulation.)
- **SystemC** (write this because it is commonly used for ESL/TLM modeling.)
- **Memory-mapped registers** (write this because software controls hardware through registers.)
- **Interrupt** (write this because hardware notifies software during co-simulation.)
- **DMA - Direct Memory Access** (write this because data-transfer behavior is often verified in co-simulation.)
- **Trace / waveform** (write this because simulation produces observable evidence of behavior.)
- **Verification** (write this because co-simulation is mainly a verification activity.)

<a id="topic-3-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 174758.png](<images/Screenshot 2026-05-12 174758.png>) contains **Codesign vs Co-simulation, Architectural models**.
2. **Draw this relationship figure**:

```text
Hardware-Software Co-Design
    |
    +-- requirements
    +-- architecture exploration
    +-- HW/SW partitioning
    +-- interface definition
    +-- hardware + software implementation
    +-- co-simulation
    +-- integration

Co-simulation is one verification activity inside co-design.
```

3. **Draw this co-simulation model**:

```text
Software / driver
      |
CPU model or ISS
      |
TLM bus / interconnect
      |
RTL or high-level hardware model
      |
Memory / DMA / accelerator
```

<a id="topic-4"></a>

## Topic 4: Architectural Models

<a id="topic-4-question"></a>

### Question

**Explain architectural models in SoC design.**

### CLO Mapping

This topic belongs to **CLO 4: Analyze the Design Methodologies of SoC; TLM and its need in SoC Design**.

Reason: Architectural models are used in ESL/TLM-based SoC design to evaluate processors, buses, memories, accelerators, software and communication before final RTL implementation.

### What The Question Is Asking

The examiner is asking how designers represent an SoC architecture before detailed RTL is complete.

For full marks, answer:

1. Define architectural model.
2. Explain why it is needed.
3. Differentiate functional model and architectural model.
4. Explain what components are modeled.
5. Explain mapping of functions to architecture.
6. Explain TLM and abstraction levels.
7. Give examples and a figure.

<a id="topic-4-explanation"></a>

### Main Explanation

An **architectural model** is an abstract model of the SoC structure used to evaluate how the system will be implemented. It represents major architecture components such as processors, memories, buses/interconnects, accelerators, peripherals and software execution resources.

Important definition:

```text
An architectural model is a high-level representation of the SoC architecture
that shows processing resources, memories, communication paths, peripherals,
software execution resources and their timing/performance behavior before
final RTL implementation.
```

The functional architecture co-design PPT says that after the functional specification is developed, a candidate architecture or family of architectures is defined. It lists architectural components such as microprocessors, microcontrollers, DSPs, buses, memories, peripherals, RTOS and dedicated hardware processing units such as MPEG decoders. It also says the functional specification is decomposed and mapped onto architectural blocks.

Detailed source notes are kept in [sources/CLO4_Topic4_sources.md](<sources/CLO4_Topic4_sources.md>).

#### Functional Model Vs Architectural Model

These two models are different.

| Model | Meaning | Main Question |
|---|---|---|
| Functional model | Describes what the system does | Is the required behavior correct? |
| Architectural model | Describes how the system may be built | Can this architecture meet performance, power and cost goals? |

Example:

Functional model:

```text
Input video -> filter -> compress -> store/transmit
```

Architectural model:

```text
CPU runs control software.
DMA moves video frames.
Hardware accelerator performs filtering.
DDR memory stores frame buffers.
AXI interconnect carries traffic.
Interrupt controller notifies CPU when work is complete.
```

The functional model is behavior-centered. The architectural model is resource-centered.

#### Why Architectural Models Are Needed

Architectural models are needed because starting directly at RTL is too slow and risky for large SoCs.

They help answer questions such as:

- How many processors are needed?
- Should a function run on CPU, DSP or accelerator?
- Is the memory bandwidth enough?
- Is the bus/interconnect a bottleneck?
- How large should buffers be?
- What is the expected latency?
- Can real-time deadlines be met?
- Does the architecture support software scheduling?
- Is power/area reasonable?
- Which design option should be selected before RTL?

Exam line: **Architectural modeling allows design-space exploration before the expensive RTL and physical-design stages.**

<a id="topic-4-types"></a>

### Types Of Architectural Models

#### 1. Processor Model

A **processor model** represents a CPU, microcontroller or DSP used to execute software.

It may model:

- instruction execution speed,
- pipeline behavior,
- cache behavior,
- interrupt handling,
- memory-access latency,
- software task execution time.

At high level, it may be an approximate performance model. At a more detailed level, it may be an **ISS - Instruction Set Simulator** that executes the processor instruction set.

Why it matters: software performance depends on the processor, cache and memory system.

#### 2. Memory Model

A **memory model** represents storage and memory access behavior.

It may model:

- SRAM/DRAM capacity,
- latency,
- bandwidth,
- arbitration delay,
- refresh behavior for DRAM,
- cache misses,
- buffer size.

Why it matters: many SoCs fail performance goals because the memory system cannot supply data fast enough.

#### 3. Interconnect / Bus Model

An **interconnect model** represents communication between masters and slaves.

Examples:

- AMBA AXI bus,
- AMBA APB peripheral bus,
- crossbar,
- Network-on-Chip,
- bus bridge.

It may model:

- transaction latency,
- bandwidth,
- arbitration,
- contention,
- priority,
- burst transfers,
- address decoding.

Why it matters: even if each block is fast, the SoC can be slow if the interconnect is congested.

#### 4. Accelerator Model

An **accelerator model** represents dedicated hardware for a specific task.

It may model:

- processing latency,
- throughput,
- input/output buffers,
- register interface,
- DMA behavior,
- interrupts,
- power estimate.

Why it matters: co-design decisions depend on whether an accelerator gives enough benefit to justify area and verification cost.

#### 5. Peripheral Model

A **peripheral model** represents I/O blocks such as UART, SPI, I2C, USB, Ethernet, timers or GPIO.

It may model:

- register behavior,
- interrupts,
- protocol timing,
- data transfer rate,
- error flags,
- software-visible status.

Why it matters: embedded software and drivers depend heavily on peripheral behavior.

#### 6. RTOS / Software Scheduling Model

An **RTOS model** represents task scheduling, interrupt handling and software timing.

It may model:

- task priorities,
- context-switch overhead,
- timer ticks,
- interrupt latency,
- message queues,
- synchronization.

Why it matters: real-time behavior depends on both hardware speed and software scheduling.

#### 7. Power/Area/Cost Model

A **power/area/cost model** estimates implementation cost before the final design.

It may estimate:

- silicon area,
- dynamic power,
- leakage power,
- memory size cost,
- accelerator cost,
- bus/interconnect cost.

Why it matters: the fastest architecture may be unacceptable if it exceeds area or power budget.

#### 8. Performance Model

A **performance model** estimates latency, throughput and utilization.

It may answer:

- How long does one transaction take?
- Can the system process required frames/packets/samples per second?
- Which block is idle or overloaded?
- Does memory bandwidth limit the system?

Why it matters: performance must be checked before RTL, because late architecture changes are expensive.

<a id="topic-4-mapping"></a>

### Function-Architecture Mapping

The co-design PPT describes mapping as assigning each function from the functional model to a hardware or software resource in the architecture model.

Important definition:

```text
Function-architecture mapping means assigning every functional component
to an architectural resource such as a CPU task, DSP task, hardware accelerator,
memory block, peripheral or communication path.
```

Example functional model:

```text
Capture image -> filter -> compress -> encrypt -> transmit
```

Possible mapping:

| Function | Architectural Resource | Why |
|---|---|---|
| Capture image | Sensor interface hardware | Needs precise external timing |
| Filter image | Hardware accelerator | High pixel throughput needed |
| Compress image | DSP or accelerator | Compute-intensive task |
| Encrypt data | Crypto accelerator | Fast and low-power security operation |
| Transmit data | Software protocol stack + network peripheral | Flexible protocol handling |

After mapping, the designer evaluates:

- processor load,
- accelerator utilization,
- memory bandwidth,
- communication latency,
- power and area,
- real-time deadlines.

If the architecture fails, the designer changes the mapping or architecture.

#### Design Space Exploration

**DSE** means **Design Space Exploration**. It is the process of comparing multiple architectural choices before selecting the final design.

Examples of design-space choices:

- one CPU vs two CPUs,
- CPU only vs CPU plus accelerator,
- small cache vs large cache,
- shared memory vs local memory,
- bus vs Network-on-Chip,
- software compression vs hardware compression.

Architectural models make DSE practical because they run faster than detailed RTL and allow early comparison.

Exam line: **Architectural models convert a functional specification into candidate implementations and allow mapping, simulation and performance analysis before RTL.**

<a id="topic-4-tlm"></a>

### TLM And Abstraction Levels

**TLM** means **Transaction-Level Modeling**. It models communication as transactions instead of low-level pin toggles.

For example, a pin-level bus model may describe every clock edge and signal:

```text
addr, data, valid, ready, write, byte_enable, response
```

A TLM model may describe the same operation as:

```text
write(address, data)
read(address)
burst_transfer(start_address, length)
```

Why TLM is useful:

- faster simulation than RTL,
- easier architecture exploration,
- supports early software development,
- models communication without full signal detail,
- helps evaluate latency, bandwidth and contention,
- suitable for co-simulation with software.

#### Why TLM Is Needed In SoC Design

SoC design contains many communicating blocks. A CPU reads and writes registers. A DMA controller transfers buffers. An accelerator reads input data and writes output data. A memory controller accepts bursts. A peripheral raises interrupts. If all of this is modeled only at RTL from the beginning, simulation becomes slow and architectural exploration becomes difficult.

TLM solves this by changing the question from:

```text
What does every bus signal do on every clock cycle?
```

to:

```text
Which component sends what transaction to which component,
with what address/data/command/response and approximate timing?
```

This abstraction is exactly why TLM is useful in CLO4. It supports:

- **architecture exploration**: compare bus, NoC, memory and accelerator alternatives,
- **performance modeling**: estimate latency, bandwidth and contention,
- **early software development**: run drivers and firmware on a virtual platform,
- **hardware/software co-design**: check whether software and hardware partitioning works,
- **model reuse**: reuse standardized transaction-level models across projects,
- **co-simulation**: connect software models, CPU models and hardware models.

Accellera describes SystemC TLM as important for architectural exploration, performance analysis, virtual platforms for software development and functional verification. This directly matches the SoC design use case.

#### Transaction Payload

A TLM transaction usually carries information similar to a bus operation, but in a compact abstract form.

Typical payload fields:

| Field | Meaning | Example |
|---|---|---|
| Command | Type of operation | read or write |
| Address | Target address | `0x4000_0000` |
| Data | Data transferred | register value or memory data |
| Length | Number of bytes | 4 bytes, 64 bytes |
| Byte enable | Which bytes are valid | partial register/memory write |
| Response | Success/error result | OK, error, retry |
| Delay | Timing annotation | 20 ns latency |

Example:

```text
Transaction:
command  = WRITE
address  = ACCEL_CONTROL
data     = START
response = OK
delay    = 10 ns
```

This single transaction may represent many RTL-level signal transitions.

#### TLM Vs RTL Example

Assume software reads a UART status register.

At RTL, the model must evaluate signals such as:

```text
PADDR, PSEL, PENABLE, PWRITE, PRDATA, PREADY, PSLVERR, clock, reset
```

At TLM, the model may represent this as:

```text
status = read(UART_STATUS_ADDRESS)
```

The TLM model can still return:

- the status value,
- an error response,
- an approximate delay,
- debug information.

But it does not need to simulate every APB signal transition unless that detail is required.

#### Timing Detail In TLM

TLM is not always "no timing." It can have different timing accuracy.

| TLM Style | Timing Detail | Use |
|---|---|---|
| Untimed functional model | No meaningful timing | check behavior only |
| Loosely timed model | rough timing annotations | fast software development and virtual platforms |
| Approximately timed model | more ordered timing phases, contention and arbitration | performance and architecture analysis |
| Cycle-accurate model | every clock cycle modeled | detailed hardware timing, slower |
| RTL model | signal-level and register-transfer detail | implementation and verification |

Important point:

```text
TLM is an abstraction family. The designer chooses accuracy based on the question.
```

If the question is "Does the driver program the correct register?", a loosely timed model may be enough. If the question is "Does the memory bus meet bandwidth under contention?", an approximately timed model is more appropriate. If the question is "Does the valid/ready handshake obey protocol cycle by cycle?", RTL is needed.

#### Temporal Decoupling And DMI

Two TLM speed ideas are useful for exam depth.

**Temporal decoupling** means a model can run ahead of the global simulation clock and synchronize later. This reduces frequent simulator context switches and improves speed.

Example:

```text
CPU model executes many instructions locally,
then synchronizes with global simulation time after a quantum.
```

**DMI - Direct Memory Interface** allows a model to access modeled memory more directly when it is safe, instead of going through the full interconnect transaction path every time.

Why these matter:

- they make virtual platforms much faster,
- they help boot software and run test programs,
- they reduce simulation overhead,
- they are useful when exact bus contention is not the focus.

#### TLM Accuracy Warning

TLM models must be used carefully. If a model is too abstract, it may hide real hardware issues.

Possible risks:

- ignoring arbitration may hide bus bottlenecks,
- ignoring clock cycles may hide latency problems,
- ignoring protocol details may miss handshake bugs,
- inaccurate peripheral models may mislead driver development,
- wrong timing annotations may lead to incorrect performance conclusions.

Therefore, TLM models must be validated and refined as the design matures.

Exam line: **TLM gives speed by abstraction, but the abstraction must match the design question being answered.**

#### Abstraction Levels In SoC Modeling

| Level | Meaning | Speed | Detail |
|---|---|---|---|
| Algorithm / functional model | Describes required behavior | Very fast | Low implementation detail |
| Architectural model | Models processors, memories, buses and accelerators | Fast | Medium detail |
| TLM model | Models communication as transactions | Fast to medium | More communication detail |
| Cycle-accurate model | Models behavior cycle by cycle | Slower | High timing detail |
| RTL model | Register-transfer hardware description | Slow | Detailed hardware implementation |
| Gate-level model | Synthesized gates and timing | Slowest | Physical implementation detail |

The co-design PPT says the functional model is gradually refined into an architectural model, architectural components communicate at transaction level, and the model can later be refined into RTL through high-level synthesis or RTL handoff.

#### Refinement Path From ESL/TLM To RTL

The important idea is **gradual refinement**.

```text
Functional model
    |
    v
ESL architectural model
    |
    v
TLM platform model
    |
    v
Approximately timed / cycle-aware model
    |
    v
RTL implementation
    |
    v
Gate-level netlist and physical implementation
```

At each step, the model becomes more detailed and usually slower:

- functional model checks correct algorithm behavior,
- ESL architectural model checks system organization,
- TLM model checks communication and software interaction,
- approximately timed model checks latency/contention more carefully,
- RTL model implements exact cycle-level hardware behavior,
- gate-level model checks synthesized implementation effects.

This refinement path is why ESL/TLM is not separate from real design. It is the early part of the design flow that guides what the RTL should become.

#### Why Not Start Directly With RTL?

RTL is detailed and accurate, but it is slow to create and slow to simulate. If a wrong architecture is discovered at RTL stage, changing processors, memory hierarchy or interconnect may require major redesign. Architectural modeling avoids this by checking big design choices earlier.

Exam line: **TLM is important in SoC design because it gives a fast middle level between pure functional models and detailed RTL.**

<a id="topic-4-final-answer"></a>

### Final Exam-Ready Answer

An architectural model is a high-level representation of an SoC architecture used to evaluate implementation choices before final RTL design. It describes the major resources of the system, such as processors, microcontrollers, DSPs, buses, memories, peripherals, RTOS, accelerators and communication paths.

Architectural models are different from functional models. A functional model describes what the system does, while an architectural model describes how the system may be built. For example, a functional model may say that video data is captured, filtered, compressed and stored. An architectural model decides whether these functions run on a CPU, DSP, hardware accelerator or peripheral, and how data moves through memory and interconnect.

Architectural modeling is needed because SoC design has many possible implementation choices. Designers must decide the number and type of processors, memory hierarchy, bus/interconnect structure, accelerator placement, buffer sizes, software scheduling and communication mechanisms. These decisions affect performance, power, area, cost and time-to-market. Architectural models allow design-space exploration before expensive RTL implementation.

In function-architecture co-design, the functional model is decomposed and mapped to architectural resources. Each function is assigned to hardware or software, and the resulting architecture is evaluated for latency, throughput, bandwidth, utilization and real-time deadlines. If performance is insufficient, the designer may add an accelerator, change memory size, change bus architecture or move a function from software to hardware.

TLM, or Transaction-Level Modeling, is important in architectural modeling because it represents communication as read/write transactions rather than individual pin-level signals. This allows faster simulation and early software development. Architectural models can later be refined into RTL and finally into gate-level implementation. Thus, architectural models connect abstract system behavior to practical SoC implementation.

For deeper understanding, ESL and TLM reduce design risk by allowing the SoC team to work before detailed RTL exists. At ESL, the team can model the whole system at a high abstraction level and explore architecture choices. With TLM, communication between CPU, memory, DMA, peripherals and accelerators can be represented as transactions. This makes simulation much faster because the simulator does not evaluate every bus signal and clock edge. Instead, it evaluates higher-level operations such as `read`, `write`, `burst_transfer` or `interrupt`.

TLM models may be loosely timed or approximately timed. Loosely timed models are useful for early software development and virtual platforms because they run very fast. Approximately timed models add more timing, ordering, contention and arbitration detail, so they are better for performance analysis. However, TLM does not replace RTL. RTL is still required for detailed signal-level implementation, protocol checking, synthesis and timing sign-off. Therefore, ESL/TLM should be written as early design and architecture exploration methodology, not as final hardware implementation.

### Short 10-Mark Exam Answer

An architectural model is an abstract model of the SoC structure. It represents processors, memories, buses, peripherals, RTOS, accelerators and communication paths. It is used to evaluate system organization before detailed RTL implementation.

A functional model describes what the system does, while an architectural model describes how the system will be realized. During function-architecture mapping, each function is assigned to a hardware or software resource. The designer then analyzes latency, throughput, bandwidth, power, area and real-time behavior.

Architectural models are useful for design-space exploration. They help compare alternatives such as CPU-only design, CPU plus accelerator, different memory sizes, bus vs NoC and different software scheduling options. TLM is often used because it models communication as transactions, giving faster simulation than RTL while still capturing important system behavior. Therefore, architectural models are essential for early SoC design decisions.

ESL, or Electronic System Level, is the abstraction level above RTL where whole-system decisions are made. TLM, or Transaction-Level Modeling, is a common ESL modeling style for communication. In TLM, components communicate through transaction calls rather than pin-level signals. This allows fast virtual platforms, early driver/software development and early performance estimation. The designer can start with an untimed or loosely timed model for speed, then refine toward approximately timed, cycle-accurate and finally RTL models as more detail is needed.

<a id="topic-4-technical-words"></a>

### Technical Words To Use For Marks

- **Architectural model** (write this because it is the exact topic.)
- **Functional model** (write this because the architectural model is refined from behavior.)
- **Function-architecture mapping** (write this because it explains assigning functions to resources.)
- **DSE - Design Space Exploration** (write this because architectural models are used to compare alternatives.)
- **ESL - Electronic System Level** (write this because architectural modeling occurs above RTL.)
- **TLM - Transaction-Level Modeling** (write this because architectural components communicate at transaction level.)
- **Transaction** (write this because TLM abstracts bus/register/memory communication into read, write and burst operations.)
- **Virtual platform** (write this because TLM platforms allow software and driver development before silicon.)
- **Initiator** (write this because CPUs, DMA engines and accelerator masters start TLM transactions.)
- **Target** (write this because memories, peripherals and register blocks respond to TLM transactions.)
- **LT - Loosely Timed** (write this because it explains the fastest TLM style used for early software and virtual platforms.)
- **AT - Approximately Timed** (write this because it explains the more timing-aware TLM style used for performance analysis.)
- **Temporal decoupling** (write this because it explains why TLM simulation can be much faster than RTL.)
- **DMI - Direct Memory Interface** (write this because it is a TLM speed mechanism for modeled memory access.)
- **Timed model** (write this because timing annotations are needed for performance conclusions.)
- **Untimed model** (write this because some early models check only function, not timing.)
- **Cycle-accurate model** (write this because it is more detailed than TLM and closer to RTL behavior.)
- **Bit-accurate model** (write this because some ESL models must produce exact data values even if timing is abstract.)
- **Processor / microcontroller / DSP** (write these because they are common software execution resources.)
- **RTOS - Real-Time Operating System** (write this because software scheduling may be part of the architecture.)
- **Bus / interconnect / NoC** (write these because communication architecture strongly affects performance.)
- **Memory model** (write this because memory bandwidth and latency often determine SoC performance.)
- **Accelerator** (write this because dedicated hardware is a major architecture choice.)
- **Performance model** (write this because latency, throughput and utilization must be estimated early.)
- **Bandwidth** (write this because communication capacity is a key architectural constraint.)
- **Latency** (write this because response time is a key performance metric.)
- **RTL - Register Transfer Level** (write this because architectural models are later refined into RTL.)
- **High-level synthesis** (write this because some architectural/behavioral models may be refined automatically toward RTL.)

<a id="topic-4-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 174758.png](<images/Screenshot 2026-05-12 174758.png>) contains **Codesign vs Co-simulation, Architectural models**.
2. **Draw this functional-to-architectural refinement figure**:

```text
Requirements
    |
Functional model
    |
Architecture candidates
    |
Function-architecture mapping
    |
TLM / architectural simulation
    |
Performance and tradeoff analysis
    |
Selected architecture
    |
RTL hardware + embedded software
```

3. **Draw this architectural model figure**:

```text
                   +--------------------+
                   | CPU / Microcontroller |
                   +----------+---------+
                              |
                      AMBA AXI / NoC
        +----------+----------+----------+----------+
        |                     |                     |
   +----v----+          +-----v-----+         +-----v------+
   | Memory  |          | DMA       |         | Accelerator|
   | model   |          | model     |         | model      |
   +---------+          +-----------+         +------------+
        |                     |
   +----v----+          +-----v-----+
   | RTOS /  |          | Peripheral|
   | software|          | models    |
   +---------+          +-----------+
```

Why this figure is useful: it shows that an architectural model is not only hardware logic. It includes processors, communication, memory, accelerators, peripherals and software execution behavior.

4. **Draw this TLM abstraction figure**:

```text
RTL bus view:
addr + data + valid + ready + response + clock cycles + signal toggles

TLM view:
write(address, data, delay)
read(address, delay)
burst_transfer(start_address, length, delay)
```

Why this figure is useful: it shows exactly why TLM is faster than RTL. Many low-level signal events are replaced by one transaction.

5. **Draw this TLM refinement figure**:

```text
Untimed functional model
        |
Loosely timed TLM
        |
Approximately timed TLM
        |
Cycle-accurate model
        |
RTL model
        |
Gate-level model
```

Why this figure is useful: it shows that modeling moves from fast/abstract to slow/detailed as the design matures.

---

## CLO 4 Completion Checklist

- [x] Topic 1: SoC Design Methodologies - TDD, BBD and PBD.
- [x] Topic 2: Hardware-Software Co-Design.
- [x] Topic 3: Co-Design Vs Co-Simulation.
- [x] Topic 4: Architectural Models.
- [x] Full forms and definitions added for key terms.
- [x] Clickable index added for all major sections.
- [x] Figure/image reminders added for exam drawing.
- [x] Separate source files created under `sources/`.
