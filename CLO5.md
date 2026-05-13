# CLO 5 - SoC Verification and Testing

## Clickable Index

- [CLO 5 Master Definitions](#clo5-master-definitions)
- [CLO 5 Full-Form Review Addendum](#clo5-full-form-review)
- [CLO 5 PYQ-Based Question Bank](<PYQ/CLO5_PYQ_Question_Bank.md>)
- [Topic 1: Verification Techniques - OVM, UVM and VVM](#topic-1)
  - [Question](#topic-1-question)
  - [Main Explanation](#topic-1-explanation)
  - [Final Exam-Ready Answer](#topic-1-final-answer)
  - [Technical Words](#topic-1-technical-words)
  - [Images / Diagrams](#topic-1-diagrams)
- [Topic 2: SoC Verification Flow](#topic-2)
  - [Question](#topic-2-question)
  - [Main Explanation](#topic-2-explanation)
  - [Power Modes Explanation](#topic-2-power-modes)
  - [Final Exam-Ready Answer](#topic-2-final-answer)
  - [Technical Words](#topic-2-technical-words)
  - [Images / Diagrams](#topic-2-diagrams)
- [Topic 3: SoC Test Scheduling and Test Integration](#topic-3)
  - [Question](#topic-3-question)
  - [Main Explanation](#topic-3-explanation)
  - [BIST, ATPG And DFT Component Comparison](#topic-3-dft-comparison)
  - [Final Exam-Ready Answer](#topic-3-final-answer)
  - [Technical Words](#topic-3-technical-words)
  - [Images / Diagrams](#topic-3-diagrams)

<a id="clo5-master-definitions"></a>

## CLO 5 Master Definitions

Use this section before revising the detailed topics. These are the terms that repeatedly appear in CLO 5. For each term, learn three things: **full form**, **what/where it is**, and **why it is written in the answer**.

| Term | Full Form / Meaning | What And Where It Is | Why It Matters For Marks |
|---|---|---|---|
| CLO | Course Learning Outcome | The syllabus outcome that groups exam topics and expected learning level. | Helps map each answer to the correct exam outcome. |
| SoC | System on Chip | A complete electronic system integrated on one chip, usually with processor, memory, interconnect, peripherals and IP blocks. | CLO 5 is about verifying and testing complete integrated chips, not only one logic gate or one small block. |
| IP | Intellectual Property | A reusable design block, such as CPU core, UART, DMA, USB, memory controller or accelerator. It is inside the SoC after integration. | SoC verification is difficult because many IP blocks must work together correctly. |
| VIP | Verification Intellectual Property / Verification IP | Reusable verification component, usually in a testbench, used to verify protocols such as AXI, APB, UART, PCIe or DDR. It is not usually silicon hardware. | Shows reuse in UVM/OVM verification methodology. |
| RTL | Register Transfer Level | Hardware design description written in Verilog, SystemVerilog or VHDL before synthesis. | Verification mainly checks RTL behavior before fabrication. |
| DUT | Design Under Test | The hardware block, subsystem or full SoC being verified in simulation/emulation. | Needed when explaining testbench diagrams. |
| DFT | Design for Testability | Extra test hardware added into the design, such as scan chains, BIST, wrappers and test controllers. | Explains how fabricated chips can be tested after manufacturing. |
| ATE | Automatic Test Equipment | Large external manufacturing tester outside the chip. It applies patterns at chip pins and checks responses. | Shows the difference between external tester and internal SoC test structures. |
| JTAG | Joint Test Action Group | Low-pin-count test/debug access standard using pins such as TCK, TMS, TDI and TDO, plus on-chip TAP hardware. | Used to access chip test/debug logic with few pins. |
| TAP | Test Access Port | On-chip JTAG controller state machine and access logic. | Explains how JTAG commands are shifted, captured and updated. |
| TAM | Test Access Mechanism | On-chip test data transport path from chip-level access to embedded cores and responses back. | Core term for SoC test integration and scheduling. |
| BIST | Built-In Self-Test | On-chip self-test hardware that generates test activity and checks responses internally. | Reduces ATE data volume and helps test embedded memories/logic. |
| MBIST | Memory Built-In Self-Test | BIST specialized for SRAM, ROM, register files and memory macros. | SoCs contain many embedded memories that need efficient testing. |
| LBIST | Logic Built-In Self-Test | BIST specialized for random digital logic, often using pseudo-random patterns and response signatures. | Explains logic self-test beyond memory testing. |
| ATPG | Automatic Test Pattern Generation | EDA software process that creates structural test vectors for faults such as stuck-at and transition faults. | Shows where scan test patterns come from. |
| Scan chain | Scan flip-flop chain | On-chip DFT hardware that connects flip-flops as shift registers in test mode. | Improves controllability and observability of internal state. |
| Core wrapper | Test wrapper around an embedded core | On-chip boundary test logic around an IP core. | Isolates a core and connects it to TAM during SoC-level test. |
| Test controller | Chip test-control hardware | On-chip DFT controller that selects test modes, starts BIST, enables scan/wrappers and reads status. | Coordinates internal test operations that ATE cannot directly control. |
| OVM | Open Verification Methodology | Older SystemVerilog verification methodology/class library. | Historical base for reusable transaction-level verification. |
| UVM | Universal Verification Methodology | Standard SystemVerilog verification methodology using agents, sequences, drivers, monitors, scoreboards and coverage. | Most important reusable SoC verification methodology. |
| VVM | VHDL Verification Methodology | VHDL-oriented structured verification approach, commonly represented by UVVM and OSVVM. | Shows that VHDL designs also have structured verification methods. |
| UVVM | Universal VHDL Verification Methodology | VHDL verification framework/library that uses structured test sequencers, BFMs and VVCs. | Gives a practical example of VVM-style verification. |
| OSVVM | Open Source VHDL Verification Methodology | VHDL verification methodology/packages for randomization, coverage, scoreboards, logs and models. | Shows advanced verification features in VHDL. |
| VVC | VHDL Verification Component | Reusable VHDL verification component, usually representing one interface or protocol. | VHDL equivalent idea to reusable protocol verification components. |
| BFM | Bus Functional Model | Testbench model that drives/responds to bus transactions at protocol level. | Converts high-level transactions into signal-level bus activity. |
| TLM | Transaction-Level Modeling | Modeling style where communication is described as transactions such as read, write, burst or packet. | Makes SoC verification easier than manually describing every pin toggle. |
| ABV | Assertion-Based Verification | Verification technique using assertions/properties to check protocol and timing rules automatically. | Helps catch violations immediately during simulation/formal checking. |
| Agent | Verification component | In UVM, usually contains sequencer, driver and monitor for one interface. | Explains modular reusable verification environments. |
| Monitor | Passive testbench checker component | Observes DUT signals and converts them into transactions. | Used for scoreboarding and coverage without driving signals. |
| Scoreboard | Testbench checking component | Compares actual DUT behavior with expected/reference behavior. | Shows automatic checking instead of manual waveform inspection. |
| Functional coverage | Specification-driven coverage | Measures whether planned features/scenarios were exercised. | Proves that important verification scenarios were actually tested. |
| Code coverage | RTL implementation coverage | Measures executed statements, branches, conditions, toggles and FSM states. | Shows whether written RTL was exercised by tests. |
| CDC | Clock Domain Crossing | Signal transfer between different clock domains. It is a hardware design issue checked by tools/assertions. | Important because metastability and sampling errors are common SoC bugs. |
| RDC | Reset Domain Crossing | Signal or state interaction across different reset domains. | Important because reset release ordering can create unknown or unsafe states. |
| PMU | Power Management Unit | On-chip hardware block/controller that sequences clocks, resets, isolation, retention and power switches. | Required when explaining power modes and low-power verification. |
| DVFS | Dynamic Voltage and Frequency Scaling | Low-power technique that changes voltage/frequency based on performance need. | Useful term for power-mode verification. |
| DMA | Direct Memory Access | On-chip controller that moves data between memory/peripherals without continuous CPU work. | Creates concurrency and memory traffic verification cases. |
| CPU | Central Processing Unit | Processor core inside the SoC that runs firmware/software. | Important for hardware/software co-verification and processor-driven tests. |
| DSP | Digital Signal Processor | Specialized processor/accelerator for signal-processing workloads. | Useful example of an SoC core with separate test and power needs. |
| SRAM | Static Random Access Memory | On-chip memory commonly used for caches, buffers and register files. | Important because embedded memories often need MBIST. |
| UART | Universal Asynchronous Receiver/Transmitter | Serial communication peripheral often used as a simple protocol example. | Useful example for verification components, BFMs and test scheduling examples. |
| FIFO | First-In First-Out | Buffer where data leaves in the same order it entered. | Common in CDC, streaming interfaces and coverage examples. |
| FSM | Finite State Machine | Sequential control logic with defined states and transitions. | Important for code coverage and control-path verification. |
| EDA | Electronic Design Automation | Software tools used for simulation, synthesis, formal, ATPG, STA and DFT. | Separates tool activity from actual hardware inside the SoC. |
| AMBA | Advanced Microcontroller Bus Architecture | Arm family of SoC bus/interconnect protocols. | Common protocol family in SoC verification examples. |
| AXI | Advanced eXtensible Interface | AMBA high-performance bus protocol used for memory-mapped transfers. | Useful example for UVM agents, BFMs and bus verification. |
| APB | Advanced Peripheral Bus | AMBA simpler low-power peripheral bus protocol. | Common example for register/peripheral verification. |
| AHB | Advanced High-performance Bus | AMBA bus protocol often used in embedded SoCs. | Helps compare common SoC interconnect protocols. |
| ISR | Interrupt Service Routine | Software routine executed when an interrupt occurs. | Needed in hardware/software co-verification. |
| RTOS | Real-Time Operating System | Software operating system with deterministic scheduling behavior. | Used when verifying software interactions with SoC hardware. |
| PLL | Phase-Locked Loop | Clock-generation hardware, often analog/mixed-signal, inside or near clock system. | Important for clock/frequency constraints and full-chip verification. |
| STA | Static Timing Analysis | EDA timing check that verifies setup/hold timing without exhaustive simulation. | Key post-synthesis/gate-level sign-off concept. |
| GLS | Gate-Level Simulation | Simulation of synthesized gate netlist, sometimes with SDF timing delays. | Checks selected timing/reset/X-propagation behavior after synthesis. |
| SDF | Standard Delay Format | File format containing timing delays used in gate-level simulation. | Explains how gate delays are annotated in GLS. |
| UPF | Unified Power Format | Power-intent format describing power domains, isolation, retention and level shifting. | Useful when discussing low-power verification. |
| LFSR | Linear Feedback Shift Register | Hardware pattern generator often used in LBIST. | Shows how logic BIST creates pseudo-random test patterns. |
| MISR | Multiple Input Signature Register | Hardware response compactor used in LBIST. | Shows how many logic responses are compressed into a signature. |
| Fault model | Abstract manufacturing defect model | Represents physical defects as testable logical faults such as stuck-at, transition or bridging faults. | Explains what ATPG patterns are trying to detect. |
| Stuck-at fault | Signal fixed at 0 or 1 | Structural fault where a node behaves as if permanently stuck-at-0 or stuck-at-1. | Most basic manufacturing fault model. |
| Transition fault | Slow-to-rise or slow-to-fall fault | Delay fault where a node changes too slowly for at-speed operation. | Important for timing-related manufacturing defects. |
| Bridging fault | Short between nodes | Defect where two wires/nodes are unintentionally connected. | Shows why structural testing is broader than functional simulation. |
| Fault coverage | Percentage of modeled faults detected | Ratio of detected modeled faults to total target faults. | Key test-quality metric. |
| Pattern compression | Test data compression | Reduces external ATE pattern volume using on-chip decompression/compaction. | Reduces tester memory and test time. |
| Boundary scan cell | JTAG-accessible cell near chip pin | Test cell placed near chip I/O so pin/interconnect values can be shifted, captured and updated. | Explains what boundary scan physically adds near I/O pins. |
| Test mode | Special operating mode for manufacturing test | Mode where scan, BIST, wrappers, clocks or isolation controls are configured for testing. | Needed to explain scheduling conflicts and DFT control. |

Quick expansions for example terms that appear in explanations:

- **ASIC - Application-Specific Integrated Circuit**: custom chip implementation.
- **FPGA - Field-Programmable Gate Array**: reconfigurable hardware platform often used for prototyping.
- **VHDL - VHSIC Hardware Description Language**: hardware description language; **VHSIC** means Very High Speed Integrated Circuit.
- **SV - SystemVerilog**: hardware design and verification language used with UVM.
- **AMBA ACE - Advanced Microcontroller Bus Architecture Advanced Coherency Extensions**: coherency extension for Arm interconnects.
- **AMBA CHI - Advanced Microcontroller Bus Architecture Coherent Hub Interface**: coherent interconnect protocol used in larger Arm-based systems.
- **DDR - Double Data Rate** and **DRAM - Dynamic Random Access Memory**: external/main memory technology examples.
- **RAM - Random Access Memory** and **ROM - Read-Only Memory**: common memory categories.
- **ECC - Error Correction Code**: detects/corrects memory or data-transfer errors.
- **GPIO - General-Purpose Input/Output**, **SPI - Serial Peripheral Interface**, **I2C - Inter-Integrated Circuit**, **USB - Universal Serial Bus**: common peripheral/interface examples.
- **GPU - Graphics Processing Unit** and **AI - Artificial Intelligence accelerator**: common accelerator examples.
- **ISS - Instruction Set Simulator**: software model of a processor used in hardware/software co-verification.
- **ECO - Engineering Change Order**: late design fix after synthesis or implementation.
- **RTC - Real-Time Clock**: low-power clock/timekeeping block.
- **API - Application Programming Interface**: software interface used by drivers or firmware.
- **HW/SW - Hardware/Software**: used in hardware/software co-verification.
- **TCK, TMS, TDI, TDO, TRST**: JTAG test clock, test-mode select, test-data in, test-data out and optional test reset.
- **SI, SO, SE**: scan input, scan output and scan enable in scan-chain testing.
- **IR drop**: supply-voltage drop caused by current through power-network resistance during high switching activity.

Memory line for the whole CLO:

```text
Verification checks the design before fabrication.
Testing checks manufactured silicon after fabrication.
UVM/OVM/VVM organize verification.
DFT, scan, BIST, TAM - Test Access Mechanism, JTAG and ATE support manufacturing test.
Test scheduling reduces test time safely under constraints.
```

<a id="clo5-full-form-review"></a>

## CLO 5 Full-Form Review Addendum

For CLO 5, always separate **verification** and **testing**.

**Verification** checks the design before fabrication. It uses simulation, assertions, formal methods, UVM - Universal Verification Methodology environments, scoreboards, functional coverage and regression testing to prove that RTL - Register Transfer Level behavior matches the specification.

**Testing** checks manufactured silicon after fabrication. It uses DFT - Design for Testability structures such as scan chains, BIST - Built-In Self-Test, JTAG - Joint Test Action Group boundary scan, TAM - Test Access Mechanism and ATE - Automatic Test Equipment to detect physical defects.

**UVM - Universal Verification Methodology** is a testbench methodology, not chip hardware. Its agents, sequences, drivers, monitors, scoreboards and coverage collectors live in the verification environment.

**DFT - Design for Testability** is real hardware inserted into the chip. Scan chains, BIST controllers, wrappers and test controllers occupy area and must be considered during design, timing closure and test scheduling.

**ATPG - Automatic Test Pattern Generation** is a tool process. It creates structural test patterns for fault models such as stuck-at faults, transition faults and bridging faults. The generated patterns are later applied through scan, TAM and ATE paths.

<a id="topic-1"></a>

## Topic 1: Verification Techniques - OVM, UVM and VVM

<a id="topic-1-question"></a>

### Question

**Explain SoC Verification and Testing with reference to verification techniques such as OVM, UVM and VVM.**

### CLO Mapping

This topic belongs to **CLO 5: Discuss the SoC Design Verification strategies and Test Scheduling**.

Reason: This topic is part of **SoC Verification and Testing**, which includes verification techniques, SoC verification flow, test scheduling and test integration. These are all directly aligned with CLO 5.

### What The Question Is Asking

The examiner is not only asking for definitions of OVM, UVM and VVM. The answer should show that you understand why verification is difficult in SoC design, how a verification environment is built, and how these methodologies support reusable, scalable and coverage-driven verification.

For full marks, answer in this order:

1. Define **verification** and **testing** separately.
2. Explain why SoC verification is difficult.
3. Explain the SoC verification flow.
4. Explain **Open Verification Methodology (OVM)**, **Universal Verification Methodology (UVM)** and **VHDL Verification Methodology (VVM)**.
5. Compare them.
6. Mention test scheduling and test integration because they are in the same CLO.
7. Draw a verification environment block diagram.

<a id="topic-1-explanation"></a>

### Answer

#### Short Forms Used In This Topic

- **SoC - System on Chip**: a complete electronic system integrated on one chip, usually containing processor, memory, interconnect, IP blocks and peripherals.
- **OVM - Open Verification Methodology**: an older SystemVerilog verification methodology used to build reusable transaction-level testbenches.
- **UVM - Universal Verification Methodology**: the standardized SystemVerilog methodology used for reusable, coverage-driven and scalable verification.
- **VVM - VHDL Verification Methodology**: a VHDL-oriented verification-methodology idea, commonly represented by UVVM or OSVVM.
- **VIP - Verification Intellectual Property / Verification IP**: a reusable verification component used to verify a standard interface or protocol, such as AXI, APB, UART, PCIe or DDR.
- **IP - Intellectual Property**: a reusable design block or verification block, such as a processor core, bus controller, USB controller or memory controller.
- **RTL - Register Transfer Level**: the hardware design description level written in languages such as Verilog, SystemVerilog or VHDL.
- **DUT - Design Under Test**: the hardware block, subsystem or SoC being verified.
- **BFM - Bus Functional Model**: a verification model that drives or responds to bus transactions at protocol level.
- **CDC - Clock Domain Crossing**: transfer of signals between two different clock domains.
- **DFT - Design for Testability**: design techniques added so manufactured chips can be tested efficiently.

SoC verification and testing are two related but different activities. **Verification** checks whether the design implementation satisfies the specification before fabrication. It answers: *Have we designed the right logic correctly?* **Testing** checks manufactured silicon for physical defects after fabrication. It answers: *Has this chip been manufactured correctly?*

This distinction is important because an SoC can be functionally correct but still fail after fabrication due to manufacturing defects, and a physically defect-free chip can still be useless if the RTL logic is wrong. Verification is mainly a **design correctness** activity. Testing is mainly a **manufacturing quality** activity. A strong exam answer must keep both connected but not mix them.

### Why SoC Verification Is Difficult

A simple digital block can be verified with a small set of input-output tests. A SoC cannot be verified like that because the problem is not only one block's logic. The real difficulty is **integration**. A modern SoC contains processors, memories, DMA controllers, buses, accelerators, interrupts, reset controllers, clock domains, power domains, analog/mixed-signal blocks, third-party IP and embedded software. Each of these may be correct alone, but the complete chip may still fail when they interact.

#### Small Definitions Of These SoC Blocks

- **Processor / CPU core**: The programmable execution unit that runs instructions and controls general system behavior. In verification, it matters because processor traffic, cache misses, exceptions and privilege modes can expose integration bugs.
- **Memory**: Storage blocks such as SRAM, ROM, cache, scratchpad, register files, DRAM or Flash. In verification, memories matter because incorrect address mapping, access permission, initialization, latency or data ordering can break the SoC.
- **DMA controller - Direct Memory Access controller**: A block that transfers data between memory and peripherals without continuous CPU involvement. In verification, DMA is important because it creates concurrent memory traffic and can conflict with CPU/cache accesses.
- **Bus / Interconnect / NoC - Network on Chip**: The communication fabric that connects processors, memories and IP (Intellectual Property) blocks. It carries addresses, data, control signals and responses. In verification, it matters because protocol violations, arbitration errors, deadlocks or ordering mistakes can affect the whole chip.
- **Accelerator**: A specialized hardware block designed to perform a specific task faster or more efficiently than a CPU, such as image processing, encryption, AI inference or signal processing. In verification, accelerators matter because they often share memory, interrupts and configuration registers with the processor.
- **Interrupt**: A hardware signal or event that requests processor attention. It allows peripherals to tell the CPU that service is needed. In verification, interrupt priority, masking, clearing and timing must be checked carefully.
- **Reset controller**: The block that generates and sequences reset signals for different parts of the SoC. In verification, it matters because blocks must enter a known state, and wrong reset order can cause unpredictable startup behavior.
- **Clock domain**: A region of logic driven by the same clock signal. A SoC can have many clock domains. In verification, clock-domain crossings must be checked because data moving between different clocks can suffer from metastability or synchronization errors.
- **Power domain**: A region of the SoC that can be powered on, powered off or voltage-scaled independently. In verification, power domains matter because isolation, retention, wake-up sequence and power-state transitions can cause failures.
- **Analog/mixed-signal block**: A block that handles analog signals or both analog and digital signals, such as **PLL - Phase-Locked Loop**, **ADC - Analog-to-Digital Converter**, **DAC - Digital-to-Analog Converter**, **SerDes - Serializer/Deserializer** high-speed serial interface blocks, sensors or power-management circuits. In verification, it matters because digital logic must interact correctly with non-ideal analog behavior.
- **Third-party IP - third-party Intellectual Property**: A pre-designed block purchased or reused from another team/vendor, such as USB (Universal Serial Bus), PCIe (Peripheral Component Interconnect Express), Ethernet, DDR (Double Data Rate) controller or security IP. In verification, third-party IP matters because integration assumptions, interface timing and configuration may not exactly match the SoC environment.
- **Embedded software / firmware**: Low-level software running on the SoC processor to initialize hardware, configure registers, handle interrupts and control peripherals. In verification, it matters because many bugs appear only when hardware and software execute together.

Typical SoC verification problems are:

1. **Interface mismatch**: two IPs may follow slightly different assumptions about protocol timing, handshaking, burst length, byte enables or reset behavior.

   This is one of the most common SoC integration problems. Each IP block may be correct according to its own local specification, but the connection between two blocks may be wrong. For example, one block may assume that a valid signal remains high until ready is asserted, while the connected block may sample valid for only one clock cycle. Similarly, a bus master may generate burst transfers of a length that the slave does not support.

   Interface mismatch can happen in address buses, data buses, control signals, interrupt lines, reset signals, clock enables and protocol handshakes. In SoC verification, the engineer must check that both sides of the interface follow the same protocol rules. This is done using protocol checkers, assertions, bus functional models, monitors and coverage.

   Exam line: **Interface mismatch occurs when two individually correct IP blocks fail after connection because their protocol, timing or configuration assumptions are different.**

2. **Synchronization errors**: data crossing from one clock domain to another can become metastable or be sampled incorrectly.

   A SoC usually contains multiple clock domains. For example, the CPU may run at a high frequency, the peripheral bus may run slower, and an external interface may use another independent clock. When a signal moves from one clock domain to another, it may change near the sampling edge of the receiving clock. This can cause metastability, where the receiving flip-flop temporarily enters an undefined voltage state before settling to 0 or 1.

   Synchronization errors are dangerous because they may not appear in every simulation. They may occur only at specific clock phase relationships or under rare timing conditions. Examples include missed pulses, duplicated pulses, corrupted multi-bit data, wrong FIFO full/empty flags and incorrect interrupt detection.

   The solution is to use proper clock-domain crossing structures such as two-flop synchronizers for single-bit control signals, asynchronous FIFOs for data buses, handshake synchronizers for control transfers and gray-coded pointers for FIFO address crossing. Verification must include CDC checks, assertions and stress tests with unrelated clock frequencies.

   Exam line: **Synchronization error occurs when signals cross between different clock domains without proper synchronizers, causing metastability, data loss or incorrect sampling.**

3. **Software-hardware interaction bugs**: a register may work in RTL, but firmware may program it in the wrong order or assume wrong interrupt behavior.

   In an SoC, hardware does not operate alone. Firmware configures registers, enables clocks, sets interrupt masks, starts DMA transfers, handles status bits and controls power modes. A hardware block may pass block-level RTL verification, but still fail when real software uses it.

   Example: a peripheral may require software to clear a status bit before enabling an interrupt. If firmware enables the interrupt first, the system may immediately enter an unexpected interrupt loop. Another example is a DMA controller where software starts the transfer before writing the destination address, causing data to be written to the wrong location. Similarly, a register may be write-one-to-clear, but firmware may treat it like a normal read-write register.

   These bugs are found through hardware-software co-verification, register tests, firmware-driven simulation, emulation, virtual platforms and UVM register models. The verification plan must check register reset values, access permissions, side effects, ordering requirements, interrupt clearing behavior and error conditions.

   Exam line: **Software-hardware interaction bugs occur when hardware behavior and firmware programming assumptions do not match.**

4. **Concurrency bugs**: DMA, CPU, cache, memory controller and bus masters may access shared resources at the same time.

   Concurrency means that multiple activities happen at the same time. In a SoC, the CPU may execute software, DMA may transfer data, a display controller may fetch pixels, an accelerator may read input buffers, and a memory controller may serve all of them together. Even if each block works correctly alone, simultaneous access can create bugs.

   Common concurrency bugs include race conditions, lost updates, inconsistent shared memory data, cache coherency errors, bus arbitration mistakes, deadlocks and starvation. For example, the CPU may read a buffer while DMA is still writing it. Another example is two bus masters requesting the same slave at the same time, but the arbiter incorrectly grants both or blocks both.

   Verification must create parallel traffic scenarios, not only simple sequential tests. Constrained-random testing is useful here because it can generate many combinations of CPU, DMA, interrupt and memory traffic. Scoreboards, assertions and coverage are needed to check whether all transactions complete correctly and whether no master is starved.

   Exam line: **Concurrency bugs occur because multiple SoC masters operate simultaneously and compete for shared resources such as buses, memory, registers and interrupts.**

5. **Corner-case explosion**: the number of possible states, transactions and timing combinations becomes too large for directed testing alone.

   A corner case is a rare but legal situation that may expose a bug. In SoC verification, the number of possible corner cases becomes extremely large because many blocks, clocks, resets, interrupts, power modes, bus transactions and software sequences interact.

   Example corner cases include reset during a DMA transfer, interrupt arriving during low-power entry, back-to-back bus bursts, FIFO almost-full and almost-empty transitions, simultaneous read/write to the same register, bus error during cache refill, refresh during urgent DRAM access, and power shutdown while a peripheral is active.

   Directed testing cannot manually cover all these combinations. Therefore, SoC verification uses constrained-random stimulus, functional coverage, assertions, coverage closure, formal verification and regression testing. The goal is not to test random cases blindly, but to systematically cover important state combinations and protocol scenarios.

   Exam line: **Corner-case explosion means the SoC has too many possible legal state and timing combinations to verify only by manually written directed tests.**

6. **IP reuse risk**: reused hard, firm or soft IP may not exactly match the new SoC's bus, clocking, power or performance assumptions.

   SoCs commonly reuse IP blocks to reduce design time. These may be internal IPs from the same company or third-party IPs from external vendors. The problem is that an IP block verified in one SoC may not automatically be correct in another SoC environment.

   Reuse risk appears when the new SoC has a different bus protocol, address map, clock frequency, reset sequence, power-domain structure, interrupt controller, endian format, data width, security requirement or performance requirement. For example, a reused USB controller may assume one reset sequence, but the new SoC reset controller may release resets in another order. A reused memory controller may meet bandwidth requirements in one design but fail when connected to more masters in another design.

   Verification must check IP integration, wrapper logic, protocol adaptation, configuration registers, clock/reset connectivity, power intent, timing assumptions and performance under system traffic. IP reuse saves time only if the integration assumptions are carefully verified.

   Exam line: **IP reuse risk means a previously verified IP block may fail in a new SoC because the surrounding system assumptions have changed.**

7. **Late bug cost**: a bug found after physical design or fabrication is much more expensive than a bug found at executable-model or RTL level.

   The cost of fixing a bug increases as the design moves forward. If a bug is found during specification or executable modeling, it may require only a model or document change. If it is found during RTL, it requires code changes and regression testing. If it is found after synthesis, place-and-route or timing closure, the fix may disturb area, timing and power. If it is found after fabrication, the cost can include silicon respin, delayed product release, board changes, firmware workaround or product recall.

   This is why verification must start early and continue at every abstraction level. Early verification checks the specification and architecture. RTL verification checks functional correctness. Gate-level simulation checks timing-related behavior. Emulation and FPGA prototyping run software and long tests. Post-silicon validation checks real hardware behavior.

   In exams, this point is important because it explains why SoC verification methodology is necessary. Verification is not just a final step. It is a continuous process used to reduce risk before the chip is manufactured.

   Exam line: **Late bug cost means the later a design error is found in the SoC flow, the more expensive and time-consuming it becomes to fix.**

Therefore, SoC verification needs a **verification methodology**, not only individual test cases. OVM, UVM and VVM are methodologies because they define how to organize testbenches, generate stimulus, monitor behavior, compare results, measure coverage and reuse verification components.

### Verification Strategy

In a top-down SoC design flow, verification starts early. The system is first described using system-level models or executable specifications. A system-level verification environment is created with testbenches, models and a formal test plan. This environment becomes the golden reference for verifying blocks, subsystems and the final integrated SoC. This is better than waiting until all blocks are complete because late system-level bugs cause expensive redesign.

In a bottom-up flow, blocks may be designed and verified separately first, and then the full system is verified after integration. This is useful for beginning implementation quickly, but it is risky because system-level bugs appear late. A top-down or mixed approach is normally stronger for SoC work because the system verification environment is ready before all blocks are completed. Then each block can be verified in the same context in which it will finally be used.

The basic SoC verification flow is:

1. **Requirement analysis and verification plan**: Identify all features, interfaces, protocols, error cases and performance conditions to be verified.
2. **Executable specification or golden model**: Create a behavioral model/reference model that predicts correct output.
3. **Testbench architecture**: Build reusable drivers, monitors, agents, scoreboards, coverage collectors and assertions.
4. **Block-level verification**: Verify individual IPs using directed tests, constrained-random tests, assertions and coverage.
5. **Subsystem verification**: Verify communication among related IPs, such as processor-memory, bus-DMA, cache-coherency or memory-controller interactions.
6. **System-level verification**: Verify the complete SoC with realistic software, interrupts, bus traffic, power modes, resets and corner cases.
7. **Coverage closure**: Measure functional coverage and code coverage to find untested scenarios, then add tests or constraints to close the gap.
8. **Regression testing**: Re-run the test suite automatically whenever RTL, firmware or configuration changes.
9. **Gate-level and timing verification**: Run selected gate-level simulations, static timing analysis and equivalence checks after synthesis.
10. **DFT and manufacturing test planning**: Add scan, BIST, test access mechanisms and test scheduling so manufactured chips can be tested efficiently.

The most important idea is **coverage-driven verification**. In coverage-driven verification, tests are not considered complete only because simulation passed. They are considered strong only when the verification plan's features, corner cases and protocol situations have been covered. This is why functional coverage and code coverage are repeatedly used in SoC verification answers.

### Verification Environment To Draw

Remember this diagram for exams. It is the standard structure behind OVM/UVM-style verification.

```text
                  +----------------------+
                  |       Test Case       |
                  | sequences / scenarios |
                  +----------+-----------+
                             |
                             v
                  +----------------------+
                  |      Sequencer       |
                  +----------+-----------+
                             |
                             v
                  +----------------------+
                  | Driver / BFM / Agent |
                  +----------+-----------+
                             |
                             v
+----------------+     +-----+------+     +------------------+
| Coverage       |<----| DUT / SoC  |---->| Monitor          |
| Collector      |     | Interface  |     | transaction log  |
+----------------+     +-----+------+     +--------+---------+
                             |                     |
                             v                     v
                  +----------------------+  +---------------+
                  | Assertions / Checks  |  | Scoreboard    |
                  +----------------------+  | vs reference  |
                                            +---------------+
```

Write below the diagram: **Stimulus is generated by sequences, driven through BFMs or drivers to the DUT, monitored at interfaces, checked by assertions and scoreboards, and measured using coverage.**

### How The Verification Environment Works

The **test case** selects the scenario to be verified, such as reset behavior, bus read/write transfer, burst transfer, interrupt handling, illegal access, DMA transfer or memory-controller access. The **sequence** generates transaction items. A transaction is a high-level operation, for example: "AXI write to address A with data D" rather than individual signal transitions.

The **sequencer** controls the order in which transactions are sent. The **driver** or **BFM** converts each transaction into pin-level signal activity according to the protocol. For example, an AXI driver converts a write transaction into valid/ready handshakes, address phase, data phase and response phase.

The **DUT** is the design under test, such as an IP block, subsystem or complete SoC. The **monitor** observes the DUT interface without driving it. It converts signal-level activity back into transactions and sends them to the scoreboard and coverage collector. This is important because checking should be based on what the DUT actually did, not only on what the test intended to do.

The **scoreboard** compares actual DUT output against expected output from the reference model. If the DUT output differs, the scoreboard reports an error. The **coverage collector** records which features, transactions, boundary cases and protocol states have been exercised. **Assertions** check local rules such as "grant must follow request", "valid data must remain stable until ready", or "reset must put the block into a known state".

This structure gives three advantages. First, it makes the testbench reusable. Second, it separates stimulus generation, signal driving, checking and coverage. Third, it supports automation through constrained-random testing and regression runs.

### OVM - Open Verification Methodology

**OVM** stands for **Open Verification Methodology**. It is a SystemVerilog-based open verification class library and methodology originally developed by Cadence and Mentor Graphics. OVM introduced a common framework for building reusable verification components, verification IP, tests and testbenches.

In OVM, the testbench is **component-based** and **transaction-based**. Component-based means the testbench is split into reusable blocks such as generators, drivers, monitors, scoreboards and coverage collectors. Transaction-based means the testbench communicates using high-level operations such as read, write, burst, packet, frame or command, instead of manually toggling every signal in every test.

#### How A Testbench Becomes Transaction-Based

A testbench becomes **transaction-based** when the test writer stops describing every clock-by-clock signal change in the main test and instead describes one complete protocol operation as a structured object or record.

At signal level, an AXI write is many small events:

```text
put address on AWADDR
assert AWVALID
wait for AWREADY
put data on WDATA
assert WVALID
wait for WREADY
set WLAST if final beat
wait for BVALID
check BRESP
assert BREADY
```

At transaction level, the same operation is represented as one item:

```text
AXI_WRITE {
  address     = 0x8000_1000
  data        = [0x12, 0x34, 0x56, 0x78]
  burst_len   = 4
  transfer_sz = 32 bits
  response    = expected OKAY
}
```

The technical mechanism is:

1. **Transaction object / sequence item**: A class or record stores operation fields such as address, data, read/write type, burst length, byte enables, ID, response type and delay. In UVM this is usually a `uvm_sequence_item`.
2. **Sequence**: The sequence creates transaction objects. It may create directed transactions or constrained-random transactions.
3. **Sequencer**: The sequencer orders and arbitrates which transaction item is sent next to the driver.
4. **Driver / BFM - Bus Functional Model**: The driver receives the transaction and converts it into exact pin-level protocol activity using a virtual interface. This is where valid/ready handshakes, clock waits, address phase, data phase and response phase are actually driven.
5. **DUT - Design Under Test**: The real RTL still sees only signals. The DUT does not know that the test was written as a transaction.
6. **Monitor**: The monitor samples the same interface signals and reconstructs what happened into a transaction object.
7. **Analysis port / scoreboard / coverage collector**: The monitor sends reconstructed transactions to the scoreboard and coverage collector. The scoreboard checks expected vs actual behavior at transaction level instead of checking every waveform manually.

So transaction-based verification does not remove signal-level behavior. It **localizes** signal-level protocol detail inside the driver and monitor. The rest of the testbench works with meaningful operations.

Typical UVM-style flow:

```text
sequence creates transaction
        |
        v
sequencer sends transaction to driver
        |
        v
driver converts transaction into signal toggles
        |
        v
DUT responds at signal level
        |
        v
monitor observes signals and rebuilds transaction
        |
        v
scoreboard and coverage check transaction meaning
```

Small pseudo-code idea:

```systemverilog
class axi_item extends uvm_sequence_item;
  rand bit        write;
  rand bit [31:0] addr;
  rand bit [31:0] data[];
  rand int        burst_len;
  bit  [1:0]      response;
endclass

// Test writer thinks at transaction level:
item.write = 1;
item.addr = 32'h8000_1000;
item.burst_len = 4;
start_item(item);
finish_item(item);

// Driver hides the pin-level protocol:
seq_item_port.get_next_item(item);
drive_axi_address_phase(item.addr, item.burst_len);
drive_axi_data_phase(item.data);
collect_axi_response(item.response);
seq_item_port.item_done();
```

This is why it is called transaction-based: the testbench communication between sequence, driver, monitor, scoreboard and coverage is based on **transaction objects**, while only the driver and monitor deal with cycle-by-cycle protocol signals.

This matters in SoC verification because most SoC bugs occur at interfaces. If an SoC uses standard buses or protocols, it is inefficient to write a new protocol testbench every time. A reusable OVM verification component can be connected to the same kind of interface in many designs. For example, an OVM-style bus agent can be reused when verifying an IP block, then reused again when that IP is integrated into a subsystem, and then reused again at full-chip level.

OVM improved verification productivity because it supported:

- **Reusable Verification Intellectual Property (VIP)**, also called verification IP, for standard interfaces.
- **Transaction-level modeling (TLM)** for communication between testbench components.
- **Constrained-random verification** to explore many valid scenarios.
- **Functional coverage** to measure whether important features were tested.
- **Scoreboards and monitors** for automated checking.
- **Configuration and factory concepts** for modifying environments without rewriting all code.

The main limitation of OVM is historical. It was a strong methodology, but the industry still had multiple competing approaches. Different teams used OVM, VMM or internal methodologies, so verification IP reuse across companies and tools was not smooth. This is why UVM became important: it standardized the reusable verification concepts that OVM had already popularized.

In an exam, write this line clearly: **OVM is the open SystemVerilog verification methodology that provided the base for UVM, and its main contribution was reusable transaction-level verification components.**

### UVM - Universal Verification Methodology

**UVM** stands for **Universal Verification Methodology**. It is the most widely used SystemVerilog verification methodology for reusable, scalable and standardized verification environments. Its purpose is to improve interoperability, reduce rewriting of verification IP and make verification components easier to reuse across projects, teams and EDA tools.

UVM keeps the useful ideas of OVM and standardizes them. It is built around object-oriented SystemVerilog classes and a well-defined testbench hierarchy. A UVM testbench usually has:

- **uvm_test**: top-level test that selects configuration and sequences.
- **uvm_env**: verification environment containing agents, scoreboards and coverage.
- **uvm_agent**: groups sequencer, driver and monitor for one interface.
- **uvm_sequencer**: controls the stream of transaction items.
- **uvm_driver**: converts transaction-level items into pin-level signal activity.
- **uvm_monitor**: observes DUT interface activity and converts it back into transactions.
- **uvm_scoreboard**: compares actual DUT behavior with expected behavior.
- **coverage collector**: measures functional coverage against the verification plan.
- **assertions**: check protocol rules and design properties during simulation.

#### Meaning Of Functional Coverage

**Functional coverage** means measuring whether the important functions, features, scenarios and corner cases mentioned in the verification plan have actually occurred during simulation. It answers the question: **Did we test the required behavior?**

This is different from only asking whether the test passed. A test can pass but still be weak if it never exercised important situations. For example, a bus test may pass after checking only normal single transfers, but it may not have covered burst transfers, error responses, unaligned accesses, back-to-back requests, reset during transfer or maximum address boundary cases.

Functional coverage is usually planned by the verification engineer. The engineer decides what must be covered based on the specification. Examples:

- For a **bus protocol**, cover read, write, burst length, response type, wait states, error response and boundary address.
- For a **DMA controller**, cover source address, destination address, transfer size, interrupt generation, abort, error condition and overlapping CPU access.
- For a **memory controller**, cover read, write, row hit, row miss, bank conflict, refresh, priority and QoS cases.
- For an **interrupt controller**, cover interrupt priority, masking, nesting, simultaneous interrupts and interrupt clear behavior.

In UVM, a coverage collector or subscriber samples transactions observed by the monitor and records whether planned cases have been hit. If some cases are not hit, they are called **coverage holes**. The verifier then adds new directed tests, modifies random constraints or creates new sequences to hit those missing cases.

Exam line: **Functional coverage measures whether the planned design features, corner cases and protocol scenarios have been exercised, so it tells the verification team what has actually been tested.**

The main strength of UVM is that it supports **coverage-driven verification**. In simple directed testing, the engineer writes a few hand-made tests. In UVM, constrained-random sequences generate many legal and corner-case transactions. Monitors and coverage collectors report what has actually been exercised. If coverage holes remain, constraints or directed tests are added. This loop continues until coverage closure is reached.

UVM is deep because it solves four common SoC verification problems:

1. **Stimulus generation problem**: sequences and sequence items generate structured transactions, including legal random, illegal, stress and corner-case scenarios.

   In verification, **stimulus** means the input activity applied to the DUT. For a small circuit, stimulus may be a few input values. For a SoC block, stimulus means full transactions such as bus reads, bus writes, burst transfers, DMA descriptors, interrupt events, reset sequences, packet transfers and error scenarios.

   UVM solves this using **sequence items** and **sequences**. A sequence item represents one transaction, such as an AXI write, APB read, UART frame or DMA command. A sequence generates many such items in a controlled way. The sequence can generate normal legal traffic, random traffic, illegal traffic, stress traffic and rare corner cases.

   This is important because manually writing every test case is not practical in SoC verification. UVM lets the verifier use constrained-random generation: the testbench creates random transactions, but within legal protocol constraints. If a corner case is missing, the verifier can modify constraints or write a directed sequence for that scenario.

   Example: For a memory controller, a UVM sequence can generate reads, writes, back-to-back bursts, unaligned accesses, refresh timing stress, different priorities and bank-conflict situations. This is much stronger than testing only one read and one write.

   Exam line: **UVM solves the stimulus generation problem by using sequence items and sequences to create reusable, constrained-random and directed transaction-level stimulus.**

2. **Checking problem**: scoreboards, reference models and assertions check correctness automatically instead of relying on waveform inspection.

   In simple simulation, a designer may look at waveforms manually and decide whether the output is correct. This is not scalable for SoC verification because there may be millions of cycles, many interfaces and many parallel transactions. Manual checking becomes slow, incomplete and error-prone.

   UVM solves this using **monitors**, **scoreboards**, **reference models** and **assertions**. A monitor observes DUT activity and converts signal-level activity into transactions. A reference model predicts the expected result. A scoreboard compares actual DUT output against the expected output. Assertions check protocol rules immediately during simulation.

   This means the testbench can automatically say pass or fail. It can detect data mismatch, wrong ordering, missing response, illegal protocol behavior, incorrect interrupt, wrong register value or unexpected timeout.

   Example: For a DMA controller, the reference model knows what data should be copied from source memory to destination memory. The scoreboard compares final memory contents with the expected data. If the DMA drops a beat, writes to the wrong address or completes early, the scoreboard reports an error.

   Exam line: **UVM solves the checking problem by using monitors, reference models, scoreboards and assertions to automatically compare expected and actual behavior.**

3. **Reuse problem**: agents and Verification Intellectual Property (VIP) components can be reused across IP (Intellectual Property), subsystem and SoC verification.

   SoC verification contains many repeated interfaces. For example, AXI, APB, AHB, UART, SPI, I2C, PCIe, DDR and Ethernet may appear in many designs. If the verification team writes a new testbench from zero for every block, verification becomes slow and inconsistent.

   UVM solves this by organizing verification components into reusable structures. A **UVM agent** usually contains a sequencer, driver and monitor for one interface. **Verification Intellectual Property (VIP)**, also called **verification IP**, is a packaged reusable verification component for a standard protocol. The same agent can be used at block level, subsystem level and SoC level.

   Reuse has two forms. **Horizontal reuse** means using the same agent across different projects or IPs that use the same protocol. **Vertical reuse** means using the same verification component from IP-level verification up to subsystem and full-SoC verification.

   Example: An AXI UVM agent used to verify a DMA block can later be reused to verify a memory subsystem and then reused again in the complete SoC simulation. At IP level, the agent may be active and generate traffic. At SoC level, the same agent may become passive and only monitor traffic.

   Exam line: **UVM solves the reuse problem by packaging drivers, monitors, sequencers, agents and Verification Intellectual Property (VIP) so that the same verification components can be reused across IP, subsystem and SoC levels.**

4. **Control problem**: factory override, configuration database and phasing allow the same testbench to be customized without rewriting the whole environment.

   A large verification environment must be flexible. Different tests may need different drivers, constraints, protocol settings, address maps, active/passive agents, timeout values, coverage options and error-injection modes. If every test requires rewriting the testbench, the environment becomes unmanageable.

   UVM solves this using three important mechanisms: **factory**, **configuration database** and **phasing**.

   The **factory** allows one component type to be replaced by another at run time. For example, a normal driver can be replaced with an error-injecting driver without changing the original environment code. This is called factory override.

   The **configuration database** passes settings into components. For example, it can pass virtual interface handles, address ranges, agent mode, protocol parameters, scoreboard options and coverage enable settings.

   **Phasing** gives a standard order for building and running the testbench. The environment is built, connected, configured, run and cleaned up in a predictable sequence. This prevents confusion in large testbenches where many components depend on each other.

   Example: In one test, an AXI agent may be active and generate traffic. In another test, the same agent may be passive and only monitor the processor's real traffic. This can be controlled using configuration database without rewriting the full testbench.

   Exam line: **UVM solves the control problem through factory overrides, configuration database and standard phases, allowing a common testbench to be customized for many tests.**

These mechanisms make UVM scalable for large SoC teams because the same environment can generate many kinds of traffic, check itself automatically, reuse verified components and adapt to different tests without rewriting the complete testbench.

UVM also works well with **assertion-based verification**. Assertions check local design rules during simulation. For example, a bus assertion can check that address remains stable while a valid signal is asserted and ready is low. This catches protocol violations immediately and makes debugging easier.

UVM is especially suitable for SoC verification because SoCs are integration-heavy. For example, an AMBA (Advanced Microcontroller Bus Architecture), AXI (Advanced eXtensible Interface), APB (Advanced Peripheral Bus), memory-controller, DMA (Direct Memory Access), PCIe (Peripheral Component Interconnect Express) or UART (Universal Asynchronous Receiver/Transmitter) interface can be verified using reusable UVM agents and Verification Intellectual Property (VIP). These can be reused first at IP level, then at subsystem level, and finally at SoC level. This matches the course idea that system-level verification infrastructure should verify subsystems and components in a common context.

For exams, describe the UVM verification loop like this:

```text
Verification Plan -> UVM Testbench -> Random/Directed Sequences
-> Simulation -> Scoreboard/Assertions -> Coverage Report
-> Add More Tests/Constraints -> Coverage Closure
```

This loop is important because it proves that UVM is not just a testbench library. It is a complete verification methodology.

### VVM - VHDL Verification Methodology

The syllabus writes **VVM**. The safest exam interpretation is **VHDL Verification Methodology**: a structured way of building reusable verification environments in **VHDL - VHSIC Hardware Description Language**. In practical VHDL verification, this idea is commonly represented by **UVVM - Universal VHDL Verification Methodology** and **OSVVM - Open Source VHDL Verification Methodology**.

Be careful: some books and industry material discuss **VMM - Verification Methodology Manual**, not VVM. VMM is a SystemVerilog methodology historically associated with Synopsys and Arm. If the question paper clearly says **VMM**, answer VMM. If it says **VVM**, answer it as VHDL-oriented verification methodology and mention UVVM/OSVVM.

#### Why VVM Is Needed

Traditional VHDL testbenches are often written as long procedural files. They may manually assign signals, wait for clocks, check outputs with simple `assert` statements and print messages. This is acceptable for small blocks, but it becomes weak for SoC/IP verification because:

1. the same bus read/write code is repeated many times,
2. checking is mixed with stimulus and becomes hard to maintain,
3. there is little reusable verification structure,
4. test logs become difficult to interpret,
5. randomized testing and functional coverage are not naturally organized,
6. complex interfaces such as AXI, UART, SPI, I2C or Ethernet need protocol-level abstraction.

VVM-style methodologies solve this by raising the testbench from **signal-level toggling** to **transaction-level verification**. Instead of writing every signal transition manually, the test writer calls high-level operations such as:

```text
write(address, data)
read(address, expected_data)
send_uart(byte)
check_value(actual, expected)
```

This makes the testbench easier to read, reuse and debug.

Exam line: **VVM gives VHDL verification a structured methodology by separating stimulus generation, bus functional access, checking, coverage, logging and reusable verification components.**

#### UVVM - Universal VHDL Verification Methodology

**UVVM** means **Universal VHDL Verification Methodology**. It is a free and open-source methodology/library for creating structured VHDL-based testbenches. UVVM is useful because it gives VHDL users a methodology similar in spirit to UVM, but using VHDL packages, procedures, records, entities and architectures instead of SystemVerilog classes.

UVVM has two practical levels:

1. **Simple level**: utility library plus **BFMs - Bus Functional Models**.
2. **Advanced level**: **VVC Framework - VHDL Verification Component Framework**, VVCs and command distribution.

A **BFM - Bus Functional Model** is a verification model that performs protocol-level actions. For example, instead of manually toggling address, data, valid and ready signals, an AXI-Lite BFM can provide a procedure such as:

```text
axilite_write(address, data)
axilite_read(address, data)
```

The BFM hides the detailed pin-level protocol and lets the test writer think in transactions.

A **VVC - VHDL Verification Component** is a reusable VHDL verification component, usually built around a BFM. It accepts high-level commands from the test sequencer, executes those commands on a DUT interface, logs activity and supports checking. A VVC is similar in purpose to a UVM agent, but it is implemented using VHDL style.

For example, an AXI VVC can be used to generate AXI transactions, a UART VVC can send and receive serial frames, and an SPI VVC can perform SPI transfers. The test sequencer controls these components using readable high-level commands.

Exam line: **UVVM provides VHDL testbench structure through utility packages, Bus Functional Models and VHDL Verification Components.**

#### OSVVM - Open Source VHDL Verification Methodology

**OSVVM** means **Open Source VHDL Verification Methodology**. It is another major VHDL verification methodology. OSVVM provides package-based verification capabilities for VHDL testbenches.

Important OSVVM features are:

- **Transaction-Level Modeling (TLM)**: verification is written using high-level transactions rather than only signal assignments.
- **RandomPkg**: supports random value generation and constrained-random style tests.
- **CoveragePkg**: supports functional coverage, so the verification team can measure whether planned scenarios have occurred.
- **ScoreboardGenericPkg**: provides scoreboard support for comparing expected and actual results.
- **AlertLogPkg**: provides controlled error reporting, alerts and pass/fail messages.
- **TranscriptPkg**: supports transcript/log file generation.
- **MemoryPkg**: provides memory modeling utilities.
- **FIFOs and synchronization utilities**: help coordinate parallel testbench processes.

The most important OSVVM idea is that VHDL can support advanced verification features such as randomized testing, functional coverage, scoreboards and logs without changing to SystemVerilog. OSVVM also emphasizes **Intelligent Coverage randomization**, where coverage goals guide stimulus generation so that repeated useless random values are reduced.

Exam line: **OSVVM adds advanced verification features to VHDL, including transaction-level modeling, constrained random generation, functional coverage, scoreboards, FIFOs, logs, alerts and memory models.**

#### VVM-Style Testbench Architecture

Draw this if the exam asks for a VVM/UVVM/OSVVM environment:

```text
              +----------------------+
              |   VHDL Test Case     |
              |  Test Sequencer      |
              +----------+-----------+
                         |
          high-level commands / transactions
                         |
              +----------v-----------+
              | VVC / BFM Layer      |
              | protocol operations  |
              +----------+-----------+
                         |
                  signal-level pins
                         |
              +----------v-----------+
              | DUT - Design Under   |
              | Test                 |
              +----------+-----------+
                         |
          observed responses / events
                         |
        +----------------+----------------+
        |                                 |
+-------v--------+              +---------v---------+
| Monitor/Checker|              | Scoreboard        |
| protocol check |              | expected vs actual|
+-------+--------+              +---------+---------+
        |                                 |
        +----------------+----------------+
                         |
              +----------v-----------+
              | Coverage + Logs +    |
              | Alerts / Reports     |
              +----------------------+
```

This diagram shows the key principle: the test case does not directly control every DUT signal. It sends high-level commands to reusable verification components. Those components drive the DUT, monitor behavior, check results, collect coverage and report errors.

#### Step-By-Step VVM Verification Flow

1. **Create a verification plan**: Decide which features, commands, corner cases, error cases and protocol rules must be verified.
2. **Build reusable BFMs/VVCs**: Create or reuse protocol-level components for interfaces such as AXI, APB, UART, SPI, I2C or memory bus.
3. **Write test sequences**: Use readable high-level commands instead of manually toggling signals.
4. **Drive the DUT**: The BFM/VVC converts the transaction into pin-level signal activity.
5. **Monitor the DUT response**: A monitor or checker observes outputs, protocol behavior and response timing.
6. **Use a scoreboard**: Expected transactions are compared with actual DUT output.
7. **Collect functional coverage**: The testbench records whether important values, boundary cases and protocol scenarios occurred.
8. **Log alerts and results**: Errors, warnings, notes and final pass/fail results are printed in a controlled format.
9. **Improve tests until coverage closure**: If coverage holes remain, add new random constraints or directed tests.

#### Example: VVM For A UART Block

Suppose the DUT is a UART controller.

Without VVM-style methodology, the testbench may manually toggle serial input bits, wait for exact bit times, check status registers and print messages. This becomes hard to maintain.

With VVM/UVVM/OSVVM style:

- a UART BFM sends bytes using a high-level command,
- a UART VVC receives serial frames,
- the scoreboard compares transmitted bytes with received bytes,
- coverage records baud-rate modes, parity modes, stop-bit settings and error cases,
- alert/log packages report framing error, parity error or timeout.

So the test becomes readable:

```text
configure_uart(baud_rate, parity, stop_bits)
uart_transmit(data_byte)
expect_uart_receive(data_byte)
check_coverage()
```

The actual VHDL syntax depends on the library, but the exam idea is this: **VVM makes VHDL verification transaction-oriented, reusable and self-checking.**

#### VVM Compared With UVM

VVM and UVM solve similar verification problems, but they use different languages and mechanisms.

| Point | UVM | VVM / UVVM / OSVVM |
|---|---|---|
| Main language | SystemVerilog | VHDL |
| Main style | Object-oriented class library | VHDL packages, procedures, records, entities and architectures |
| Stimulus | Sequences and sequence items | Test sequencer commands, BFMs and VVCs |
| Reusable component | Agent / VIP | BFM / VVC / verification component |
| Checking | Monitors, scoreboards, assertions | Checkers, scoreboards, alerts, logs |
| Coverage | Functional coverage in SystemVerilog/UVM | OSVVM coverage packages or VHDL coverage utilities |
| Best fit | Large ASIC/SoC SystemVerilog verification | VHDL and FPGA-heavy projects |

The key similarity is that both avoid unstructured testbenches. Both encourage reusable components, transaction-level stimulus, automatic checking, scoreboards, logging and coverage.

The key difference is that UVM is a standardized SystemVerilog class-based methodology, while VVM/UVVM/OSVVM gives similar structure to VHDL verification.

#### Why VVM Matters In SoC Verification

SoC designs contain many reused IP blocks and standard interfaces. If a VHDL team verifies every interface manually, the testbench becomes difficult to scale. VVM helps because:

- BFMs avoid repeated low-level bus-driving code,
- VVCs make interface verification reusable,
- scoreboards automate checking,
- coverage tells whether the test plan is exercised,
- alerts/logs make debugging easier,
- transaction-level commands make tests readable,
- reusable VHDL components can be used at IP, subsystem and SoC levels.

For SoC verification, this means a UART VVC, SPI VVC, AXI BFM or memory model can first verify a block, then be reused when that block is integrated into a subsystem or full SoC.

#### Limitations And Safe Exam Wording

Do not write that VVM is the same as UVM. They are similar in goal, but not identical in implementation.

Safe exam wording:

**VVM refers to VHDL-oriented verification methodology. In practice it is commonly represented by UVVM and OSVVM. It provides UVM-like discipline for VHDL testbenches by using Bus Functional Models, VHDL Verification Components, transaction-level commands, scoreboards, functional coverage, logs and alerts. It is especially useful for VHDL and FPGA-heavy projects.**

### Comparison Of OVM, UVM And VVM

| Point | OVM | UVM | VVM / UVVM / OSVVM |
|---|---|---|---|
| Full form | Open Verification Methodology | Universal Verification Methodology | VHDL Verification Methodology / Universal VHDL Verification Methodology / Open Source VHDL Verification Methodology |
| Main language | SystemVerilog | SystemVerilog | VHDL |
| Status | Predecessor of UVM | Standard industrial methodology | VHDL-oriented verification framework |
| Main purpose | Reusable SV verification components and testbenches | Standard reusable and interoperable verification environments | Structured VHDL testbenches with BFMs/VVCs/coverage |
| Key idea | Open reusable Verification Intellectual Property (VIP) and Transaction-Level Modeling (TLM)-based testbench | Standardized coverage-driven, constrained-random verification | VHDL-based reusable verification components and utilities |
| Best use | Legacy OVM environments, understanding UVM roots | Large ASIC/SoC/IP verification | VHDL and FPGA-heavy projects |
| Exam point | OVM formed the base of UVM | UVM is the standardized successor and most widely used | VVM gives UVM-like structure to VHDL verification |

### SoC Test Scheduling And Test Integration

Verification checks design correctness before fabrication, but **testing** checks manufactured chips for defects. Testing is difficult because an SoC contains many embedded cores and internal nodes that are not directly accessible from chip pins. As transistor count increases, the number of possible internal fault sites also increases, so **DFT** and **scan chains** are used to improve controllability and observability.

**SoC test integration** means combining the test requirements of all cores and IP blocks into one chip-level test strategy. Each IP may come with its own testbench, manufacturing tests, BIST, scan chains or test access requirements. At SoC level, these tests must be connected through wrappers, test access mechanisms and external test interfaces such as JTAG. The aim is to make all embedded cores testable after integration.

**SoC test scheduling** means deciding the order and parallelism of tests so total test time is minimized without violating constraints. Tests cannot always run together because they may share a test bus, exceed power limits, require the same memory, or interfere with each other. A good schedule runs independent tests in parallel where possible and serializes conflicting tests.

For test integration, think of the SoC as many cores hidden inside one chip. External **ATE - Automatic Test Equipment** cannot directly touch every internal flip-flop, memory and IP interface. So the designer adds **DFT - Design for Testability** features. Scan chains improve controllability and observability of sequential logic. **BIST - Built-In Self-Test** helps memories or cores test themselves. Test wrappers isolate cores during testing. **TAM - Test Access Mechanism** transports test data from chip pins or JTAG into the embedded cores.

Draw this if the question moves toward testing:

```text
External Tester / JTAG
          |
          v
  +------------------+
  | Test Controller  |
  +--------+---------+
           |
           v
  +------------------------+        +----------------+
  | TAM - Test Access      |------->| Core Wrapper   |
  | Mechanism / Test Bus   |        +-------+--------+
  +------------------------+                |
                                            v
                                    +---------------+
                                    | IP Core / BIST|
                                    +---------------+
```

The test controller selects which test runs. The **TAM - Test Access Mechanism** carries test data. The wrapper connects or isolates the core during test mode. **BIST - Built-In Self-Test** generates internal test patterns and checks results, especially for embedded memories.

Important constraints in test scheduling are:

- **Power constraint**: too many tests running together can exceed safe power.
- **TAM - Test Access Mechanism constraint**: multiple cores may share limited test bus or TAM - Test Access Mechanism width.
- **Resource conflict**: two tests may need the same memory, processor, bus or clock source.
- **Dependency constraint**: some tests must run after reset, configuration or another test.
- **Time constraint**: total test application time must be reduced for manufacturing cost.

Example: suppose an SoC has CPU test, SRAM BIST, DSP test and bus interconnect test. CPU scan and DSP scan may be able to run in parallel if they use different **TAM - Test Access Mechanism** channels and do not exceed the power limit. But SRAM BIST and CPU test may need to be separated if both create high switching activity or need the same memory bus. The schedule is therefore not random; it is an optimization problem under power, time and resource constraints.

Thus, a complete SoC verification and testing strategy moves from early executable models and verification environments to block-level verification, system integration verification, coverage closure, DFT, test integration and final test scheduling.

<a id="topic-1-final-answer"></a>

### Final Exam-Ready Answer

SoC verification and testing are essential because a modern SoC integrates many heterogeneous IP blocks such as processors, memories, buses, accelerators, peripherals, clock/reset logic, power-management logic and embedded software. Verification ensures before fabrication that the design satisfies its specification, while testing ensures after fabrication that the manufactured chip has no physical faults. Therefore, verification is related to design correctness, while testing is related to manufacturing correctness.

The SoC verification process begins with a verification plan derived from the system requirements. The plan identifies the functions, interfaces, protocols, boundary conditions, error cases and performance conditions that must be verified. A system-level model or executable specification is built and used as a golden reference. Individual IP blocks are then verified using testbenches, bus functional models, directed tests, constrained-random tests, assertions, coverage collectors and scoreboards. After block-level verification, subsystem and full-chip verification are performed to check communication among IPs, bus protocols, interrupt behavior, memory interactions, reset behavior, clock-domain interactions, power modes and software execution. Regression testing and coverage closure are used to ensure that all required scenarios have been exercised.

OVM, UVM and VVM are structured verification methodologies used to build reusable verification environments. OVM, or Open Verification Methodology, is an open SystemVerilog methodology developed to create reusable verification IP, transaction-level testbenches, monitors, drivers, scoreboards and coverage components. In OVM, tests generate transaction-level stimulus, drivers convert transactions into signal activity, monitors observe DUT interfaces, scoreboards compare expected and actual results, and coverage collectors measure whether verification goals have been reached. OVM is important because it formed the base for UVM.

UVM, or Universal Verification Methodology, is the standardized successor of OVM and is widely used in SoC verification. A UVM environment contains tests, sequences, sequencers, drivers, monitors, agents, scoreboards, assertions, reference models and coverage collectors. The driver converts transaction-level stimulus into signal-level activity for the DUT, while monitors observe DUT behavior and send transactions to scoreboards and coverage collectors. UVM supports constrained-random stimulus, functional coverage, assertion-based verification, factory-based reuse, configuration control, phasing and transaction-level modeling. Here, **functional coverage** means measuring whether planned features, corner cases and protocol scenarios have actually been exercised during simulation. Therefore, UVM is very useful in SoC verification because the same verification IP can be reused at IP, subsystem and full-chip levels. This reuse is important because SoCs contain many standard interfaces and reused IP blocks.

VVM refers to VHDL-oriented verification methodology, commonly represented by UVVM or OSVVM. It provides structured VHDL testbenches using bus functional models, VHDL verification components, scoreboards, logs, alerts, coverage and randomized testing. It is useful for VHDL and FPGA-based projects where a team wants UVM-like verification discipline without shifting completely to SystemVerilog. Thus, OVM and UVM are mainly SystemVerilog-based methodologies, while VVM gives similar structured verification ideas to VHDL environments.

After functional verification, SoC testing is planned for manufactured silicon. Test integration combines the test requirements of all embedded cores, memories and buses into one chip-level DFT strategy using scan chains, BIST, wrappers and test access mechanisms. Test scheduling decides the order and parallel execution of tests so that test time is minimized without violating power, resource and test-access constraints. Hence, OVM, UVM and VVM help verify design correctness before fabrication, while DFT, test integration and test scheduling help test the fabricated SoC efficiently.

<a id="topic-1-technical-words"></a>

### Technical Words To Use For Marks

- **System-level verification environment** (write this because it shows you know SoC verification is planned at system level, not only after block design.)
- **Formal test plan** (write this because it proves the answer is not random testing; every feature must map to planned tests.)
- **Golden model / reference model** (write this because scoreboards need expected results for comparison.)
- **Verification Intellectual Property (VIP) / Verification IP** (write this because OVM/UVM are mainly about reusable verification components for standard interfaces and protocols.)
- **Transaction-Level Modeling / TLM** (write this because SoC buses are easier to verify using transactions instead of only pin toggles.)
- **Bus Functional Model / BFM** (write this because course slides mention bus functional models as IP deliverables.)
- **Driver** (write this because it converts transactions into DUT signal activity.)
- **Monitor** (write this because it observes DUT behavior without driving signals.)
- **Scoreboard** (write this because it shows automated output checking.)
- **Functional coverage** (write this because it shows how we know required scenarios have been exercised.)
- **Code coverage** (write this because it measures RTL statement/branch/toggle coverage.)
- **Coverage closure** (write this because it is a standard endpoint of verification.)
- **Constrained-random stimulus** (write this because UVM/OVM are strongly associated with randomized legal scenario generation.)
- **Assertion-Based Verification / ABV** (write this because protocol and timing rules can be checked automatically during simulation.)
- **Regression testing** (write this because SoC verification must rerun tests after RTL changes.)
- **Agent** (write this because UVM environments group sequencer, driver and monitor into reusable agents.)
- **Sequencer / Sequence** (write this because UVM stimulus generation is sequence-based.)
- **Factory and configuration database** (write this because these are UVM reuse/customization mechanisms.)
- **Reusable verification component** (write this because OVM/UVM/VVM mainly exist to avoid rewriting testbench components for every IP.)
- **VVC - VHDL Verification Component** (write this because it is the VHDL/UVVM counterpart of a verification component.)
- **DFT - Design for Testability** (write this because testing manufactured chips requires controllability and observability.)
- **Scan chain** (write this because scan explains how internal storage cells become controllable and observable during testing.)
- **BIST - Built-In Self-Test** (write this because embedded memories/cores often need self-test support.)
- **TAM - Test Access Mechanism** (write this because SoC test scheduling depends on access bandwidth.)
- **Test scheduling** (write this because it connects verification/testing theory to the CLO 5 test-planning part.)
- **Test integration** (write this because each IP's tests must be combined into a chip-level strategy.)

<a id="topic-1-diagrams"></a>

### Images / Diagrams To Remember

1. **Syllabus image**: It contains the exact topic and CLO mapping. Remember it only for mapping, not for drawing.
2. **Verification environment diagram above**: Draw this in the exam for OVM/UVM/VVM questions.
3. **Testing flow idea**: If the question asks test scheduling/integration, draw:  
   `IP/Core Tests -> Test Wrapper/BIST/Scan -> TAM - Test Access Mechanism/JTAG/Test Controller -> Test Schedule -> ATE`.

---

<a id="topic-2"></a>

## Topic 2: SoC Verification Flow

<a id="topic-2-question"></a>

### Question

**Explain the SoC verification flow in detail.**

### CLO Mapping

This topic belongs to **CLO 5: Discuss the SoC Design Verification strategies and Test Scheduling**.

Reason: **SoC verification flow** is directly listed under the **SoC Verification and Testing** part of the syllabus. It is not a memory-design or processor-architecture topic; it is about the strategy used to prove that an SoC design is correct before fabrication and ready for test planning.

### What The Question Is Asking

The examiner wants the complete sequence of activities followed during SoC verification. Do not write only "simulation is done". A good answer must explain how verification starts from requirements, how a verification plan is made, how block-level and system-level verification are connected, how hardware/software co-verification is done, and how sign-off is reached using coverage and regression.

For full marks, answer in this order:

1. Define SoC verification flow.
2. Explain why a flow is required.
3. Draw the SoC verification flow diagram.
4. Explain every stage deeply.
5. Mention the feedback loop: bugs and coverage holes go back to RTL, testbench or specification.
6. End with verification sign-off, DFT readiness and test integration.

<a id="topic-2-explanation"></a>

### Core Idea

**SoC verification flow** is the step-by-step process used to prove that a System on Chip (SoC) behaves according to its specification before it is manufactured. It does not mean running one simulation at the end. It means checking the design repeatedly at different levels as the SoC becomes more detailed: first at the system-model level, then at the IP/block level, then at the subsystem level, then at the full-chip level, then with embedded software, and finally after synthesis and timing checks.

Think of it like this: an SoC starts as a requirement and architecture idea. Then it becomes executable models, RTL blocks, connected subsystems, a full-chip RTL design, a gate-level netlist and finally silicon. At each stage, verification asks: **Does this stage still match the specification?** If the answer is no, the team goes back and fixes the specification, model, RTL, testbench, constraints or software. That backward correction is the **feedback loop**.

It is called a **flow** because the work moves through ordered stages:

```text
Specification -> Model Verification -> IP Verification -> Subsystem Verification
-> Full-Chip Verification -> Hardware/Software Verification
-> Coverage Closure -> Gate-Level/Timing Checks -> Sign-off
```

But it is not a one-way road. If a bug appears during subsystem or full-chip verification, the design may go back to IP RTL, the testbench, the golden model or even the requirement document. Therefore, a practical SoC verification flow is **iterative**, meaning earlier stages may be revisited until the design is correct and coverage goals are satisfied.

Exam line: **SoC verification flow is an iterative, multi-level verification process that checks the SoC from specification and system model through IP, subsystem, full-chip, hardware/software and post-synthesis stages, with feedback loops for bug fixing and coverage closure.**

The key point is this: **SoC verification begins before RTL is complete and continues until final sign-off.** In a good top-down flow, the team first creates system-level models and a verification environment. Then individual blocks are verified inside a reusable context. Finally, the complete SoC is verified with real software, realistic traffic, coverage closure, timing checks and DFT/test readiness checks.

### Figure To Remember

Draw this diagram in the exam. It is the most useful figure for **SoC Verification Flow**.

```text
 Requirements / SoC Specification
              |
              v
 Verification Plan and Coverage Plan
              |
              v
 Executable Model / Golden Reference Model
              |
              v
 Verification Environment
 Testbench + BFM/Agents + Monitors + Scoreboard + Assertions
              |
              v
 IP / Block-Level Verification
              |
              v
 Subsystem Verification
 Bus + Memory + DMA + Interrupts + Interconnect
              |
              v
 HW/SW Co-Verification
 Firmware + Drivers + RTOS + Boot + Interrupts
              |
              v
 Full-Chip SoC Verification
 Reset + Clocks + Power Modes + Real Use Cases
              |
              v
 Coverage Closure and Regression Testing
              |
              v
 Gate-Level / Timing / Equivalence Checks
              |
              v
 DFT Readiness + Test Integration + Verification Sign-off

 Feedback loop from every stage:
 Bug / Coverage Hole / Spec Ambiguity
      -> update RTL, testbench, model, constraint or specification
```

Figure reference: look at [SOC Design Flow.pdf, p.4](<System on chip/SOC Design Flow.pdf#page=4>) and [SOC Design Flow.pdf, p.6](<System on chip/SOC Design Flow.pdf#page=6>) for the course-slide idea of developing system-level models, a system-level verification environment, testbenches, formal test plan and golden representation early. Also look at [Functional Architecture Co Design 2.pdf, p.12](<System on chip/Functional Architecture Co Design 2.pdf#page=12>) for the stepwise refinement idea from requirements to functional model, architectural model and RTL. This figure is needed because examiners usually give more marks when the flow is shown visually instead of only described in paragraphs.

### How To Remember Each Block In The Flow

Use this memory line:

```text
Spec -> Plan -> Model -> Environment -> IP -> Subsystem -> HW/SW
-> Full Chip -> Coverage -> Gates/Timing -> DFT/Sign-off
```

Each word has a purpose:

1. **Requirements / SoC Specification**

   This is the starting document. It says what the chip must do: features, interfaces, memory map, power modes, reset behavior, clocking, interrupts, performance and software-visible behavior.

   Remember it as: **What should the SoC do?**

   Why it matters: verification cannot prove correctness unless correctness is first defined.

2. **Verification Plan And Coverage Plan**

   This converts the specification into a verification checklist. It says which features will be tested, which tests are needed, which assertions are required, which coverage points must be measured and what sign-off means.

   Remember it as: **How will we prove it?**

   Why it matters: without a plan, tests may pass but important features may remain untested.

3. **Executable Model / Golden Reference Model**

   This is a high-level model of expected behavior. It may be written in C, C++, SystemC, MATLAB, Python, VHDL, SystemVerilog or another modeling language. The scoreboard can compare RTL output with this expected output.

   Remember it as: **What is the correct answer?**

   Why it matters: the testbench needs a trusted expected result, not only waveform inspection.

4. **Verification Environment**

   This is the testbench infrastructure: BFMs, agents, drivers, monitors, scoreboards, assertions and coverage collectors. It generates stimulus, drives the DUT, observes responses, checks correctness and measures coverage.

   Remember it as: **The machine that tests the design.**

   Why it matters: SoC verification needs reusable automated checking, not manual signal toggling.

5. **IP / Block-Level Verification**

   Each individual IP block is verified separately before integration. Examples are UART, SPI, DMA, memory controller, timer, interrupt controller, cache or accelerator.

   Remember it as: **Check every part alone.**

   Why it matters: bugs are easier to find and debug inside a small block than inside the full SoC.

6. **Subsystem Verification**

   Related blocks are connected and verified together. Examples are CPU + bus + memory, DMA + memory controller, peripheral + interrupt controller, or cache + interconnect.

   Remember it as: **Check blocks working together.**

   Why it matters: many SoC bugs are integration bugs, not single-block bugs.

7. **Hardware/Software Co-Verification**

   Hardware is verified together with firmware, drivers, boot code, interrupt service routines or RTOS behavior. This checks whether software programs the hardware correctly and whether hardware responds as software expects.

   Remember it as: **Check hardware with real software behavior.**

   Why it matters: many SoC failures happen because register programming order, interrupt clearing, DMA setup or boot sequence is wrong.

8. **Full-Chip SoC Verification**

   The complete SoC is verified with realistic system scenarios. This includes reset, clocking, power modes, memory map, processor access, debug, interrupts, DMA, boot and end-to-end use cases.

   Remember it as: **Check the whole chip as one system.**

   Why it matters: the final chip must work as an integrated system, not only as separate verified blocks.

9. **Coverage Closure And Regression Testing**

   Coverage closure means checking whether all planned features, corner cases and code structures have been exercised. Regression testing means rerunning tests after changes to ensure old behavior is not broken.

   Remember it as: **Did we test enough, and did fixes break anything?**

   Why it matters: simulation pass is not enough; verification must prove that planned scenarios were covered.

10. **Gate-Level / Timing / Equivalence Checks**

   After synthesis, the RTL becomes a gate-level netlist. The team checks that synthesis did not change behavior, timing constraints are met, clock-domain crossings are safe and the gate-level design matches RTL.

   Remember it as: **Did implementation preserve the RTL behavior?**

   Why it matters: a functionally correct RTL can still fail after synthesis or timing closure.

11. **DFT Readiness + Test Integration + Verification Sign-off**

   DFT readiness checks whether scan, BIST, wrappers and test access mechanisms are ready for manufacturing test. Test integration combines all core tests into a chip-level strategy. Sign-off means verification goals are met and the design is ready to move forward.

   Remember it as: **Is the chip ready to be manufactured and tested?**

   Why it matters: verification connects to manufacturing; a correct design must also be testable after fabrication.

#### One-Line Memory Trick

Write this in rough work before drawing:

```text
What -> How -> Expected -> Testbench -> Blocks -> Groups -> Software
-> Whole Chip -> Coverage -> Gates -> Sign-off
```

This maps to:

```text
Spec -> Plan -> Model -> Environment -> IP -> Subsystem -> HW/SW
-> Full Chip -> Coverage -> Gate-Level -> DFT/Sign-off
```

### Why A Verification Flow Is Required

A SoC contains many components: processor cores, memories, buses, DMA controllers, accelerators, timers, interrupt controllers, clock/reset logic, power-management blocks, debug blocks, analog or mixed-signal IP and embedded software. Verifying each block separately is necessary but not sufficient. A block can pass its own tests and still fail after integration because the bug may be in the interaction.

Examples:

- A DMA controller may work alone, but fail when CPU cache and memory controller access the same memory region.
- A bus slave may pass directed tests, but fail during burst transfers or back-to-back transactions.
- A peripheral may work in RTL, but fail when firmware programs registers in a different order.
- A reset controller may work in one clock domain, but not in another.
- A power-management unit may shut down a block while a transaction is still pending.

Therefore, verification must be **planned**, **layered**, **coverage-driven** and **iterative**. The flow prevents late discovery of system bugs and gives a measurable way to decide whether verification is complete.

### Step 1: Requirements And SoC Specification

The flow begins with the **SoC requirements** and **design specification**. This stage defines what the chip must do. It includes functional requirements, interface protocols, performance targets, power modes, reset behavior, interrupt behavior, memory map, clocking scheme, boot sequence, security features, debug access and expected software behavior.

This step is not just documentation. It decides the verification target. If a feature is not clearly written in the specification, it cannot be verified properly. For example, if the specification does not define what should happen when a bus error occurs during a DMA transfer, the verification team cannot create a correct expected result.

Important outputs of this stage:

- List of SoC features.
- List of IP blocks and interfaces.
- Memory map and register map.
- Protocol assumptions.
- Clock, reset and power-domain details.
- Performance and latency expectations.
- Error handling requirements.
- Software-visible behavior.

Write in the exam: **The specification is the starting point because verification proves conformance to specification, not personal expectation.**

<a id="topic-2-power-modes"></a>

### Power Modes In SoC Verification

A **power mode** is an operating state of the SoC in which power, clocks, voltage and activity are controlled differently to save energy or meet performance needs. A chip does not always run at maximum power. Sometimes it runs normally, sometimes it slows down, sometimes it turns off clocks, and sometimes it shuts down complete blocks to save battery or reduce heat.

Simple meaning:

```text
Power mode = defined power/performance state of the SoC
```

Examples of common power modes:

1. **Active / Run mode**: The processor, clocks, memories and required peripherals are on. The SoC performs normal work.
2. **Idle mode**: The SoC is powered, but some units are waiting. The CPU may be idle while clocks are still available.
3. **Clock-gated mode**: Clock is stopped to an inactive block to reduce dynamic power. The block still has power, so its state may remain.
4. **Sleep / Standby mode**: Many clocks are off and only wake-up logic remains active. The SoC consumes less power but can wake up on an interrupt, timer or external event.
5. **Retention mode**: A block is mostly powered down, but small retention registers keep important state so the block can resume quickly.
6. **Power-gated / Shut-down mode**: Power is completely removed from a block or domain. This saves more power, but the block loses state unless retention is used.
7. **Deep sleep mode**: A very low-power state where most of the SoC is off. Wake-up takes longer because clocks, power domains and memories may need restoration.
8. **DVFS mode**: Dynamic Voltage and Frequency Scaling, where voltage and clock frequency are changed depending on performance need.

Power modes are controlled by a **PMU - Power Management Unit** or power controller. Firmware usually programs control registers to enter or exit low-power states. The PMU then sequences clocks, resets, isolation, retention and power switches.

#### Why Power Modes Must Be Verified

Power modes are risky because the chip changes state while logic may still contain data, pending transactions or interrupts. A block may work correctly in active mode but fail when entering or exiting low-power mode.

Common power-mode bugs:

- A block is powered down while a bus transaction is still pending.
- A clock is gated while data is being transferred.
- A wake-up interrupt is missed.
- A retained register does not keep its value.
- A non-retained register is expected to keep its value but is lost.
- An isolation signal is missing, so an off block drives unknown values into an on block.
- Reset after wake-up happens in the wrong order.
- Firmware enters sleep before DMA or memory write is complete.
- A power domain turns on, but its clock or reset is not released correctly.

This is why power modes are part of SoC verification flow. They must be specified, planned, tested, covered and checked at subsystem and full-chip level.

#### Important Power-Mode Terms

- **Power domain**: A region of the SoC that can be powered independently.
- **Clock gating**: Stopping the clock to an inactive block to reduce dynamic power.
- **Power gating**: Turning off power to a block to reduce leakage power.
- **Retention register**: A special register that keeps important state during low-power mode.
- **Isolation cell**: Logic that prevents an off domain from sending unknown values into an on domain.
- **Level shifter**: Logic used when signals cross between voltage domains.
- **Wake-up source**: An event that brings the SoC out of sleep, such as timer, interrupt, GPIO, RTC or external signal.
- **Low-power entry sequence**: The ordered steps used to enter a low-power mode safely.
- **Low-power exit sequence**: The ordered steps used to restore clocks, power, reset and state after wake-up.
- **PMU - Power Management Unit**: The controller that manages power modes and power-domain sequencing.

#### What Verification Must Check

For power modes, the verification plan should check:

1. Can the SoC enter each power mode correctly?
2. Can the SoC wake up correctly from each power mode?
3. Are clocks stopped only when safe?
4. Are pending bus, DMA and memory transactions completed or safely paused?
5. Are retention registers preserving required state?
6. Are non-retained registers reset or reinitialized correctly?
7. Are isolation cells active when a power domain is off?
8. Are wake-up interrupts detected correctly?
9. Does firmware follow the correct low-power entry and exit sequence?
10. Are power-mode transitions covered in functional coverage?

#### Small Diagram To Remember

```text
 Active / Run
      |
      v
 Idle / Clock Gated
      |
      v
 Sleep / Retention
      |
      v
 Deep Sleep / Power Gated
      |
      v
 Wake-up Event -> Restore Power -> Restore Clocks -> Release Reset -> Resume
```

Exam line: **Power modes are defined SoC operating states such as active, idle, sleep, retention and power-down, used to reduce power by controlling clocks, voltage and power domains. They must be verified because low-power entry, wake-up, retention, isolation, reset and pending transactions can create system-level bugs.**

### Step 2: Verification Plan And Coverage Plan

After the specification, the team prepares a **verification plan**. This is the most important planning document in the verification flow. It maps every feature in the specification to one or more verification activities.

A verification plan answers:

- What must be verified?
- At which level will it be verified: IP, subsystem or full SoC?
- Which tests will be directed?
- Which tests will be constrained-random?
- Which assertions are required?
- Which coverage points are required?
- Which reference model will be used?
- What is the pass/fail condition?
- What is the sign-off condition?

The **coverage plan** is part of the verification plan. It defines what must be measured. Coverage is necessary because a simulation can pass even if it did not exercise important cases. For example, a bus test may pass for single transfers but never test burst transfer, unaligned address, wait states, error response or simultaneous requests from multiple masters.

Types of coverage:

#### 1. Functional Coverage

**Functional coverage** checks whether the planned features, scenarios, corner cases and protocol situations from the verification plan have actually occurred during simulation.

It is based on the **specification**, not directly on RTL code. The verification engineer decides what behavior must be covered. For example, if the specification says a DMA controller supports 8-byte, 16-byte, 32-byte and 64-byte transfers, functional coverage checks whether tests actually exercised all these transfer sizes.

Functional coverage answers:

```text
Did we test the required design behavior?
```

Examples:

- For a bus: read transfer, write transfer, burst transfer, error response, wait state, boundary address.
- For DMA: all transfer sizes, source/destination address ranges, interrupt on completion, abort condition, bus error.
- For power modes: active, idle, sleep, retention, power-down, wake-up from each source.
- For interrupt controller: masked interrupt, unmasked interrupt, simultaneous interrupts, priority handling.

Why it matters: a simulation may pass but still miss important features. Functional coverage tells what scenarios were actually exercised.

Exam line: **Functional coverage is specification-driven coverage that measures whether planned features, corner cases and scenarios have been exercised.**

#### 2. Code Coverage

**Code coverage** checks how much of the RTL code was executed during simulation. It is based on the design implementation, not directly on the specification.

Code coverage answers:

```text
Did our tests execute the written RTL code?
```

Common code coverage types:

- **Statement coverage**: checks whether each RTL statement executed.
- **Branch coverage**: checks whether both true and false paths of `if`, `case` or conditional logic executed.
- **Condition coverage**: checks whether Boolean sub-expressions became true and false.
- **Toggle coverage**: checks whether signal bits switched from 0 to 1 and 1 to 0.
- **FSM coverage**: checks whether finite-state-machine states and transitions were reached.

#### How Code Coverage Is Checked

Code coverage is checked automatically by the simulation tool. The simulator instruments the RTL code, meaning it internally adds counters or tracking points to statements, branches, conditions, signals and FSM states. When tests run, the simulator records which parts of the RTL were exercised and which were not.

Simple example:

```verilog
always_ff @(posedge clk) begin
  if (reset) begin
    state <= IDLE;
  end else if (start) begin
    state <= BUSY;
  end else if (error) begin
    state <= ERROR;
  end
end
```

The coverage tool checks:

- Did the `reset` branch execute?
- Did the `start` branch execute?
- Did the `error` branch execute?
- Did `state` enter `IDLE`, `BUSY` and `ERROR`?
- Did the bits of `state` toggle from 0 to 1 and 1 to 0?

If the tests only apply `reset` and `start`, but never create `error`, then the simulator will report that the `error` branch and `ERROR` state were not covered. This becomes a **coverage hole**. The verification engineer then adds a test or modifies constraints to force an error condition.

So the process is:

```text
Run tests -> simulator records executed RTL parts -> coverage report is generated
-> uncovered code is analyzed -> new tests/constraints are added
```

Important: the simulator checks whether RTL code was executed, but it does not automatically know whether the design behavior is correct. Correctness still needs scoreboards, assertions and reference models.

Example: If a reset error-handling branch exists in RTL but no test causes that error, branch coverage will show that the branch was not executed.

Important distinction: high code coverage does not prove that the design is functionally correct. It only proves that the code was exercised. A test can execute RTL code and still not check the correct output. That is why code coverage must be used with scoreboards, assertions and functional coverage.

Exam line: **Code coverage is implementation-driven coverage that measures whether RTL statements, branches, conditions, toggles and FSM states were exercised by tests.**

#### 3. Assertion Coverage

**Assertion coverage** checks whether assertions were activated, evaluated and meaningfully tested during simulation.

An **assertion** is a rule written to check design behavior. For example:

```text
If valid is high and ready is low, address must remain stable.
```

Assertion coverage answers:

```text
Were the assertion properties actually exercised?
```

This is important because an assertion can exist in the testbench but never be triggered. For example, an assertion may check bus error behavior, but if no test ever creates a bus error, the assertion did not really verify that scenario.

Assertion coverage helps measure:

- whether a property was attempted,
- whether its antecedent/trigger condition occurred,
- whether pass/fail paths were evaluated,
- whether important protocol rules were checked under real stimulus.

Example: In an AXI-like bus, an assertion may check that data remains stable during wait states. Assertion coverage confirms that wait-state conditions actually occurred during simulation, so the assertion was not idle.

Exam line: **Assertion coverage measures whether assertion properties were triggered and evaluated, proving that protocol rules and design properties were actually exercised.**

#### 4. Cross Coverage

**Cross coverage** checks combinations of two or more coverage items. It is important because a feature may work alone, but fail in combination with another feature.

Cross coverage answers:

```text
Did we test important combinations of conditions?
```

Examples:

- Burst length crossed with response type:

  ```text
  burst length = 1, 4, 8, 16
  response type = OKAY, ERROR
  ```

  This checks whether every burst length was tested with both normal and error responses.

- Power mode crossed with interrupt source:

  ```text
  power mode = active, sleep, deep sleep
  interrupt source = timer, GPIO, DMA, UART
  ```

  This checks whether each wake-up source was tested from each low-power state.

- DMA transfer size crossed with address alignment:

  ```text
  transfer size = 8, 16, 32, 64 bytes
  alignment = aligned, unaligned
  ```

  This checks whether the DMA works for all important size and alignment combinations.

Why it matters: SoC bugs often appear only when two features interact. A power mode may work alone, and interrupts may work alone, but interrupt wake-up from deep sleep may fail. Cross coverage catches this kind of missing verification.

Exam line: **Cross coverage measures whether important combinations of features or conditions have been exercised, such as burst length with response type or power mode with interrupt source.**

#### Quick Difference Table

| Coverage type | Main question | Based on | Example |
|---|---|---|---|
| Functional coverage | Did we test required behavior? | Specification / verification plan | DMA transfer sizes, power modes, interrupt cases |
| Code coverage | Did we execute RTL code? | RTL implementation | Statements, branches, toggles, FSM states |
| Assertion coverage | Did properties get exercised? | Assertions / protocol rules | Valid-ready stability property triggered |
| Cross coverage | Did we test combinations? | Coverage model | Power mode crossed with interrupt source |

This stage is selected as a keyword-heavy part because it gives exam marks: it shows that verification is measurable, not random.

### Step 3: Executable Model Or Golden Reference Model

The next step is to create an **executable model** or **golden reference model**. This model predicts the correct behavior of the SoC or a major function. It may be written in C, C++, SystemC, MATLAB, Python, SystemVerilog or another high-level form. The model does not need to include all gate-level details. Its purpose is to represent correct functional behavior.

For example:

- For an image-processing accelerator, the golden model may produce the expected processed image.
- For an encryption accelerator, the golden model may produce the expected ciphertext.
- For a memory controller, the reference model may predict read/write ordering and legal responses.
- For a bus subsystem, the reference model may predict transactions, responses and error behavior.

The golden model is used by the scoreboard. The scoreboard compares actual DUT output with expected output from the reference model. Without a reference model, checking becomes weak because engineers may only inspect waveforms manually.

This step is also useful because it exposes ambiguity early. If the model writer and RTL designer interpret the specification differently, the mismatch is found before silicon.

### Step 4: Verification Environment Development

The verification environment is the infrastructure used to apply stimulus, observe behavior, check results and measure coverage. In an OVM/UVM-style environment, it contains tests, sequences, sequencers, drivers, monitors, agents, scoreboards, coverage collectors, assertions and configuration.

In VVM/UVVM/OSVVM-style environments, the same idea is implemented using VHDL test sequencers, BFMs, VVCs, monitors, scoreboards, alerts and coverage utilities.

The verification environment must be reusable because the same IP or interface may be verified at multiple levels. For example, an AXI agent may be used at IP level to test a slave block, at subsystem level to test an interconnect, and at SoC level to monitor processor traffic.

Important parts:

- **Testbench**: top-level structure that connects verification components to the DUT.
- **Driver/BFM**: converts transactions into pin-level protocol activity.
- **Monitor**: observes DUT signals and converts them back to transactions.
- **Scoreboard**: compares expected and actual results.
- **Assertions**: check protocol rules and design properties.
- **Coverage collector**: records what has been tested. It can record functional coverage items such as transaction type, address range, burst length, transfer size, response type, error condition, reset case, interrupt source, power mode, FIFO full/empty condition, DMA transfer type, cache/memory access type, protocol state and important combinations such as burst length crossed with response type or power mode crossed with interrupt source.
- **Configuration**: controls address maps, active/passive agents, protocol settings and test modes.

A coverage collector usually receives transactions from a monitor. For example, if a monitor observes an AXI write burst, the coverage collector may record: "write transaction occurred", "burst length was 8", "address was in peripheral range", "response was OKAY", and "this happened during active power mode". These records show which planned scenarios have been hit and which are still coverage holes.

This stage is important because a weak testbench gives false confidence. A strong testbench finds bugs automatically and can be reused throughout the flow.

### Step 5: IP Or Block-Level Verification

At block level, each individual IP is verified against its own specification. Examples include UART, SPI, DMA, timer, interrupt controller, cache controller, memory controller, bus bridge, accelerator or custom logic.

Block-level verification checks:

- Reset behavior.
- Register read/write behavior.
- Legal and illegal commands.
- Boundary values.
- Protocol compliance.
- Interrupt generation and clearing.
- Error handling.
- FIFO full/empty conditions.
- Timeout conditions.
- Back-to-back transactions.
- Clock-domain crossing behavior if present.

Block-level verification is necessary because bugs are easier to locate inside a small block. Simulation is also faster at block level, so many random and directed tests can be run. However, block-level verification is not enough because it cannot prove that the IP will interact correctly with other SoC components.

Exam line: **Block-level verification gives confidence in individual IP correctness, but system-level verification is still required for integration correctness.**

### Step 6: Subsystem Verification

After IP verification, related blocks are integrated into subsystems. A subsystem may include processor + bus + memory, DMA + memory controller, image pipeline, audio subsystem, security subsystem, NoC/interconnect subsystem or peripheral subsystem.

Subsystem verification checks interactions among blocks. This stage is where many SoC bugs appear because multiple verified IPs now share clocks, resets, buses, interrupts, memory and power domains.

Important checks:

- Bus arbitration among multiple masters.
- Address decoding and memory map correctness.
- Burst, pipelined and back-to-back transfers.
- DMA and CPU access to shared memory.
- Interrupt routing and prioritization.
- Cache and memory consistency if applicable.
- Reset sequencing across blocks.
- Clock-domain crossing synchronizers.
- Error propagation from slave to master.
- Performance under realistic traffic.

Subsystem verification often uses **passive monitors** on internal interfaces. A passive monitor observes without driving. This is important because it allows the verifier to check internal behavior without disturbing the subsystem.

### Step 7: Hardware/Software Co-Verification

SoC behavior depends not only on RTL hardware but also on software. Therefore, **hardware/software co-verification** is the stage where the hardware design is verified together with the software that will run on it. This software may include boot code, firmware, device drivers, interrupt handlers, RTOS code and application-level test programs.

The main idea is:

```text
Correct RTL + wrong software sequence = system failure
Correct software + wrong hardware behavior = system failure
```

So hardware/software co-verification checks whether the **contract between hardware and software** is correct. That contract includes memory-mapped registers, interrupt behavior, DMA operation, reset values, status bits, error flags, timing assumptions, power-control registers and software-visible side effects.

#### How Hardware/Software Co-Verification Is Performed

This stage can be performed using several platforms:

1. **RTL simulation**: accurate signal-level simulation of RTL with embedded software running on a processor model. It is accurate but slow.
2. **Instruction-Set Simulation (ISS)**: simulates the processor instruction behavior faster than full RTL, useful for software execution and early debug.
3. **Virtual platform**: high-level model of the SoC used to run firmware before RTL is complete.
4. **Hardware emulation**: maps RTL to an emulator so larger software workloads can run faster than RTL simulation.
5. **FPGA prototyping**: maps the SoC or subsystem to FPGA hardware to run long software tests at higher speed.
6. **Co-simulation**: combines software models, processor models, RTL blocks and testbench components in one verification setup.

The deeper the platform, the more hardware-accurate it is. The higher-level the platform, the faster it is for software. A good SoC project often uses more than one.

#### 1. Boot Sequence

The **boot sequence** is the ordered startup process after reset. It normally includes reset release, fetching the reset vector, setting stack pointer, running boot ROM, initializing clocks, configuring memory, loading firmware and jumping to application code.

What must be verified:

- processor starts from the correct reset address,
- boot ROM is correctly mapped,
- stack pointer and vector table are initialized,
- clocks and PLLs are configured in the correct order,
- memories are initialized before use,
- firmware image is loaded from the correct boot source,
- secure boot or authentication works if present,
- boot failure paths are handled correctly.

Technical example: If the boot ROM expects the firmware image in Flash address range `0x00000000` but the SoC address decoder maps Flash somewhere else, the processor may fetch wrong instructions and the chip will not boot.

Exam line: **Boot-sequence co-verification checks whether reset, vector table, boot ROM, memory initialization, clock setup and firmware loading occur in the correct order.**

#### 2. Firmware Register Programming

Most SoC hardware blocks are controlled through **memory-mapped registers**. Firmware writes control registers, reads status registers and clears interrupt/error flags. This is called register programming.

What must be verified:

- reset values of registers are correct,
- read-only, write-only and read-write permissions are correct,
- write-one-to-clear and read-to-clear bits behave correctly,
- reserved bits do not cause unexpected behavior,
- software writes registers in the required order,
- hardware updates status bits correctly,
- register side effects match documentation,
- register access width and alignment are handled correctly.

Technical example: A status bit may be **write-one-to-clear**. If firmware writes `0` expecting to clear it, the interrupt may remain pending forever. The hardware is not necessarily wrong; the software assumption is wrong. Co-verification catches this mismatch.

Exam line: **Firmware register programming verification checks whether software-visible control, status, interrupt and error registers behave exactly as firmware expects.**

#### 3. Device Drivers

A **device driver** is software that controls a hardware peripheral. It hides low-level register operations behind higher-level functions. For example, a UART driver may provide `uart_send()` and `uart_receive()` functions while internally programming baud rate, FIFO, interrupt enable and status registers.

What must be verified:

- driver writes correct register values,
- driver waits for correct status bits,
- driver handles busy, timeout and error states,
- driver does not access hardware before clocks/reset are ready,
- driver handles interrupt or polling mode correctly,
- driver supports correct data width, endian format and alignment,
- driver works with actual hardware timing.

Technical example: A UART RTL block may be correct, but the driver may read the receive register before checking the "data available" bit. In simulation, this may return invalid data. That is a driver/hardware integration bug.

Exam line: **Device-driver co-verification checks whether software controls peripherals correctly through registers, status bits, interrupts, timeouts and error paths.**

#### 4. Interrupt Service Routines

An **ISR - Interrupt Service Routine** is the software function executed when an interrupt occurs. Hardware raises an interrupt request, the interrupt controller prioritizes it, the processor jumps to the ISR, the ISR services the event and then normal software resumes.

What must be verified:

- interrupt is connected to the correct interrupt-controller input,
- interrupt enable/mask bits work,
- vector table points to the correct ISR,
- interrupt priority and nesting are correct,
- interrupt pending/clear behavior is correct,
- ISR clears the hardware source properly,
- ISR does not lose events during back-to-back interrupts,
- interrupt latency is acceptable,
- spurious interrupts are handled safely.

Technical example: If a DMA completion interrupt is level-sensitive and firmware clears the interrupt controller bit but does not clear the DMA status bit, the interrupt may immediately re-trigger. This is a classic hardware/software interrupt bug.

Exam line: **ISR co-verification checks interrupt connection, masking, priority, vector-table entry, service routine execution, clearing behavior and interrupt latency.**

#### 5. DMA Setup By Software

**DMA - Direct Memory Access** allows data transfer between memory and peripherals without the CPU copying every word. Firmware usually configures source address, destination address, transfer length, burst size, direction, permissions and interrupt-on-completion.

What must be verified:

- source and destination addresses are programmed correctly,
- transfer length and burst size are legal,
- address alignment rules are respected,
- DMA starts only after descriptors are complete,
- cache coherency is handled if CPU cache is present,
- memory protection and privilege rules are obeyed,
- completion interrupt is generated,
- error interrupt is generated for illegal access,
- abort, pause and resume behavior work.

Technical example: If CPU cache contains dirty data and DMA reads from memory before cache is cleaned, DMA may read stale data. The hardware and software must agree on cache maintenance rules.

Exam line: **DMA co-verification checks whether firmware correctly programs DMA descriptors, addresses, lengths, cache maintenance, completion interrupts and error handling.**

#### 6. RTOS Scheduling Interactions

An **RTOS - Real-Time Operating System** schedules multiple tasks and handles timing, synchronization and interrupts. In an RTOS-based SoC, a hardware event may wake a task, trigger an ISR, release a semaphore or cause a context switch.

What must be verified:

- high-priority tasks run when hardware events occur,
- ISRs interact correctly with RTOS APIs,
- semaphores, queues and mutexes are used correctly,
- context switches do not corrupt hardware state,
- deadlines are met,
- low-priority tasks do not block critical hardware service,
- tick interrupt and timer behavior are correct,
- tickless idle or low-power scheduling works if enabled.

Technical example: A driver ISR may give a semaphore to wake a task waiting for DMA completion. If the ISR uses the wrong RTOS API or interrupt priority is invalid for the RTOS rules, the task may never wake or the kernel may behave incorrectly.

Exam line: **RTOS co-verification checks task scheduling, interrupt-to-task handoff, synchronization objects, context switches and timing deadlines under real hardware events.**

#### 7. Memory Map Access From Software

The **memory map** defines where each memory, peripheral and register block appears in the processor address space. Software depends completely on this map.

What must be verified:

- every peripheral appears at the correct base address,
- address decoder selects the correct slave,
- unmapped addresses return correct error response,
- secure/non-secure regions are protected if security is present,
- user/supervisor privilege rules are enforced,
- access width and alignment are handled,
- endian behavior is correct,
- memory attributes such as cacheable, bufferable and device memory are correct.

Technical example: If firmware writes to the timer base address but the interconnect decodes that address to the UART block, software may configure the wrong device. This may not be caught in block-level verification because each block was correct alone.

Exam line: **Memory-map co-verification checks whether software-visible addresses, permissions, attributes and error responses match the SoC specification.**

#### 8. Exception And Error Handling

An **exception** is an event that changes normal program flow. It may be caused by interrupt, bus fault, illegal instruction, memory protection violation, divide-by-zero, privilege violation or system call. Error handling is the hardware/software response to such abnormal conditions.

What must be verified:

- bus errors are reported to the processor correctly,
- illegal accesses generate correct faults,
- error status registers are updated,
- firmware reads and clears error information correctly,
- fatal and recoverable errors are distinguished,
- exception vectors point to correct handlers,
- nested exceptions are handled safely,
- system can recover or enter safe state.

Technical example: If software accesses a protected memory region, the SoC should raise a memory-management fault or bus fault, not silently corrupt memory. The exception handler should record the fault and take the correct recovery action.

Exam line: **Exception and error co-verification checks whether hardware faults, bus errors, illegal accesses and software handlers interact correctly.**

#### 9. Low-Power Entry And Exit Controlled By Firmware

Low-power modes are usually entered by firmware writing PMU control registers. The **PMU - Power Management Unit** then sequences clock gating, isolation, retention, power switches, reset and wake-up logic.

What must be verified:

- firmware waits until transactions are idle before low-power entry,
- clocks are gated only after safe conditions,
- retention registers preserve required state,
- isolation is enabled before power-off,
- wake-up sources are enabled correctly,
- exit latency is acceptable,
- firmware restores clocks, memory and devices correctly,
- interrupts during sleep are not lost,
- RTOS tick/time is corrected if tickless idle is used.

Technical example: If firmware enters sleep while DMA is still writing memory, data may be partially written. Co-verification checks whether firmware, PMU and DMA status logic prevent this unsafe transition.

Exam line: **Low-power co-verification checks firmware-controlled power entry/exit, PMU sequencing, retention, isolation, wake-up events and pending transaction safety.**

#### 10. Hardware Accelerator Use By Software

A **hardware accelerator** is a specialized block used to perform a task faster than software, such as encryption, image processing, compression, AI inference or signal processing. Software usually configures the accelerator, provides input/output buffer addresses, starts execution, waits for completion and handles errors.

What must be verified:

- software programs accelerator registers correctly,
- input and output buffers are mapped correctly,
- cache coherency is handled,
- accelerator starts only after valid configuration,
- completion interrupt or status bit is correct,
- output data matches the golden reference model,
- error cases such as invalid descriptor or unsupported size are handled,
- multiple accelerator jobs are queued or rejected correctly.

Technical example: For an encryption accelerator, software writes key address, plaintext address, ciphertext address and start bit. Co-verification checks whether the hardware reads the correct buffers, produces the expected ciphertext and raises completion interrupt correctly.

Exam line: **Accelerator co-verification checks whether software correctly configures, starts, synchronizes with and validates specialized hardware blocks.**

#### Why This Stage Is Important

Hardware/software co-verification is important because many SoC bugs are not visible in pure block-level RTL simulation. They appear only when real software sequences interact with real hardware behavior.

Common bug types found here:

- wrong register programming order,
- incorrect reset or boot assumptions,
- wrong interrupt priority or clear sequence,
- stale cache data during DMA,
- invalid memory map or permission,
- driver timeout due to hardware latency,
- lost wake-up event during low-power mode,
- accelerator started before buffers are ready.

This stage may be done using RTL simulation, instruction-set simulation, virtual platforms, emulation or FPGA prototyping. RTL simulation is accurate but slow. Emulation and prototyping are faster and can run more realistic software. A good answer should mention both because SoC software may be too large to verify only with slow RTL simulation.

Example: A UART may pass block verification, but the driver may fail if the status bit clears on read and the software expects it to clear on write. This is a hardware/software integration bug, not a pure RTL bug.

Exam line: **Hardware/software co-verification verifies the interaction between RTL hardware and embedded software, including boot, register programming, drivers, interrupts, DMA, RTOS behavior, memory map, exceptions, low-power control and accelerator use.**

### Step 8: Full-Chip SoC Verification

Full-chip verification checks the **complete integrated SoC** after all major IP blocks, interconnects, memories, clock/reset logic, power-management logic, debug logic and software-visible interfaces have been connected. At this level, the purpose is not to repeat every detailed block-level test. The purpose is to verify system-level behavior that appears only when the complete chip is assembled.

Simple meaning:

```text
Full-chip verification = verify that the whole SoC works as one integrated system
```

This stage checks whether the individually verified blocks still work correctly when they share clocks, resets, buses, memory, interrupts, power domains, debug access and firmware control.

#### Why Full-Chip Verification Is Different From Block Verification

At block level, the testbench directly controls one IP. At full-chip level, many blocks are controlled indirectly through the processor, firmware, interconnect, interrupts and top-level registers. Bugs are harder to debug because the failure may be caused by interaction, not by one block alone.

Example:

- The UART block may be correct.
- The interrupt controller may be correct.
- The processor may be correct.
- But at full-chip level, the UART interrupt may be connected to the wrong interrupt line, so software never receives the UART interrupt.

That is a full-chip integration bug.

#### How Full-Chip Verification Is Performed

Full-chip verification commonly uses:

1. **Full-chip RTL simulation** for selected high-value scenarios.
2. **UVM/VVM system testbench** with active and passive agents.
3. **Firmware-driven tests** where software running on the processor accesses real SoC registers.
4. **Assertions and protocol checkers** on major interfaces.
5. **Passive monitors** on internal buses, interrupts, clocks, reset and power signals.
6. **Emulation or FPGA prototyping** for long software workloads.
7. **Coverage collection** for top-level scenarios such as boot, reset, interrupts, power modes and memory-map access.

The full-chip environment may use a mix of active and passive agents. Some interfaces are driven by testbench components, while others are only monitored because they are driven internally by CPU, DMA, GPU or firmware.

#### 1. Top-Level Reset And Boot

Top-level reset and boot verification checks whether the entire SoC starts correctly from a known state.

What must be verified:

- all reset sources work, such as power-on reset, warm reset, watchdog reset and software reset,
- reset is distributed to all blocks correctly,
- reset deassertion order is safe across clock and power domains,
- processor starts from the correct reset vector,
- boot ROM is mapped correctly,
- clocks are available before CPU/peripherals use them,
- memories are initialized before code/data access,
- boot firmware executes and reaches the expected checkpoint,
- reset during an active transaction does not leave the SoC stuck.

Technical example: If reset is released to the CPU before the memory subsystem is ready, the CPU may fetch invalid instructions. This may not appear at block level because CPU and memory were verified separately.

Exam line: **Top-level reset and boot verification checks whether the complete SoC enters a known state, releases reset safely and executes the boot sequence correctly.**

#### 2. Clock Generation And Clock Gating

Clock generation verifies PLLs, oscillators, clock dividers, clock muxes and generated clocks. Clock gating verifies whether clocks are stopped safely for inactive blocks to save power.

What must be verified:

- correct clock source is selected,
- PLL lock or clock-ready status is handled before use,
- clock frequencies and dividers are programmed correctly,
- clock mux switching does not glitch,
- clock gating does not stop an active transfer,
- gated clocks restart correctly,
- clock-domain crossings are synchronized,
- firmware cannot accidentally disable a clock needed by an active block.

Technical example: A peripheral may be accessible only when its bus clock is enabled. If firmware reads the peripheral while its clock is gated, the bus may hang or return an error. Full-chip verification checks this with real register accesses.

Exam line: **Clock verification checks clock generation, clock selection, gating, restart and safe clock-domain interaction across the complete SoC.**

#### 3. Power Modes And Wake-Up Paths

Full-chip power verification checks whether the SoC can enter and exit low-power modes safely. This includes active, idle, sleep, retention, power-gated and deep-sleep states.

What must be verified:

- PMU control registers are accessible,
- firmware can request power-mode transitions,
- isolation is enabled before a power domain turns off,
- retained state is preserved,
- non-retained state is reset or reinitialized,
- wake-up sources are connected correctly,
- wake-up interrupt reaches the processor,
- clocks and resets are restored in the correct order,
- pending transactions are completed or safely paused before power-down,
- exit latency meets requirement.

Technical example: The SoC may enter deep sleep with only the RTC or GPIO wake-up logic alive. Full-chip verification checks whether a GPIO wake-up event powers the required domain, restores clocks, releases reset and resumes firmware.

Exam line: **Power-mode verification checks PMU sequencing, isolation, retention, wake-up sources, clock/reset restoration and safe low-power entry/exit at full-chip level.**

#### 4. Full Memory Map

The full memory map defines the address locations of ROM, RAM, Flash, DRAM, peripherals, debug blocks and reserved regions. Software depends on this map.

What must be verified:

- every memory and peripheral appears at the correct base address,
- address ranges do not overlap incorrectly,
- unmapped regions return the correct error response,
- byte/halfword/word accesses behave correctly,
- endian behavior is correct,
- memory attributes such as device, cacheable and bufferable are correct,
- secure/non-secure and privilege permissions are applied if present,
- register reset values match the specification.

Technical example: If the timer register block is accidentally decoded at the UART address range, both timer and UART may pass block-level verification, but full-chip software will configure the wrong hardware.

Exam line: **Full memory-map verification checks top-level address decoding, register visibility, access permissions, error responses and software-visible address correctness.**

#### 5. Processor Access To All Peripherals

At full-chip level, the processor must be able to access every software-visible peripheral through the interconnect.

What must be verified:

- CPU can read/write all peripheral registers,
- access permissions are correct,
- register side effects are correct,
- bus responses are correct,
- accesses work through bridges such as AXI-to-APB or AHB-to-APB,
- timeout or error response occurs for invalid access,
- firmware can configure each peripheral through its driver,
- endianness and alignment are correct.

Technical example: A peripheral may be correct on its own APB interface, but an AXI-to-APB bridge may incorrectly translate write strobes. Full-chip verification catches this when CPU writes through the real bus path.

Exam line: **Processor-peripheral verification checks whether CPU firmware can correctly access and control every peripheral through the real SoC interconnect.**

#### 6. Interrupt Routing From All Sources

Interrupt routing checks whether interrupts from all IP blocks reach the interrupt controller and processor correctly.

What must be verified:

- every interrupt source is connected to the correct interrupt-controller input,
- interrupt polarity and sensitivity are correct,
- level-triggered and edge-triggered behavior is correct,
- interrupt masks and enables work,
- interrupt priorities are correct,
- interrupt clear sequence works,
- simultaneous interrupts are prioritized correctly,
- wake-up interrupts work during low-power states,
- software vector table and ISR mapping are correct.

Technical example: If DMA completion interrupt is connected to interrupt line 18 but firmware expects line 19, the DMA may complete but software will never run the correct ISR.

Exam line: **Full-chip interrupt verification checks routing, priority, masking, clearing, vectoring and wake-up behavior for all interrupt sources.**

#### 7. Debug And JTAG Access

Debug access allows engineers to halt processors, inspect registers, read/write memory, set breakpoints and trace execution. JTAG or similar debug interfaces provide external access to internal debug infrastructure.

What must be verified:

- debug port or JTAG TAP is connected correctly,
- debug access can halt and resume the processor,
- memory and register access through debug works,
- breakpoints and watchpoints work if supported,
- debug access respects security and lock settings,
- debug remains usable after reset,
- debug access does not corrupt normal operation,
- multi-core debug selects the correct core,
- trace or timestamp features work if present.

Technical example: The chip may boot normally, but if JTAG debug cannot access the CPU after reset, post-silicon bring-up becomes difficult. Full-chip verification checks that debug paths are connected and authorized correctly.

Exam line: **Debug/JTAG verification checks external debug access, halt/resume, memory/register access, breakpoints, trace and security restrictions at chip level.**

#### 8. System Bus And NoC Traffic

The system bus or **NoC - Network on Chip** connects processors, DMA, accelerators, memories and peripherals. Common SoC protocols include AMBA AXI, AHB, APB, ACE, CHI or vendor-specific NoCs.

What must be verified:

- masters and slaves are connected correctly,
- address decoding selects the correct target,
- arbitration works under multiple requests,
- protocol rules are not violated,
- ordering requirements are preserved,
- outstanding transactions are handled correctly,
- deadlock and livelock do not occur,
- bridges between protocols work correctly,
- backpressure and flow control work,
- error responses propagate correctly.

Technical example: CPU, DMA and accelerator may all issue AXI transactions at the same time. Full-chip verification checks whether the interconnect arbitrates them correctly and whether responses return to the correct master ID.

Exam line: **Bus/NoC verification checks full-chip connectivity, arbitration, protocol correctness, ordering, response routing, backpressure and deadlock freedom.**

#### 9. Multi-Master Contention

Multi-master contention occurs when several bus masters request shared resources at the same time. Examples of masters are CPU, GPU, DMA, display controller, camera interface, DSP, AI accelerator and debug unit.

What must be verified:

- arbitration gives access to one master at a time,
- high-priority traffic receives required service,
- low-priority traffic is not starved,
- memory bandwidth is sufficient,
- QoS settings work,
- cache coherency rules are preserved if coherent masters exist,
- shared-memory data is not corrupted,
- write/read ordering rules are maintained.

Technical example: A display controller may need regular memory bandwidth. If a DMA engine and CPU traffic starve display fetches, the screen may underflow. Full-chip verification must check this contention behavior.

Exam line: **Multi-master contention verification checks arbitration, QoS, fairness, memory bandwidth and shared-resource behavior when many SoC masters operate simultaneously.**

#### 10. Error Handling At Chip Level

Chip-level error handling checks how the SoC responds to faults that cross block boundaries.

What must be verified:

- invalid address access returns correct bus error,
- ECC or parity errors are reported,
- memory protection violations raise correct exceptions,
- timeout errors are detected,
- error status registers update correctly,
- error interrupts reach the processor,
- software can clear or log the error,
- fatal errors move the SoC to a safe state,
- watchdog reset works if system hangs.

Technical example: If a bus slave does not respond, the interconnect may generate a timeout. Full-chip verification checks whether that timeout becomes a bus error, whether the CPU receives the correct exception and whether firmware can recover.

Exam line: **Chip-level error handling verification checks fault detection, error propagation, exception generation, status reporting, interrupting and safe recovery.**

#### 11. Security Or Privilege Access If Present

Many SoCs include security or privilege mechanisms. These may separate secure and non-secure worlds, user and supervisor privilege, trusted and untrusted masters, or protected memory regions.

What must be verified:

- secure registers are inaccessible from non-secure software,
- user-mode software cannot access privileged registers,
- memory protection or firewall rules work,
- debug access is locked when required,
- secure boot configuration is enforced if present,
- illegal access returns correct error or exception,
- DMA and accelerators obey security attributes,
- privilege transitions are controlled.

Technical example: If non-secure software can write a secure key register because an interconnect protection bit is wrong, the chip has a serious security bug. Full-chip verification checks access from real masters through real paths.

Exam line: **Security/privilege verification checks whether protected memories, registers, debug paths and masters obey secure/non-secure and privilege access rules.**

#### 12. Real Application Scenarios

Real application scenarios verify end-to-end SoC use cases instead of isolated features. These tests represent how the chip will actually be used.

Examples:

- boot firmware and configure all clocks,
- receive data from sensor,
- DMA data into memory,
- accelerator processes data,
- CPU handles interrupt,
- result is transmitted through communication interface,
- system enters sleep and wakes on event.

What must be verified:

- end-to-end data path is correct,
- software and hardware synchronize correctly,
- timing and performance are acceptable,
- interrupts and DMA work during real use,
- memory and cache behavior are correct,
- power transitions do not break the use case,
- errors are handled without system deadlock.

Technical example: In a camera SoC, a real scenario may involve camera input, DMA, image-processing accelerator, memory controller, display output and CPU control. Each block may pass alone, but full-chip verification proves the full pipeline works.

Exam line: **Real-application scenario verification checks complete end-to-end SoC behavior under realistic software, traffic, interrupts, memory usage and power conditions.**

#### Why Full-Chip Verification Must Be Selective

Full-chip verification is expensive and slow. It should not repeat every block-level corner case. Detailed protocol corner cases belong mostly at IP/subsystem level. Full-chip verification should focus on:

- boot,
- connectivity,
- reset/clock/power integration,
- interrupt routing,
- memory map,
- processor access,
- shared-resource contention,
- debug access,
- top-level error handling,
- realistic end-to-end use cases.

Exam line: **Full-chip verification focuses on integration and system behavior, not exhaustive re-testing of every IP block.**

### Step 9: Coverage Closure And Regression Testing

After many tests are run, the team studies coverage reports. **Coverage closure** means reaching the planned functional and code coverage goals. It does not mean blindly reaching 100% everywhere. It means all meaningful planned features, corner cases and RTL structures have been exercised or intentionally waived with justification.

If coverage is low, the team asks:

- Is the test missing?
- Is the constraint too tight?
- Is the coverage point wrong?
- Is the RTL unreachable?
- Is the specification unclear?
- Is there a real design bug?

Regression testing means rerunning a selected test suite automatically after changes. This is critical because fixing one bug can break another feature. A regression suite usually includes smoke tests, directed tests, random tests, protocol tests, software tests and previously failing tests.

Important exam line: **Coverage tells what has been tested; regression tells whether old working behavior remains working after changes.**

### Step 10: Gate-Level, Timing And Equivalence Verification

After RTL verification, the design is synthesized into a **gate-level netlist**. RTL describes behavior using registers, combinational logic and high-level constructs. Synthesis converts that RTL into actual standard cells such as AND, OR, NAND, NOR, flip-flops, multiplexers and buffers.

At this point, the verification question changes:

```text
RTL was functionally correct, but did synthesis, timing, reset, CDC/RDC or gate-level effects change anything?
```

So Step 10 checks that the post-synthesis design still behaves like the verified RTL and can physically meet timing.

#### Why This Stage Is Needed

RTL simulation assumes idealized behavior. It does not fully represent:

- real gate delays,
- setup and hold timing,
- clock skew,
- reset release timing,
- unknown X values from uninitialized flops,
- synthesis optimizations,
- clock-domain crossing risks,
- reset-domain crossing risks,
- timing exceptions and false paths,
- scan/DFT insertion effects if already added.

Therefore, even after RTL verification passes, the design must still go through lint, CDC/RDC, equivalence, timing and selected gate-level checks.

#### 1. Lint Checks

**Lint checks** are static checks on RTL code. They find coding, structural and style issues before synthesis or sign-off.

Lint does not run simulation. It analyzes the code and warns about risky constructs.

What lint checks can find:

- undeclared or unused signals,
- width mismatch,
- incomplete `case` statements,
- inferred latches,
- multiple drivers on the same signal,
- unreachable code,
- unconnected ports,
- combinational loops,
- blocking/nonblocking assignment misuse,
- reset not used consistently,
- unsynthesizable or tool-dependent coding.

Technical example: If an `if` statement in combinational logic does not assign an output in every path, synthesis may infer a latch. The RTL may appear to work in simple simulation, but the latch can create timing and functional problems. Lint flags this early.

Exam line: **Lint checks statically analyze RTL to find coding and structural problems such as inferred latches, width mismatches, multiple drivers, unconnected signals and unreachable logic.**

#### 2. CDC Checks - Clock Domain Crossing

**CDC** means **Clock Domain Crossing**. A CDC occurs when a signal moves from one clock domain to another. For example, data may move from a CPU clock domain to a peripheral clock domain.

CDC is dangerous because the receiving flip-flop may sample a signal while it is changing, causing metastability or incorrect sampling.

What CDC verification checks:

- signals crossing between asynchronous clocks,
- missing synchronizers,
- single-bit control synchronizers,
- multi-bit data crossing safety,
- asynchronous FIFO correctness,
- handshake synchronizer correctness,
- reconvergence of separately synchronized signals,
- clock-gating and generated-clock assumptions,
- false CDC waivers.

Common CDC structures:

- two-flop synchronizer for single-bit control,
- asynchronous FIFO for multi-bit data,
- valid/ready handshake for control transfer,
- gray-coded pointers for FIFO crossings.

Technical example: A one-cycle pulse generated in a fast clock domain may be missed by a slower clock domain. CDC verification checks whether the design uses a pulse synchronizer or handshake instead of directly sampling the pulse.

Exam line: **CDC checks verify that signals crossing between different clock domains use safe synchronizers, FIFOs or handshakes so metastability and data corruption are avoided.**

#### 3. RDC Checks - Reset Domain Crossing

**RDC** means **Reset Domain Crossing**. An RDC problem occurs when signals pass between logic controlled by different reset signals, different reset release timings or different reset polarities.

RDC is similar to CDC in risk because reset release can create unsafe transitions. A block may start operating while another block is still in reset, causing corrupted control signals or invalid data.

What RDC verification checks:

- signals crossing between different reset domains,
- reset release order,
- asynchronous reset deassertion safety,
- reset synchronizers,
- reset polarity mismatches,
- partial reset conditions,
- reset crossing into active logic,
- data/control corruption during reset transitions.

Technical example: A control signal from Block A may drive Block B. If Block A comes out of reset earlier than Block B, Block B may sample an invalid transition during reset release. RDC tools detect such unsafe reset-domain paths.

Exam line: **RDC checks verify that signals crossing between different reset domains or reset-release timings do not cause data loss, control corruption or unsafe startup behavior.**

#### 4. Formal Equivalence Checking

**Formal equivalence checking** proves that two versions of the design are functionally equivalent. In this step, it usually compares:

```text
RTL design  <->  synthesized gate-level netlist
```

The purpose is to prove that synthesis did not change the intended logic function.

What equivalence checking verifies:

- optimized gate netlist matches RTL behavior,
- state elements correspond correctly,
- synthesis did not remove required logic,
- constant propagation did not alter behavior incorrectly,
- retiming or optimization is functionally safe,
- ECO changes preserve intended behavior.

This is different from simulation. Simulation checks selected input scenarios. Formal equivalence uses mathematical proof to compare the logic more exhaustively.

Technical example: A synthesis tool may optimize a logic cone because it thinks a condition is constant. If that assumption is wrong due to incorrect constraints, equivalence checking can show a mismatch between RTL and netlist.

Exam line: **Formal equivalence checking mathematically proves that the synthesized gate-level netlist is functionally equivalent to the verified RTL.**

#### 5. Static Timing Analysis

**Static Timing Analysis (STA)** checks whether the design meets timing without simulating every input combination. It analyzes timing paths using cell delays, wire delays, clock constraints and timing libraries.

STA mainly checks:

- **setup time**: data arrives early enough before the capturing clock edge,
- **hold time**: data remains stable long enough after the capturing clock edge,
- clock skew,
- clock uncertainty,
- input and output delays,
- generated clocks,
- multi-cycle paths,
- false paths,
- maximum delay paths,
- minimum delay paths.

Simple meaning:

```text
Setup check = data should not arrive too late
Hold check  = data should not change too early
```

What STA finds:

- paths too slow for the target clock frequency,
- paths too fast that violate hold time,
- missing or wrong clock constraints,
- incorrect timing exceptions,
- unsafe paths between clocks if not properly constrained.

Technical example: If a register-to-register path has too much combinational logic, data may not reach the next register before the next clock edge. STA reports a setup violation. The fix may require logic optimization, pipelining, clock adjustment or placement/routing improvement.

Exam line: **Static timing analysis checks setup and hold timing over all timing paths using constraints and timing libraries, without exhaustive simulation.**

#### 6. Gate-Level Simulation

**Gate-level simulation (GLS)** runs simulation on the synthesized or placed-and-routed gate-level netlist instead of RTL. It may use delay annotation such as **SDF - Standard Delay Format** to include estimated or extracted timing delays.

Gate-level simulation is used selectively because it is much slower than RTL simulation.

What GLS checks:

- reset and initialization behavior,
- X-propagation issues,
- gate-level timing behavior in selected tests,
- clock/reset startup sequence,
- scan or test-mode behavior if included,
- power-up behavior,
- simulation mismatch between RTL and netlist,
- timing-annotated behavior for critical scenarios.

Technical example: RTL simulation may initialize a register to a known value in a testbench, but in the real gate-level netlist that register may power up as unknown unless reset. Gate-level simulation can reveal this X-value issue.

Exam line: **Gate-level simulation runs selected tests on the synthesized netlist, often with delay annotation, to catch reset, initialization, X-propagation and timing-related issues that RTL simulation may hide.**

#### 7. X-Propagation Checks

In digital simulation, **X** means unknown value. X can come from uninitialized registers, incomplete reset, bus contention, undriven signals, power-off domains or conflicting drivers.

X-propagation checks verify whether unknown values can spread through the design and affect outputs, control logic or software-visible behavior.

What X-propagation checks find:

- unreset flip-flops used before initialization,
- missing reset on control registers,
- uninitialized memory reads,
- bus contention,
- power-domain off signals entering active logic,
- incomplete `case` or `if` assignments,
- RTL simulation hiding X because of optimistic behavior,
- gate-level simulation revealing unknown values.

Technical example: A state machine register may not be reset. RTL simulation may accidentally start it in a convenient value, but gate-level simulation may show `X`, causing the FSM to enter an illegal state. X-propagation analysis detects this risk.

Exam line: **X-propagation checks detect unknown values caused by uninitialized logic, missing reset, power-off domains or bus contention, and verify that these X values do not corrupt functional behavior.**

#### How These Checks Work Together

These checks are complementary:

| Check | Main purpose | Main question |
|---|---|---|
| Lint | RTL quality | Is the RTL coded safely? |
| CDC | Clock crossing safety | Are clock-domain crossings synchronized? |
| RDC | Reset crossing safety | Are reset-domain crossings safe? |
| Formal equivalence | RTL vs netlist correctness | Did synthesis preserve function? |
| STA | Timing correctness | Are setup and hold constraints met? |
| Gate-level simulation | Netlist behavior | Does selected netlist simulation behave correctly? |
| X-propagation | Unknown-value safety | Can X values corrupt behavior? |

#### Why Gate-Level Simulation Is Selective

Gate-level simulation is very slow compared to RTL simulation. Full regression at gate level is usually impractical. Therefore, teams run selected high-value tests:

- reset and boot test,
- basic firmware test,
- scan/test mode smoke test,
- clock and reset sequence test,
- low-power wake-up test,
- representative full-chip scenario,
- tests that previously exposed X or timing issues.

Static timing analysis and formal equivalence checking reduce the need for massive gate-level simulation, but they do not eliminate it completely.

Exam line: **Step 10 ensures that the verified RTL remains correct after synthesis and physical implementation by checking RTL quality, CDC/RDC safety, equivalence, timing, gate-level behavior and X-propagation.**

### Step 11: DFT Readiness, Test Integration And Sign-Off

Verification flow finally connects to testing. The design must be prepared for manufacturing test using DFT features such as scan chains, memory BIST, logic BIST, test wrappers and test access mechanisms.

At this stage, the team checks:

- Scan chains are inserted and connected correctly.
- Memories have BIST or suitable test access.
- Test modes are controllable.
- JTAG or other test interface works.
- DFT logic does not disturb normal functional behavior.
- Test patterns can be generated.
- Test power constraints are considered.
- Core-level tests are integrated into SoC-level testing.

**Verification sign-off** means the design has met its planned verification exit criteria. It usually includes passing regressions, closed or justified coverage, no critical open bugs, clean protocol assertions, acceptable lint/CDC/RDC results, equivalence passing, timing clean or timing exceptions justified, and DFT readiness.

### Feedback Loop In Verification Flow

The SoC verification flow is not purely linear. Every stage can create feedback.

Examples:

- If a test fails, RTL may need correction.
- If coverage is missing, new tests or constraints may be added.
- If the scoreboard disagrees with RTL, the reference model or specification may need review.
- If a subsystem fails, an interface assumption may need correction.
- If software fails, the register map or driver sequence may need correction.
- If timing fails, RTL or constraints may need modification.

This feedback loop is important. In the exam, write: **A practical SoC verification flow is iterative because bugs, coverage holes and specification ambiguities are fed back into design, model, testbench and verification plan updates.**

<a id="topic-2-final-answer"></a>

### Final Exam-Ready Answer

SoC verification flow is the systematic process used to prove that a system-on-chip implementation satisfies its specification before fabrication. It starts from the SoC requirements and continues through verification planning, executable modeling, testbench creation, block-level verification, subsystem verification, hardware/software co-verification, full-chip verification, coverage closure, regression testing, gate-level checks, DFT readiness and final sign-off.

The first step is requirement and specification analysis. The verification team studies the SoC functions, interfaces, memory map, register map, clock and reset behavior, power modes, interrupt behavior, performance requirements and software-visible behavior. From this, a verification plan is prepared. The verification plan maps each specification feature to tests, assertions, coverage points, reference models and sign-off criteria. A coverage plan is also created so that the team can measure whether important scenarios have actually been exercised.

Next, an executable model or golden reference model is developed. This model represents the expected behavior of the design and is used by the scoreboard to compare expected and actual outputs. A reusable verification environment is then built using testbenches, bus functional models, agents, drivers, monitors, scoreboards, assertions and coverage collectors. This environment may follow OVM/UVM in SystemVerilog or VVM/UVVM/OSVVM in VHDL.

The design is then verified in layers. At IP or block level, each core is verified for reset behavior, register access, legal and illegal commands, protocol correctness, boundary conditions, interrupts and error handling. At subsystem level, related blocks are integrated and verified together, such as processor-memory, DMA-memory, bus-interconnect or peripheral subsystems. This stage checks arbitration, address decoding, interrupt routing, shared-memory behavior, clock-domain crossing, reset sequencing and performance under traffic.

After this, hardware/software co-verification is performed because the final SoC behavior depends on firmware and drivers as well as RTL. Boot code, register programming, interrupt service routines, DMA setup, low-power entry/exit and device-driver behavior are verified using simulation, emulation, virtual platforms or FPGA prototypes. Full-chip verification then checks complete SoC behavior such as boot, reset, clocks, power modes, memory map, processor access to peripherals, debug access, interrupt routing and end-to-end application scenarios.

Finally, coverage closure and regression testing are done. Functional coverage checks whether planned features and corner cases have been exercised, while code coverage checks RTL execution. Regression testing ensures that bug fixes do not break previously working behavior. After RTL verification, gate-level verification, formal equivalence checking, static timing analysis, CDC/RDC checks and selected gate-level simulations are performed. The flow ends with DFT readiness, test integration and verification sign-off. Therefore, SoC verification flow is an iterative, coverage-driven and layered process that gives confidence that the SoC is functionally correct and ready for manufacturing test.

<a id="topic-2-technical-words"></a>

### Technical Words To Use For Marks

- **SoC verification flow** (write this because the question is asking for the ordered process, not only definitions.)
- **Requirements analysis** (write this because verification always starts from what the design is supposed to do.)
- **Design specification** (write this because verification proves conformance to specification.)
- **Verification plan** (write this because it shows planned, systematic verification.)
- **Coverage plan** (write this because it shows how completion is measured.)
- **Executable specification** (write this because early high-level models help validate behavior before RTL is complete.)
- **Golden reference model** (write this because scoreboards need expected results.)
- **Virtual testbench** (write this because system-level behavior can be verified before final hardware exists.)
- **Reusable verification environment** (write this because SoC verification needs reuse across IP, subsystem and chip levels.)
- **BFM / Bus Functional Model** (write this because SoC interfaces are verified through protocol-level read/write transactions.)
- **Agent** (write this because it groups driver, monitor and sequencer for one interface.)
- **Monitor** (write this because observing internal and external interfaces is essential in subsystem and full-chip verification.)
- **Scoreboard** (write this because automated checking gives stronger verification than waveform inspection.)
- **Assertion-Based Verification** (write this because protocol rules and design properties must be checked automatically.)
- **Functional coverage** (write this because it proves planned scenarios were exercised.)
- **Code coverage** (write this because it proves RTL structures were executed.)
- **Coverage closure** (write this because it is a standard verification sign-off activity.)
- **Regression testing** (write this because design changes must not break already verified behavior.)
- **IP-level verification** (write this because each core must be verified before integration.)
- **Subsystem verification** (write this because many SoC bugs occur in interactions between verified blocks.)
- **Full-chip verification** (write this because final SoC integration must be checked as a whole.)
- **Hardware/software co-verification** (write this because SoC correctness depends on firmware and drivers.)
- **Emulation / FPGA prototyping** (write this because full software workloads may be too slow for RTL simulation.)
- **CDC - Clock Domain Crossing** (write this because SoCs usually contain multiple clocks.)
- **RDC - Reset Domain Crossing** (write this because reset sequencing bugs are common in SoCs.)
- **Formal equivalence checking** (write this because it proves synthesized netlist matches RTL.)
- **Static timing analysis** (write this because timing correctness is checked after synthesis and physical implementation.)
- **Gate-level simulation** (write this because selected post-synthesis tests verify gate-level behavior.)
- **DFT readiness** (write this because verification flow must connect to manufacturing test.)
- **Verification sign-off** (write this because it is the final exit point of the verification flow.)

<a id="topic-2-diagrams"></a>

### Images / Diagrams To Remember

1. **Main SoC verification flow diagram above**: Draw this whenever the question says "SoC verification flow".
2. **Course figure/source to look at**: [SOC Design Flow.pdf, p.4](<System on chip/SOC Design Flow.pdf#page=4>) and [SOC Design Flow.pdf, p.6](<System on chip/SOC Design Flow.pdf#page=6>). These slides are useful because they justify system-level models, verification environment, formal test plan and golden model.
3. **Stepwise refinement source to look at**: [Functional Architecture Co Design 2.pdf, p.12](<System on chip/Functional Architecture Co Design 2.pdf#page=12>) and [Functional Architecture Co Design 2.pdf, p.15](<System on chip/Functional Architecture Co Design 2.pdf#page=15>). These are useful because they support the idea that verification starts at high abstraction and then moves toward architecture and RTL.

---

<a id="topic-3"></a>

## Topic 3: SoC Test Scheduling and Test Integration

<a id="topic-3-question"></a>

### Question

**Explain SoC test scheduling and test integration in detail.**

### CLO Mapping

This topic belongs to **CLO 5: Discuss the SoC Design Verification strategies and Test Scheduling**.

Reason: **SoC Test Scheduling and Test Integration** is directly listed under the **SoC Verification and Testing** portion of the syllabus. It is the testing-side continuation of SoC verification flow. Verification proves the RTL/design behavior before fabrication; test integration and scheduling prepare the fabricated SoC for efficient manufacturing test.

### What The Question Is Asking

The examiner is asking how embedded cores inside a SoC are made testable and how their tests are organized to reduce test time and cost. Do not answer this as only "testing is done after fabrication". The answer must explain test wrappers, scan chains, BIST, test access mechanisms, test controller, ATE/JTAG interface, test constraints and scheduling.

For full marks, answer in this order:

1. Define SoC testing and distinguish it from verification.
2. Explain why SoC testing is difficult.
3. Explain SoC test integration.
4. Draw the SoC test architecture.
5. Explain SoC test scheduling.
6. Draw a scheduling diagram.
7. Explain constraints: power, **TAM - Test Access Mechanism** width, resource conflicts, precedence, thermal and test time.
8. End with the objective: minimum test application time with correct fault coverage and safe power.

<a id="topic-3-explanation"></a>

### Core Idea

**SoC test integration** means connecting the test structures of all embedded IP cores, memories, interconnects and chip-level logic into one complete chip-level test architecture.

**SoC test scheduling** means deciding when each core test will run, whether tests can run in parallel, and how test access resources are allocated so that total test application time is minimized without violating power, resource, precedence and test-access constraints.

In simple words:

- **Test integration** answers: *How do we access and test every embedded core inside the SoC?*
- **Test scheduling** answers: *In what order, and with what parallelism, should the core tests be applied?*

This topic is important because SoC testing directly affects manufacturing cost. The longer a chip stays on automatic test equipment, the higher the cost per chip. But running too many tests in parallel may exceed power or create conflicts. So the problem is an optimization problem.

### Verification Vs Testing

Verification and testing are related but not the same.

| Point | Verification | Testing |
|---|---|---|
| Main purpose | Check design correctness | Check manufactured chip correctness |
| Time | Before fabrication | After fabrication |
| Object checked | RTL, netlist, models, software behavior | Physical silicon |
| Main faults | Functional bugs, protocol bugs, integration bugs | Manufacturing defects such as stuck-at, bridging, delay, memory defects |
| Tools | Simulation, emulation, formal, UVM/VVM, assertions | ATE, ATPG, scan, BIST, JTAG, test controller |
| Output | Confidence that design matches specification | Pass/fail decision for fabricated chip |

Exam line: **Verification finds design bugs; testing finds manufacturing defects.**

### Why SoC Testing Is Difficult

SoC testing is harder than testing a small standalone chip because the cores are embedded inside one chip. External pins cannot directly access every internal signal, flip-flop, memory and IP block.

Major difficulties are:

1. **Limited controllability**: external tester cannot directly force values into internal nodes.
2. **Limited observability**: external tester cannot directly observe internal responses.
3. **Large test data volume**: many cores and memories require many test patterns.
4. **High test application time**: applying all tests serially would take too long.
5. **Power during test**: test mode can create more switching activity than normal operation.
6. **Resource conflicts**: multiple cores may need the same bus, memory, test clock or **TAM - Test Access Mechanism** wires.
7. **Heterogeneous IP**: hard, firm and soft cores may come from different vendors with different test requirements.
8. **Embedded memories**: SRAMs and ROMs need specialized memory test algorithms or BIST.
9. **Interconnect test**: buses, bridges and NoC links also need testing, not only cores.
10. **Test access routing**: adding test buses and wrappers increases area and routing overhead.

Therefore, SoC testing requires **DFT**, **test integration** and **test scheduling**.

### Figure 1: SoC Test Integration Architecture

Draw this figure when the question asks test integration.

```text
                    +----------------------+
                    | External Tester / ATE|
                    | or JTAG Interface    |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    | Chip Test Controller |
                    | test mode selection  |
                    +----------+-----------+
                               |
                               v
                    +----------------------+
                    | TAM / Test Access    |
                    | Mechanism / Test Bus |
                    +----+-----------+-----+
                         |           |
       +-----------------+           +------------------+
       |                                        |
       v                                        v
+--------------+                         +--------------+
| Core Wrapper |                         | Core Wrapper |
| scan access  |                         | scan access  |
+------+-------+                         +------+-------+
       |                                        |
       v                                        v
+--------------+                         +--------------+
| IP Core 1    |                         | IP Core 2    |
| Scan / BIST  |                         | Scan / BIST  |
+--------------+                         +--------------+

             +-------------------------------+
             | Memory BIST / Logic BIST /    |
             | Interconnect Test Structures  |
             +-------------------------------+
```

Figure source: look at [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.86](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=86>) for DFT and scan-chain context, and [SOC Design Flow.pdf, p.6](<System on chip/SOC Design Flow.pdf#page=6>) for the need to develop a DFT strategy. This figure is needed because it shows the four main test-integration parts: external tester, test controller, TAM and core wrappers.

### Components Of SoC Test Integration

### 1. External Tester / ATE

**ATE** means **Automatic Test Equipment**. It applies test patterns to the chip and observes output responses. ATE is expensive, so reducing test time reduces manufacturing cost.

ATE provides:

- Test patterns.
- Test clocks.
- Test control signals.
- Expected response comparison.
- Pass/fail decision.

However, ATE can only access chip pins. Since SoC cores are embedded, internal test access structures are needed.

This point is very important. **ATE is not inside the SoC.** ATE is a large external tester machine used in manufacturing. It sits outside the chip and connects to the chip package pins through a probe card, socket or tester interface. It can apply test patterns to external pins and measure responses from external pins.

But most SoC logic is not directly connected to external pins. A processor core, SRAM, DSP, accelerator, interconnect, cache, DMA controller or embedded peripheral is buried inside the chip. The ATE cannot directly touch every internal flip-flop, memory bit, bus signal or IP interface. Therefore, the SoC must contain extra **on-chip hardware test structures**.

So the split is:

```text
ATE = external manufacturing tester hardware outside the SoC
Internal test access structures = DFT hardware inserted inside the SoC
```

Internal test access structures include:

1. **Test controller**: on-chip hardware that selects test modes, starts tests and controls scan/BIST/TAM operation.
2. **TAM - Test Access Mechanism**: on-chip test bus or test path that carries test data from chip pins or JTAG to embedded cores and carries responses back.
3. **Core wrapper**: on-chip wrapper logic around an embedded IP core. It isolates the core during test and connects it to the TAM.
4. **Scan chains**: on-chip chains of flip-flops connected in shift-register form during test mode, allowing internal state to be controlled and observed.
5. **BIST - Built-In Self-Test**: on-chip self-test hardware, often used for memories or logic. It can generate test patterns and check responses internally.
6. **JTAG / boundary scan logic**: on-chip access logic connected to a small number of external pins, used for test, debug and controlling internal test modes.

Without these internal structures, the ATE could only test the outer pins and would not be able to efficiently test embedded cores. With DFT structures, the flow becomes:

```text
ATE / JTAG pins
      |
      v
On-chip test controller
      |
      v
TAM / test bus / scan access path
      |
      v
Core wrapper / scan chain / BIST
      |
      v
Embedded IP core or memory
```

Exam line: **ATE is external tester hardware, while scan chains, BIST, TAM, core wrappers, JTAG logic and test controller are on-chip DFT hardware added inside the SoC so that embedded cores can be controlled and observed during manufacturing test.**

### 2. JTAG / Boundary Scan

**JTAG** means **Joint Test Action Group**. In chips, the word usually refers to the **IEEE 1149.1 boundary-scan test access architecture**. It provides standardized test and debug access through a small number of pins. It is useful for board-level test, chip access, debug and sometimes controlling internal test modes.

JTAG has two parts:

1. **External side**: ATE, debugger or JTAG probe outside the chip.
2. **Internal side**: JTAG hardware inside the SoC, such as the TAP controller, instruction register, data registers and boundary-scan cells.

So JTAG is not only software. The JTAG interface depends on real **on-chip test hardware** inside the SoC and real external pins connected to an external tester/debugger.

Common JTAG pins are:

- **TCK - Test Clock**: clock used for shifting test/debug data.
- **TMS - Test Mode Select**: controls the state of the TAP controller.
- **TDI - Test Data In**: serial data input into the chip.
- **TDO - Test Data Out**: serial data output from the chip.
- **TRST - Test Reset**: optional reset for JTAG test logic.

The important internal hardware is the **TAP - Test Access Port controller**. The TAP controller is a small on-chip state machine. It controls whether the chip is shifting an instruction, shifting test data, capturing data or updating data.

What happens in JTAG / boundary scan:

1. **The external tester or debugger connects to the JTAG pins**. This external tool may be ATE in manufacturing or a JTAG debugger during bring-up.
2. **The tester drives TCK and TMS**. These signals move the TAP controller through its states.
3. **An instruction is shifted into the instruction register through TDI**. The instruction tells the chip what operation to perform, such as reading chip ID, bypassing the chip, sampling pins, controlling boundary-scan cells or accessing internal test registers.
4. **The selected data register becomes active**. Depending on the instruction, this may be a boundary-scan register, device-ID register, bypass register, debug register or private SoC test register.
5. **Test data is shifted in through TDI**. The bits move serially through the selected register.
6. **The TAP controller captures or updates the value**. Capture means reading present values into the register. Update means applying shifted values to internal test logic or boundary cells.
7. **Response data is shifted out through TDO**. The tester observes this output and compares it with expected response.

In **boundary scan**, special cells are placed near the chip input/output pins. These boundary-scan cells can capture pin values or drive pin values during test. This allows board-level testing even when physical pins are difficult to probe directly.

Example: if a board trace between two chips is broken, boundary scan can make one chip drive a known value on a pin and make another chip capture that value. If the captured value is wrong, the board connection may be faulty.

In SoC testing, JTAG may be used to:

- Enter test mode.
- Configure test controller registers.
- Access scan chains.
- Trigger BIST.
- Observe test results.

JTAG is useful but may not be enough for high-volume core testing because it is mostly serial and has limited bandwidth. That is why TAM and internal test buses are used for large test data movement.

Exam line: **JTAG is an external access standard supported by on-chip TAP and boundary-scan hardware. During test, instructions and data are shifted through TDI/TDO under TAP control so that pins, test registers, BIST and internal test modes can be accessed using only a few external pins.**

### 3. Test Controller

The **test controller** is an **on-chip hardware control block**. It coordinates the testing process. It selects test mode, enables wrappers, starts BIST, controls scan operation and routes test data through the TAM.

The test controller is important because all cores cannot be tested randomly. The chip must enter a safe test state. Clocks, resets, isolation signals, scan-enable signals and BIST start signals must be controlled correctly.

What happens in the test controller:

1. **Test mode is selected**. This may happen through JTAG, special test pins, ATE commands or internal test registers.
2. **The controller places the SoC in a safe test state**. Normal functional activity may be stopped, selected clocks may be enabled, resets may be controlled and some blocks may be isolated.
3. **The controller selects which core or memory is being tested**. It may choose CPU scan, DSP scan, SRAM MBIST, logic BIST, interconnect test or another test.
4. **The controller configures test paths**. It connects the selected core wrapper, scan chain or BIST block to the TAM or JTAG path.
5. **The controller starts the test**. For scan, it controls scan enable and capture clocks. For BIST, it sends a start signal.
6. **The controller waits for completion**. It monitors done signals, fail signals, signatures or status registers.
7. **The controller reports the result**. The result may be read by ATE or JTAG as pass/fail/status data.

The test controller is not the same as the CPU. In many manufacturing test modes, the CPU may be inactive. The test controller is separate DFT hardware designed to control test structures even when normal software is not running.

Exam line: **The test controller is on-chip DFT hardware that sequences the SoC test mode by selecting cores, enabling wrappers, controlling scan/BIST/TAM signals and reporting pass/fail status to the external tester.**

### 4. Test Access Mechanism / TAM

**TAM** means **Test Access Mechanism**. It is the internal path used to transport test data from chip pins or test controller to embedded cores and back.

TAM is **inside the SoC**. It is not an external tester. It is an on-chip test transport structure, like a test bus, scan path or hierarchical access network. Its job is to solve the embedded-core access problem: the ATE can reach chip pins, but embedded cores are deep inside the chip.

TAM may be implemented as:

- Dedicated test bus.
- Multiplexed test bus.
- Daisy-chain scan path.
- Hierarchical TAM.
- Network-style test access.
- Reused functional bus in some designs.

What happens in TAM:

1. **The external tester or JTAG interface provides test data at chip-level access pins**.
2. **The test controller selects the destination core**. For example, it may select CPU scan chain, SRAM BIST controller or DSP wrapper.
3. **The TAM transports test data to that selected core**. Depending on the design, this movement may be serial, parallel, bus-based or hierarchical.
4. **The core wrapper or scan chain applies the test data to the embedded core**.
5. **The core response is captured**.
6. **The TAM transports the response back to the test controller, JTAG or ATE output path**.
7. **The external tester compares the response with expected output**.

The width of the TAM matters. A wider TAM can reduce test time because more test data can be shifted in parallel. But a wider TAM increases routing overhead and may consume more area. Therefore, TAM design is a trade-off between test time and hardware overhead.

Example: if a core requires 10,000 test bits and the TAM can deliver only 1 bit per test clock, the test takes many shift cycles. If the TAM has 16 parallel wires, more bits can be delivered per clock, so the test becomes faster. But those 16 wires consume routing area.

Exam line: **TAM is on-chip test transport hardware that carries test patterns and responses between external access points and embedded cores; its bandwidth strongly affects total test application time.**

### 5. Core Wrapper

A **core wrapper** is **on-chip test logic placed around an embedded IP core**. It separates the core from the rest of the SoC during test and connects the core to the TAM.

A wrapper helps in:

- Applying test stimuli to core inputs.
- Capturing core output responses.
- Isolating the core from neighboring logic.
- Connecting internal scan chains to TAM.
- Supporting different test modes.
- Reusing core-level test patterns at SoC level.

Core wrappers are essential for third-party IP because the SoC integrator may not know the internal implementation details of a hard IP core. The wrapper creates a standard test interface around the core.

What happens in a core wrapper:

1. **Normal mode**: the wrapper is transparent. The IP core communicates normally with the SoC interconnect, memories, interrupts and neighboring blocks.
2. **Test mode begins**: the test controller enables wrapper test mode.
3. **The wrapper isolates the core**. The core is separated from surrounding functional logic so test values do not disturb the rest of the chip.
4. **The wrapper connects core inputs and outputs to the TAM**. Now the external tester can indirectly control and observe the core.
5. **Test patterns are applied to the core**. Inputs may come from scan chains, wrapper cells or TAM data.
6. **Core responses are captured**. Output values are stored in wrapper cells or scan chains.
7. **Responses are sent back through the TAM**. The tester compares them with expected results.

The wrapper is especially useful for **pattern retargeting**. A core vendor may give test patterns for the core alone. After the core is embedded inside a SoC, those patterns must be delivered through the SoC-level TAM and wrapper. The wrapper provides the standard access point that makes this possible.

Exam line: **A core wrapper is on-chip boundary logic around an IP core; during test it isolates the core, connects it to the TAM, applies test stimuli and captures responses so core-level tests can be reused at SoC level.**

### 6. Scan Chains

A **scan chain** is an **on-chip DFT - Design for Testability structure** in which internal flip-flops are connected together like a serial shift register during test mode. It is real hardware inserted inside the SoC during DFT insertion. It is not software, and it is not outside the chip.

To understand scan chains, first understand the testing problem. A digital chip has many internal flip-flops. These flip-flops store the state of the circuit. In normal operation, their values change only through the functional logic of the design. An external tester can easily control chip pins, but it cannot directly set or observe every internal flip-flop. That makes sequential logic very hard to test because the tester may need many clock cycles just to force the chip into one useful internal state.

Scan chains solve this by giving the tester direct controlled access to internal state. In test mode, many flip-flops are temporarily connected end-to-end. The tester can shift data into them, use them to apply values to combinational logic, capture the response, and shift the response back out.

The two key ideas are:

1. **Controllability**: the ability to force an internal node or flip-flop to a required value.
2. **Observability**: the ability to observe an internal value from outside the chip.

Without scan:

- Internal states are difficult to set because the tester can only use primary inputs and normal functional paths.
- Internal responses are difficult to observe because many signals never reach chip pins directly.
- Sequential circuit testing becomes complex because the tester must drive long functional sequences to reach one internal condition.
- ATPG tools may fail to generate high-quality patterns because many internal faults are not reachable or observable.

With scan:

- Test data can be shifted into internal flip-flops.
- Internal flip-flop values can be controlled directly.
- The combinational logic between flip-flops can be tested more easily.
- Responses can be captured into flip-flops.
- Captured responses can be shifted out and compared with expected responses.

#### What Changes In The Hardware

A normal flip-flop has a data input `D`, clock input and output `Q`. A scan flip-flop adds extra test connections:

- **SI - Scan In**: serial input used during test shifting.
- **SO - Scan Out**: serial output connected to the next scan flip-flop.
- **SE - Scan Enable**: control signal that selects normal mode or scan mode.

In normal mode:

```text
SE = 0
Functional data D goes into the flip-flop.
The circuit behaves like the original design.
```

In scan mode:

```text
SE = 1
Scan input SI goes into the flip-flop.
Flip-flops behave like one long shift register.
```

Simple view:

```text
Scan In -> [FF1] -> [FF2] -> [FF3] -> [FF4] -> Scan Out
```

This chain may contain hundreds or thousands of flip-flops. Large SoCs usually have many scan chains in parallel to reduce shift time.

#### What Actually Happens In Scan Testing

Scan testing usually has three phases: **shift**, **capture** and **shift out**.

1. **Shift-in phase**: `SE - Scan Enable` is set to 1. The tester shifts a test vector into the scan chain. This loads selected internal flip-flop values.
2. **Capture phase**: `SE` is set to 0 for one or more functional clock cycles. The loaded flip-flop values pass through combinational logic, and the response is captured into destination flip-flops.
3. **Shift-out phase**: `SE` is set back to 1. The captured response is shifted out through the scan output.
4. **Comparison phase**: ATE compares the shifted-out response with the expected response generated by ATPG.

The full flow is:

```text
ATPG pattern
   |
   v
Shift test bits into scan flip-flops
   |
   v
Capture logic response using functional clock
   |
   v
Shift captured response out
   |
   v
ATE compares actual response with expected response
```

#### Small Example

Suppose a small circuit has three internal flip-flops: `A`, `B` and `C`. A fault can be detected only when `A = 1`, `B = 0` and `C = 1`. Without scan, the tester must find a functional input sequence that naturally brings the circuit into that exact state. That may be difficult or impossible.

With scan, the tester simply shifts `101` into the scan chain. Then it applies one capture clock and shifts out the response. This is why scan greatly improves controllability and observability.

#### Faults Detected Using Scan

Scan chains are commonly used with ATPG to detect structural manufacturing faults such as:

- **Stuck-at fault**: a signal is permanently stuck at 0 or 1.
- **Transition delay fault**: a signal changes too slowly from 0 to 1 or 1 to 0.
- **Bridging fault**: two wires are accidentally shorted together.
- **Open fault**: a connection is broken.

Scan does not directly prove that the design specification is correct. That is the job of verification. Scan helps test whether the manufactured chip has physical defects.

#### Why Scan Is Important In SoC Testing

In an SoC, many IP cores are embedded deep inside the chip. Their internal flip-flops cannot be reached from external pins. Scan chains create internal access paths. These scan paths may connect to core wrappers, TAM and ATE. Therefore, scan chains are a major part of SoC test integration.

Important point for exams: scan chains are not used because the normal circuit is wrong. They are added because manufacturing defects can occur after fabrication, and the tester needs a practical way to control and observe internal logic.

#### Advantages Of Scan Chains

- They improve controllability of internal flip-flops.
- They improve observability of internal responses.
- They make ATPG easier and more effective.
- They increase fault coverage.
- They simplify testing of sequential logic.
- They support structural testing of embedded cores.

#### Limitations Of Scan Chains

- They add area overhead because flip-flops need scan multiplexers.
- They add routing overhead because scan flip-flops must be connected.
- They increase test time because long chains require many shift cycles.
- They can increase test power because many flip-flops toggle during shifting.
- They need careful clock, reset and test-mode control.

How to remember scan chains:

```text
Scan = make hidden flip-flops visible and controllable.
Shift in -> capture -> shift out -> compare.
```

Exam line: **A scan chain is on-chip DFT hardware that connects internal flip-flops into shift-register paths during test mode. It improves controllability and observability by allowing ATPG patterns to be shifted into internal state, captured through logic and shifted out for ATE comparison.**

### 7. BIST

**BIST** means **Built-In Self-Test**. It is **test hardware built inside the SoC or inside a block** so that the block can test itself with minimum help from external ATE. BIST is not just a test pattern. It is a small hardware system that can generate test activity, apply it to the target block, check the response and report pass/fail status.

The main idea is simple:

```text
Instead of sending every test pattern from outside,
put a small tester inside the chip.
```

This is why it is called **built-in** self-test. The tester-like logic is built into the silicon.

#### Why BIST Is Needed

SoCs contain many embedded memories, processor cores, accelerators, bus structures and logic blocks. Many of these blocks are not directly accessible from external pins. If ATE had to send every test pattern through chip pins, test data volume and test time would become very large.

BIST solves this by moving some test work inside the chip. The external tester may only need to:

1. Put the chip in test mode.
2. Start the BIST.
3. Wait for completion.
4. Read pass/fail status.

The BIST hardware itself performs most of the detailed testing internally.

#### Basic BIST Hardware Blocks

A BIST structure may contain:

- **BIST controller**: controls the self-test sequence.
- **Pattern generator**: creates test data internally.
- **Address generator**: used mainly in memory BIST to select memory addresses.
- **Comparator**: compares actual output with expected output.
- **Response compactor**: compresses many output responses into a smaller signature.
- **Status register**: stores pass, fail, done and sometimes failing address information.
- **Interface muxes**: switch the block between normal functional mode and test mode.

So BIST is definitely **inside the SoC**. It is on-chip DFT hardware. ATE is outside the chip, while BIST is inside the chip.

#### Common Types Of BIST

- **MBIST - Memory Built-In Self-Test**: used for SRAMs, ROMs, register files and memory macros.
- **LBIST - Logic Built-In Self-Test**: used for random digital logic.

Both are BIST, but they test different structures and use different methods.

#### Memory BIST / MBIST

**MBIST - Memory Built-In Self-Test** is used because embedded memories are very common in SoCs. A chip may contain instruction memory, data memory, cache RAMs, FIFOs, register files, buffers and many SRAM macros. Testing all of them through normal processor reads and writes would be slow and incomplete.

MBIST uses memory-specific test algorithms. These algorithms write and read memory in planned patterns to detect memory faults.

Common memory faults include:

- **Stuck-at fault**: a memory bit is always 0 or always 1.
- **Transition fault**: a bit cannot change correctly from 0 to 1 or 1 to 0.
- **Coupling fault**: writing one memory cell incorrectly affects another cell.
- **Address decoder fault**: the wrong memory location is selected.
- **Retention fault**: a memory cell cannot hold data long enough.

What happens in MBIST:

1. **ATE, JTAG or the test controller starts MBIST** by setting a start bit.
2. **The MBIST controller takes control of the memory**. Normal CPU, DMA or bus access is blocked.
3. **The address generator selects memory locations** in a defined order.
4. **The pattern generator writes test data** such as all-0, all-1, checkerboard, walking 1 or walking 0.
5. **The controller reads the memory back**.
6. **The comparator checks actual data against expected data**.
7. **The controller repeats the algorithm** for many addresses and data patterns.
8. **The status register records pass/fail**. Some MBISTs also record the failing address and failing data bit.
9. **ATE or JTAG reads the final result**.

Simple MBIST flow:

```text
Start MBIST
    |
    v
Generate address
    |
    v
Write test pattern
    |
    v
Read memory
    |
    v
Compare expected vs actual data
    |
    v
Report pass/fail
```

A strong phrase to remember is: **MBIST is a memory-specific on-chip tester**. It knows how to walk through memory addresses, write patterns, read them back and detect memory faults.

#### Logic BIST / LBIST

**LBIST - Logic Built-In Self-Test** is used for digital logic rather than memories. Random logic does not have neat addressable locations like memory, so LBIST usually works differently from MBIST.

LBIST commonly uses:

- **LFSR - Linear Feedback Shift Register**: generates pseudo-random test patterns.
- **Scan chains**: apply pseudo-random patterns to internal flip-flops and capture logic responses.
- **MISR - Multiple Input Signature Register**: compacts many response bits into a short signature.
- **Signature comparison**: compares the final signature with the expected good signature.

What happens in LBIST:

1. **The test controller starts LBIST**.
2. **The LFSR generates pseudo-random patterns**.
3. **The patterns are loaded into scan chains or applied to logic inputs**.
4. **The logic is clocked so faults can affect outputs**.
5. **Responses are captured**.
6. **The MISR compacts responses into a signature**.
7. **The final signature is compared with the expected signature**.
8. **Pass/fail result is reported**.

Simple LBIST flow:

```text
Start LBIST
    |
    v
LFSR generates pseudo-random patterns
    |
    v
Scan chains apply patterns to logic
    |
    v
Logic response is captured
    |
    v
MISR compacts response into signature
    |
    v
Compare signature and report pass/fail
```

LBIST is useful because it reduces the amount of test data that ATE must store. Instead of storing every pattern externally, the chip generates many patterns internally.

#### BIST In Normal Mode Vs Test Mode

In normal operation, BIST should not interfere with the functional circuit. The CPU should access memory normally, buses should run normally and accelerators should work normally. The BIST logic is idle.

In test mode, muxes and control signals give BIST access to the target block. For example, in MBIST, the memory address/data/control lines may come from the MBIST controller instead of the CPU or bus. After the test is complete, control returns to the normal functional path.

This is important because BIST is physically present inside the SoC, but it should only control the block during test mode.

#### BIST Vs External ATE Testing

In pure external testing, ATE must provide test patterns, control signals and expected responses from outside the chip. This can require large tester memory and long test time.

With BIST, the chip performs much of the test internally. ATE acts more like a supervisor: it starts the test and reads the result. This is why BIST is very useful for embedded memories and repeated structures.

#### Advantages Of BIST

- It reduces external test data volume.
- It reduces dependence on external pin access.
- It can test deeply embedded memories and logic.
- It can reduce ATE test time.
- It can support at-speed testing inside the chip.
- It can make field test or power-on self-test possible in some systems.

#### Limitations Of BIST

- It adds area overhead because extra hardware is inserted.
- It adds design complexity.
- It may increase power during test because many internal nodes switch.
- LBIST may not detect every hard-to-test fault unless combined with ATPG or scan.
- MBIST must be designed carefully for the memory type and fault model.

How to remember BIST:

```text
BIST = mini tester inside the chip.
MBIST = mini tester for memory.
LBIST = mini tester for logic.
ATE starts it, BIST runs it, status reports it.
```

Exam line: **BIST is on-chip DFT hardware that performs self-test by generating test patterns internally, applying them to memory or logic, checking/compacting responses and reporting pass/fail status to the test controller, JTAG or ATE. MBIST targets memories, while LBIST targets random logic.**

### 8. ATPG And Test Patterns

**ATPG** means **Automatic Test Pattern Generation**. ATPG is mainly an **EDA software tool activity**, not a hardware block inside the SoC. It generates test vectors for structural faults such as stuck-at faults, transition faults and bridging faults.

ATPG patterns are often applied through scan chains. The test integration flow must ensure that ATPG patterns generated for each core can be delivered at SoC level through wrappers and TAM.

What happens in ATPG:

1. **The ATPG tool reads the gate-level netlist and scan structure**.
2. **A fault model is selected**. Common examples are stuck-at-0, stuck-at-1, transition-delay and bridging faults.
3. **The tool tries to create input and scan values that activate each fault**. Activating a fault means making the faulty circuit behave differently from the fault-free circuit.
4. **The tool propagates the fault effect to an observable point**. Usually this is a scan output, primary output or test response compactor.
5. **The tool saves the test pattern**. The pattern includes scan-in data, primary input data, capture clocks and expected scan-out response.
6. **Patterns are converted into ATE-ready format**.
7. **During manufacturing test, ATE applies those patterns through scan/TAM/JTAG paths**.
8. **The actual chip response is compared with expected response**.

ATPG is connected to hardware because its generated patterns depend on scan chains, wrappers, TAM and test modes. If the SoC test architecture is poor, ATPG patterns may exist at core level but may be difficult to apply after integration.

Exam line: **ATPG is a test-pattern generation process performed by EDA tools; the generated patterns are applied through on-chip scan, wrapper and TAM hardware to detect manufacturing faults.**

<a id="topic-3-dft-comparison"></a>

### Deep Comparison: BIST, MBIST, LBIST, ATPG, Scan, JTAG And TAM

These terms are related, but they are not the same thing. In exam answers, do not write them as if all are "testing methods" only. Some are **on-chip hardware**, some are **external interfaces**, some are **EDA tool processes**, and some are **test transport paths**.

The clean separation is:

```text
ATE = external tester machine outside the chip
JTAG = external access standard + on-chip TAP hardware
TAM - Test Access Mechanism = on-chip path that transports test data
Scan chain = on-chip DFT structure inside logic
BIST = on-chip self-test hardware
MBIST = BIST specialized for memories
LBIST = BIST specialized for logic
ATPG = EDA software process that generates test patterns
Core wrapper = on-chip interface around an embedded core
Test controller = on-chip hardware that sequences test operation
```

#### BIST Vs ATPG

**BIST - Built-In Self-Test** is hardware added inside the SoC. It allows a memory or logic block to test itself by generating patterns internally and checking responses internally. The external tester does not need to send every test vector. It may only start the BIST and read the final pass/fail result. Therefore, BIST reduces ATE data volume, external pin dependency and test application complexity.

**ATPG - Automatic Test Pattern Generation** is not normally a hardware block inside the SoC. ATPG is an EDA software process performed before manufacturing test. The ATPG tool analyzes the gate-level netlist, scan chains and fault models, then produces test vectors. During manufacturing test, those vectors are applied through ATE, scan chains, TAM and wrappers.

The deepest difference is this: **BIST moves pattern generation and response checking inside the chip**, while **ATPG generates patterns outside the chip using software tools and then applies those patterns through DFT hardware**. BIST is useful when internal access is difficult or when there are many repeated structures, especially memories. ATPG is useful for systematically targeting structural faults in logic using the actual gate-level implementation.

Exam comparison line: **BIST is on-chip self-test hardware; ATPG is an off-chip EDA pattern-generation process whose patterns are applied through on-chip DFT structures.**

#### MBIST Vs LBIST

**MBIST - Memory Built-In Self-Test** is BIST for memories such as SRAM, ROM, register files and memory macros. It is common because SoCs contain many embedded memories, and those memories may not be directly accessible from chip pins. MBIST usually contains an address generator, data-pattern generator, read/write controller and comparator. It runs memory-specific algorithms such as march tests, walking 1, walking 0, checkerboard or all-0/all-1 patterns.

**LBIST - Logic Built-In Self-Test** is BIST for random digital logic. It usually uses pseudo-random pattern generation and response compaction. Logic responses are compressed into a signature, and the final signature is compared with the expected signature. LBIST is more difficult than MBIST because random logic does not have the regular structure of memory arrays. Some faults may be hard to activate or observe using pseudo-random patterns.

The difference is therefore based on the **type of circuit being tested**. MBIST targets regular memory arrays where address, data and read/write operations are central. LBIST targets combinational and sequential logic where signal paths, flip-flops and logic gates are central.

Exam comparison line: **MBIST tests embedded memories using memory algorithms; LBIST tests logic using internally generated patterns and compressed response signatures.**

#### Scan Chains Vs BIST

**Scan chains** are on-chip DFT structures that make internal flip-flops controllable and observable. In scan mode, flip-flops are connected as shift registers. The tester can shift in a known internal state, apply a capture clock, then shift out the response. Scan chains are not complete self-test systems by themselves. They provide access to internal state.

**BIST** is more autonomous. A BIST block includes some internal pattern generation and response checking. In MBIST, the controller can generate addresses, write patterns, read memory and compare data. In LBIST, the logic may receive pseudo-random patterns and produce compressed signatures.

So scan chains mainly solve the **access problem**: how to control and observe internal sequential nodes. BIST solves the **self-test problem**: how to generate and evaluate tests inside the chip with less external test data.

Exam comparison line: **Scan chains provide controllability and observability; BIST provides internal pattern generation and response checking.**

#### ATPG Vs Scan Chains

ATPG and scan chains work together, but they are different. **ATPG** is the software process that creates the test vectors. **Scan chains** are the hardware paths used to apply many of those vectors inside the chip.

For example, the ATPG tool may decide that a certain fault can be detected if internal flip-flop A is set to 1, flip-flop B is set to 0 and a specific input is toggled. The scan chain makes this possible because the tester can shift those values directly into internal flip-flops. After capture, the scan chain shifts the response back out.

Without scan chains, ATPG for sequential circuits becomes much harder because the tool has to reach internal states only through normal functional inputs. With scan chains, the sequential circuit becomes easier to test because internal state can be loaded and observed directly.

Exam comparison line: **ATPG produces the test vectors; scan chains physically deliver those vectors into internal flip-flops and shift responses out.**

#### JTAG Vs TAM

**JTAG - Joint Test Action Group** is a standardized access interface using a small number of pins such as TCK, TMS, TDI and TDO. It is excellent for debug, board test, chip identification, boundary scan and accessing control/status registers. JTAG is partly external because it uses external pins and external tools, but it also needs on-chip TAP controller hardware.

**TAM - Test Access Mechanism** is the internal SoC test transport path. It carries test data from chip-level access points to embedded cores and carries responses back. TAM may be wider and more parallel than JTAG because high-volume manufacturing test needs faster data movement.

The difference is: **JTAG is the standardized doorway into the chip**, while **TAM is the internal hallway that carries test data to the embedded rooms/cores**. JTAG may configure the test controller or start BIST, but TAM handles large-scale internal test transport when many embedded cores must be tested efficiently.

Exam comparison line: **JTAG is a low-pin-count access standard; TAM is the internal SoC test data transport mechanism used to reach embedded cores.**

#### Core Wrapper Vs TAM

The **core wrapper** surrounds one embedded IP core. It isolates the core in test mode and provides a standard test interface. The wrapper is local to a core. It helps apply core-level test patterns after the core has been integrated inside the SoC.

The **TAM** is the shared or hierarchical path that connects chip-level test access to many core wrappers. TAM is not wrapped around one specific core; it is the transport network between the test controller/external interface and multiple embedded cores.

The difference is: **the wrapper is the test boundary around a core**, while **TAM is the route used to reach that wrapper**. A good SoC test architecture needs both. Without a wrapper, the embedded core may not have a clean test interface. Without TAM, the wrapper may exist but test data cannot efficiently reach it from outside.

Exam comparison line: **A core wrapper gives a core a test interface; TAM connects that interface to chip-level test access.**

#### Test Controller Vs ATE

**ATE - Automatic Test Equipment** is external manufacturing equipment outside the chip. It applies test patterns, controls test pins, measures responses and makes pass/fail decisions. It is a machine used in production testing.

The **test controller** is on-chip DFT hardware. It receives commands from ATE, JTAG or test pins and then controls internal test operations. It selects test modes, enables scan, starts BIST, selects TAM paths and collects status.

The difference is: **ATE is outside the chip and provides the manufacturing test environment**, while **the test controller is inside the chip and coordinates internal DFT structures**. ATE cannot directly control every internal memory, scan chain or wrapper unless the test controller and test access architecture make those structures reachable.

Exam comparison line: **ATE is external tester hardware; the test controller is internal SoC hardware that translates external test control into internal test sequencing.**

#### Complete Relationship In One Flow

The best way to remember all of them is to follow the data/control path:

```text
ATPG tool creates scan test patterns
              |
              v
ATE stores/applies those patterns from outside the chip
              |
              v
JTAG pins or test pins provide chip-level entry
              |
              v
Test controller selects test mode and target core
              |
              v
TAM transports test data inside the SoC
              |
              v
Core wrapper isolates and connects the embedded core
              |
              v
Scan chains apply/capture logic-test data
              |
              v
Response goes back through wrapper/TAM/JTAG or test pins to ATE
```

For BIST, the flow is shorter because the chip does more work internally:

```text
ATE/JTAG starts BIST
      |
      v
Test controller enables MBIST/LBIST
      |
      v
On-chip BIST generates patterns and checks responses
      |
      v
Pass/fail result goes back to test controller and ATE/JTAG
```

#### Summary Table

| Term | Full Form | What It Is | Where It Exists | Main Role |
|---|---|---|---|---|
| ATE | Automatic Test Equipment | External tester machine | Outside chip | Applies tests and checks pass/fail |
| JTAG | Joint Test Action Group | Access standard plus TAP hardware | Pins + on-chip TAP | Low-pin test/debug access |
| TAP | Test Access Port | JTAG controller hardware | Inside SoC | Controls JTAG shifting/capture/update |
| TAM | Test Access Mechanism | Test transport path | Inside SoC | Moves test data to/from embedded cores |
| Core wrapper | Core test wrapper | Test boundary logic | Around IP core inside SoC | Isolates core and connects it to TAM |
| Scan chain | Scan flip-flop chain | DFT hardware path | Inside logic | Shifts test data in/out of flip-flops |
| BIST | Built-In Self-Test | Self-test hardware | Inside SoC/block | Generates/checks tests internally |
| MBIST | Memory Built-In Self-Test | Memory self-test hardware | Near memory macros | Tests SRAM/ROM/register files |
| LBIST | Logic Built-In Self-Test | Logic self-test hardware | Inside logic test architecture | Tests random logic using signatures |
| ATPG | Automatic Test Pattern Generation | EDA software process | Outside chip, before test | Generates structural test vectors |

Final exam line: **In SoC test integration, ATPG generates patterns, ATE applies or starts tests, JTAG/test pins provide access, the test controller sequences test modes, TAM transports data, wrappers isolate embedded cores, scan chains control and observe logic, and BIST/MBIST/LBIST perform internal self-test.**

### What Is Test Integration?

**Test integration** is the process of combining all block-level and core-level test structures into a complete SoC-level test architecture.

It includes:

1. Collecting test information for every core.
2. Integrating scan chains.
3. Adding core wrappers.
4. Connecting wrappers to TAM.
5. Integrating memory BIST and logic BIST.
6. Connecting JTAG or ATE interface.
7. Creating test modes and test controller logic.
8. Verifying that test mode does not disturb normal operation.
9. Combining core tests, memory tests, interconnect tests and chip-level tests.
10. Preparing data needed for manufacturing test.

### Test Integration Flow

A good SoC test integration flow is:

```text
Core Test Requirements
 scan chains, BIST, patterns, power, clocks, test time
              |
              v
DFT Architecture Selection
 scan + BIST + wrapper + TAM + JTAG/test controller
              |
              v
Core Wrapper Insertion
 isolate core and provide standard test interface
              |
              v
TAM Design
 decide bus width, routing, hierarchy and access paths
              |
              v
Test Controller Integration
 control test modes, scan enable, BIST start and result capture
              |
              v
Pattern Retargeting / Test Data Preparation
 move core-level tests to SoC-level access paths
              |
              v
DFT Verification
 verify scan, BIST, wrappers, TAM and test modes
              |
              v
Manufacturing Test Program
 ATE/JTAG patterns, schedule and pass/fail limits
```

The term **pattern retargeting** is useful. It means adapting tests created for an individual core so they can be applied when the core is embedded inside the SoC through wrappers and TAM.

### What Is Test Scheduling?

**Test scheduling** is the process of assigning start times, end times and resource allocations to core tests so that all tests complete in minimum time while satisfying constraints.

If there are five core tests, the simplest schedule is serial:

```text
Time ->
Core 1: [ Test C1 ]
Core 2:             [ Test C2 ]
Core 3:                         [ Test C3 ]
Core 4:                                     [ Test C4 ]
Core 5:                                                 [ Test C5 ]
```

This is safe but slow.

A better schedule runs independent tests in parallel:

```text
Time ->
Core 1: [ Test C1          ]
Core 2: [ Test C2 ]
Core 3:          [ Test C3      ]
Core 4: [ Test C4    ]
Core 5:                    [ Test C5 ]
```

Parallel testing reduces test time, but only if power, **TAM - Test Access Mechanism** capacity and resource constraints are not violated.

### Figure 2: Rectangle-Packing View Of Test Scheduling

This is a strong diagram for exam answers because it shows test scheduling as a resource allocation problem.

```text
Available TAM - Test Access Mechanism Width / Test Bus Wires
^
|  +----------+ +------+
|  | Core A   | |Core C|
|  | Test     | |Test  |
|  +----------+ +------+
|
|        +--------------+
|        | Core B Test  |
|        +--------------+
|
|  +--------------------+
|  | Core D Test        |
|  +--------------------+
+----------------------------------> Time

Each rectangle:
horizontal length = how long that core test runs
vertical size     = how many TAM - Test Access Mechanism wires/channels that test occupies
packing objective = arrange tests to finish as early as possible
constraints       = power, total TAM - Test Access Mechanism width, conflicts, dependencies
```

Figure source: look at the rectangle-packing test scheduling sources in [CLO5_Topic3_sources.md](<sources/CLO5_Topic3_sources.md>). This figure is needed because it clearly shows why scheduling is not only ordering tests; it is allocating **TAM - Test Access Mechanism** capacity over time.

### Inputs To Test Scheduling

The test scheduler needs:

- Number of cores.
- Test time of each core.
- **TAM - Test Access Mechanism** width required by each core.
- Power consumed by each test.
- Test patterns and scan chain lengths.
- BIST execution time.
- ATE channel limits.
- Test clock limits.
- Core dependencies.
- Shared-resource conflicts.
- Whether a test is preemptive or non-preemptive.
- Whether tests can run in parallel.

If these inputs are unknown, scheduling cannot be optimized.

### Objectives Of Test Scheduling

**Test scheduling** means deciding **when each core test starts, when it ends, and which test resources it uses**. In an SoC, many blocks must be tested: CPU core, SRAMs, DSP, interconnect, UART, DMA, memories, PLL-related test logic and other IP blocks. If every test is run one after another, the total manufacturing test time becomes very large. If all tests are run together, the chip may exceed power, thermal or access limits. Therefore, test scheduling is a constrained optimization problem.

The main objective is to minimize **test application time**.

**Test application time** means the total time required to apply all required manufacturing tests to one chip. This directly affects manufacturing cost because **ATE - Automatic Test Equipment** is expensive. If one chip takes longer on the tester, fewer chips can be tested per hour.

However, the scheduler cannot simply run everything in parallel. It must reduce time while keeping the test safe and valid.

Other important objectives are:

- **Reduce ATE - Automatic Test Equipment cost**: less test time means less tester occupation time per chip.
- **Reduce test data volume**: fewer externally stored patterns reduce ATE memory requirement.
- **Avoid exceeding test power limit**: too much switching during scan/BIST can cause voltage drop, overheating or damage.
- **Use TAM - Test Access Mechanism bandwidth efficiently**: TAM - Test Access Mechanism wires/channels should not remain idle if useful tests can run safely.
- **Avoid test-resource conflicts**: two tests must not fight for the same test bus, memory, clock, wrapper or ATE channel.
- **Reduce idle time of TAM - Test Access Mechanism wires**: unused test access capacity wastes possible parallelism.
- **Preserve required fault coverage**: reducing test time must not remove important patterns or reduce defect detection too much.
- **Support memory, logic, interconnect and core tests**: the schedule must cover all required test types, not only CPU or memory tests.

The best schedule is not always the one with maximum parallelism. The best schedule is the one that gives **minimum safe test time under constraints**. This is why SoC test scheduling is usually discussed together with TAM optimization, wrapper design, power constraints, precedence constraints and tester data volume.

How to remember:

```text
Test scheduling = minimize time, but obey constraints.
Fast is not enough; it must be safe, accessible and complete.
```

Exam line: **The objective of SoC test scheduling is to minimize total test application time and ATE cost while satisfying TAM - Test Access Mechanism bandwidth, power, thermal, clock, precedence, data-volume and resource constraints without reducing fault coverage.**

### Constraints In SoC Test Scheduling

A **constraint** is a limit that the scheduler must not violate. In SoC test scheduling, constraints are very important because tests use real chip resources. A test may need scan chains, BIST controllers, TAM - Test Access Mechanism wires, clocks, memory buses, power domains and ATE channels. Two tests can run together only if their combined requirements fit within the available limits.

### 1. Power Constraint

**Power constraint** means the total power consumed during simultaneous tests must remain below the safe test power limit.

Testing often causes higher switching activity than normal operation. During scan shifting, many flip-flops toggle together. During BIST, many memory locations or logic nodes may switch repeatedly. If too many blocks are tested at the same time, test power can exceed the safe limit.

High test power can cause:

- **IR drop**: supply voltage drops due to high current.
- **Timing failure**: logic may fail because voltage drop slows gates.
- **Overheating**: local or global chip temperature rises.
- **False failure**: a good chip may fail the test because the test condition is too stressful.
- **Physical damage**: extreme power may damage the chip.

Example:

- CPU scan test consumes 40 mW.
- DSP scan test consumes 50 mW.
- SRAM BIST consumes 30 mW.
- Power limit is 80 mW.

CPU + DSP cannot run together because:

```text
40 mW + 50 mW = 90 mW > 80 mW
```

CPU + SRAM BIST can run together because:

```text
40 mW + 30 mW = 70 mW <= 80 mW
```

So the scheduler may run CPU and SRAM BIST together, but it must separate CPU and DSP. This is why **power-constrained test scheduling** is important.

Exam line: **Power-constrained scheduling prevents unsafe parallel testing by ensuring that the sum of active test powers never exceeds the chip's test power limit.**

### 2. TAM - Test Access Mechanism Bandwidth Constraint

**TAM - Test Access Mechanism** is the on-chip path that transports test stimuli from chip-level access points to embedded cores and transports test responses back. It may be implemented as test buses, test wires, scan access paths or hierarchical test networks.

**TAM - Test Access Mechanism bandwidth constraint** means the total number of TAM - Test Access Mechanism wires/channels used by simultaneous tests must not exceed the available TAM - Test Access Mechanism width.

Example:

```text
Available TAM - Test Access Mechanism width = 16 wires
Core A test needs 10 wires
Core B test needs 8 wires
```

Core A + Core B cannot run together because:

```text
10 + 8 = 18 wires > 16 wires
```

TAM - Test Access Mechanism bandwidth controls how much test data can be transported in parallel. A wider TAM - Test Access Mechanism can reduce test time because more bits move per test clock. But a wider TAM - Test Access Mechanism also increases routing area, wiring congestion and hardware overhead. Therefore, TAM - Test Access Mechanism width is a trade-off:

```text
More TAM width -> lower test time, higher area/routing overhead
Less TAM width -> lower hardware overhead, higher test time
```

This is why many research papers discuss **wrapper/TAM co-optimization**. The wrapper controls how a core connects to test access, while TAM - Test Access Mechanism controls how much test data can reach that core. Both affect test time.

Exam line: **TAM - Test Access Mechanism bandwidth constraint limits parallel testing because the sum of TAM wires required by simultaneously tested cores must not exceed the available Test Access Mechanism width.**

### 3. Resource Conflict Constraint

A **resource conflict** occurs when two tests need the same hardware or test resource at the same time, but that resource cannot be shared.

Shared resources may include:

- Test bus.
- TAM - Test Access Mechanism wires.
- Test clock generator.
- PLL - Phase-Locked Loop.
- Memory or memory port.
- BIST controller.
- Core wrapper.
- Power domain control.
- Reset control.
- External ATE channels.
- JTAG TAP - Test Access Port.

Example: CPU scan test and interconnect test may both need the same test bus. Even if power is safe and TAM width is enough, both tests cannot run together if the bus can connect to only one test path at a time.

Resource conflicts are practical constraints. They come from the actual SoC test architecture. A schedule that ignores them may look good on paper but cannot be applied on real silicon.

Exam line: **Resource-constrained scheduling prevents two tests from using the same non-shareable test hardware, bus, clock, memory, wrapper or ATE channel at the same time.**

### 4. Precedence Constraint

A **precedence constraint** means one test must be completed before another test can start. It is a dependency relation between tests.

Some tests depend on earlier configuration, diagnosis or setup. Examples:

- Test controller must be configured before BIST starts.
- PLL or clock logic may need testing before high-speed logic tests.
- Memory BIST may be needed before processor software-based tests.
- Scan-chain integrity may be checked before scan ATPG patterns are applied.
- Parent core or parent test access path may need setup before child cores in hierarchical SoCs.
- Power-domain test may need isolation/retention checks before low-power mode testing.

Precedence constraints are important because SoC testing is not only a set of independent blocks. Some tests prepare the chip for later tests, and some tests rely on earlier results.

Example:

```text
1. Configure test controller
2. Run scan-chain integrity check
3. Run ATPG scan patterns
4. Run memory BIST
5. Run processor-based software test
```

The scheduler cannot randomly move step 5 before step 4 if the software test depends on working memory.

Exam line: **Precedence-constrained scheduling enforces required test order when one test must configure, validate or enable another test.**

### 5. Thermal Constraint

**Thermal constraint** means the test schedule must avoid excessive chip temperature or local hot spots.

Power and temperature are related, but they are not identical. Even if total average power is acceptable, two nearby cores tested together may create a local hot region. This is especially important in dense SoCs and 3D ICs, where heat removal is more difficult.

Thermal-aware scheduling may avoid:

- testing neighboring high-power cores simultaneously,
- running long high-power tests back-to-back,
- activating the same region of the chip continuously,
- exceeding maximum junction temperature.

Example: CPU and DSP may individually be safe, and their combined total power may fit the power limit, but if they are physically close on the die, testing both together may create local heating. The scheduler may separate them or insert a cooler low-power test between them.

Exam line: **Thermal-aware scheduling controls the spatial and temporal placement of tests so that local hot spots and excessive chip temperature are avoided.**

### 6. Clock And Frequency Constraint

**Clock and frequency constraint** means tests requiring incompatible clocks cannot run together.

Different tests may need different clock conditions:

- Scan shift may use a slow external or test clock.
- At-speed delay testing may use a high-speed functional clock.
- MBIST may run from an internal BIST clock.
- PLL tests may require special clock configuration.
- Different power domains may have different clock availability.

If two tests require different clock modes from the same clock generator, they may conflict.

Example: one core may need slow scan shift clock while another test needs an at-speed capture clock from the PLL. If the chip cannot provide both clock configurations safely at the same time, the tests must be scheduled separately.

Exam line: **Clock-constrained scheduling separates tests that require incompatible test clocks, scan clocks, BIST clocks or functional at-speed clocks.**

### 7. Test Mode Conflict

A **test mode conflict** occurs when two tests require incompatible chip modes.

Examples:

- One test requires scan shift mode, while another requires MBIST mode in the same domain.
- One test needs the core isolated, while another needs the interconnect active.
- One test requires a power domain ON, while another test sequence assumes that domain is OFF.
- One test requires reset asserted, while another requires normal operation.
- One test uses JTAG debug mode, while another uses manufacturing scan mode.

Test modes are controlled by test controller signals, muxes, scan-enable lines, isolation controls, BIST start signals and power-mode controls. If two tests require contradictory settings, they cannot run together.

Exam line: **Test mode conflicts occur when two tests require incompatible control settings such as scan mode, BIST mode, reset mode, isolation mode or power mode.**

### 8. Tester Memory / Data Volume Constraint

**Tester memory constraint** means the ATE has limited memory for storing test patterns and expected responses.

ATPG scan tests can generate very large pattern sets. If all patterns are stored externally, ATE memory requirement increases. Large test data volume also increases loading time and test cost.

Techniques used to reduce tester data volume include:

- **BIST - Built-In Self-Test**: generates many patterns inside the chip.
- **Test compression**: compresses scan input patterns and compacts output responses.
- **Pattern reduction**: removes redundant or low-value patterns.
- **Efficient TAM - Test Access Mechanism scheduling**: uses available test access paths without wasting bandwidth.
- **Pattern retargeting**: adapts core-level patterns to SoC-level access paths.

Exam line: **Tester data-volume constraint limits how much pattern data can be stored and applied by ATE, so BIST, compression and efficient scheduling are used to reduce manufacturing test cost.**

### Types Of Test Scheduling

| Type | Meaning | Use |
|---|---|---|
| Serial scheduling | Runs one test at a time | Simple and safe, but usually slow |
| Parallel scheduling | Runs multiple independent tests at the same time | Reduces total test time when constraints allow |
| Power-constrained scheduling | Limits parallelism based on total test power | Prevents IR drop, overheating and chip damage |
| Resource-constrained scheduling | Limits tests based on TAM - Test Access Mechanism, clocks, wrappers, ATE channels or shared resources | Most practical SoC scheduling model |
| Precedence-constrained scheduling | Forces some tests to occur before others | Needed when setup, diagnosis or hierarchy creates dependencies |
| Preemptive scheduling | Allows a test to pause and resume later | Can improve resource use but increases control complexity |
| Non-preemptive scheduling | Once a test starts, it runs to completion | Simpler and common in manufacturing test |
| Hierarchical scheduling | Considers parent/child core hierarchy and subsystem structure | Useful for large SoCs with nested IP blocks |
| Thermal-aware scheduling | Avoids local hot spots and excessive temperature | Important for dense SoCs and 3D ICs |

#### Serial Scheduling

Serial scheduling is the simplest method. Only one test runs at a time. It is easy to control and usually avoids most conflicts, but it wastes possible parallelism.

```text
Core A -> Core B -> Core C -> Core D
```

Use it when the test architecture is simple or when power/resource constraints are very tight.

#### Parallel Scheduling

Parallel scheduling runs multiple tests at the same time. It reduces test time, but only when combined requirements fit inside the power, TAM - Test Access Mechanism, clock and resource limits.

```text
Time 0: Core A + Core B
Time 1: Core C + Memory BIST
```

Use it when tests are independent and do not exceed constraints.

#### Preemptive Vs Non-Preemptive Scheduling

In **preemptive scheduling**, a test can be paused and resumed. This may help when a resource must be temporarily given to a higher-priority test. But it is harder to implement because the test state must be saved or safely restarted.

In **non-preemptive scheduling**, once a test begins, it runs to completion. This is simpler and common because many manufacturing tests are easier to manage as complete blocks.

Exam line: **Serial scheduling is simple but slow; parallel scheduling reduces test time; constrained scheduling decides safe parallelism under power, TAM - Test Access Mechanism, resource, precedence, clock, thermal and data-volume limits.**

### Example Test Schedule

Assume the SoC has four tests:

| Core/Test | Test Time | TAM - Test Access Mechanism Wires Needed | Test Power |
|---|---:|---:|---:|
| CPU scan test | 10 units | 8 | 40 mW |
| SRAM MBIST - Memory Built-In Self-Test | 6 units | 4 | 30 mW |
| DSP scan test | 8 units | 8 | 50 mW |
| UART scan/interconnect test | 4 units | 2 | 10 mW |

Limits:

- Total TAM - Test Access Mechanism width = 12 wires.
- Total test power limit = 80 mW.

Now check possible combinations:

| Combination | TAM Check | Power Check | Can Run Together? |
|---|---|---|---|
| CPU + SRAM MBIST | 8 + 4 = 12 <= 12 | 40 + 30 = 70 <= 80 | Yes |
| CPU + UART | 8 + 2 = 10 <= 12 | 40 + 10 = 50 <= 80 | Yes |
| DSP + UART | 8 + 2 = 10 <= 12 | 50 + 10 = 60 <= 80 | Yes |
| CPU + DSP | 8 + 8 = 16 > 12 | 40 + 50 = 90 > 80 | No |
| SRAM MBIST + DSP | 4 + 8 = 12 <= 12 | 30 + 50 = 80 <= 80 | Yes |

One possible schedule is:

```text
Time 0-6:   CPU + SRAM MBIST
            TAM - Test Access Mechanism = 8 + 4 = 12
            Power = 40 + 30 = 70 mW

Time 6-10:  CPU + UART
            TAM - Test Access Mechanism = 8 + 2 = 10
            Power = 40 + 10 = 50 mW

Time 10-18: DSP
            TAM - Test Access Mechanism = 8
            Power = 50 mW
```

CPU test lasts 10 units. It runs from time 0 to time 10. SRAM MBIST finishes at time 6. UART fills the remaining CPU interval from time 6 to time 10. DSP cannot run with CPU because both TAM - Test Access Mechanism and power limits are violated, so DSP is scheduled after CPU.

Why not CPU + DSP together?

```text
TAM - Test Access Mechanism = 8 + 8 = 16 > 12
Power = 40 + 50 = 90 mW > 80 mW
```

So CPU and DSP cannot be scheduled together. This example shows that test scheduling is controlled by constraints, not only by convenience.

#### What The Example Teaches

- A test with short duration can fill idle space if it does not exceed constraints.
- Parallel testing is allowed only when both TAM - Test Access Mechanism and power limits are satisfied.
- The scheduler tries to reduce empty time on the test resource.
- A schedule that is fastest mathematically may still be invalid physically.
- Test scheduling is similar to packing rectangles into the smallest time window.

### Test Integration Vs Test Scheduling

Test integration and test scheduling are connected, but they answer different questions.

**Test integration** asks:

```text
How do we make embedded cores accessible and testable?
```

It is mainly an architecture and connectivity problem. It creates the infrastructure: scan chains, BIST, wrappers, test controller, JTAG/ATE access and TAM - Test Access Mechanism.

**Test scheduling** asks:

```text
Once the test infrastructure exists, when should each test run?
```

It is mainly a time and resource optimization problem. It uses the integrated test infrastructure efficiently.

| Point | Test Integration | Test Scheduling |
|---|---|---|
| Main question | How are all cores made accessible for test? | When should each test run? |
| Focus | Architecture and connectivity | Time/resource optimization |
| Main elements | Scan chains, BIST, wrappers, TAM - Test Access Mechanism, JTAG, test controller | Start time, finish time, parallelism, constraints |
| Main resource concern | Can the core be reached and isolated? | Can tests share time, power, TAM - Test Access Mechanism and clocks safely? |
| Output | Integrated SoC-level test architecture | Optimized test schedule |
| Main objective | Make every embedded core testable | Minimize test application time safely |
| Example | Connect CPU wrapper to TAM - Test Access Mechanism | Run CPU test with SRAM MBIST but not with DSP |

Exam line: **Test integration creates the test infrastructure; test scheduling uses that infrastructure efficiently under power, TAM - Test Access Mechanism, resource, precedence, clock, thermal and data-volume constraints.**

### Relationship With DFT

**DFT - Design for Testability** is the foundation of both test integration and scheduling. DFT means adding hardware features that make the manufactured chip easier to test. Without DFT, internal cores are difficult to control and observe because ATE can mainly access chip pins.

DFT answers:

```text
What hardware should be added so the chip can be tested?
```

Test integration answers:

```text
How are all those DFT structures connected at SoC level?
```

Test scheduling answers:

```text
How are those test structures used over time?
```

Important DFT structures:

- **Scan chains**: make internal flip-flops controllable and observable.
- **BIST - Built-In Self-Test**: lets memory or logic test itself internally.
- **Boundary scan / JTAG - Joint Test Action Group**: provides low-pin external access.
- **Core wrappers**: isolate embedded cores and connect them to test access paths.
- **Test controller**: sequences scan, BIST, wrapper and TAM control signals.
- **TAM - Test Access Mechanism**: transports test data to and from embedded cores.
- **Test compression**: reduces external test data volume.
- **Isolation cells for test mode**: prevent test activity from disturbing neighboring logic.

DFT must be planned early because adding test logic late can disturb timing, area, routing, power and floorplanning. For example, adding many scan chains or TAM - Test Access Mechanism wires late may create routing congestion. Adding BIST late may change memory interfaces. Adding wrappers late may affect integration timing.

Exam line: **DFT provides the hardware structures, test integration connects them into a chip-level test architecture, and test scheduling decides how to use them over time to reduce manufacturing test cost safely.**

<a id="topic-3-final-answer"></a>

### Final Exam-Ready Answer

SoC test scheduling and test integration are important parts of SoC testing. Verification checks whether the design is functionally correct before fabrication, whereas testing checks whether the manufactured silicon is free from physical defects. In an SoC, testing is difficult because many IP cores, memories, buses and internal nodes are embedded inside the chip and cannot be directly accessed from external pins. Therefore, a proper design-for-test strategy is required.

SoC test integration is the process of combining the test structures of all embedded cores into a complete chip-level test architecture. It includes scan-chain integration, BIST integration, core wrapper insertion, test access mechanism design, JTAG or ATE interface connection, test controller design and pattern retargeting. A core wrapper isolates the core during test and connects it to the test access mechanism. The **TAM - Test Access Mechanism** transports test data between the external tester and the embedded cores. BIST allows memories or logic blocks to test themselves, while scan chains improve controllability and observability of sequential logic.

After test integration, test scheduling is performed. SoC test scheduling decides the order and parallelism of core tests so that total test application time is minimized. It assigns start time, finish time and test resources to each core test. If all tests are applied serially, test time becomes very high. If tests are applied in parallel without control, power, thermal or resource limits may be violated. Hence, test scheduling is an optimization problem.

The main constraints in SoC test scheduling are **TAM - Test Access Mechanism** bandwidth, test power, shared resources, precedence constraints, clock constraints, thermal limits, test mode conflicts and ATE data limitations. For example, two cores cannot be tested together if their combined power exceeds the power limit or if their combined **TAM - Test Access Mechanism** width exceeds the available **TAM - Test Access Mechanism** width. Similarly, a memory BIST may need to finish before software-based processor testing begins.

A common way to understand test scheduling is the rectangle-packing model. Each core test is represented as a rectangle, where the horizontal dimension represents test time and the vertical dimension represents **TAM - Test Access Mechanism** width. The scheduler packs these rectangles into the smallest possible total time while respecting power and resource constraints. This shows that test scheduling is not just a list of tests, but a constrained optimization problem.

Thus, test integration creates the infrastructure required to test every embedded core, while test scheduling uses that infrastructure efficiently. Together, they reduce test application time, reduce ATE cost, maintain safe test power, preserve fault coverage and make the SoC ready for manufacturing test.

### Short 10-Mark Exam Answer

SoC test integration and test scheduling are required because a system-on-chip contains many embedded cores and memories that cannot be directly controlled or observed from external pins. Test integration means connecting all core-level and chip-level test structures into one complete SoC-level test architecture. It includes scan chains, memory BIST, logic BIST, core wrappers, test access mechanism, JTAG/ATE interface and a chip test controller. The core wrapper isolates an embedded core during test and provides a standard test interface. The **TAM - Test Access Mechanism** carries test patterns and responses between the external tester and internal cores. BIST allows internal memories or logic to test themselves.

Test scheduling means deciding when each test should be applied and which tests can run in parallel. The objective is to minimize total test application time and ATE cost while satisfying constraints. Important constraints are power limit, **TAM - Test Access Mechanism** bandwidth, shared resource conflicts, precedence between tests, test clock limitations, thermal limits and test mode conflicts. For example, two core tests may not run together if their total power exceeds the chip's safe test power or if their combined **TAM - Test Access Mechanism** width exceeds available **TAM - Test Access Mechanism** wires.

Therefore, SoC test integration makes embedded cores accessible for testing, while SoC test scheduling applies those tests efficiently. A good test schedule reduces manufacturing test time without reducing fault coverage or damaging the chip due to excessive power.

<a id="topic-3-technical-words"></a>

### Technical Words To Use For Marks

- **SoC test integration** (write this because it is the process of combining all embedded-core test structures into one chip-level test system.)
- **SoC test scheduling** (write this because the question asks how tests are ordered and parallelized.)
- **DFT - Design for Testability** (write this because testing embedded cores requires extra test logic.)
- **Controllability** (write this because internal nodes must be forced to known values during test.)
- **Observability** (write this because internal responses must be captured and checked.)
- **ATE - Automatic Test Equipment** (write this because manufacturing tests are applied through tester hardware.)
- **JTAG / Boundary Scan** (write this because it is a standard external test/debug access path.)
- **TAM - Test Access Mechanism** (write this because it transports test data to and from embedded cores.)
- **Core wrapper** (write this because embedded IP must be isolated and connected to test access paths.)
- **Scan chain** (write this because it improves controllability and observability of flip-flops.)
- **ATPG - Automatic Test Pattern Generation** (write this because structural test patterns are generated automatically.)
- **BIST - Built-In Self-Test** (write this because memories and some logic blocks can test themselves.)
- **MBIST - Memory Built-In Self-Test** (write this because SoCs contain many embedded memories.)
- **LBIST - Logic Built-In Self-Test** (write this because logic can be tested with on-chip pattern generation.)
- **Pattern retargeting** (write this because core-level patterns must be adapted to SoC-level access paths.)
- **Test application time** (write this because the main scheduling objective is to reduce total test time.)
- **Fault coverage** (write this because tests must detect a high percentage of modeled faults.)
- **Power-constrained scheduling** (write this because parallel tests must not exceed safe test power.)
- **Resource-constrained scheduling** (write this because TAM wires, clocks, ATE channels and shared memories are limited.)
- **Precedence constraint** (write this because some tests must run before others.)
- **Test conflict** (write this because two tests may require the same resource or incompatible mode.)
- **Thermal-aware scheduling** (write this because local heating can restrict parallel testing.)
- **Rectangle-packing model** (write this because it is a standard way to explain TAM-width vs test-time scheduling.)
- **Wrapper/TAM co-optimization** (write this because wrapper design and TAM allocation together affect test time.)
- **Tester data volume** (write this because ATE memory and pattern data size affect test cost.)
- **Manufacturing test** (write this because this topic is about testing fabricated silicon.)

<a id="topic-3-diagrams"></a>

### Images / Diagrams To Remember

1. **SoC test integration architecture**: Draw `ATE/JTAG -> Test Controller -> TAM/Test Bus -> Core Wrappers -> IP Cores/BIST`. This is the best figure for test integration.
2. **Rectangle-packing schedule**: Draw available **TAM - Test Access Mechanism** capacity vertically and time horizontally; represent each core test as a rectangle. This is the best figure for test scheduling.
3. **Figure/source to look at**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.86](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=86>) for DFT and scan-chain context. Use this to justify why internal access is needed.
4. **Figure/source to look at for DFT strategy**: [SOC Design Flow.pdf, p.6](<System on chip/SOC Design Flow.pdf#page=6>) because it directly mentions developing a DFT strategy.
5. **Figure/source to look at for rectangle-packing idea**: [CLO5_Topic3_sources.md](<sources/CLO5_Topic3_sources.md>) because it contains the research sources that explain wrapper/TAM co-optimization and rectangle-packing test scheduling.

### CLO 5 Coverage Status

The main CLO 5 syllabus headlines are now covered in this file:

1. **Verification Techniques - OVM, UVM and VVM**
2. **SoC Verification Flow**
3. **SoC Test Scheduling and Test Integration**

Use the clickable index at the top of this file to jump to each topic, its question, final answer, technical words and diagrams.
