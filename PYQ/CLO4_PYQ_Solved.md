# CLO 4 PYQ Solved - Design Methodologies, TLM And Hardware/Software Co-Design

## Clickable Index

- [Q1. Integration Platforms In SoC Design](#q1-integration-platforms-in-soc-design)
- [Q2. Transaction-Level Modeling](#q2-transaction-level-modeling)
- [Q3. SoC Design Methodologies](#q3-soc-design-methodologies)
- [Q4. Software Design In SoC](#q4-software-design-in-soc)
- [Q5. Hardware-Software Co-Design](#q5-hardware-software-co-design)

## CLO Mapping

This file maps to **CLO 4: Analyze the Design Methodologies of SoC; TLM and its need in SoC Design**.

Use with:

- [CLO4.md](<../CLO4.md>)
- [PYQ Master Index](<PYQ_Master_Index.md>)

## Local PPT / Book References To Use

Use these while revising or writing this CLO4 PYQ answer:

- [14-SOC Design Methodologies.pdf, p.2](<../System on chip/14-SOC Design Methodologies.pdf#page=2>) supports the idea that SoC design integrates software and hardware IP using multiple design methodologies.
- [14-SOC Design Methodologies.pdf, p.5](<../System on chip/14-SOC Design Methodologies.pdf#page=5>) lists TDD, BBD and PBD as the primary design methods.
- [14-SOC Design Methodologies.pdf, p.7](<../System on chip/14-SOC Design Methodologies.pdf#page=7>) supports Timing Driven Design.
- [14-SOC Design Methodologies.pdf, p.11](<../System on chip/14-SOC Design Methodologies.pdf#page=11>) supports Block Based Design and HW/SW tradeoffs.
- [14-SOC Design Methodologies.pdf, p.16](<../System on chip/14-SOC Design Methodologies.pdf#page=16>) supports Platform Based Design.
- [14-SOC Design Methodologies.pdf, p.18](<../System on chip/14-SOC Design Methodologies.pdf#page=18>) supports bus planning, hardware/software co-design and verification in platform-based design.
- [14-SOC Design Methodologies.pdf, p.20](<../System on chip/14-SOC Design Methodologies.pdf#page=20>) gives a comparison of TDD, BBD and PBD.
- [Functional Architecture Co Design 2.pdf, p.5](<../System on chip/Functional Architecture Co Design 2.pdf#page=5>) defines hardware/software co-design.
- [Functional Architecture Co Design 2.pdf, p.12](<../System on chip/Functional Architecture Co Design 2.pdf#page=12>) supports transaction-level communication and refinement from architecture to RTL.
- [Software_Design-in-SOC  and architectural .pdf, p.4](<../System on chip/Software_Design-in-SOC  and architectural .pdf#page=4>) supports software layers, drivers, RTOS services, interrupts and APIs.
- Detailed source maps: [CLO4_Topic1_sources.md](<../sources/CLO4_Topic1_sources.md>), [CLO4_Topic2_sources.md](<../sources/CLO4_Topic2_sources.md>), [CLO4_Topic3_sources.md](<../sources/CLO4_Topic3_sources.md>) and [CLO4_Topic4_sources.md](<../sources/CLO4_Topic4_sources.md>).

<a id="q1-integration-platforms-in-soc-design"></a>

## Q1. Discuss Different Integration Platforms In SoC Design

**PYQ source:** EST 2024 Q1, EST 2025 Q1.

### What The Question Is Asking

This question asks how complex SoCs are integrated using reusable platforms, tools and abstraction layers. It is not only about physically connecting wires. It includes IP integration, software integration, power intent, verification setup and system modeling.

### Definition

An **SoC integration platform** is a reusable environment or infrastructure used to assemble processors, memories, interconnects, IP cores, accelerators, software and verification components into a complete SoC.

### Why Integration Platforms Are Needed

Modern SoCs contain many third-party and in-house IP blocks. If each SoC is integrated manually from zero, the design becomes slow, error-prone and difficult to verify. Integration platforms reduce this problem by providing:

- standard interfaces,
- reusable bus/interconnect infrastructure,
- IP configuration rules,
- register and memory-map generation,
- power-intent handling,
- verification environment generation,
- software driver and firmware support,
- early architecture exploration.

### Types Of Integration Platforms

#### 1. IP-Based Integration Platform

This platform is based on reusable **IP - Intellectual Property** blocks such as processor cores, DDR controllers, DMA controllers, UART, SPI, I2C, PCIe, USB, accelerators and memories.

The platform defines:

- how IP blocks are described,
- how interfaces are connected,
- how registers are mapped,
- how clocks/resets are handled,
- how interrupts and DMA channels are connected.

Example: an SoC generator that connects an Arm/RISC-V processor, AXI interconnect, SRAM, timers, UART and GPIO using pre-verified IP.

#### 2. Bus/Interconnect Integration Platform

The interconnect platform connects masters and slaves. Masters include CPU, DMA, GPU and accelerators. Slaves include memories, peripherals and control registers.

Common interface families:

- **AMBA - Advanced Microcontroller Bus Architecture**
- **AXI - Advanced eXtensible Interface**
- **AHB - Advanced High-performance Bus**
- **APB - Advanced Peripheral Bus**
- **NoC - Network-on-Chip**

Why it matters: the interconnect decides address decoding, arbitration, QoS, bandwidth, latency and ordering.

#### 3. Platform-Based Design

**PBD - Platform Based Design** starts from a reusable platform rather than a blank design. The platform may include processor subsystem, interconnect, memory controller, standard peripherals, debug, boot flow and software stack.

This is useful when creating multiple derivative products. Example: one base multimedia SoC platform can be reused for low-end, mid-range and high-end products by changing accelerators, memory size and peripheral mix.

#### 4. Virtual Platform / ESL Platform

A **virtual platform** is an executable software model of the SoC. It is usually built at **ESL - Electronic System Level** using **TLM - Transaction-Level Modeling**.

It allows:

- early software development before RTL is complete,
- architecture exploration,
- boot-code testing,
- driver development,
- performance estimation,
- hardware/software partitioning.

#### 5. FPGA Prototyping And Emulation Platform

An FPGA prototype maps the SoC RTL onto FPGA hardware. Emulation maps the design onto a special hardware emulator. These platforms run faster than RTL simulation and allow real software workloads.

Use:

- validate software,
- run long tests,
- debug system-level behavior,
- check hardware/software integration.

Limitation: setup cost and debug complexity are high.

#### 6. Power-Intent Integration Platform

Low-power SoCs use multiple power domains, voltage islands, isolation cells, retention registers and power switches. Power intent is often captured using **UPF - Unified Power Format**.

The PYQ answer hint mentions SoC Compiler and UPF automation. Write this if expected:

```text
During SoC integration, EDA integration tools can automate generation, update,
promotion and demotion of UPF files so that power intent remains consistent
from block level to top-level SoC integration.
```

This matters because block-level power intent must be correctly merged into full-chip power intent.

#### 7. Verification Integration Platform

This platform integrates UVM agents, assertions, scoreboards, coverage collectors, test sequences and reference models. It ensures that integrated IP blocks are not only connected but also verified together.

### Figure To Draw

```text
              SoC Integration Platform
        +--------------------------------+
        | Processor subsystem            |
        | Interconnect / NoC / buses      |
        | Memory controllers              |
        | Peripheral IP                   |
        | Accelerators                    |
        | Power intent / UPF              |
        | Register map / interrupts       |
        | Software drivers / firmware     |
        | Verification environment        |
        +--------------------------------+
```

### Final Exam Answer

Different integration platforms in SoC design provide reusable infrastructure to assemble IP blocks, processors, memories, interconnects, power domains, software and verification environments. IP-based platforms reuse verified design blocks. Bus or NoC integration platforms provide standard communication, address decoding, arbitration and QoS. Platform-based design reuses a complete subsystem or architecture to create derivative products quickly. Virtual platforms and ESL/TLM models allow early software development and architecture exploration. FPGA prototyping and emulation platforms run RTL faster for system validation. Power-intent platforms manage UPF and low-power integration across hierarchy. Verification platforms integrate UVM components, coverage and assertions. Together, these platforms reduce manual integration errors, improve reuse, shorten time-to-market and make large SoC design manageable.

### Technical Words

- **IP - Intellectual Property** (reusable hardware/software design block.)
- **PBD - Platform Based Design** (reuse of a base architecture.)
- **ESL - Electronic System Level** (high-level executable system modeling.)
- **TLM - Transaction-Level Modeling** (modeling using transactions instead of signal toggles.)
- **UPF - Unified Power Format** (captures low-power intent.)
- **NoC - Network-on-Chip** (scalable packet-based interconnect.)

<a id="q2-transaction-level-modeling"></a>

## Q2. With A Block Diagram, Explain Transaction-Level Modeling

**PYQ source:** EST 2024 Q3, EST 2025 Q3.

### Definition

**TLM - Transaction-Level Modeling** is a high-level modeling style where communication between components is represented as transactions such as read, write, burst, packet or command, instead of individual signal transitions.

### Why TLM Is Needed

RTL models every signal and clock cycle. That is accurate but slow. Early SoC design needs faster models for architecture exploration and software development. TLM provides this by hiding low-level pin toggling and focusing on what data is transferred, where it goes and what timing cost it has.

### Block Diagram

```text
       Initiator                                  Target
   +--------------+       transaction        +--------------+
   | CPU model    | -----------------------> | Memory model |
   | DMA model    |    read/write/burst      | Peripheral   |
   +--------------+                          +--------------+
          |                                          |
          +------------ Interconnect model ----------+
```

### How It Works

An initiator starts a transaction. A target responds to it.

Example transaction:

```text
command = READ
address = 0x80000000
length  = 64 bytes
data    = returned by memory
delay   = estimated memory/interconnect latency
```

At RTL level, this same operation would require address lines, valid/ready signals, burst counters, byte enables, data buses and clock cycles. TLM compresses all that into a higher-level function call or transaction object.

### Levels Of Timing Accuracy

**Untimed functional model:** only correctness of function is modeled.

**Loosely timed TLM:** approximate time is added; useful for fast software development.

**Approximately timed TLM:** more timing phases are modeled; useful for architecture performance analysis.

**Cycle-accurate model:** closer to RTL timing but slower.

### TLM Vs RTL

| Point | TLM | RTL |
|---|---|---|
| Abstraction | Transactions | Signals and registers |
| Speed | Fast | Slow |
| Timing | Approximate or loosely timed | Cycle accurate |
| Use | Early architecture/software | Final hardware implementation |
| Example | `read(address, length)` | AXI valid, ready, address, data, response |

### Final Exam Answer

Transaction-level modeling represents SoC communication using high-level transactions instead of cycle-by-cycle signal activity. A CPU, DMA or accelerator acts as an initiator and sends read/write/burst transactions through an interconnect model to target models such as memory or peripherals. TLM is useful because it runs faster than RTL, supports early software development, enables architecture exploration and allows performance estimation before detailed RTL is ready. It can be untimed, loosely timed, approximately timed or cycle accurate depending on required accuracy. However, TLM does not replace RTL; it is refined later into detailed hardware implementation and verification models.

### Technical Words

- **Initiator** (component that starts a transaction.)
- **Target** (component that responds.)
- **Payload** (data structure carrying command, address, data and control fields.)
- **Loosely timed** (fast timing approximation.)
- **Approximately timed** (more detailed timing phases.)
- **Virtual platform** (executable SoC model used before RTL.)

<a id="q3-soc-design-methodologies"></a>

## Q3. Explain SoC Design Methodologies

**PYQ source:** EST 2024 Q4, EST 2025 Q4.

### Main Methodologies

The main SoC design methodologies are:

1. **TDD - Timing Driven Design**
2. **BBD - Block Based Design**
3. **PBD - Platform Based Design**

### TDD - Timing Driven Design

TDD focuses on meeting timing constraints from the beginning of design. Timing is not checked only at the end; it influences synthesis, floorplanning, placement, routing and optimization.

It is used because deep-submicron delay is strongly affected by interconnect, placement and clock distribution. A design may be logically correct but fail if critical paths exceed the clock period.

Key ideas:

- constraints are defined early,
- timing analysis is repeated through the flow,
- critical paths are optimized,
- floorplanning and placement are guided by timing,
- clock tree and routing are considered.

### BBD - Block Based Design

BBD divides a large SoC into blocks. Each block is designed with its own timing, area, power and interface budgets.

It is used because a full SoC is too complex to design flat. Teams work in parallel on blocks and later integrate them.

Key ideas:

- hierarchical partitioning,
- block-level constraints,
- interface contracts,
- independent verification,
- top-level integration.

### PBD - Platform Based Design

PBD starts with a reusable platform containing processor subsystem, interconnect, memory, standard peripherals, debug, software stack and sometimes verification infrastructure.

It is used to reduce development time and improve reuse. New products are created by configuring or extending an existing platform.

Key ideas:

- reuse of IP and architecture,
- standard interfaces,
- reusable software and verification,
- derivative SoC products,
- faster time-to-market.

### Comparison

| Methodology | Main focus | Best when | Risk |
|---|---|---|---|
| TDD | Timing closure | High-speed design | Can become late-stage optimization if not planned well |
| BBD | Hierarchical blocks | Large SoC teams | Interface/budget mismatch |
| PBD | Reuse and integration | Product families | Platform may restrict flexibility |

### Final Exam Answer

SoC design methodologies are structured approaches used to manage complexity, timing, reuse and integration. Timing Driven Design focuses on meeting timing constraints throughout synthesis and physical design. It is important because interconnect and placement delay dominate in deep-submicron SoCs. Block Based Design partitions the SoC into manageable blocks with timing, area, power and interface budgets, allowing parallel design and hierarchical integration. Platform Based Design reuses a pre-defined architecture, IP set, interconnect, software stack and verification environment to create derivative SoCs faster. Modern SoC design usually combines all three: platform reuse at system level, block-based implementation at subsystem level and timing-driven closure during physical design.

<a id="q4-software-design-in-soc"></a>

## Q4. Explain Software Design In SoC And Issues Associated With It

**PYQ source:** EST 2024 Q5, EST 2025 Q5.

### Definition

Software design in SoC is the process of developing firmware, drivers, operating-system support, boot code, middleware and application software that run on the processors inside the SoC and control the hardware blocks.

### Main Software Components

**Boot code:** initializes processor, clocks, memory controller and basic hardware.

**Firmware:** low-level embedded software that controls SoC hardware features such as power modes, security, boot and configuration.

**Device drivers:** software modules that control hardware blocks such as UART, SPI, DMA, accelerator, Ethernet or display controller.

**HAL - Hardware Abstraction Layer:** provides a uniform API above hardware-specific registers.

**RTOS - Real-Time Operating System:** manages tasks, interrupts, scheduling, timers, synchronization and real-time constraints.

**Compiler and toolchain:** converts C/C++/assembly into target processor instructions and links the final executable.

**Debugger and simulator:** help inspect software behavior, register values, memory state and hardware/software interaction.

### Software Design Flow

```text
System requirements
     |
Hardware/software partitioning
     |
Processor and memory-map definition
     |
Boot code and firmware
     |
Device drivers and HAL
     |
RTOS / bare-metal software
     |
Application software
     |
Co-simulation, emulation, FPGA prototype and silicon validation
```

### Issues In SoC Software Design

**1. Hardware dependency:** software must match memory maps, registers, interrupts, reset values and hardware behavior.

**2. Driver complexity:** drivers must configure registers in correct order, handle interrupts, errors, DMA and power states.

**3. Timing and real-time constraints:** software may miss deadlines if interrupts, task scheduling or memory latency are not controlled.

**4. Hardware/software synchronization:** shared memory, cache coherency, DMA buffers and interrupt status registers must be synchronized.

**5. Boot complexity:** modern SoCs have secure boot, multiple cores, power domains, clocks and memory initialization.

**6. Debug difficulty:** bugs may appear only when hardware and software run together.

**7. Power management:** software must safely enter and exit sleep, retention or power-off states.

**8. Portability:** software should be reusable across derivative SoCs but hardware differences make this difficult.

**9. Compiler and optimization effects:** compiler output affects performance, memory footprint and execution timing.

**10. Security and safety:** software must enforce privilege, secure access, fault handling and isolation.

### Final Exam Answer

Software design in SoC includes boot code, firmware, device drivers, HAL, RTOS support, middleware and application software. It is tightly connected to hardware because software programs registers, handles interrupts, configures DMA, controls accelerators and manages power modes. A complete software development environment needs compiler, linker, debugger, simulator, driver framework, operating system support and hardware/software co-verification. Major issues include hardware dependency, driver complexity, timing constraints, memory-map errors, interrupt handling, cache coherency, DMA synchronization, boot initialization, low-power control, portability and debugging difficulty. Therefore, SoC software must be developed together with hardware using virtual platforms, co-simulation, emulation and FPGA prototyping.

<a id="q5-hardware-software-co-design"></a>

## Q5. Explain Hardware-Software Co-Design

**PYQ source:** MST 2026 Q1(d).

### Definition

**Hardware/software co-design** is the joint design of hardware and software so that system functions are partitioned between processors, accelerators, memories and software tasks in an optimized way.

### Why It Is Needed

In an SoC, some tasks are better in software and some are better in hardware.

Software is flexible and programmable but may be slower for repetitive high-throughput operations.

Hardware is faster and more parallel but less flexible and more expensive to change after fabrication.

### Partitioning Criteria

| Criterion | Prefer software | Prefer hardware |
|---|---|---|
| Flexibility | Algorithm changes often | Algorithm fixed |
| Performance | Low/medium speed | High throughput or low latency |
| Power | Occasional task | Repeated heavy computation |
| Cost | Avoid extra area | Area is acceptable for speed |
| Time-to-market | Quick software update | Stable hardware acceleration |

### Co-Design Flow

```text
System specification
     |
Functional modeling
     |
Architecture exploration
     |
Hardware/software partitioning
     |
Interface definition
     |
Hardware RTL + software development
     |
Co-simulation / emulation
     |
Integration and validation
```

### Example

In a video-processing SoC:

- control, UI and configuration run on CPU software,
- frame filtering may run on a hardware accelerator,
- DMA moves image buffers,
- interrupts notify software when processing completes,
- driver configures accelerator registers.

### Final Exam Answer

Hardware/software co-design is a system-level design methodology in which hardware and software are developed together. It decides which functions should run as software on processors and which should be implemented as dedicated hardware accelerators. The goal is to meet performance, power, area, cost and flexibility requirements. Co-design uses ESL/TLM models, virtual platforms, profiling, partitioning, interface definition, driver development and co-simulation. It is essential in SoC design because final behavior depends on both RTL hardware and embedded software.
