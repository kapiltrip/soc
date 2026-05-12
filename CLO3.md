# CLO 3 - SoC Memory Design and Memory Controller Architecture

## Clickable Index

- [CLO 3 Master Definitions](#clo3-master-definitions)
- [Topic 1: SoC Memory Design - Memory Technology](#topic-1)
  - [Question](#topic-1-question)
  - [Main Explanation](#topic-1-explanation)
  - [Beginner Foundation](#topic-1-beginner-foundation)
  - [Memory Roles](#topic-1-memory-roles)
  - [Why Each Memory Is Suited](#topic-1-suited-roles)
  - [Technology Selection](#topic-1-selection)
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
  - [SDRAM Foundation](#topic-3-foundation)
  - [Address Organization](#topic-3-address-organization)
  - [Why Latencies Exist](#topic-3-why-latencies-exist)
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
| DDR | Double Data Rate | Interface idea where data transfers occur on both rising and falling clock edges; commonly used as shorthand for DDR SDRAM. |
| DDR SDRAM | Double Data Rate Synchronous Dynamic Random Access Memory | SDRAM interface family that transfers data on both rising and falling clock edges to increase bandwidth. |
| LPDDR | Low-Power Double Data Rate | Low-power DDR DRAM family optimized for mobile, embedded and battery-powered SoCs. |
| HBM | High Bandwidth Memory | Stacked DRAM technology using a very wide interface and advanced packaging for very high bandwidth. |
| eDRAM | Embedded Dynamic Random Access Memory | DRAM-like memory integrated on-chip or near logic; denser than SRAM but needs refresh and special process support. |
| ROM | Read-Only Memory | Non-volatile memory for fixed code/data such as boot code, reset vectors and fixed lookup tables. |
| PROM | Programmable Read-Only Memory | ROM that can be programmed after manufacturing, usually once. |
| OTP | One-Time Programmable | Memory that can be programmed once and then permanently retains data. |
| EEPROM | Electrically Erasable Programmable Read-Only Memory | Non-volatile memory that can be electrically erased and rewritten, slower and endurance-limited. |
| NOR Flash | Non-volatile Flash memory with good random read behavior | Used for boot code, firmware and execute-in-place code storage. |
| NAND Flash | Dense non-volatile Flash memory | Used for mass storage; needs ECC - Error Correction Code, bad-block management and wear leveling. |
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
| DSP | Digital Signal Processor | Processor/accelerator for signal-processing tasks such as filtering, audio, modem and control algorithms. |
| DMA | Direct Memory Access | Hardware controller that moves data between memory and peripherals, or between memory regions, without continuous CPU involvement. |
| Hardware accelerator | Specialized compute block | SoC block designed to perform a specific task faster or more energy-efficiently than a general-purpose CPU. |
| AXI | Advanced eXtensible Interface | AMBA bus/interconnect protocol commonly used for high-performance SoC memory transactions. |
| AHB | Advanced High-performance Bus | AMBA bus protocol commonly used for on-chip communication in embedded SoCs. |
| NoC | Network on Chip | On-chip communication network connecting masters, memories and controllers. |
| PHY | Physical Layer | Circuit block that drives/receives electrical memory-interface signals such as DDR/LPDDR signals. |
| ECC | Error Correction Code | Extra protection bits used to detect and often correct memory errors. |
| QoS | Quality of Service | Memory-controller policy support for latency, bandwidth, priority and fairness guarantees. |
| SoC master / Memory master | Request-initiating block | Any block that can start a memory transaction, such as CPU, GPU, DMA, display controller, camera interface, DSP or accelerator. |
| Arbiter | Access-decision logic | Controller logic that decides which waiting master/request gets service first. |
| Scheduler | Command-ordering logic | Controller logic that chooses an efficient and legal order for memory commands. |
| Starvation | Excessive waiting due to priority/reordering | Condition where a request or master waits too long because other traffic keeps being served first. |
| FR-FCFS | First-Ready First-Come First-Served | Memory scheduling policy that prioritizes ready commands/row hits while considering arrival order. |
| Row buffer | Open row storage inside a DRAM bank | Holds the currently activated row; row hits are faster than row conflicts. |
| Bank | Independent DRAM subarray | Allows overlapping operations and bank interleaving. |
| Rank | Group of DRAM chips/devices selected together | Common organization unit in DDR memory systems. |
| Channel | Independent memory interface path | More channels usually increase bandwidth. |
| ACT / ACTIVATE | Activate command | Opens a DRAM row in a selected bank. |
| READ command | Memory read command | Command that transfers selected data from an open DRAM row/column to the controller. |
| WRITE command | Memory write command | Command that writes controller-provided data into selected columns of an open DRAM row. |
| PRE / PRECHARGE | Precharge command | Closes the open row and prepares a bank for another row. |
| REFRESH command | DRAM refresh command | Restores charge in DRAM cells so stored data is not lost. |
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
DRAM - Dynamic Random Access Memory, SDRAM - Synchronous Dynamic Random Access Memory, DDR - Double Data Rate, LPDDR - Low-Power Double Data Rate and HBM - High Bandwidth Memory are DRAM-family memories/interfaces that give large main-memory capacity and bandwidth.
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

<a id="topic-1-beginner-foundation"></a>

### Beginner Foundation: What Memory Means In An SoC

Before learning SRAM, DRAM, Flash and other technologies, first understand what memory is doing in a chip.

An **SoC - System on Chip** contains processing blocks that perform work: CPU cores, GPU cores, DSP blocks, AI accelerators, DMA controllers and peripheral controllers. These blocks constantly need information. They need program instructions, input data, temporary results, configuration values, status flags, packet data, audio/video samples and persistent firmware. **Memory** is the hardware storage system that holds this information.

At the smallest level, memory stores **bits**. A bit is a binary value: 0 or 1. Eight bits usually form one **byte**. Processors normally access memory using **addresses**. An address is like a numbered location. When the CPU wants data, it sends an address and a read request. When the CPU wants to store data, it sends an address, write data and a write request.

Simple idea:

```text
Address = where the data is located
Read    = get data from that address
Write   = store data at that address
```

In a real SoC, memory is not one big box. It is divided into many types because every type has different strengths. Some memories are very fast but small. Some are large but slower. Some lose data without power. Some retain data after power is removed. Some are inside the SoC die. Some are outside the SoC package or on the board. Some can be read and written many times per second. Some are good for storage but bad for frequent writes.

The most important memory properties are:

- **Latency**: how long one access takes. Low latency means the CPU waits less.
- **Bandwidth**: how much data can be transferred per second. High bandwidth matters for video, AI, graphics and networking.
- **Capacity**: how much data can be stored. Storage memory needs high capacity.
- **Density**: how many bits fit in a given silicon area. Higher density usually reduces cost per bit.
- **Volatility**: whether the data disappears when power is removed.
- **Endurance**: how many write/erase cycles the memory can tolerate before wearing out.
- **Retention**: how long the memory can keep data correctly.
- **Power**: active access power, leakage power and standby/refresh power.
- **Area**: how much chip silicon is consumed.
- **Controller complexity**: how much extra hardware/firmware is needed to use the memory correctly.

This is why the memory question is really a tradeoff question. If the examiner asks "memory technology", they are asking: **Which memory type should be used for which job, and why?**

<a id="topic-1-memory-roles"></a>

### Working Memory, Main Memory And Storage Memory

A beginner mistake is to call every memory "RAM". In SoC design, memories have different jobs.

**Working memory** is used while the chip is actively computing. It stores variables, stack data, temporary buffers and intermediate results. SRAM, caches, TCM and DRAM are working memories.

**Main memory** is the large memory used by the processor and software during normal operation. In large SoCs, main memory is usually off-chip DRAM such as DDR SDRAM or LPDDR.

**Storage memory** keeps code and data even when the system is powered off. ROM, NOR Flash, NAND Flash, eMMC and UFS are storage or persistent memories.

Use this simple memory-role map:

| Role In SoC | Usually Used Memory | Why That Memory Is Suited |
|---|---|---|
| Immediate CPU operands | Register file | Extremely fast and close to the execution unit |
| Fast average instruction/data access | SRAM cache | Low latency and hardware-managed reuse of recent data |
| Deterministic real-time code/data | TCM or scratchpad SRAM | Predictable latency without cache-miss uncertainty |
| Small stream buffering | FIFO or local SRAM | Preserves order and absorbs speed mismatch |
| Large runtime program/data memory | DRAM / DDR / LPDDR | High capacity and lower cost per bit than SRAM |
| Low-power mobile main memory | LPDDR | DRAM capacity with mobile power modes and lower-voltage operation |
| Extreme accelerator bandwidth | HBM | Very wide, close, stacked DRAM interface gives very high bandwidth |
| First boot code | ROM or NOR Flash | Non-volatile and readable immediately after reset |
| Firmware and execute-in-place code | NOR Flash | Good random reads and memory-mapped code access |
| Large persistent storage | NAND Flash, eMMC, UFS | High density and low cost per bit |

Exam line: **Memory technology is selected according to the job: SRAM for speed, DRAM for capacity, ROM/NOR for boot code, NAND/eMMC/UFS for storage, LPDDR for low power and HBM for bandwidth.**

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

<a id="topic-1-suited-roles"></a>

### Why Each Memory Is Suited To Its Role

This section is the key to understanding Topic 1. Do not memorize only "SRAM is fast" and "DRAM is dense". Always connect the physical behavior of the memory to the SoC design reason.

#### 1. Register File Is Suited For Immediate Computation

A **register file** is inside the processor or accelerator. It is used for the values that the execution unit needs right now. For example, if an ALU - Arithmetic Logic Unit adds two numbers, those numbers are usually read from registers, not from DRAM.

It is suited for this role because it can be built with very fast, often multi-port storage close to the datapath. But it is extremely expensive in area, so it is only used for a small number of values.

#### 2. SRAM Is Suited For Fast On-Chip Memory

**SRAM - Static Random Access Memory** stores data using latch-based cells. Because the cell holds its state while power is present, it does not need refresh. That makes it fast and simple to access compared with DRAM.

It is suited for caches, scratchpads, TCM, FIFOs and local buffers because these structures need low latency, frequent reads/writes and predictable behavior. It is not suited for huge main memory because each SRAM bit uses more transistors and more silicon area than DRAM.

#### 3. Cache SRAM Is Suited For Average Performance

A **cache** is SRAM used automatically by hardware to keep recently used instructions or data close to the CPU. It is suited when programs show locality: recently used addresses are likely to be reused, and nearby addresses are likely to be accessed soon.

Cache is excellent for average performance because many accesses become cache hits. But it is less ideal for strict real-time deadlines because a cache miss may take much longer than a hit.

#### 4. Scratchpad And TCM Are Suited For Predictable Real-Time Access

**Scratchpad memory** and **TCM - Tightly Coupled Memory** are SRAM-based memories controlled by software or system configuration. They are suited for real-time code because the access time is more predictable than cache.

For example, an interrupt handler, motor-control loop or DSP kernel may be placed in TCM so the processor does not unexpectedly wait for a cache miss or off-chip DRAM access.

#### 5. DRAM Is Suited For Large Main Memory

**DRAM - Dynamic Random Access Memory** stores each bit as charge on a capacitor. A capacitor-based cell is much smaller than an SRAM latch, so DRAM gives much higher density and lower cost per bit.

It is suited for large main memory because software, operating systems, graphics, AI workloads and applications need much more memory than can fit economically in SRAM. The cost is that DRAM is slower, needs refresh, and needs a controller to obey timing commands.

#### 6. LPDDR Is Suited For Mobile And Low-Power Main Memory

**LPDDR - Low-Power Double Data Rate** is DRAM optimized for power-sensitive systems. It is suited for smartphones, tablets, automotive embedded platforms and battery-powered SoCs because it provides DRAM capacity and bandwidth while reducing operating and standby power.

The tradeoff is that LPDDR still needs a specialized controller/PHY and power-state management. It is not just "normal RAM"; it is a power-optimized DRAM interface family.

#### 7. HBM Is Suited For Extreme Bandwidth

**HBM - High Bandwidth Memory** uses stacked DRAM dies and a very wide interface placed close to the processor or accelerator. It is suited for GPUs, AI accelerators and high-performance computing chips where thousands of operations need data every cycle.

HBM is not selected mainly for low cost. It is selected when bandwidth and energy per transferred bit are more important than package simplicity and cost.

#### 8. ROM And NOR Flash Are Suited For Boot

When the SoC is powered on, SRAM and DRAM do not contain valid program code because they are volatile. The CPU needs a non-volatile place to fetch the first instructions. This is why SoCs use **ROM - Read Only Memory** or **NOR Flash** for boot code.

ROM is suited when the code is fixed permanently. NOR Flash is suited when the system needs non-volatile firmware that can be updated and read randomly. NOR can also support **XIP - Execute In Place**, where the CPU executes code directly from Flash.

#### 9. NAND Flash, eMMC And UFS Are Suited For Large Storage

**NAND Flash** is optimized for high density and low cost per bit. It is suited for storing operating-system images, applications, logs, media and user data. It is not ideal for direct instruction execution because it is page/block-oriented and needs management.

**eMMC - embedded MultiMediaCard** and **UFS - Universal Flash Storage** are managed NAND storage solutions. They are suited when the SoC designer wants Flash storage without manually handling every raw NAND detail. The internal controller handles tasks such as ECC, bad-block management and wear leveling.

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

**NOR Flash** is a type of **non-volatile Flash memory** used mainly for boot code, firmware and code storage. **Non-volatile** means it keeps data even when power is removed. This is why it is useful for storing the first program that runs when the SoC powers on.

The name **NOR** comes from the internal memory-cell connection style, which resembles NOR-gate-style organization. The important exam idea is not the transistor-level circuit detail, but the behavior: **NOR Flash supports efficient random read access**, so the processor can read instructions from different addresses without first loading a whole large block into RAM.

In an SoC system, NOR Flash is usually not used as the main working memory. It is used as **program/firmware storage**. At reset, the processor must fetch its first instructions from somewhere stable. Since SRAM and DRAM lose contents when power is off, boot code must come from ROM or non-volatile Flash. NOR Flash is useful here because it can be read like a memory-mapped device.

Important definition:

```text
NOR Flash = non-volatile memory with good random read access,
commonly used for boot code, firmware and execute-in-place code.
```

#### Why NOR Flash Is Used For Boot

When an SoC is powered on, the CPU needs a reset vector or boot address. That address must contain valid instructions before DRAM is initialized. NOR Flash is suitable because:

- it retains code without power,
- it supports fast random reads,
- it can be memory-mapped into the processor address space,
- it can support **XIP - Execute In Place**,
- it is reliable for small boot and firmware images.

**XIP - Execute In Place** means the CPU can execute code directly from NOR Flash instead of first copying the code into RAM. This is useful in embedded systems where boot time, simplicity and small memory footprint matter.

Key characteristics:

- **Non-volatile**: keeps data without power.
- **Good random read behavior**: individual addresses can be read efficiently compared with NAND Flash.
- **Memory-mapped code access**: can appear in the CPU address map like a readable memory region.
- **Suitable for boot and firmware**: stores reset code, bootloader and firmware image.
- **Supports XIP - Execute In Place** in many systems: code can run directly from Flash.
- **More expensive per bit than NAND Flash**: not ideal for very large storage.
- **Slower write/erase compared with RAM**: not suitable for frequent high-speed writes.
- **Limited write/erase endurance**: Flash cells wear out after many program/erase cycles.
- **Usually smaller capacity than NAND**: used for code storage, not mass storage.

#### How NOR Flash Is Different From RAM

**RAM - Random Access Memory**, such as SRAM or DRAM, is used for active computation because it supports fast reads and writes. But most RAM is volatile, so it loses data when power is removed.

NOR Flash is the opposite in purpose. It is non-volatile, so it stores code permanently, but writes and erases are much slower than RAM. Therefore, firmware may be stored in NOR Flash, while variables, stack, heap and frequently changing data are placed in SRAM or DRAM.

```text
NOR Flash = stores code permanently, slower writes, non-volatile
RAM       = stores working data temporarily, fast reads/writes, usually volatile
```

#### How NOR Flash Is Different From NAND Flash

Both NOR Flash and NAND Flash are non-volatile, but they are optimized for different jobs.

**NOR Flash** is better for random reads and code execution. It is used for boot code and firmware. It is more expensive per bit and usually lower density.

**NAND Flash** is better for high-density storage. It stores large files, operating-system images, media and user data. But NAND usually needs a controller for **ECC - Error Correction Code**, bad-block management and wear leveling. It is not as convenient for direct code execution.

| Point | NOR Flash | NAND Flash |
|---|---|---|
| Best for | Boot code, firmware, XIP | Large storage, files, OS images |
| Read behavior | Good random read | Better sequential/page-based access |
| Density | Lower than NAND | Higher than NOR |
| Cost per bit | Higher | Lower |
| Execute directly? | Often possible through XIP | Usually not directly; code is copied to RAM |
| Controller need | Simpler | More complex: ECC, bad blocks, wear leveling |

#### Where NOR Flash Sits In The Boot Flow

Typical boot flow:

```text
Power ON / Reset
      |
      v
CPU fetches reset vector from ROM or NOR Flash
      |
      v
Bootloader starts
      |
      v
Initialize clocks, SRAM, DRAM controller and peripherals
      |
      v
Load larger firmware/OS from Flash/storage if needed
      |
      v
Run application
```

If NOR Flash supports XIP, some code may continue running directly from NOR Flash. If the application needs higher speed, the bootloader may copy code from NOR Flash into SRAM or DRAM and execute from there.

#### Why NOR Flash Is Not Used For Everything

NOR Flash is excellent for boot and firmware, but it is not used as general-purpose main memory because:

- writes are slow,
- erases happen in blocks/sectors,
- endurance is limited,
- cost per bit is higher than NAND,
- density is lower than NAND,
- SRAM/DRAM are much faster for active data.

So a typical SoC may use:

```text
ROM or NOR Flash -> first boot code
SRAM             -> stack, variables, small fast buffers
DRAM/LPDDR       -> large runtime memory
NAND/eMMC/UFS    -> mass storage
```

Exam line: **NOR Flash is non-volatile memory with good random-read behavior, commonly used for boot code and firmware because it can be memory-mapped and may support execute-in-place, but it is slower to write, endurance-limited and more expensive per bit than NAND Flash.**

### NAND Flash

**NAND Flash** is a type of **non-volatile Flash memory** optimized for **high storage density** and **low cost per bit**. Non-volatile means it keeps data even when power is removed. NAND Flash is mainly used for **mass storage**, not for direct instruction execution.

The name **NAND** comes from the internal memory-cell connection style, which resembles NAND-gate-style organization. The key exam idea is this: NAND Flash stores a lot of data cheaply, but it is accessed in larger chunks and needs more management than NOR Flash.

Important definition:

```text
NAND Flash = dense non-volatile memory used for mass storage,
such as OS images, apps, media, logs and user data.
```

#### Why NAND Flash Exists

An SoC often needs two different kinds of non-volatile memory:

1. **Small reliable boot/code memory**: this may be ROM or NOR Flash.
2. **Large storage memory**: this is usually NAND Flash or managed NAND such as eMMC/UFS.

NOR Flash is good for random code reads, but it is too expensive per bit for very large storage. NAND Flash solves the capacity problem. It can store large amounts of data at lower cost, which is why it is used in phones, SSDs, memory cards, embedded storage and many consumer devices.

Why NAND Flash is used:

- It gives high storage density.
- It has lower cost per bit than NOR Flash.
- It is non-volatile.
- It is suitable for large firmware images, operating systems, applications, logs and user data.
- It is widely available in managed forms such as **eMMC - embedded MultiMediaCard** and **UFS - Universal Flash Storage**.

#### Page And Block-Based Access

NAND Flash is not accessed like SRAM or NOR Flash. It is organized into **pages** and **blocks**.

- A **page** is the unit normally used for reading and programming/writing.
- A **block** is a group of pages and is the unit normally used for erase.

This creates an important rule:

```text
NAND can read/program pages,
but erase usually happens at block level.
```

Example:

```text
Block
 ├── Page 0
 ├── Page 1
 ├── Page 2
 ├── ...
 └── Page N
```

If software wants to update a small piece of data, the NAND controller may need to manage page writes, block erases and data movement. This is why NAND needs a controller and management algorithms.

#### Why NAND Is Not Used For Direct Code Execution

NAND Flash is usually not ideal for **XIP - Execute In Place**. XIP means executing code directly from non-volatile memory. NOR Flash can support this more easily because it has better random read behavior and can be memory-mapped for instruction fetch.

NAND Flash is more storage-oriented:

- random reads are slower than NOR,
- reads are page-based,
- bad blocks must be handled,
- ECC is needed,
- code often must be copied into RAM before execution.

Typical boot idea:

```text
ROM / NOR Flash starts boot
      |
      v
Bootloader initializes SRAM/DRAM
      |
      v
Bootloader copies OS/firmware from NAND/eMMC/UFS to RAM
      |
      v
CPU executes from RAM
```

This is why the short line says: **NAND is used for storage rather than direct code execution.**

Key characteristics:

- **Very high density**: stores many bits in a small area.
- **Low cost per bit**: cheaper than NOR Flash for large storage.
- **Non-volatile**: retains data without power.
- **Page/block-based access**: reads and programs pages, erases blocks.
- **Slower random read than NOR**: less suitable for direct instruction fetch.
- **Writes and erases are more complex**: erase must occur before rewriting many Flash cells.
- **Limited endurance**: each block can tolerate only a limited number of program/erase cycles.
- **Requires ECC - Error Correction Code**: raw NAND can have bit errors, so error correction is necessary.
- **Requires bad-block management**: some blocks may be bad from manufacturing or become bad over time.
- **Requires wear leveling**: writes must be spread across blocks so the same block is not worn out too quickly.
- **Often managed through eMMC - embedded MultiMediaCard, UFS - Universal Flash Storage or SSD controllers**: these controllers hide much of the NAND complexity from the SoC.

#### ECC - Error Correction Code In NAND

NAND Flash is dense, but density comes with reliability challenges. Some bits may read incorrectly due to noise, wear, retention loss or cell interference. Therefore, NAND systems use **ECC - Error Correction Code**.

ECC adds extra check bits so the controller can:

- detect bit errors,
- correct correctable errors,
- report uncorrectable errors,
- improve storage reliability.

Exam line: **ECC is essential in NAND Flash because dense Flash cells are error-prone and the controller must detect and correct bit errors.**

#### Bad-Block Management

NAND Flash may contain bad blocks even when new. More blocks may become bad as the memory is used. Therefore, the controller maintains a bad-block table and avoids using those blocks.

Without bad-block management, data could be written into unreliable regions and become corrupted.

Exam line: **Bad-block management prevents the system from storing data in NAND blocks that are defective or have become unreliable.**

#### Wear Leveling

Flash memory wears out because program/erase cycles stress the memory cells. If the same block is erased and written repeatedly, it will fail earlier than other blocks.

**Wear leveling** spreads writes across many blocks so that no small set of blocks wears out too quickly.

Example:

```text
Bad approach: write logs repeatedly to the same block.
Better approach: rotate log writes across many blocks.
```

Exam line: **Wear leveling increases NAND lifetime by distributing program/erase cycles across many physical blocks.**

#### Managed NAND: eMMC And UFS

Raw NAND is difficult to use directly because the SoC must handle ECC, bad blocks, wear leveling, page mapping and erase management. Many systems therefore use managed NAND devices.

**eMMC - embedded MultiMediaCard** is a managed NAND storage solution with an internal controller. It is common in embedded systems.

**UFS - Universal Flash Storage** is a higher-performance managed Flash storage interface, common in phones and high-performance embedded devices.

Managed NAND hides much of the raw NAND complexity:

```text
SoC sends read/write storage commands
      |
      v
eMMC/UFS controller handles NAND management internally
      |
      v
NAND Flash stores the actual data
```

#### NAND Cell Density Types

NAND stores more bits per cell in variants:

- **SLC - Single-Level Cell**: one bit per cell; high endurance and performance.
- **MLC - Multi-Level Cell**: two bits per cell; higher density, lower endurance than SLC.
- **TLC - Triple-Level Cell**: three bits per cell; higher density, lower endurance/performance.
- **QLC - Quad-Level Cell**: four bits per cell; very high density, stronger latency/endurance tradeoff.

The trend is:

```text
More bits per cell -> higher density and lower cost per bit
More bits per cell -> lower endurance, slower writes and harder error correction
```

#### NAND Flash Vs NOR Flash

| Point | NAND Flash | NOR Flash |
|---|---|---|
| Best use | Large storage | Boot code and firmware |
| Access style | Page/block-oriented | Better random read |
| Density | Very high | Lower |
| Cost per bit | Low | Higher |
| Direct execution | Usually not preferred | Often supports XIP |
| Controller complexity | High: ECC, bad blocks, wear leveling | Simpler |
| Example use | eMMC, UFS, SSD, media storage | Boot Flash, firmware, BIOS-like code |

Exam line: **NAND Flash is dense non-volatile storage used for mass data, but it needs page/block management, ECC, bad-block management and wear leveling; NOR Flash is better for boot and direct code reads.**

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

<a id="topic-1-selection"></a>

### Memory Technology Selection In SoC

SoC designers choose memory technology by asking a practical question:

```text
What kind of data is this, how fast must it be accessed,
how much of it is needed, and must it survive power-off?
```

The answer decides the memory technology.

#### 1. If The Data Is Needed Immediately

Use **register files** or very small local SRAM.

This is the case for CPU operands, accelerator partial sums, DSP coefficients being used in the current cycle, status flags and pipeline state. These memories must be extremely close to the logic because every extra cycle can reduce processor throughput.

Why suited:

- fastest access,
- close to execution logic,
- can support multiple reads/writes per cycle,
- avoids waiting for larger memory.

Why not used for everything:

- too small,
- too expensive in silicon area,
- not suitable for large program/data storage.

#### 2. If The Data Is Frequently Reused

Use **SRAM cache**.

This is common for CPU instructions, stack data, array data and recently accessed memory lines. Cache is suitable because programs often reuse the same data or nearby data. The cache controller automatically keeps useful copies near the processor.

Why suited:

- improves average memory access time,
- reduces off-chip DRAM traffic,
- hides main-memory latency,
- uses SRAM speed for frequently used data.

Why not always enough:

- cache misses are slower,
- cache behavior may be unpredictable,
- coherence is needed in multi-core systems,
- cache consumes area and power.

#### 3. If The Data Has A Real-Time Deadline

Use **TCM - Tightly Coupled Memory**, scratchpad memory or local SRAM buffers.

This is common for interrupt handlers, motor control, sensor loops, communication deadlines, safety checks and DSP kernels. In these cases, predictable timing is more important than average speed. Cache may be fast on average, but a miss can break a real-time deadline.

Why suited:

- deterministic access latency,
- software can decide what is stored there,
- avoids cache-miss uncertainty,
- useful for real-time and safety-critical code.

Why not used for everything:

- limited capacity,
- requires software/compiler planning,
- not automatically managed like cache.

#### 4. If The System Needs Large Runtime Memory

Use **DRAM - Dynamic Random Access Memory**, usually as **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory** or **LPDDR - Low-Power Double Data Rate**.

This is the main working memory for operating systems, large applications, graphics buffers, AI tensors, multimedia buffers and large data structures. SRAM cannot provide this capacity economically, so DRAM is used.

Why suited:

- high density,
- lower cost per bit than SRAM,
- large available capacity,
- supports burst transfers and bank-level parallelism.

Why it needs controller support:

- DRAM needs refresh,
- rows must be activated and precharged,
- timing rules must be obeyed,
- banks must be scheduled,
- PHY training/calibration may be needed for high-speed DDR/LPDDR.

#### 5. If The System Is Battery Or Power Sensitive

Use **LPDDR - Low-Power Double Data Rate** for main memory, plus aggressive on-chip SRAM buffering and power modes.

LPDDR is suitable for mobile and embedded SoCs because off-chip memory access can consume significant energy. LPDDR reduces power through low-voltage operation and low-power states such as self-refresh or deep power-down modes.

Why suited:

- lower-power DRAM operation,
- useful standby modes,
- good capacity for mobile systems,
- suitable for package-constrained devices.

Why not always selected:

- still needs a complex controller and PHY,
- power-state transitions must be managed,
- may not be the cheapest or simplest choice for every system.

#### 6. If The System Is Bandwidth Limited

Use wider memory systems, multiple channels, on-chip SRAM tiling, or **HBM - High Bandwidth Memory**.

AI accelerators, GPUs and high-performance networking chips may perform enough computation that ordinary memory bandwidth becomes the bottleneck. HBM is suited because it provides a very wide, close memory interface using stacked DRAM and advanced packaging.

Why suited:

- very high bandwidth,
- good energy per transferred bit for heavy data movement,
- keeps parallel compute units fed,
- reduces long board-level memory traces.

Why not used everywhere:

- high package cost,
- design complexity,
- not necessary for low-bandwidth microcontrollers or simple embedded SoCs.

#### 7. If The Data Must Exist At Power-On

Use **ROM - Read Only Memory** or **NOR Flash**.

When the chip resets, volatile memories such as SRAM and DRAM do not contain valid boot code. The CPU must fetch the first instruction from a non-volatile memory region. This is why boot ROM and NOR Flash are important.

Why suited:

- retains code without power,
- available at reset,
- can store bootloader and secure boot code,
- NOR can support random reads and XIP - Execute In Place.

Why not used for active working memory:

- writes are slow or impossible,
- erase/program cycles are limited,
- lower density than NAND for large storage,
- not suitable for stack/heap variables that change frequently.

#### 8. If The Data Is Large Persistent Storage

Use **NAND Flash**, **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** or SSD-like storage.

This is used for operating-system images, application files, user data, logs, media and large firmware images. NAND is suited because it stores many bits cheaply.

Why suited:

- high density,
- low cost per bit,
- non-volatile,
- widely available as managed storage.

Why controller management is required:

- NAND has page/block access rules,
- erase happens at block level,
- blocks wear out after program/erase cycles,
- ECC is needed to correct bit errors,
- bad blocks must be avoided,
- wear leveling spreads writes across the device.

#### Example Design Choices

For a small microcontroller SoC:

- ROM or NOR Flash stores boot/program code because it is non-volatile.
- SRAM stores stack, heap, variables and buffers because it is fast and simple.
- TCM may store interrupt handlers because timing must be predictable.
- Off-chip DRAM may be absent because the system does not need huge capacity.

For a smartphone SoC:

- boot ROM starts secure boot because it is trusted and non-volatile.
- SRAM caches and TCM support CPU, GPU, DSP and modem workloads.
- LPDDR provides large low-power main memory.
- UFS or eMMC stores the operating system, apps, photos and user data.

For an AI accelerator:

- SRAM buffers hold activations, weights and partial sums near compute arrays.
- HBM or LPDDR supplies large external bandwidth.
- DMA - Direct Memory Access engines move data without constant CPU involvement.
- memory reuse is critical because moving data often costs more energy than computing on it.

For a networking SoC:

- SRAM or QDR SRAM stores fast packet buffers and lookup tables.
- FIFOs absorb bursty traffic between interfaces and processing blocks.
- DRAM stores large packet queues.
- Flash stores firmware.
- low-latency random access matters because packet decisions must be made quickly.

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

Memory technology in SoC design means the physical and architectural type of memory used to store instructions, data, temporary results, buffers, firmware and persistent information. An SoC does not use a single memory technology because different data has different requirements. The CPU needs extremely fast operands, real-time software needs predictable access, applications need large working memory, and the system needs non-volatile storage for boot code and files. Therefore, memory technology selection is one of the central tradeoffs in SoC design.

The basic idea is that memory stores bits at addresses. A processor or hardware block reads from an address to get data and writes to an address to update data. However, all storage locations cannot be built using the same memory cell. A very fast memory cell usually consumes more area and power. A dense memory cell stores many bits cheaply but is usually slower or harder to control. A non-volatile memory keeps data without power but may have slower write/erase operation and limited endurance. Hence, SoCs use a hierarchy of register files, SRAM, DRAM, ROM and Flash-based storage.

The fastest storage is the **register file**, which is inside the processor or accelerator datapath. It is suited for immediate computation because arithmetic and logic units need operands every cycle. Register files are extremely fast but very small and expensive per bit, so they cannot be used for large program or data storage.

The next important technology is **SRAM - Static Random Access Memory**. SRAM is volatile memory that stores each bit using latch-based cells. It is called static because it does not need periodic refresh while power is supplied. SRAM gives low latency and good random-access behavior, so it is suited for on-chip caches, scratchpad memories, TCM - Tightly Coupled Memory, FIFOs - First-In First-Out buffers, packet buffers and lookup tables. The reason SRAM is suited for these uses is that these blocks need frequent fast reads and writes close to the processor or accelerator. The limitation is that SRAM uses more transistors per bit than DRAM, so it occupies large die area and has high cost per bit.

SRAM can be used in two important architectural ways. In a **cache**, hardware automatically stores recently used instructions or data to improve average memory access time. Cache is useful because programs show locality. In **scratchpad memory** or **TCM**, software or system configuration decides what is stored there. Scratchpad and TCM are useful for real-time systems because their latency is predictable, while cache latency can vary because of cache hits and misses.

For large runtime memory, SoCs use **DRAM - Dynamic Random Access Memory**. DRAM stores a bit as charge on a capacitor. This cell is much smaller than an SRAM latch, so DRAM provides higher density and lower cost per bit. This makes DRAM suited for main memory: operating-system memory, large applications, graphics buffers, AI data, multimedia buffers and general program data. However, capacitor charge leaks away, so DRAM needs refresh. It also requires commands such as activate, read, write, precharge and refresh. Therefore, a DRAM-based system needs a memory controller and PHY - Physical Layer.

Modern SoCs usually access external DRAM through **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory**, **LPDDR - Low-Power Double Data Rate** or **HBM - High Bandwidth Memory**. DDR SDRAM is suited for general high-capacity main memory because it transfers data on both clock edges and supports burst transfers. LPDDR is suited for mobile and embedded SoCs because it provides DRAM capacity with lower-power operation and power-saving modes. HBM is suited for GPUs, AI accelerators and high-performance systems because stacked DRAM and a very wide interface provide extremely high bandwidth, although cost and package complexity increase.

Some SoCs may use **eDRAM - Embedded Dynamic Random Access Memory** as an intermediate technology. eDRAM is denser than SRAM and can be useful for large on-chip buffers or caches, but it still needs refresh and is harder to integrate with standard logic processes. Therefore, it is a compromise between SRAM speed and DRAM density, not a universal replacement for either.

The SoC also needs non-volatile memory because volatile memories lose data when power is removed. **ROM - Read Only Memory** stores fixed boot code, reset vectors or permanent tables. It is suited for first-stage boot because it is available immediately after reset and cannot be accidentally erased. The limitation is that ROM is inflexible after fabrication.

**NOR Flash** is non-volatile memory suited for firmware, bootloaders and execute-in-place code. It has good random read behavior and can often be memory-mapped into the processor address space. This means the CPU can fetch instructions directly from NOR Flash in many embedded systems. NOR is not used for mass storage because it has lower density and higher cost per bit than NAND Flash, and write/erase operations are slower than RAM.

**NAND Flash** is non-volatile memory suited for large persistent storage. It is used in storage devices such as **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** and SSDs because it provides high density and low cost per bit. NAND is not normally used for direct code execution because it is page/block-oriented and needs management. A NAND controller must handle **ECC - Error Correction Code**, bad-block management, wear leveling, mapping and erase management.

The main tradeoffs in memory technology are speed versus density, capacity versus area, volatility versus persistence, bandwidth versus power, endurance versus write frequency and simplicity versus controller complexity. On-chip SRAM is fast and predictable but expensive in area. Off-chip DRAM is large and cheaper per bit but has higher latency, I/O power and controller complexity. ROM and Flash preserve data without power but are slower or less flexible for writes. Thus, a good SoC memory system uses each technology where it is strongest: registers and SRAM near computation, DRAM/LPDDR/HBM for large runtime memory, and ROM/NOR/NAND-based memory for boot and persistent storage.

Therefore, memory technology selection directly affects SoC performance, power, cost, die area, boot behavior and memory-controller architecture. The memory controller is simple for SRAM, timing-oriented for DRAM and management-heavy for NAND Flash. This is why memory technology is not only a storage topic; it is a complete SoC architecture decision.

### Short 10-Mark Exam Answer

Memory technology in SoC design means the physical and architectural type of memory used to store instructions, data, buffers, firmware and persistent information. Different technologies are required because no single memory is best in speed, capacity, power, cost, area and non-volatility.

Register files are used inside processors for immediate operands because they are the fastest but very small. **SRAM - Static Random Access Memory** is volatile, fast and does not require refresh, so it is used for caches, scratchpads, TCM - Tightly Coupled Memory, FIFOs and small on-chip buffers. SRAM is not used for huge memory because it has large area and high cost per bit.

**DRAM - Dynamic Random Access Memory** stores data as charge on capacitors and therefore needs refresh. It is denser and cheaper per bit than SRAM, so it is used for large main memory. In SoCs, this is usually external **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory** or **LPDDR - Low-Power Double Data Rate**. LPDDR is used in mobile/embedded SoCs because it reduces memory power. **HBM - High Bandwidth Memory** is used when very high bandwidth is required, such as in GPU or AI accelerator SoCs.

Non-volatile memories are used when data must remain after power-off. **ROM - Read Only Memory** stores fixed boot code. NOR Flash is used for boot firmware and XIP - Execute In Place because it has good random-read behavior. NAND Flash is used for high-density storage such as **eMMC - embedded MultiMediaCard**, **UFS - Universal Flash Storage** and SSDs, but it needs **ECC - Error Correction Code**, bad-block management and wear leveling.

The main tradeoffs are latency, bandwidth, density, area, power, volatility, endurance, retention and controller complexity. Thus, a good SoC uses fast SRAM near computation, DRAM/LPDDR/HBM for large runtime memory and ROM/NOR/NAND-based memory for boot and storage.

<a id="topic-1-technical-words"></a>

### Technical Words To Use For Marks

- **Bit** (write this because memory fundamentally stores 0/1 values.)
- **Byte** (write this because memory capacity and addresses are often discussed in bytes.)
- **Address** (write this because processors access memory by specifying locations.)
- **Read operation** (write this because memory access includes fetching stored data.)
- **Write operation** (write this because memory access includes updating stored data.)
- **Working memory** (write this because SRAM/DRAM are used during active computation.)
- **Main memory** (write this because DRAM/DDR/LPDDR are usually the large runtime memory.)
- **Storage memory** (write this because ROM/Flash/eMMC/UFS retain data after power-off.)
- **Memory technology** (write this because the question asks about the physical/architectural memory types used in SoC.)
- **Volatile memory** (write this because SRAM and DRAM lose data when power is removed.)
- **Non-volatile memory** (write this because ROM and Flash retain boot code and persistent data.)
- **Register file** (write this because it is the fastest small storage inside a processor or accelerator.)
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
- **PHY - Physical Layer** (write this because high-speed DDR/LPDDR/HBM memory needs electrical interface circuitry.)
- **XIP - Execute In Place** (write this because NOR Flash may allow direct code execution from non-volatile memory.)
- **SLC/MLC/TLC/QLC** (write this because NAND density and endurance depend on how many bits are stored per cell.)

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

**L1 cache** means **Level 1 cache**. It is the first cache level seen by the processor core and is usually the closest memory structure after the CPU register file. It is made using fast **SRAM - Static Random Access Memory** because the processor may need to access it almost every cycle.

The main purpose of L1 cache is to avoid going to slower lower-level memory for every instruction and data access. Without L1 cache, the CPU would frequently wait for L2 cache, L3 cache or off-chip DRAM. With L1 cache, many accesses are satisfied close to the core.

Important definition:

```text
L1 cache = smallest and fastest cache level placed closest to the CPU core,
used to store recently or nearby-used instructions and data.
```

#### L1 Instruction Cache And L1 Data Cache

L1 cache is often split into:

- **I-cache - Instruction cache**: stores recently fetched program instructions.
- **D-cache - Data cache**: stores recently accessed data such as variables, stack values, arrays and structure fields.

This split is common because the CPU often needs to fetch an instruction and access data in the same cycle. If instruction fetch and data access used one small unified cache port, they could conflict. Separate I-cache and D-cache allow instruction fetch and data load/store operations to happen in parallel.

Simple view:

```text
              +----------------+
              |   CPU Core     |
              +---+--------+---+
                  |        |
          instruction    data load/store
                  |        |
                  v        v
            +---------+  +---------+
            | I-cache |  | D-cache |
            +---------+  +---------+
                  \        /
                   v      v
                  L2 / lower memory
```

#### How L1 Cache Works

When the processor wants an instruction or data item, it sends an address. The L1 cache checks whether a copy of that address is already present.

- If present, it is a **cache hit**. Data is returned quickly from L1.
- If absent, it is a **cache miss**. The data must be fetched from L2/L3/DRAM, and the CPU may stall or wait.

Caches usually move data in **cache lines** or **cache blocks**, not only one byte at a time. A cache line is a small fixed-size block of adjacent memory addresses. For example, if the CPU reads one address, the cache may bring the surrounding nearby addresses too. This is important because of spatial locality.

Inside the cache, each stored cache line usually has:

- **data field**: the actual instruction/data bytes stored in the cache line,
- **tag field**: identifies which main-memory address region this cache line belongs to,
- **valid bit**: tells whether the cache entry contains meaningful data,
- **dirty bit** in write-back data caches: tells whether cached data has been modified and must later be written back to lower memory.

The processor address is commonly divided into:

```text
Tag + Index + Offset
```

- **Index** selects which cache location/set to check.
- **Tag** is compared to confirm that the selected entry is the correct memory block.
- **Offset** selects the required byte/word inside the cache line.

This is how the cache knows whether an access is a hit or miss. If the valid bit is set and the tag matches, it is a cache hit. If the tag does not match or the valid bit is not set, it is a cache miss.

Use of L1 cache:

- recently used instructions,
- recently used data,
- reducing instruction fetch and data fetch delay,
- reducing average memory access time,
- reducing traffic to L2/L3/DRAM,
- keeping the processor pipeline supplied with instructions and operands.

#### Relation With Locality

L1 cache exists because programs show **locality**.

**Temporal locality** means that if an instruction or data value is used now, it may be used again soon. Example: a loop executes the same instructions repeatedly, so those instructions remain useful in the I-cache. A frequently used variable may remain useful in the D-cache.

**Spatial locality** means that if one memory address is used, nearby addresses may be used soon. Example: when a program reads an array, it often reads consecutive elements. The D-cache brings a full cache line, so nearby array elements are already available for the next accesses.

**Sequential locality** is especially important for the I-cache. Program instructions are often fetched from consecutive addresses. So when the I-cache fetches a block of instructions, the next instruction is likely already present.

Examples:

```c
for (i = 0; i < 100; i++) {
    sum = sum + a[i];
}
```

In this loop:

- The loop instructions show **temporal locality** because the same instructions execute again and again.
- The array `a[i]` shows **spatial locality** because `a[0]`, `a[1]`, `a[2]` and nearby elements are stored close together.
- The instruction stream shows **sequential locality** because the CPU normally fetches the next instruction after the current one.

This is why a small L1 cache can be very effective. It does not need to store the entire program. It only needs to store the small active working part of the program.

Tradeoff:

- very fast,
- limited capacity,
- more area and power per bit,
- may create unpredictability due to misses,
- split I-cache/D-cache increases parallel access but duplicates some control structures,
- cache consistency must be handled when DMA or other masters modify memory,
- in real-time systems, cache misses can make timing less predictable than TCM or scratchpad memory.

Exam line: **L1 cache improves average memory access time by exploiting temporal, spatial and sequential locality; I-cache benefits mainly from repeated/sequential instruction fetch, while D-cache benefits from repeated and nearby data accesses.**

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

The **memory controller** is a digital hardware block in the SoC that manages access to memory. It receives read/write requests from processors, caches, DMA engines and accelerators, then converts those requests into legal memory operations for the actual memory device.

Important definition:

```text
Memory controller = hardware block that accepts memory requests from the SoC,
arbitrates and schedules them, and generates the correct commands/timing
for the target memory technology.
```

It normally sits between the **SoC interconnect/cache subsystem** and the external memory interface.

Simple placement:

```text
CPU / GPU / DMA / DSP / AI accelerator / peripherals
        |
        v
Cache subsystem / SoC interconnect / NoC
        |
        v
Memory Controller
        |
        v
PHY - Physical Layer
        |
        v
External DRAM / LPDDR / DDR / HBM
```

The memory controller is not just software. It is mostly **physical digital logic inside the SoC**. Firmware or software may configure its registers, but the controller hardware performs the actual arbitration, timing, command generation, refresh control and response handling.

#### What The Memory Controller Does

A memory controller may perform:

- **Address decoding**: decides which memory region or device a request belongs to.
- **Address mapping**: maps system addresses into channel, rank, bank, row and column fields for DRAM.
- **Arbitration**: decides which requester gets service first when multiple masters request memory.
- **Command scheduling**: orders memory commands to improve bandwidth and reduce latency.
- **Timing control**: obeys memory timing parameters such as activate-to-read delay, precharge time and refresh time.
- **Refresh control**: periodically refreshes DRAM cells so data is not lost.
- **Read/write data buffering**: temporarily stores pending reads and writes.
- **QoS - Quality of Service**: gives priority or bandwidth guarantees to urgent traffic such as display, camera or real-time audio.
- **ECC - Error Correction Code** if supported: detects and corrects memory bit errors.
- **Power management**: enters/exits low-power modes such as self-refresh or power-down.

#### Why DRAM Is Mentioned In This Discussion

In a memory hierarchy question, **DRAM - Dynamic Random Access Memory** is mentioned because it is usually the large **main memory** at the lower level of the hierarchy. When an access misses in L1/L2/L3 cache, the data often has to come from off-chip DRAM, DDR SDRAM or LPDDR. That access is much slower than an L1 cache hit, so DRAM creates the major **miss penalty** in AMAT - Average Memory Access Time.

DRAM is also mentioned because it cannot be accessed like simple SRAM. SRAM can often be treated like a simple addressable memory: give address, read/write data, obey simpler timing. DRAM is different because it is organized into **banks, rows and columns** and stores bits as charge on capacitors. The controller must open a row using an **ACTIVATE** command, read or write columns, close rows using **PRECHARGE**, and periodically perform **REFRESH**.

So when we say "memory controller pressure" or "DRAM traffic", we mean:

```text
More cache misses / DMA transfers / accelerator requests
        -> more requests reach the memory controller
        -> more commands must be scheduled to DRAM
        -> higher latency, contention and bandwidth demand
```

This is why DRAM is central to the memory hierarchy discussion. It is the large capacity memory, but it is slower and command/timing-heavy, so the hierarchy tries to reduce unnecessary DRAM accesses.

#### Relation Between Cache Hierarchy And Controller Traffic

If the SoC has a large cache:

- DRAM traffic is reduced,
- memory controller pressure is lower,
- average latency improves.

Meaning: if the data is found in L1/L2/L3 cache, the request does not need to go to external DRAM. The memory controller is not involved for that cache hit. This saves latency, bandwidth and energy.

If the SoC has weak caching:

- more requests reach DRAM,
- controller scheduling becomes more important,
- bandwidth bottlenecks become visible.

Meaning: if cache miss rate is high, more requests travel through the interconnect to the memory controller. The controller must then decide the order of reads/writes and obey DRAM timing. If too many requests arrive, the controller queue fills and latency increases.

#### Relation Between Scratchpad/TCM And DRAM

If the SoC uses scratchpad/TCM:

- software can move critical data closer to compute,
- DRAM accesses become more controlled,
- real-time behavior improves.

Here, **scratchpad memory** and **TCM - Tightly Coupled Memory** are on-chip SRAM-based memories. They are close to the processor or accelerator and are usually software-managed. If a real-time loop, interrupt routine or DSP kernel stores its important code/data in TCM, it does not repeatedly access external DRAM. This reduces dependence on the memory controller.

This is the connection:

```text
Critical data in TCM/scratchpad
        -> fewer unpredictable DRAM accesses
        -> less memory-controller contention
        -> more predictable real-time behavior
```

So the word **DRAM** appears here because scratchpad/TCM is often used to avoid slow, variable-latency DRAM access. DRAM is excellent for large capacity, but not ideal for strict real-time deadlines because its access time depends on cache misses, controller queues, bank conflicts, row hits/misses and refresh.

#### Relation With Multiple SoC Masters

If the SoC has multiple masters:

- memory controller must arbitrate among **CPU - Central Processing Unit**, **GPU - Graphics Processing Unit**, **DMA - Direct Memory Access**, **DSP - Digital Signal Processor**, camera/display controllers and accelerators,
- quality-of-service may be required,
- starvation must be avoided,
- real-time traffic may need priority.

A **master** is any SoC block that can initiate memory transactions. The CPU is a master, but it is not the only one. A display controller may continuously read frames from memory. A camera block may continuously write image data. A DMA controller may transfer blocks of data. An AI accelerator may stream weights and activations. If all of them request DRAM at the same time, the memory controller must decide who gets served first.

Example:

```text
Display read request: urgent because missing data can cause screen underflow
CPU request: important for software performance
DMA transfer: high bandwidth but may tolerate some delay
AI accelerator: may need sustained bandwidth
```

The controller uses arbitration and QoS policies so urgent traffic is served on time while other traffic still makes progress. This prevents **starvation**, where one requester waits too long because other requesters keep getting priority.

#### Technology Dependence Of Memory Controllers

The controller depends strongly on memory technology:

| Memory Type | Controller Nature | Why |
|---|---|---|
| SRAM | Simple controller | Random access, no refresh, simpler timing |
| DRAM / DDR / LPDDR | Timing and scheduling controller | Needs activate/read/write/precharge/refresh and bank scheduling |
| HBM | High-bandwidth multi-channel controller | Needs many channels/pseudo-channels and high parallel bandwidth |
| NOR Flash | Command-based controller | Reads are simpler, but program/erase need command sequences |
| NAND Flash | Management-heavy controller | Needs ECC, bad-block management, wear leveling and page/block handling |

Thus, memory hierarchy and memory controller architecture cannot be separated. The hierarchy reduces pressure on main memory, and the controller manages the remaining traffic efficiently.

Exam line: **The memory hierarchy decides how many requests reach main memory; the memory controller decides how those requests are legally and efficiently served by DRAM or another memory technology.**

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

Memory hierarchy also affects memory controller architecture. The **memory controller** is the hardware block that receives memory requests from the cache subsystem, interconnect, DMA engines and accelerators, then converts them into legal commands for the target memory. DRAM is important in this discussion because it is usually the large main memory below the cache hierarchy. When a cache miss occurs, data often must be fetched from DRAM, creating miss penalty. Since DRAM is organized into banks, rows and columns and requires activate, read/write, precharge and refresh operations, the controller must perform timing control, scheduling and arbitration.

A strong cache hierarchy reduces the number of requests reaching DRAM, while weak caching increases memory-controller pressure. Scratchpad or TCM can reduce unpredictable DRAM access by placing critical code/data close to the processor. In multi-master SoCs, the controller must arbitrate among **CPU - Central Processing Unit**, **DMA - Direct Memory Access**, **GPU - Graphics Processing Unit**, **DSP - Digital Signal Processor**, camera/display controllers and accelerators, and may require **QoS - Quality of Service** policies. Thus, memory hierarchy and memory controller design together determine SoC performance, power and real-time behavior.

### Short 10-Mark Exam Answer

Memory design hierarchy in SoC is the arrangement of different memory levels from fastest and smallest to slowest and largest. A typical SoC hierarchy contains registers, L1 cache, L2/L3 cache, scratchpad or **TCM - Tightly Coupled Memory**, on-chip **SRAM - Static Random Access Memory** / **ROM - Read-Only Memory**, off-chip **DRAM - Dynamic Random Access Memory** / **LPDDR - Low-Power Double Data Rate** and Flash storage. This hierarchy is required because fast memories are expensive and small, while large memories are slower but cheaper per bit.

Cache hierarchy improves average memory access time by exploiting temporal and spatial locality. A cache hit gives fast access, while a cache miss causes a miss penalty because data must be fetched from a lower level such as L2, L3 or DRAM. The average memory access time depends on hit time, miss rate and miss penalty.

The main tradeoffs are latency versus capacity, bandwidth versus cost, area versus performance, power versus speed, predictability versus average performance and on-chip versus off-chip placement. On-chip **SRAM - Static Random Access Memory** gives low latency and high bandwidth but consumes die area. Off-chip **DRAM - Dynamic Random Access Memory** gives large capacity but has higher latency, I/O power and controller complexity. Scratchpad / **TCM - Tightly Coupled Memory** gives predictable timing but needs software management, while cache is hardware-managed but can suffer misses.

Thus, a good SoC memory hierarchy places fast memory near computation, large memory farther away and non-volatile memory for boot/storage. This reduces average access time, improves bandwidth, controls cost and reduces pressure on the memory controller. The memory controller is important because it manages the remaining traffic to main memory, especially DRAM/LPDDR, by handling arbitration, command scheduling, timing rules and refresh.

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
- **Memory controller** (write this because it connects the hierarchy to actual external memory access.)
- **DRAM traffic** (write this because cache misses and DMA transfers create requests to main memory.)
- **Arbitration** (write this because multiple SoC masters may request memory at the same time.)
- **Command scheduling** (write this because DRAM commands must be ordered efficiently.)
- **Refresh** (write this because DRAM cells lose charge and must be periodically restored.)
- **QoS - Quality of Service** (write this because display, camera and real-time traffic may need priority.)
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

<a id="topic-3-foundation"></a>

### SDRAM Foundation: What It Is And Why We Use It

To understand SDRAM, first remember the memory hierarchy idea:

```text
CPU registers / cache / SRAM = very fast but small
SDRAM / DDR / LPDDR          = large main memory but slower
Flash / storage              = persistent but much slower for writes
```

**SDRAM - Synchronous Dynamic Random Access Memory** is mainly used as **large main memory** in an SoC system. It is normally outside the SoC die, connected through a memory controller and PHY. It is used because programs, operating systems, image frames, video buffers, AI tensors and application data need much more capacity than on-chip SRAM can provide.

Why we do not simply use SRAM for main memory:

- SRAM is fast, but each bit uses more transistors.
- Large SRAM would consume too much chip area.
- Large SRAM would increase chip cost and leakage power.
- DRAM/SDRAM gives much higher density and lower cost per bit.

Why SDRAM is not as simple as SRAM:

- DRAM stores each bit as charge on a capacitor.
- Capacitor charge leaks with time, so refresh is required.
- A row must be activated before column data can be read/written.
- An already open row may need to be closed before another row is opened.
- Multiple timing rules must be obeyed by the memory controller.

So the reason we study SDRAM basics is this:

```text
SDRAM gives large memory capacity,
but the controller must carefully manage banks, rows, columns,
commands and timing to get good performance.
```

### What "Synchronous" Means

**Synchronous** means the memory operates according to a clock. The memory controller sends commands such as ACTIVATE, READ, WRITE, PRECHARGE and REFRESH on clock edges. Data movement also follows clock timing.

This is important because synchronous operation allows predictable command scheduling. The controller can count clock cycles and know when the next legal command can be issued.

Example:

```text
Clock cycle 0: ACTIVATE row
Clock cycle 1-3: wait tRCD
Clock cycle 4: READ column
Clock cycle 5-8: wait CAS latency
Clock cycle 9 onward: data burst appears
```

This does not mean SDRAM is instantly fast. It means the controller and memory follow a clocked protocol.

### What "Dynamic" Means

**Dynamic** means stored data must be periodically restored. A DRAM cell stores a bit as electrical charge on a tiny capacitor. Charge leaks over time. If the charge is not refreshed, the stored value may be lost.

This is why SDRAM needs **REFRESH**. Refresh is not optional. It is required for data retention. During refresh, the memory may be unavailable for normal access, so refresh contributes to latency and can reduce available bandwidth.

Exam line: **SDRAM is dense because it stores bits in capacitor cells, but it needs refresh and controller-managed timing because capacitor charge leaks and row access is not instant.**

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

Each DRAM cell stores one bit as charge on a capacitor, controlled by an access transistor. A charged capacitor may represent logic 1 and a discharged capacitor may represent logic 0, depending on implementation. Because the stored charge leaks, DRAM must be periodically refreshed.

Simple DRAM cell:

```text
          Bit Line
             |
          +-----+
WL ----->|  T  |---- Storage Capacitor
          +-----+          |
                           C
                           |
                         Ground

WL = word line
T  = access transistor
C  = storage capacitor
```

When a row is selected, the word line turns on the access transistors for many cells in that row. The tiny charge from each capacitor is shared with a bit line. Because this charge is very small, the memory uses **sense amplifiers** to detect and strengthen the value.

Important point: DRAM read is not like reading a simple register. The act of sensing the tiny capacitor charge disturbs the stored charge, so the value must be restored. This is one reason row activation and timing delays exist.

The memory array is organized as:

- rows,
- columns,
- banks,
- row buffers/sense amplifiers.

To access data, the address is split into row and column parts. First the row is selected. Then the column is selected from that row. In older asynchronous DRAM, row and column addresses were controlled using **RAS - Row Address Strobe** and **CAS - Column Address Strobe**. In SDRAM, these actions are represented as clocked commands.

Simple idea:

```text
ACTIVATE = choose/open a row
READ     = choose columns from the open row
WRITE    = update columns in the open row
PRECHARGE = close the row and prepare for another row
```

<a id="topic-3-address-organization"></a>

### SDRAM Address Organization

An SoC processor generates a normal system address. The memory controller maps that address into SDRAM fields.

Typical address breakdown:

```text
System address
      |
      v
Channel + Rank + Bank + Row + Column + Byte offset
```

Definitions:

- **Channel**: an independent memory interface. More channels can increase bandwidth because they can operate independently.
- **Rank**: a group of memory devices/chips selected together on a memory module or package interface.
- **Bank**: an internal DRAM subarray with its own row buffer. Banks allow overlapping operations.
- **Row**: a long line of DRAM cells opened together by an ACTIVATE command.
- **Column**: selected part of the open row used by READ or WRITE commands.
- **Byte offset**: selects the exact byte/word inside the transferred data beat or burst.

Why this matters:

The same sequence of CPU addresses can behave very differently depending on how addresses are mapped to banks, rows and columns. A good mapping can spread traffic across banks and improve parallelism. A bad mapping can send too many accesses to the same bank and create bank conflicts.

Example:

```text
Good case: consecutive cache-line fills go to different banks
        -> bank interleaving works
        -> higher throughput

Bad case: many requests go to different rows in same bank
        -> repeated precharge + activate
        -> higher latency
```

Exam line: **SDRAM address mapping matters because it decides whether requests become row hits, bank-interleaved accesses or bank conflicts.**

### SDRAM Commands

Important SDRAM commands are:

- **ACTIVATE**: opens a row in a bank and loads it into the row buffer.
- **READ**: reads selected columns from an open row.
- **WRITE**: writes selected columns into an open row.
- **PRECHARGE**: closes the currently open row in a bank.
- **REFRESH**: restores charge in DRAM cells.
- **BURST TERMINATE**: stops a burst operation where supported.
- **NOP**: no operation, used when waiting for timing constraints.

These commands are needed because SDRAM is not accessed as one flat memory array. The controller cannot simply say "give me address X immediately." It must first make sure the correct bank and row are ready, then access columns from that row.

Typical read from a closed bank:

```text
1. Choose bank and row.
2. Issue ACTIVATE to open the row.
3. Wait tRCD because the row must be sensed into the row buffer.
4. Issue READ to select the column.
5. Wait CAS latency because data must move through internal/output circuitry.
6. Receive burst data on the data bus.
```

Typical write from a closed bank:

```text
1. Choose bank and row.
2. Issue ACTIVATE.
3. Wait tRCD.
4. Issue WRITE.
5. Send burst write data.
6. Wait write recovery time if precharging after the write.
```

The controller inserts **NOP - No Operation** cycles or chooses another bank when it must wait for timing. This is why banked architecture is useful: while one bank is waiting internally, another bank may be ready for useful work.

### Row Buffer

When a row is activated, the entire row is sensed into the row buffer. The row buffer acts like a temporary fast storage for the active row.

The row buffer is made from sense amplifiers and latch-like circuitry associated with a bank. It is not a software-visible memory like SRAM, but it strongly affects performance. Once a row is open, column accesses to that same row are faster because the data is already in the row buffer.

Think of the row buffer like opening a page in a book:

```text
Open page = ACTIVATE row into row buffer
Read line = READ column from open row
Close page = PRECHARGE before opening another row
```

If the next required data is on the same open page, access is quick. If it is on a different page in the same bank, the old page must be closed and the new page opened.

There are three important cases:

1. **Row hit**: requested data is in the currently open row. This is fastest because no new activate is needed.
2. **Row miss / row conflict**: a different row is open in the same bank. The controller must precharge the old row and activate the new one. This is slow.
3. **Row closed / empty bank**: no row is open. The controller activates the required row and then reads/writes. This is intermediate.

Exam line: **SDRAM latency depends heavily on whether the access is a row hit, row miss or closed-row access.**

### Banked Architecture

Modern SDRAM is divided into multiple banks. Each bank has its own row array and row buffer. A bank can be thought of as a semi-independent internal memory section. Banks allow the memory controller to overlap operations.

Why banks are needed:

- A single huge DRAM array would force too much waiting.
- Activating, precharging and refreshing rows take time.
- Multiple banks allow the controller to work on another bank while one bank is internally busy.
- Bank-level parallelism improves throughput even though each bank still has DRAM timing limits.

For example:

- Bank 0 may be serving a read burst.
- Bank 1 may be precharging.
- Bank 2 may be activating a row.
- Bank 3 may be preparing for the next command.

This improves throughput because the memory controller can hide some timing delays by switching to another bank while one bank is waiting.

Important distinction:

```text
Latency = time for one request to complete.
Bandwidth = amount of data transferred per second.
```

Banked architecture may not remove the physical latency of one row activation, but it can improve total bandwidth by overlapping work across banks.

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

Why we do bank interleaving:

- to reduce idle cycles on the data bus,
- to hide tRCD/tRP waiting time,
- to avoid repeated conflicts in one bank,
- to serve multiple masters more efficiently,
- to improve sustained bandwidth for cache fills, DMA, display, camera and accelerator traffic.

But bank interleaving works only when the address stream and address mapping allow requests to go to different banks. If many requests target different rows in the same bank, performance can still be poor.

### Burst Transfer

SDRAM transfers data in bursts. After an initial column address, multiple consecutive data words are transferred. This is efficient because programs often access sequential memory locations and cache lines are filled using bursts.

Burst transfer helps:

- cache-line fill,
- frame-buffer access,
- streaming media,
- DMA transfers,
- graphics and AI workloads.

DDR SDRAM transfers data on both rising and falling clock edges, increasing data rate without requiring the core memory array to run at the same high speed.

Why burst transfer exists:

Once a row is open and a starting column is selected, nearby columns can be transferred efficiently. This matches **spatial locality**, because programs often access nearby addresses. It also matches cache behavior, because caches usually fill an entire cache line instead of one byte.

Example:

```text
CPU misses in L1 cache
      |
      v
Memory controller requests a full cache line from SDRAM
      |
      v
SDRAM returns several consecutive words as a burst
      |
      v
Cache stores the line for future nearby accesses
```

<a id="topic-3-why-latencies-exist"></a>

### Why SDRAM Latencies Exist

SDRAM latencies are not arbitrary numbers. They come from physical and architectural operations inside the memory.

#### 1. Why ACTIVATE Takes Time

The ACTIVATE command opens a row. Opening a row means enabling thousands of DRAM cells connected to bit lines and sensing their tiny capacitor charges. Sense amplifiers must detect very small voltage differences and restore stable values.

This is why the controller must wait before issuing READ or WRITE after ACTIVATE. That waiting time is represented by **tRCD - Row-to-Column Delay**.

#### 2. Why CAS Latency Exists

After the row is open, the controller issues a READ command for a column. The selected data must pass through column selection logic, internal datapaths, output registers and the external data interface. This pipeline delay is **CL - CAS Latency**.

So CAS latency does not mean "time to open a row." It means the delay from the READ command to the first returned data after the row is already active.

#### 3. Why PRECHARGE Takes Time

Before a different row can be opened in the same bank, the currently open row must be closed. The bit lines must be restored/prepared to a neutral starting condition. This is called precharging.

The time required is **tRP - Row Precharge Time**. Row conflicts are slow because they require:

```text
PRECHARGE old row -> wait tRP -> ACTIVATE new row -> wait tRCD -> READ -> wait CL
```

#### 4. Why tRAS Exists

After a row is activated, it must remain active long enough for sensing/restoration to complete correctly. The controller cannot immediately close the row too early. This minimum row-open time is **tRAS - Row Active Time**.

#### 5. Why tRC Exists

**tRC - Row Cycle Time** is the minimum time from one ACTIVATE to the next ACTIVATE in the same bank. It includes the time needed to activate a row, keep it active long enough and precharge before another row can be activated.

#### 6. Why Refresh Causes Delay

DRAM cells leak charge even if the processor does not access them. Refresh periodically reopens/restores rows so data is not lost. During some refresh operations, parts of memory are unavailable for normal reads/writes.

This delay is represented by **tRFC - Refresh Cycle Time**. Refresh is one reason DRAM access can sometimes be delayed even when the processor request itself is simple.

#### 7. Why Read/Write Turnaround Matters

The SDRAM data bus is shared for reads and writes. Switching direction from read to write or write to read can require extra cycles so that two devices do not drive the bus at the same time and signals remain valid.

This matters in memory-controller scheduling. A controller may group reads together or writes together to reduce turnaround overhead, but it must still avoid starving urgent traffic.

### Important SDRAM Latencies

| Timing Term | Full Form / Meaning | What Causes It | Why It Matters |
|---|---|---|---|
| **CL / CAS latency** | Column Address Strobe latency; READ to first data delay | column selection and internal/output pipeline delay | visible read latency after row is already open |
| **tRCD** | Row-to-Column Delay; ACTIVATE to READ/WRITE delay | row sensing and row-buffer setup after activation | paid when opening a closed row |
| **tRP** | Row Precharge Time | closing current row and preparing bit lines for next row | paid during row conflict before another row can open |
| **tRAS** | Row Active Time | row must remain active long enough for sensing/restoration | prevents closing a row too early |
| **tRC** | Row Cycle Time | full activate-active-precharge cycle in same bank | limits how quickly same bank can open rows repeatedly |
| **tCCD** | Column-to-Column Delay | spacing between column commands | affects back-to-back READ/WRITE command rate |
| **tWR** | Write Recovery Time | written data must be safely restored before precharge | affects when a bank can close after a write |
| **tRFC** | Refresh Cycle Time | refresh operation occupies memory resources | reduces available access time during refresh |
| **tRRD** | Row-to-Row Delay | spacing between ACTIVATE commands to different banks | limits how aggressively banks can be activated |
| **tFAW** | Four Activate Window | power/current limit on too many activates in a short time | prevents excessive activation current |

For exams, if you cannot remember every timing parameter, remember these three first:

```text
tRCD = delay after opening a row before read/write
CL   = delay after READ before first data
tRP  = delay to close a row before opening another row
```

These three are enough to explain row hit, closed-row access and row conflict.

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

The **memory controller** is the block that makes SDRAM usable by the SoC. The CPU, DMA or accelerator usually sends normal read/write transactions. SDRAM does not understand those transactions directly. The memory controller converts them into SDRAM commands and legal timing sequences.

Example:

```text
CPU load from address X
        |
        v
Cache miss reaches memory controller
        |
        v
Controller maps X -> channel/rank/bank/row/column
        |
        v
Controller checks bank state
        |
        v
Issues PRE/ACT/READ commands as needed
        |
        v
SDRAM returns burst data
        |
        v
Cache line is filled and CPU continues
```

The memory controller must:

- map addresses to channel/rank/bank/row/column,
- issue ACTIVATE, READ, WRITE, PRECHARGE and REFRESH commands,
- obey timing constraints,
- exploit row-buffer hits,
- use bank interleaving,
- schedule refresh,
- handle read/write turnaround,
- meet QoS or real-time requirements.

Memory-controller scheduling is important because two legal schedules can have very different performance. A good controller keeps banks busy and reduces row conflicts, but must still be fair to all requesters.

Example of scheduling difference:

```text
Request A: Bank 0, Row 10
Request B: Bank 0, Row 10
Request C: Bank 0, Row 99
```

If the controller serves A then B, B becomes a row hit. If it serves A then C, the controller must close Row 10 and open Row 99, creating a row conflict. Therefore, reordering requests can improve performance.

However, the controller cannot only maximize row hits. If it always serves row hits, another master may wait too long. Therefore, real controllers balance:

- row-buffer locality,
- bank parallelism,
- request age,
- read/write turnaround,
- refresh deadlines,
- priority and QoS,
- fairness and starvation avoidance.

Exam line: **The SDRAM controller improves performance by converting SoC requests into legal command sequences while exploiting row hits and bank interleaving without violating timing or fairness.**

<a id="topic-3-final-answer"></a>

### Final Exam-Ready Answer

**SDRAM - Synchronous Dynamic Random Access Memory** is a clock-controlled DRAM technology used as large main memory in SoC systems. It is called dynamic because each bit is stored as charge on a tiny capacitor and the charge must be periodically refreshed. It is called synchronous because commands and data transfers are coordinated with a clock. SDRAM is used because it provides much higher density and lower cost per bit than SRAM, making it suitable for large program data, operating-system memory, video buffers, graphics data, DMA buffers and AI workloads.

SDRAM is not accessed like simple SRAM. Internally, it is organized into **banks, rows and columns**. A bank is an internal semi-independent memory section. A row is a long line of DRAM cells. A column selects part of an already opened row. The memory controller maps a system address into channel, rank, bank, row and column fields. This mapping matters because it decides whether requests become row hits, bank-interleaved accesses or bank conflicts.

To access SDRAM, the controller issues commands. **ACTIVATE** opens a row in a selected bank and senses the row into the row buffer. **READ** or **WRITE** accesses columns from the open row. **PRECHARGE** closes the open row and prepares the bank for another row. **REFRESH** restores charge in DRAM cells so data is not lost. These commands are necessary because DRAM cells store weak capacitor charge and rows must be sensed, restored and prepared before reliable access.

The **row buffer** is central to SDRAM performance. When a row is activated, the row is copied into sense amplifiers/row buffer circuitry. If the next request accesses the same open row, it is a **row hit** and is fast. If no row is open, the controller must activate the required row first. If a different row is already open in the same bank, it is a **row conflict**, so the controller must precharge the old row, activate the new row and then read/write. Therefore, SDRAM latency changes depending on bank state and row-buffer locality.

Banked architecture improves throughput by dividing SDRAM into multiple banks, each with its own row buffer. While one bank is waiting after activation or precharge, another bank can perform a read/write burst. This is called **bank interleaving**. Bank interleaving does not remove the physical delay of DRAM cells, but it hides some waiting time and keeps the data bus more active. It is important for cache-line fills, DMA transfers, display/camera traffic and accelerator workloads.

Important SDRAM latencies include **CL - CAS Latency**, **tRCD - Row-to-Column Delay**, **tRP - Row Precharge Time**, **tRAS - Row Active Time**, **tRC - Row Cycle Time** and **tRFC - Refresh Cycle Time**. tRCD exists because the row must be sensed after ACTIVATE. CAS latency exists because data takes time to move from the selected column through internal/output circuitry. tRP exists because bit lines must be prepared before opening another row. tRFC exists because refresh occupies memory resources. A row hit mainly pays CAS latency, a closed-row access pays tRCD plus CAS latency, and a row conflict pays tRP plus tRCD plus CAS latency.

Thus, SDRAM performance depends not only on clock frequency. It depends on row hits, row conflicts, bank interleaving, burst length, refresh overhead, read/write turnaround and memory-controller scheduling. A good SoC memory controller improves SDRAM performance by mapping addresses carefully, exploiting row-buffer locality, spreading traffic across banks, obeying timing constraints and balancing bandwidth, latency, fairness and QoS.

### Short 10-Mark Exam Answer

**SDRAM - Synchronous Dynamic Random Access Memory** is clock-controlled DRAM used as large main memory in SoC systems. It stores bits as charge on capacitors, so it needs refresh. It is organized into banks, rows and columns. To access data, the memory controller activates a row in a bank, then issues READ or WRITE commands to access columns in that open row.

Each bank has a row buffer. If the next request goes to the already open row, it is a row hit and is fast. If no row is open, the controller must activate a row first. If a different row is open in the same bank, the controller must precharge the old row and activate the new one, causing a row conflict and higher latency.

Banked architecture allows bank interleaving. While one bank waits after activate or precharge, another bank can transfer data. This improves bandwidth and hides some DRAM delay. SDRAM also transfers data in bursts, which is useful for cache-line fills and sequential data.

Important latencies are **CL - CAS Latency**, **tRCD - Row-to-Column Delay**, **tRP - Row Precharge Time**, **tRAS - Row Active Time** and **tRFC - Refresh Cycle Time**. SDRAM performance depends on row hits, bank conflicts, burst length, refresh and memory-controller scheduling.

<a id="topic-3-technical-words"></a>

### Technical Words To Use For Marks

- **SDRAM** (write this because the question is specifically about synchronous DRAM.)
- **DDR SDRAM** (write this because modern SoC DRAM usually transfers data on both clock edges.)
- **Banked architecture** (write this because multiple banks enable interleaving and higher throughput.)
- **Channel** (write this because memory bandwidth can increase using independent memory interfaces.)
- **Rank** (write this because SDRAM addresses may include device/module grouping.)
- **Bank** (write this because each bank has its own row buffer and timing state.)
- **Row** (write this because ACTIVATE opens a row.)
- **Column** (write this because READ/WRITE selects columns from an open row.)
- **Row buffer** (write this because row hits and row conflicts depend on it.)
- **Sense amplifier** (write this because tiny DRAM capacitor charge must be detected and restored.)
- **Row hit** (write this because it explains the fastest SDRAM access case.)
- **Row miss / row conflict** (write this because it explains extra precharge and activate delay.)
- **Closed-row access** (write this because it is the middle case between row hit and row conflict.)
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
- **tRRD** (write this because ACTIVATE commands to different banks still need spacing.)
- **tFAW** (write this because too many activates in a short window can exceed current limits.)
- **Burst length** (write this because SDRAM transfers multiple words per command.)
- **Bank interleaving** (write this because it hides latency and improves bandwidth.)
- **Bank-level parallelism** (write this because multiple banks allow overlapping operations.)
- **Address mapping** (write this because system addresses are mapped to channel/rank/bank/row/column.)
- **Read/write turnaround** (write this because switching bus direction can add delay.)
- **Row-buffer locality** (write this because repeated access to the same open row improves performance.)
- **Memory controller** (write this because SDRAM command scheduling is done by the controller.)

<a id="topic-3-diagrams"></a>

### Images / Diagrams To Remember

1. **SDRAM banked architecture**: Draw command logic connected to multiple banks, each with row array and row buffer.
2. **Latency cases**: Draw row hit, closed-row and row-conflict timelines.
3. **DRAM cell diagram**: Draw access transistor plus storage capacitor. This explains why DRAM is dense and why refresh is needed.
4. **Address breakdown diagram**: Draw `System address -> Channel / Rank / Bank / Row / Column / Offset`. This helps explain why address mapping affects bank conflicts.
5. **Command sequence diagram**: Draw `ACT -> tRCD -> READ -> CL -> Data` and `PRE -> tRP -> ACT -> tRCD -> READ -> CL -> Data`.
6. **Book figure/source to cite**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.167](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=167>) for DRAM row/column organization.
7. **Book figure/source to cite**: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.171](<Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=171>) and p.172 for DDR SDRAM banked architecture.
8. **PPT/lecture source to cite**: [module 1 part 1 introduction to system approach.pdf, p.20](<System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22 for why SoCs use large off-chip memory and cache hierarchy.

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

The examiner is asking you to explain the role, internal blocks and design importance of the memory controller. A weak answer only says: "A memory controller controls memory." A full-mark answer must explain what exactly it controls: request arbitration, address decoding, **DRAM - Dynamic Random Access Memory** command generation, row/bank management, refresh, timing constraints, buffering, **QoS - Quality of Service** and error protection.

For full marks, answer in this order:

1. Define memory controller.
2. Explain why an SoC needs a memory controller.
3. Draw a block diagram showing **CPU - Central Processing Unit**, **GPU - Graphics Processing Unit**, **DMA - Direct Memory Access**, interconnect, memory controller and **DRAM - Dynamic Random Access Memory**.
4. Explain the main blocks inside the memory controller.
5. Explain how it converts read/write requests into memory commands.
6. Explain timing, refresh, arbitration, scheduling and buffering.
7. Discuss design tradeoffs: latency, bandwidth, power, area, predictability and **QoS - Quality of Service**.
8. Link the answer back to memory hierarchy and **SDRAM - Synchronous Dynamic Random Access Memory** banked architecture.

<a id="topic-5-explanation"></a>

### Core Idea

A **memory controller** is the hardware block that sits between **SoC masters** and the memory device. A **SoC master** or **memory master** is any block that can initiate a memory transaction. Examples include **CPU - Central Processing Unit** cores, **GPU - Graphics Processing Unit**, **DSP - Digital Signal Processor**, **DMA - Direct Memory Access** engine, display controller, camera interface, network block and hardware accelerators.

These masters usually do not directly drive memory pins. They send abstract read/write transactions through an interconnect such as **AXI - Advanced eXtensible Interface**, **AHB - Advanced High-performance Bus**, **NoC - Network on Chip** or another bus fabric. The memory controller accepts those requests and converts them into the exact memory operations required by **SRAM - Static Random Access Memory**, **SDRAM - Synchronous Dynamic Random Access Memory**, **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory**, **LPDDR - Low-Power Double Data Rate** or another memory technology.

The simplest way to remember it is:

```text
SoC masters -> Interconnect / NoC -> Memory controller -> Memory PHY -> Memory chips

NoC = Network on Chip
PHY = Physical Layer
```

The controller is important because memory devices have strict timing and command requirements. For example, **SDRAM - Synchronous Dynamic Random Access Memory** cannot be read like a simple register. Before data can be read, the controller may need to open a row using the **ACTIVATE** command, wait for **tRCD - Row-to-Column Delay**, issue a **READ** command, wait for **CL - CAS Latency / Column Address Strobe Latency**, transfer burst data, and later use **PRECHARGE** to close the bank. If **REFRESH** is due, the controller must pause or schedule around normal traffic and refresh the **DRAM - Dynamic Random Access Memory** cells. If many masters request memory together, the controller must use **arbitration** to choose service order and prevent **starvation**, where a requester waits too long because other requests keep being served first.

### Why We Talk About DRAM Here, Not Only SRAM

In the memory-controller topic, we talk a lot about **DRAM - Dynamic Random Access Memory** because DRAM is usually the large external **main memory** in an SoC. It is also the memory technology that makes the controller architecturally complex.

**SRAM - Static Random Access Memory** is much simpler from a controller point of view:

- SRAM does not need refresh.
- SRAM does not use ACTIVATE, PRECHARGE or row-buffer management.
- SRAM usually has simpler read/write timing.
- SRAM is often on-chip and close to the CPU, cache, scratchpad or accelerator.
- SRAM is fast but too area-expensive for very large main memory.

So an SRAM controller or SRAM interface may still exist, but it is usually much simpler: provide an address, assert read/write control, obey simple timing, and transfer data.

**DRAM - Dynamic Random Access Memory**, **SDRAM - Synchronous Dynamic Random Access Memory**, **DDR - Double Data Rate** and **LPDDR - Low-Power Double Data Rate** are different:

- DRAM stores data as charge on capacitors, so refresh is mandatory.
- SDRAM is organized into banks, rows and columns.
- A row must be activated before column access.
- A bank may need precharge before opening another row.
- Timing parameters such as **tRCD - Row-to-Column Delay**, **tRP - Row Precharge Time**, **tRAS - Row Active Time**, **tRC - Row Cycle Time**, **tRFC - Refresh Cycle Time** and **CL - CAS Latency** must be obeyed.
- Multiple masters may compete for the same DRAM bandwidth.
- The controller must schedule commands to reduce row conflicts and exploit bank interleaving.

Therefore, when the exam asks about **memory controller architecture**, DRAM is discussed more than SRAM because DRAM needs a real command scheduler, timing controller, refresh controller, row/bank manager, **PHY - Physical Layer** interface and **QoS - Quality of Service** logic. SRAM is still important in the memory hierarchy, but it does not create the same level of controller complexity.

Exam line: **SRAM needs simple low-latency access control; DRAM needs a full memory controller because it has refresh, banks, rows, commands, strict timing and shared-bandwidth scheduling.**

Therefore, the memory controller is both a **correctness block** and a **performance block**. It makes memory access legal according to device timing, and it also decides how efficiently the memory bandwidth is used.

### Basic Block Diagram

Use this diagram in exams when asked to draw memory controller architecture:

```text
 CPU cores     GPU / DSP     DMA       Display / Camera
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

Full forms for diagram labels:

- **GPU - Graphics Processing Unit**.
- **DSP - Digital Signal Processor**.
- **DMA - Direct Memory Access**.
- **AXI - Advanced eXtensible Interface**.
- **AHB - Advanced High-performance Bus**.
- **NoC - Network on Chip**.
- **ECC - Error Correction Code**.
- **QoS - Quality of Service**.
- **DDR - Double Data Rate**.
- **LPDDR - Low-Power Double Data Rate**.
- **PHY - Physical Layer**.
- **DRAM - Dynamic Random Access Memory**.

This diagram is useful because it shows that the memory controller is not a single small circuit. It is a collection of sub-blocks that manage requests, addresses, timing, data movement, reliability and quality of service.

### Why SoC Needs A Memory Controller

An SoC needs a memory controller for the following reasons:

1. **Different masters share memory**: **CPU - Central Processing Unit**, **GPU - Graphics Processing Unit**, **DMA - Direct Memory Access**, display controller and accelerators may all access the same **DRAM - Dynamic Random Access Memory**. The controller decides whose request is served first.
2. **DRAM has complex timing**: **SDRAM - Synchronous Dynamic Random Access Memory** and **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory** require ACTIVATE, READ, WRITE, PRECHARGE and REFRESH commands with exact timing gaps.
3. **Address must be mapped**: A processor address must be translated into channel, rank, bank, row and column fields.
4. **Data width mismatch exists**: A CPU may request a cache line, a DMA may request a burst, and the memory device may have a different bus width. The controller packs/unpacks data.
5. **Bandwidth must be maximized**: The controller schedules row hits, bank interleaving and bursts to improve throughput.
6. **Latency must be controlled**: Critical requests such as CPU cache misses or display fetches cannot wait indefinitely.
7. **Refresh is mandatory**: DRAM cells leak charge, so the controller must periodically refresh rows.
8. **Reliability is needed**: Many systems use **ECC - Error Correction Code**, parity, address protection, access permissions or error reporting.
9. **Power must be managed**: **DDR - Double Data Rate** / **LPDDR - Low-Power Double Data Rate** memories support low-power modes, self-refresh and clock gating.
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

A memory controller is a hardware block in an SoC that manages all communication between SoC masters and the memory system. **SoC masters** are request-generating blocks such as **CPU - Central Processing Unit** cores, **GPU - Graphics Processing Unit**, **DMA - Direct Memory Access** engine, display controller, camera interface, **DSP - Digital Signal Processor** and accelerators. These masters generate read and write requests through the system interconnect. The memory controller accepts these high-level requests and converts them into correct low-level memory operations for **SRAM - Static Random Access Memory**, **SDRAM - Synchronous Dynamic Random Access Memory**, **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory**, **LPDDR - Low-Power Double Data Rate** or other memory devices.

The memory controller is required because modern memories, especially SDRAM and DDR memories, cannot be accessed as simple registers. DRAM-based memories have banked organization, row buffers, burst transfers, refresh requirements and strict timing constraints. The controller maps a system address into channel, rank, bank, row and column fields. It then generates commands such as ACTIVATE, READ, WRITE, PRECHARGE and REFRESH while obeying timing parameters such as **tRCD - Row-to-Column Delay**, **CL - CAS Latency / Column Address Strobe Latency**, **tRP - Row Precharge Time**, **tRAS - Row Active Time**, **tRC - Row Cycle Time** and **tRFC - Refresh Cycle Time**.

DRAM is discussed more than SRAM in memory-controller architecture because DRAM creates most of the controller complexity. **SRAM - Static Random Access Memory** is fast, on-chip in many cases, and does not need refresh, activate/precharge commands or row-buffer scheduling. **DRAM - Dynamic Random Access Memory** gives large main-memory capacity, but it needs refresh, bank/row management, command scheduling, timing control and a PHY. Therefore, SRAM needs simpler access control, while DRAM needs a full memory-controller architecture.

Internally, a memory controller contains request queues, address decoder, arbiter, scheduler, command generator, timing controller, refresh controller, read/write buffers, data path logic, **ECC - Error Correction Code** logic and **QoS - Quality of Service** control. The request queues hold pending transactions. The arbiter decides which master should be considered. The scheduler selects an efficient command order by considering row-buffer hits, bank conflicts, read/write turnaround, refresh and priority. The timing controller ensures that all memory commands are issued only when legal. The refresh controller periodically refreshes DRAM cells to preserve data. Read and write buffers allow burst transfers and multiple outstanding memory requests.

The memory controller strongly affects SoC performance. A good controller increases bandwidth by using row-buffer locality, bank interleaving, burst transfers and multi-channel memory. It reduces latency by prioritizing critical requests and avoiding unnecessary precharge/activate operations. It improves fairness by preventing starvation among CPU, GPU, DMA and real-time masters. It also improves reliability through ECC and error reporting. In multimedia and real-time SoCs, the controller may provide QoS guarantees so that display, camera or audio traffic receives memory service before deadlines.

The design of a memory controller involves tradeoffs. Optimizing only for row-buffer hits can improve bandwidth but may hurt fairness. Giving strict priority to real-time traffic can meet deadlines but may starve best-effort traffic. Large buffers and complex scheduling improve performance but increase area, power and verification complexity. Open-page policy improves locality, while close-page policy may reduce latency for random traffic. Therefore, the memory controller is a central part of SoC memory architecture because it determines how efficiently and predictably the processor-memory system works.

### Short 10-Mark Exam Answer

A memory controller is the SoC hardware block that connects processors and other memory masters to the memory device. It receives read/write requests from **CPU - Central Processing Unit**, **GPU - Graphics Processing Unit**, **DMA - Direct Memory Access**, display and accelerators through the interconnect and converts them into memory commands.

For **SDRAM - Synchronous Dynamic Random Access Memory** / **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory**, the controller performs address mapping into channel, rank, bank, row and column. It issues ACTIVATE, READ, WRITE, PRECHARGE and REFRESH commands while satisfying timing parameters such as **tRCD - Row-to-Column Delay**, **CL - CAS Latency**, **tRP - Row Precharge Time** and **tRFC - Refresh Cycle Time**. It contains request queues, arbiter, scheduler, timing controller, refresh controller, read/write buffers, data path, **ECC - Error Correction Code** and **QoS - Quality of Service** logic.

The memory controller improves performance by using bank interleaving, row-buffer hits, burst transfers and multi-channel access. It also provides fairness and QoS among different SoC masters. DRAM is the main example because it needs these scheduling and timing functions; SRAM access is much simpler and usually does not dominate controller architecture. Hence, memory controller architecture is essential for latency, bandwidth, reliability, power and real-time behavior in SoC memory design.

<a id="topic-5-technical-words"></a>

### Technical Words To Use For Marks

- **Memory controller** (write this because it is the exact architecture block asked in the question.)
- **SoC master / memory master** (write this because CPU, GPU, DMA and display are the request sources.)
- **CPU - Central Processing Unit** (write this because CPU cache misses are common memory requests.)
- **GPU - Graphics Processing Unit** (write this because graphics traffic often needs high memory bandwidth.)
- **DMA - Direct Memory Access** (write this because DMA engines generate burst transfers without constant CPU control.)
- **DSP - Digital Signal Processor** (write this because DSP blocks may generate streaming memory traffic.)
- **Interconnect / NoC - Network on Chip** (write this because masters reach memory through a bus or network fabric.)
- **AXI - Advanced eXtensible Interface** (write this because many SoCs use AXI-style memory transactions.)
- **AHB - Advanced High-performance Bus** (write this because embedded SoCs may use AHB-style interconnect.)
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
- **tRCD - Row-to-Column Delay** (write this because it is the delay between row activation and column access.)
- **CAS latency / CL - Column Address Strobe Latency** (write this because it is the delay between READ and data output.)
- **tRP - Row Precharge Time** (write this because it is the precharge delay.)
- **tRFC - Refresh Cycle Time** (write this because refresh consumes memory-service time.)
- **Read/write buffer** (write this because buffering supports outstanding requests and burst traffic.)
- **Burst transfer** (write this because DDR memories transfer multiple data beats per command.)
- **ECC - Error Correction Code** (write this because many controllers include error detection and correction.)
- **QoS - Quality of Service** (write this because real-time and high-priority traffic require service guarantees.)
- **Open-page policy** (write this because it keeps rows open for locality.)
- **Close-page policy** (write this because it prepares banks for random accesses.)
- **Bank interleaving** (write this because it hides bank timing delays and improves bandwidth.)
- **Refresh overhead** (write this because refresh reduces available bandwidth.)
- **Memory PHY - Physical Layer** (write this because DDR/LPDDR needs physical-layer signaling and timing.)

<a id="topic-5-diagrams"></a>

### Images / Diagrams To Remember

1. **Memory controller block diagram**: Draw SoC masters, interconnect, memory controller blocks and DDR/LPDDR memory. This is the most important diagram for this topic.
2. **DRAM command flow diagram**: Draw address decode -> ACTIVATE -> `tRCD - Row-to-Column Delay` wait -> READ/WRITE -> `CL - CAS Latency` -> data burst -> PRECHARGE/keep row open.
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

### Important Blocks In This Model: DMA And Accelerators

Before studying processor-memory interaction models, understand that the **CPU - Central Processing Unit** is not the only block that uses memory. Modern SoCs have other blocks that can also read and write memory. These blocks become **memory masters**, meaning they can initiate memory transactions.

#### DMA - Direct Memory Access

**DMA** means **Direct Memory Access**. A **DMA controller** is a hardware block that transfers data between memory and peripherals, or between two memory regions, without the CPU manually moving every word of data.

Without DMA, the CPU would move data like this:

```text
1. CPU reads one word from source.
2. CPU writes that word to destination.
3. CPU repeats this thousands or millions of times.
```

This wastes CPU cycles because the CPU becomes a data-copy machine instead of doing useful computation.

With DMA, the CPU only configures the DMA controller:

```text
Source address      = where data starts
Destination address = where data should go
Transfer size       = how many bytes/words
Direction/type      = memory-to-memory, peripheral-to-memory, memory-to-peripheral
Start bit           = begin transfer
```

Then the DMA controller performs the transfer by itself:

```text
CPU configures DMA registers
        |
        v
DMA reads source data from memory/peripheral
        |
        v
DMA writes data to destination memory/peripheral
        |
        v
DMA raises interrupt when done
```

Where DMA is used:

- moving camera frames into memory,
- moving audio samples between memory and audio interface,
- copying blocks of memory,
- feeding data to a hardware accelerator,
- moving network packets,
- storage transfers,
- display/video buffer movement.

Why DMA matters in processor-memory interaction:

- DMA creates memory requests even when the CPU is not directly loading/storing data.
- DMA can generate long burst transfers and consume high memory bandwidth.
- DMA can compete with CPU cache misses, GPU traffic, display traffic and accelerator traffic.
- DMA reduces CPU workload but increases memory-system traffic.
- DMA may cause cache-coherency issues if CPU cache contains old copies of memory that DMA updates.

Example:

```text
Camera -> DMA -> DRAM frame buffer
CPU/GPU later reads the frame buffer
```

Here, the camera data does not pass word-by-word through the CPU. The DMA controller writes the frame into **DRAM - Dynamic Random Access Memory** directly. But the memory controller still sees many write requests, so DMA affects bandwidth and contention.

Exam line: **DMA - Direct Memory Access is a hardware controller that moves data without continuous CPU involvement; it improves CPU efficiency but becomes another memory master that can contend for memory bandwidth.**

#### Hardware Accelerator

A **hardware accelerator** is a specialized hardware block designed to perform a specific task faster or more energy-efficiently than a general-purpose CPU.

The CPU is flexible. It can run many kinds of software. But because it is general-purpose, it may not be the fastest or most power-efficient block for repeated heavy operations. An accelerator is built for a narrower job.

Examples of accelerators:

- **GPU - Graphics Processing Unit** for graphics and parallel computation.
- **DSP - Digital Signal Processor** for signal-processing operations.
- AI / neural-network accelerator for matrix multiplication and inference.
- Video encoder/decoder for H.264/H.265/AV1 processing.
- Image signal processor for camera pipelines.
- Crypto accelerator for encryption/decryption.
- Network packet accelerator.
- Compression/decompression accelerator.

What an accelerator does:

1. CPU configures accelerator registers.
2. Accelerator reads input data from memory.
3. Accelerator performs specialized computation.
4. Accelerator writes output data back to memory.
5. Accelerator interrupts CPU or sets status when complete.

Simple flow:

```text
CPU sets accelerator registers
        |
        v
Accelerator reads input buffer from memory
        |
        v
Accelerator computes result
        |
        v
Accelerator writes output buffer to memory
        |
        v
CPU reads result/status
```

Why accelerators matter in processor-memory interaction:

- Accelerators often need high memory bandwidth.
- They may issue many reads/writes independently of the CPU.
- They can reduce CPU computation time but increase memory pressure.
- They may need local SRAM buffers to reduce repeated DRAM access.
- They may use DMA internally to fetch and store data.
- They can contend with CPU, GPU, display and other masters at the memory controller.

Example:

```text
AI accelerator reads weights + input activations from DRAM
        |
        v
performs multiply-accumulate operations
        |
        v
writes output activations back to DRAM
```

If the memory system cannot feed the accelerator fast enough, the accelerator becomes underutilized. This is called **memory bandwidth bottleneck**. The compute unit may be capable of many operations per second, but it stalls waiting for data.

Exam line: **A hardware accelerator is a specialized SoC block that performs a specific computation efficiently, but it still depends on the memory system for input and output data, so it becomes an important memory master in processor-memory interaction models.**

#### Why DMA And Accelerators Are Included In This Topic

The topic is called processor-memory interaction, but in modern SoCs the memory system is shared by many requesters. The processor is only one requester. DMA controllers and accelerators can generate memory traffic at the same time.

This means the memory model must consider:

- CPU instruction fetches,
- CPU data loads/stores,
- cache misses,
- DMA transfers,
- accelerator input reads,
- accelerator output writes,
- contention at memory modules, banks, channels and controller queues.

So when this topic says "processor requests", it often represents a more general idea:

```text
memory requests from CPU + DMA + accelerators + other SoC masters
```

That is why the model is useful for SoC design. It estimates whether the memory system can serve all requesters without excessive stalls, contention or bandwidth loss.

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

Thus, models of processor-memory interaction help in understanding the relationship between memory latency, contention, bandwidth, cache misses, memory modules and controller scheduling. They are essential in SoC design because modern SoCs contain many processors, **DMA - Direct Memory Access** controllers and hardware accelerators sharing the same memory system.

### Short 10-Mark Exam Answer

Simple processor-memory interaction models are used to analyze how memory requests from processors are served by memory modules. In practical SoCs, the requests may also come from **DMA - Direct Memory Access** controllers and hardware accelerators. In a single processor-single memory model, the processor sends one request and waits for the memory response. This blocking behavior shows that high memory latency causes processor stalls.

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
- **DMA - Direct Memory Access** (write this because DMA controllers create memory requests without continuous CPU involvement.)
- **DMA controller** (write this because it is the hardware block that performs memory/peripheral transfers after CPU configuration.)
- **Hardware accelerator** (write this because accelerators are specialized blocks that also read/write memory.)
- **Memory master** (write this because CPU, DMA and accelerators can all initiate memory transactions.)
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
