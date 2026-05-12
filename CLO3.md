# CLO 3 - SoC Memory Design and Memory Controller Architecture

## Clickable Index

- [CLO 3 Master Definitions](#clo3-master-definitions)
- [Topic 1: SoC Memory Design - Memory Technology](#topic-1)
  - [Question](#topic-1-question)
  - [Main Explanation](#topic-1-explanation)
  - [Final Exam-Ready Answer](#topic-1-final-answer)
  - [Technical Words](#topic-1-technical-words)
  - [Images / Diagrams](#topic-1-diagrams)
- [Topic 2: Memory Design Hierarchy and Tradeoffs](#topic-2)
  - [Question](#topic-2-question)
  - [Main Explanation](#topic-2-explanation)
  - [Final Exam-Ready Answer](#topic-2-final-answer)
  - [Technical Words](#topic-2-technical-words)
  - [Images / Diagrams](#topic-2-diagrams)
- [Topic 3: SDRAM Basics - Banked Architecture and Latencies](#topic-3)
  - [Question](#topic-3-question)
  - [Main Explanation](#topic-3-explanation)
  - [Final Exam-Ready Answer](#topic-3-final-answer)
  - [Technical Words](#topic-3-technical-words)
  - [Images / Diagrams](#topic-3-diagrams)
- [Topic 4: Quality-Aware Scheduling](#topic-4)
  - [Question](#topic-4-question)
  - [Main Explanation](#topic-4-explanation)
  - [Final Exam-Ready Answer](#topic-4-final-answer)
  - [Technical Words](#topic-4-technical-words)
  - [Images / Diagrams](#topic-4-diagrams)
- [Topic 5: Memory Controller](#topic-5)
  - [Question](#topic-5-question)
  - [Main Explanation](#topic-5-explanation)
  - [Final Exam-Ready Answer](#topic-5-final-answer)
  - [Technical Words](#topic-5-technical-words)
  - [Images / Diagrams](#topic-5-diagrams)
- [Topic 6: Models of Simple Processor-Memory Interaction](#topic-6)
  - [Question](#topic-6-question)
  - [Main Explanation](#topic-6-explanation)
  - [Final Exam-Ready Answer](#topic-6-final-answer)
  - [Technical Words](#topic-6-technical-words)
  - [Images / Diagrams](#topic-6-diagrams)

<a id="clo3-master-definitions"></a>

## CLO 3 Master Definitions

Use this section to revise the full forms and meanings used throughout CLO 3. For memory questions, always know whether the term is a **memory technology**, **memory structure**, **memory interface**, **controller block**, or **timing parameter**.

| Term | Full Form / Meaning | Definition / Where It Fits |
|---|---|---|
| SoC | System on Chip | Complete system integrated on one chip, including processor, memory, interconnect, controllers and peripherals. |
| SRAM | Static Random Access Memory | Fast volatile memory that stores data using latch-based cells and does not need refresh while powered. Used for caches, TCM, scratchpads, FIFOs and buffers. |
| DRAM | Dynamic Random Access Memory | Dense volatile memory that stores bits as charge on capacitors and therefore needs periodic refresh. Used for large main memory. |
| SDRAM | Synchronous Dynamic Random Access Memory | DRAM synchronized to a clock, organized with banks, rows, columns and commands such as activate/read/write/precharge/refresh. |
| DDR SDRAM | Double Data Rate Synchronous Dynamic Random Access Memory | SDRAM interface family that transfers data on both rising and falling clock edges to increase bandwidth. |
| LPDDR | Low-Power Double Data Rate | Low-power DDR DRAM family optimized for mobile, embedded and battery-powered SoCs. |
| HBM | High Bandwidth Memory | Stacked DRAM technology using a very wide interface and advanced packaging for very high bandwidth. |
| eDRAM | Embedded Dynamic Random Access Memory | DRAM-like memory integrated on-chip or near logic; denser than SRAM but needs refresh and special process support. |
| ROM | Read-Only Memory | Non-volatile memory for fixed code/data such as boot code, reset vectors and fixed lookup tables. |
| PROM | Programmable Read-Only Memory | ROM that can be programmed after manufacturing, usually once. |
| OTP | One-Time Programmable | Memory that can be programmed once and then permanently retains data. |
| EEPROM | Electrically Erasable Programmable Read-Only Memory | Non-volatile memory that can be electrically erased and rewritten, slower and endurance-limited. |
| NOR Flash | Non-volatile Flash memory with good random read behavior | Used for boot code, firmware and execute-in-place code storage. |
| NAND Flash | Dense non-volatile Flash memory | Used for mass storage; needs ECC, bad-block management and wear leveling. |
| eMMC | embedded MultiMediaCard | Managed NAND storage package/interface used in embedded systems. |
| UFS | Universal Flash Storage | Higher-performance managed NAND storage interface used in phones and embedded systems. |
| NVM | Non-Volatile Memory | Any memory that retains data without power, such as ROM, Flash, MRAM, ReRAM or PCM. |
| FRAM / F-RAM | Ferroelectric Random Access Memory | Non-volatile memory with low power and high endurance for frequent small writes. |
| MRAM | Magnetoresistive Random Access Memory | Non-volatile memory storing data magnetically; promising for embedded NVM. |
| ReRAM / RRAM | Resistive Random Access Memory | Non-volatile memory using resistance states to store data. |
| PCM / PRAM | Phase-Change Memory / Phase-Change Random Access Memory | Non-volatile memory using material phase changes to store data. |
| pSRAM | pseudo-Static Random Access Memory | DRAM-like internal storage with an SRAM-like external interface. |
| nvSRAM | non-volatile Static Random Access Memory | SRAM-like fast memory with non-volatile backup storage. |
| TCM | Tightly Coupled Memory | Fast on-chip memory closely connected to the CPU for deterministic low-latency access. |
| ITCM | Instruction Tightly Coupled Memory | TCM used for time-critical instructions. |
| DTCM | Data Tightly Coupled Memory | TCM used for time-critical data. |
| FIFO | First-In First-Out | Ordered buffer where the first written data is the first read data. |
| CPU | Central Processing Unit | Processor core that fetches instructions and accesses memory. |
| GPU | Graphics Processing Unit | Graphics/parallel processing accelerator that often needs high memory bandwidth. |
| DSP | Digital Signal Processor | Processor/accelerator for signal-processing tasks. |
| DMA | Direct Memory Access | Controller that transfers data without continuous CPU involvement. |
| NoC | Network on Chip | On-chip communication network connecting masters, memories and controllers. |
| PHY | Physical Layer | Circuit block that drives/receives electrical memory-interface signals such as DDR/LPDDR signals. |
| ECC | Error Correction Code | Extra protection bits used to detect and often correct memory errors. |
| QoS | Quality of Service | Memory-controller policy support for latency, bandwidth, priority and fairness guarantees. |
| FR-FCFS | First-Ready First-Come First-Served | Memory scheduling policy that prioritizes ready commands/row hits while considering arrival order. |
| Row buffer | Open row storage inside a DRAM bank | Holds the currently activated row; row hits are faster than row conflicts. |
| Bank | Independent DRAM subarray | Allows overlapping operations and bank interleaving. |
| Rank | Group of DRAM chips/devices selected together | Common organization unit in DDR memory systems. |
| Channel | Independent memory interface path | More channels usually increase bandwidth. |
| ACT / ACTIVATE | Activate command | Opens a DRAM row in a selected bank. |
| PRE / PRECHARGE | Precharge command | Closes the open row and prepares a bank for another row. |
| CAS | Column Address Strobe | DRAM column access concept; appears in CAS latency. |
| CL | CAS Latency | Delay between READ command and data availability. |
| tRCD | Row-to-Column Delay | Delay between ACTIVATE and READ/WRITE. |
| tRP | Row Precharge Time | Time required to precharge a bank before another row can be activated. |
| tRAS | Row Active Time | Minimum time a row must remain active before precharge. |
| tRC | Row Cycle Time | Minimum time between two ACTIVATE commands to the same bank. |
| tRFC | Refresh Cycle Time | Time consumed by a DRAM refresh operation. |
| XIP | Execute In Place | Running code directly from non-volatile memory such as NOR Flash without copying it to RAM first. |
| SLC / MLC / TLC / QLC | Single/Multi/Triple/Quad-Level Cell | NAND Flash storage density types storing 1, 2, 3 or 4 bits per cell. |
| QDR SRAM | Quad Data Rate Static Random Access Memory | High-speed SRAM interface type useful for packet buffers and lookup tables. |

Memory line for CLO 3:

```text
SRAM is fast and on-chip.
DRAM/SDRAM/DDR/LPDDR/HBM are Dynamic Random Access Memory families/interfaces that give large main-memory capacity and bandwidth.
ROM/Flash/NVM are non-volatile memories that keep data without power.
The memory controller converts SoC requests into legal memory commands.
Scheduling, banking and QoS - Quality of Service decide latency, bandwidth and fairness.
```

<a id="topic-1"></a>

## Topic 1: SoC Memory Design - Memory Technology

<a id="topic-1-question"></a>

### Question

**Explain memory technology in SoC memory design.**

### CLO Mapping

This topic belongs to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

Reason: The syllabus places **Memory Technology** under **SoC Memory Design**, and CLO 3 explicitly mentions memory design and memory controller architecture. This topic is not mainly about SoC verification or design methodology; it is about selecting and understanding the memory technologies used inside and around an SoC.

### What The Question Is Asking

The examiner is asking you to explain the different memory technologies used in SoC design and the tradeoffs behind choosing them. Do not answer with only definitions of SRAM and DRAM. A complete answer should explain why memory technology matters, how memories differ by speed, density, power, volatility, cost and location, and why an SoC normally uses a mixture of memory types.

For full marks, answer in this order:

1. Define memory technology in the context of SoC.
2. Explain why memory is critical in SoC performance and cost.
3. Classify memory as volatile/non-volatile and on-chip/off-chip.
4. Explain SRAM, DRAM/eDRAM, ROM, Flash and emerging NVM.
5. Compare technologies using latency, bandwidth, density, power, endurance and process compatibility.
6. Draw memory technology hierarchy or on-chip/off-chip memory diagram.
7. End with how memory technology selection affects memory controller architecture.

<a id="topic-1-explanation"></a>

### Core Idea

**Memory technology** means the physical and architectural type of memory used to store instructions, data, configuration, buffers, code and persistent information in an SoC. In an SoC, memory is not a single block. It is a system of different technologies: registers, SRAM caches, scratchpads, ROM, embedded SRAM, embedded DRAM, off-chip DRAM, **LPDDR - Low-Power Double Data Rate**, Flash, **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** and sometimes emerging **NVM - Non-Volatile Memory**.

The important point is this: **no single memory technology is best for all needs**. Fast memory is usually expensive in area and power. Dense memory is usually slower. Non-volatile memory keeps data without power but has write/erase limitations. Off-chip memory gives large capacity but adds latency, pins, controller complexity and board-level energy.

Therefore, SoC memory design is a tradeoff between:

- speed,
- area,
- capacity,
- bandwidth,
- latency,
- energy,
- leakage,
- cost per bit,
- process compatibility,
- reliability,
- retention,
- endurance,
- software programmability.

### Why Memory Technology Is Important In SoC

In many SoCs, the processor or accelerator is not the only performance bottleneck. The memory system often limits performance because computation units can only work when instructions and data arrive on time. A fast processor becomes underutilized if instruction fetch or data fetch is delayed.

Memory technology affects:

1. **Processor performance**: instruction fetch and data fetch cycles depend on cache and memory speed.
2. **Area**: large on-chip SRAM can dominate die area.
3. **Power**: memory accesses consume dynamic energy, while SRAM leakage and DRAM refresh consume standby power.
4. **Cost**: on-chip memory increases die size; off-chip memory adds package, pins and board cost.
5. **Bandwidth**: multimedia, AI, graphics and networking SoCs need large data movement bandwidth.
6. **Real-time behavior**: scratchpad or **TCM - Tightly Coupled Memory** gives predictable latency, while cache misses are less predictable.
7. **Boot and storage**: ROM/NOR/NAND Flash store boot code, firmware and persistent data.
8. **Memory-controller complexity**: DRAM, **LPDDR - Low-Power Double Data Rate**, NAND Flash and other Flash memories need controllers for timing, refresh, **ECC - Error Correction Code** or wear management.

Exam line: **Memory technology selection determines the SoC's speed, power, die area, cost and memory-controller complexity.**

### Figure 1: Memory Technology Pyramid

Draw this figure in the exam when the question asks for memory technology.

```text
 Fastest, smallest, highest cost/bit
                 ^
                 |
            +----------+
            | Registers|
            +----------+
            |  SRAM    |  L1/L2 cache, TCM, scratchpad, FIFO
            +----------+
            | eDRAM    |  denser on-chip memory, needs refresh
            +----------+
            | DRAM /   |  off-chip main memory, DDR/LPDDR/HBM
            | LPDDR    |
            +----------+
            | NOR Flash|  boot code, XIP, firmware storage
            +----------+
            | NAND     |  large storage, eMMC/UFS/SSD, needs controller
            | Flash    |
            +----------+
                 |
                 v
 Slowest, largest, lowest cost/bit, often non-volatile
```

Figure source: look at [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.13](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=13>) for storage as a SoC design decision involving size, volatility and on-die/off-die placement. Also look at [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22 for the on-chip/off-chip memory discussion. This figure is useful because it visually shows the central tradeoff: speed and predictability at the top, capacity and low cost per bit at the bottom.

### Classification Of Memory Technologies

### 1. Volatile And Non-Volatile Memory

**Volatile memory** loses stored data when power is removed. It is used when speed and frequent read/write access are important.

Examples:

- Registers.
- **SRAM - Static Random Access Memory**.
- **DRAM - Dynamic Random Access Memory**.
- **eDRAM - Embedded Dynamic Random Access Memory**.
- **LPDDR - Low-Power Double Data Rate**.

**Non-volatile memory** retains data even when power is removed. It is used for boot code, firmware, configuration, program storage, file systems and persistent data.

Examples:

- Mask ROM.
- **OTP - One-Time Programmable** memory.
- **EEPROM - Electrically Erasable Programmable Read-Only Memory**.
- NOR Flash.
- NAND Flash.
- **FRAM - Ferroelectric Random Access Memory**.
- **MRAM - Magnetoresistive Random Access Memory**.
- **ReRAM - Resistive Random Access Memory**.
- **PCM - Phase-Change Memory**.

Use this line in exams: **Volatile memory is mainly for active computation; non-volatile memory is mainly for boot, storage and persistence.**

### 2. On-Chip And Off-Chip Memory

**On-chip memory** is integrated on the same silicon die as the processor and accelerators. It gives low latency and high bandwidth because it is physically close to the compute blocks. But it consumes die area and is limited in capacity.

On-chip examples:

- Register files.
- SRAM caches.
- **TCM - Tightly Coupled Memory**.
- Scratchpad memory.
- **FIFOs - First-In First-Out buffers**.
- small ROM.
- **eDRAM - Embedded Dynamic Random Access Memory** in some processes.

**Off-chip memory** is placed outside the SoC die, either in the same package, on the board, or as an external memory device. It provides much larger capacity but needs pins, interfaces and a memory controller.

Off-chip examples:

- **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory**.
- **LPDDR - Low-Power Double Data Rate**.
- **HBM - High Bandwidth Memory**.
- external NAND/NOR Flash.
- **eMMC - embedded MultiMediaCard** / **UFS - Universal Flash Storage**.

The lecture material emphasizes that putting memory on the die improves accessibility, access time and bandwidth, but DRAM process technology differs from normal microprocessor logic technology and on-die capacity is limited. This is the main reason SoCs often combine small fast on-chip memory with larger off-chip memory.

### Figure 2: On-Chip And Off-Chip Memory In SoC

```text
                 +----------------------------------+
                 |              SoC Die             |
                 |                                  |
                 |  +------+     +---------------+  |
                 |  | CPU  |<--->| L1/L2 Cache   |  |
                 |  +------+     +---------------+  |
                 |      |              |            |
                 |      v              v            |
                 |  +---------------------------+   |
                 |  | On-chip SRAM / TCM / ROM  |   |
                 |  +---------------------------+   |
                 |      |                            |
                 |      v                            |
                 |  +---------------------------+   |
                 |  | Memory Controller         |   |
                 |  +---------------------------+   |
                 +--------------|-------------------+
                                |
              package/board pins|PHY/interface
                                v
                 +-------------------------------+
                 | Off-chip DRAM / LPDDR / Flash |
                 +-------------------------------+
```

Figure source: look at [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22 because those slides explain why designers choose between on-die ROM/RAM and large off-die memory. This figure is useful because it connects memory technology to physical SoC organization.

### SRAM - Static Random Access Memory

**SRAM** stores each bit using a bistable latch, commonly implemented as a 6-transistor cell in CMOS. It is called static because it does not need periodic refresh as long as power is supplied.

Key characteristics:

- Very low latency.
- High random-access performance.
- No refresh required.
- Volatile.
- Large cell area compared with DRAM.
- High cost per bit.
- Significant leakage in advanced nodes.
- Easy to integrate with logic CMOS compared with DRAM.

SRAM is used in SoCs for:

- **L1/L2/L3 caches**.
- **Scratchpad memory**.
- **TCM - Tightly Coupled Memory**.
- **Register files**.
- **FIFOs - First-In First-Out buffers**.
- **Packet buffers**.
- **Lookup tables**.
- **Small real-time data buffers**.

SRAM is chosen when speed and predictability matter more than density. For example, an L1 cache must be extremely fast, so SRAM is used even though it consumes more area. A real-time microcontroller may use SRAM TCM because it gives predictable access time unlike cache, where a miss can cause delay.

#### Meaning Of Common SRAM-Based SoC Memories

These are all usually implemented using SRAM-like storage cells or SRAM macros, but they are not the same architecturally. The difference is in **who controls the memory**, **where it sits**, and **why it is used**.

##### 1. L1 / L2 / L3 Caches

**Cache memory** is small, fast memory placed close to the processor to reduce the average time needed to access instructions and data. It automatically stores copies of recently used or likely-to-be-used data from lower memory levels.

**L1 cache - Level 1 cache** is the closest cache to the CPU core. It is usually the smallest and fastest cache. Many processors split L1 into **instruction cache** and **data cache**. The instruction cache stores recently fetched instructions, while the data cache stores recently accessed data.

**L2 cache - Level 2 cache** is usually larger than L1 but slower. It may be private to one CPU core or shared by a small group of cores.

**L3 cache - Level 3 cache** is usually larger again and often shared among multiple CPU cores or clusters. It is slower than L1/L2 but still much faster than off-chip DRAM.

Cache is **hardware-managed**. Software normally does not manually decide every cache line. The cache controller automatically checks whether requested data is present. If present, it is a **cache hit**. If absent, it is a **cache miss**, and data must be fetched from lower memory.

Why caches are there:

- To reduce average memory-access latency.
- To reduce traffic to off-chip DRAM.
- To exploit temporal locality: recently used data may be used again.
- To exploit spatial locality: nearby addresses may be used soon.
- To keep the CPU from waiting too often for slow main memory.

Important exam point: **Caches improve average performance but do not always give predictable latency**, because a cache hit is fast but a cache miss is slower. This matters in real-time systems.

##### 2. Scratchpad Memory

**Scratchpad memory** is fast on-chip SRAM that is directly addressed by software. Unlike cache, it is usually **software-managed**, not automatically filled by hardware.

Software, firmware or compiler decides what data/code should be placed in scratchpad memory. For example, a signal-processing routine may place frequently used coefficients, small arrays or temporary buffers in scratchpad memory.

Why scratchpad memory is there:

- It gives predictable access time.
- It avoids cache-miss uncertainty.
- It can reduce energy because accesses stay on-chip.
- It is useful in DSP, embedded and real-time systems.
- It lets software explicitly control important data placement.

Difference from cache:

```text
Cache       = hardware decides what is stored.
Scratchpad  = software/compiler decides what is stored.
```

Exam line: **Scratchpad memory is software-managed on-chip SRAM used for fast and predictable access to selected code or data.**

##### 3. TCM - Tightly Coupled Memory

**TCM - Tightly Coupled Memory** is on-chip memory connected very closely to the processor core, often through a dedicated low-latency path rather than through the normal cache hierarchy or shared interconnect.

TCM is common in microcontrollers and real-time processors. It may be divided into:

- **ITCM - Instruction Tightly Coupled Memory**: stores time-critical instructions.
- **DTCM - Data Tightly Coupled Memory**: stores time-critical data.

TCM is usually deterministic. That means access time is known and predictable. This is why it is valuable in real-time control systems, motor control, automotive systems and interrupt-heavy embedded systems.

Why TCM is there:

- To provide guaranteed low-latency access.
- To avoid cache misses for critical code/data.
- To support real-time deadlines.
- To give the CPU a private fast memory path.

Difference from scratchpad: both are software-managed fast memories, but TCM is usually more tightly connected to the CPU and designed for deterministic processor access. Scratchpad is a more general term for software-managed local SRAM.

Exam line: **TCM is tightly connected on-chip memory used for deterministic low-latency instruction or data access in real-time processors.**

##### 4. Register Files

A **register file** is a small, very fast storage array inside a processor, DSP, GPU, accelerator or peripheral. It holds operands, temporary values, architectural registers or internal state.

Register files are closer to computation than cache or SRAM memories. For example, when the CPU executes an instruction such as addition, the operands are often read from the CPU register file, processed by the ALU, and the result is written back to the register file.

Why register files are there:

- To provide extremely fast operand access.
- To support multiple reads/writes per cycle.
- To hold current working values near the execution units.
- To reduce the need to access memory for every operation.

Important distinction:

```text
Register file = inside CPU/accelerator execution datapath.
SRAM cache    = near CPU but outside the core datapath.
DRAM          = main memory, usually off-chip.
```

Exam line: **A register file is a very small and very fast storage structure inside a processor or accelerator used to hold operands and temporary state for immediate computation.**

##### 5. FIFOs - First-In First-Out Buffers

**FIFO** means **First-In First-Out**. A FIFO is a buffer where the first data item written is the first data item read. It preserves order.

FIFOs are used when two blocks communicate at different rates or in different clock domains. For example, a producer may generate data faster than a consumer can accept it. The FIFO temporarily stores data so the producer and consumer do not need to operate in perfect lockstep.

FIFOs may be:

- **Synchronous FIFO**: read and write sides use the same clock.
- **Asynchronous FIFO**: read and write sides use different clocks, useful for clock-domain crossing.

Why FIFOs are there:

- To absorb bursty traffic.
- To match producer/consumer speeds.
- To preserve data order.
- To safely pass data between clock domains.
- To decouple modules connected by streaming interfaces.

Examples: UART receive buffer, network packet pipeline, DMA stream buffer, audio sample buffer, video line buffer.

Exam line: **A FIFO is an ordered on-chip buffer that decouples producer and consumer blocks and is often used for streaming data or clock-domain crossing.**

##### 6. Packet Buffers

A **packet buffer** is memory used to temporarily store packets or frames in communication/networking systems. It may store Ethernet packets, wireless frames, USB packets, PCIe packets or NoC flits.

Packet buffers are usually SRAM because packet handling requires fast read/write access. A network interface may receive a packet, store it in a packet buffer, inspect headers, modify metadata and then transmit or DMA the packet to system memory.

Why packet buffers are there:

- To handle bursty network/communication traffic.
- To store packets while headers are processed.
- To absorb speed mismatch between input link, processor and memory.
- To support retransmission, queueing or priority scheduling.
- To prevent packet loss when downstream logic is temporarily busy.

Exam line: **Packet buffers are SRAM-based temporary storage used in communication blocks to hold packets while they are processed, queued or transferred.**

##### 7. Lookup Tables

A **lookup table** is memory that stores precomputed values so hardware or software can read a result instead of recalculating it.

Lookup tables are used when a function is expensive to compute but easy to store. For example, a graphics block may use lookup tables for gamma correction, a DSP may use sine/cosine tables, and a network block may use tables for address translation, routing or classification.

Why lookup tables are there:

- To reduce computation time.
- To simplify hardware logic.
- To improve throughput.
- To store configuration, coefficients or mapping information.
- To support fast decisions in networking, DSP and graphics pipelines.

Lookup tables may be implemented using ROM if values are fixed, or SRAM if values must be updated at run time.

Exam line: **A lookup table stores precomputed or configurable values so the SoC can replace slow computation with fast memory access.**

##### 8. Small Real-Time Data Buffers

**Small real-time data buffers** are small on-chip memories used to hold time-critical data that must be available within a predictable deadline.

Examples include:

- sensor samples,
- control-loop variables,
- audio samples,
- motor-control data,
- interrupt data,
- real-time communication buffers,
- safety-critical status data.

They are usually implemented using SRAM because SRAM gives fast and predictable access. In real-time systems, predictability may matter more than average speed. A cache may be fast on average, but a cache miss can create an unpredictable delay. A small SRAM buffer or TCM can provide fixed access time.

Why these buffers are there:

- To meet real-time deadlines.
- To avoid unpredictable cache-miss delays.
- To keep urgent data close to the CPU or accelerator.
- To reduce access energy and latency.
- To protect critical data from memory-contention delays.

Exam line: **Small real-time data buffers are fast on-chip SRAM buffers used to store deadline-critical data with predictable access latency.**

#### Quick Comparison

| Memory Structure | Managed By | Typical Location | Main Purpose |
|---|---|---|---|
| L1/L2/L3 cache | Hardware cache controller | Near CPU/core cluster | Improve average memory performance |
| Scratchpad memory | Software/compiler | On-chip SRAM region | Predictable software-controlled storage |
| TCM - Tightly Coupled Memory | Software/system configuration | Dedicated CPU local memory path | Deterministic real-time access |
| Register file | CPU/accelerator datapath | Inside processor/accelerator | Immediate operand/state storage |
| FIFO | Hardware read/write control | Between producer and consumer blocks | Ordered buffering and rate matching |
| Packet buffer | Communication controller/software | Network/IO subsystem SRAM | Temporary packet/frame storage |
| Lookup table | Hardware/software | ROM or SRAM near user block | Fast precomputed/configurable values |
| Real-time data buffer | Software/hardware | Local SRAM/TCM | Deadline-critical predictable storage |

### SRAM Cell Idea To Draw

```text
        BL                         BLB
        |                           |
       access                    access
        |                           |
      +----+                    +----+
      | Q  |<--- cross-coupled--| QB |
      +----+--- inverters ------+----+
        |                           |
        +---------- WL -------------+

BL/BLB = bit lines
WL     = word line
Q/QB   = stored complementary values
```

This simple cell diagram is useful when asked "memory technology" because it shows why SRAM is fast and refresh-free: data is held by a latch, not by a tiny capacitor.

### DRAM - Dynamic Random Access Memory

**DRAM** stores each bit as charge on a capacitor controlled by an access transistor. It is called dynamic because the charge leaks away and must be refreshed periodically.

Key characteristics:

- Much higher density than SRAM.
- Lower cost per bit than SRAM.
- Volatile.
- Requires refresh.
- Slower access than SRAM.
- More complex timing: activate, read/write, precharge, refresh.
- Needs a memory controller.
- Usually implemented in a process optimized for memory density, not pure logic.

DRAM is used for:

- main memory,
- frame buffers,
- large application data,
- operating-system memory,
- multimedia buffers,
- AI/ML data sets,
- graphics memory.

In SoCs, DRAM is usually off-chip because large DRAM arrays need specialized process technology and large capacity. The SoC contains a DRAM controller and **PHY - Physical Layer** to communicate with external **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory**, **LPDDR - Low-Power Double Data Rate** or **HBM - High Bandwidth Memory**.

### DRAM Cell Idea To Draw

```text
          Bit Line
             |
             |
          +-----+
 WL ---->|  T  |---- Storage capacitor
          +-----+          |
                           C
                           |
                         Ground

T = access transistor
C = capacitor storing charge
```

This diagram helps you explain why DRAM is dense but needs refresh: the bit is stored as charge on a capacitor, and charge leaks over time.

### SDRAM, DDR, LPDDR And HBM

**SDRAM - Synchronous Dynamic Random Access Memory** is a DRAM type that works in synchronization with a clock. Older asynchronous DRAM did not use the same kind of strict clocked command interface. SDRAM improved memory control because the controller could issue commands in a clocked sequence.

In SDRAM, memory is not accessed like a simple array. It is organized internally into **banks**, **rows** and **columns**. Before reading or writing, the controller usually opens a row using an **ACTIVATE** command, then accesses columns using READ or WRITE commands, and later closes the row using a **PRECHARGE** command. Because DRAM cells leak charge, the controller must also issue **REFRESH** commands.

Why SDRAM is used:

- It provides much larger capacity than SRAM.
- It is suitable for main memory.
- It supports burst transfers.
- It allows bank-level parallelism.
- It works with a memory controller that schedules commands.

Exam line: **SDRAM is clock-synchronized DRAM organized into banks, rows and columns, and it requires a controller to issue activate, read/write, precharge and refresh commands.**

#### DDR SDRAM - Double Data Rate SDRAM

**DDR SDRAM** means **Double Data Rate Synchronous Dynamic Random Access Memory**. It is a family of SDRAM interfaces that transfers data on both the rising and falling edges of the clock. This doubles the data-transfer opportunity compared with single-edge transfer.

DDR is usually used as **external main memory** for processors, GPUs, DSPs and accelerators. The SoC does not simply connect to DDR like a normal SRAM. It needs a **DDR memory controller** and a **DDR PHY - Physical Layer**. The controller schedules commands and manages timing. The PHY handles electrical signaling, clocking, training and data capture.

Why DDR is used:

- It gives high capacity at lower cost per bit than SRAM.
- It provides high bandwidth for main memory.
- It supports burst transfers, which match cache-line fills and streaming data.
- It is widely available as off-chip memory.
- DDR generations improve bandwidth, density and signaling.

Important point: DDR still stores data using DRAM capacitor cells. The word DDR mainly describes the **interface behavior**, not a new storage cell.

Exam line: **DDR SDRAM is clocked DRAM that transfers data on both clock edges and is commonly used as high-bandwidth off-chip main memory through a memory controller and PHY.**

#### LPDDR - Low-Power Double Data Rate

**LPDDR** means **Low-Power Double Data Rate**. It is a DDR-family DRAM designed for low energy consumption. It is common in smartphones, tablets, wearables, embedded AI modules, automotive systems and other power-sensitive SoCs.

LPDDR is still DRAM, so it still needs refresh and a memory controller. Its main difference from normal DDR is that it is optimized for lower power operation through lower voltage, low-power modes and mobile-oriented signaling/features.

LPDDR is used when:

- battery life matters,
- standby power matters,
- package size is limited,
- the SoC is mobile or embedded,
- memory bandwidth is needed but power must be controlled.

LPDDR power features may include:

- low operating voltage,
- deep power-down modes,
- self-refresh modes,
- partial-array self-refresh,
- temperature-aware refresh,
- clock stopping or low-power idle states.

Exam line: **LPDDR is low-power DDR DRAM used as external main memory in mobile and embedded SoCs where bandwidth is needed but energy and standby power must be reduced.**

#### HBM - High Bandwidth Memory

**HBM** means **High Bandwidth Memory**. It is a DRAM technology designed for extremely high bandwidth. HBM uses multiple stacked DRAM dies and a very wide interface. It is usually placed close to the processor/accelerator, often in the same package using advanced packaging such as an interposer.

HBM is different from normal DDR/LPDDR mainly in physical organization and interface width. Instead of using a relatively narrower external memory bus at high speed, HBM uses a much wider interface at shorter physical distance. This gives very high bandwidth and better energy per bit for bandwidth-heavy workloads, but it increases packaging cost and design complexity.

HBM is used in:

- GPUs - Graphics Processing Units,
- AI accelerators,
- high-performance computing chips,
- data-center accelerators,
- high-bandwidth networking or scientific computing systems.

Why HBM is used:

- It provides very high memory bandwidth.
- It reduces long board-level memory traces.
- It is efficient for massive parallel data movement.
- It supports bandwidth-hungry accelerators better than ordinary external memory in many cases.

Tradeoff: HBM gives excellent bandwidth but is expensive and package-complex. It is not used in every SoC because many embedded or mobile systems do not need that much bandwidth or cannot afford the packaging cost.

Exam line: **HBM is stacked high-bandwidth DRAM placed close to the processor/accelerator through advanced packaging, mainly used when bandwidth is more important than low cost.**

#### Comparison Of SDRAM, DDR, LPDDR And HBM

| Term | Full Form | Main Idea | Typical Use | Key Tradeoff |
|---|---|---|---|---|
| SDRAM | Synchronous Dynamic Random Access Memory | Clocked DRAM with banks, rows, columns and commands | General DRAM architecture concept | Needs controller, timing and refresh |
| DDR SDRAM | Double Data Rate Synchronous Dynamic Random Access Memory | Transfers data on both clock edges | External main memory for many SoCs | High bandwidth but needs DDR controller/PHY |
| LPDDR | Low-Power Double Data Rate | DDR-family DRAM optimized for lower power | Mobile, embedded and battery-powered SoCs | Lower power, but protocol/power-state control is complex |
| HBM | High Bandwidth Memory | Stacked DRAM with very wide interface | GPU, AI and HPC accelerators | Very high bandwidth, but expensive advanced packaging |

Final memory line: **SDRAM is the clocked DRAM base idea; DDR increases transfer rate; LPDDR reduces power; HBM increases bandwidth using stacked DRAM and wide interfaces.**

Exam line: **DDR, LPDDR and HBM are not different basic storage principles from DRAM; they are DRAM interface, power and packaging families optimized for bandwidth, power or physical integration.**

### eDRAM - Embedded DRAM

**eDRAM** means embedded DRAM. It integrates DRAM-like storage on the same die or package context as logic. It is denser than SRAM but more difficult to integrate because DRAM process requirements differ from logic process requirements.

Advantages:

- Higher density than SRAM.
- Potentially useful for large on-chip cache or frame buffers.
- Lower leakage per bit than SRAM in some cases.

Disadvantages:

- Needs refresh.
- Process integration is harder.
- Access time is generally slower than SRAM.
- Design and verification complexity are higher.

eDRAM is a middle option: denser than SRAM but less simple and less universally available in logic processes.

### ROM - Read Only Memory

**ROM** stores fixed data or program code that does not change during normal operation. It is non-volatile.

Types:

- **Mask ROM**: programmed during fabrication.
- **PROM/OTP**: programmable once.
- **EEPROM**: electrically erasable and programmable, but slower and limited endurance.

ROM is used in SoCs for:

- bootloader code,
- reset vectors,
- microcode,
- security keys in special protected forms,
- fixed lookup tables,
- calibration constants.

ROM is small, reliable and non-volatile, but inflexible. If boot ROM code has a bug, it usually cannot be changed after fabrication. Therefore, many SoCs use a small ROM only for secure first-stage boot and load larger firmware from Flash.

### NOR Flash

**NOR Flash** is non-volatile memory often used for boot code and firmware. It supports random read access better than NAND and can support execute-in-place in many embedded systems.

Key characteristics:

- Non-volatile.
- Good random read behavior.
- Suitable for boot and code storage.
- More expensive per bit than NAND.
- Slower write/erase compared with RAM.
- Limited write/erase endurance.

NOR Flash is used when the system must start quickly and read code reliably. It is common for boot code, firmware, BIOS-like storage, automotive controllers and embedded systems.

### NAND Flash

**NAND Flash** is non-volatile memory optimized for high density and low cost per bit. It is used for storage rather than direct code execution.

Key characteristics:

- Very high density.
- Low cost per bit.
- Non-volatile.
- Page/block-based access.
- Slower random read than NOR.
- Writes and erases are more complex.
- Limited endurance.
- Requires **ECC - Error Correction Code**, bad-block management and wear leveling.
- Often managed through controllers in **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** or SSDs.

NAND stores more bits per cell in variants:

- **SLC - Single-Level Cell**: one bit per cell; high endurance and performance.
- **MLC - Multi-Level Cell**: two bits per cell; higher density, lower endurance than SLC.
- **TLC - Triple-Level Cell**: three bits per cell; higher density, lower endurance/performance.
- **QLC - Quad-Level Cell**: four bits per cell; very high density, stronger latency/endurance tradeoff.

Exam line: **NAND Flash gives storage density; NOR Flash gives better code-read and boot behavior.**

### pSRAM, nvSRAM And F-RAM

**pSRAM - pseudo-Static Random Access Memory** behaves like SRAM from the interface side but internally uses DRAM-like storage. It is useful when the designer wants a simpler SRAM-like interface with higher density than pure SRAM.

**nvSRAM - non-volatile Static Random Access Memory** combines SRAM-like operation with non-volatile backup storage. It is used when fast writes and non-volatility are both required.

**F-RAM / FRAM - Ferroelectric Random Access Memory** is non-volatile and has very low power and high endurance compared with many Flash use cases. It is useful in data logging, metering and systems where small non-volatile writes happen frequently.

These are less common than SRAM/DRAM/Flash in general SoC discussions, but mentioning them shows broad awareness of memory technologies.

### Emerging Non-Volatile Memories

Emerging memories try to combine the speed of RAM with non-volatility.

Examples:

- **MRAM - Magnetoresistive Random Access Memory**: non-volatile, good endurance, promising for embedded NVM.
- **ReRAM / RRAM - Resistive Random Access Memory**: stores data using resistance states.
- **PCM / PRAM - Phase-Change Memory / Phase-Change Random Access Memory**: stores data using material phase changes.

These technologies are important because they may reduce leakage, enable instant-on systems and replace some embedded Flash or SRAM use cases. However, they have tradeoffs in write energy, endurance, process maturity, cost and availability.

### Memory Technology Comparison Table

| Technology | Volatile? | Speed | Density | Power Concern | Typical SoC Use | Main Limitation |
|---|---|---|---|---|---|---|
| Register file | Yes | Highest | Very low | Area and dynamic power | CPU datapath | Too costly for large storage |
| SRAM | Yes | Very high | Low | Leakage and area | Cache, TCM, scratchpad, FIFO | Large area per bit |
| eDRAM | Yes | Medium-high | Medium-high | Refresh | large on-chip cache/buffer | Process and refresh complexity |
| DRAM / DDR | Yes | Medium | High | Refresh, I/O power | off-chip main memory | controller and latency |
| LPDDR | Yes | Medium | High | optimized for low power | mobile/embedded main memory | lower-power tradeoffs, protocol support |
| HBM | Yes | Very high bandwidth | High | package complexity | GPU/AI/HPC SoCs | cost and integration complexity |
| ROM | No | Medium-fast read | High | inflexible updates | boot code, fixed tables | cannot update easily |
| NOR Flash | No | good random read | Medium | write/erase energy | boot firmware, XIP | cost/bit higher than NAND |
| NAND Flash | No | good sequential/storage | Very high | ECC/wear management | mass storage, eMMC/UFS | controller required, endurance |
| FRAM/MRAM/ReRAM | No | varies | varies | write energy/endurance tradeoffs | embedded NVM, logs, instant-on | maturity/cost/process availability |

### Memory Technology Selection In SoC

SoC designers choose memory technology based on workload and constraints.

For a small microcontroller SoC:

- ROM or Flash stores program code.
- SRAM stores stack, heap and variables.
- small cache may not be needed.
- low power and deterministic latency matter.

For a smartphone SoC:

- boot ROM starts the system.
- SRAM caches and TCM support processors and DSPs.
- LPDDR provides large low-power main memory.
- NAND/UFS stores OS, apps, media and user data.

For an AI accelerator:

- SRAM buffers hold weights and activations near compute units.
- HBM or LPDDR provides high external bandwidth.
- DMA and memory controllers feed compute arrays.
- memory bandwidth and data reuse dominate performance.

For a networking SoC:

- SRAM/QDR SRAM may be used for fast packet buffers and tables.
- DRAM stores large queues and packet memory.
- Flash stores firmware.
- memory latency and random transaction rate are important.

### Relationship With Memory Controller Architecture

Memory technology directly affects the memory controller.

For SRAM:

- controller is simple.
- access is random and low latency.
- no refresh required.
- timing is relatively straightforward.

For **DRAM - Dynamic Random Access Memory**, **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory** and **LPDDR - Low-Power Double Data Rate**:

- controller must handle activate, read, write, precharge and refresh.
- controller must obey timing parameters.
- bank scheduling matters.
- row-buffer hits and misses affect latency.
- **PHY - Physical Layer** calibration/training may be required.
- power-down/self-refresh modes must be controlled.

For NAND Flash:

- controller must handle pages and blocks.
- **ECC - Error Correction Code** is essential.
- bad-block management is required.
- wear leveling is required.
- garbage collection and mapping layers may be required.

For NOR Flash:

- controller is simpler for reads.
- writes and erases still need command sequences and timing.
- **XIP - Execute In Place** support may be needed for code execution.

Exam line: **The memory controller is simple for SRAM, timing-oriented for DRAM, and management-heavy for NAND Flash.**

### Common Mistakes To Avoid

Do not write:

- "SRAM is non-volatile." It is volatile.
- "DRAM does not need refresh." DRAM needs refresh.
- "Flash is used like normal RAM." Flash writes/erases are slow and endurance-limited.
- "NAND and NOR are the same." NOR is better for code/boot reads; NAND is better for dense storage.
- "On-chip memory is always better." On-chip memory is faster but limited by die area and process cost.
- "Cache and memory are separate from SoC design." Cache, scratchpad and memory controller are central SoC design decisions.

<a id="topic-1-final-answer"></a>

### Final Exam-Ready Answer

Memory technology in SoC design refers to the different physical and architectural memory types used to store instructions, data, buffers, firmware and persistent information. A modern SoC does not use only one memory. It uses a hierarchy of technologies such as registers, SRAM caches, scratchpads, ROM, embedded memory, off-chip DRAM, **LPDDR - Low-Power Double Data Rate** and Flash. The choice of memory technology affects performance, area, power, cost, bandwidth, latency, reliability and memory-controller complexity.

The fastest memories are register files and SRAM. SRAM is volatile and stores data using latch-based cells, so it does not need refresh. It has low latency and high random-access speed, which makes it suitable for caches, scratchpads, tightly coupled memories, FIFOs and small on-chip buffers. However, SRAM has large area per bit and high cost per bit, so it cannot economically provide very large memory capacity.

DRAM stores data as charge on a capacitor and therefore needs periodic refresh. It is denser and cheaper per bit than SRAM but slower and more complex to control. In SoCs, large main memory is usually implemented using off-chip **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory** or **LPDDR - Low-Power Double Data Rate** DRAM because very large memory capacity cannot be placed efficiently on the logic die. LPDDR is especially useful in mobile and low-power SoCs because it operates at lower voltage and includes power-saving modes. **eDRAM - Embedded Dynamic Random Access Memory** is a compromise technology that offers higher density than SRAM on-chip, but it needs refresh and is harder to integrate with logic processes.

Non-volatile memories are used for boot code, firmware and persistent storage. ROM stores fixed code such as reset vectors and bootloaders, but it is not flexible after fabrication. NOR Flash is suitable for boot code, firmware and execute-in-place applications because it has good random read behavior. NAND Flash provides much higher density and lower cost per bit, so it is used for mass storage such as **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** and SSDs. However, NAND requires a controller for **ECC - Error Correction Code**, bad-block management and wear leveling.

The main memory-technology tradeoffs are speed versus density, capacity versus area, volatility versus persistence, bandwidth versus power and simplicity versus controller complexity. On-chip SRAM gives fast and predictable access but consumes die area. Off-chip DRAM gives large capacity but adds latency, pins, I/O power and a complex controller. Flash gives non-volatile storage but has limited write endurance and slower erase/write behavior. Therefore, SoC memory design combines multiple technologies to satisfy performance, power and cost requirements.

Thus, memory technology selection is a central part of SoC design. It determines not only where data is stored, but also how the processor, interconnect, DMA engines and memory controller are designed. A good SoC memory system uses fast SRAM close to computation, dense DRAM for main memory and non-volatile memory for boot and storage.

### Short 10-Mark Exam Answer

Memory technology in SoC design means the type of memory used for storing program code, data, buffers and persistent information. Different memory technologies are used because no single memory is best in speed, density, power, area and cost.

SRAM is volatile, fast and does not require refresh. It is used for caches, scratchpads, register files and on-chip buffers, but it has large area per bit. DRAM is volatile and stores data as charge on a capacitor, so it needs refresh. It is denser and cheaper than SRAM, so it is used as main memory, usually off-chip as **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory** or **LPDDR - Low-Power Double Data Rate**. LPDDR is preferred in low-power SoCs. **eDRAM - Embedded Dynamic Random Access Memory** provides higher density than SRAM on-chip but needs refresh and special process support.

ROM and Flash are non-volatile memories. ROM stores fixed boot code or tables. NOR Flash is used for boot and firmware because it supports fast random reads and execute-in-place style usage. NAND Flash is used for high-density storage such as **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** and SSDs, but it needs **ECC - Error Correction Code**, bad-block management and wear leveling.

The main tradeoffs in memory technology are latency, bandwidth, density, power, volatility, endurance, reliability and process compatibility. Therefore, an SoC normally uses a memory hierarchy: fast SRAM near the processor, larger DRAM for main memory and non-volatile Flash/ROM for boot and storage. The selected memory technology also determines the complexity of the memory controller.

<a id="topic-1-technical-words"></a>

### Technical Words To Use For Marks

- **Memory technology** (write this because the question asks about the physical/architectural memory types used in SoC.)
- **Volatile memory** (write this because SRAM and DRAM lose data when power is removed.)
- **Non-volatile memory** (write this because ROM and Flash retain boot code and persistent data.)
- **SRAM - Static Random Access Memory** (write this because it is the main fast on-chip memory technology.)
- **DRAM - Dynamic Random Access Memory** (write this because it is the main high-density memory technology.)
- **eDRAM - Embedded DRAM** (write this because it shows the intermediate option between SRAM and off-chip DRAM.)
- **ROM - Read Only Memory** (write this because SoCs often use ROM for fixed boot code.)
- **NOR Flash** (write this because it is used for boot, firmware and random-read code storage.)
- **NAND Flash** (write this because it is used for high-density storage and needs controller management.)
- **LPDDR - Low-Power Double Data Rate** (write this because low-power SoCs use lower-voltage DRAM interfaces.)
- **HBM - High Bandwidth Memory** (write this because bandwidth-hungry SoCs such as AI/GPU designs may use stacked DRAM.)
- **Scratchpad memory** (write this because SoCs can use software-managed memory for predictable access.)
- **Cache memory** (write this because hardware-managed SRAM reduces average memory latency.)
- **TCM - Tightly Coupled Memory** (write this because real-time SoCs use predictable low-latency local memory.)
- **Latency** (write this because memory speed is judged by access delay.)
- **Bandwidth** (write this because multimedia/AI SoCs need high data movement rate.)
- **Density** (write this because it explains why DRAM/NAND store more bits per area than SRAM.)
- **Cost per bit** (write this because memory choice is strongly economic.)
- **Leakage power** (write this because on-chip SRAM can consume standby power.)
- **Refresh** (write this because DRAM/eDRAM need periodic restoration of stored charge.)
- **Endurance** (write this because Flash and some NVMs have limited write/erase cycles.)
- **Retention** (write this because non-volatile memories must retain data without power.)
- **ECC - Error Correction Code** (write this because DRAM and NAND systems often need error protection.)
- **Wear leveling** (write this because NAND writes must be distributed to avoid early block failure.)
- **Bad-block management** (write this because NAND cannot assume every block remains usable.)
- **Process compatibility** (write this because DRAM and Flash may not integrate easily with logic CMOS.)
- **On-chip memory** (write this because it gives low latency but limited capacity.)
- **Off-chip memory** (write this because it gives large capacity but requires pins/controller/PHY.)
- **Memory controller** (write this because the selected memory technology determines controller complexity.)

<a id="topic-1-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 124230.png](<images/Screenshot 2026-05-12 124230.png>) contains the exact syllabus headline for this topic. Use it only for topic tracking, not as an exam diagram.
2. **Memory technology pyramid**: Draw the pyramid from registers/SRAM at the top to DRAM/Flash at the bottom. This is the best exam figure for memory technology.
3. **On-chip/off-chip memory diagram**: Draw CPU/cache/on-chip SRAM connected to memory controller and off-chip DRAM/Flash. This shows why memory technology affects SoC architecture.
4. **SRAM cell and DRAM cell diagrams**: Draw these if the question asks for memory technologies at circuit level.
5. **Course figure/source to look at**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.13](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=13>) because it shows storage as a SoC design decision involving size, volatility and on-die/off-die choice.
6. **Course source to look at**: [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22 because it explains why memory may be on-chip or off-chip.

---

<a id="topic-2"></a>

## Topic 2: Memory Design Hierarchy and Tradeoffs

<a id="topic-2-question"></a>

### Question

**Explain memory design hierarchy and tradeoffs in SoC memory design.**

### CLO Mapping

This topic belongs to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

Reason: **Memory design hierarchy and tradeoffs** is directly listed under **SoC Memory Design** in the syllabus. It asks how different memory levels are arranged in an SoC and what tradeoffs are made among speed, capacity, cost, power, latency, bandwidth and predictability.

### What The Question Is Asking

The examiner is not asking only for a generic memory pyramid. The answer should explain why SoCs use multiple memory levels, how each level contributes to performance, and what design tradeoffs decide whether memory should be register, cache, scratchpad, on-chip SRAM, eDRAM, off-chip DRAM or Flash.

For full marks, answer in this order:

1. Define memory hierarchy in SoC.
2. Explain why hierarchy is needed.
3. Draw a memory hierarchy diagram.
4. Explain each level: registers, cache, scratchpad/TCM, on-chip SRAM/ROM, eDRAM, off-chip DRAM and non-volatile memory.
5. Explain tradeoffs: latency, bandwidth, capacity, area, power, cost, predictability, programmability and controller complexity.
6. Mention cache hit/miss, locality and miss penalty.
7. Connect hierarchy to memory-controller architecture.

<a id="topic-2-explanation"></a>

### Core Idea

**Memory hierarchy** is the layered arrangement of memories in an SoC, ordered from fastest and smallest storage near the processor to slower and larger storage farther away. The goal is to make the system behave as if it has both fast access and large capacity, even though no single memory technology provides both.

The core tradeoff is:

```text
Closer to CPU/accelerator = faster, smaller, costlier per bit, lower latency
Farther from CPU/accelerator = slower, larger, cheaper per bit, higher latency
```

SoC memory hierarchy exists because processor and accelerator speeds are much higher than main-memory access speeds. If every instruction and data access went directly to off-chip DRAM, the processor would stall frequently. Therefore, small fast memories are placed close to compute units, and large dense memories are placed farther away.

### PPT / Lecture Citation

The exact topic headline is visible in [Screenshot 2026-05-12 124327.png](<images/Screenshot 2026-05-12 124327.png>). The supporting PPT/lecture PDF is [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>), which states that SoC applications can range from simple on-chip ROM/RAM systems to systems needing large off-chip memory, MMU and cache hierarchy. The same PPT continues on p.21 and p.22 explaining why all memory cannot simply be placed on die. For processor-side effect, [SOC components -processor.pdf, p.18](<System on chip/SOC components -processor.pdf#page=18>) says every processor has a memory system and faster cache/memory reduces instruction-fetch and data-fetch cycles.

### Figure 1: SoC Memory Hierarchy

Draw this figure in the exam.

```text
Fastest / smallest / most expensive per bit
                 ^
                 |
          +---------------+
          | CPU Registers |
          +---------------+
          | L1 I/D Cache  |
          +---------------+
          | L2 / L3 Cache |
          +---------------+
          | TCM /         |
          | Scratchpad    |
          +---------------+
          | On-chip SRAM  |
          | ROM / eDRAM   |
          +---------------+
          | Off-chip DRAM |
          | DDR / LPDDR   |
          +---------------+
          | Flash / UFS / |
          | eMMC / SSD    |
          +---------------+
                 |
                 v
Slowest / largest / cheapest per bit
```

Figure source: cite [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22 for the on-chip/off-chip memory hierarchy idea. Also cite [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.159](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=159>) for the two-level cache hierarchy figure involving processor, L1, L2 and memory. This figure is needed because it shows the basic speed-capacity-cost tradeoff visually.

### Why Memory Hierarchy Is Needed

A memory hierarchy is needed because memory technologies have conflicting properties.

Fast memory such as registers and SRAM has low latency, but it occupies large silicon area and is expensive per bit. Dense memory such as DRAM and NAND Flash stores many bits cheaply, but it is slower and needs controllers. Non-volatile memory stores data without power, but it has slower writes, limited endurance or erase constraints.

If an SoC used only SRAM:

- it would be fast,
- but area and cost would become too large,
- and capacity would be limited.

If an SoC used only DRAM:

- capacity would be high,
- but processor latency would be too high,
- and every access would need a complex controller.

If an SoC used only Flash:

- data would be non-volatile,
- but writes would be slow,
- endurance would be limited,
- and it would not support normal high-speed computation.

Therefore, SoCs use a hierarchy: fast memories for active computation, larger memories for working data and non-volatile memories for boot and storage.

### Locality: The Principle Behind Cache Hierarchy

Cache hierarchy works because programs show **locality**.

1. **Temporal locality**: if data or instruction is used now, it is likely to be used again soon.
2. **Spatial locality**: if one address is accessed, nearby addresses are likely to be accessed soon.
3. **Sequential locality**: instructions are often fetched from consecutive addresses.

Because of locality, a small cache can satisfy many accesses. When the requested data is found in cache, it is a **cache hit**. When it is not found, it is a **cache miss**, and the data must be fetched from a lower memory level. The time penalty for doing this is called **miss penalty**.

Exam line: **Memory hierarchy reduces average memory access time by exploiting locality.**

### Memory Hierarchy Levels In SoC

### 1. Register File

Registers are the closest storage to the processor execution units. They are extremely fast and are accessed directly by instructions. However, they are very small and expensive in area.

Use:

- operands,
- addresses,
- status values,
- temporary computation data.

Tradeoff:

- best speed,
- very small capacity,
- high area cost per bit.

### 2. L1 Cache

L1 cache is the first cache level and is usually split into instruction cache and data cache. It is made using SRAM and is designed for very low latency.

Use:

- recently used instructions,
- recently used data,
- reducing instruction fetch and data fetch delay.

Tradeoff:

- very fast,
- limited capacity,
- more area and power per bit,
- may create unpredictability due to misses.

L1 is often split into **I-cache** and **D-cache** because instruction fetch and data access can occur in parallel. This increases bandwidth but may slightly reduce flexibility compared with a unified cache.

### 3. L2 / L3 Cache

L2 and L3 caches are larger but slower than L1. They reduce the number of expensive accesses to off-chip memory.

Use:

- shared data among cores,
- larger working sets,
- reducing DRAM traffic,
- improving average memory access time.

Tradeoff:

- larger capacity than L1,
- lower miss rate,
- higher latency than L1,
- increased area and coherence complexity.

In multi-core SoCs, L2 or L3 may be shared. Shared cache improves communication and reduces off-chip bandwidth demand, but it also introduces cache-coherency and arbitration issues.

### 4. Scratchpad Memory / TCM

**Scratchpad memory** is software-managed on-chip SRAM. **TCM** means **Tightly Coupled Memory**. Unlike cache, scratchpad/TCM is not automatically managed by hardware. Software or compiler decides what data goes there.

Use:

- real-time code,
- interrupt handlers,
- DSP kernels,
- predictable buffers,
- critical loops.

Tradeoff:

- predictable latency,
- no cache-miss uncertainty,
- lower hardware complexity than cache,
- but requires software/compiler management.

This is especially important in real-time SoCs. A cache miss can create unpredictable delay, but TCM access can be deterministic.

### 5. On-Chip SRAM / ROM / eDRAM

On-chip memory sits on the SoC die. It may include SRAM, ROM, eDRAM, FIFOs and local buffers.

Advantages:

- low latency,
- high bandwidth,
- no board-level I/O delay,
- lower access energy than off-chip memory,
- useful for accelerators and DMA buffers.

Disadvantages:

- limited by die area,
- increases chip cost,
- leakage can be significant,
- DRAM/eDRAM may need process support and refresh.

The PPT states that putting memory on the die improves access time and bandwidth, but also points out the problems: DRAM process technology differs from processor process technology and on-die memory capacity is limited.

### 6. Off-Chip DRAM / LPDDR

Off-chip **DRAM - Dynamic Random Access Memory** provides large main memory. It is usually accessed through a memory controller and **PHY - Physical Layer**.

Use:

- operating system memory,
- application memory,
- frame buffers,
- large data sets,
- multimedia/AI workloads.

Tradeoff:

- large capacity,
- lower cost per bit,
- higher latency,
- high I/O power,
- needs memory controller,
- affected by bank conflicts, refresh and scheduling.

**LPDDR - Low-Power Double Data Rate** is commonly used in mobile SoCs because it offers lower-power DRAM operation compared with high-performance desktop/server-style DDR choices.

### 7. Non-Volatile Memory

Flash, ROM, **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** and SSD-like storage sit lower in the hierarchy.

Use:

- boot code,
- firmware,
- file system,
- OS image,
- user data,
- persistent logs.

Tradeoff:

- retains data without power,
- high density,
- slow writes/erases,
- limited endurance,
- often needs ECC, wear leveling and bad-block management.

### Figure 2: Cache-Based Memory Hierarchy

Use this if the question focuses more on processor-memory performance.

```text
                 +-----------+
                 | Processor |
                 +-----+-----+
                       |
                       v
              +----------------+
              | L1 I/D Cache   |
              | fastest SRAM   |
              +-------+--------+
                      |
                      v
              +----------------+
              | L2 / L3 Cache  |
              | larger SRAM    |
              +-------+--------+
                      |
                      v
              +----------------+
              | Memory Ctrl    |
              +-------+--------+
                      |
                      v
              +----------------+
              | DRAM / LPDDR   |
              +----------------+
```

Figure source: cite [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.159](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=159>) because it shows processor, L1 cache, L2 cache and memory. This is useful because it directly supports the L1-L2-memory hierarchy answer.

### Major Tradeoffs In Memory Hierarchy

### 1. Latency Vs Capacity

Small memories are usually faster. Large memories are usually slower.

Example:

- registers and L1 cache are very fast but small;
- DRAM is large but slower;
- Flash is larger and persistent but much slower for writes.

So the hierarchy places small fast memory near the processor and large slow memory farther away.

### 2. Bandwidth Vs Cost

High bandwidth requires wide data paths, multiple banks, interleaving, multi-port memories, high-speed PHYs or stacked memory. These increase area, power and cost.

Example:

- HBM gives high bandwidth but increases package complexity and cost.
- LPDDR gives lower power but still needs controller/PHY complexity.
- On-chip SRAM gives high bandwidth but consumes die area.

### 3. Area Vs Performance

Increasing cache size usually reduces miss rate, but consumes more die area and may increase access time. A very large L1 cache may become slower, defeating its purpose. Therefore, L1 is kept small and fast, while L2/L3 are made larger and slower.

Exam line: **A larger cache can reduce miss rate but may increase hit time, area and power.**

### 4. Power Vs Speed

Fast memories and high-bandwidth interfaces consume power. Off-chip memory access is often much more energy-expensive than on-chip SRAM access because it drives package pins and board traces.

Power tradeoffs include:

- dynamic power per access,
- leakage power in SRAM,
- refresh power in DRAM,
- I/O power for off-chip memory,
- standby/self-refresh modes.

### 5. Predictability Vs Average Performance

Cache improves average performance but creates variable access time because hits are fast and misses are slow. Scratchpad/TCM gives predictable latency but requires explicit software management.

This tradeoff is important in real-time systems:

- cache is good for average throughput,
- TCM/scratchpad is good for deterministic timing.

### 6. Hardware Complexity Vs Software Control

Cache is hardware-managed, so it is easy for programmers but needs tag arrays, replacement policy, coherence handling and miss logic. Scratchpad is simpler in hardware but shifts responsibility to software/compiler.

Tradeoff:

- cache: easier programming, complex hardware, unpredictable misses;
- scratchpad: predictable and simpler hardware, harder software management.

### 7. On-Chip Vs Off-Chip Memory

On-chip memory:

- lower latency,
- higher bandwidth,
- lower access energy,
- limited size,
- increases die area/cost.

Off-chip memory:

- large capacity,
- cheaper per bit,
- higher latency,
- consumes I/O power,
- needs controller and pins.

The PPT directly supports this tradeoff: on-die memory improves memory access time and bandwidth, but capacity and DRAM process mismatch limit how much can be integrated.

### 8. Shared Vs Private Memory

Private memory/cache is close to one core and can be faster. Shared memory/cache allows communication among cores but needs arbitration and coherence.

Private cache advantages:

- low access latency,
- less contention,
- simple local access.
**Arbitration** means the SoC decides **which master gets access first** when multiple cores/masters request the same shared resource at the same time.

Example: Core 0 and Core 1 both request the shared cache/interconnect/DRAM controller. The arbiter grants access to one first, then the other.

**Coherence** means all cores must see a **consistent and updated view of memory**, even when copies of the same data exist in different private caches.

Example: Core 0 updates variable `X` in its private cache. Core 1 must not continue using an old stale copy of `X`; the coherence protocol updates or invalidates Core 1’s copy.

So write it like this:

> Shared memory/cache allows communication among multiple cores, but when many cores request the shared resource simultaneously, **arbitration** is required to decide access priority. Also, because different cores may keep local cached copies of the same data, **cache coherence** is required to ensure that all cores observe a consistent and up-to-date value of shared data.

Shared cache advantages:

- better sharing,
- lower off-chip traffic,
- easier communication.

Shared cache disadvantages:

- contention,
- coherence complexity,
- variable latency.

### 9. Unified Cache Vs Split I/D Cache

Unified cache stores both instructions and data. Split cache separates instruction cache and data cache.

Split I/D cache:

- allows instruction fetch and data access in parallel,
- increases bandwidth,
- common for L1 caches.

Unified cache:

- flexible sharing of capacity between instruction and data,
- common in lower cache levels such as L2/L3.

### 10. Inclusion And Coherence Tradeoff

Multilevel caches may be inclusive, exclusive or non-inclusive.

- **Inclusive cache**: upper-level cache contains copies of lower-level cache lines.
- **Exclusive cache**: data exists in only one level at a time.
- **Non-inclusive cache**: no strict inclusion guarantee.

In multi-core SoCs, cache coherence ensures that all cores see a consistent view of shared memory. Coherence improves programmability but adds hardware complexity and traffic.

### Average Memory Access Time

Use this formula when explaining hierarchy quantitatively:

```text
AMAT = Hit Time + (Miss Rate x Miss Penalty)
```

For two levels:

```text
AMAT = L1 Hit Time
     + L1 Miss Rate x (L2 Hit Time + L2 Miss Rate x Main Memory Penalty)
```

Meaning:

- low hit time is important for the first level;
- low miss rate is important for lower levels;
- miss penalty is large when data must come from off-chip DRAM.

This formula is very useful in exams because it turns the answer from descriptive to analytical.

### Example Tradeoff

Suppose an SoC has:

- small L1 cache: 1-cycle hit time, 8% miss rate;
- larger L1 cache: 2-cycle hit time, 4% miss rate;
- miss penalty: 20 cycles.

Small L1:

```text
AMAT = 1 + (0.08 x 20) = 2.6 cycles
```

Larger L1:

```text
AMAT = 2 + (0.04 x 20) = 2.8 cycles
```

Even though the larger cache has fewer misses, it can be worse if it increases hit time too much. This is a classic memory hierarchy tradeoff.

### Memory Hierarchy And Memory Controller

The memory controller sits between the SoC interconnect/cache subsystem and external memory. Its design depends on the hierarchy.

If the SoC has a large cache:

- DRAM traffic is reduced,
- memory controller pressure is lower,
- average latency improves.

If the SoC has weak caching:

- more requests reach DRAM,
- controller scheduling becomes more important,
- bandwidth bottlenecks become visible.

If the SoC uses scratchpad/TCM:

- software can move critical data closer to compute,
- DRAM accesses become more controlled,
- real-time behavior improves.

If the SoC has multiple masters:

- memory controller must arbitrate among CPU, GPU, DMA, DSP and accelerators,
- quality-of-service may be required,
- starvation must be avoided,
- real-time traffic may need priority.

Thus, memory hierarchy and memory controller architecture cannot be separated. The hierarchy reduces pressure on main memory, and the controller manages the remaining traffic efficiently.

### Common Mistakes To Avoid

- Do not say "bigger cache is always better." Bigger cache may increase hit time, area and power.
- Do not say "on-chip memory is always better." It is faster but capacity-limited and expensive in die area.
- Do not say "cache and scratchpad are the same." Cache is hardware-managed; scratchpad is software-managed.
- Do not ignore miss penalty. A low miss rate still matters because DRAM access is expensive.
- Do not forget predictability. Real-time SoCs may prefer TCM/scratchpad over cache.
- Do not write only SRAM/DRAM definitions. The question asks hierarchy and tradeoffs.

<a id="topic-2-final-answer"></a>

### Final Exam-Ready Answer

Memory design hierarchy in an SoC is the layered organization of memory resources from small, fast memories near the processor to large, slower memories farther away. It usually includes registers, L1 cache, L2/L3 cache, scratchpad or **TCM - Tightly Coupled Memory**, on-chip **SRAM - Static Random Access Memory**, **ROM - Read-Only Memory**, **eDRAM - Embedded Dynamic Random Access Memory**, off-chip **DRAM - Dynamic Random Access Memory** or **LPDDR - Low-Power Double Data Rate** and non-volatile storage such as Flash. The purpose of the hierarchy is to provide low average access time and high bandwidth while still giving the system enough storage capacity at reasonable area, power and cost.

The need for memory hierarchy arises because no single memory technology can satisfy all SoC requirements. Registers and SRAM are very fast but small and expensive per bit. DRAM provides large capacity but has higher latency, refresh overhead and controller complexity. Flash provides non-volatile storage but has slow writes and limited endurance. Therefore, SoCs place small fast memories close to compute units and larger slower memories farther away.

Cache hierarchy works by exploiting locality. Temporal locality means recently used data is likely to be used again. Spatial locality means nearby addresses are likely to be accessed soon. When data is found in cache, it is a hit; when it is absent, it is a miss and must be fetched from a lower memory level. The miss penalty can be large, especially when data comes from off-chip DRAM. Therefore, average memory access time depends on hit time, miss rate and miss penalty.

Different levels of the hierarchy have different roles. L1 cache is small and fast and is often split into instruction and data caches to increase bandwidth. L2 and L3 caches are larger and reduce traffic to main memory. Scratchpad or **TCM - Tightly Coupled Memory** provides deterministic low-latency storage for real-time or critical code but requires software management. On-chip **SRAM - Static Random Access Memory** gives high bandwidth and low latency but increases die area. Off-chip **DRAM - Dynamic Random Access Memory** provides large capacity but needs a memory controller and has higher latency and I/O power. Non-volatile memory stores boot code, firmware and persistent data.

The main tradeoffs in memory hierarchy are latency versus capacity, bandwidth versus cost, area versus performance, power versus speed, predictability versus average performance, hardware complexity versus software control and on-chip versus off-chip placement. A larger cache may reduce miss rate but increase hit time and power. Off-chip memory gives capacity but adds latency and controller complexity. Cache improves average performance but scratchpad/TCM gives predictable timing. Hence, memory hierarchy is a central SoC design decision.

Memory hierarchy also affects memory controller architecture. A strong cache hierarchy reduces the number of requests reaching DRAM, while weak caching increases memory-controller pressure. In multi-master SoCs, the controller must arbitrate among **CPU - Central Processing Unit**, **DMA - Direct Memory Access**, **GPU - Graphics Processing Unit**, **DSP - Digital Signal Processor** and accelerators, and may require **QoS - Quality of Service** policies. Thus, memory hierarchy and memory controller design together determine SoC performance, power and real-time behavior.

### Short 10-Mark Exam Answer

Memory design hierarchy in SoC is the arrangement of different memory levels from fastest and smallest to slowest and largest. A typical SoC hierarchy contains registers, L1 cache, L2/L3 cache, scratchpad or **TCM - Tightly Coupled Memory**, on-chip **SRAM - Static Random Access Memory** / **ROM - Read-Only Memory**, off-chip **DRAM - Dynamic Random Access Memory** / **LPDDR - Low-Power Double Data Rate** and Flash storage. This hierarchy is required because fast memories are expensive and small, while large memories are slower but cheaper per bit.

Cache hierarchy improves average memory access time by exploiting temporal and spatial locality. A cache hit gives fast access, while a cache miss causes a miss penalty because data must be fetched from a lower level such as L2, L3 or DRAM. The average memory access time depends on hit time, miss rate and miss penalty.

The main tradeoffs are latency versus capacity, bandwidth versus cost, area versus performance, power versus speed, predictability versus average performance and on-chip versus off-chip placement. On-chip **SRAM - Static Random Access Memory** gives low latency and high bandwidth but consumes die area. Off-chip **DRAM - Dynamic Random Access Memory** gives large capacity but has higher latency, I/O power and controller complexity. Scratchpad / **TCM - Tightly Coupled Memory** gives predictable timing but needs software management, while cache is hardware-managed but can suffer misses.

Thus, a good SoC memory hierarchy places fast memory near computation, large memory farther away and non-volatile memory for boot/storage. This reduces average access time, improves bandwidth, controls cost and reduces pressure on the memory controller.

<a id="topic-2-technical-words"></a>

### Technical Words To Use For Marks

- **Memory hierarchy** (write this because the question asks for layered memory organization.)
- **Registers** (write this because they are the fastest storage closest to execution units.)
- **L1 cache** (write this because it is the first and fastest cache level.)
- **L2/L3 cache** (write this because larger lower-level caches reduce DRAM traffic.)
- **Scratchpad memory** (write this because it is software-managed on-chip memory used in many SoCs.)
- **TCM - Tightly Coupled Memory** (write this because it gives deterministic low-latency access for real-time code.)
- **On-chip memory** (write this because it gives low latency but increases die area.)
- **Off-chip memory** (write this because it gives capacity but adds latency and controller complexity.)
- **Temporal locality** (write this because cache hierarchy depends on reuse over time.)
- **Spatial locality** (write this because caches fetch blocks/lines containing neighboring addresses.)
- **Cache hit** (write this because a hit is the fast case in cache access.)
- **Cache miss** (write this because a miss forces access to a lower memory level.)
- **Miss penalty** (write this because it explains why off-chip access hurts performance.)
- **AMAT - Average Memory Access Time** (write this because it gives a quantitative memory hierarchy argument.)
- **Hit time** (write this because larger caches can increase hit time.)
- **Miss rate** (write this because cache size/associativity tradeoffs aim to reduce it.)
- **Bandwidth** (write this because SoC multimedia/AI workloads need high data movement rate.)
- **Latency** (write this because memory delay directly affects processor stalls.)
- **Cache coherence** (write this because multi-core SoCs need consistent shared-memory views.)
- **Unified cache** (write this because it stores both instructions and data.)
- **Split I/D cache** (write this because L1 often separates instruction and data caches for bandwidth.)
- **Inclusive cache** (write this because multilevel hierarchy may enforce inclusion.)
- **Predictability** (write this because real-time SoCs may prefer scratchpad/TCM to cache.)
- **Memory controller pressure** (write this because cache hierarchy affects how many requests reach DRAM.)
- **Quality of Service / QoS** (write this because multi-master SoCs may need prioritized memory access.)

<a id="topic-2-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 124327.png](<images/Screenshot 2026-05-12 124327.png>) contains the exact syllabus headline. Use it for topic tracking.
2. **PPT/lecture source to cite**: [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) because it explicitly mentions on-chip ROM/RAM, off-chip memory, MMU and cache hierarchy.
3. **PPT/lecture source to cite**: [module 1 part 1 introduction to system approach.pdf, p.21](<System on chip/module 1 part 1 introduction to system approach.pdf#page=21>) and p.22 because they explain why all memory cannot simply be placed on die.
4. **PPT/lecture source to cite**: [SOC components -processor.pdf, p.18](<System on chip/SOC components -processor.pdf#page=18>) because it says faster cache and memory reduce instruction-fetch and data-fetch cycles.
5. **Memory hierarchy pyramid**: Draw registers, L1, L2/L3, scratchpad/TCM, on-chip SRAM/ROM, off-chip DRAM and Flash.
6. **Cache hierarchy diagram**: Draw processor -> L1 -> L2/L3 -> memory controller -> DRAM. Cite [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.159](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=159>) for the two-level cache hierarchy idea.
7. **AMAT formula**: Write `AMAT = Hit Time + Miss Rate x Miss Penalty` beside the diagram. This helps score because it explains the tradeoff analytically.

---

<a id="topic-3"></a>

## Topic 3: SDRAM Basics - Banked Architecture and Latencies

<a id="topic-3-question"></a>

### Question

**Explain SDRAM basics with banked architecture and latencies.**

### CLO Mapping

This topic belongs to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

Reason: SDRAM basics, banked architecture and latencies are part of the **SoC Memory Design** unit. The topic directly affects memory-controller architecture because the controller must schedule activate, read/write, precharge and refresh commands while respecting SDRAM timing constraints.

### What The Question Is Asking

The examiner wants you to explain how SDRAM is organized internally and why its latency is not a single fixed delay. A good answer should cover rows, columns, banks, row buffers, RAS/CAS, activate, read/write, precharge, refresh, burst transfer, bank interleaving and timing parameters such as CAS latency, RAS-to-CAS delay and precharge time.

For full marks, answer in this order:

1. Define SDRAM.
2. Explain DRAM cell, row and column organization.
3. Explain banked architecture.
4. Explain row buffer and open-row behavior.
5. Explain SDRAM command sequence.
6. Explain important latencies.
7. Explain bank interleaving and burst transfer.
8. Connect SDRAM behavior to memory-controller scheduling.

<a id="topic-3-explanation"></a>

### Core Idea

**SDRAM** means **Synchronous Dynamic Random Access Memory**. It is dynamic because each bit is stored as charge on a capacitor and must be refreshed. It is synchronous because its commands and data transfers are coordinated with a clock.

The important point is this: **SDRAM access time depends on the state of the bank and row being accessed.** If the requested row is already open, the access is faster. If another row is open, the controller must precharge the old row and activate the new row before reading or writing. Therefore, SDRAM latency depends on row hits, row misses, bank conflicts and timing parameters.

### PPT / Book Citation

The direct local source is the Flynn/Luk textbook. [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.167](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=167>) introduces SDRAM and the row/column DRAM array. Pages 168-170 explain RAS, CAS, refresh, chip access time, cycle time and burst/page modes. Pages 171-172 explain DDR SDRAM, multiple arrays/banks and independently activated rows. The relevant PPT context is [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22, which explains why large off-chip memory and cache hierarchy are needed in SoC systems.

### Figure 1: SDRAM Banked Architecture

Draw this figure in the exam.

```text
                 +----------------------+
Address/Command->| SDRAM Command Logic  |
Clock ---------->| ACT / READ / WRITE   |
                 | PRECHARGE / REFRESH  |
                 +----------+-----------+
                            |
        +-------------------+-------------------+
        |                   |                   |
        v                   v                   v
 +-------------+     +-------------+     +-------------+
 | Bank 0      |     | Bank 1      | ... | Bank N      |
 | Row Array   |     | Row Array   |     | Row Array   |
 | Row Buffer  |     | Row Buffer  |     | Row Buffer  |
 +------+------+     +------+------+     +------+------+
        |                   |                   |
        +-------------------+-------------------+
                            |
                            v
                  +------------------+
                  | Column Mux / I/O |
                  | Burst Transfer   |
                  +------------------+
                            |
                            v
                         Data Bus
```

Figure source: cite [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.171](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=171>) and p.172. Those pages discuss DDR SDRAM internal configuration and multiple DRAM arrays/banks. This figure is needed because the banked architecture is the reason SDRAM can overlap or interleave accesses.

### DRAM Cell, Row And Column

Each DRAM cell stores one bit as charge on a capacitor, controlled by an access transistor. Because the stored charge leaks, DRAM must be periodically refreshed.

The memory array is organized as:

- rows,
- columns,
- banks,
- row buffers/sense amplifiers.

To access data, the address is split into row and column parts. First the row is selected. Then the column is selected from that row. In older asynchronous DRAM, row and column addresses are controlled using RAS and CAS. In SDRAM, these actions are represented as clocked commands.

### SDRAM Commands

Important SDRAM commands are:

- **ACTIVATE**: opens a row in a bank and loads it into the row buffer.
- **READ**: reads selected columns from an open row.
- **WRITE**: writes selected columns into an open row.
- **PRECHARGE**: closes the currently open row in a bank.
- **REFRESH**: restores charge in DRAM cells.
- **BURST TERMINATE**: stops a burst operation where supported.
- **NOP**: no operation, used when waiting for timing constraints.

### Row Buffer

When a row is activated, the entire row is sensed into the row buffer. The row buffer acts like a temporary fast storage for the active row.

There are three important cases:

1. **Row hit**: requested data is in the currently open row. This is fastest because no new activate is needed.
2. **Row miss / row conflict**: a different row is open in the same bank. The controller must precharge the old row and activate the new one. This is slow.
3. **Row closed / empty bank**: no row is open. The controller activates the required row and then reads/writes. This is intermediate.

Exam line: **SDRAM latency depends heavily on whether the access is a row hit, row miss or closed-row access.**

### Banked Architecture

Modern SDRAM is divided into multiple banks. Each bank has its own row array and row buffer. Banks allow the memory controller to overlap operations.

For example:

- Bank 0 may be serving a read burst.
- Bank 1 may be precharging.
- Bank 2 may be activating a row.
- Bank 3 may be preparing for the next command.

This improves throughput because the memory controller can hide some timing delays by switching to another bank while one bank is waiting.

### Bank Interleaving

**Bank interleaving** means spreading consecutive or independent memory requests across different banks so that their operations can overlap.

Example:

```text
Time ->
Bank 0: ACT ---- READ burst ---- PRE
Bank 1:      ACT ---- READ burst ---- PRE
Bank 2:           ACT ---- READ burst ---- PRE
Bank 3:                ACT ---- READ burst ---- PRE
```

This increases bandwidth because the bus can remain busy while different banks perform internal row operations.

### Burst Transfer

SDRAM transfers data in bursts. After an initial column address, multiple consecutive data words are transferred. This is efficient because programs often access sequential memory locations and cache lines are filled using bursts.

Burst transfer helps:

- cache-line fill,
- frame-buffer access,
- streaming media,
- DMA transfers,
- graphics and AI workloads.

DDR SDRAM transfers data on both rising and falling clock edges, increasing data rate without requiring the core memory array to run at the same high speed.

### Important SDRAM Latencies

| Timing Term | Meaning | Why It Matters |
|---|---|---|
| **CL / CAS latency** | Delay from READ command to first data | determines visible read latency after row is open |
| **tRCD** | RAS-to-CAS delay; ACTIVATE to READ/WRITE delay | needed after opening a row |
| **tRP** | precharge time; time to close a row before another activate | paid during row conflict |
| **tRAS** | minimum row active time | row must remain active long enough |
| **tRC** | row cycle time; ACTIVATE to next ACTIVATE in same bank | limits repeated row accesses in same bank |
| **tCCD** | column-to-column delay | affects spacing of consecutive column commands |
| **tWR** | write recovery time | delay after write before precharge |
| **tRFC** | refresh cycle time | memory unavailable during refresh |

### Access Case Examples

### 1. Row Hit

```text
READ -> wait CAS latency -> data burst
```

This is fastest because the correct row is already open.

### 2. Closed Row

```text
ACTIVATE -> wait tRCD -> READ -> wait CAS latency -> data burst
```

This is slower than a row hit because the row must first be activated.

### 3. Row Conflict

```text
PRECHARGE -> wait tRP -> ACTIVATE -> wait tRCD
-> READ -> wait CAS latency -> data burst
```

This is the slowest common case because the wrong row was open.

### Figure 2: SDRAM Latency Cases

```text
Row Hit:
READ -------- CL -------- Data

Closed Row:
ACT --- tRCD --- READ --- CL --- Data

Row Conflict:
PRE --- tRP --- ACT --- tRCD --- READ --- CL --- Data
```

This is the best latency diagram to draw because it directly explains why SDRAM access time changes from request to request.

### Role Of Memory Controller

The memory controller converts processor/DMA/accelerator requests into SDRAM commands. It must:

- map addresses to channel/rank/bank/row/column,
- issue ACTIVATE, READ, WRITE, PRECHARGE and REFRESH commands,
- obey timing constraints,
- exploit row-buffer hits,
- use bank interleaving,
- schedule refresh,
- handle read/write turnaround,
- meet QoS or real-time requirements.

Memory-controller scheduling is important because two legal schedules can have very different performance. A good controller keeps banks busy and reduces row conflicts, but must still be fair to all requesters.

<a id="topic-3-final-answer"></a>

### Final Exam-Ready Answer

SDRAM stands for Synchronous Dynamic Random Access Memory. It is dynamic because each bit is stored as charge on a capacitor and must be refreshed periodically. It is synchronous because its operations are controlled by a clock. SDRAM is used as large main memory in SoC systems, usually as off-chip DDR or LPDDR memory connected through a memory controller.

Internally, SDRAM is organized into rows, columns and banks. A memory access first selects a bank and row using an activate command. The selected row is copied into the row buffer. Then a read or write command selects the required column data from that open row. If the next request accesses the same open row, it is called a row hit and is fast. If it accesses a different row in the same bank, the old row must be precharged and the new row must be activated, causing extra latency.

Banked architecture divides SDRAM into multiple banks, each with its own row buffer. This allows the memory controller to interleave requests. While one bank is waiting after activation or precharge, another bank can perform a read or write burst. Thus, bank interleaving improves bandwidth and hides some internal DRAM delays.

The important SDRAM latencies are CAS latency, tRCD, tRP, tRAS, tRC, tWR and tRFC. CAS latency is the delay between a read command and first data. tRCD is the delay between activate and read/write. tRP is the precharge delay needed to close a row. tRAS is the minimum row active time. tRFC is the refresh delay. A row hit only pays read/CAS latency, a closed-row access pays activate plus read latency, and a row conflict pays precharge, activate and read latency.

Therefore, SDRAM performance depends not only on clock frequency but also on bank state, row-buffer locality, burst length, refresh overhead and controller scheduling. A good SoC memory controller maps addresses and schedules commands to maximize row hits, exploit bank parallelism, reduce row conflicts and satisfy latency/bandwidth requirements.

### Short 10-Mark Exam Answer

SDRAM is synchronous dynamic RAM used as large main memory in SoC systems. It stores data in capacitor-based DRAM cells, so it needs refresh. It is organized into banks, rows and columns. To access data, the memory controller activates a row in a bank, then issues read/write commands for columns in that row.

The banked architecture allows multiple banks to operate in an interleaved manner. Each bank has a row buffer. If a request goes to an already open row, it is a row hit and is fast. If another row in the same bank is required, the controller must precharge the old row and activate the new row, causing higher latency. Important latencies include CAS latency, tRCD, tRP, tRAS and refresh latency.

Thus, SDRAM performance depends on row hits, bank conflicts, burst transfer, refresh and memory-controller scheduling. The controller improves performance by exploiting bank interleaving and row-buffer locality.

<a id="topic-3-technical-words"></a>

### Technical Words To Use For Marks

- **SDRAM** (write this because the question is specifically about synchronous DRAM.)
- **DDR SDRAM** (write this because modern SoC DRAM usually transfers data on both clock edges.)
- **Banked architecture** (write this because multiple banks enable interleaving and higher throughput.)
- **Row buffer** (write this because row hits and row conflicts depend on it.)
- **Row hit** (write this because it explains the fastest SDRAM access case.)
- **Row miss / row conflict** (write this because it explains extra precharge and activate delay.)
- **ACTIVATE command** (write this because a row must be opened before column access.)
- **READ/WRITE command** (write this because column access happens after activation.)
- **PRECHARGE command** (write this because a bank must close a row before opening another.)
- **REFRESH command** (write this because DRAM cells leak charge.)
- **CAS latency / CL** (write this because it is the most recognized SDRAM latency.)
- **tRCD** (write this because it is the activate-to-read/write delay.)
- **tRP** (write this because it is the row precharge delay.)
- **tRAS** (write this because it defines minimum row active time.)
- **tRC** (write this because it defines row cycle time.)
- **tRFC** (write this because refresh blocks normal memory access.)
- **Burst length** (write this because SDRAM transfers multiple words per command.)
- **Bank interleaving** (write this because it hides latency and improves bandwidth.)
- **Memory controller** (write this because SDRAM command scheduling is done by the controller.)

<a id="topic-3-diagrams"></a>

### Images / Diagrams To Remember

1. **SDRAM banked architecture**: Draw command logic connected to multiple banks, each with row array and row buffer.
2. **Latency cases**: Draw row hit, closed-row and row-conflict timelines.
3. **Book figure/source to cite**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.167](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=167>) for DRAM row/column organization.
4. **Book figure/source to cite**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.171](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=171>) and p.172 for DDR SDRAM banked architecture.
5. **PPT/lecture source to cite**: [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22 for why SoCs use large off-chip memory and cache hierarchy.

---

<a id="topic-4"></a>

## Topic 4: Quality-Aware Scheduling

<a id="topic-4-question"></a>

### Question

**Explain quality-aware scheduling in SoC memory systems.**

### CLO Mapping

This topic belongs to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

Reason: Quality-aware scheduling is listed under **SoC Memory Design**. It is mainly about how the memory controller schedules requests from multiple SoC masters while satisfying quality requirements such as latency, bandwidth, fairness and deadlines.

### What The Question Is Asking

The examiner is asking how a memory controller decides which memory request should be served first when many masters compete for memory. A good answer should explain QoS, real-time traffic, best-effort traffic, priority, latency, bandwidth, fairness, starvation, row-buffer locality and bank scheduling.

<a id="topic-4-explanation"></a>

### Core Idea

**Quality-aware scheduling** means scheduling memory requests while considering **Quality of Service (QoS)** requirements, not only raw throughput. In an SoC, several masters may request memory at the same time: CPU, GPU, display controller, camera, DMA, DSP, AI accelerator, modem and peripherals. These masters do not all have the same urgency.

Examples:

- Display refresh needs guaranteed bandwidth to avoid frame drop.
- Audio needs regular service to avoid glitches.
- CPU needs low average latency for responsiveness.
- DMA wants high throughput.
- AI accelerator wants large bandwidth.
- Background storage copy can tolerate delay.

Quality-aware scheduling tries to serve these requests so that urgent real-time traffic meets deadlines while best-effort traffic still makes progress.

### Local And Web Context

Local PPT support: [SOC components -processor.pdf, p.4](<System on chip/SOC components -processor.pdf#page=4>) says memory and interconnect can be treated as delay elements in performance analysis, and [SOC components -processor.pdf, p.18](<System on chip/SOC components -processor.pdf#page=18>) says faster cache and memory reduce instruction/data fetch cycles. [module 1 part 1 introduction to system approach.pdf, p.39](<System on chip/module 1 part 1 introduction to system approach.pdf#page=39>) says processor, memory or I/O should be sized to meet high-priority real-time constraints. For QoS traffic-class wording, see the web sources in [CLO3_Topic4_sources.md](<sources/CLO3_Topic4_sources.md>), especially AMD Versal QoS documentation.

### Figure 1: Quality-Aware Memory Scheduling

```text
 +---------+   +---------+   +---------+   +----------+
 | CPU     |   | GPU     |   | DMA     |   | Display  |
 | latency |   | bw      |   | bw      |   | deadline |
 +----+----+   +----+----+   +----+----+   +----+-----+
      |             |             |             |
      +-------------+-------------+-------------+
                    |
                    v
        +-----------------------------+
        | QoS / Quality-Aware         |
        | Memory Scheduler            |
        | priority + age + deadline   |
        | bandwidth + row-buffer hit  |
        +--------------+--------------+
                       |
                       v
        +-----------------------------+
        | SDRAM Controller            |
        | banks, rows, refresh, timing|
        +--------------+--------------+
                       |
                       v
                 DDR / LPDDR Memory
```

Figure source: use [CLO3_Topic4_sources.md](<sources/CLO3_Topic4_sources.md>) for QoS source references. This figure is needed because it shows that quality-aware scheduling sits between multiple SoC masters and the SDRAM command scheduler.

### Why Quality-Aware Scheduling Is Needed

A simple memory controller may use **FCFS**: first come, first served. This is fair in arrival order but not necessarily good for performance or real-time quality.

Problems with simple FCFS:

- A display request may wait behind many CPU requests and miss its deadline.
- A real-time audio/video stream may underflow.
- A high-bandwidth accelerator may monopolize memory.
- A low-priority master may starve.
- Row-buffer locality may be wasted.

Therefore, quality-aware scheduling uses priority and QoS information.

### Quality Metrics

Quality-aware scheduling may optimize:

- **Latency**: how long a request waits.
- **Bandwidth**: amount of data served per unit time.
- **Deadline**: latest time by which a request must finish.
- **Jitter**: variation in service time.
- **Fairness**: no master should be starved.
- **Throughput**: total memory utilization.
- **Energy**: fewer row conflicts and better burst scheduling can reduce power.
- **QoS class**: real-time, isochronous, low-latency, best-effort.

### Traffic Classes

Common traffic classes:

| Class | Example | Requirement |
|---|---|---|
| Real-time / deadline | display refresh, audio, camera | must be served before deadline |
| Low-latency | CPU, interrupt-related memory access | short response time |
| High-bandwidth | GPU, AI accelerator, DMA | sustained bandwidth |
| Best-effort | background copy, storage, logging | can wait |

### Scheduling Policies

### 1. Fixed Priority

Each master is assigned a priority. Higher-priority requests are served first.

Advantage:

- simple,
- good for urgent traffic.

Disadvantage:

- low-priority masters may starve.

### 2. Round Robin

Masters are served in cyclic order.

Advantage:

- fair,
- avoids starvation.

Disadvantage:

- may not meet deadlines,
- may ignore row-buffer locality.

### 3. Weighted Round Robin

Each master gets a weight. Higher-weight masters get more service.

Advantage:

- supports bandwidth allocation,
- fairer than fixed priority.

Disadvantage:

- may still be weak for strict deadlines.

### 4. Deadline-Aware Scheduling

Requests with earlier deadlines are served first.

Advantage:

- good for real-time audio/video/display.

Disadvantage:

- can reduce total throughput if it ignores SDRAM bank/row behavior.

### 5. FR-FCFS

**FR-FCFS** means **First Ready - First Come First Served**. It prioritizes ready row-buffer hits before older row misses.

Advantage:

- improves DRAM throughput by exploiting row-buffer locality.

Disadvantage:

- may be unfair or harm real-time requests if used alone.

### 6. QoS-Aware Hybrid Scheduling

Practical memory controllers often combine policies:

- real-time requests get deadline/priority handling;
- best-effort requests use row-buffer locality;
- aging prevents starvation;
- bandwidth counters enforce minimum service;
- refresh and power constraints are respected.

### Scheduler Decision Factors

A quality-aware scheduler considers:

- request priority,
- request age,
- deadline,
- master ID,
- QoS value,
- bank availability,
- row-buffer hit/miss,
- read/write direction,
- refresh timing,
- power state,
- bandwidth budget,
- fairness counters.

### Example

Suppose requests arrive:

| Request | Master | Type | Quality Need |
|---|---|---|---|
| R1 | CPU | read | low latency |
| R2 | Display | read | deadline |
| R3 | DMA | burst read | bandwidth |
| R4 | GPU | read | bandwidth |
| R5 | Background copy | write | best effort |

A pure throughput scheduler may choose row hits first. A quality-aware scheduler may choose:

```text
1. Display request first if deadline is near.
2. CPU request next for low latency.
3. GPU/DMA bursts using bank interleaving for bandwidth.
4. Background write when bus is idle or write batching is efficient.
```

This protects real-time quality without completely ignoring throughput.

### Relationship With SDRAM Bank Scheduling

Quality-aware scheduling must still obey SDRAM rules. Even if a display request is urgent, the controller must respect tRCD, tRP, CAS latency, refresh and bank availability.

The best scheduler balances two goals:

1. **Quality goal**: meet deadlines, bandwidth and latency guarantees.
2. **DRAM efficiency goal**: use row hits, bank interleaving and burst transfers.

If the scheduler only optimizes QoS, bandwidth may fall. If it only optimizes row-buffer hits, real-time traffic may miss deadlines. Therefore, quality-aware scheduling is a tradeoff.

<a id="topic-4-final-answer"></a>

### Final Exam-Ready Answer

Quality-aware scheduling in an SoC memory system is the process of scheduling memory requests according to quality-of-service requirements such as latency, bandwidth, deadline, jitter and fairness. It is needed because modern SoCs have many memory masters such as CPU, GPU, DMA, display controller, camera interface, DSP and accelerators. These masters generate different types of traffic and do not have equal urgency.

A simple first-come-first-served scheduler may be fair by arrival order, but it can fail in SoC systems because a real-time display or audio request may wait behind non-critical traffic. Similarly, a throughput-oriented scheduler may prioritize row-buffer hits and improve DRAM efficiency, but it may starve low-priority or deadline-critical requests. Therefore, quality-aware scheduling considers both system-level QoS and SDRAM-level efficiency.

The important quality parameters are latency, bandwidth, deadline, fairness, jitter and traffic class. Real-time traffic such as display and audio needs guaranteed service before deadlines. CPU traffic often needs low latency. GPU, DMA and AI accelerators need high bandwidth. Background traffic is usually best-effort. A quality-aware memory scheduler uses priority, request age, deadlines, bandwidth counters, QoS values and starvation prevention to decide which request should be served next.

Quality-aware scheduling must also respect SDRAM timing and bank behavior. The memory controller must consider row-buffer hits, bank conflicts, activate, precharge, CAS latency, refresh and read/write turnaround. A good scheduler balances row-buffer locality and bank interleaving with QoS requirements. For example, it may serve a deadline-critical display request before a row-hit best-effort request, but it may also batch non-urgent writes or use bank interleaving to improve bandwidth.

Thus, quality-aware scheduling improves SoC memory behavior by ensuring that important masters receive the required latency or bandwidth while maintaining overall memory throughput and fairness. It is essential in multimedia, mobile, automotive and real-time SoCs where missing a memory-service deadline can cause visible or functional failure.

### Short 10-Mark Exam Answer

Quality-aware scheduling is a memory-controller scheduling technique in which memory requests are served according to QoS requirements such as latency, bandwidth, deadline and fairness. It is required because an SoC has many memory masters: CPU, GPU, DMA, display, camera, DSP and accelerators. These masters compete for DRAM, but their requirements are different.

A quality-aware scheduler gives suitable service to real-time, low-latency, high-bandwidth and best-effort traffic. It may use fixed priority, weighted round robin, deadline-aware scheduling, aging and bandwidth reservation. It must also consider SDRAM efficiency, including row-buffer hits, bank conflicts, activate/precharge delays, CAS latency and refresh.

The goal is to meet quality requirements without wasting memory bandwidth or starving any master. Therefore, quality-aware scheduling balances QoS guarantees with efficient SDRAM command scheduling.

<a id="topic-4-technical-words"></a>

### Technical Words To Use For Marks

- **Quality-aware scheduling** (write this because it is the exact topic.)
- **QoS - Quality of Service** (write this because quality means latency, bandwidth, deadline and fairness guarantees.)
- **Memory master** (write this because CPU, GPU, DMA and display all request memory.)
- **Traffic class** (write this because different masters have different service requirements.)
- **Real-time traffic** (write this because display/audio/camera may have deadlines.)
- **Best-effort traffic** (write this because some memory traffic can wait.)
- **Latency guarantee** (write this because CPU and real-time requests need bounded delay.)
- **Bandwidth guarantee** (write this because GPU/DMA/display need sustained data rate.)
- **Deadline-aware scheduling** (write this because some requests must be served before a time limit.)
- **Fairness** (write this because low-priority masters should not starve.)
- **Starvation prevention** (write this because strict priority can block low-priority traffic.)
- **Aging** (write this because request priority can increase as it waits.)
- **Weighted round robin** (write this because it gives controlled bandwidth sharing.)
- **FR-FCFS** (write this because row-buffer hits improve SDRAM throughput.)
- **Row-buffer locality** (write this because SDRAM efficiency depends on row hits.)
- **Bank conflict** (write this because conflicting bank/row requests increase latency.)
- **Memory-controller arbitration** (write this because the scheduler chooses among competing requests.)
- **Isochronous traffic** (write this because audio/video traffic needs regular service.)
- **Jitter** (write this because variation in service time affects real-time streams.)

<a id="topic-4-diagrams"></a>

### Images / Diagrams To Remember

1. **Quality-aware scheduler block diagram**: Draw CPU/GPU/DMA/display requests entering a QoS-aware memory scheduler, then SDRAM controller and DDR/LPDDR memory.
2. **Traffic-class table**: Draw real-time, low-latency, high-bandwidth and best-effort traffic with examples.
3. **Source to cite for local context**: [SOC components -processor.pdf, p.18](<System on chip/SOC components -processor.pdf#page=18>) because it connects memory speed to instruction/data fetch cycles.
4. **Source to cite for real-time context**: [module 1 part 1 introduction to system approach.pdf, p.39](<System on chip/module 1 part 1 introduction to system approach.pdf#page=39>) because it mentions sizing processor, memory or I/O for high-priority real-time constraints.
5. **Source file for web/QoS details**: [CLO3_Topic4_sources.md](<sources/CLO3_Topic4_sources.md>) because it contains ARM/AMD and research references for QoS-aware memory scheduling.

<a id="topic-5"></a>

## Topic 5: Memory Controller

<a id="topic-5-question"></a>

### Question

**Explain the memory controller in SoC memory design.**

### CLO Mapping

This topic belongs to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

Reason: The syllabus explicitly places **Memory Controller** under **SoC Memory Design**, and CLO 3 directly mentions **memory controller architecture**. This topic is not only about memory devices such as SRAM or DRAM. It is about the control block that allows processors, DMA engines and accelerators inside the SoC to correctly and efficiently access external or internal memory.

### What The Question Is Asking

The examiner is asking you to explain the role, internal blocks and design importance of the memory controller. A weak answer only says: "A memory controller controls memory." A full-mark answer must explain what exactly it controls: request arbitration, address decoding, DRAM command generation, row/bank management, refresh, timing constraints, buffering, QoS and error protection.

For full marks, answer in this order:

1. Define memory controller.
2. Explain why an SoC needs a memory controller.
3. Draw a block diagram showing CPU/GPU/DMA/interconnect, memory controller and DRAM.
4. Explain the main blocks inside the memory controller.
5. Explain how it converts read/write requests into memory commands.
6. Explain timing, refresh, arbitration, scheduling and buffering.
7. Discuss design tradeoffs: latency, bandwidth, power, area, predictability and QoS.
8. Link the answer back to memory hierarchy and SDRAM banked architecture.

<a id="topic-5-explanation"></a>

### Core Idea

A **memory controller** is the hardware block that sits between SoC masters and the memory device. SoC masters include CPU cores, GPU, DSP, DMA engine, display controller, camera interface, network block and accelerators. These masters usually do not directly drive DRAM pins. They send abstract read/write transactions through an interconnect such as AXI, AHB, NoC or another bus fabric. The memory controller accepts those requests and converts them into the exact memory operations required by SRAM, SDRAM, DDR, LPDDR or another memory technology.

The simplest way to remember it is:

```text
SoC masters -> Interconnect / NoC -> Memory controller -> Memory PHY -> Memory chips
```

The controller is important because memory devices have strict timing and command requirements. For example, SDRAM cannot be read like a simple register. Before data can be read, the controller may need to open a row using ACTIVATE, wait for tRCD, issue READ, wait for CAS latency, transfer burst data, and later PRECHARGE the bank. If refresh is due, the controller must pause normal traffic and refresh the DRAM cells. If many masters request memory together, the controller must arbitrate among them and prevent starvation.

Therefore, the memory controller is both a **correctness block** and a **performance block**. It makes memory access legal according to device timing, and it also decides how efficiently the memory bandwidth is used.

### Basic Block Diagram

Use this diagram in exams when asked to draw memory controller architecture:

```text
 CPU cores     GPU/DSP       DMA       Display/Camera
    |            |            |              |
    +------------+------------+--------------+
                         |
                  SoC Interconnect
                   AXI / AHB / NoC
                         |
              +----------------------+
              |  Memory Controller   |
              |----------------------|
              | Request queues       |
              | Address decoder      |
              | Arbiter / scheduler  |
              | Row/bank manager     |
              | Timing controller    |
              | Refresh controller   |
              | Read/write buffers   |
              | ECC / protection     |
              | QoS logic            |
              +----------------------+
                         |
                    DDR / LPDDR PHY
                         |
              DRAM channel / ranks / banks
```

This diagram is useful because it shows that the memory controller is not a single small circuit. It is a collection of sub-blocks that manage requests, addresses, timing, data movement, reliability and quality of service.

### Why SoC Needs A Memory Controller

An SoC needs a memory controller for the following reasons:

1. **Different masters share memory**: CPU, GPU, DMA, display and accelerators may all access the same DRAM. The controller decides whose request is served first.
2. **DRAM has complex timing**: SDRAM/DDR memories require ACTIVATE, READ, WRITE, PRECHARGE and REFRESH commands with exact timing gaps.
3. **Address must be mapped**: A processor address must be translated into channel, rank, bank, row and column fields.
4. **Data width mismatch exists**: A CPU may request a cache line, a DMA may request a burst, and the memory device may have a different bus width. The controller packs/unpacks data.
5. **Bandwidth must be maximized**: The controller schedules row hits, bank interleaving and bursts to improve throughput.
6. **Latency must be controlled**: Critical requests such as CPU cache misses or display fetches cannot wait indefinitely.
7. **Refresh is mandatory**: DRAM cells leak charge, so the controller must periodically refresh rows.
8. **Reliability is needed**: Many systems use ECC, parity, address protection, access permissions or error reporting.
9. **Power must be managed**: DDR/LPDDR memories support low-power modes, self-refresh and clock gating.
10. **Real-time behavior may be required**: Automotive, camera, display and communication SoCs need predictable memory service.

### Main Blocks Inside A Memory Controller

#### 1. Request Interface

The request interface receives read and write transactions from the SoC interconnect. These transactions contain:

- address,
- read/write type,
- burst length,
- byte enables,
- transaction ID,
- priority or QoS value,
- source master information.

The memory controller must accept multiple outstanding requests and preserve required ordering rules. For example, two writes from the same processor to the same address region may need ordering, while independent reads from different masters may be reordered for efficiency.

#### 2. Request Queues

The controller stores incoming requests in queues. Separate queues may exist for reads, writes, urgent traffic, best-effort traffic or each master. Queues are needed because the memory device cannot serve all requests immediately.

Queues improve performance because the controller can inspect multiple pending requests and choose a good one. For example, if one request is a row hit and another request needs precharge and activate, serving the row hit first may improve bandwidth. However, excessive reordering can hurt fairness, so the controller must balance performance and starvation prevention.

#### 3. Address Decoder And Address Mapper

The address decoder converts a system address into memory fields:

```text
System address -> Channel -> Rank -> Bank -> Row -> Column -> Byte offset
```

This mapping is very important. If consecutive addresses are mapped well across banks and channels, bank interleaving improves bandwidth. If the mapping is poor, many requests may hit the same bank and create bank conflicts.

Address mapping affects:

- row-buffer hit rate,
- bank parallelism,
- channel utilization,
- latency,
- power,
- predictability.

For example, a streaming video buffer may benefit from sequential burst mapping, while multicore traffic may benefit from spreading addresses across banks/channels.

#### 4. Arbiter

The arbiter decides which request should be considered for service when multiple masters are waiting. Arbitration policies include:

- first-come-first-served,
- fixed priority,
- round robin,
- weighted round robin,
- deadline-based arbitration,
- age-based arbitration,
- QoS-aware arbitration.

The arbiter is necessary because a modern SoC has many competing requesters. Without arbitration, one master could dominate memory and delay others.

#### 5. Scheduler

The scheduler decides the exact order of memory commands. Arbitration chooses among requesters; scheduling chooses how to issue commands to the memory device efficiently.

For SDRAM/DDR, the scheduler considers:

- whether the requested row is already open,
- whether a bank is busy,
- whether tRCD, tRP, tRAS, tRC and CAS latency are satisfied,
- whether a refresh is pending,
- whether read/write turnaround delay is needed,
- whether QoS deadlines are approaching,
- whether writes should be drained in a batch.

A common scheduling idea is to prefer row-buffer hits because they avoid extra activate/precharge delay. But a controller cannot only serve row hits because that can starve other traffic. Therefore, practical schedulers combine row-buffer efficiency with fairness and QoS.

#### 6. Command Generator

The command generator converts scheduled memory operations into device commands. For SDRAM/DDR, these include:

- ACTIVATE,
- READ,
- WRITE,
- PRECHARGE,
- REFRESH,
- mode register commands,
- power-down or self-refresh commands.

The command generator must issue these commands at the right time and with the right bank, row and column addresses. This is the part that makes high-level SoC transactions compatible with low-level memory protocol.

#### 7. Timing Controller

The timing controller enforces all timing constraints of the memory device. This is one of the most important parts of the memory controller.

Typical timing parameters include:

- **tRCD**: delay between ACTIVATE and READ/WRITE.
- **CL / CAS latency**: delay between READ command and data output.
- **tRP**: precharge time before another row can be activated.
- **tRAS**: minimum active time of a row.
- **tRC**: complete row cycle time.
- **tRFC**: time consumed by refresh.
- **read/write turnaround time**: delay when switching bus direction.

The timing controller prevents illegal command sequences. Without it, data corruption or unreliable memory operation can occur.

#### 8. Refresh Controller

DRAM stores data as charge in capacitors. This charge leaks over time. The refresh controller periodically refreshes memory rows so data is not lost.

Refresh creates a design tradeoff:

- If refresh is delayed too much, data retention can fail.
- If refresh is too frequent or poorly scheduled, useful memory bandwidth is wasted.
- If refresh occurs during real-time traffic, latency may increase.

Good controllers schedule refresh carefully, sometimes using distributed refresh, postponed refresh or priority-aware refresh.

#### 9. Read And Write Buffers

Read and write buffers temporarily hold data and requests. They are needed because the SoC side and memory side may operate at different speeds and because data returns after variable latency.

Write buffers allow the controller to collect writes and issue them together. This reduces read/write bus turnaround overhead. Read buffers hold returned data until it can be delivered to the correct master.

Buffers also allow multiple outstanding requests. This is important because a processor can continue execution or issue more misses if the memory system supports nonblocking behavior.

#### 10. Data Path And Burst Handling

Modern DRAM transfers data in bursts. A cache miss may require a full cache line, not just one word. The controller must manage:

- burst length,
- bus width conversion,
- byte enables,
- alignment,
- cache-line fills,
- write masks,
- data return order.

This is why the data path of a memory controller can be large and timing-critical.

#### 11. ECC And Error Handling

Many SoCs include error protection in the memory controller. ECC can detect and correct memory bit errors. Error handling may include:

- single-bit correction,
- double-bit detection,
- error logging,
- interrupt generation,
- memory scrubbing,
- protection against illegal address accesses.

ECC improves reliability but adds area, latency and extra memory bits.

#### 12. QoS And Real-Time Support

QoS logic gives controlled service to different traffic classes. For example:

- display traffic needs regular bandwidth,
- CPU cache misses need low latency,
- GPU and AI accelerator traffic need high bandwidth,
- background DMA can usually wait.

QoS support may use priority values, bandwidth counters, deadline timers, credits or weighted arbitration. This connects directly to Topic 4, **Quality-Aware Scheduling**.

### Memory Controller Operation Step By Step

For a read request from a CPU cache miss:

1. CPU sends a read request to the interconnect.
2. Interconnect forwards the request to the memory controller.
3. Controller places the request in a read queue.
4. Address decoder maps the address to channel, rank, bank, row and column.
5. Scheduler checks whether the required row is already open.
6. If row is closed, command generator issues ACTIVATE.
7. Timing controller waits for tRCD.
8. Controller issues READ command.
9. After CAS latency, data is returned from DRAM.
10. Read buffer captures data and sends it back to the requesting CPU.

For a write request:

1. Master sends write address and data.
2. Controller stores the write in write buffer.
3. Scheduler may delay or batch writes to reduce turnaround overhead.
4. Controller opens the correct row if needed.
5. WRITE command is issued.
6. Data is transferred to memory.
7. Ordering and completion rules are maintained.

### Open-Page And Close-Page Policies

The memory controller must decide what to do after accessing a row.

**Open-page policy** keeps a row open after access. This is good when future requests are likely to hit the same row. It improves row-buffer hit rate and bandwidth for locality-heavy workloads.

**Close-page policy** precharges the row after access. This is good when future requests are likely to go to different rows. It can reduce latency for random traffic because the bank is ready for a new row.

Many controllers use adaptive policies that change behavior based on workload.

### Relationship With SDRAM Banked Architecture

The memory controller gets the main benefit from SDRAM banked architecture. Since SDRAM has multiple banks, the controller can activate one bank while reading another, or alternate requests among banks to hide delays. This is called bank interleaving.

However, banked architecture also creates conflicts. If several requests go to the same bank but different rows, the controller must precharge and activate repeatedly. This increases latency. Therefore, the controller tries to:

- maximize row hits,
- spread traffic across banks,
- avoid unnecessary precharge,
- respect timing constraints,
- prevent one master from monopolizing one bank,
- schedule refresh without large delay spikes.

### Relationship With Memory Hierarchy

The memory controller is below the cache hierarchy and above the memory device. Caches reduce the number of requests reaching the memory controller. But when a cache miss occurs, the memory controller determines how quickly the missing block is fetched.

SoC memory hierarchy and memory controller are connected in this way:

```text
Registers -> L1 cache -> L2/L3 cache -> Memory controller -> DRAM/LPDDR
```

If cache hit rate is high, the memory controller sees fewer requests. If many masters generate cache misses or DMA traffic, the controller becomes a bottleneck. This is why memory controller scheduling is central to SoC performance.

### Design Tradeoffs

#### 1. Latency Versus Bandwidth

A latency-optimized controller serves urgent requests quickly. A bandwidth-optimized controller reorders requests to improve row hits and burst efficiency. These goals can conflict.

Example: A CPU cache miss may be urgent, but serving a group of row-hit DMA requests first may improve total bandwidth. The controller must choose based on policy.

#### 2. Fairness Versus Priority

Strict priority helps real-time traffic but may starve lower-priority masters. Fairness prevents starvation but may delay urgent traffic. QoS-aware arbitration balances both.

#### 3. Complexity Versus Area And Power

More queues, reorder logic, ECC, QoS counters and adaptive schedulers improve performance, but they increase silicon area, power and verification effort.

#### 4. Predictability Versus Average Performance

Real-time systems prefer predictable worst-case latency. High-performance systems often prefer average throughput. Row-hit scheduling improves average bandwidth but can make worst-case latency harder to bound.

#### 5. Open-Page Versus Close-Page

Open-page policy is good for locality. Close-page policy is better for random traffic. Adaptive policy is better but more complex.

#### 6. Refresh Overhead Versus Data Retention

Refresh is compulsory for DRAM. The controller must guarantee refresh while minimizing performance disturbance.

### Why This Topic Is Important For Exams

This topic connects many CLO 3 ideas:

- memory technology,
- memory hierarchy,
- SDRAM banked organization,
- latency,
- bandwidth,
- QoS scheduling,
- processor-memory interaction.

If an exam asks about memory controller, do not write only definitions. Show that the controller is the architectural bridge between SoC requesters and physical memory timing.

<a id="topic-5-final-answer"></a>

### Final Exam-Ready Answer

A memory controller is a hardware block in an SoC that manages all communication between SoC masters and the memory system. SoC masters such as CPU cores, GPU, DMA engine, display controller, camera interface, DSP and accelerators generate read and write requests through the system interconnect. The memory controller accepts these high-level requests and converts them into correct low-level memory operations for SRAM, SDRAM, DDR, LPDDR or other memory devices.

The memory controller is required because modern memories, especially SDRAM and DDR memories, cannot be accessed as simple registers. They have banked organization, row buffers, burst transfers, refresh requirements and strict timing constraints. The controller maps a system address into channel, rank, bank, row and column fields. It then generates commands such as ACTIVATE, READ, WRITE, PRECHARGE and REFRESH while obeying timing parameters such as tRCD, CAS latency, tRP, tRAS, tRC and tRFC.

Internally, a memory controller contains request queues, address decoder, arbiter, scheduler, command generator, timing controller, refresh controller, read/write buffers, data path logic, ECC logic and QoS control. The request queues hold pending transactions. The arbiter decides which master should be considered. The scheduler selects an efficient command order by considering row-buffer hits, bank conflicts, read/write turnaround, refresh and priority. The timing controller ensures that all memory commands are issued only when legal. The refresh controller periodically refreshes DRAM cells to preserve data. Read and write buffers allow burst transfers and multiple outstanding memory requests.

The memory controller strongly affects SoC performance. A good controller increases bandwidth by using row-buffer locality, bank interleaving, burst transfers and multi-channel memory. It reduces latency by prioritizing critical requests and avoiding unnecessary precharge/activate operations. It improves fairness by preventing starvation among CPU, GPU, DMA and real-time masters. It also improves reliability through ECC and error reporting. In multimedia and real-time SoCs, the controller may provide QoS guarantees so that display, camera or audio traffic receives memory service before deadlines.

The design of a memory controller involves tradeoffs. Optimizing only for row-buffer hits can improve bandwidth but may hurt fairness. Giving strict priority to real-time traffic can meet deadlines but may starve best-effort traffic. Large buffers and complex scheduling improve performance but increase area, power and verification complexity. Open-page policy improves locality, while close-page policy may reduce latency for random traffic. Therefore, the memory controller is a central part of SoC memory architecture because it determines how efficiently and predictably the processor-memory system works.

### Short 10-Mark Exam Answer

A memory controller is the SoC hardware block that connects processors and other memory masters to the memory device. It receives read/write requests from CPU, GPU, DMA, display and accelerators through the interconnect and converts them into memory commands.

For SDRAM/DDR, the controller performs address mapping into channel, rank, bank, row and column. It issues ACTIVATE, READ, WRITE, PRECHARGE and REFRESH commands while satisfying timing parameters such as tRCD, CAS latency, tRP and tRFC. It contains request queues, arbiter, scheduler, timing controller, refresh controller, read/write buffers, data path, ECC and QoS logic.

The memory controller improves performance by using bank interleaving, row-buffer hits, burst transfers and multi-channel access. It also provides fairness and QoS among different SoC masters. Hence, memory controller architecture is essential for latency, bandwidth, reliability, power and real-time behavior in SoC memory design.

<a id="topic-5-technical-words"></a>

### Technical Words To Use For Marks

- **Memory controller** (write this because it is the exact architecture block asked in the question.)
- **SoC master** (write this because CPU, GPU, DMA and display are the request sources.)
- **Interconnect / NoC** (write this because masters reach memory through a bus or network fabric.)
- **Request queue** (write this because memory requests wait before being scheduled.)
- **Arbitration** (write this because the controller must choose among competing masters.)
- **Scheduler** (write this because command order affects bandwidth and latency.)
- **Address mapping** (write this because system addresses become channel/rank/bank/row/column addresses.)
- **Channel** (write this because multiple channels increase memory bandwidth.)
- **Rank** (write this because DDR memory may organize chips into ranks.)
- **Bank** (write this because SDRAM bank parallelism is controlled by the controller.)
- **Row buffer** (write this because row hits and row conflicts dominate SDRAM performance.)
- **ACTIVATE command** (write this because a DRAM row must be opened before access.)
- **READ / WRITE command** (write this because these are the actual data-transfer commands.)
- **PRECHARGE command** (write this because the bank must be prepared before opening another row.)
- **REFRESH command** (write this because DRAM data must be periodically restored.)
- **Timing controller** (write this because memory commands must obey exact timing rules.)
- **tRCD** (write this because it is the delay between row activation and column access.)
- **CAS latency / CL** (write this because it is the delay between READ and data output.)
- **tRP** (write this because it is the precharge delay.)
- **tRFC** (write this because refresh consumes memory-service time.)
- **Read/write buffer** (write this because buffering supports outstanding requests and burst traffic.)
- **Burst transfer** (write this because DDR memories transfer multiple data beats per command.)
- **ECC** (write this because many controllers include error detection and correction.)
- **QoS** (write this because real-time and high-priority traffic require service guarantees.)
- **Open-page policy** (write this because it keeps rows open for locality.)
- **Close-page policy** (write this because it prepares banks for random accesses.)
- **Bank interleaving** (write this because it hides bank timing delays and improves bandwidth.)
- **Refresh overhead** (write this because refresh reduces available bandwidth.)
- **Memory PHY** (write this because DDR/LPDDR needs physical-layer signaling and timing.)

<a id="topic-5-diagrams"></a>

### Images / Diagrams To Remember

1. **Memory controller block diagram**: Draw SoC masters, interconnect, memory controller blocks and DDR/LPDDR memory. This is the most important diagram for this topic.
2. **DRAM command flow diagram**: Draw address decode -> ACTIVATE -> tRCD wait -> READ/WRITE -> CAS latency -> data burst -> PRECHARGE/keep row open.
3. **Address mapping diagram**: Draw system address divided into channel, rank, bank, row, column and byte offset.
4. **Source figure to look for**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.169](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=169>) has a memory controller style DRAM module figure with dynamic memory controller and timing controller.
5. **Source figure to look for**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.173](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=173>) has SDRAM channels and controller.
6. **Detailed source file**: [CLO3_Topic5_sources.md](<sources/CLO3_Topic5_sources.md>) contains the local book, PPT and web references for this topic.

<a id="topic-6"></a>

## Topic 6: Models of Simple Processor-Memory Interaction

<a id="topic-6-question"></a>

### Question

**Explain the models of simple processor-memory interaction.**

### CLO Mapping

This topic belongs to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

Reason: The syllabus lists **Models of Simple Processor-Memory Interaction** under **SoC Memory Design**. It is part of CLO 3 because it explains how processors generate memory requests, how memory modules serve them, and how contention, bandwidth and latency determine SoC performance.

### What The Question Is Asking

The examiner is asking you to explain how the interaction between processors and memory can be modeled mathematically or architecturally. This is not only a descriptive topic. You should explain the reason for modeling, the simple blocking model, the multiprocessor/multimemory model, the effect of contention, achieved bandwidth and the Strecker-Ravi type bandwidth model.

For full marks, answer in this order:

1. Explain why processor-memory interaction must be modeled.
2. Define memory request, access time, service time and bandwidth.
3. Explain the single processor-single memory blocking model.
4. Explain the multiple processor-multiple memory module model.
5. Explain contention and memory interleaving.
6. Explain equivalence between many simple processors and one pipelined processor issuing many outstanding requests.
7. Write and explain the bandwidth formula.
8. Discuss limitations of the model and its relevance to SoC.

<a id="topic-6-explanation"></a>

### Core Idea

The **processor-memory interaction model** is a simplified way to estimate how well a memory system can serve processor requests. In a real SoC, processors do not run only on arithmetic units. They continuously fetch instructions, load data, store results, handle cache misses and interact with DMA or accelerators. If the memory system cannot provide data fast enough, the processor stalls.

The goal of the model is to answer questions such as:

- How many memory requests can be served per memory cycle?
- What happens when many processors access the same memory module?
- How much bandwidth is lost due to contention?
- How many memory modules are needed to support a given request rate?
- How do caches and nonblocking memory systems reduce stalls?

This topic is important because SoC performance is often limited by memory, not by the processor core alone.

### Basic Terms

#### Memory Request

A memory request is a read or write operation generated by a processor, cache, DMA engine or accelerator. In a simple model, each request goes to one memory module and needs one service period.

#### Access Time

Access time is the time between issuing a memory request and receiving the requested data. In processor terms, high access time means the CPU waits longer for instructions or data.

#### Service Time

Service time, usually denoted as **Ts**, is the time during which a memory module is busy serving one request. If a module is busy, another request to the same module must wait.

#### Bandwidth

Bandwidth is the number of memory requests or data units served per unit time.

If **B** requests are served in one service time **Ts**, then:

```text
Bw = B / Ts
```

Here, **B** is achieved bandwidth measured in requests per service time, and **Bw** is bandwidth per second or per time unit.

### Model 1: Single Processor - Single Memory Module

The simplest model has one processor and one memory module.

```text
Processor -> Memory module
```

In this model:

- the processor sends one request,
- the memory serves it,
- the processor waits until the response returns,
- then the processor continues.

This is a **blocking model** because the processor cannot make useful progress while waiting for memory. It is easy to analyze because there is no contention from other processors. If memory latency is large, processor utilization becomes poor.

This model explains why caches are important. If most accesses hit in cache, the processor avoids slow memory access. If cache misses are frequent, the processor spends many cycles waiting.

### Model 2: Multiple Processors - Multiple Memory Modules

A more realistic model has **n processors** and **m independent memory modules**.

```text
P1   P2   P3   ...   Pn
 |    |    |          |
 +----+----+----------+
          |
    Interconnect
          |
 M1   M2   M3   ...   Mm
```

Each processor may generate a memory request. Each request is mapped to one memory module. If different processors access different memory modules, the requests can be served in parallel. If two or more processors access the same module in the same service period, only one request can be served and the others must wait or be retried.

This conflict is called **memory contention**.

The model shows why memory interleaving is useful. If addresses are spread across multiple modules or banks, requests are more likely to go to different modules, increasing parallelism and bandwidth.

### Model 3: One Pipelined Processor With Multiple Outstanding Requests

The same model can also represent one advanced processor that can issue multiple outstanding memory requests. A nonblocking cache, out-of-order processor or DMA-capable system may allow several cache misses to be pending at the same time.

The idea is:

```text
n simple processors each issue 1 request
          is similar to
1 pipelined processor issues n outstanding requests
```

This equivalence is important because the memory system sees **n requests per service time** in both cases. It does not always matter whether the requests came from many processors or from one aggressive processor. The memory controller still has to schedule multiple pending requests among memory modules.

### Contention In Processor-Memory Interaction

Contention happens when more than one request wants the same memory resource at the same time.

Contention can occur at:

- memory module level,
- SDRAM bank level,
- row-buffer level,
- memory channel level,
- interconnect or bus level,
- memory-controller queue level.

In the simple model, contention is usually analyzed at the memory module level. If several requests choose the same module, that module can serve only one request during that service period. The other requests reduce effective bandwidth.

### The Strecker-Ravi Type Bandwidth Model

The standard simple model assumes:

1. There are **n memory requests** per service time.
2. There are **m independent memory modules**.
3. Each request chooses a memory module uniformly at random.
4. Each memory module can serve at most one request per service time.
5. There is no bus/interconnect contention.
6. Previous cycles are ignored in the simple approximation.

For any one memory module, the probability that a particular request does **not** go to that module is:

```text
1 - 1/m
```

For **n** independent requests, the probability that no request goes to that module is:

```text
(1 - 1/m)^n
```

Therefore, the probability that the module is busy is:

```text
1 - (1 - 1/m)^n
```

Since there are **m** modules, the expected number of busy modules is:

```text
B(m,n) = m [1 - (1 - 1/m)^n]
```

Here:

- **B(m,n)** is the average number of memory requests served per service time.
- **m** is the number of memory modules.
- **n** is the number of requests made per service time.

The bandwidth per time unit is:

```text
Bw = B(m,n) / Ts
```

This formula is important because it shows that achieved bandwidth is less than or equal to the ideal bandwidth. The ideal case would serve all requests if there were enough modules and no conflicts. In practice, random conflicts reduce the number of requests served.

### Numerical Example

Suppose:

```text
n = 4 requests per service time
m = 4 memory modules
```

Then:

```text
B(4,4) = 4 [1 - (1 - 1/4)^4]
       = 4 [1 - (3/4)^4]
       = 4 [1 - 81/256]
       = 4 [175/256]
       = 2.734 requests per service time
```

The ideal value is 4 requests per service time, but the achieved value is about 2.73 because some requests collide on the same memory modules.

Relative performance can be written as:

```text
P_rel = B / n
```

For this example:

```text
P_rel = 2.734 / 4 = 0.6835
```

This means the system achieves about 68 percent of the ideal request service rate under the simplified assumptions.

### Interpretation Of The Formula

The formula teaches several important ideas:

1. **Increasing memory modules improves bandwidth** because requests have more places to go.
2. **Bandwidth does not increase linearly forever** because collisions still occur and other bottlenecks appear.
3. **If n is much larger than m**, many requests compete for the same modules.
4. **If m is much larger than n**, contention is lower, but hardware cost is higher.
5. **Caches reduce n** because fewer requests reach main memory.
6. **Bank interleaving increases effective m** because independent banks can serve requests in overlapping time.
7. **Nonblocking caches increase outstanding n**, which can improve memory-level parallelism but also increases pressure on the controller.

### Relationship With Cache Misses

In a cache-based processor, main memory is mainly accessed when cache misses occur. Therefore, the request rate **n** can be interpreted as the expected number of cache misses entering the memory system per service time.

Good caches reduce memory pressure:

```text
Higher cache hit rate -> fewer memory requests -> lower n -> less contention
```

But high-performance processors may issue several misses before earlier ones complete:

```text
Nonblocking cache -> multiple outstanding misses -> higher memory-level parallelism
```

This can improve performance if the memory system has enough independent banks/modules. It can hurt performance if all requests collide at the same module or channel.

### Relationship With Memory Controller

The memory controller is the practical hardware that deals with this interaction. In the simple model, requests are randomly distributed across modules. In a real SoC, the memory controller can improve the situation by:

- mapping addresses across banks and channels,
- reordering requests,
- prioritizing urgent traffic,
- batching writes,
- exploiting row-buffer hits,
- using bank interleaving,
- applying QoS scheduling,
- managing outstanding requests.

Therefore, simple processor-memory models explain the reason behind memory-controller design choices.

### Relationship With SDRAM Banked Architecture

The **m memory modules** in the model can be thought of as independent memory modules, channels or banks. SDRAM banks allow overlapping operations. If requests go to different banks, the controller can hide some latency. If requests repeatedly go to the same bank but different rows, bank conflicts reduce performance.

This directly connects Topic 3 and Topic 6:

- Topic 3 explains banks, rows and latencies.
- Topic 6 explains how request distribution affects achieved bandwidth.
- Topic 5 explains how the memory controller schedules those requests.

### Limitations Of The Simple Model

The model is useful for understanding, but it is simplified. Its limitations are:

1. It assumes uniform random distribution of requests.
2. It ignores row-buffer locality.
3. It ignores detailed DRAM timing such as tRCD, tRP, CAS latency and refresh.
4. It ignores interconnect or bus contention.
5. It assumes each module serves one request per service time.
6. It may ignore queue state from previous cycles.
7. It does not model priorities, QoS or real-time deadlines.
8. It does not fully model cache coherence or ordering rules.

Even with these limitations, it is valuable because it clearly shows the basic effect of memory contention and memory parallelism.

### Why This Topic Is Important For Exams

This topic lets you explain memory performance using more than words. If you include the formula, the meaning of **n**, **m**, **B**, **Ts**, contention and relative performance, your answer becomes technical and scoring.

In exams, always connect the model to SoC:

- Multiple processors and accelerators generate requests.
- Memory modules/channels/banks provide parallelism.
- Contention reduces achieved bandwidth.
- Caches reduce request rate.
- Memory controller scheduling improves practical performance.

<a id="topic-6-final-answer"></a>

### Final Exam-Ready Answer

Models of simple processor-memory interaction are used to estimate how effectively a memory system can serve the memory requests generated by processors. They are important because processor performance depends not only on clock frequency, but also on how quickly instructions and data can be fetched from memory. If memory access time is high or if many requests contend for the same memory resource, processors stall and overall SoC performance reduces.

The simplest model consists of one processor and one memory module. The processor issues a memory request and waits until the memory returns the data. This is a blocking model because the processor cannot continue while the memory access is pending. It shows that high memory latency directly reduces processor utilization and explains why cache memory is required.

A more useful model contains **n processors** and **m independent memory modules**. Each processor may generate a memory request in a memory service time **Ts**. If requests go to different memory modules, they can be served in parallel. If two or more requests go to the same module, contention occurs and only one request can be served during that service time. Therefore, achieved bandwidth is lower than ideal bandwidth. This model also applies to one pipelined processor or nonblocking cache that can issue multiple outstanding memory requests, because the memory system still sees multiple requests per service time.

In the Strecker-Ravi type model, it is assumed that **n requests** are uniformly distributed over **m memory modules**, and each module can serve at most one request per service time. The probability that a particular module receives no request is `(1 - 1/m)^n`. Therefore, the probability that the module is busy is `1 - (1 - 1/m)^n`. Since there are `m` modules, the average number of busy modules, or achieved bandwidth in requests per service time, is:

```text
B(m,n) = m [1 - (1 - 1/m)^n]
```

The memory bandwidth per time unit is:

```text
Bw = B(m,n) / Ts
```

This formula shows that memory bandwidth depends on both the number of requests and the number of independent memory modules. Increasing the number of memory modules or banks reduces contention and increases bandwidth, but the improvement is not perfectly linear because multiple requests may still choose the same module. Cache memory reduces the request rate reaching main memory, while nonblocking caches and pipelined processors increase the number of outstanding requests. The memory controller improves practical performance by address interleaving, request reordering, bank scheduling, row-buffer management and QoS-aware arbitration.

Thus, models of processor-memory interaction help in understanding the relationship between memory latency, contention, bandwidth, cache misses, memory modules and controller scheduling. They are essential in SoC design because modern SoCs contain many processors and accelerators sharing the same memory system.

### Short 10-Mark Exam Answer

Simple processor-memory interaction models are used to analyze how memory requests from processors are served by memory modules. In a single processor-single memory model, the processor sends one request and waits for the memory response. This blocking behavior shows that high memory latency causes processor stalls.

In an n processor-m memory model, n requests may be generated in one memory service time Ts and distributed over m independent memory modules. If requests go to different modules, they are served in parallel. If multiple requests go to the same module, contention occurs and bandwidth is reduced.

For uniformly distributed requests, the average number of busy memory modules is:

```text
B(m,n) = m [1 - (1 - 1/m)^n]
```

Bandwidth is:

```text
Bw = B(m,n) / Ts
```

This model also represents one pipelined processor or nonblocking cache issuing multiple outstanding requests. It shows that memory interleaving, caches, multiple banks/channels and memory-controller scheduling are necessary to reduce contention and improve SoC performance.

<a id="topic-6-technical-words"></a>

### Technical Words To Use For Marks

- **Processor-memory interaction** (write this because it is the exact topic and frames the answer.)
- **Memory request** (write this because the model counts read/write requests.)
- **Access time** (write this because processor stall depends on time to get data.)
- **Service time Ts** (write this because the bandwidth model is based on service period.)
- **Bandwidth** (write this because the model estimates served requests per time.)
- **Blocking model** (write this because a simple processor waits for memory response.)
- **Memory module** (write this because m independent modules provide parallelism.)
- **n processors** (write this because the request side of the model is represented by n.)
- **m memory modules** (write this because the service side of the model is represented by m.)
- **Contention** (write this because bandwidth loss occurs when requests collide.)
- **Memory interleaving** (write this because spreading addresses across modules reduces contention.)
- **Outstanding request** (write this because pipelined/nonblocking systems may issue many requests.)
- **Nonblocking cache** (write this because it allows multiple misses to be pending.)
- **Cache miss** (write this because main memory pressure usually comes from misses.)
- **Achieved bandwidth B** (write this because the formula gives average served requests.)
- **Bw = B / Ts** (write this because it converts served requests into bandwidth.)
- **B(m,n) = m[1 - (1 - 1/m)^n]** (write this because it is the scoring mathematical expression.)
- **Uniform distribution** (write this because the formula assumes random mapping over modules.)
- **Busy module probability** (write this because the formula is derived from probability of module use.)
- **Relative performance P_rel** (write this because it compares achieved service to ideal service.)
- **Memory-level parallelism** (write this because multiple outstanding requests can improve utilization.)
- **Bank conflict** (write this because real SDRAM contention often happens at bank level.)
- **Interconnect contention** (write this because practical SoCs also have bus/NoC bottlenecks.)
- **Memory-controller scheduling** (write this because the controller manages requests in real hardware.)

<a id="topic-6-diagrams"></a>

### Images / Diagrams To Remember

1. **Single processor-single memory model**: Draw one processor connected to one memory module and label it as blocking access.
2. **n processor-m memory module model**: Draw P1 to Pn connected through interconnect to M1 to Mm. Mark contention when two processors access the same module.
3. **Pipelined processor equivalence diagram**: Draw n simple processors each issuing one request and compare it with one processor issuing n outstanding requests.
4. **Formula derivation diagram**: Show one memory module and write probability of no request as `(1 - 1/m)^n`, then busy probability as `1 - (1 - 1/m)^n`.
5. **Source figure to look for**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.176](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=176>) has the figure comparing n simple processors and one processor making n requests.
6. **Detailed source file**: [CLO3_Topic6_sources.md](<sources/CLO3_Topic6_sources.md>) contains the local book, PPT and web references for this topic.

### CLO 3 Coverage Status

All main syllabus headlines currently provided under CLO 3 are now covered:

1. **SoC Memory Design - Memory Technology**
2. **Memory Design Hierarchy and Tradeoffs**
3. **SDRAM Basics - Banked Architecture and Latencies**
4. **Quality-Aware Scheduling**
5. **Memory Controller**
6. **Models of Simple Processor-Memory Interaction**
