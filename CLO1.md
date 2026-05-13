# CLO 1 - Introduction: Systems Approach, System Architecture, Components, Hardware/Software And Chip Basics

## Clickable Index

- [CLO 1 Master Definitions](#clo1-master-definitions)
- [CLO 1 Full-Form Review Addendum](#clo1-full-form-review)
- [Topic 1: Introduction To Systems Approach, System Architecture, Components Of System, Hardware And Software, Chip Basics](#topic-1)
  - [Question](#topic-1-question)
  - [CLO Mapping](#topic-1-clo-mapping)
  - [What The Question Is Asking](#topic-1-what-asking)
  - [Main Explanation](#topic-1-main-explanation)
  - [Systems Approach](#topic-1-systems-approach)
  - [System Architecture](#topic-1-system-architecture)
  - [Components Of A System](#topic-1-components)
  - [Hardware And Software](#topic-1-hardware-software)
  - [Chip Basics](#topic-1-chip-basics)
  - [How This Connects To SoC Design Flow](#topic-1-design-flow-link)
  - [Final Exam-Ready Answer](#topic-1-final-answer)
  - [Short 10-Mark Answer](#topic-1-short-answer)
  - [Technical Words](#topic-1-technical-words)
  - [Images / Diagrams](#topic-1-diagrams)

<a id="clo1-master-definitions"></a>

## CLO 1 Master Definitions

Use this section before revising CLO 1. This topic is introductory, so the marks come from writing clear definitions and then connecting them to SoC design decisions.

| Term | Full Form / Meaning | Definition / Why It Matters |
|---|---|---|
| CLO | Course Learning Outcome | The syllabus outcome used to group topics and expected exam answers. |
| SoC | System on Chip | Complete system integrated on one chip, normally including processors, memories, interconnects, peripherals, accelerators, control logic, debug/test logic and embedded software. |
| System | Interacting set of elements | A group of hardware, software, people/processes or subsystems that work together to produce required behavior. In SoC, the system is mainly hardware plus software integrated to meet an application need. |
| Systems approach | Whole-system design view | Design method that starts from requirements, interfaces, constraints and tradeoffs rather than optimizing one block alone. |
| Systems engineering | Multi-disciplinary system development approach | Methodical approach for defining, designing, realizing, integrating, verifying, operating and retiring a system. |
| System boundary | Limit of what is inside the system | Defines what belongs to the SoC/system and what is external environment. |
| Environment | External context of the system | External devices, users, power supply, sensors, actuators, board, software ecosystem and operating conditions. |
| Stakeholder | Person/group with interest in system | Customer, designer, verification engineer, software developer, manufacturer, user or maintainer. |
| Requirement | Need the system must satisfy | Statement of required function, performance, power, cost, safety, reliability or interface behavior. |
| Specification | Precise design target | More detailed, measurable description derived from requirements. |
| Constraint | Limitation on design choices | Power, area, cost, schedule, process node, temperature, memory size, latency or standards compliance. |
| Tradeoff | Engineering compromise | Improving one metric may worsen another, such as increasing performance but increasing power and area. |
| System architecture | High-level organization of a system | Defines major building blocks, their functions, relationships, interfaces and design principles. |
| Functional architecture | What functions the system performs | Describes operations such as sensing, computing, storing, communicating and controlling. |
| Logical architecture | Abstract block organization | Maps functions into logical blocks and interactions without final physical implementation detail. |
| Physical architecture | Actual implementation structure | Maps logical blocks into processors, memories, buses, accelerators, IP blocks and physical chip/board resources. |
| Component | System building block | Processor, memory, interconnect, peripheral, accelerator, software module or IP block. |
| Subsystem | Group of related components | Example: CPU subsystem, memory subsystem, communication subsystem or power-management subsystem. |
| Interface | Boundary for communication | Defines how components exchange signals, data, commands, timing and control. |
| Hardware | Physical electronic implementation | Circuits, processors, memories, accelerators, interconnects, peripherals and gates. |
| Software | Instructions executed by hardware | Program code running on processors, including firmware, drivers, operating system and applications. |
| Firmware | Low-level embedded software | Software closely tied to hardware, often used for boot, initialization, control registers and device management. |
| Embedded software | Software inside embedded system/SoC product | Code running on SoC processors to control hardware and implement product behavior. |
| GPP | General-Purpose Processor | Flexible processor used to run many software tasks, operating systems or control functions. |
| ASIC | Application-Specific Integrated Circuit | Custom chip optimized for a specific function or product. |
| ASIP | Application-Specific Instruction Processor | Programmable processor customized for a specific application/domain. |
| FPGA | Field-Programmable Gate Array | Reconfigurable hardware fabric that can be programmed after manufacturing. |
| IP | Intellectual Property | Reusable design block, such as processor core, memory controller, bus interface or accelerator. |
| Processor | Programmable hardware execution unit | Fetches, decodes and executes instructions from software. |
| Memory | Storage component | Stores program code, data, buffers, configuration and intermediate results. |
| Interconnect | Communication fabric | Connects processors, memories, accelerators and peripherals inside the SoC. |
| Peripheral | Support/control block | UART, SPI, GPIO, timer, interrupt controller, USB, Ethernet or other I/O/control unit. |
| Accelerator | Specialized hardware block | Performs a specific computation faster or more efficiently than software on a general processor. |
| Analog/mixed-signal block | Non-purely digital block | ADC, DAC, PLL, sensor interface, RF block or power-management circuit. |
| IC | Integrated Circuit | Circuit fabricated on a semiconductor die. |
| Chip | Packaged or unpackaged IC | Common term for integrated circuit product. |
| Die | Silicon piece containing the circuit | Individual chip cut from a processed wafer. |
| Wafer | Thin round silicon slice | Many die are fabricated together on one wafer. |
| Package | Protective/electrical enclosure | Connects the die to external pins/balls and protects it mechanically. |
| Transistor | Basic electronic switching device | Fundamental building block of digital logic and memory. |
| CMOS | Complementary Metal-Oxide-Semiconductor | Dominant technology for digital integrated circuits. |
| Clock cycle | One period of system clock | Basic timing unit in synchronous digital hardware. |
| Cycle time | Time duration of one clock cycle | Determines clock frequency and affects performance. |
| Critical path | Longest timing path | Sets minimum clock period for synchronous logic. |
| Latency | Time for one operation to complete | Important for response time and real-time behavior. |
| Throughput | Work completed per unit time | Important for streaming, data processing and system capacity. |
| Area | Silicon area consumed | Affects die cost, yield, routing and integration density. |
| Yield | Fraction/number of good die | Determines how many defect-free chips come from a wafer and strongly affects cost. |
| Power | Energy consumed per unit time | Affects battery life, heat, reliability and package/cooling needs. |
| Dynamic power | Switching power | Power consumed when capacitances charge/discharge during activity; roughly related to capacitance, voltage and frequency. |
| Leakage power | Static power | Power consumed even when logic is idle because transistors leak current. |
| Reliability | Probability of correct operation over time | Affected by defects, temperature, voltage, aging, noise and radiation. |
| Configurability | Ability to adapt after or near design time | Includes FPGA/reconfigurable logic, parameterized IP and software programmability. |
| PPA | Power, Performance, Area | Main chip design quality tradeoff. |
| NRE | Non-Recurring Engineering cost | One-time design cost for developing a chip/product. |
| Recurring cost | Per-unit production cost | Cost repeated for each manufactured chip/product. |
| Time-to-market | Time needed to deliver product | Important because late products may lose market value. |
| Verification | Checking design against specification | Ensures the design was built correctly. |
| Validation | Checking against user/stakeholder need | Ensures the right system was built. |
| RTL | Register Transfer Level | Hardware design abstraction describing registers and data transfers between them. |
| HDL | Hardware Description Language | Language such as Verilog, SystemVerilog or VHDL used to describe digital hardware. |
| CPU | Central Processing Unit | Main programmable processor that runs firmware, operating system code or application software. |
| DSP | Digital Signal Processor | Processor or datapath optimized for signal-processing operations such as multiply-accumulate, filtering and streaming data. |
| DMA | Direct Memory Access | Hardware engine that moves data between memory, peripherals and accelerators without the CPU copying every word. |
| SRAM | Static Random Access Memory | Fast volatile memory used for caches, scratchpads, buffers and on-chip memories. |
| DRAM | Dynamic Random Access Memory | Dense volatile memory used for large main memory; stores data as charge and needs refresh. |
| ROM | Read Only Memory | Non-volatile memory used for fixed boot code, reset vectors or constants. |
| TCM | Tightly Coupled Memory | Low-latency on-chip memory closely connected to a processor for predictable instruction/data access. |
| NoC | Network on Chip | Packet-based on-chip interconnect that connects many processors, memories and IP blocks through routers and links. |
| AXI | Advanced eXtensible Interface | AMBA high-performance memory-mapped interface used for processor, memory and accelerator traffic. |
| AHB | Advanced High-performance Bus | AMBA bus protocol used in embedded systems for moderate/high-bandwidth transfers. |
| APB | Advanced Peripheral Bus | AMBA low-complexity bus used for low-bandwidth peripheral register access. |
| UART | Universal Asynchronous Receiver/Transmitter | Serial communication peripheral used for byte-oriented asynchronous communication. |
| SPI | Serial Peripheral Interface | Synchronous serial interface commonly used for sensors, Flash and peripheral devices. |
| GPIO | General-Purpose Input/Output | Programmable digital pins used for simple input/output control. |
| ADC | Analog-to-Digital Converter | Mixed-signal block that converts analog voltage/current into digital values. |
| DAC | Digital-to-Analog Converter | Mixed-signal block that converts digital values into analog output. |
| PLL | Phase-Locked Loop | Clock-generation/synchronization circuit used to generate stable SoC clock frequencies. |
| RF | Radio Frequency | Analog/mixed-signal circuitry for wireless communication frequencies. |
| PMU | Power Management Unit | Hardware controller that manages clocks, resets, power domains and low-power states. |
| JTAG | Joint Test Action Group | Standard low-pin debug/test access mechanism used for boundary scan and chip debug. |
| BIST | Built-In Self-Test | On-chip test logic that lets memories or logic test themselves. |
| OS | Operating System | System software that manages processor, memory, drivers, files, tasks and applications. |
| RTOS | Real-Time Operating System | Operating system designed for predictable task scheduling and interrupt response. |
| AI | Artificial Intelligence | Workload category involving inference/training-style computations, often accelerated by dedicated hardware. |

<a id="clo1-full-form-review"></a>

## CLO 1 Full-Form Review Addendum

Use this addendum when revising the introduction diagrams. In CLO 1, the examiner usually checks whether you can connect high-level system words to actual SoC blocks.

When you write **CPU - Central Processing Unit**, explain that it is the programmable control and execution block. It fetches instructions, runs firmware/software, programs peripherals through registers and coordinates interrupts.

When you write **memory**, do not leave it generic. Mention **SRAM - Static Random Access Memory** for fast on-chip storage, **ROM - Read Only Memory** for boot code, and **DRAM - Dynamic Random Access Memory** for large main memory. This shows that you understand memory is a hierarchy, not one block.

When you write **interconnect**, connect it to **AXI - Advanced eXtensible Interface**, **AHB - Advanced High-performance Bus**, **APB - Advanced Peripheral Bus** or **NoC - Network on Chip**. This shows how components actually communicate inside the SoC.

When you write **peripherals**, give examples with full forms: **UART - Universal Asynchronous Receiver/Transmitter**, **SPI - Serial Peripheral Interface** and **GPIO - General-Purpose Input/Output**. This makes the answer concrete instead of abstract.

When you write **hardware/software partitioning**, explain that repeated high-throughput work may become hardware accelerators, while control, configuration and changing behavior remain software. This is the bridge from CLO 1 introduction to CLO 4 co-design.

One-line memory aid:

```text
Systems approach decides the whole product view.
System architecture decides the major blocks and interfaces.
Hardware/software partitioning decides what is implemented in circuits and what runs as code.
Chip basics decide whether the architecture is practical in time, area, power, reliability and cost.
```

---

<a id="topic-1"></a>

## Topic 1: Introduction To Systems Approach, System Architecture, Components Of System, Hardware And Software, Chip Basics

<a id="topic-1-question"></a>

### Question

**Explain Introduction to Systems Approach, System Architecture, Components of system, Hardware and software, and Chip basics.**

<a id="topic-1-clo-mapping"></a>

### CLO Mapping

This topic belongs to **CLO 1: Familiarize with Design Flow of SoC**.

Reason: Before learning the detailed SoC design flow, the student must understand what a system is, how system architecture is formed, what components make up an SoC, how hardware and software are partitioned, and what chip-level constraints control the design. These are the foundation for requirements, architecture selection, implementation, verification and optimization.

Detailed local PPT/book/web references are kept in [sources/CLO1_Topic1_sources.md](<sources/CLO1_Topic1_sources.md>).

<a id="topic-1-what-asking"></a>

### What The Question Is Asking

The examiner is asking for an introductory system-level answer, not a narrow processor answer. A complete answer must explain:

1. What a **system** is.
2. What the **systems approach** means.
3. What **system architecture** means.
4. What components make up a system or SoC.
5. How hardware and software differ.
6. Why SoC design combines hardware and software.
7. Why chip basics such as time, area, power, reliability and configurability matter.
8. How these ideas connect to the SoC design flow.

Exam answer order:

```text
system -> systems approach -> system architecture ->
components -> hardware/software tradeoff -> chip basics ->
connection to SoC design flow.
```

<a id="topic-1-main-explanation"></a>

### Main Explanation

A **System on Chip** is not only a collection of gates. It is a complete system integrated into one chip. It may contain processors, memories, interconnects, accelerators, peripherals, analog blocks, power/reset/clock blocks, debug/test structures and embedded software.

The important idea is:

```text
The SoC must be designed as a system, not as isolated blocks.
```

If the processor is fast but memory is too slow, the system fails its performance target. If hardware is correct but software cannot program it correctly, the product fails. If a block is optimized for speed but violates power or area budget, the chip may be impractical. If interfaces are unclear, integration fails. Therefore, SoC design begins with a systems approach.

The local lecture [module 1 part 1 introduction to system approach.pdf](<System on chip/module 1 part 1 introduction to system approach.pdf>) says an SoC architecture is an ensemble of processors, memories and interconnects tailored to an application domain. It also says system architecture defines system-level building blocks and their interconnection. The local chip-basics lecture says SoC tradeoffs include time, area, power, reliability and configurability.

NASA's systems engineering material also supports the same idea at a general engineering level: a system is a combination of elements that work together to produce required capability, and systems engineering uses a broad view of requirements, interfaces, tradeoffs and verification.

<a id="topic-1-systems-approach"></a>

### Systems Approach

**Systems approach** means designing by looking at the whole system, its purpose, components, interfaces, constraints and lifecycle instead of optimizing each block independently.

Beginner definition:

```text
Systems approach = understand the complete product need first,
then design components and interfaces so the whole system satisfies that need.
```

In SoC design, this means the designer asks:

- What application is the chip for?
- What performance is required?
- What power limit exists?
- What memory capacity is needed?
- What hardware blocks are required?
- What software will run?
- What interfaces must be supported?
- What standards must be followed?
- What cost and area are acceptable?
- What reliability and safety level is needed?
- How will the system be verified?

#### Why A Systems Approach Is Needed

An SoC is complex because many parts interact.

Example:

```text
CPU is fast.
But memory controller is slow.
So CPU stalls.
System performance is poor.
```

Another example:

```text
Accelerator is very fast.
But software driver cannot feed it data correctly.
So accelerator is underused.
```

Another example:

```text
Memory is large.
But interconnect bandwidth is low.
So display/video traffic misses deadlines.
```

These examples show why local optimization is not enough. The SoC must be judged as a complete system.

#### System Boundary

The **system boundary** defines what is inside the system and what is outside.

For an SoC:

```text
Inside boundary:
CPU, memory controller, SRAM, NoC, peripherals, accelerators, firmware.

Outside boundary:
board DRAM, sensors, display panel, user, power supply, external storage.
```

Why this matters:

- it clarifies design responsibility,
- it defines interfaces,
- it prevents confusion during integration,
- it helps verification planning.

#### Requirements And Specifications

A **requirement** states what the system must achieve.

Example:

```text
The SoC shall process 4K video at 60 frames per second.
```

A **specification** makes the requirement more precise and design-ready.

Example:

```text
The video accelerator shall process 3840 x 2160 frames at 60 fps
with maximum memory bandwidth of X GB/s and power below Y mW.
```

Systems approach converts vague needs into measurable specifications.

#### Constraints

A **constraint** is a limit that the design must obey.

Common SoC constraints:

- power budget,
- die area,
- clock frequency,
- memory bandwidth,
- real-time deadline,
- package pin count,
- process technology,
- cost,
- schedule,
- thermal limit,
- safety/reliability rules.

Good system design balances all constraints rather than maximizing one metric.

#### Verification And Validation

**Verification** asks:

```text
Did we build the system correctly according to specification?
```

**Validation** asks:

```text
Did we build the right system for the user/application need?
```

Both are part of systems approach.

<a id="topic-1-system-architecture"></a>

### System Architecture

**System architecture** is the high-level organization of a system. It defines the major components, their responsibilities, interfaces, relationships and design principles.

For an SoC:

```text
SoC architecture = processors + memories + interconnects + accelerators +
peripherals + software structure + interfaces + constraints.
```

The local PPT says architecture denotes the operational structure and user's view of the system, and that system architecture defines system-level building blocks such as processors and memories and their interconnection.

#### What Architecture Decides

System architecture decides:

- number and type of processors,
- memory hierarchy,
- interconnect/bus/NoC structure,
- hardware accelerators,
- peripheral set,
- hardware/software partitioning,
- clock and power domains,
- address map,
- interrupt structure,
- data movement paths,
- security boundaries,
- verification strategy.

Architecture is therefore the bridge between requirements and implementation.

#### Architecture Vs Implementation

Do not confuse architecture with final gate-level implementation.

| Point | Architecture | Implementation |
|---|---|---|
| Level | High-level organization | Detailed hardware/software realization |
| Question | What blocks and interfaces are needed? | How exactly are they built? |
| Example | CPU + SRAM + AXI bus + accelerator | RTL, gates, layout, firmware code |
| Concern | function, performance, interfaces, tradeoffs | timing, synthesis, placement, routing, code |

#### Views Of Architecture

System architecture can be explained using different views.

| View | Meaning | SoC Example |
|---|---|---|
| Functional view | What the system does | capture image, compress video, transmit data |
| Logical view | How functions are grouped | processor subsystem, memory subsystem, video subsystem |
| Physical view | Actual implementation resources | CPU core, SRAM macro, NoC, DDR controller, accelerator |
| Software view | Software structure | bootloader, firmware, drivers, RTOS, application |
| Interface view | How blocks communicate | AXI bus, interrupts, DMA channels, memory map |
| Performance view | Timing and throughput behavior | latency, bandwidth, fps, cycles per task |
| Power view | Power domains and modes | active, sleep, retention, power gating |

Writing architecture from multiple views gives a mature answer.

#### Example: Camera SoC Architecture

```text
Camera sensor -> image signal processor -> video encoder -> memory -> display/network
                         |
                       CPU controls registers, interrupts and software flow
```

Components:

- sensor interface,
- image accelerator,
- video encoder,
- memory controller,
- CPU,
- DMA,
- interconnect,
- display/network interface,
- firmware/driver.

This example shows why SoC architecture is not only a processor. It is the organization of computation, storage, communication and control.

<a id="topic-1-components"></a>

### Components Of A System

A **component** is a building block of the system. In SoC design, components can be hardware blocks, software modules or interfaces.

#### Main SoC Hardware Components

##### 1. Processor

A **processor** is a programmable hardware block that executes software instructions.

Role:

- runs firmware,
- handles control decisions,
- configures peripherals,
- starts accelerators,
- handles interrupts,
- runs operating system or RTOS,
- manages software tasks.

##### 2. Memory

**Memory** stores instructions, data, buffers and configuration.

Examples:

- register files,
- cache,
- SRAM,
- ROM,
- DRAM,
- Flash,
- scratchpad,
- TCM.

Memory matters because processor performance depends strongly on memory latency and bandwidth.

##### 3. Interconnect

**Interconnect** connects blocks inside the SoC.

Examples:

- bus,
- crossbar,
- Network on Chip,
- AXI/AHB/APB fabric.

It carries addresses, data, commands and responses between processors, memories, accelerators and peripherals.

##### 4. Peripherals

**Peripherals** are support blocks that connect the SoC to external devices or provide control functions.

Examples:

- UART,
- SPI,
- I2C,
- GPIO,
- timers,
- PWM,
- USB,
- Ethernet,
- interrupt controller.

##### 5. Accelerators

An **accelerator** is specialized hardware for a specific task.

Examples:

- video encoder,
- cryptographic engine,
- AI matrix engine,
- image signal processor,
- DSP datapath.

Accelerators are used when software on a general processor is too slow or too power-hungry.

##### 6. Analog And Mixed-Signal Blocks

Some SoCs include analog or mixed-signal circuits.

Examples:

- ADC - Analog-to-Digital Converter,
- DAC - Digital-to-Analog Converter,
- PLL - Phase-Locked Loop,
- RF - Radio Frequency block,
- sensor interface,
- power-management circuits.

##### 7. Clock, Reset And Power Management

These blocks keep the SoC operational.

Examples:

- clock generator,
- PLL,
- reset controller,
- PMU - Power Management Unit,
- voltage regulator interface,
- clock gating,
- power gating.

##### 8. Debug And Test Blocks

Debug and test blocks help development and manufacturing.

Examples:

- JTAG,
- trace unit,
- scan chains,
- BIST,
- debug access port.

##### 9. Software Components

Software is also part of the complete system.

Examples:

- boot ROM code,
- bootloader,
- firmware,
- device drivers,
- HAL - Hardware Abstraction Layer,
- RTOS - Real-Time Operating System,
- operating system,
- middleware,
- application software.

#### Component Interaction

The most important exam point is that components interact.

Example:

```text
CPU configures DMA.
DMA moves data from camera buffer to memory.
Accelerator processes the data.
Interrupt tells CPU processing is complete.
Driver passes result to application.
```

The SoC works only if hardware and software components cooperate correctly.

<a id="topic-1-hardware-software"></a>

### Hardware And Software

One of the most important SoC design decisions is:

```text
Which functions should be implemented in hardware,
and which functions should be implemented in software?
```

This is called **hardware/software partitioning**.

#### Hardware

**Hardware** means physical circuits.

Hardware is good for:

- high performance,
- parallel execution,
- low energy per operation for repeated tasks,
- deterministic timing,
- dedicated real-time processing.

Examples:

- video encoder hardware,
- cryptographic accelerator,
- image filter pipeline,
- memory controller,
- packet classifier.

Limitations:

- less flexible after fabrication,
- harder to change,
- increases area,
- may increase verification effort,
- design mistakes can require costly respin.

#### Software

**Software** means instructions executed by a processor.

Software is good for:

- flexibility,
- programmability,
- updates after product release,
- complex control logic,
- easier debugging,
- reuse across products,
- faster development for changing features.

Examples:

- device drivers,
- protocol stack,
- control algorithm,
- UI logic,
- firmware configuration,
- error handling.

Limitations:

- usually slower than dedicated hardware for data-heavy tasks,
- consumes instruction fetch/decode energy,
- depends on processor speed and memory system,
- may have timing uncertainty due to cache, interrupts or OS scheduling.

#### Why Software Can Be Slower

Software runs on a processor. For every operation, the processor must:

- fetch instruction,
- decode instruction,
- read operands,
- execute,
- access memory if needed,
- write result.

Dedicated hardware can implement the same operation directly as a circuit and exploit parallelism.

Example:

```text
Software loop processes pixels one by one.
Hardware image pipeline processes many pixels in parallel or every clock cycle.
```

#### Why Software Is Still Needed

Software is needed because not every function should become fixed hardware.

Software is better for:

- changing algorithms,
- configuration,
- product variants,
- rare control paths,
- protocol updates,
- user features,
- diagnostics.

#### Hardware/Software Spectrum

The local PPT and textbook place custom ASIC hardware and software on GPPs as two extremes, with ASIPs and FPGAs between them.

```text
Most flexible                                      Fastest / most specialized

Software on GPP -> ASIP -> FPGA/reconfigurable logic -> ASIC hardware
```

| Option | Meaning | Main benefit | Main cost |
|---|---|---|---|
| Software on GPP | Code on general processor | maximum flexibility | lower performance/energy efficiency |
| ASIP | customized instruction processor | domain speedup with programmability | design/tool complexity |
| FPGA | reconfigurable hardware | post-fabrication hardware flexibility | area/power overhead |
| ASIC hardware | fixed custom circuit | best performance/energy for task | least flexible |

#### Performance-Critical Code

A common design idea:

```text
Implement performance-critical parts in hardware.
Keep control, configuration and changing behavior in software.
```

The local lecture gives the common idea that if a small part of code consumes most execution time, implementing that part efficiently in hardware can greatly speed up the application.

#### Example: Video SoC

Software:

- user interface,
- driver,
- configuration,
- error handling,
- file/container management.

Hardware:

- pixel processing pipeline,
- motion estimation,
- video encoding,
- memory DMA,
- display timing.

Reason:

```text
Pixel processing is repetitive and data-heavy, so hardware is efficient.
Control decisions change often, so software is flexible.
```

<a id="topic-1-chip-basics"></a>

### Chip Basics

Chip basics explain whether a system architecture is practical as silicon.

The local chip-basics PPT summarizes five basic SoC tradeoff dimensions:

1. **Time**
2. **Area**
3. **Power**
4. **Reliability**
5. **Configurability**

Modern industry often summarizes the core chip-quality tradeoff as **PPA - Power, Performance, Area**.

#### 1. Time / Performance

**Time** means how long operations take. In synchronous digital hardware, time is organized using clock cycles.

Important terms:

- **clock cycle**: one period of clock,
- **cycle time**: duration of one clock cycle,
- **clock frequency**: cycles per second,
- **critical path**: longest delay path limiting the clock,
- **latency**: time for one operation,
- **throughput**: work completed per unit time.

Example:

```text
Clock frequency = 1 GHz
Cycle time = 1 ns
```

Performance can be improved by:

- pipelining,
- parallelism,
- faster memory,
- accelerators,
- wider datapaths,
- better interconnect,
- optimized software.

But faster design may increase area and power.

#### Pipeline Tradeoff

Pipelining splits work into stages.

```text
Without pipeline:
Instruction completes all work before next begins.

With pipeline:
Different instructions occupy different stages at the same time.
```

Benefit:

- higher throughput.

Cost:

- pipeline registers,
- clock overhead,
- branch penalty,
- hazard handling,
- more complex verification.

#### Cache Miss Example

The chip-basics PPT notes that unanticipated extra cycles can occur due to events such as cache misses.

Example:

```text
CPU expects data in 1 cycle.
Cache miss occurs.
Data comes from lower memory after many cycles.
Processor stalls.
```

So performance depends on architecture and memory system, not only clock frequency.

#### 2. Area

**Area** means silicon area used by the design.

Area matters because:

- larger die costs more,
- fewer die fit on one wafer,
- larger die have lower yield risk,
- routing becomes harder,
- more area can increase leakage power,
- package cost may increase.

The SIA semiconductor FAQ explains that many integrated circuits are formed on one wafer and that yield is the percentage or number of defect-free die or packaged units meeting specifications. Since wafer processing cost is largely paid for the wafer, better yield strongly affects cost per chip.

#### Die, Wafer And Yield

```text
Wafer = large round silicon slice.
Die   = one individual chip cut from wafer.
Yield = fraction/number of good die that pass tests.
```

If die area increases:

- fewer die fit per wafer,
- probability of a defect hitting a die increases,
- cost per good chip increases.

This is why "add more hardware" is not always acceptable.

#### 3. Power

**Power** is energy consumed per unit time.

Power matters because:

- battery life depends on it,
- heat depends on it,
- reliability depends on temperature,
- package/cooling cost depends on it,
- high power may limit clock frequency.

Two major power components:

```text
Total power = dynamic/switching power + static/leakage power
```

**Dynamic power** occurs when signals switch and capacitances charge/discharge.

Simplified relationship:

```text
Dynamic power roughly increases with capacitance, voltage squared and frequency.
```

**Leakage power** occurs even when circuits are not actively switching.

Low-power techniques:

- clock gating,
- power gating,
- voltage scaling,
- frequency scaling,
- sleep/retention modes,
- memory banking,
- hardware acceleration for energy-heavy loops,
- optimized software.

#### 4. Reliability

**Reliability** means the chip continues operating correctly over time and conditions.

Reliability is affected by:

- manufacturing defects,
- temperature,
- voltage noise,
- aging,
- radiation,
- timing margin,
- electromigration,
- soft errors,
- wearout.

Techniques:

- ECC - Error Correction Code,
- parity,
- redundancy,
- watchdog timer,
- lockstep processors,
- BIST - Built-In Self-Test,
- voltage/temperature monitoring,
- safe reset and recovery.

#### 5. Configurability

**Configurability** means the ability to adapt the system without redesigning everything.

Examples:

- software programmability,
- firmware updates,
- configurable IP,
- parameterized cores,
- FPGA fabric,
- programmable accelerators,
- reusable platforms.

Configurability reduces risk and can improve time-to-market, but may cost area/power/performance.

#### Chip Basics Tradeoff Table

| Metric | Meaning | If Improved | Possible Cost |
|---|---|---|---|
| Time / performance | How fast tasks complete | faster product | more power, area, complexity |
| Area | silicon used | lower cost if reduced | may reduce performance/features |
| Power | energy/time | longer battery, less heat | may reduce speed |
| Reliability | correct operation over lifetime | safer product | redundancy/monitoring cost |
| Configurability | ability to adapt | flexibility/reuse | area/power/performance overhead |

#### PPA - Power, Performance, Area

Synopsys defines PPA in silicon chip design as **Power, Performance and Area**, three key metrics used to evaluate design quality and efficiency.

Important exam line:

```text
SoC design is a PPA tradeoff: improving performance often increases power or area,
while reducing area or power may reduce performance.
```

<a id="topic-1-design-flow-link"></a>

### How This Connects To SoC Design Flow

This topic is introductory, but it directly prepares the SoC design flow.

Basic flow:

```text
Application need / stakeholder need
        |
Requirements and constraints
        |
System architecture
        |
Hardware/software partitioning
        |
Component selection: processors, memories, interconnects, IP blocks
        |
Architecture modeling and tradeoff analysis
        |
RTL hardware design + software development
        |
Integration
        |
Verification and validation
        |
Physical design and fabrication
        |
Testing and product deployment
```

Where each part fits:

| Intro topic | Role in design flow |
|---|---|
| Systems approach | Keeps design aligned with complete product need |
| System architecture | Defines blocks, interfaces and organization |
| Components | Provides building blocks to implement architecture |
| Hardware/software | Decides what becomes circuits and what becomes code |
| Chip basics | Checks whether design is practical in time, area, power, reliability and cost |

Exam line:

```text
The systems approach turns SoC design from block-by-block circuit design into requirement-driven architecture design.
```

<a id="topic-1-final-answer"></a>

### Final Exam-Ready Answer

The systems approach is a method of designing a System on Chip by considering the complete system, its requirements, components, interfaces, constraints and lifecycle. A system is a combination of interacting elements that work together to provide a required capability. In SoC design, these elements include processors, memories, interconnects, accelerators, peripherals, analog blocks, debug/test structures and embedded software. The systems approach is needed because optimizing one block alone does not guarantee that the complete SoC will meet performance, power, cost or reliability requirements.

System architecture is the high-level organization of the system. It defines the system-level building blocks, their responsibilities, their relationships and their interconnections. In an SoC, system architecture includes processor selection, memory hierarchy, bus or Network-on-Chip structure, hardware accelerators, peripheral set, address map, clock and power domains, interrupt structure, software layers and external interfaces. Architecture acts as the bridge between requirements and implementation.

The main components of an SoC are processors, memories, interconnects, peripherals, accelerators, analog/mixed-signal blocks, clock/reset/power-management blocks, debug/test logic and software. The processor runs software and controls the system. Memory stores code and data. Interconnect carries communication between blocks. Peripherals provide I/O and control. Accelerators implement performance-critical functions efficiently. Software includes firmware, drivers, operating system, real-time tasks and applications.

A major SoC design decision is hardware/software partitioning. Hardware is physical circuitry and gives high performance, parallelism, energy efficiency and deterministic timing for repeated tasks. However, it is less flexible and expensive to change after fabrication. Software runs on processors and gives flexibility, programmability, easier updates and faster development, but it may be slower and less energy-efficient because instructions must be fetched, decoded and executed. Therefore, performance-critical parts are often implemented in hardware, while control, configuration and changing behavior are implemented in software. ASIPs and FPGAs lie between pure software and fixed ASIC hardware.

Chip basics determine whether the architecture is practical in silicon. Important chip tradeoffs are time, area, power, reliability and configurability. Time includes clock cycle, cycle time, latency and throughput. Area affects die size, routing, yield and cost. Power includes dynamic switching power and leakage power and affects battery life, heat and reliability. Reliability concerns correct operation despite defects, noise, aging and environmental effects. Configurability allows reuse and adaptation but can add area or performance overhead. These tradeoffs are often summarized as PPA: Power, Performance and Area.

Thus, the introduction to systems approach teaches that SoC design begins from system requirements and architecture, not from isolated gates. A good SoC design balances hardware and software, selects suitable components, defines clear interfaces and optimizes chip-level tradeoffs so that the final product meets its required function, performance, power, cost and reliability goals.

<a id="topic-1-short-answer"></a>

### Short 10-Mark Answer

The systems approach means designing the complete SoC by considering requirements, components, interfaces, constraints and tradeoffs. It avoids optimizing isolated blocks without checking the full system behavior.

System architecture is the high-level organization of the SoC. It defines processors, memories, interconnects, accelerators, peripherals, software layers and interfaces. It connects requirements to implementation.

The main SoC components are processor, memory, interconnect, peripherals, accelerators, analog/mixed-signal blocks, clock/reset/power blocks, debug/test blocks and embedded software.

Hardware is physical circuitry. It is fast, parallel and efficient for repeated tasks but less flexible. Software is instruction code running on processors. It is flexible and updateable but may be slower and less energy-efficient. SoC design partitions functions between hardware and software.

Chip basics include time/performance, area, power, reliability and configurability. These determine whether an architecture is practical. The central chip tradeoff is PPA: Power, Performance and Area.

<a id="topic-1-technical-words"></a>

### Technical Words To Use In Exam

- **SoC - System on Chip** (write this because the course topic is SoC design.)
- **Systems approach** (write this because the question directly asks it.)
- **System boundary** (write this because it shows what is inside and outside the system.)
- **Requirement** (write this because design starts from required behavior.)
- **Specification** (write this because requirements must become measurable targets.)
- **Constraint** (write this because power, area, cost and timing limit design choices.)
- **System architecture** (write this because it is the central topic.)
- **Functional architecture** (write this because architecture begins from system functions.)
- **Physical architecture** (write this because functions must map to real hardware/software blocks.)
- **Component** (write this because the question asks components of system.)
- **Interface** (write this because components interact through interfaces.)
- **Processor** (write this because it gives programmability.)
- **Memory** (write this because it stores instructions and data.)
- **Interconnect** (write this because it connects SoC blocks.)
- **Peripheral** (write this because I/O and control blocks are system components.)
- **Accelerator** (write this because performance-critical functions often move to hardware.)
- **Hardware/software partitioning** (write this because hardware vs software is a main design decision.)
- **GPP - General-Purpose Processor** (write this because software usually runs on a GPP.)
- **ASIC - Application-Specific Integrated Circuit** (write this because fixed custom hardware is one extreme.)
- **ASIP - Application-Specific Instruction Processor** (write this because it lies between GPP and ASIC.)
- **FPGA - Field-Programmable Gate Array** (write this because it provides configurable hardware.)
- **Firmware** (write this because SoC software often controls hardware directly.)
- **PPA - Power, Performance, Area** (write this because chip basics are design tradeoffs.)
- **Cycle time** (write this because time/performance depends on clock cycle.)
- **Critical path** (write this because it limits clock frequency.)
- **Die area** (write this because silicon area affects chip cost.)
- **Wafer** (write this because chips are manufactured together on wafers.)
- **Yield** (write this because good die per wafer determines cost.)
- **Dynamic power** (write this because switching activity consumes power.)
- **Leakage power** (write this because static power matters in modern chips.)
- **Reliability** (write this because chips must operate correctly over lifetime.)
- **Configurability** (write this because reuse and adaptation affect SoC design.)
- **Verification** (write this because the design must match the specification.)
- **Validation** (write this because the product must meet the real need.)

<a id="topic-1-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image part 1**: [Screenshot 2026-05-12 231802.png](<images/Screenshot 2026-05-12 231802.png>) contains the syllabus headline **Introduction: Introduction to Systems Approach - System Architecture, Components of system**.
2. **Topic image part 2**: [Screenshot 2026-05-12 231845.png](<images/Screenshot 2026-05-12 231845.png>) completes the headline with **Hardware and software, Chip basics**.
3. **Syllabus/CLO image**: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) maps the introduction section to the first course-learning stage and shows CLO 1 as familiarization with SoC design flow.

#### Figure 1: Systems Approach For SoC

```text
Application need
      |
Requirements + constraints
      |
System architecture
      |
Hardware/software partitioning
      |
Components + interfaces
      |
Implementation + integration
      |
Verification + validation
```

Why this figure is useful: it shows that SoC design starts from system need, not from isolated gates.

#### Figure 2: SoC System Architecture

```text
                   System on Chip
+------------------------------------------------+
| CPU / processor                                |
| Memory: cache, SRAM, ROM, DRAM controller      |
| Interconnect: bus / crossbar / NoC             |
| Accelerators: video, crypto, AI, DSP           |
| Peripherals: UART, SPI, GPIO, timer            |
| Analog/mixed-signal: ADC, DAC, PLL, RF         |
| Power/reset/clock management                   |
| Debug/test logic                               |
| Embedded software: firmware, drivers, OS       |
+------------------------------------------------+
```

Why this figure is useful: it gives a complete component view of an SoC.

#### Figure 3: Hardware/Software Spectrum

```text
Flexible                                             Fast / efficient

Software on GPP -> ASIP -> FPGA/reconfigurable -> ASIC hardware
```

Why this figure is useful: it explains programmability versus performance.

#### Figure 4: Chip Basics Tradeoff

```text
                  Chip design quality
                         |
       +-----------------+-----------------+
       |                 |                 |
     Time              Area              Power
       |                 |                 |
  latency/throughput  die/yield/cost  dynamic/leakage/heat
       |
Reliability and configurability must also be satisfied.
```

Why this figure is useful: it connects chip basics to practical SoC design.

#### Figure 5: Die, Wafer And Yield

```text
Wafer = large silicon disk

+----------------------------------+
| [die] [die] [die] [die] [die]    |
| [die] [bad] [die] [die] [die]    |
| [die] [die] [die] [bad] [die]    |
+----------------------------------+

Yield = good die / total die
```

Why this figure is useful: it explains why area affects cost.

---

## CLO 1 Coverage Status

- [x] Topic 1: Introduction to Systems Approach, System Architecture, Components of System, Hardware and Software, Chip Basics.
- [x] Full forms and definitions added.
- [x] Local PPT/book references separated into `sources/`.
- [x] Web references separated into `sources/`.
- [x] Exam diagrams added.
