# CLO 2 - SoC Components: Processors, Memory Systems And On-Chip Interconnect

## Clickable Index

- [CLO 2 Master Definitions](#clo2-master-definitions)
- [CLO 2 Review Addendum: Factual Integration And Exam Traps](#clo2-review-addendum)
- [Topic 1: SoC Components - Core Logic, Processors, Choice Of Processors, Processor Architecture And Microarchitecture](#topic-1)
  - [Question](#topic-1-question)
  - [CLO Mapping](#topic-1-clo-mapping)
  - [What The Question Is Asking](#topic-1-what-asking)
  - [Main Explanation](#topic-1-main-explanation)
  - [Core Logic In SoC](#topic-1-core-logic)
  - [Processor In SoC](#topic-1-processor-in-soc)
  - [Choice Of Processors](#topic-1-choice-processors)
  - [Types Of Processors In SoC](#topic-1-types-processors)
  - [Processor Architecture](#topic-1-processor-architecture)
  - [Processor Microarchitecture](#topic-1-processor-microarchitecture)
  - [Architecture Vs Microarchitecture](#topic-1-architecture-vs-microarchitecture)
  - [Performance Metrics And Tradeoffs](#topic-1-performance)
  - [Final Exam-Ready Answer](#topic-1-final-answer)
  - [Short 10-Mark Answer](#topic-1-short-answer)
  - [Technical Words](#topic-1-technical-words)
  - [Images / Diagrams](#topic-1-diagrams)
- [Topic 2: Memory Design Overview And SoC On-Die Memory Systems](#topic-2)
  - [Question](#topic-2-question)
  - [CLO Mapping](#topic-2-clo-mapping)
  - [What The Question Is Asking](#topic-2-what-asking)
  - [Main Explanation](#topic-2-main-explanation)
  - [Why Memory Design Is Important In SoC](#topic-2-why-important)
  - [Memory Hierarchy Overview](#topic-2-memory-hierarchy)
  - [Cache Hierarchy In Depth: Level 1, Level 2 And Level 3](#topic-2-cache-hierarchy-deep)
  - [Cache Internals: Lines, Tags, Hits And Misses](#topic-2-cache-internals)
  - [Scratchpad Memory In Depth](#topic-2-scratchpad-deep)
  - [TCM - Tightly Coupled Memory In Depth](#topic-2-tcm-deep)
  - [Cache Vs Scratchpad Vs TCM](#topic-2-cache-scratchpad-tcm)
  - [SoC On-Die Memory Systems](#topic-2-on-die)
  - [On-Die Vs Off-Die Memory](#topic-2-on-die-vs-off-die)
  - [On-Die Memory Design Tradeoffs](#topic-2-tradeoffs)
  - [Memory Map And Access](#topic-2-memory-map)
  - [Final Exam-Ready Answer](#topic-2-final-answer)
  - [Short 10-Mark Answer](#topic-2-short-answer)
  - [Technical Words](#topic-2-technical-words)
  - [Images / Diagrams](#topic-2-diagrams)
- [Topic 3: Board-Based Off-Die Memory Systems, Simple DRAM And The Memory Array](#topic-3)
  - [Question](#topic-3-question)
  - [CLO Mapping](#topic-3-clo-mapping)
  - [What The Question Is Asking](#topic-3-what-asking)
  - [Main Explanation](#topic-3-main-explanation)
  - [Board-Based Off-Die Memory Systems](#topic-3-board-based)
  - [Why Off-Die Memory Is Used](#topic-3-why-off-die)
  - [Simple DRAM Cell](#topic-3-dram-cell)
  - [DRAM Memory Array](#topic-3-memory-array)
  - [DRAM Access Sequence](#topic-3-access-sequence)
  - [Board-Level Design Issues](#topic-3-board-level)
  - [Final Exam-Ready Answer](#topic-3-final-answer)
  - [Short 10-Mark Answer](#topic-3-short-answer)
  - [Technical Words](#topic-3-technical-words)
  - [Images / Diagrams](#topic-3-diagrams)
- [Topic 4: Models Of Simple Processor-Memory Interaction](#topic-4)
  - [Question](#topic-4-question)
  - [CLO Mapping](#topic-4-clo-mapping)
  - [What The Question Is Asking](#topic-4-what-asking)
  - [Main Explanation](#topic-4-main-explanation)
  - [Why Processor-Memory Interaction Is Modeled](#topic-4-why-modeled)
  - [Basic Terms](#topic-4-basic-terms)
  - [Model 1: One Processor And One Memory](#topic-4-model-1)
  - [Model 2: Many Processors And One Memory](#topic-4-model-2)
  - [Model 3: Many Processors And Many Memory Modules](#topic-4-model-3)
  - [Pipelined Processor Equivalence](#topic-4-pipelined-equivalence)
  - [Relation To Cache, Interleaving And DRAM](#topic-4-relation-cache-dram)
  - [Final Exam-Ready Answer](#topic-4-final-answer)
  - [Short 10-Mark Answer](#topic-4-short-answer)
  - [Technical Words](#topic-4-technical-words)
  - [Images / Diagrams](#topic-4-diagrams)
- [Topic 5: On-Chip Interconnect, Bus Vs NoC And NoC Architectures](#topic-5)
  - [Question](#topic-5-question)
  - [CLO Mapping](#topic-5-clo-mapping)
  - [What The Question Is Asking](#topic-5-what-asking)
  - [Main Explanation](#topic-5-main-explanation)
  - [Why On-Chip Interconnect Is Needed](#topic-5-why-needed)
  - [Bus-Based Interconnect](#topic-5-bus)
  - [Crossbar And Hierarchical Interconnect](#topic-5-crossbar)
  - [NoC - Network On Chip](#topic-5-noc)
  - [Bus Vs NoC](#topic-5-bus-vs-noc)
  - [NoC Architecture Components](#topic-5-noc-components)
  - [NoC Topologies](#topic-5-topologies)
  - [Routing, Switching And Flow Control](#topic-5-routing)
  - [Design Tradeoffs And Challenges](#topic-5-tradeoffs)
  - [Final Exam-Ready Answer](#topic-5-final-answer)
  - [Short 10-Mark Answer](#topic-5-short-answer)
  - [Technical Words](#topic-5-technical-words)
  - [Images / Diagrams](#topic-5-diagrams)

<a id="clo2-master-definitions"></a>

## CLO 2 Master Definitions

Use this section before revising CLO 2. For this CLO, always know whether a term is a **SoC component**, **processor type**, **architecture concept**, **microarchitecture feature**, **performance metric**, or **interconnect/memory support concept**.

| Term | Full Form / Meaning | Definition / Why It Matters |
|---|---|---|
| CLO | Course Learning Outcome | The syllabus outcome used to group exam topics and expected answers. |
| SoC | System on Chip | Complete system integrated on one chip, usually containing processors, memories, interconnect, peripherals, accelerators, debug/test logic and embedded software. |
| Core logic | Main digital compute/control logic | Digital part of the SoC that performs computation and control, especially processor cores, controllers, datapaths and accelerators. |
| Processor | Programmable execution unit | Hardware block that fetches, decodes and executes instructions from software. |
| CPU | Central Processing Unit | Main general-purpose processor that runs system software, control code or application code. |
| Processor core | CPU implementation block | The actual reusable processor IP block integrated into an SoC. |
| GPP | General-Purpose Processor | Processor designed to run many kinds of software, usually chosen when flexibility and software ecosystem matter. |
| MCU | Microcontroller Unit | Small embedded processor system optimized for control, low power, deterministic behavior and peripheral interaction. |
| DSP | Digital Signal Processor | Processor optimized for signal-processing workloads such as filtering, audio, video and communication algorithms. |
| ASIP | Application-Specific Instruction Processor | Processor whose instruction set or datapath is customized for a specific application/domain. |
| FPGA | Field-Programmable Gate Array | Reconfigurable hardware fabric; can implement soft processors and custom accelerators without fabricating a new chip. |
| Soft processor | Configurable processor implemented in programmable logic or RTL | Processor supplied as synthesizable logic/bitstream, useful for FPGA/adaptive SoC integration and customization. |
| Hard processor | Processor implemented as fixed silicon macro | Physical processor implementation with known timing, power and area; less flexible but more predictable. |
| Processor IP | Processor Intellectual Property | Reusable licensed processor design block such as Arm Cortex, RISC-V core, MicroBlaze or Nios-style soft core. |
| ISA | Instruction Set Architecture | Programmer-visible contract of a processor: instructions, registers, data types, memory model, exceptions and privilege behavior. |
| Microarchitecture | Internal implementation of ISA | Pipeline, execution units, caches, branch predictor, issue width and scheduling used to implement an ISA. |
| Register file | Set of internal processor registers | Fast storage used for operands, addresses and results during instruction execution. |
| ALU | Arithmetic Logic Unit | Execution unit that performs integer arithmetic and logical operations. |
| FPU | Floating-Point Unit | Execution unit for floating-point arithmetic. |
| PSW | Program Status Word | Processor status/control register holding flags, condition codes, interrupt enable bits or processor mode. |
| CC | Condition Code | Status flag set by operations, such as zero, negative, carry or overflow, used by conditional branches. |
| PC | Program Counter | Register holding the address of the next instruction to fetch. |
| IR | Instruction Register | Register holding the currently fetched instruction. |
| RISC | Reduced Instruction Set Computer | ISA style usually using simpler, regular, often load/store instructions that are easier to pipeline/decode. |
| CISC | Complex Instruction Set Computer | ISA style with more complex/variable instructions, often allowing memory operands in arithmetic operations. |
| L/S | Load/Store architecture | Instruction style where memory is accessed only by load/store instructions, while ALU operations use registers. |
| R/M | Register/Memory architecture | Instruction style where arithmetic instructions may use an operand directly from memory. |
| Branch | Control-flow instruction | Instruction that changes the program counter, such as jump, conditional branch, call or return. |
| Interrupt | External or asynchronous event | Event usually from hardware/peripheral requiring processor service through an interrupt handler. |
| Exception | Internal or synchronous event | Event caused by instruction execution, such as divide-by-zero, invalid instruction or page fault. |
| ISR | Interrupt Service Routine | Software routine executed when an interrupt occurs. |
| Pipeline | Overlapped instruction execution | Microarchitecture technique where different stages of different instructions execute simultaneously. |
| IF | Instruction Fetch | Pipeline stage that fetches instruction from instruction memory/cache. |
| ID | Instruction Decode | Pipeline stage that decodes opcode and identifies required operands/control signals. |
| AG | Address Generation | Pipeline stage that computes memory address for load/store operations. |
| DF | Data Fetch | Pipeline stage that fetches operands/data from register file or memory/cache. |
| EX | Execute | Pipeline stage where ALU/FPU/functional units perform the operation. |
| WB | Write Back | Pipeline stage that writes result back to register file or architectural state. |
| Hazard | Pipeline conflict | Condition that prevents smooth pipeline progress, such as data dependency, resource conflict or branch uncertainty. |
| Data hazard | Operand dependency conflict | Later instruction needs a value produced by an earlier unfinished instruction. |
| Structural hazard | Resource conflict | Multiple instructions need the same hardware resource at the same time. |
| Control hazard | Branch/control-flow conflict | Pipeline does not know the correct next instruction because branch outcome/target is not known yet. |
| Stall | Pipeline pause | Delay inserted when pipeline cannot safely continue. |
| Forwarding / bypassing | Sending result directly to dependent stage | Reduces stalls by passing a produced value before it is written back to the register file. |
| Branch prediction | Guessing branch direction/target | Reduces branch stalls by predicting control flow before branch is fully resolved. |
| In-order execution | Program-order execution | Instructions execute/complete in original program order; simpler and often more deterministic. |
| Out-of-order execution | Dynamic reordered execution | Processor executes ready instructions before older stalled ones to improve performance. |
| Superscalar | Multiple-issue processor | Processor that can issue more than one instruction per cycle using multiple execution resources. |
| VLIW | Very Long Instruction Word | Architecture where compiler packs independent operations into a wide instruction word for parallel execution. |
| SIMD | Single Instruction Multiple Data | One instruction applies the same operation to multiple data elements, useful for vectors, multimedia and DSP. |
| MIMD | Multiple Instruction Multiple Data | Multiple processors execute independent instruction streams on different data streams. |
| Cache | Hardware-managed fast copy memory | Small fast memory, usually Static Random Access Memory based, that stores copies of recently or nearby used instructions/data from slower memory to reduce average access time. |
| L1 cache | Level 1 cache | First cache level closest to a processor core; smallest and fastest cache, often split into Instruction cache and Data cache. |
| L2 cache | Level 2 cache | Second cache level; usually larger than Level 1 cache but slower, used to catch Level 1 misses before they reach lower memory. |
| L3 cache | Level 3 cache | Third cache level; often shared by multiple cores or clusters and commonly used as a Last-Level Cache before the memory controller. |
| I-cache | Instruction cache | Cache that stores instruction cache lines so the processor can fetch program code quickly. |
| D-cache | Data cache | Cache that stores data cache lines used by load/store instructions. |
| LLC | Last-Level Cache | Final cache level before main memory; reduces traffic to the memory controller and off-die DRAM. |
| Cache line / block | Fixed-size memory chunk stored in cache | Small block such as 32, 64 or 128 bytes transferred between cache levels; spatial locality works because nearby bytes come together. |
| Tag | Address identifier stored with a cache line | Tells the cache which memory block is currently stored in a selected cache entry. |
| Index | Address bits used to select cache set | Chooses where the cache should look for a line. |
| Offset | Address bits selecting byte/word inside line | Chooses the exact data inside the cache line after the line is found. |
| Valid bit | Cache metadata bit | Shows whether a cache entry contains meaningful data. |
| Dirty bit | Cache metadata bit | Shows that cached data was modified and must be written back before eviction in a write-back cache. |
| Cache hit | Requested data found in cache | Fast case; the processor can receive data from the current cache level. |
| Cache miss | Requested data not found in cache | Slow case; the cache must fetch the line from a lower memory level such as Level 2 cache, Level 3 cache, on-chip SRAM or DRAM path depending on the address map. |
| Cache refill / line fill | Loading a missed cache line | Lower memory supplies the missing line and the cache stores it for future hits. |
| Eviction | Removing an old cache line | Happens when a new line must be placed into a full cache set. |
| Write-through cache | Write policy | Store updates are written to the cache and also immediately passed to lower memory. |
| Write-back cache | Write policy | Store updates modify the cache first; lower memory is updated later when the dirty line is evicted or cleaned. |
| Write-allocate | Write miss policy | On a store miss, the cache first loads the line into cache and then writes it. |
| No-write-allocate | Write miss policy | On a store miss, the write goes to lower memory without bringing the line into cache. |
| Associativity | Number of possible places for a cache line | Higher associativity reduces conflict misses but increases lookup complexity, area and power. |
| Direct-mapped cache | One possible cache place per memory block | Simple and fast, but conflict misses can be high. |
| Set-associative cache | Few possible places per memory block | Common balance between hit rate and hardware cost. |
| Fully associative cache | Any line can go anywhere | Flexible but expensive for large caches because many tags must be compared. |
| Locality | Reuse pattern in program memory access | Reason caches work; programs tend to reuse the same addresses or nearby addresses. |
| Temporal locality | Reuse over time | Recently used instruction/data is likely to be used again soon. |
| Spatial locality | Reuse of nearby addresses | If one address is used, neighboring addresses are likely to be used soon. |
| Cache coherency | Correctness of shared cached data | Ensures different processors, caches and sometimes coherent DMA engines observe consistent values for shared memory. |
| Cache maintenance | Software/hardware cache management operations | Clean, invalidate or flush operations used when non-coherent DMA/peripherals share memory with cached CPU data. |
| MMU | Memory Management Unit | Hardware that translates virtual addresses to physical addresses and supports memory protection. |
| TLB | Translation Lookaside Buffer | Cache for address-translation entries used by an MMU. |
| Memory hierarchy | Layered memory organization | Registers, caches, on-die SRAM/ROM, off-die DRAM and storage arranged by speed, size, cost and distance from processor. |
| On-die memory | Memory inside the SoC die | Physical memory blocks fabricated on the same silicon die as processor/interconnect. Faster and lower latency than off-die memory but limited in capacity. |
| Off-die memory | Memory outside the SoC die | Memory placed on board/package outside the SoC die, such as DDR DRAM; larger capacity but higher latency and interface cost. |
| RAM | Random Access Memory | Read/write memory used for temporary data/code. Usually volatile. |
| ROM | Read Only Memory | Non-volatile memory used for fixed boot code, constants or firmware roots of trust. |
| SRAM | Static Random Access Memory | Fast volatile memory built from latch-like cells; commonly used for caches, TCM, scratchpad and on-die memory macros. |
| DRAM | Dynamic Random Access Memory | Dense volatile memory using capacitor-based cells that need refresh; usually used as large main memory, commonly off-die in SoCs. |
| eDRAM | Embedded Dynamic Random Access Memory | DRAM integrated on chip; denser than SRAM but process/integration and refresh complexity can be significant. |
| Embedded memory macro | Pre-designed physical memory block | Hard/compiled memory IP such as SRAM, ROM or register file inserted into SoC layout. |
| Memory compiler | Memory macro generator | EDA/IP tool that generates SRAM/ROM/register-file instances with selected size, ports, aspect ratio, timing and power options. |
| TCM | Tightly Coupled Memory | Low-latency on-die memory directly connected to a processor for deterministic code/data access. |
| ITCM | Instruction Tightly Coupled Memory | TCM usually used for critical instruction/interrupt code. |
| DTCM | Data Tightly Coupled Memory | TCM usually used for critical data, stacks or real-time buffers. |
| Scratchpad memory | Software-managed local memory | On-die SRAM controlled by software rather than hardware cache replacement. |
| FIFO | First In First Out | Queue memory used for buffering streams between producer and consumer blocks. |
| Buffer | Temporary storage | Small memory region used to absorb rate mismatch, hold packets/frames or decouple blocks. |
| Boot ROM | Boot Read Only Memory | On-die non-volatile memory that stores the first code executed after reset. |
| Memory map | Address layout of the SoC | Defines which address ranges correspond to ROM, SRAM, cacheable memory, peripheral registers, external DRAM and reserved regions. |
| Address space | Range of addresses visible to a processor or bus master | Determines what software/hardware can access and how large the accessible memory region is. |
| Memory-mapped I/O | Input/output registers placed in address space | Lets software access peripherals by reading and writing addresses, similar to memory locations. |
| Local memory | Memory close to one processor or accelerator | Gives low-latency access to a specific block but may be less convenient for sharing. |
| Shared memory | Memory accessible by multiple masters | Allows communication between processors, Direct Memory Access engines and accelerators, but needs arbitration and sometimes coherency. |
| DMA | Direct Memory Access | Hardware engine that copies data between memory and peripherals/accelerators without the CPU moving every byte. |
| ECC | Error Correction Code | Extra bits and logic used to detect and often correct memory bit errors. |
| Parity | Error-detection bit | Simpler protection than ECC; detects some errors but usually cannot correct them. |
| Bank | Independently accessible memory subdivision | Allows parallelism or interleaving inside SRAM/DRAM/memory macros. |
| Word line | Row select signal in a memory array | Activates a row of memory cells. |
| Bit line | Column data path in a memory array | Carries the stored bit value during read/write operation. |
| Sense amplifier | Memory read circuit | Detects small voltage differences on bit lines and converts them into digital 0/1 values. |
| Access time | Delay from request to first valid data | Major memory performance metric. |
| Bandwidth | Data transferred per second | Important for streaming, graphics, AI, camera, display and multicore traffic. |
| Determinism | Predictable timing behavior | Important for real-time systems where worst-case timing matters. |
| Board-based memory | Memory placed on the printed circuit board | Off-die memory device mounted outside the SoC package/die and connected through board traces. |
| PCB | Printed Circuit Board | Physical board carrying the SoC package, memory chips, power network and signal traces. |
| Package | Chip enclosure and connection structure | Connects the silicon die to external pins/balls so signals can reach the board. |
| Memory channel | Independent memory interface path | Group of command, address, data, clock and control signals between memory controller and memory device/module. |
| Rank | Group of memory chips selected together | Memory organization unit that responds as one wider memory data interface. |
| DIMM | Dual Inline Memory Module | Board/module containing multiple DRAM chips, common in computers and servers. |
| SoDIMM | Small Outline Dual Inline Memory Module | Smaller DRAM module form factor often used in laptops/compact systems. |
| DQ | Data input/output pins | DRAM data signals used to transfer read/write data. |
| DQS | Data Strobe | Timing strobe used with DDR data signals so receiver knows when data is valid. |
| CA bus | Command/Address bus | Interface signals carrying memory commands and address information. |
| CK | Clock | DDR memory timing reference signal. |
| CS | Chip Select | Signal used to select a specific memory chip or rank. |
| ODT | On-Die Termination | Termination resistance inside the memory device used to improve signal integrity. |
| Signal integrity | Quality of electrical signals | Board-level issue involving reflections, noise, skew, crosstalk and timing margin. |
| DRAM cell | Dynamic Random Access Memory bit cell | Usually one access transistor plus one storage capacitor that stores one bit as charge. |
| 1T1C | One Transistor One Capacitor | Common DRAM cell structure: one transistor controls access to one capacitor. |
| Volatile memory | Loses data without power | SRAM/DRAM need power to retain data. |
| Non-volatile memory | Retains data without power | ROM, Flash, eFuse/OTP retain data after power off. |
| Memory port | Access interface to memory | A single-port memory supports one access at a time; dual-port/multi-port memory supports more concurrent accesses but costs more area. |
| SDRAM | Synchronous Dynamic Random Access Memory | DRAM whose commands and data transfers are synchronized to a clock. |
| DDR SDRAM | Double Data Rate Synchronous Dynamic Random Access Memory | SDRAM family transferring data on both rising and falling clock edges. |
| LPDDR | Low-Power Double Data Rate | DDR DRAM family optimized for mobile and low-power SoCs. |
| Row decoder | Circuit that selects a memory row | Activates one word line from the row address. |
| Column decoder | Circuit that selects columns | Chooses which columns from an active row are read or written. |
| Row buffer | Temporary storage for an opened DRAM row | Holds sensed data from an active row and enables fast column accesses to that row. |
| RAS | Row Address Strobe | Older DRAM signal/concept for selecting row address; related to row activation. |
| CAS | Column Address Strobe | Older DRAM signal/concept for selecting column address; appears in CAS latency. |
| ACTIVATE | DRAM row-open command | Opens a selected row and loads it into sense amplifiers/row buffer. |
| READ | DRAM read command | Reads selected column data from an active row. |
| WRITE | DRAM write command | Writes selected column data into an active row. |
| PRECHARGE | DRAM row-close command | Closes a currently active row and prepares the bank for another row. |
| REFRESH | DRAM restore command | Periodically restores charge in DRAM cells so data is not lost. |
| Destructive read | Read operation that disturbs stored charge | In DRAM, reading a cell requires sensing and restoring the charge. |
| Retention time | Time a DRAM cell can hold charge | Determines how often refresh is required. |
| CL | CAS Latency | Delay between a read command and availability of first data. |
| tRCD | Row-to-Column Delay | Delay between ACTIVATE and READ/WRITE command. |
| tRP | Row Precharge Time | Delay required to close a row before opening another row. |
| tRFC | Refresh Cycle Time | Time DRAM is busy during refresh operation. |
| Memory request | Read or write access sent to memory | Generated by CPU, cache miss logic, Direct Memory Access engine, accelerator or peripheral. |
| Memory response | Data or completion returned by memory | Allows the requester to continue after read/write service. |
| Service time | Time a memory module needs to serve one request | Often written as Ts in simple processor-memory models. |
| Request rate | Number of memory requests generated per unit time | Determines pressure on the memory system. |
| Memory module | Independently serviceable memory unit | In simple models, a module can represent a bank, channel, memory block or independent memory controller path. |
| Memory contention | Multiple requests competing for same memory resource | Causes waiting, stalls and lower achieved bandwidth. |
| Busy module | Memory module serving at least one request | Used to calculate achieved bandwidth in simple interaction models. |
| Blocking request | Request that stops progress until it completes | Simple processor model where processor waits for memory response. |
| Nonblocking cache | Cache that can continue after a miss | Supports multiple outstanding misses instead of stalling on the first miss. |
| Outstanding request | Request issued but not yet completed | More outstanding requests increase memory-level parallelism but also pressure the memory system. |
| MSHR | Miss Status Holding Register | Hardware structure that tracks outstanding cache misses in nonblocking caches. |
| MLP | Memory-Level Parallelism | Ability to overlap multiple memory accesses to hide latency and improve bandwidth use. |
| Memory interleaving | Distributing addresses across modules/banks/channels | Reduces contention and increases parallel memory bandwidth. |
| Arbiter | Resource-selection logic | Chooses which requester gets access when multiple requests compete. |
| Scheduler | Request-ordering logic | Reorders or prioritizes memory requests to improve bandwidth, latency, fairness or quality of service. |
| AMAT | Average Memory Access Time | Cache/memory metric: hit time plus miss rate multiplied by miss penalty. |
| Hit rate | Fraction of accesses found in cache | Higher hit rate reduces requests reaching slower memory. |
| Miss rate | Fraction of accesses not found in cache | Higher miss rate increases traffic to lower memory levels. |
| Miss penalty | Extra delay caused by a cache miss | Includes lower-level cache, memory controller and DRAM access time. |
| Achieved bandwidth | Actual served requests per service time | Lower than ideal bandwidth when contention occurs. |
| On-chip interconnect | On-chip communication fabric | Hardware wires, switches, protocols and arbitration logic that connect SoC blocks. |
| Bus | Shared communication path | Interconnect where multiple blocks communicate using shared address/data/control resources. |
| Shared bus | One common bus used by many blocks | Simple but only limited transfers can occur at once, so it becomes a bottleneck. |
| Hierarchical bus | Multiple buses connected by bridges | Used to separate high-speed memory traffic from low-speed peripheral traffic. |
| Crossbar | Switch matrix interconnect | Allows multiple masters and slaves to communicate in parallel if paths do not conflict. |
| Switch fabric | General switching network | Interconnect structure that dynamically connects sources to destinations. |
| NoC | Network on Chip | Packet-based on-chip communication network using routers, links and network interfaces. |
| Network interface | Adapter between IP block and NoC | Converts bus-style transactions into NoC packets and converts packets back into transactions. |
| Router | NoC switching node | Receives packets/flits, chooses output direction and forwards them to another router or local block. |
| Link | Physical connection between routers/nodes | Carries flits or packets between NoC components. |
| Node / Tile | NoC endpoint region | Usually contains an IP block, local network interface and sometimes a router. |
| Packet | Formatted unit of network communication | Contains header, payload and sometimes tail/control information. |
| Flit | Flow control digit | Smaller unit of a packet moved through a NoC link/router during flow control. |
| Header | Routing/control part of packet | Contains destination, transaction type, route or other control fields. |
| Payload | Data part of packet | Carries read data, write data or transaction information. |
| Topology | Network connection pattern | Defines how routers/nodes are connected, such as mesh, ring, torus, tree or star. |
| Mesh topology | 2D grid network | Common NoC topology with routers connected north/south/east/west; regular and layout-friendly. |
| Torus topology | Mesh with wraparound links | Reduces edge distance but adds longer wraparound wires. |
| Ring topology | Nodes connected in a loop | Simple and area-efficient for moderate systems, but latency grows with hop count. |
| Star topology | Central hub connection | Simple for small systems but hub becomes bottleneck. |
| Tree topology | Hierarchical branch network | Useful for hierarchy but upper links can become bottlenecks. |
| Fat tree | Tree with higher bandwidth near root | Reduces upper-level bottleneck compared with a simple tree. |
| Routing | Path-selection method | Decides which output direction a packet/flit should take. |
| XY routing | Deterministic mesh routing | Routes first in X direction, then in Y direction; simple and deadlock-avoiding under proper conditions. |
| Deterministic routing | Fixed path rule | Same source-destination pair normally follows the same path. |
| Adaptive routing | Traffic-aware path rule | Chooses among possible paths depending on congestion or faults. |
| Switching | Method of moving packets through routers | Includes store-and-forward, virtual cut-through and wormhole switching. |
| Wormhole switching | Packet split into flits through routers | Header flit reserves/chooses path while following flits stream behind it, reducing buffer needs. |
| Store-and-forward | Whole packet buffered before forwarding | Simpler but may add latency and buffer cost. |
| Flow control | Preventing buffer/link overflow | Coordinates when flits can move so receivers are not overrun. |
| Backpressure | Reverse congestion signal | Tells upstream router/source to stop or slow sending because downstream buffers are full. |
| Virtual channel | Logical channel over one physical link | Helps avoid head-of-line blocking and can support QoS or deadlock avoidance. |
| Head-of-line blocking | Front packet blocks packets behind it | Occurs when one blocked packet prevents later packets from using available paths. |
| Congestion | Too much traffic for available network resources | Increases latency and reduces throughput. |
| Hop count | Number of router-to-router steps | More hops generally increase latency and energy. |
| Deadlock | Cyclic waiting with no progress | Packets wait on each other forever due to resource dependency cycle. |
| Livelock | Movement without delivery | Packet keeps moving but never reaches destination. |
| QoS | Quality of Service | Mechanisms for priority, bandwidth, latency or deadline guarantees in the interconnect. |
| Coherence | Consistency of cached copies | Ensures multiple caches see correct shared memory values. |
| ACE | AXI Coherency Extensions | AMBA protocol extension for cache-coherent communication, superseded in many newer systems by CHI. |
| CHI | Coherent Hub Interface | AMBA coherent interconnect protocol for high-performance coherent systems. |
| AXI | Advanced eXtensible Interface | High-performance AMBA protocol used for memory-mapped SoC communication. |
| AHB | Advanced High-performance Bus | AMBA bus protocol used in embedded SoCs, especially moderate-performance subsystems. |
| APB | Advanced Peripheral Bus | Simple low-power AMBA bus for low-bandwidth peripheral registers. |
| Bridge | Interconnect adapter | Connects different bus protocols, widths, clocks or address regions. |
| CDC | Clock Domain Crossing | Transfer of signals/data between different clock domains, often needed in large interconnects. |
| CPI | Cycles Per Instruction | Average number of clock cycles needed per instruction; lower is usually better. |
| IPC | Instructions Per Cycle | Average number of instructions completed per cycle; higher is usually better. |
| MIPS | Million Instructions Per Second | Rough instruction throughput metric; can be misleading across different ISAs/workloads. |
| Latency | Time for one operation/request | Important for real-time response and memory access behavior. |
| Throughput | Work completed per unit time | Important for streaming, multimedia, networking and compute workloads. |
| PPA | Power, Performance, Area | Main processor design tradeoff. |

Memory line for CLO 2:

```text
Processor choice decides programmability and system control.
Processor architecture defines the software-visible contract.
Processor microarchitecture decides how that contract is implemented in hardware.
Memory design decides where instructions/data are stored, how fast they can be accessed, and how much power/area the storage system consumes.
```

---

<a id="topic-1"></a>

## Topic 1: SoC Components - Core Logic, Processors, Choice Of Processors, Processor Architecture And Microarchitecture

<a id="topic-1-question"></a>

### Question

**Explain SoC Components: Core Logic - Processors, choice of processors, and basic concepts of processor architecture/microarchitecture.**

<a id="topic-1-clo-mapping"></a>

### CLO Mapping

This topic belongs to **CLO 2: Describe SoC and its Components; Bus Architecture and Interconnection of SoC**.

Reason: The syllabus places this topic under **SoC Components**. CLO 2 explicitly mentions SoC components, bus architecture and interconnection. Processor cores are one of the main SoC components and they directly interact with memory and interconnect.

Detailed local PPT/book/web references are kept in [sources/CLO2_Topic1_sources.md](<sources/CLO2_Topic1_sources.md>).

<a id="topic-1-what-asking"></a>

### What The Question Is Asking

The examiner is not asking only "what is a processor." A complete answer must explain:

1. What **core logic** means inside an SoC.
2. Why processors are central SoC components.
3. How designers choose a processor for an SoC.
4. What types of processors may be used.
5. Difference between **architecture / ISA** and **microarchitecture**.
6. Basic processor architecture concepts: instruction set, registers, load/store, register-memory, branches, interrupts and exceptions.
7. Basic processor microarchitecture concepts: pipeline, instruction unit, execution unit, memory system, hazards and performance limitations.
8. How processor choice affects power, performance, area, software and system integration.

Exam answer order:

```text
SoC components -> core logic -> processor role -> processor selection ->
processor types -> architecture/ISA -> microarchitecture -> performance tradeoffs.
```

<a id="topic-1-main-explanation"></a>

### Main Explanation

A **System on Chip (SoC)** is built from many components: processors, memories, interconnects, peripherals, accelerators, debug/test logic and sometimes analog/mixed-signal blocks. Among these, the **processor** is one of the most important components because it gives the SoC programmability.

The processor runs software. That software may include:

- boot code,
- firmware,
- device drivers,
- real-time tasks,
- operating system,
- application code,
- control algorithms.

The processor is therefore the bridge between hardware and software. A hardware accelerator may perform a fast computation, but the processor usually configures it, starts it, handles its interrupt and manages the complete system.

The local PPT [SOC components -processor.pdf](<System on chip/SOC components -processor.pdf>) says processor selection is important because SoC processors and systems are becoming increasingly complex. It also says SoC applications often use many different processor types suited to the application.

Web support: Arm officially describes architecture profiles such as A-profile for applications, R-profile for real-time systems and M-profile for microcontrollers. RISC-V International describes ISA specifications as the fundamental guidelines for designing and implementing RISC-V processors. These sources support the difference between processor architecture and processor implementation.

<a id="topic-1-core-logic"></a>

### Core Logic In SoC

**Core logic** means the main digital logic that performs computation, control and data processing inside the SoC.

Important definition:

```text
Core logic = the central digital computation/control portion of an SoC,
including processor cores, controllers, datapaths, accelerators and related
logic that implement the main system behavior.
```

Core logic is different from:

- **memory macros**, which mainly store data,
- **analog blocks**, which process continuous signals,
- **I/O pads**, which connect to external pins,
- **test structures**, which help manufacturing test.

Core logic usually includes:

- CPU or processor cores,
- DSP cores,
- control logic,
- DMA engines,
- bus/interconnect logic,
- hardware accelerators,
- interrupt controllers,
- security engines,
- protocol controllers.

#### Why Processor Core Logic Matters

Processor core logic matters because it determines:

- what software can run,
- how fast control code executes,
- whether an OS/RTOS can be supported,
- how interrupts are handled,
- how peripherals are controlled,
- how accelerators are configured,
- how much area and power the compute subsystem consumes,
- how easily the product can be updated by software.

Exam line: **Processor core logic gives an SoC programmability; without it, the chip would be mostly fixed-function hardware.**

<a id="topic-1-processor-in-soc"></a>

### Processor In SoC

A **processor** is a programmable hardware block that repeatedly performs an instruction cycle:

```text
fetch instruction -> decode instruction -> read operands -> execute operation -> write result -> update program counter
```

In an SoC, the processor is not alone. It is connected to:

- instruction memory/cache,
- data memory/cache,
- bus or NoC interconnect,
- DMA controller,
- interrupt controller,
- timers,
- peripherals,
- accelerators,
- debug logic,
- power/reset/clock controllers.

Simple SoC processor view:

```text
                 +----------------+
                 | Processor core |
                 |  fetch/decode  |
                 |  execute/WB    |
                 +--------+-------+
                          |
                    Bus / NoC / Interconnect
        +-----------------+------------------+
        |                 |                  |
   +----v----+       +----v-----+       +----v-----+
   | Memory  |       |Peripherals|      |Accelerator|
   +---------+       +----------+       +----------+
```

#### Why An SoC May Have Multiple Processors

An SoC may include more than one processor because different tasks need different compute styles.

Examples:

- **application CPU** runs Linux/Android or high-level application software,
- **microcontroller core** handles low-power control or always-on tasks,
- **DSP core** handles audio, modem or signal processing,
- **real-time core** handles safety-critical deterministic control,
- **security core** handles cryptographic and secure boot tasks,
- **soft processor** inside FPGA fabric handles local control,
- **accelerator** handles specialized computation under CPU control.

The Flynn/Luk textbook and local PPT both support this idea: SoC designs often use different processor types suited to application requirements.

#### Processor As An IP Block

Most SoC teams do not design a processor from scratch. They often license or reuse a processor IP block.

Processor IP may be:

| IP Form | Meaning | Use |
|---|---|---|
| Soft IP | RTL/synthesizable processor source | configurable and portable, but less predictable |
| Firm IP | constrained/partly implemented processor | balance of flexibility and predictability |
| Hard IP | physical silicon macro | predictable timing/power/area, but less flexible |

The processor may be purchased/licensed from third parties, reused internally, or implemented as an open/standard ISA design such as RISC-V.

<a id="topic-1-choice-processors"></a>

### Choice Of Processors

**Processor selection** means choosing the processor core or processor mix that allows the SoC to meet its functional, software, performance, power, area, cost and schedule requirements.

Important definition:

```text
Choice of processor = selecting the processor architecture, processor core,
configuration, memory system and software ecosystem that best match the SoC
application requirements.
```

The local processor PPT says processor selection is often obvious but restricted because the processor must run specific system software. It also says compute-limited applications require a processor configured and parameterized to meet that requirement.

#### Processor Selection Flow

Use this flow in your answer:

```text
Application requirements
      |
      v
Software requirement: OS/RTOS/firmware/toolchain?
      |
      v
Performance requirement: latency, throughput, real-time?
      |
      v
Power/area/cost limits
      |
      v
Memory/interconnect needs
      |
      v
Select processor type and configuration
      |
      v
Check with simulation/benchmarks
      |
      v
Add accelerator / DSP / extra core if needed
```

#### Main Criteria For Choosing A Processor

| Criterion | Meaning | Why It Matters |
|---|---|---|
| Software compatibility | Can it run required OS, RTOS, drivers and tools? | Processor must support the software stack |
| ISA ecosystem | Compiler, debugger, libraries, OS support | Strong ecosystem reduces development risk |
| Performance | Clock rate, IPC, CPI, cache, pipeline, execution units | Determines whether workload deadlines are met |
| Real-time behavior | Predictability and interrupt latency | Required for control, automotive, medical and safety systems |
| Power/energy | Dynamic and leakage power | Critical for battery and thermally constrained products |
| Area/cost | Silicon area and license cost | Affects die cost and product economics |
| Memory support | cache, TCM, MMU, MPU, address width | Affects OS support, bandwidth and latency |
| Interconnect compatibility | AXI/AHB/APB/NoC interfaces | Determines integration with SoC bus/memory system |
| Security | privilege levels, TrustZone-like isolation, secure boot support | Needed for secure products |
| Safety/reliability | lockstep, ECC, fault detection | Needed for safety-critical products |
| Configurability | custom instructions, cache size, pipeline options | Allows tuning to application |
| Verification/IP maturity | proven core, documentation, verification collateral | Reduces tapeout risk |

#### Processor Choice Based On Application

| Application Need | Suitable Processor Choice | Reason |
|---|---|---|
| Rich OS, high application performance | Application processor / Cortex-A style / high-end RISC-V core | supports MMU, caches, high performance |
| Hard real-time deterministic control | Real-time processor / Cortex-R style / lockstep capable core | predictable latency and safety features |
| Low-power embedded control | Microcontroller / Cortex-M style / small RISC-V MCU core | low area, low power, interrupt-friendly |
| Audio/video/signal processing | DSP or SIMD-capable processor | MAC, vector/SIMD and streaming efficiency |
| Domain-specific compute | ASIP or accelerator plus CPU | custom instructions/datapath for workload |
| FPGA-based local control | Soft processor such as MicroBlaze/Nios-style core | configurable and integrated in programmable fabric |
| High throughput parallel workload | multicore, SIMD, vector, GPU/NPU/accelerator | exploits parallelism |

#### Why The Processor Must Match Software

The processor is selected not only for hardware performance but also for software compatibility.

A processor used for a rich operating system generally needs:

- MMU - Memory Management Unit,
- caches,
- privilege levels,
- interrupt controller support,
- compiler/toolchain,
- debug support,
- OS port.

A small deeply embedded controller may not need an MMU. It may only need:

- predictable interrupt latency,
- low power,
- small area,
- integrated timers/peripherals,
- simple RTOS or bare-metal firmware support.

Exam line: **The best processor is not always the fastest processor; it is the processor that satisfies software, performance, power, area, cost and real-time requirements together.**

<a id="topic-1-types-processors"></a>

### Types Of Processors In SoC

#### 1. GPP - General-Purpose Processor

A **GPP - General-Purpose Processor** is designed to run many types of software. It is flexible and usually has strong compiler, OS and tool support.

Examples of use:

- application software,
- operating system,
- device drivers,
- protocol stacks,
- control flow,
- user interface,
- file/network management.

Benefits:

- high flexibility,
- mature software ecosystem,
- reusable across products,
- good for complex control and OS tasks.

Limitations:

- not always energy-efficient for repetitive heavy computation,
- may be slower than dedicated hardware for data-heavy tasks,
- performance depends on cache/memory/interconnect behavior.

#### 2. MCU - Microcontroller Processor

An **MCU - Microcontroller Unit** is a small embedded processor system optimized for control tasks, low power and deterministic response.

It is useful for:

- sensor control,
- motor control,
- timers,
- low-power always-on domain,
- basic firmware,
- real-time I/O control.

Compared with an application processor, an MCU usually has:

- smaller area,
- lower power,
- simpler pipeline,
- simpler memory system,
- fast interrupt response,
- fewer OS requirements.

#### 3. DSP - Digital Signal Processor

A **DSP - Digital Signal Processor** is optimized for repetitive mathematical operations used in signal processing.

DSP workloads include:

- audio filtering,
- modem/baseband processing,
- image/video processing,
- control loops,
- FFT/filtering,
- multiply-accumulate operations.

DSPs often include:

- MAC - Multiply Accumulate unit,
- SIMD/vector operations,
- circular addressing,
- saturation arithmetic,
- predictable loop execution,
- high memory bandwidth for streams.

#### 4. ASIP - Application-Specific Instruction Processor

An **ASIP - Application-Specific Instruction Processor** is a processor customized for a specific application or domain.

It sits between a GPP and fixed hardware:

```text
GPP: flexible but may be slow
ASIP: partly customized, still programmable
ASIC accelerator: fastest but least flexible
```

ASIP may add custom instructions such as:

- crypto round operation,
- DSP filter operation,
- matrix multiply primitive,
- bit manipulation,
- image-processing primitive.

Why useful:

- improves performance for target domain,
- preserves some programmability,
- may reduce power compared with running everything on GPP.

#### 5. Soft Processor

A **soft processor** is a processor implemented using programmable logic or synthesizable RTL rather than fixed silicon.

The local PPT says a soft core can be used in FPGA bitstream form. It lists reasons such as system-level integration cost reduction, design reuse, exact fit for microcontroller/peripheral combination and future protection against discontinued variants.

Examples:

- AMD/Xilinx MicroBlaze,
- Intel/Altera Nios-style soft processor,
- RISC-V soft cores,
- OpenRISC/LEON-style open cores.

Benefits:

- configurable,
- useful in FPGA/adaptive SoC designs,
- can be tailored to local control,
- reduces need for external microcontroller,
- can be reused across FPGA products.

Limitations:

- usually larger area and lower performance than hard processors,
- consumes FPGA fabric resources,
- power/time/area cost may be higher,
- may not be suitable for high-performance application software.

Web support: AMD describes MicroBlaze as a soft processor core for AMD adaptive SoCs/FPGAs, and MicroBlaze V as a soft-core RISC-V processor IP.

#### 6. Multicore / Multiprocessor SoC

A **multicore SoC** contains more than one processor core.

It may be:

- homogeneous: same type of core repeated,
- heterogeneous: different cores for different jobs.

Examples:

- application CPU + microcontroller,
- CPU + DSP,
- CPU cluster + NPU/GPU accelerator,
- real-time lockstep cores for safety,
- big/little-style performance/power core mix.

Benefits:

- parallel execution,
- separation of real-time and application tasks,
- better energy/performance scaling,
- dedicated cores for security/control/signal processing.

Challenges:

- shared memory consistency,
- cache coherency,
- interconnect bandwidth,
- synchronization,
- software scheduling,
- debug complexity.

<a id="topic-1-processor-architecture"></a>

### Processor Architecture

**Processor architecture** usually means the programmer-visible structure of the processor. In many contexts, it mainly means **ISA - Instruction Set Architecture**.

Important definition:

```text
Processor architecture / ISA = the software-visible contract of a processor:
instructions, registers, data types, memory addressing, exception behavior,
privilege model and programmer-visible state.
```

The local PPT says processor architecture consists of the instruction set. The Flynn/Luk textbook says the processor architecture is the instruction set, while the implementation is more than the instruction set.

#### What ISA Defines

An ISA may define:

- instruction formats,
- arithmetic/logical instructions,
- load/store instructions,
- branch/jump/call/return instructions,
- register set,
- program counter,
- status flags/condition codes,
- memory addressing modes,
- privilege levels,
- exception/interrupt behavior,
- memory model,
- optional extensions such as floating point, vector, compressed instructions or custom instructions.

#### Register Set

A **register set** is the set of fast internal processor registers used by instructions.

Registers may include:

- general-purpose registers,
- floating-point registers,
- vector registers,
- stack pointer,
- program counter,
- status/control registers.

Why registers matter:

- registers are much faster than memory,
- ALU operations usually use registers,
- compiler performance depends heavily on register availability,
- more registers can reduce memory traffic,
- but more registers may increase area and context-switch overhead.

The local processor PPT says instruction sets are usually based on register sets holding operands and addresses, and that register sizes commonly use 32 or 64-bit words.

#### L/S - Load/Store Architecture

**L/S** means **Load/Store architecture**. It is commonly associated with RISC-style processors.

In a load/store architecture:

```text
load  : memory -> register
ALU   : register + register -> register
store : register -> memory
```

Example:

```text
LD   R1, [A]
LD   R2, [B]
ADD  R3, R1, R2
ST   [C], R3
```

Benefits:

- simple regular instruction format,
- easier decode,
- easier pipelining,
- cleaner timing behavior,
- good for compiler optimization.

Limitation:

- may need more instructions than register-memory style,
- code size may be larger unless compressed instructions are used.

#### R/M - Register/Memory Architecture

**R/M** means **Register/Memory architecture**. In this style, some arithmetic instructions can use memory directly as an operand.

Example:

```text
ADD R1, [B]
```

Meaning:

```text
R1 = R1 + memory[B]
```

Benefits:

- fewer instructions for some operations,
- code may be more compact,
- smaller instruction cache pressure in some cases.

Limitations:

- instruction decoding is more complex,
- variable instruction length can be harder to decode,
- execution timing may be less regular,
- more hardware may be needed for instruction fetch/decode.

The PPT and book explain this as an area-time tradeoff: R/M can produce compact programs, but decoding and implementation complexity increase.

#### RISC Vs CISC

| Point | RISC / Load-Store Style | CISC / Register-Memory Style |
|---|---|---|
| Main idea | Simple regular instructions | Complex and compact instructions |
| ALU operands | Usually registers only | Registers and sometimes memory |
| Decode | Easier | More complex |
| Pipelining | Easier | Harder but possible with advanced decode |
| Code size | Can be larger | Can be smaller |
| Hardware complexity | Often simpler front-end | More complex front-end |
| SoC relevance | Popular for embedded cores | x86-style systems use complex decoding internally |

Important: RISC and CISC are not "good vs bad." They represent different tradeoffs. Modern processors often blur the boundary.

#### Branches

A **branch** changes control flow by changing the program counter.

Types:

- unconditional branch/jump,
- conditional branch,
- subroutine call,
- return.

Conditional branches often depend on condition codes:

```text
ALU operation sets flags: zero, negative, carry, overflow
branch checks flags
PC changes if condition is true
```

Branches are important because they can break the pipeline. If the processor does not know whether a branch is taken, it may fetch the wrong next instruction. Branch prediction is used to reduce this delay.

#### Interrupts And Exceptions

**Interrupts** and **exceptions** both transfer control to special handler code, but they are not the same.

| Point | Interrupt | Exception |
|---|---|---|
| Source | Usually external hardware/peripheral | Usually caused by current instruction |
| Timing | Often asynchronous | Often synchronous |
| Example | timer interrupt, UART interrupt, DMA done | divide by zero, invalid instruction, page fault |
| Handler | ISR or interrupt handler | exception handler |
| Purpose | respond to external events | handle abnormal/internal events |

The local PPT says embedded SoC controllers have external interrupts and internal exceptions that require attention from an interrupt manager or handler program.

Key classifications:

- **maskable vs non-maskable**: can be ignored/disabled or cannot be ignored,
- **synchronous vs asynchronous**: caused by instruction or external event,
- **terminate vs resume**: stop program or resume after handler,
- **between vs within instructions**: when the event is recognized.

Exam line: **Architecture defines what the programmer and compiler see; microarchitecture defines how the processor internally implements it.**

<a id="topic-1-processor-microarchitecture"></a>

### Processor Microarchitecture

**Processor microarchitecture** is the internal hardware organization used to implement the ISA.

Important definition:

```text
Microarchitecture = internal processor implementation: pipeline stages,
instruction fetch/decode, execution units, register file, cache hierarchy,
branch prediction, issue logic, scheduling, buffers and control logic.
```

Two processors can use the same ISA but have different microarchitectures.

Example:

```text
Same ISA:
RISC-V RV32I

Possible microarchitectures:
small 3-stage in-order microcontroller core
5-stage pipelined embedded core
superscalar out-of-order high-performance core
```

They can run the same machine instructions, but their speed, power, area and complexity will be different.

#### Main Microarchitecture Blocks

The local PPT says every processor has:

- memory system,
- execution unit/datapath,
- instruction unit.

#### 1. Instruction Unit

The **instruction unit** fetches, decodes and controls instruction execution.

It may include:

- program counter,
- instruction fetch logic,
- instruction cache,
- branch predictor,
- decoder,
- control unit,
- issue/dispatch logic.

Why it matters:

- controls instruction flow,
- decides what operation happens next,
- handles branches and instruction dependencies,
- feeds execution units.

#### 2. Execution Unit / Datapath

The **execution unit** performs operations.

It may include:

- ALU,
- multiplier/divider,
- FPU,
- SIMD/vector unit,
- load/store unit,
- branch unit,
- register file,
- bypass/forwarding paths.

Why it matters:

- more execution units can improve throughput,
- specialized units improve performance for specific workloads,
- extra units increase area and power.

#### 3. Memory System

The **memory system** supplies instructions and data.

It may include:

- instruction cache,
- data cache,
- TCM/scratchpad,
- MMU/MPU,
- TLB,
- store buffer,
- load/store queue,
- bus interface.

Why it matters:

- a fast execution unit is useless if instructions/data arrive too slowly,
- cache misses create stalls,
- memory bandwidth affects CPI/IPC,
- real-time systems may prefer predictable memory over complex caches.

#### Pipeline

A **pipeline** overlaps different stages of different instructions.

Simple stages from the local PPT/book:

```text
IF -> ID -> AG -> DF -> EX -> WB
```

Meaning:

| Stage | Full Form | Meaning |
|---|---|---|
| IF | Instruction Fetch | fetch instruction from memory/cache |
| ID | Instruction Decode | decode opcode and control fields |
| AG | Address Generation | compute memory address for load/store |
| DF | Data Fetch | fetch operand/data |
| EX | Execute | perform ALU/FPU/branch operation |
| WB | Write Back | write result to register/architectural state |

Pipeline idea:

```text
Cycle 1: I1 IF
Cycle 2: I1 ID, I2 IF
Cycle 3: I1 AG, I2 ID, I3 IF
Cycle 4: I1 DF, I2 AG, I3 ID, I4 IF
```

The processor is not finishing all instructions instantly. It is overlapping different instruction phases to increase throughput.

#### Issue Width

**Issue width** means how many instructions the processor can issue per cycle.

| Processor Type | Meaning |
|---|---|
| Single-issue | issues at most one instruction per cycle |
| Superscalar | dynamically issues multiple instructions per cycle |
| VLIW | compiler packs multiple operations into one wide instruction |

The local PPT says simple processors issue one instruction per cycle, while desktop/laptop/server processors may issue multiple instructions each cycle.

#### Pipeline Hazards / Pipeline Breaks

The local PPT says pipeline breaks or delays are the major limit on performance.

##### 1. Data Conflict / Data Hazard

A data hazard happens when an instruction needs a value that has not yet been produced.

Example:

```text
I1: ADD R1, R2, R3
I2: SUB R4, R1, R5
```

`I2` needs `R1`, but `I1` has not written it back yet.

Solutions:

- forwarding/bypassing,
- stalling,
- out-of-order execution,
- compiler scheduling.

##### 2. Resource Contention / Structural Hazard

Resource contention happens when two instructions need the same hardware resource at the same time.

Examples:

- one memory port but two memory accesses,
- one multiplier but two multiply operations,
- limited register-file ports,
- one bus interface with multiple pending requests.

Solutions:

- add more resources,
- schedule instructions differently,
- stall one instruction,
- use out-of-order execution.

##### 3. Run-On Delay

Run-on delay occurs especially in in-order execution when a long-latency operation delays later instructions.

Example:

```text
I1: DIV R1, R2, R3     long divide operation
I2: ADD R4, R5, R6     ready but cannot complete if in-order rules block it
```

##### 4. Branch / Control Hazard

A branch hazard occurs when the processor does not know the next instruction address until the branch is resolved.

Solutions:

- branch prediction,
- branch target buffer,
- speculative execution,
- delayed branch/compiler scheduling,
- shorter branch-resolution path.

Exam line: **Microarchitecture tries to increase performance by overlapping and parallelizing instruction execution, but hazards, memory delays and branches limit the benefit.**

<a id="topic-1-architecture-vs-microarchitecture"></a>

### Architecture Vs Microarchitecture

This is one of the most important distinctions in the topic.

| Point | Architecture / ISA | Microarchitecture |
|---|---|---|
| Main idea | What software sees | How hardware implements it |
| Defines | instructions, registers, addressing, exceptions, privilege model | pipeline, caches, branch predictor, execution units, issue width |
| Visible to programmer? | Yes | Mostly no |
| Affects binary compatibility? | Yes | Usually no, if ISA is same |
| Examples | Armv8-A, Armv8-M, RISC-V RV32I/RV64GC, x86-64 | Cortex-A implementation, small RISC-V microcontroller core, out-of-order core |
| Main concern | software contract | power, performance, area, timing |

#### Example 1: Same ISA, Different Microarchitecture

Two processors may both implement the same RISC-V ISA:

```text
Core A: small in-order 3-stage pipeline
Core B: high-performance out-of-order superscalar pipeline
```

Software compiled for the ISA can run on both, but:

- Core A is smaller and lower power,
- Core B is faster but larger and more power-hungry.

#### Example 2: Arm Profiles

Arm describes three architecture profiles:

- **A-profile** for application processors and rich operating systems,
- **R-profile** for real-time systems,
- **M-profile** for microcontrollers and small low-power embedded devices.

These profiles are architecture-level choices. Actual processor cores implementing them can still have different microarchitectures.

#### Why This Distinction Matters In SoC

If the SoC requires a specific software ecosystem, ISA compatibility matters. If the SoC must meet power/performance/area targets, microarchitecture matters.

Example:

```text
Software requirement: run Linux -> need suitable ISA/profile, MMU, toolchain.
Performance requirement: process data fast -> need suitable pipeline/cache/execution units.
Power requirement: battery product -> need small energy-efficient microarchitecture.
```

Exam line: **Architecture decides software compatibility; microarchitecture decides implementation efficiency.**

<a id="topic-1-performance"></a>

### Performance Metrics And Tradeoffs

Processor choice is a tradeoff. A processor cannot be judged only by clock frequency.

#### Important Metrics

| Metric | Meaning | Why It Matters |
|---|---|---|
| Clock frequency | cycles per second | Higher frequency can improve speed but increases power/timing difficulty |
| CPI | average cycles per instruction | Lower CPI usually means better efficiency |
| IPC | instructions per cycle | Higher IPC means more work per cycle |
| MIPS | million instructions per second | Rough metric, but misleading across ISAs/workloads |
| Latency | time for one task/operation | important for response time and real-time systems |
| Throughput | tasks/data processed per unit time | important for streaming and high-volume workloads |
| Power | energy/time consumed | critical for battery and thermal limits |
| Area | silicon cost | affects die size, yield and product cost |
| Determinism | predictability of execution time | important for real-time and safety-critical systems |

#### Basic Performance Relation

Use this simple relation in exams:

```text
CPU time = Instruction count x CPI x Clock cycle time
```

or:

```text
CPU time = (Instruction count x CPI) / Clock frequency
```

This shows why processor performance depends on:

- number of instructions,
- cycles per instruction,
- clock frequency.

But in SoC design, memory and interconnect also matter. A processor with a high clock frequency may still be slow if it waits on cache misses, DRAM or bus contention.

#### Area-Time-Power Tradeoff

Processor design always balances:

```text
Performance vs Area vs Power
```

Examples:

- deeper pipeline may raise clock frequency but increase branch penalty and power,
- larger cache may reduce misses but increase area and leakage,
- multiple cores may improve throughput but increase software and coherency complexity,
- out-of-order execution may improve IPC but adds large hardware cost,
- SIMD may improve vector workloads but not general branch-heavy code.

The local chip-basics PPT emphasizes time, area and power as basic design tradeoffs.

#### Real-Time Vs High Throughput

Do not confuse real-time with high speed.

| Concept | Meaning | Example |
|---|---|---|
| Real-time | response must occur before deadline | airbag controller, motor control |
| High throughput | lots of work per second | video encoding, network packet processing |

A real-time processor needs predictability. A high-throughput processor needs high average performance. Sometimes a small deterministic core is better than a complex high-performance core.

<a id="topic-1-final-answer"></a>

### Final Exam-Ready Answer

An SoC is a complete system integrated on one chip and contains processors, memories, interconnects, peripherals, accelerators and control logic. In the SoC components topic, **core logic** refers to the main digital computation and control logic inside the SoC. The processor is a major part of core logic because it gives the SoC programmability and runs software such as firmware, drivers, RTOS, operating system and application code.

The choice of processor is an important SoC design decision. The processor must match the software requirement, performance requirement, real-time requirement, power budget, area cost, memory system and interconnect structure. If the SoC must run a rich operating system, an application processor with MMU, caches and strong software ecosystem may be needed. If the SoC needs deterministic control, a real-time or microcontroller-class processor may be better. If the workload is signal-processing heavy, a DSP or SIMD/vector-capable processor may be chosen. If the workload is domain-specific, an ASIP, accelerator or soft processor may be used.

Processor architecture mainly means the instruction set architecture, or ISA. The ISA is the software-visible contract of the processor. It defines instructions, registers, data types, memory addressing, condition codes, branches, interrupts, exceptions and privilege behavior. Common instruction styles include load/store architecture, where ALU operations use registers and memory is accessed only through load/store instructions, and register-memory architecture, where instructions may operate directly on memory operands. Load/store style is regular and easier to pipeline, while register-memory style can give compact code but may require more complex decoding.

Processor microarchitecture is the internal hardware implementation of the ISA. It includes the instruction unit, execution unit, register file, pipeline, caches, branch prediction, issue logic, scheduling and memory interface. The same ISA can be implemented by different microarchitectures. A small in-order core and a high-performance out-of-order superscalar core may execute the same ISA but differ greatly in performance, power and area.

A basic processor executes instructions through stages such as instruction fetch, instruction decode, address generation, data fetch, execute and write back. Pipelining overlaps these stages for different instructions to improve throughput. However, pipeline performance is limited by hazards such as data conflicts, resource contention, run-on delays and branches. Techniques such as forwarding, additional resources, branch prediction, superscalar issue and out-of-order execution can reduce these delays but increase area and power.

Therefore, processor selection in SoC design is a tradeoff among programmability, performance, power, area, cost, real-time behavior, software ecosystem and integration effort. Architecture decides what software can run, while microarchitecture decides how efficiently the processor implements that architecture in hardware.

<a id="topic-1-short-answer"></a>

### Short 10-Mark Answer

Core logic in an SoC is the main digital computation and control logic, including processor cores, controllers, datapaths and accelerators. A processor is a programmable hardware block that fetches, decodes and executes instructions. It is central to an SoC because it runs firmware, drivers, operating system and application software.

Processor selection depends on software compatibility, performance, real-time behavior, power, area, memory system, interconnect support, toolchain, IP availability and verification risk. A general-purpose processor is chosen for flexibility, a microcontroller for low-power control, a DSP for signal processing, an ASIP for domain-specific programmable acceleration and a soft processor for FPGA/configurable designs.

Processor architecture mainly means ISA, the programmer-visible contract. It defines instructions, registers, addressing, branches, interrupts and exceptions. Load/store architectures use registers for ALU operations and separate load/store instructions for memory access. Register-memory architectures allow memory operands in some arithmetic instructions.

Microarchitecture is the internal implementation of the ISA. It includes pipeline stages, execution units, caches, branch prediction, issue logic and memory interface. A basic pipeline has instruction fetch, decode, address generation, data fetch, execute and write back stages. Pipeline delays arise from data hazards, resource contention, long-latency operations and branches. Thus, architecture controls software compatibility, while microarchitecture controls performance, power and area.

<a id="topic-1-technical-words"></a>

### Technical Words To Use For Marks

- **SoC - System on Chip** (write this because the topic is about SoC components.)
- **Core logic** (write this because the syllabus says CoreLogic and it means the main digital computation/control logic.)
- **Processor core** (write this because the processor is the core logic block that runs software.)
- **GPP - General-Purpose Processor** (write this because many SoCs need a flexible software processor.)
- **MCU - Microcontroller Unit** (write this because low-power embedded control often uses microcontroller-class cores.)
- **DSP - Digital Signal Processor** (write this because signal-processing SoCs often need DSP-style execution.)
- **ASIP - Application-Specific Instruction Processor** (write this because it explains customized programmable processors.)
- **Soft processor** (write this because the PPT discusses soft cores and FPGA/adaptive SoC use.)
- **Processor IP** (write this because SoCs often integrate licensed/reused processor cores.)
- **ISA - Instruction Set Architecture** (write this because processor architecture mainly means software-visible instruction contract.)
- **Microarchitecture** (write this because the topic explicitly asks architecture/microarchitecture.)
- **Register file** (write this because instructions use registers for operands and results.)
- **ALU - Arithmetic Logic Unit** (write this because it is the main integer execution unit.)
- **FPU - Floating-Point Unit** (write this because floating-point workloads need specialized execution support.)
- **PSW - Program Status Word** (write this because condition/status information is part of architecture.)
- **CC - Condition Code** (write this because branches often test condition flags.)
- **PC - Program Counter** (write this because it controls instruction fetch sequence.)
- **RISC - Reduced Instruction Set Computer** (write this because load/store style is associated with RISC.)
- **CISC - Complex Instruction Set Computer** (write this because register-memory style is associated with more complex instructions.)
- **L/S - Load/Store architecture** (write this because the PPT explicitly compares load/store and register-memory styles.)
- **R/M - Register/Memory architecture** (write this because the PPT explains memory operands and decode complexity.)
- **Branch** (write this because control flow affects pipeline performance.)
- **Interrupt** (write this because embedded SoC processors respond to external events.)
- **Exception** (write this because processor architecture defines internal fault handling.)
- **Pipeline** (write this because almost all modern processors use instruction execution pipelines.)
- **IF, ID, AG, DF, EX, WB** (write these because they show exact pipeline stages from the PPT/book.)
- **Hazard** (write this because pipeline delays are a major performance limit.)
- **Data hazard** (write this because dependent instructions may need unavailable operands.)
- **Resource contention / structural hazard** (write this because multiple instructions can demand the same resource.)
- **Branch prediction** (write this because it reduces control-flow pipeline delays.)
- **Superscalar** (write this because multiple issue improves instruction-level parallelism.)
- **VLIW - Very Long Instruction Word** (write this because it is a compiler-scheduled ILP approach.)
- **SIMD - Single Instruction Multiple Data** (write this because array/vector processors exploit data parallelism.)
- **MIMD - Multiple Instruction Multiple Data** (write this because multiprocessors execute independent instruction streams.)
- **CPI - Cycles Per Instruction** (write this because it is a basic processor performance metric.)
- **IPC - Instructions Per Cycle** (write this because it measures instruction throughput.)
- **PPA - Power, Performance, Area** (write this because processor choice is a tradeoff among these.)
- **MMU - Memory Management Unit** (write this because rich OS support usually requires virtual memory.)
- **Cache** (write this because cache/memory speed affects instruction/data fetch cycles.)
- **Real-time determinism** (write this because some SoCs need predictable response, not just high average speed.)

<a id="topic-1-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image part 1**: [Screenshot 2026-05-12 230027.png](<images/Screenshot 2026-05-12 230027.png>) contains the syllabus headline **SoC Components: CoreLogic - Processors, choice of processors, Basic concepts of processor**.
2. **Topic image part 2**: [Screenshot 2026-05-12 230034.png](<images/Screenshot 2026-05-12 230034.png>) completes the headline with **architecture/microarchitecture**.
3. **Syllabus/CLO image**: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) maps this topic to the SoC Components section and CLO 2.

#### Figure 1: SoC Processor As Core Logic

Draw this when asked about processor as an SoC component:

```text
                 System on Chip
+--------------------------------------------------+
| Processor core / CPU                             |
|   + instruction unit + execution unit + registers |
|                                                  |
| Interconnect / Bus / NoC                         |
|                                                  |
| Memory       Peripherals       DMA       Accelerator|
+--------------------------------------------------+
```

Why this figure is useful: it shows that the processor is part of a larger SoC and depends on memory/interconnect/peripherals.

#### Figure 2: Processor Selection Flow

Draw this when asked "choice of processors":

```text
Application requirements
        |
Software / OS / RTOS needs
        |
Performance + real-time needs
        |
Power + area + cost limits
        |
Memory + interconnect needs
        |
Choose GPP / MCU / DSP / ASIP / soft processor / multicore
        |
Simulate and verify against requirements
```

Why this figure is useful: it shows processor selection is driven by system requirements, not only clock speed.

#### Figure 3: Architecture Vs Microarchitecture

```text
Software / compiler
        |
        v
ISA / Architecture
instructions, registers, branches, exceptions, memory model
        |
        v
Microarchitecture
pipeline, caches, execution units, branch predictor, issue logic
        |
        v
Physical implementation
gates, timing, area, power
```

Why this figure is useful: it clearly separates what software sees from how hardware implements it.

#### Figure 4: Basic Pipeline

```text
Instruction flow:

IF -> ID -> AG -> DF -> EX -> WB

IF = Instruction Fetch
ID = Instruction Decode
AG = Address Generation
DF = Data Fetch
EX = Execute
WB = Write Back
```

Why this figure is useful: it is the simplest diagram for processor microarchitecture.

#### Figure 5: Pipeline Hazards

```text
Pipeline performance limit
        |
        +-- Data hazard: operand not ready
        +-- Structural hazard: resource conflict
        +-- Control hazard: branch target/outcome unknown
        +-- Long-latency operation: multiply/divide/cache miss
```

Why this figure is useful: it directly matches the PPT discussion of pipeline delays/breaks.

#### Figure 6: Load/Store Vs Register/Memory

```text
Load/Store:
LD R1, [A]
LD R2, [B]
ADD R3, R1, R2
ST [C], R3

Register/Memory:
ADD R1, [B]
```

Why this figure is useful: it explains the architecture tradeoff between regular execution and compact instruction encoding.

---

<a id="topic-2"></a>

## Topic 2: Memory Design Overview And SoC On-Die Memory Systems

<a id="topic-2-question"></a>

### Question

**Explain Memory Design - Overview, and SoC (On-Die) Memory Systems.**

<a id="topic-2-clo-mapping"></a>

### CLO Mapping

This topic belongs to **CLO 2: Describe SoC and its Components; Bus Architecture and Interconnection of SoC**.

Reason: The syllabus places this topic in the **SoC Components** portion. Memory is one of the main SoC components, along with processors, interconnects, peripherals and accelerators. This topic also connects to CLO 3 because CLO 3 later studies memory technologies and memory controllers in more detail. For this answer, the focus is the **component-level view**: what memory blocks exist inside the SoC, why they are needed, and how they are organized.

Detailed local PPT/book/web references are kept in [sources/CLO2_Topic2_sources.md](<sources/CLO2_Topic2_sources.md>).

<a id="topic-2-what-asking"></a>

### What The Question Is Asking

The examiner is not asking only for a list of memories. A complete answer must explain:

1. What a **memory system** means in an SoC.
2. Why memory design is a major part of SoC design.
3. What **on-die memory** means physically.
4. Which memory blocks are commonly present on the SoC die.
5. Why on-die memory is fast but limited.
6. Why large memory is often kept off-die.
7. How memory hierarchy connects processor, cache, SRAM, ROM and external memory.
8. How memory choice affects **latency, bandwidth, area, power, cost, capacity, determinism and programmability**.
9. What diagrams should be drawn in an exam.

Exam answer order:

```text
Memory system -> memory hierarchy -> on-die memory definition ->
types of on-die memories -> why they are used -> tradeoffs ->
on-die vs off-die -> final answer.
```

<a id="topic-2-main-explanation"></a>

### Main Explanation

A **memory system** is the complete storage arrangement used by an SoC to hold instructions, data, constants, temporary buffers, boot code, register state and communication queues. It is not a single memory block. A real SoC normally contains many memory structures at different distances from the processor and interconnect.

The processor cannot perform useful work with only an Arithmetic Logic Unit or pipeline. It must continuously fetch instructions, read operands, write results, load configuration data, handle stacks, access buffers and communicate with peripherals. If memory cannot supply data fast enough, the processor or accelerator stalls. Therefore, memory design strongly controls SoC performance.

Important beginner point:

```text
Processor = executes instructions.
Memory = stores the instructions and data that the processor needs.
Interconnect = carries requests between processors, memories and peripherals.
```

So when we discuss memory in SoC design, we are asking:

- Where is the program stored?
- Where is data stored during execution?
- Which memory is closest to the **CPU - Central Processing Unit**?
- Which memory is large enough for applications?
- Which memory is predictable enough for real-time code?
- Which memory is cheap enough for large capacity?
- Which memory is low power enough for the target product?

**On-die memory** means memory physically fabricated on the same silicon die as the SoC logic. It is hardware, not software. It occupies real chip area and is implemented using memory arrays, peripheral circuits, decoders, word lines, bit lines, sense amplifiers, read/write drivers and sometimes error-correction logic.

Typical on-die memories include:

- processor register files,
- Level 1/Level 2/Level 3 caches,
- Static Random Access Memory blocks,
- boot Read Only Memory,
- scratchpad memory,
- Tightly Coupled Memory,
- First In First Out queues,
- packet/video/audio buffers,
- lookup tables,
- configuration memories,
- small non-volatile memories such as eFuse or One-Time Programmable memory in some SoCs.

The key idea:

```text
On-die memory is fast because it is physically close to the logic.
On-die memory is limited because silicon area is expensive.
```

<a id="topic-2-why-important"></a>

### Why Memory Design Is Important In SoC

Memory design is important because most SoC workloads are not limited only by computation. They are often limited by data movement.

Example:

```text
CPU - Central Processing Unit executes an instruction.
CPU needs next instruction.
CPU needs data operands.
CPU writes result.
Cache miss occurs.
Request goes through interconnect.
External memory is accessed.
CPU waits if data is not ready.
```

Even if the **CPU - Central Processing Unit** clock frequency is high, it may waste cycles waiting for memory. This is called the **memory bottleneck** or **processor-memory gap**.

Memory design affects:

1. **Performance**: Faster memory reduces stalls and improves instruction/data throughput.
2. **Power**: Moving data far across the chip or off the chip consumes energy.
3. **Area**: Large **SRAM - Static Random Access Memory** arrays can occupy a large part of the die.
4. **Cost**: Bigger die area reduces manufacturing yield and increases cost.
5. **Real-time behavior**: Cache misses make timing less predictable; Tightly Coupled Memory and scratchpad memory give more predictable timing.
6. **Boot behavior**: Boot Read Only Memory must be available immediately after reset.
7. **Security**: Secure boot code, keys and fuses may need protected on-die storage.
8. **Interconnect traffic**: On-die local memories reduce traffic to shared buses, Network on Chip and external Dynamic Random Access Memory.
9. **System integration**: Different masters such as Central Processing Unit, Direct Memory Access engine, Digital Signal Processor, Graphics Processing Unit and accelerators may compete for memory.

Memory is therefore a system-level design decision, not just a storage detail.

#### Why Not Use One Big Fast Memory?

A beginner may ask: if on-die memory is fast, why not make the whole memory on the chip?

The answer is tradeoff:

- Large on-die Static Random Access Memory consumes huge silicon area.
- Large area increases cost and reduces yield.
- More memory can increase leakage power.
- Dynamic Random Access Memory is denser, but standard logic process and dense Dynamic Random Access Memory process are not always the same.
- Off-die Double Data Rate Dynamic Random Access Memory gives much larger capacity at lower cost per bit.
- Some products need gigabytes of memory, which is unrealistic to place entirely on the SoC die.

Therefore, SoCs use a **hierarchy**:

```text
Small, fast, expensive memory near the processor.
Large, slower, cheaper memory farther away.
```

<a id="topic-2-memory-hierarchy"></a>

### Memory Hierarchy Overview

**Memory hierarchy** means arranging memory into levels according to speed, capacity, cost and distance from the processor.

Basic hierarchy:

```text
Fastest / smallest / closest

CPU - Central Processing Unit registers
Level 1 Instruction cache and Level 1 Data cache
Tightly Coupled Memory / scratchpad memory
Level 2 cache
Level 3 cache / system-level cache
On-die SRAM - Static Random Access Memory / ROM - Read Only Memory / buffers
Off-die DRAM - Dynamic Random Access Memory such as
DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory
or LPDDR - Low-Power Double Data Rate
Non-volatile storage such as Flash, eMMC or UFS

Slowest / largest / farthest
```

Why this hierarchy exists:

- CPU - Central Processing Unit registers are extremely fast, but very small.
- Level 1 cache is very fast, but still small.
- Level 2/Level 3 cache is larger, but slower than Level 1 cache.
- On-die Static Random Access Memory can be used for buffers and real-time memory, but costs die area.
- Off-die Dynamic Random Access Memory gives large capacity, but has higher latency and needs a memory controller.
- Flash or storage keeps data without power, but is much slower than Random Access Memory.

#### Locality

Memory hierarchy works because programs show **locality**. Locality means program memory accesses are not completely random. They usually have patterns.

**Temporal locality** means if data or an instruction is used now, it may be used again soon.

Example:

```text
for (i = 0; i < 1000; i++)
    sum = sum + a[i];
```

In this loop, the loop instructions are fetched again and again. The variable `sum` is also reused repeatedly. This is temporal locality.

**Spatial locality** means if one address is used, nearby addresses may be used soon.

Example:

```text
a[0], a[1], a[2], a[3] ...
```

Array elements are stored close together in memory. If `a[0]` is read, `a[1]` and `a[2]` may be read soon. Instruction addresses also usually move forward sequentially, so nearby instruction bytes are likely to be fetched.

This is the reason caches are useful. A cache does not normally fetch only one byte. It fetches a **cache line**, which is a small block of nearby bytes. If the program uses nearby addresses soon, the data is already in the cache.

Important exam line:

```text
Caches exploit temporal and spatial locality automatically.
Scratchpad memory and Tightly Coupled Memory exploit locality through software, compiler or firmware placement.
```

<a id="topic-2-cache-hierarchy-deep"></a>

### Cache Hierarchy In Depth: Level 1, Level 2 And Level 3

A **cache** is a small, fast, hardware-managed memory that stores copies of instructions or data from lower memory levels. It is normally built using **SRAM - Static Random Access Memory** because SRAM is fast, random-access, compatible with logic processes and does not need refresh like **DRAM - Dynamic Random Access Memory**.

A cache is not the original permanent location of data. The original data may be in on-chip Static Random Access Memory, off-chip Dynamic Random Access Memory, Read Only Memory or storage after loading. The cache keeps a copy so that repeated access becomes faster.

The main reason cache exists is the **processor-memory gap**:

```text
Processor pipeline can execute quickly.
Large memory is slower and farther away.
If every instruction/data access went to DRAM - Dynamic Random Access Memory, the CPU - Central Processing Unit would stall often.
Cache keeps likely-needed data close to the CPU.
```

#### 1. L1 Cache - Level 1 Cache

**L1 cache** means **Level 1 cache**. It is the first cache level seen by the processor core and is physically closest to the execution pipeline. It is the smallest and fastest cache level.

In many processors, Level 1 cache is split into:

- **I-cache - Instruction cache**: stores instructions, meaning program code fetched by the instruction fetch stage.
- **D-cache - Data cache**: stores data used by load and store instructions.

This split is important. A processor often needs to fetch the next instruction and access data in the same cycle or nearby cycles. If instruction fetch and data load/store shared one small Level 1 cache port, they would conflict more often. Separate Instruction cache and Data cache allow instruction access and data access to happen more independently.

Why Level 1 cache is small:

- It must be extremely fast.
- It sits close to the processor pipeline.
- Large cache arrays take longer to search.
- More capacity increases area, power and access delay.

What Level 1 cache does:

- supplies instructions quickly to the instruction fetch stage,
- supplies operands quickly to load instructions,
- accepts store data quickly from the processor,
- reduces the number of requests sent to Level 2 cache or memory.

Beginner example:

```text
CPU - Central Processing Unit executes a loop.
The loop instructions fit in L1 Instruction cache.
The CPU fetches them quickly every iteration.
If array data also fits or streams well through L1 Data cache, data loads are faster.
```

#### 2. L2 Cache - Level 2 Cache

**L2 cache** means **Level 2 cache**. It is below Level 1 cache in the hierarchy. It is usually larger than Level 1 cache but slower. It may be private to one core or shared by a small cluster of cores, depending on the SoC design.

Why Level 2 cache is used:

- Level 1 cache is too small to hold the full working set of many programs.
- If a Level 1 miss occurs, going directly to Dynamic Random Access Memory would be expensive in time and energy.
- Level 2 cache catches many Level 1 misses and prevents them from becoming external memory accesses.

Level 2 cache is often **unified**, meaning it may store both instruction lines and data lines. This is different from the common split Level 1 Instruction cache and Level 1 Data cache arrangement.

What happens in a common hierarchy:

```text
CPU - Central Processing Unit asks Level 1 cache.
If Level 1 cache misses, request goes to Level 2 cache.
If Level 2 cache hits, Level 2 supplies the line to Level 1.
If Level 2 cache misses, request goes farther down the hierarchy.
```

#### 3. L3 Cache - Level 3 Cache / LLC - Last-Level Cache

**L3 cache** means **Level 3 cache**. In many multicore SoCs, Level 3 cache is larger, slower than Level 2 cache and shared among multiple cores or clusters. It may also be called **LLC - Last-Level Cache** if it is the final cache level before the memory controller and main memory.

Why Level 3 cache is useful:

- It reduces traffic to off-die Dynamic Random Access Memory.
- It allows shared data to stay on chip when several cores use it.
- It can reduce memory-controller contention.
- It can improve energy efficiency because on-chip cache access is usually cheaper than going off chip.
- It helps multicore performance because not every Level 2 miss must immediately become a DRAM access.

Level 3 cache is not present in every SoC. Small microcontroller-style SoCs may have no Level 3 cache. High-performance application processors, server SoCs and complex multicore SoCs are more likely to use a shared last-level cache.

#### Cache Level Summary

| Cache level | Full form | Usual location | Size trend | Speed trend | Main role |
|---|---|---|---|---|---|
| L1 I-cache | Level 1 Instruction cache | Inside/near core frontend | Smallest | Fastest | Fast instruction fetch |
| L1 D-cache | Level 1 Data cache | Inside/near load-store path | Smallest | Fastest | Fast load/store data access |
| L2 cache | Level 2 cache | Core or cluster level | Medium | Slower than Level 1 cache | Catch Level 1 misses |
| L3 cache / LLC | Level 3 cache / Last-Level Cache | Shared system/cluster level | Largest cache | Slower than Level 2 cache | Reduce Dynamic Random Access Memory traffic and support sharing |

<a id="topic-2-cache-internals"></a>

### Cache Internals: Lines, Tags, Hits And Misses

To understand cache, remember that cache stores **blocks**, not isolated variables. A block stored in cache is called a **cache line**.

When the CPU sends an address to cache, the cache divides the address conceptually into:

```text
Tag | Index | Offset
```

- **Tag** identifies which memory block is stored.
- **Index** selects the cache set or place where the cache should look.
- **Offset** selects the exact byte/word inside the cache line.

Each cache line normally has metadata:

- **Valid bit**: says whether the cache line contains meaningful data.
- **Dirty bit**: says whether the line was modified in cache and must be written back before replacement.
- **Tag bits**: identify the memory block.
- sometimes protection, coherency, parity or Error Correction Code bits.

#### What Happens On A Cache Hit

A **cache hit** happens when the requested address is already present in the cache and the valid bit is set.

Flow:

```text
CPU - Central Processing Unit sends address.
Cache checks index and tag.
Tag matches and valid bit is set.
Cache returns data quickly.
CPU continues with little or no stall.
```

This is the fast case. A high hit rate is valuable because most memory accesses are served close to the processor.

#### What Happens On A Cache Miss

A **cache miss** happens when the requested cache line is not present in the cache.

Flow:

```text
CPU - Central Processing Unit sends address.
Cache checks index and tag.
Requested line is absent.
Cache requests the line from lower memory level.
CPU may stall, or a nonblocking cache may continue with other work.
Lower memory returns the line.
Cache refills the line.
CPU receives the requested data.
```

The extra delay is called **miss penalty**. Miss penalty may include Level 2 cache access, Level 3 cache access, interconnect delay, memory-controller scheduling and Dynamic Random Access Memory timing.

This is why cache gives good **average** performance but not always predictable worst-case timing.

#### Cache Replacement

If the cache set is full and a new line must be inserted, the cache must remove an old line. This is called **eviction** or **replacement**.

Replacement policy decides which line is removed. Examples:

- **LRU - Least Recently Used**: removes the line not used for the longest time.
- **Pseudo-LRU - Pseudo Least Recently Used**: cheaper approximation of Least Recently Used.
- **Random replacement**: chooses a line randomly.

Replacement matters because a poor replacement decision can increase misses.

#### Cache Write Policies

When the CPU - Central Processing Unit writes data, the cache must decide how lower memory is updated.

**Write-through cache**:

- Write updates the cache and also immediately writes lower memory.
- Simpler for correctness.
- More lower-memory traffic.

**Write-back cache**:

- Write updates only the cache first.
- The line becomes **dirty**.
- Lower memory is updated later when the line is evicted or explicitly cleaned.
- Better for reducing traffic, but needs dirty bits and cache maintenance/coherency handling.

**Write-allocate**:

- On a write miss, bring the cache line into cache, then write it.
- Useful when nearby data may be accessed again.

**No-write-allocate**:

- On a write miss, send the write to lower memory without loading the line into cache.
- Useful for streaming writes that may not be reused.

#### Cache Associativity

**Associativity** means how many possible places a memory block can occupy in the cache.

| Cache organization | Meaning | Advantage | Limitation |
|---|---|---|---|
| Direct-mapped cache | Each memory block has only one possible place | Simple, fast, lower power | More conflict misses |
| Set-associative cache | Each block can go into one of several ways in a set | Common practical balance | More tag comparisons |
| Fully associative cache | Block can go anywhere in cache | Fewest conflict misses | Expensive for large caches |

Associativity exists because the cache must be searched quickly. More flexibility reduces conflicts, but hardware becomes larger and more power-hungry.

#### Cache, Average Memory Access Time And Predictability

A common cache performance expression is:

```text
AMAT = hit time + miss rate x miss penalty
```

**AMAT** means **Average Memory Access Time**.

Meaning:

- **hit time**: time to access cache when data is present,
- **miss rate**: fraction of accesses that miss,
- **miss penalty**: extra delay to fetch missing data from lower memory.

Cache improves average memory access time when hit rate is high. But cache can be difficult for real-time systems because one access may be a hit and another may be a miss. That difference can change worst-case execution time.

<a id="topic-2-scratchpad-deep"></a>

### Scratchpad Memory In Depth

**Scratchpad memory** is a software-managed local memory, usually implemented as on-die **SRAM - Static Random Access Memory**. It is a real hardware memory block inside the SoC, not just a software idea.

The key difference from cache:

```text
Cache: hardware automatically decides what to store.
Scratchpad: software/compiler/firmware decides what to store.
```

Scratchpad memory has normal addresses in the memory map. If software reads or writes a scratchpad address, it directly accesses that local memory. There are no cache tags, no cache hit/miss decision, no automatic cache replacement and no automatic line refill from lower memory.

How data gets into scratchpad:

- the linker places selected code or data sections there,
- startup firmware copies critical data into it,
- software explicitly copies buffers into it,
- a Direct Memory Access engine moves blocks between Dynamic Random Access Memory and scratchpad,
- a compiler/runtime system may manage scratchpad placement for predictable workloads.

Why scratchpad is used:

- access time is more predictable than cache,
- it avoids cache miss uncertainty,
- it reduces traffic on shared interconnect and external memory,
- it gives high local bandwidth to a processor, Digital Signal Processor or accelerator,
- it is useful for data that is known to be important before execution.

Typical scratchpad contents:

- audio filter coefficients,
- video tiles,
- neural-network activation tiles,
- packet descriptors,
- temporary matrix blocks,
- real-time control variables,
- communication buffers between processor and accelerator.

Example:

```text
An AI accelerator processes an image tile.
The tile is copied from DRAM - Dynamic Random Access Memory into local scratchpad.
The accelerator repeatedly reads the tile from scratchpad.
After processing, the result is copied back to DRAM - Dynamic Random Access Memory.
```

This is better than repeatedly accessing off-die Dynamic Random Access Memory because local scratchpad has lower latency, higher local bandwidth and lower energy per access.

Limitations of scratchpad:

- software must manage placement,
- wrong placement can waste limited local memory,
- explicit copying adds programming complexity,
- shared data may require synchronization,
- capacity is limited because on-die SRAM is expensive.

Exam line:

```text
Scratchpad memory trades automatic hardware management for predictable software-controlled access.
```

<a id="topic-2-tcm-deep"></a>

### TCM - Tightly Coupled Memory In Depth

**TCM** means **Tightly Coupled Memory**. It is low-latency on-die memory placed very close to a processor and connected through a direct or dedicated path. It is usually implemented using Static Random Access Memory.

TCM is physical hardware inside the SoC. It is not a cache and not a register file. It is a memory block with an address range, ports and timing behavior. The processor can access it with predictable low latency.

Common types:

- **ITCM - Instruction Tightly Coupled Memory**: stores time-critical instructions.
- **DTCM - Data Tightly Coupled Memory**: stores time-critical data.

Why TCM exists:

- some code must execute with predictable timing,
- interrupt service routines may need very fast response,
- safety-critical control loops cannot tolerate random cache misses,
- external memory may be unavailable during early boot or low-power transitions,
- real-time software needs known worst-case access time.

What is placed in Instruction Tightly Coupled Memory:

- interrupt handlers,
- exception handlers,
- boot routines,
- real-time control loops,
- safety-critical code,
- small kernels that must not suffer instruction cache misses.

What is placed in Data Tightly Coupled Memory:

- real-time stacks,
- control variables,
- sensor samples,
- motor-control data,
- small lookup tables,
- buffers used by deterministic routines.

How TCM differs from cache:

```text
Cache stores copies of memory blocks automatically.
TCM is directly addressed memory.

Cache can hit or miss.
TCM access is normally fixed-latency if the path is not contended.

Cache improves average performance.
TCM improves predictable worst-case timing.
```

TCM is often controlled through the linker script and memory map. For example, the embedded software project may place `.isr_vector` and `.fast_text` sections into Instruction Tightly Coupled Memory, and `.fast_data` or real-time stack sections into Data Tightly Coupled Memory.

Important beginner point:

```text
TCM does not magically contain critical code.
The SoC provides the hardware memory.
The software build system or firmware must place/copy the right code and data there.
```

Limitations of TCM:

- small capacity,
- consumes silicon area,
- usually local to one processor or cluster,
- less flexible for large shared data,
- software must decide what belongs there,
- verification must check address mapping and boot/copy behavior.

<a id="topic-2-cache-scratchpad-tcm"></a>

### Cache Vs Scratchpad Vs TCM

These three are easy to confuse because all are fast on-die memories. The difference is mainly **who controls placement** and **what timing behavior is expected**.

| Point | Cache | Scratchpad memory | TCM - Tightly Coupled Memory |
|---|---|---|---|
| Full meaning | Hardware-managed copy memory | Software-managed local SRAM | Processor-close deterministic memory |
| Physical nature | SRAM arrays plus tag/control logic | SRAM memory block | SRAM memory block close/directly connected to CPU |
| Who decides contents? | Cache hardware | Software/compiler/firmware/DMA | Software/linker/firmware |
| Addressing | Uses normal memory addresses but stores copies internally | Direct memory-map address range | Direct memory-map address range |
| Tags needed? | Yes | No | No |
| Hit/miss behavior? | Yes | No cache hit/miss | No cache hit/miss |
| Main strength | Good average performance | Software-controlled locality | Predictable low-latency CPU access |
| Main weakness | Misses create timing variation | Programmer/compiler complexity | Small and processor-local |
| Best use | General-purpose programs | Known hot data, tiles, buffers | Interrupts, real-time code/data |
| Exam phrase | Reduces Average Memory Access Time | Avoids cache unpredictability | Improves worst-case timing |

Memory hierarchy usually uses all of them where appropriate:

```text
General code/data -> cache.
Known accelerator/DSP working buffers -> scratchpad.
Critical real-time code/data -> TCM.
Large program/data -> off-die DRAM.
```

<a id="topic-2-on-die"></a>

### SoC On-Die Memory Systems

**SoC on-die memory system** means all memory blocks fabricated inside the SoC die and connected to processors, accelerators, interconnects and peripherals.

It is a physical hardware system. It may include:

- hard memory macros inserted during physical design,
- compiled Static Random Access Memory or Read Only Memory blocks,
- cache arrays inside or near processor cores,
- local memories near accelerators,
- buffers near input/output controllers,
- boot Read Only Memory,
- configuration or security storage.

On-die memory may be **centralized** or **distributed**.

#### Centralized On-Die Memory

In centralized memory, one memory block is shared by many SoC masters.

Example:

```text
CPU, DMA and accelerator all access one shared SRAM through an interconnect.
```

Advantages:

- easier sharing,
- simpler memory map,
- better capacity utilization,
- one common storage pool.

Disadvantages:

- contention can occur,
- arbitration is needed,
- access latency may increase,
- bandwidth may be limited by shared ports.

#### Distributed On-Die Memory

In distributed memory, multiple smaller memories are placed near the blocks that use them.

Example:

```text
CPU has TCM.
Video accelerator has local frame buffer.
Network block has packet FIFO.
DSP has local scratchpad.
```

Advantages:

- lower local latency,
- higher parallel bandwidth,
- less interconnect traffic,
- better real-time behavior.

Disadvantages:

- harder sharing,
- software placement becomes important,
- unused memory in one block may not help another block,
- address map and verification become more complex.

#### Common On-Die Memory Blocks

##### 1. Register File

A **register file** is the small, very fast storage inside a processor or accelerator. It stores operands and results used directly by execution units such as the Arithmetic Logic Unit or Floating-Point Unit.

Why it is there:

- instructions need source operands,
- results must be stored before later instructions use them,
- accessing registers is much faster than accessing memory,
- the instruction set architecture exposes many registers to software.

Example:

```text
ADD R3, R1, R2
```

Here `R1`, `R2` and `R3` are registers inside the register file.

##### 2. Cache Memory

**Cache memory** is fast **SRAM - Static Random Access Memory** based memory used to store copies of recently used instructions or data from lower memory levels. In hardware, a cache is not just a plain memory array. It contains data storage, tag storage, valid bits, dirty bits, comparators, replacement logic and control logic.

Do not think of cache as a separate software buffer. The processor sends normal instruction fetch, load and store addresses. The cache hardware checks whether those addresses are already present in its SRAM arrays. If present, the access is a **cache hit**. If absent, the access is a **cache miss** and the cache must fetch the missing cache line from a lower memory level.

Common cache levels:

- **L1 cache - Level 1 cache**: closest to the core, smallest and fastest. Often split into **I-cache - Instruction cache** and **D-cache - Data cache**.
- **L2 cache - Level 2 cache**: larger and slower than Level 1 cache; catches many Level 1 misses.
- **L3 cache - Level 3 cache**: often shared among cores, larger but slower than Level 2 cache; may also be the **LLC - Last-Level Cache**.

Why it is there:

- reduces average memory latency,
- reduces external memory traffic,
- uses locality,
- hides some Dynamic Random Access Memory delay.

Cache is hardware-managed, so software usually does not explicitly move every item into cache. The cache controller uses tags, valid bits, replacement policy and cache lines. This automatic management is very useful for general-purpose software, but the hit/miss behavior can make exact timing harder to predict in real-time systems.

##### 3. SRAM - Static Random Access Memory

**SRAM - Static Random Access Memory** is a fast volatile memory. It is called static because it keeps its data as long as power is supplied and does not need periodic refresh.

In SoCs, SRAM is used for:

- caches,
- on-chip RAM,
- scratchpad,
- TCM,
- First In First Out queues,
- packet buffers,
- lookup tables,
- accelerator local buffers.

Why SRAM is common on-die:

- it integrates well with normal logic processes,
- it is fast,
- it can be accessed with predictable timing,
- it is suitable for small and medium memory arrays.

Limitation:

- SRAM cell area is much larger than Dynamic Random Access Memory cell area, so large SRAM is expensive.

##### 4. ROM - Read Only Memory / Boot ROM

**ROM - Read Only Memory** stores fixed data or code. **Boot ROM** stores the first code executed when the SoC comes out of reset.

Boot ROM is important because when power is applied:

1. The processor starts at a reset address.
2. It needs valid code immediately.
3. External memory may not be initialized yet.
4. The memory controller may not be configured yet.
5. Secure boot checks may need trusted code.

So Boot ROM is usually on-die and available without external initialization.

What Boot ROM may do:

- set up clocks,
- initialize basic hardware,
- configure memory controller,
- load firmware from Flash or external storage,
- verify signatures for secure boot,
- jump to the next boot stage.

##### 5. Scratchpad Memory

**Scratchpad memory** is software-managed on-die **SRAM - Static Random Access Memory**. It is a physical memory block inside the System on Chip, mapped to a specific address range.

It is called software-managed because hardware does not automatically fill it like a cache. Software, compiler, firmware or a **DMA - Direct Memory Access** engine decides what data or code should be placed there. When the processor accesses a scratchpad address, it is directly reading or writing that local SRAM. There is no tag comparison, no cache line refill and no replacement policy.

Why it is there:

- gives predictable access time,
- avoids cache miss uncertainty,
- stores real-time code/data,
- reduces shared memory traffic,
- helps accelerators and Digital Signal Processors.

Scratchpad is especially useful when the programmer already knows which data will be reused. For example, an image-processing accelerator may copy one tile from off-die Dynamic Random Access Memory into scratchpad, process that tile many times locally, and then write the result back. This reduces repeated slow external memory accesses.

Example:

```text
Audio filter coefficients placed in scratchpad.
Motor-control interrupt routine placed in scratchpad.
AI accelerator tile data placed in local scratchpad.
```

##### 6. TCM - Tightly Coupled Memory

**TCM - Tightly Coupled Memory** is low-latency on-die memory directly connected to a processor, normally used for deterministic instruction or data access.

TCM is also real hardware inside the SoC. It is not a cache. It does not automatically store recently used memory blocks. Instead, Tightly Coupled Memory occupies a defined address range, and software/linker scripts place critical code or data into that range.

Types:

- **ITCM - Instruction Tightly Coupled Memory**: stores time-critical instructions.
- **DTCM - Data Tightly Coupled Memory**: stores time-critical data.

Why TCM is there:

- interrupt handlers must execute quickly,
- real-time control code needs predictable timing,
- cache misses are not acceptable for some deadlines,
- direct CPU connection reduces access delay.

Typical Instruction Tightly Coupled Memory contents are interrupt vectors, interrupt service routines, exception handlers and small real-time loops. Typical Data Tightly Coupled Memory contents are real-time stacks, control variables, sensor samples, lookup tables and buffers used by deterministic code.

Important distinction:

```text
Cache improves average performance.
TCM improves predictable worst-case access.
```

##### 7. FIFO - First In First Out

**FIFO - First In First Out** is a queue memory. Data enters at one end and leaves in the same order.

Why it is there:

- connects producer and consumer blocks,
- absorbs temporary rate mismatch,
- supports streaming data,
- helps interfaces running at different speeds,
- can help clock-domain crossing when designed as asynchronous FIFO.

Example:

```text
Camera interface writes pixels into FIFO.
Image processor reads pixels from FIFO.
```

##### 8. Buffers

A **buffer** is temporary memory used to hold data while another block is not ready or while data is being processed.

SoC buffers include:

- packet buffers,
- audio buffers,
- video line buffers,
- display frame buffers,
- Direct Memory Access descriptors,
- accelerator input/output buffers.

Why buffers are there:

- data producers and consumers often run at different rates,
- bursts must be smoothed,
- external memory latency must be hidden,
- data may need to be stored between processing stages.

##### 9. Lookup Tables

A **lookup table** is memory that stores precomputed values.

Why it is there:

- replaces repeated computation with memory read,
- improves speed,
- reduces energy for complex functions,
- useful in Digital Signal Processor, graphics, communication and security blocks.

Example:

```text
Sine/cosine table.
CRC table.
Encryption substitution table.
Activation-function table in an AI accelerator.
```

##### 10. eFuse / OTP / Small Non-Volatile Memory

Some SoCs contain small one-time or limited-write non-volatile memories.

**eFuse** means electronically programmable fuse. **OTP** means One-Time Programmable memory.

They may store:

- chip identity,
- trim values,
- security keys,
- boot configuration,
- feature enable/disable bits,
- calibration data.

These are not large data memories. They are small but important for manufacturing, security and configuration.

<a id="topic-2-on-die-vs-off-die"></a>

### On-Die Vs Off-Die Memory

**On-die memory** is located inside the SoC silicon die. **Off-die memory** is outside the SoC die, either in the same package, on the printed circuit board or in a separate memory device.

| Point | On-Die Memory | Off-Die Memory |
|---|---|---|
| Physical location | Same silicon die as SoC | Outside SoC die |
| Typical technology | SRAM - Static Random Access Memory, ROM - Read Only Memory, register file, cache, TCM - Tightly Coupled Memory | DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory, LPDDR - Low-Power Double Data Rate, Flash, eMMC - embedded MultiMediaCard, UFS - Universal Flash Storage |
| Latency | Low | Higher |
| Bandwidth | High local bandwidth possible | Limited by memory interface, pins and controller |
| Capacity | Limited | Much larger |
| Cost per bit | High | Lower |
| Power per access | Often lower for small local access | Higher due to I/O and longer paths |
| Predictability | Can be predictable | DRAM timing and contention can vary |
| Main use | cache, boot code, real-time data, buffers | main memory, large program/data storage |

#### Why On-Die Memory Is Fast

On-die memory is fast because:

- wires are shorter,
- the interface can be wide,
- no package pins are needed for local access,
- timing can be optimized with the logic,
- local memories can be placed near the block that uses them.

#### Why On-Die Memory Is Limited

On-die memory is limited because:

- memory cells occupy silicon area,
- large die area increases cost,
- larger die can reduce yield,
- more memories increase leakage power,
- memories need testing, repair and verification,
- large on-die memory may create routing and timing challenges.

#### Why Off-Die DRAM Is Still Used

Large applications need memory capacity that is too big for practical on-die SRAM.

Off-die **DRAM - Dynamic Random Access Memory** is used because it offers:

- high density,
- large capacity,
- lower cost per bit,
- standard memory components,
- flexible product configurations.

But DRAM needs:

- memory controller,
- refresh,
- timing management,
- board/package interface,
- signal integrity care,
- power management.

Exam line:

```text
On-die memory is chosen for speed and predictability.
Off-die memory is chosen for large capacity and lower cost per bit.
```

<a id="topic-2-tradeoffs"></a>

### On-Die Memory Design Tradeoffs

Memory design is about tradeoffs. A strong exam answer should not say "faster memory is always better." Faster memory can cost more area, power and design complexity.

#### 1. Latency

**Latency** is the time between making a memory request and receiving data.

Low latency is important for:

- instruction fetch,
- load/store operations,
- interrupt handlers,
- real-time control,
- small random accesses.

Registers, Level 1 cache and TCM - Tightly Coupled Memory have low latency. Off-die DRAM - Dynamic Random Access Memory has higher latency.

#### 2. Bandwidth

**Bandwidth** is the amount of data transferred per second.

High bandwidth is important for:

- video,
- camera,
- graphics,
- AI accelerators,
- networking,
- memory copy,
- multicore systems.

Bandwidth can be improved by:

- wider memory interface,
- more banks,
- more ports,
- distributed memories,
- local buffers,
- burst transfers,
- parallel access paths.

But wider buses and multi-port memories increase area and power.

#### 3. Capacity

**Capacity** is how much data a memory can store.

On-die memory has limited capacity because chip area is expensive. Off-die DRAM and Flash provide much larger capacity.

Capacity decisions include:

- cache size,
- SRAM size,
- Boot ROM size,
- FIFO depth,
- scratchpad size,
- buffer size.

Too little memory causes stalls or overflows. Too much memory wastes area and power.

#### 4. Area

**Area** means silicon area consumed by memory. In modern SoCs, memory arrays can occupy a large fraction of die area.

Area matters because:

- larger die costs more,
- yield may decrease,
- routing becomes harder,
- leakage power may increase.

This is why designers avoid putting all main memory on the SoC die.

#### 5. Power

Memory consumes:

- **dynamic power** during reads/writes,
- **leakage power** while powered but idle,
- extra power for large decoders, sense amplifiers and long wires.

Low-power memory design may use:

- clock gating,
- power gating,
- retention mode,
- banking,
- sleep mode,
- low-voltage operation,
- smaller local memories to reduce external traffic.

#### 6. Determinism

**Determinism** means predictable access timing.

Cache has variable timing because of hits and misses. TCM and scratchpad can be more deterministic because software places critical code/data there and access paths are more direct.

Determinism is important for:

- automotive control,
- motor control,
- industrial control,
- real-time operating systems,
- interrupt response,
- safety-critical SoCs.

#### 7. Ports And Parallel Access

A **memory port** is an access interface to a memory.

Common types:

- **single-port memory**: one access at a time,
- **dual-port memory**: two accesses can occur in the same cycle under allowed conditions,
- **multi-port memory**: multiple read/write accesses, usually expensive.

More ports improve concurrency but increase area, power and timing complexity.

Example:

```text
CPU and DMA both need the same SRAM.
If the SRAM is single-port, they must take turns.
If the SRAM is dual-port, some parallel access is possible.
```

#### 8. Physical Placement

On-die memory should be placed near the blocks that use it frequently.

Why placement matters:

- long wires add delay,
- long wires consume power,
- congestion can make timing closure harder,
- local placement improves bandwidth.

For example, TCM near the CPU makes sense. A packet buffer near a network interface makes sense. A display line buffer near display logic makes sense.

#### 9. Reliability And Protection

Large memories can suffer from bit errors. SoCs may use:

- **parity** for error detection,
- **ECC - Error Correction Code** for detection and correction,
- redundancy and repair for manufacturing defects,
- Built-In Self-Test for memory test.

Reliability is especially important in automotive, aerospace, server, medical and safety applications.

#### 10. Cache Coherency And Sharing

When multiple processors or Direct Memory Access engines access shared memory, the system must ensure that they see correct data.

Example:

```text
CPU writes data into cache.
DMA reads memory.
If cache data was not written back, DMA may read old memory data.
```

This is why SoCs need cache maintenance, coherent interconnects, non-cacheable regions or carefully managed buffers.

<a id="topic-2-memory-map"></a>

### Memory Map And Access

A **memory map** defines which address ranges belong to which memory or peripheral.

Example:

```text
0x0000_0000 - 0x0000_FFFF    Boot ROM
0x1000_0000 - 0x1001_FFFF    On-chip SRAM
0x2000_0000 - 0x2000_7FFF    TCM
0x4000_0000 - 0x4000_FFFF    Peripheral registers
0x8000_0000 - 0xBFFF_FFFF    External DRAM
```

The memory map is important because software does not directly see physical blocks. Software sees addresses. The processor, bus/interconnect, Memory Management Unit, address decoder and memory controller decide where the access goes.

#### Memory-Mapped I/O

**Memory-mapped I/O** means peripheral control registers are placed in the address space.

Example:

```text
write 1 to UART control register address -> UART starts transmission
read status register address -> software checks if UART is ready
```

These addresses look like memory accesses to the processor, but the target is a hardware register inside a peripheral.

#### Virtual Memory, MMU And TLB

Some SoCs use virtual memory.

**MMU - Memory Management Unit** translates virtual addresses generated by software into physical addresses used by hardware.

**TLB - Translation Lookaside Buffer** caches recent address translations so translation is faster.

Why this matters:

- separates processes,
- protects memory,
- supports operating systems,
- allows virtual address spaces larger or different from physical layout,
- controls cacheability and access permissions.

Small microcontroller-style SoCs may not use a full MMU. They may use an **MPU - Memory Protection Unit** instead, or no address translation at all.

<a id="topic-2-final-answer"></a>

### Final Exam-Ready Answer

Memory design in a System on Chip means designing the storage hierarchy that holds instructions, data, boot code, temporary buffers, lookup tables and communication queues for processors, accelerators and peripherals. It is a major SoC design issue because processors and accelerators are useful only if the memory system can supply data at the required latency and bandwidth. A high-frequency processor can still perform poorly if it waits for cache misses, shared memory contention or external Dynamic Random Access Memory access.

A SoC memory system is normally organized as a hierarchy. The closest and fastest storage consists of processor registers, followed by Level 1 cache, Tightly Coupled Memory or scratchpad memory, then Level 2 cache and Level 3 cache, on-chip Static Random Access Memory and Read Only Memory, then large off-chip Dynamic Random Access Memory and non-volatile storage. This hierarchy exists because one memory technology cannot simultaneously provide maximum speed, huge capacity, low area, low power and low cost. Small memories near the processor are fast but expensive per bit; large memories farther away are cheaper per bit but slower.

On-die memory means memory physically fabricated on the same silicon die as the SoC logic. It is a real hardware block, not software. It may be implemented as register files, cache arrays, Static Random Access Memory macros, Boot Read Only Memory, scratchpad memory, Tightly Coupled Memory, First In First Out queues, packet buffers, accelerator local buffers, lookup tables or small non-volatile storage. These memories are connected to processor cores, Direct Memory Access engines, accelerators, peripherals and interconnects.

On-die memory is used because it gives low latency, high local bandwidth and lower access energy compared with going off chip. For example, a Boot Read Only Memory is available immediately after reset, Tightly Coupled Memory gives deterministic access for interrupt routines, and caches reduce average memory access time by keeping recently used instructions and data close to the processor. Distributed on-die memories near accelerators and peripherals also reduce interconnect traffic and allow several blocks to access local storage in parallel.

However, on-die memory is limited. Static Random Access Memory is fast and convenient to integrate, but it consumes much more area per bit than Dynamic Random Access Memory. Large memory arrays increase die size, cost, leakage power and testing effort. Therefore, SoCs normally combine limited on-die memory with large off-die memories such as Double Data Rate Dynamic Random Access Memory or Low-Power Double Data Rate Dynamic Random Access Memory. On-die memory is chosen for speed, predictability and local bandwidth; off-die memory is chosen for large capacity and lower cost per bit.

The design tradeoffs in SoC memory include latency, bandwidth, capacity, area, power, determinism, number of ports, physical placement, reliability and sharing. Cache gives good average performance but can have unpredictable miss delays. Scratchpad memory and Tightly Coupled Memory give more predictable timing but require software or compiler management. Multi-port memories improve parallel access but increase area and power. Shared memories improve flexibility but need arbitration and sometimes cache coherency. Therefore, good SoC memory design balances performance, power, area and cost according to the application requirements.

<a id="topic-2-short-answer"></a>

### Short 10-Mark Answer

Memory design in SoC is the design of the memory hierarchy used to store instructions, data, boot code and temporary buffers. It is important because processor and accelerator performance depends heavily on memory latency and bandwidth.

An SoC normally uses a hierarchy: **CPU - Central Processing Unit** registers, **L1 cache - Level 1 cache**, **L2 cache - Level 2 cache**, **L3 cache - Level 3 cache**, **TCM - Tightly Coupled Memory** or scratchpad memory, on-chip **SRAM - Static Random Access Memory** / **ROM - Read Only Memory**, off-chip **DRAM - Dynamic Random Access Memory** and non-volatile storage. This hierarchy balances speed, capacity, cost and power.

On-die memory is memory fabricated on the same silicon die as the SoC logic. Examples are register files, cache Static Random Access Memory, Boot Read Only Memory, scratchpad memory, Tightly Coupled Memory, **FIFOs - First In First Out queues**, packet buffers and accelerator local memory. It is fast and energy-efficient because it is close to the logic, but it is limited in size because silicon area is expensive.

Off-die memory such as DDR DRAM or LPDDR gives large capacity at lower cost per bit, but has higher latency and requires a memory controller. Hence SoCs use on-die memory for speed, boot, buffering and real-time access, and off-die memory for large program/data storage.

Important tradeoffs are latency, bandwidth, capacity, area, power, determinism, port count, placement and reliability. Cache improves average performance, while scratchpad or TCM improves predictable timing. A good SoC memory system balances these tradeoffs according to application needs.

<a id="topic-2-technical-words"></a>

### Technical Words To Use In Exam

- **SoC - System on Chip** (write this because the answer is about memory as an SoC component.)
- **Memory hierarchy** (write this because memory design is layered, not a single block.)
- **On-die memory** (write this because the question specifically asks SoC on-die memory systems.)
- **Off-die memory** (write this because you must contrast on-chip storage with external memory.)
- **SRAM - Static Random Access Memory** (write this because most on-die RAM/cache memories are SRAM-based.)
- **DRAM - Dynamic Random Access Memory** (write this because large main memory is often off-die DRAM.)
- **ROM - Read Only Memory** (write this because boot code is often stored in on-die ROM.)
- **Boot ROM - Boot Read Only Memory** (write this because reset and boot behavior are important in SoCs.)
- **Cache** (write this because cache reduces average memory access time.)
- **L1 cache - Level 1 cache** (write this because it is the closest, fastest cache near the processor core.)
- **I-cache - Instruction cache** (write this because instruction fetch performance depends on it.)
- **D-cache - Data cache** (write this because load/store performance depends on it.)
- **L2 cache - Level 2 cache** (write this because it catches Level 1 cache misses.)
- **L3 cache - Level 3 cache** (write this because it may be the shared system or last-level cache.)
- **LLC - Last-Level Cache** (write this because it is the final cache level before main memory in many SoCs.)
- **Cache line** (write this because cache transfers/stores blocks, not just isolated variables.)
- **Tag / valid bit / dirty bit** (write this because these explain how cache knows whether data is present and modified.)
- **Cache hit / cache miss** (write this because cache timing depends on whether data is present.)
- **Write-back cache / write-through cache** (write this because cache write policy affects memory traffic and coherency.)
- **Associativity** (write this because direct-mapped and set-associative organization affects miss rate.)
- **AMAT - Average Memory Access Time** (write this because it links hit time, miss rate and miss penalty.)
- **TCM - Tightly Coupled Memory** (write this because it gives deterministic low-latency access.)
- **ITCM - Instruction Tightly Coupled Memory** (write this because critical instructions may be placed there.)
- **DTCM - Data Tightly Coupled Memory** (write this because critical data may be placed there.)
- **Scratchpad memory** (write this because it is software-managed on-die SRAM.)
- **FIFO - First In First Out** (write this because SoC interfaces often need streaming buffers.)
- **DMA - Direct Memory Access** (write this because DMA engines access memory without CPU copying every byte.)
- **Memory map** (write this because software accesses memories through address ranges.)
- **MMU - Memory Management Unit** (write this because rich operating systems use address translation/protection.)
- **TLB - Translation Lookaside Buffer** (write this because it accelerates virtual-to-physical address translation.)
- **Latency** (write this because memory access delay controls stalls.)
- **Bandwidth** (write this because data-heavy SoCs need high transfer rate.)
- **Capacity** (write this because on-die and off-die memories differ mainly in size.)
- **PPA - Power, Performance, Area** (write this because memory design is a PPA tradeoff.)
- **Determinism** (write this because real-time systems need predictable memory timing.)
- **ECC - Error Correction Code** (write this because memory reliability is important in SoCs.)
- **Memory port** (write this because single-port/dual-port choices affect parallel access.)
- **Locality** (write this because cache effectiveness depends on temporal and spatial locality.)
- **Temporal locality** (write this because recently used instructions/data may be reused soon.)
- **Spatial locality** (write this because nearby addresses are often used soon.)

<a id="topic-2-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 230100.png](<images/Screenshot 2026-05-12 230100.png>) contains the syllabus headline **Memory Design-Overview, SOC (On-Die) Memory Systems**.
2. **Syllabus/CLO image**: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) maps this topic to the SoC Components section and CLO 2.

#### Figure 1: Memory Hierarchy

Draw this diagram for any memory overview answer:

```text
Fast / small / expensive per bit

        CPU - Central Processing Unit registers
              |
        L1 I-cache - Level 1 Instruction cache /
        L1 D-cache - Level 1 Data cache
              |
        TCM - Tightly Coupled Memory / scratchpad memory
              |
        L2 cache - Level 2 cache
              |
        L3 cache - Level 3 cache / system cache
              |
        On-die SRAM - Static Random Access Memory /
        ROM - Read Only Memory / buffers
              |
        Off-die DRAM - Dynamic Random Access Memory /
        LPDDR - Low-Power Double Data Rate
              |
        Flash / eMMC - embedded MultiMediaCard /
        UFS - Universal Flash Storage

Slow / large / cheaper per bit
```

Why this figure is useful: it shows the main memory design principle: closer memory is faster but smaller, while farther memory is larger but slower.

#### Figure 2: On-Die Memory Inside SoC

```text
                      System on Chip die
+-----------------------------------------------------------+
| CPU - Central Processing Unit core                        |
| + registers + Level 1 cache + TCM - Tightly Coupled Memory |
|                                                           |
| Level 2 cache / system cache                              |
|                                                           |
| Interconnect / Bus / Network on Chip                      |
|                                                           |
| On-chip SRAM     Boot ROM     FIFO/buffers     Accelerator |
|                                                           |
| Memory controller -----> Off-die DRAM - Dynamic Random     |
|                          Access Memory                     |
+-----------------------------------------------------------+
```

Why this figure is useful: it makes clear that on-die memories are physical hardware blocks inside the SoC, while large DRAM is usually outside and reached through a memory controller.

#### Figure 3: Cache Vs TCM - Tightly Coupled Memory / Scratchpad

```text
Cache:
CPU request -> cache hit = fast
            -> cache miss = fetch from lower memory
Hardware decides what stays in cache.

TCM - Tightly Coupled Memory / Scratchpad:
CPU request -> fixed local memory access
Software/compiler decides what is placed there.
```

Why this figure is useful: it explains why cache improves average performance while TCM/scratchpad improves predictable timing.

#### Figure 4: Memory Map View

```text
Processor address space

0x0000_0000  Boot ROM
0x1000_0000  On-chip SRAM
0x2000_0000  TCM - Tightly Coupled Memory
0x4000_0000  Peripheral registers
0x8000_0000  External DRAM
```

Why this figure is useful: it connects physical memory blocks to the addresses used by software.

#### Figure 5: Centralized Vs Distributed On-Die Memory

```text
Centralized:
CPU + DMA + Accelerator ---> Shared SRAM

Distributed:
CPU - Central Processing Unit ---> TCM - Tightly Coupled Memory
DSP - Digital Signal Processor ---> local scratchpad
Network ---> packet FIFO
Accelerator ---> local buffer
```

Why this figure is useful: it shows two possible SoC memory organizations and explains why bandwidth, sharing and locality are design decisions.

---

<a id="topic-3"></a>

## Topic 3: Board-Based Off-Die Memory Systems, Simple DRAM And The Memory Array

<a id="topic-3-question"></a>

### Question

**Explain Board-based (Off-Die) Memory Systems, Simple DRAM and the Memory Array.**

<a id="topic-3-clo-mapping"></a>

### CLO Mapping

This topic belongs to **CLO 2: Describe SoC and its Components; Bus Architecture and Interconnection of SoC**.

Reason: This topic extends the SoC component discussion from **on-die memory** to **off-die memory**. It explains how an SoC connects to board-level memory devices and why the memory controller, package pins, board traces and DRAM chips are part of the complete SoC memory system. It also overlaps with CLO 3, because simple DRAM arrays and detailed DRAM timing are memory-design topics. In CLO 2, write it as a component/interconnection answer; in CLO 3, write it as a memory architecture/controller answer.

Detailed local PPT/book/web references are kept in [sources/CLO2_Topic3_sources.md](<sources/CLO2_Topic3_sources.md>).

<a id="topic-3-what-asking"></a>

### What The Question Is Asking

The examiner is asking three connected things:

1. What **board-based memory** means.
2. What **off-die memory** means.
3. Why SoCs use external memory instead of placing all memory on the die.
4. How the SoC connects to external memory through a memory controller, package and board.
5. What **DRAM - Dynamic Random Access Memory** is.
6. How a simple DRAM cell stores one bit.
7. How many DRAM cells are organized into a memory array using rows and columns.
8. What word lines, bit lines, row decoders, column decoders and sense amplifiers do.
9. Why DRAM needs refresh.
10. What happens during activate, read, write, precharge and refresh.

Exam answer order:

```text
Board/off-die memory definition -> physical connection ->
why external memory is used -> simple DRAM cell ->
DRAM memory array -> access sequence -> board-level issues -> final answer.
```

<a id="topic-3-main-explanation"></a>

### Main Explanation

**Board-based memory** means memory that is placed outside the SoC die, usually on the **PCB - Printed Circuit Board**, and connected to the SoC through package pins or solder balls and board traces. It is also called **off-die memory** because it is not fabricated on the same silicon die as the processor and SoC logic.

This is physical hardware.

The complete path looks like this:

```text
CPU / accelerator
      |
SoC interconnect
      |
memory controller inside SoC
      |
SoC package pins / balls
      |
PCB traces
      |
external DRAM chip or memory module
```

The SoC does not directly treat a board DRAM chip like a simple register. The processor issues a memory read or write request. The request travels through the SoC interconnect to the memory controller. The memory controller converts the request into DRAM commands and electrical signals. Those signals travel through the SoC package and PCB traces to the DRAM device.

Off-die memory is used because it provides much larger capacity than practical on-die SRAM. On-die SRAM is fast but expensive in silicon area. Off-die DRAM is slower and more complex to access, but it gives high capacity at lower cost per bit.

Beginner line:

```text
On-die memory is close and fast.
Board-based off-die memory is larger and cheaper per bit.
```

<a id="topic-3-board-based"></a>

### Board-Based Off-Die Memory Systems

A **board-based off-die memory system** contains the external memory hardware and all the connection structures required to communicate with it.

It includes:

- the SoC memory controller,
- the SoC package pins/balls,
- board traces on the Printed Circuit Board,
- external memory chips,
- power supply and decoupling capacitors,
- termination resistors or on-die termination,
- clock, command, address and data signals,
- sometimes memory modules such as DIMM or SoDIMM.

#### What Is Inside The SoC And What Is Outside?

| Part | Inside SoC die? | Meaning |
|---|---:|---|
| CPU core | Yes | Generates memory reads/writes indirectly through caches/interconnect |
| Cache | Yes | On-die SRAM copy of recently used memory |
| Interconnect / bus / NoC | Yes | Carries requests inside the SoC |
| Memory controller | Usually yes | Converts SoC transactions into DRAM commands |
| PHY - Physical Layer | Usually yes or package-adjacent IP | Drives/receives high-speed memory signals |
| Package pins/balls | Package boundary | Connect internal die pads to board |
| PCB traces | Outside die | Copper connections on board |
| DRAM chip/module | Outside die | Stores large program/data memory |

The **memory controller** is a hardware block, usually inside the SoC. It knows the DRAM protocol and timing rules. The **PHY - Physical Layer** is the electrical interface that sends and receives high-speed signals such as data and strobes.

#### Typical Off-Die Memories

Common off-die memories include:

- **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory**,
- **LPDDR - Low-Power Double Data Rate** memory for mobile SoCs,
- **GDDR - Graphics Double Data Rate** memory for graphics systems,
- **HBM - High Bandwidth Memory** in advanced packages,
- NAND Flash for mass storage,
- eMMC - embedded MultiMediaCard storage,
- UFS - Universal Flash Storage.

For this syllabus line, focus mainly on **DRAM**, especially SDRAM/DDR-style memory, because the topic says **Simple DRAM and the Memory Array**.

#### Board-Based Memory Interface Signals

A DDR-style off-die memory system uses several signal groups:

| Signal group | Full form / meaning | Purpose |
|---|---|---|
| CK | Clock | Timing reference for memory commands |
| CA | Command/Address | Carries command and address information |
| CS | Chip Select | Selects the target chip or rank |
| DQ | Data | Carries read/write data |
| DQS | Data Strobe | Timing strobe associated with data transfer |
| DM / DBI | Data Mask / Data Bus Inversion | Masks writes or improves signaling/noise depending on memory generation |
| ODT | On-Die Termination | Improves signal integrity by terminating signals inside the memory device |

You do not need to draw all pins in an exam unless asked. But you should write that off-die memory needs command, address, data, clock and control signals.

#### Channel, Rank, Bank, Row And Column

These terms are often confused, so keep them separate:

| Term | Meaning |
|---|---|
| Channel | Independent path between memory controller and memory devices |
| Rank | Group of DRAM chips selected together to form a wider data interface |
| Chip/device | Individual DRAM integrated circuit |
| Bank | Internal independent DRAM subarray inside a chip |
| Row | Horizontal group of cells selected by a word line |
| Column | Vertical selection from the active row through bit lines |

Simple relationship:

```text
Memory system
  -> channel
      -> rank
          -> DRAM chip
              -> bank
                  -> row
                      -> column
                          -> cell
```

<a id="topic-3-why-off-die"></a>

### Why Off-Die Memory Is Used

Off-die memory is used because many SoCs need far more memory than can be economically placed on the SoC die.

#### 1. Large Capacity

Applications such as operating systems, graphics, video, networking, AI and user applications may need megabytes or gigabytes of memory. Placing that much memory as on-die SRAM would make the SoC die too large and expensive.

#### 2. Lower Cost Per Bit

DRAM cells are much smaller than SRAM cells. A simple DRAM bit cell is often described as **1T1C - one transistor and one capacitor**. A typical SRAM cell uses more transistors. Therefore, DRAM provides higher density.

Exam line:

```text
DRAM is used for large main memory because it has high density and low cost per bit.
```

#### 3. Product Flexibility

The same SoC can be sold with different board memory sizes.

Example:

```text
Same SoC + 1 GB LPDDR for low-end product
Same SoC + 4 GB LPDDR for higher-end product
```

This is easier than fabricating a different SoC die for every memory capacity.

#### 4. Better Manufacturing Yield

Large dies are harder to manufacture with high yield. Keeping huge memory arrays off the SoC can reduce die size and improve yield.

#### 5. Suitable Process Technology

Logic transistors and dense DRAM cells are optimized differently. A normal SoC logic process is not always ideal for very dense DRAM. External DRAM chips are manufactured using DRAM-optimized processes.

#### 6. Upgrade And Repair

Board-level memory may be replaceable or configurable in some systems. Even when soldered, product variants can use different memory densities.

#### Main Disadvantages

Off-die memory is not free. It has disadvantages:

- higher latency,
- more energy per access,
- limited pins and bus width,
- signal integrity problems,
- need for memory controller and PHY,
- board routing complexity,
- timing calibration/training,
- possible contention among SoC masters.

So the real design choice is:

```text
Use on-die memory for speed, locality and real-time behavior.
Use off-die memory for large capacity and lower cost per bit.
```

<a id="topic-3-dram-cell"></a>

### Simple DRAM Cell

**DRAM - Dynamic Random Access Memory** stores each bit as electrical charge on a tiny capacitor. It is called **dynamic** because the charge leaks over time and must be periodically refreshed.

The simplest DRAM cell is called a **1T1C cell**:

```text
1T1C = one access transistor + one storage capacitor
```

Basic cell:

```text
             Word line
                |
                v
Bit line ----[ access transistor ]---- storage capacitor
                                             |
                                            GND
```

#### Meaning Of Each Part

| Part | Meaning | Role |
|---|---|---|
| Storage capacitor | Tiny capacitor | Stores charge representing 1 or 0 |
| Access transistor | Switch controlled by word line | Connects capacitor to bit line during access |
| Word line | Row-select signal | Turns on access transistors in one row |
| Bit line | Column data wire | Carries small voltage change to sense amplifier |
| Sense amplifier | Read/restore circuit | Detects and amplifies the tiny signal |

#### How One Bit Is Stored

In a simplified explanation:

```text
Charged capacitor   = logic 1
Discharged capacitor = logic 0
```

In real DRAM, the voltage difference can be small and must be sensed carefully.

#### Why DRAM Needs Refresh

The capacitor leaks charge over time. If not refreshed, a stored 1 may slowly lose charge and become unreadable.

Therefore, DRAM requires **REFRESH** operations.

Refresh means:

```text
read the stored charge -> amplify it -> write it back strongly
```

This is why DRAM is volatile and dynamic.

#### DRAM Read Is Destructive

A DRAM read disturbs the charge stored in the cell. The sense amplifier must restore the data after sensing it.

Important line:

```text
In DRAM, reading a cell requires sensing and restoring the stored charge.
```

This is different from a simple register or SRAM-style explanation where read does not normally require refresh.

#### Why DRAM Is Dense But Slower

DRAM is dense because each bit uses a small cell. But it is slower/complex because:

- the stored signal is small,
- sensing takes time,
- refresh is required,
- rows must be activated,
- banks must be precharged,
- access timing depends on row/bank state.

<a id="topic-3-memory-array"></a>

### DRAM Memory Array

A single DRAM cell stores only one bit. To build a useful memory, millions or billions of cells are arranged in a two-dimensional array of rows and columns.

Basic memory array:

```text
                 Bit lines / columns
              BL0   BL1   BL2   BL3
               |     |     |     |
WL0 -------- [C]---[C]---[C]---[C]
WL1 -------- [C]---[C]---[C]---[C]
WL2 -------- [C]---[C]---[C]---[C]
WL3 -------- [C]---[C]---[C]---[C]
               |     |     |     |
          Sense amplifiers / row buffer

WL = Word Line
BL = Bit Line
C  = DRAM cell
```

#### Rows

A **row** is selected by a word line. When a row is activated, the word line turns on the access transistors for all cells in that row.

Important point:

```text
DRAM usually opens an entire row, not just one bit.
```

#### Columns

A **column** is selected through bit lines and column selection logic. After a row is open, the column address selects which part of the active row is transferred to or from the data pins.

#### Row Decoder

The **row decoder** takes the row address and activates exactly one word line.

Example:

```text
Row address = 0101
Row decoder activates WL5
```

#### Column Decoder

The **column decoder** selects columns from the active row.

Example:

```text
Column address = 0011
Column decoder selects the required column group
```

#### Sense Amplifier And Row Buffer

When a row is activated, the tiny charge from the cells slightly changes the bit-line voltage. The **sense amplifier** detects the small difference and drives it to a strong 0 or 1.

The sense amplifiers together act like a **row buffer**. The row buffer temporarily holds the opened row.

This creates three important cases:

| Case | Meaning | Performance |
|---|---|---|
| Row hit | Requested data is in the already open row | Fastest |
| Row miss / closed-row access | No row is open, so the target row must be activated | Medium |
| Row conflict | A different row is open, so old row must close before new row opens | Slowest |

Exam line:

```text
DRAM latency depends on whether the access is a row hit, closed-row access or row conflict.
```

#### Banks

Modern DRAM is divided into **banks**. Each bank has its own row buffer and can hold a different open row.

Why banks are used:

- allow overlapping operations,
- improve bandwidth,
- reduce waiting time,
- allow bank interleaving,
- help memory controllers schedule requests efficiently.

Simple bank diagram:

```text
DRAM chip
+------------------------------------------------+
| Bank 0 -> row array + row buffer                |
| Bank 1 -> row array + row buffer                |
| Bank 2 -> row array + row buffer                |
| Bank 3 -> row array + row buffer                |
|                                                |
| Command/address logic + data interface          |
+------------------------------------------------+
```

<a id="topic-3-access-sequence"></a>

### DRAM Access Sequence

DRAM is not accessed like a simple random register file. It has a command sequence.

#### Step 1: Address Arrives At Memory Controller

The CPU, cache miss handler, Direct Memory Access engine or accelerator sends a memory request.

Example:

```text
Read address 0x8000_1234
```

The memory controller maps this address into:

- channel,
- rank,
- bank,
- row,
- column.

#### Step 2: ACTIVATE Opens The Row

The memory controller issues an **ACTIVATE** command to open the selected row in the selected bank.

What happens physically:

1. Row decoder selects one word line.
2. Access transistors in that row turn on.
3. Cell capacitors share charge with bit lines.
4. Sense amplifiers detect tiny voltage changes.
5. The row is restored and held in the row buffer.

The controller must wait for **tRCD - Row-to-Column Delay** before issuing a read or write.

#### Step 3: READ Or WRITE Selects Columns

After the row is active:

- **READ** selects the required columns and sends data to the SoC.
- **WRITE** selects the required columns and writes new data into the row buffer/cells.

For a read, data appears after **CL - CAS Latency**.

#### Step 4: Burst Transfer

DDR memories transfer data in bursts. Instead of transferring only one small word, they transfer a block of data over several cycles.

Why burst transfer is useful:

- cache lines contain multiple bytes,
- programs often access sequential addresses,
- high-speed data bus is used efficiently,
- command overhead is reduced.

#### Step 5: PRECHARGE Closes The Row

When the controller needs another row in the same bank, it may issue **PRECHARGE**.

Precharge closes the current row and prepares the bank for another ACTIVATE.

The controller must wait for **tRP - Row Precharge Time**.

#### Step 6: REFRESH Restores Charge

Because DRAM cells leak charge, the controller periodically issues **REFRESH** commands.

During refresh:

- normal access to refreshed banks may pause,
- rows are restored,
- timing parameter **tRFC - Refresh Cycle Time** must be obeyed.

Important:

```text
Refresh protects data correctness but reduces available memory bandwidth.
```

#### Complete Read Example

```text
CPU cache miss
    |
Memory controller receives read request
    |
Address decoded into channel/rank/bank/row/column
    |
ACTIVATE selected row
    |
wait tRCD
    |
READ selected column
    |
wait CAS latency
    |
burst data returns on DQ using DQS
    |
data fills cache line
    |
PRECHARGE later if another row is needed
```

<a id="topic-3-board-level"></a>

### Board-Level Design Issues

Off-die memory is located outside the SoC die, so board-level electrical design matters.

#### 1. Pin And Package Limitation

The SoC must use package pins/balls for memory signals. More memory bandwidth usually needs more data pins, command/address pins, clocks and power/ground pins.

Problem:

```text
More pins = larger package, higher cost and harder board routing.
```

#### 2. Signal Integrity

High-speed memory signals travel through package connections and PCB traces. At high speed, traces behave like transmission lines.

Signal integrity problems include:

- reflection,
- crosstalk,
- ringing,
- noise,
- skew,
- timing margin loss,
- impedance mismatch.

This is why DDR board layout is carefully controlled.

#### 3. Timing Skew

**Skew** means signals arrive at slightly different times.

Example:

```text
DQ0 arrives earlier than DQ7.
DQS strobe is not centered with data eye.
```

The system may use training/calibration to align timing.

#### 4. Power Delivery

External memory needs stable supply voltage. Board designers add decoupling capacitors near memory chips to reduce noise and supply fast current changes.

#### 5. Termination

High-speed signals may need termination to reduce reflections. Modern DDR memories often use **ODT - On-Die Termination**.

#### 6. Thermal Issues

Memory devices consume power and generate heat. Large memory systems, high data rates and many ranks can increase temperature.

#### 7. Controller Complexity

The SoC memory controller must manage:

- DRAM initialization,
- mode-register programming,
- address mapping,
- command scheduling,
- refresh,
- timing constraints,
- read/write turnaround,
- quality of service,
- error correction if present,
- low-power states.

This is why off-die memory gives capacity but adds system complexity.

<a id="topic-3-final-answer"></a>

### Final Exam-Ready Answer

Board-based or off-die memory systems are memory systems in which the main memory is placed outside the SoC silicon die, usually on the printed circuit board or in a separate memory package/module. The SoC contains the processor cores, caches, interconnect, memory controller and physical interface, while the large memory device such as DDR SDRAM or LPDDR is external to the die. The connection passes through the SoC package pins or balls and through PCB traces to the memory chip.

Off-die memory is used because large memory capacity is difficult and expensive to integrate on the SoC die. On-die SRAM gives low latency and high local bandwidth, but it consumes large silicon area and has high cost per bit. DRAM gives much higher density because a simple DRAM bit cell can be built using one access transistor and one storage capacitor. Therefore, SoCs normally use on-die memory for fast caches, boot memory, buffers and real-time storage, while using off-die DRAM for large main memory.

A simple DRAM cell stores one bit as charge on a small capacitor. The access transistor connects the capacitor to the bit line when the word line is activated. A charged capacitor represents one logic value and a discharged capacitor represents the other. Since the capacitor leaks charge, DRAM is dynamic and must be periodically refreshed. Also, reading a DRAM cell disturbs the stored charge, so the sense amplifier must detect the small bit-line voltage change and restore the cell value.

Many DRAM cells are arranged in a two-dimensional memory array of rows and columns. The row decoder selects a word line, which activates an entire row of cells. The bit lines carry small voltage changes to sense amplifiers. The sense amplifiers amplify the data and form a row buffer. The column decoder then selects the required column data from the active row. If the next access is to the same open row, it is a row hit and is fast. If a different row must be opened, the old row may need precharge and the new row must be activated, increasing latency.

The main DRAM commands are ACTIVATE, READ, WRITE, PRECHARGE and REFRESH. ACTIVATE opens a row and loads it into the row buffer. READ or WRITE accesses selected columns. PRECHARGE closes the active row and prepares the bank for another row. REFRESH restores charge in DRAM cells so data is preserved. Timing parameters such as tRCD, CAS latency, tRP and tRFC must be obeyed by the memory controller.

Board-based off-die memory also introduces physical design issues. The memory interface must use package pins, PCB traces, clocks, command/address signals, data signals, data strobes and termination. At high speeds, signal integrity, skew, crosstalk, reflections, power delivery and thermal effects become important. Thus, off-die memory provides high capacity and low cost per bit, but it requires a memory controller, physical interface and careful board-level design.

<a id="topic-3-short-answer"></a>

### Short 10-Mark Answer

Board-based or off-die memory is memory placed outside the SoC die, usually on the PCB or in a memory package/module. The SoC accesses it through a memory controller, package pins and board traces. Examples include DDR SDRAM and LPDDR.

Off-die memory is used because it provides large capacity and low cost per bit. On-die SRAM is faster but consumes large silicon area, so it is used for caches, TCM, buffers and Boot ROM, while off-die DRAM is used for main memory.

A simple DRAM cell stores one bit as charge on a capacitor controlled by an access transistor. It is called dynamic because the charge leaks and must be refreshed. A DRAM array organizes many cells into rows and columns. A word line selects a row, bit lines connect cells to sense amplifiers, and the column decoder selects required column data.

During access, the memory controller activates a row, waits for tRCD, issues a READ or WRITE, waits for CAS latency for read data, transfers burst data, and later precharges the bank if another row is needed. Refresh commands periodically restore cell charge.

Board-based memory gives capacity but adds latency, power, pin cost, signal integrity issues and controller complexity.

<a id="topic-3-technical-words"></a>

### Technical Words To Use In Exam

- **Board-based memory** (write this because the question specifically asks memory placed on the board.)
- **Off-die memory** (write this because the memory is outside the SoC silicon die.)
- **PCB - Printed Circuit Board** (write this because board-based means physically mounted on the board.)
- **Package pins/balls** (write this because off-die memory communication must leave the chip package.)
- **Memory controller** (write this because the SoC needs a controller to convert requests into DRAM commands.)
- **PHY - Physical Layer** (write this because high-speed memory needs an electrical interface.)
- **DRAM - Dynamic Random Access Memory** (write this because the topic asks simple DRAM.)
- **SDRAM - Synchronous Dynamic Random Access Memory** (write this because modern DRAM commands are clocked.)
- **DDR SDRAM - Double Data Rate Synchronous Dynamic Random Access Memory** (write this because board memory commonly uses DDR-style DRAM.)
- **LPDDR - Low-Power Double Data Rate** (write this because mobile SoCs commonly use LPDDR off-die memory.)
- **1T1C - One Transistor One Capacitor** (write this because it explains why DRAM is dense.)
- **Storage capacitor** (write this because DRAM stores data as charge.)
- **Access transistor** (write this because it connects the capacitor to the bit line.)
- **Word line** (write this because it selects a row.)
- **Bit line** (write this because it carries the cell signal to the sense amplifier.)
- **Row decoder** (write this because it selects the row address.)
- **Column decoder** (write this because it selects data from the active row.)
- **Sense amplifier** (write this because DRAM cell signals are tiny and must be amplified.)
- **Row buffer** (write this because the activated row is held there.)
- **Bank** (write this because modern DRAM is divided into banks for parallelism.)
- **ACTIVATE command** (write this because DRAM must open a row before access.)
- **READ command** (write this because column data is read from the active row.)
- **WRITE command** (write this because data is written into the active row/cells.)
- **PRECHARGE command** (write this because the current row must be closed before another row in the same bank.)
- **REFRESH command** (write this because DRAM capacitors leak charge.)
- **CAS latency / CL** (write this because it is the known delay from READ to first data.)
- **tRCD - Row-to-Column Delay** (write this because there is delay between ACTIVATE and READ/WRITE.)
- **tRP - Row Precharge Time** (write this because closing a row takes time.)
- **tRFC - Refresh Cycle Time** (write this because refresh blocks normal access for some time.)
- **Row hit** (write this because it explains the fastest DRAM case.)
- **Row conflict** (write this because it explains extra latency.)
- **Signal integrity** (write this because board-level DDR design depends on clean high-speed signals.)
- **DQ - Data pins** (write this because data travels on DQ lines.)
- **DQS - Data Strobe** (write this because DDR data uses strobes for timing.)
- **ODT - On-Die Termination** (write this because termination improves high-speed signal quality.)

<a id="topic-3-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 230119.png](<images/Screenshot 2026-05-12 230119.png>) contains the syllabus headline **Boardbased (Off-Die) Memory Systems, Simple DRAM and the Memory Array**.
2. **Syllabus/CLO image**: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) maps this topic to the SoC Components section and CLO 2.

#### Figure 1: Board-Based Off-Die Memory System

Draw this diagram when asked about board-based/off-die memory:

```text
               System on Chip die
+----------------------------------------------+
| CPU / DMA / accelerator                       |
|        |                                     |
| SoC interconnect / bus / NoC                  |
|        |                                     |
| Memory controller + DDR PHY                   |
+--------|-------------------------------------+
         |
   package pins / balls
         |
   PCB traces: CK, CA, DQ, DQS, control
         |
+--------|-------------------------------------+
| External DRAM chip / LPDDR / DDR module       |
+----------------------------------------------+
```

Why this figure is useful: it shows exactly what is inside the SoC and what is outside the die.

#### Figure 2: Simple 1T1C DRAM Cell

```text
             Word line
                |
                v
Bit line ----[ access transistor ]---- storage capacitor
                                             |
                                            GND

1T1C = one transistor + one capacitor
```

Why this figure is useful: it explains why DRAM is dense and why it needs refresh.

#### Figure 3: DRAM Memory Array

```text
                 Bit lines / columns
              BL0   BL1   BL2   BL3
               |     |     |     |
WL0 -------- [C]---[C]---[C]---[C]
WL1 -------- [C]---[C]---[C]---[C]
WL2 -------- [C]---[C]---[C]---[C]
WL3 -------- [C]---[C]---[C]---[C]
               |     |     |     |
          Sense amplifiers / row buffer

WL = Word Line
BL = Bit Line
C  = DRAM cell
```

Why this figure is useful: it shows row-column organization, which is the base of DRAM operation.

#### Figure 4: DRAM Read Command Flow

```text
Address decode
      |
ACTIVATE row
      |
wait tRCD
      |
READ column
      |
wait CAS latency
      |
burst data on DQ using DQS
      |
PRECHARGE later if another row is needed
      |
REFRESH periodically
```

Why this figure is useful: it directly explains what happens during a DRAM access.

#### Figure 5: Row Hit Vs Row Conflict

```text
Row hit:
requested row already open -> READ column -> fast

Row conflict:
wrong row open -> PRECHARGE -> ACTIVATE new row -> READ column -> slow
```

Why this figure is useful: it explains why DRAM latency is not constant.

---

<a id="topic-4"></a>

## Topic 4: Models Of Simple Processor-Memory Interaction

<a id="topic-4-question"></a>

### Question

**Explain Models of Simple Processor-Memory Interaction.**

<a id="topic-4-clo-mapping"></a>

### CLO Mapping

This topic belongs to **CLO 2: Describe SoC and its Components; Bus Architecture and Interconnection of SoC** in the current syllabus sequence because it explains how processors, memory modules and interconnect interact as SoC components.

It also strongly overlaps with **CLO 3: Understand the Memory Design in SoC and Memory Controller Architecture**, because the same model is used to understand memory bandwidth, memory contention, memory interleaving, DRAM banks and memory-controller scheduling. If the exam asks this under memory design, write **CLO 3**. If it appears after SoC components/off-die memory, write **CLO 2 with CLO 3 overlap**.

Detailed local PPT/book/web references are kept in [sources/CLO2_Topic4_sources.md](<sources/CLO2_Topic4_sources.md>).

<a id="topic-4-what-asking"></a>

### What The Question Is Asking

The examiner is asking how processors generate memory requests and how memory systems serve those requests. A weak answer says only: "processor sends address to memory and memory returns data." A good answer explains the performance problem:

1. Processors generate instruction fetches, loads, stores and cache misses.
2. Memory has finite service time.
3. Multiple processors or outstanding requests can compete for memory modules.
4. If requests go to the same memory resource, contention occurs.
5. If requests are spread across independent modules, bandwidth improves.
6. A pipelined/nonblocking processor issuing many outstanding requests can look like many simple processors to the memory system.
7. Caches, interleaving, banks, channels and memory-controller scheduling are used to reduce stalls.

Exam answer order:

```text
define interaction -> why model needed -> basic terms ->
one processor one memory -> many processors one memory ->
many processors many memory modules -> formula ->
pipelined processor equivalence -> SoC/cache/DRAM relation.
```

<a id="topic-4-main-explanation"></a>

### Main Explanation

**Processor-memory interaction** means the way a processor requests instructions/data from memory and the way the memory system responds. A processor is not useful alone. It needs memory for:

- fetching instructions,
- reading operands,
- writing results,
- accessing stack and heap,
- handling cache misses,
- reading/writing peripheral buffers,
- communicating with Direct Memory Access engines and accelerators.

In a simple program, the processor may appear to be "executing instructions." But internally, many instructions depend on memory. A load instruction may wait for data. An instruction fetch may miss in cache. A store may wait for a write buffer. A cache line refill may go to external DRAM. If memory is slow or busy, the processor stalls.

So the model asks:

```text
How many memory requests are generated?
How many memory requests can be served?
How much waiting occurs due to latency and contention?
```

This is why processor-memory interaction is modeled.

<a id="topic-4-why-modeled"></a>

### Why Processor-Memory Interaction Is Modeled

Modern SoC performance is not decided only by processor clock frequency. A fast processor can still be slow if memory cannot feed it.

Example:

```text
CPU can execute 1 instruction per cycle.
But every few instructions, it needs data from memory.
If data is not in cache, the CPU waits many cycles.
The useful execution rate drops.
```

Models are used because they help designers estimate:

- memory bandwidth needed by processors,
- number of memory banks/modules/channels required,
- effect of cache misses,
- effect of multiple processors sharing memory,
- effect of memory interleaving,
- probability of contention,
- benefit of nonblocking caches,
- pressure on memory controller queues,
- whether the SoC will be compute-bound or memory-bound.

Without modeling, a designer may choose a powerful processor but attach it to a weak memory system. Then the processor spends time waiting rather than computing.

#### Compute-Bound Vs Memory-Bound

A workload is **compute-bound** if performance is limited mainly by arithmetic or execution resources.

Example:

```text
Many ALU operations, few cache misses.
```

A workload is **memory-bound** if performance is limited mainly by memory latency or bandwidth.

Example:

```text
Large array traversal with frequent cache misses.
```

Processor-memory interaction models help identify memory-bound behavior early.

<a id="topic-4-basic-terms"></a>

### Basic Terms

#### Processor

A **processor** is the requester in the model. It generates memory requests when it needs instructions or data.

In a real SoC, the requesters may include:

- CPU - Central Processing Unit,
- GPU - Graphics Processing Unit,
- DSP - Digital Signal Processor,
- DMA - Direct Memory Access engine,
- AI accelerator,
- display controller,
- camera interface,
- network controller.

In a simple model, all these requesters can be abstracted as "processors" or "request sources."

#### Memory Request

A **memory request** is a read or write operation sent to memory.

Examples:

```text
Instruction fetch
Load data
Store data
Cache line refill
Writeback of dirty cache line
DMA read/write transfer
Accelerator input-buffer read
```

#### Memory Module

A **memory module** is an independently serviceable memory unit.

In the mathematical model, a memory module may represent:

- one memory bank,
- one SRAM block,
- one DRAM bank,
- one memory channel,
- one independent memory controller path.

The key assumption is:

```text
Each memory module can serve at most one request during one service time.
```

#### Service Time

**Service time**, usually written as **Ts**, is the time required for a memory module to serve one request.

It includes:

- accepting the request,
- selecting the address,
- performing memory access,
- returning data or completing write,
- becoming ready for the next request.

In real DRAM, service time depends on row hits, row conflicts, precharge, activate, CAS latency, refresh and bus turnaround. In the simple model, it is treated as one fixed time to make analysis easier.

#### Contention

**Contention** occurs when two or more requests need the same memory resource at the same time.

Example:

```text
CPU and DMA both request the same memory bank.
Only one can be served now.
The other waits.
```

Contention reduces achieved bandwidth.

#### Bandwidth

**Bandwidth** is the amount of memory work completed per unit time.

In this model, bandwidth can be measured as:

```text
requests served per memory service time
```

If four memory modules each serve one request during the same service time, achieved bandwidth is four requests per service time.

#### Latency

**Latency** is the time one request waits from issue to completion.

Bandwidth and latency are different:

```text
Latency  = how long one request takes.
Bandwidth = how many requests are completed per unit time.
```

High bandwidth does not always mean low latency. A system may transfer many requests overall but still make one urgent request wait.

<a id="topic-4-model-1"></a>

### Model 1: One Processor And One Memory

The simplest model has:

```text
1 processor + 1 memory module
```

Diagram:

```text
Processor ---- request/address/data ---- Memory
          <--- response/data -----------
```

Operation:

1. Processor generates a memory request.
2. Memory accepts the request.
3. Processor waits if the request is blocking.
4. Memory returns data or completes write.
5. Processor continues.

This model explains **basic memory stall**.

If memory is slow, the processor cannot keep executing normally. It waits for data.

Example:

```text
Processor executes a load instruction.
Data is not in cache.
Request goes to memory.
Memory takes 50 cycles.
Processor waits or switches to other work if possible.
```

#### Blocking Behavior

In a blocking model, the processor cannot issue another memory request until the current one completes.

```text
request 1 -> wait -> complete -> request 2 -> wait -> complete
```

This is simple but wastes time when memory latency is high.

#### What This Model Teaches

This model teaches:

- memory latency causes stalls,
- a single memory module has limited service capacity,
- a faster processor does not help if it spends time waiting,
- cache is needed to reduce the number of slow memory requests.

<a id="topic-4-model-2"></a>

### Model 2: Many Processors And One Memory

The next model has:

```text
n processors + 1 memory module
```

Diagram:

```text
P1 ----\
P2 -----\
P3 ------>  shared memory module
P4 -----/
Pn ----/
```

Each processor may generate a memory request. But the one memory module can serve only one request per service time.

If many processors request memory together:

- one request is served,
- others wait,
- contention increases,
- latency increases,
- achieved performance drops.

This model explains why a shared memory system can become a bottleneck.

Example:

```text
4 processors issue requests in the same service time.
Only 1 shared memory module exists.
Maximum served requests = 1.
3 requests wait.
```

Ideal processor demand is four requests, but memory service capacity is one request.

#### What This Model Teaches

This model teaches:

- sharing one memory resource limits parallelism,
- more processors do not automatically mean more performance,
- memory bandwidth must scale with processor count,
- arbitration is required when multiple requesters compete,
- caches and local memories reduce pressure on shared memory.

<a id="topic-4-model-3"></a>

### Model 3: Many Processors And Many Memory Modules

A more useful model has:

```text
n processors + m independent memory modules
```

Diagram:

```text
P1 ----\
P2 -----\                         M1
P3 ------> interconnect/arbiter -> M2
P4 -----/                         M3
Pn ----/                          Mm
```

Each processor may issue one memory request during one memory service time. Each request is mapped to one of the `m` memory modules.

If requests go to different memory modules, they can be served in parallel.

```text
P1 -> M1
P2 -> M2
P3 -> M3
P4 -> M4

All four can be served together.
```

If multiple requests go to the same module, contention occurs.

```text
P1 -> M2
P2 -> M2
P3 -> M3
P4 -> M4

M2 has contention.
Only one of P1/P2 can be served immediately.
```

#### Ideal Bandwidth

If `n` processors generate requests and `m` modules are available, the ideal maximum served requests per service time is:

```text
Ideal bandwidth = min(n, m)
```

But this ideal happens only if requests are perfectly distributed across memory modules.

#### Achieved Bandwidth With Random Distribution

In the Strecker-Ravi style simple model:

- there are `n` requests,
- there are `m` independent memory modules,
- each request is equally likely to go to any module,
- each module can serve at most one request per service time.

Probability that a particular request does **not** go to a selected module:

```text
1 - 1/m
```

Probability that none of the `n` requests goes to that selected module:

```text
(1 - 1/m)^n
```

Probability that the selected module is busy:

```text
1 - (1 - 1/m)^n
```

Since there are `m` modules, average number of busy modules is:

```text
B = m [1 - (1 - 1/m)^n]
```

Here:

- `B` = achieved bandwidth in requests served per service time,
- `n` = number of requests/processors,
- `m` = number of memory modules.

#### Example

Assume:

```text
n = 4 processors
m = 4 memory modules
```

Ideal bandwidth:

```text
min(4, 4) = 4 requests per service time
```

Achieved average bandwidth:

```text
B = 4 [1 - (1 - 1/4)^4]
B = 4 [1 - (3/4)^4]
B = 4 [1 - 0.316]
B = 4 x 0.684
B = 2.736 requests per service time
```

Meaning:

```text
Even with 4 modules and 4 requests, average served requests are about 2.7, not 4,
because some requests collide on the same memory module.
```

This is the main lesson of the model: **more memory modules improve bandwidth, but contention prevents perfect scaling.**

#### Table Example

| n requests | m modules | Ideal bandwidth | Average achieved bandwidth |
|---:|---:|---:|---:|
| 1 | 4 | 1 | 1.00 |
| 2 | 4 | 2 | 1.75 |
| 4 | 4 | 4 | 2.73 |
| 8 | 4 | 4 | 3.60 |

Interpretation:

- With few requests, modules are not fully used.
- With more requests, more modules become busy.
- But collisions still occur.
- Bandwidth approaches `m`, but cannot exceed `m`.

<a id="topic-4-pipelined-equivalence"></a>

### Pipelined Processor Equivalence

The textbook model also explains an important equivalence:

```text
n simple processors each issuing 1 request
        is similar to
1 pipelined/nonblocking processor issuing n outstanding requests
```

Diagram:

```text
Case A: many simple processors

P1 -> request 1
P2 -> request 2
P3 -> request 3
P4 -> request 4

Memory system sees 4 pending requests.


Case B: one aggressive processor

Pipelined CPU -> request 1
              -> request 2
              -> request 3
              -> request 4

Memory system still sees 4 pending requests.
```

This matters because modern processors do not always wait for one memory request to finish before issuing another. They may use:

- instruction pipelining,
- out-of-order execution,
- nonblocking caches,
- Miss Status Holding Registers,
- prefetching,
- multiple load/store queue entries,
- write buffers.

#### Outstanding Requests

An **outstanding request** is a memory request that has been issued but has not yet completed.

Example:

```text
CPU issues cache miss A.
Before A returns, CPU issues cache miss B.
Before B returns, CPU issues cache miss C.
```

Now the memory system has multiple outstanding requests.

#### Why Outstanding Requests Help

Outstanding requests help hide memory latency.

Without overlap:

```text
request A -> wait 100 cycles
request B -> wait 100 cycles
request C -> wait 100 cycles
total = 300 cycles
```

With overlap:

```text
request A issued
request B issued before A returns
request C issued before B returns
memory system overlaps service
total time may be much less than 300 cycles
```

But this only helps if the memory system has enough banks, modules, channels, queues and scheduling ability. If all requests go to one busy resource, contention remains.

#### MLP - Memory-Level Parallelism

**MLP - Memory-Level Parallelism** means the ability to have multiple memory accesses in progress at the same time.

MLP is useful because:

- it hides latency,
- it keeps memory modules busy,
- it improves bandwidth utilization,
- it helps high-performance processors and accelerators.

MLP is limited by:

- number of outstanding request buffers,
- memory controller queue size,
- memory bank/channel availability,
- address distribution,
- ordering rules,
- cache dependencies.

<a id="topic-4-relation-cache-dram"></a>

### Relation To Cache, Interleaving And DRAM

Processor-memory interaction models are simple, but they connect directly to real SoC design.

#### Relation To Cache

Cache reduces the number of requests that reach slow memory.

Average Memory Access Time is often summarized as:

```text
AMAT = hit time + miss rate x miss penalty
```

Meaning:

- if hit rate is high, most accesses are served quickly by cache,
- if miss rate is high, many accesses go to lower memory,
- miss penalty includes memory-controller and DRAM access delay.

So cache improves processor-memory interaction by reducing request pressure on main memory.

#### Relation To Memory Interleaving

**Memory interleaving** distributes consecutive or patterned addresses across multiple memory modules, banks or channels.

Example:

```text
Address block 0 -> Module 0
Address block 1 -> Module 1
Address block 2 -> Module 2
Address block 3 -> Module 3
Address block 4 -> Module 0
```

Why interleaving helps:

- spreads requests across modules,
- reduces probability of contention,
- increases number of busy modules,
- improves achieved bandwidth.

AMD official memory-controller documentation describes memory interleaving as making participating memory controllers appear like one large memory pool and balancing traffic across DDR controllers. This is the real hardware version of the `m memory modules` idea.

#### Relation To DRAM Banks

The `m memory modules` in the simple model can represent DRAM banks.

If requests go to different banks:

```text
Bank 0 can activate/read while Bank 1 is serving another request.
```

If requests go to the same bank:

```text
bank conflict occurs
one request waits
```

This is why DRAM address mapping and bank scheduling matter.

#### Relation To Memory Controller

The **memory controller** tries to improve achieved bandwidth by:

- buffering requests,
- reordering safe requests,
- exploiting row hits,
- spreading traffic across banks/channels,
- prioritizing urgent traffic,
- avoiding starvation,
- respecting DRAM timing constraints,
- managing read/write turnaround,
- issuing refresh commands.

So the simple model gives the basic mathematical intuition, while the memory controller applies that idea in real hardware.

#### Relation To SoC Interconnect

In an SoC, requests do not magically go from processor to memory. They pass through:

```text
processor/cache -> interconnect/NoC -> memory controller -> DRAM
```

The interconnect can also become a bottleneck. Even if memory has many modules, poor interconnect bandwidth or congestion can limit performance.

<a id="topic-4-final-answer"></a>

### Final Exam-Ready Answer

Models of simple processor-memory interaction are used to understand how memory requests generated by processors are served by the memory system. They are important because SoC performance is not determined only by processor clock frequency. A processor continuously fetches instructions, loads data, stores results and handles cache misses. If the memory system cannot supply data fast enough, the processor stalls and overall performance decreases.

The simplest model has one processor and one memory module. The processor issues a memory request, waits for the memory service time, receives the response and then continues. This model shows the basic effect of memory latency. If the access is blocking, the processor cannot make progress while waiting for memory. Therefore, a slow memory can reduce the benefit of a fast processor.

A second model has many processors and one shared memory module. Each processor may generate a request, but the memory module can serve only one request per service time. If several processors request memory at the same time, contention occurs. One request is served and the others wait. This model shows that adding processors does not automatically improve performance unless memory bandwidth also increases.

A more realistic model has `n` processors and `m` independent memory modules. If requests are sent to different modules, they can be served in parallel. If two or more requests go to the same module, contention occurs and only one is served during that service time. Ideally, the system can serve up to `min(n, m)` requests per service time, but real achieved bandwidth is lower because requests may collide on the same module.

In the Strecker-Ravi type model, `n` requests are uniformly distributed over `m` memory modules and each module can serve at most one request per service time. The probability that a selected module receives no request is `(1 - 1/m)^n`. Therefore, the probability that it is busy is `1 - (1 - 1/m)^n`. Since there are `m` modules, the average number of busy modules, or achieved bandwidth, is:

```text
B = m [1 - (1 - 1/m)^n]
```

This formula shows that increasing the number of memory modules improves bandwidth, but performance does not scale perfectly because multiple requests can still go to the same module. For example, with `n = 4` requests and `m = 4` modules, ideal bandwidth is 4 requests per service time, but average achieved bandwidth is about 2.73 requests per service time due to contention.

The same model also applies to one pipelined or nonblocking processor issuing multiple outstanding memory requests. From the memory system's point of view, `n` simple processors each issuing one request is similar to one aggressive processor issuing `n` outstanding requests. This is why modern processors use nonblocking caches, Miss Status Holding Registers, prefetching and memory-level parallelism to hide latency.

In real SoCs, caches reduce the number of requests reaching main memory, memory interleaving spreads addresses across banks or channels, and memory controllers schedule requests to improve bandwidth and reduce contention. DRAM banks, memory channels and interleaved memory modules are practical examples of the `m` memory modules in the simple model. Thus, processor-memory interaction models explain the relationship between latency, bandwidth, contention, cache misses, outstanding requests and memory-controller scheduling.

<a id="topic-4-short-answer"></a>

### Short 10-Mark Answer

Processor-memory interaction models explain how memory requests from processors are served by memory modules. They are needed because a processor may stall if instruction/data fetches or cache misses are not served quickly.

In the one-processor one-memory model, the processor sends a request and waits for memory response. This shows memory latency and blocking behavior.

In the many-processors one-memory model, many processors compete for one shared memory module. Since only one request can be served per service time, contention occurs and other requests wait.

In the `n` processor and `m` memory module model, requests can be served in parallel if they go to different modules. If multiple requests go to the same module, contention reduces bandwidth. For random distribution:

```text
B = m [1 - (1 - 1/m)^n]
```

where `B` is average achieved bandwidth, `n` is number of requests and `m` is number of memory modules.

This model also represents one pipelined/nonblocking processor issuing many outstanding requests. Caches, memory interleaving, multiple banks/channels and memory-controller scheduling are used to reduce contention and improve SoC performance.

<a id="topic-4-technical-words"></a>

### Technical Words To Use In Exam

- **Processor-memory interaction** (write this because it is the exact topic name.)
- **Memory request** (write this because the model counts requests generated by processors.)
- **Memory response** (write this because the processor waits for data/completion.)
- **Service time / Ts** (write this because memory modules serve requests over a service interval.)
- **n processors** (write this because request sources are represented by `n`.)
- **m memory modules** (write this because service resources are represented by `m`.)
- **Contention** (write this because multiple requests may select the same memory module.)
- **Bandwidth** (write this because the model calculates served requests per service time.)
- **Achieved bandwidth** (write this because real bandwidth is less than ideal when collisions occur.)
- **Latency** (write this because one request may wait for memory.)
- **Blocking request** (write this because simple processors may stall until memory returns.)
- **Outstanding request** (write this because pipelined/nonblocking processors issue multiple pending requests.)
- **Nonblocking cache** (write this because it allows progress with outstanding misses.)
- **MSHR - Miss Status Holding Register** (write this because cache hardware tracks outstanding misses.)
- **MLP - Memory-Level Parallelism** (write this because overlapping memory requests improves utilization.)
- **Memory interleaving** (write this because spreading addresses across modules reduces contention.)
- **Bank** (write this because DRAM banks are real examples of independent modules.)
- **Memory channel** (write this because channels are another real example of independent modules.)
- **Arbiter** (write this because competing requests need selection.)
- **Scheduler** (write this because memory controllers choose request order.)
- **AMAT - Average Memory Access Time** (write this because cache hit/miss behavior affects memory interaction.)
- **Hit rate** (write this because cache hits reduce external memory requests.)
- **Miss rate** (write this because cache misses increase memory traffic.)
- **Miss penalty** (write this because memory latency appears as extra delay after a cache miss.)
- **Strecker-Ravi model** (write this if your teacher/book expects the named model for the bandwidth formula.)
- **B = m [1 - (1 - 1/m)^n]** (write this because it is the key mathematical result.)

<a id="topic-4-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image part 1**: [Screenshot 2026-05-12 230134.png](<images/Screenshot 2026-05-12 230134.png>) contains **Models of Simple**.
2. **Topic image part 2**: [Screenshot 2026-05-12 230141.png](<images/Screenshot 2026-05-12 230141.png>) contains **Processor-Memory Interaction**.
3. **Syllabus/CLO image**: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) maps the memory/interconnect sequence used for this CLO.

#### Figure 1: One Processor One Memory

```text
Processor ---- request ----> Memory module
Processor <--- response ---- Memory module
```

Why this figure is useful: it shows blocking memory access and basic memory latency.

#### Figure 2: Many Processors One Memory

```text
P1 ----\
P2 -----\
P3 ------> Shared memory module
P4 -----/
```

Why this figure is useful: it shows contention when many requesters share one memory resource.

#### Figure 3: n Processors And m Memory Modules

```text
P1 ----\
P2 -----\                         M1
P3 ------> interconnect/arbiter -> M2
P4 -----/                         M3
Pn ----/                          Mm
```

Why this figure is useful: it shows how multiple independent modules can serve requests in parallel.

#### Figure 4: Pipelined Processor Equivalence

```text
Case A:
n processors x 1 request each

P1 -> R1
P2 -> R2
P3 -> R3
P4 -> R4

Case B:
1 pipelined processor x n outstanding requests

CPU -> R1
CPU -> R2
CPU -> R3
CPU -> R4

Memory system sees n pending requests in both cases.
```

Why this figure is useful: it directly matches the textbook idea that many simple processors and one aggressive pipelined processor can create similar memory pressure.

#### Figure 5: Contention Vs Interleaving

```text
Bad distribution:
R1 -> M2
R2 -> M2
R3 -> M2
Only one request served; others wait.

Good distribution:
R1 -> M1
R2 -> M2
R3 -> M3
Three requests served in parallel.
```

Why this figure is useful: it explains why memory interleaving and address mapping improve bandwidth.

---

<a id="topic-5"></a>

## Topic 5: On-Chip Interconnect, Bus Vs NoC And NoC Architectures

<a id="topic-5-question"></a>

### Question

**Explain On-Chip Interconnect, Bus vs NOC, and NOC architectures.**

Use the standard spelling **NoC - Network on Chip** in the answer. If the question writes NOC, treat it as the same thing.

<a id="topic-5-clo-mapping"></a>

### CLO Mapping

This topic belongs to **CLO 2: Describe SoC and its Components; Bus Architecture and Interconnection of SoC**.

Reason: This is the direct **bus architecture and interconnection** part of CLO 2. It explains how processors, memories, Direct Memory Access engines, accelerators and peripherals communicate inside a System on Chip.

Detailed local PPT/book/web references are kept in [sources/CLO2_Topic5_sources.md](<sources/CLO2_Topic5_sources.md>).

<a id="topic-5-what-asking"></a>

### What The Question Is Asking

The examiner is asking you to explain the communication fabric inside an SoC. A complete answer should explain:

1. What **on-chip interconnect** means physically.
2. Why SoC blocks need an interconnect.
3. What a **bus** is and why buses are simple.
4. Why shared buses become bottlenecks in large SoCs.
5. What **NoC - Network on Chip** means.
6. How NoC is different from a bus.
7. What NoC routers, links, network interfaces, packets and flits do.
8. Important NoC topologies: mesh, torus, ring, star, tree, fat tree and hybrid topologies.
9. Routing, switching, flow control, arbitration and QoS.
10. Design tradeoffs: latency, bandwidth, area, power, scalability, routing congestion, clock domains and verification.

Exam answer order:

```text
define on-chip interconnect -> why needed -> bus -> bus limits ->
NoC definition -> bus vs NoC -> NoC components -> NoC topologies ->
routing/flow control -> tradeoffs -> final answer.
```

<a id="topic-5-main-explanation"></a>

### Main Explanation

An **on-chip interconnect** is the hardware communication system inside a System on Chip. It connects blocks such as:

- CPU - Central Processing Unit,
- GPU - Graphics Processing Unit,
- DSP - Digital Signal Processor,
- DMA - Direct Memory Access engine,
- memory controller,
- on-chip SRAM,
- Boot ROM,
- accelerators,
- peripherals,
- debug blocks,
- security blocks.

It is physical hardware. It is made from wires, multiplexers, arbiters, decoders, bridges, buffers, routers and protocol logic. It also has a logical communication protocol that defines how address, data, control and response information move between blocks.

Beginner line:

```text
Processor executes.
Memory stores.
Interconnect carries communication between them.
```

Without interconnect, every block would need a separate direct wire connection to every other block. That becomes impossible as SoC size grows. The interconnect provides an organized way for blocks to communicate.

<a id="topic-5-why-needed"></a>

### Why On-Chip Interconnect Is Needed

An SoC contains many blocks, and these blocks must exchange data.

Examples:

- CPU reads instructions from memory.
- CPU programs a UART control register.
- DMA copies data from camera buffer to memory.
- GPU reads textures from DRAM.
- AI accelerator reads input tensors and writes output tensors.
- Display controller reads frame buffer repeatedly.
- Debug block reads internal registers.
- Security block checks access permissions.

Each communication needs:

- source,
- destination,
- address,
- command,
- data,
- response,
- ordering rules,
- error handling.

The on-chip interconnect handles these communication needs.

#### Interconnect Is Not Only Wires

A beginner may think an interconnect is only a group of wires. It is more than that.

It includes:

- **address decoding**: deciding which target owns an address,
- **arbitration**: deciding which master gets access when many request together,
- **data routing**: carrying read/write data to the correct block,
- **response routing**: returning data or status to the correct requester,
- **protocol conversion**: converting AXI to APB, AXI to AHB, or other protocols,
- **width conversion**: connecting 128-bit bus to 32-bit peripheral bus,
- **clock-domain crossing**: safely crossing different clock domains,
- **power-domain crossing**: handling powered-on and powered-off regions,
- **security filtering**: blocking illegal access,
- **QoS - Quality of Service**: prioritizing urgent traffic,
- **buffering**: storing transactions temporarily.

Important line:

```text
On-chip interconnect is the communication backbone of the SoC.
```

#### Master / Slave Or Manager / Subordinate

Older bus terminology uses:

- **master**: block that starts a transaction,
- **slave**: block that responds.

Newer Arm documents often use:

- **manager**: starts transaction,
- **subordinate**: responds to transaction.

Examples:

| Requester / manager | Target / subordinate |
|---|---|
| CPU | SRAM |
| DMA | DRAM controller |
| CPU | UART register block |
| Accelerator | local buffer |
| Debug block | system register |

Use whichever terminology your teacher uses, but understand the meaning.

<a id="topic-5-bus"></a>

### Bus-Based Interconnect

A **bus** is a shared communication path used to transfer address, data and control signals between blocks.

Basic bus:

```text
CPU ----\
DMA -----\
GPU ------> Shared bus ---> Memory / Peripherals
DSP -----/
```

Only one or a limited number of transactions can use the shared bus at the same time. Therefore, a bus usually needs an **arbiter**.

#### Bus Signals

A bus commonly carries:

- address signals,
- write data,
- read data,
- read/write control,
- byte enables,
- valid/ready or request/grant signals,
- response/error signals,
- clock and reset.

#### How A Bus Transaction Happens

Example: CPU reads a peripheral register.

1. CPU places address on bus.
2. CPU marks the transaction as read.
3. Address decoder identifies target peripheral.
4. Arbiter grants bus access if multiple masters are requesting.
5. Peripheral returns read data.
6. CPU receives data and continues.

Example: CPU writes to UART register.

```text
CPU -> address + write data + write control -> bus -> UART register
UART -> response -> CPU
```

#### Arbitration In A Bus

**Arbitration** is needed when multiple masters request the bus.

Common arbitration schemes:

- fixed priority,
- round robin,
- weighted round robin,
- time-division multiplexing,
- QoS-aware arbitration.

Example:

```text
CPU, DMA and display controller request memory.
Arbiter chooses display first because display has real-time deadline.
CPU and DMA wait.
```

#### AMBA Bus Family

**AMBA - Advanced Microcontroller Bus Architecture** is an Arm family of SoC interface specifications. It is widely used in SoCs.

Important AMBA protocols:

| Protocol | Full form | Typical use |
|---|---|---|
| AXI | Advanced eXtensible Interface | High-performance memory-mapped communication |
| AHB | Advanced High-performance Bus | Embedded moderate-performance systems |
| APB | Advanced Peripheral Bus | Simple low-bandwidth peripheral registers |
| AXI-Stream | Advanced eXtensible Interface Stream | Streaming data without normal memory-mapped addresses |
| ACE | AXI Coherency Extensions | Cache-coherent communication in older coherent systems |
| CHI | Coherent Hub Interface | Newer high-performance coherent interconnect protocol |

Arm official documentation says AMBA defines interfaces and protocols for on-chip and off-chip use, and AMBA 5 includes key protocols such as CHI and AXI. Arm's AXI learning material also explains AMBA as an open-standard on-chip interconnect specification for connecting and managing functional blocks in SoC designs.

#### Advantages Of Bus

Bus-based interconnect is useful because:

- simple to understand,
- simple to implement for small SoCs,
- lower area than complex NoC for small systems,
- easier verification,
- low latency for a small number of masters,
- standard protocols such as AMBA AXI/AHB/APB support IP reuse.

#### Limitations Of Bus

A shared bus becomes weak when the SoC becomes large.

Problems:

1. **Limited parallelism**: many masters cannot use one shared bus freely at the same time.
2. **Arbitration delay**: requesters wait for bus grant.
3. **Bandwidth bottleneck**: total traffic is limited by bus width and clock.
4. **Long wires**: a global bus may span the chip, increasing delay and power.
5. **Capacitance**: many connected blocks increase electrical loading.
6. **Poor scalability**: adding more masters/slaves makes timing and arbitration harder.
7. **Clocking difficulty**: one global synchronous bus becomes hard across large chips.
8. **Routing congestion**: wide shared buses consume routing resources.

Exam line:

```text
A bus is simple and efficient for small SoCs, but it becomes a bandwidth and wiring bottleneck in large multicore SoCs.
```

<a id="topic-5-crossbar"></a>

### Crossbar And Hierarchical Interconnect

Before moving to NoC, many SoCs use improved bus structures.

#### Hierarchical Bus

A **hierarchical bus** separates traffic into levels.

Example:

```text
High-speed AXI bus -> CPU, DMA, memory controller
Low-speed APB bus  -> UART, timer, GPIO, SPI
Bridge             -> connects AXI to APB
```

Why hierarchy helps:

- high-speed blocks do not wait for low-speed peripherals,
- low-speed peripherals do not need expensive wide high-speed interfaces,
- power and area are reduced,
- address map becomes organized.

#### Bus Bridge

A **bridge** connects two bus domains.

It may convert:

- AXI to APB,
- AXI to AHB,
- wide bus to narrow bus,
- fast clock to slow clock,
- one address region to another,
- burst transaction to simple register accesses.

Bridge is hardware.

#### Crossbar

A **crossbar** is a switch matrix connecting multiple masters to multiple slaves.

```text
        +-------------------+
CPU ----|                   |---- SRAM
DMA ----|     Crossbar      |---- DRAM controller
GPU ----|                   |---- Peripheral bridge
DSP ----|                   |---- Accelerator
        +-------------------+
```

A crossbar can allow multiple simultaneous transfers if they use different source-destination paths.

Example:

```text
CPU -> SRAM
DMA -> DRAM controller

Both may occur together if crossbar paths do not conflict.
```

Advantages:

- more parallelism than shared bus,
- lower contention for independent paths,
- useful for moderate SoC complexity.

Limitations:

- area and wire cost grow quickly with number of masters and slaves,
- arbitration still needed at each target,
- global wiring can become hard,
- not as scalable as a packet-based NoC for many-core systems.

<a id="topic-5-noc"></a>

### NoC - Network On Chip

**NoC - Network on Chip** is a packet-based on-chip communication network. It connects SoC blocks using routers, links and network interfaces, similar in concept to a computer network but implemented inside a chip.

Basic idea:

```text
Instead of one big shared bus,
use many small routers and links.
Data moves as packets across the chip.
```

NoC is hardware. It is not software networking. It is an on-chip communication fabric built into the SoC.

#### Why NoC Is Used

NoC is used because large SoCs may contain:

- many CPU cores,
- GPU blocks,
- AI accelerators,
- DSPs,
- DMA engines,
- memory controllers,
- display/camera/video blocks,
- debug/security units,
- multiple clock and power domains.

In such systems, a single bus or simple crossbar becomes difficult to scale. NoC distributes communication across routers and links.

Cadence describes modern NoC IP as a configurable network-on-chip interconnect used to address increasing connectivity-fabric complexity from subsystem level to full SoC and multi-chiplet systems. Cadence also lists reduced wire count, reduced congestion and configurable bandwidth/latency as NoC benefits. Benini and De Micheli's classic NoC paper explains that on-chip physical interconnections become a limiting factor for performance and energy as SoC complexity grows, and proposes layered on-chip micronetworks for reliable component interaction.

#### Packet-Based Communication

In a NoC, a transaction is converted into a packet.

Example CPU read:

```text
CPU load miss
    |
network interface creates request packet
    |
packet travels through routers
    |
memory controller receives packet
    |
memory returns response packet
    |
CPU receives data
```

Packet may contain:

- destination address,
- source ID,
- transaction type,
- read/write command,
- data,
- byte enables,
- QoS or priority,
- response status.

#### Packet, Flit And Link

A **packet** is a complete message.

A **flit - flow control digit** is a smaller unit of a packet moved through the NoC.

Example:

```text
Packet = header flit + body flits + tail flit
```

The **header** usually contains routing information. The **payload** contains data or transaction content.

<a id="topic-5-bus-vs-noc"></a>

### Bus Vs NoC

| Point | Bus-Based Interconnect | NoC - Network on Chip |
|---|---|---|
| Basic idea | Shared communication path | Packet-switched network of routers and links |
| Best for | Small/simple SoCs | Large/multicore/accelerator-heavy SoCs |
| Communication | Address/data/control on bus | Packets/flits routed through network |
| Parallelism | Limited in shared bus | Multiple packets can move in different links |
| Scalability | Poor for many masters/slaves | Better for large systems |
| Latency | Low for small systems | Can be higher due to router hops |
| Bandwidth | Limited by shared bus width/clock | Scales with links, routers, topology and channels |
| Wiring | Wide global buses can be hard | More distributed, local links |
| Arbitration | Central or bus-level arbitration | Distributed arbitration in routers/targets |
| Area | Low for small SoCs | Router/buffer overhead |
| Power | Low for small traffic | Can be efficient for distributed traffic, but routers/buffers consume power |
| QoS | Possible but limited in simple buses | More flexible priority/virtual-channel/QoS support |
| Verification | Easier | More complex due to routing, ordering and deadlock |

#### Key Comparison Paragraph

A bus is simple because all blocks share a common communication structure. It is good when there are few masters and moderate bandwidth requirements. But as the number of masters increases, the bus becomes a shared bottleneck. Only limited transactions can proceed at once, arbitration delay increases, and long global wires create timing and power problems.

A NoC solves this by replacing the single shared structure with a network of routers and links. Different packets can travel through different parts of the network at the same time. This improves scalability and bandwidth for large SoCs. However, NoC is more complex because designers must choose topology, routing, buffering, flow control, QoS and deadlock avoidance.

Exam line:

```text
Bus is simple but less scalable.
NoC is complex but more scalable for many-core and high-bandwidth SoCs.
```

<a id="topic-5-noc-components"></a>

### NoC Architecture Components

A NoC architecture is not only a topology diagram. It contains several hardware components.

#### 1. Network Interface

The **network interface** connects an IP block to the NoC.

Its job:

- accepts local bus transaction from CPU/DMA/accelerator,
- packetizes the transaction,
- adds source/destination information,
- handles ordering and protocol fields,
- injects packet into NoC,
- receives response packets,
- converts packets back into local bus responses.

Example:

```text
AXI read request -> network interface -> NoC packet
NoC response packet -> network interface -> AXI read response
```

#### 2. Router

A **router** forwards packets/flits inside the NoC.

Router functions:

- input buffering,
- route computation,
- virtual-channel allocation,
- switch allocation,
- arbitration,
- forwarding to output link,
- local delivery to attached IP block.

Typical mesh router ports:

```text
North
South
East
West
Local
```

#### 3. Links

**Links** are physical wires between routers or between router and network interface.

Link design choices:

- width,
- clock frequency,
- pipeline stages,
- serialization,
- buffering,
- clock-domain crossing,
- power gating.

#### 4. Buffers

Buffers store flits temporarily inside routers.

Why buffers are needed:

- downstream link may be busy,
- output port may be occupied,
- destination may apply backpressure,
- traffic bursts must be absorbed.

But buffers consume area and leakage power.

#### 5. Arbiter

An **arbiter** chooses between competing flits/packets requesting the same output port.

Example:

```text
North input and West input both want East output.
Router arbiter chooses one first.
```

#### 6. QoS Logic

**QoS - Quality of Service** logic manages priority, bandwidth or latency guarantees.

Examples:

- display traffic may need guaranteed bandwidth,
- CPU interrupt-related traffic may need low latency,
- background DMA may be best effort,
- real-time audio cannot tolerate underflow.

QoS mechanisms:

- priority,
- weighted arbitration,
- traffic classes,
- bandwidth reservation,
- virtual channels,
- deadlines,
- credit control.

#### 7. Protocol Adapter / Bridge

The NoC may connect blocks using different protocols.

Examples:

- AXI manager to NoC,
- NoC to APB peripheral bridge,
- NoC to DDR controller,
- coherent CPU cluster to non-coherent accelerator.

Protocol adapters ensure correct communication.

<a id="topic-5-topologies"></a>

### NoC Topologies

**Topology** means the connection pattern of routers/nodes.

#### 1. Mesh Topology

Mesh is the most common NoC teaching topology.

```text
R -- R -- R
|    |    |
R -- R -- R
|    |    |
R -- R -- R

R = router/node
```

Features:

- regular 2D grid,
- layout-friendly,
- easy to scale,
- uses local neighbor links,
- supports simple XY routing.

Advantages:

- regular structure,
- good for tiled/many-core layouts,
- easier physical design,
- multiple paths exist between many nodes.

Disadvantages:

- corner-to-corner traffic takes many hops,
- center routers may become congested,
- bisection bandwidth depends on mesh size and link width.

Use:

- many-core processors,
- tiled accelerators,
- scalable SoC fabrics.

#### 2. Torus Topology

Torus is like mesh with wraparound links.

```text
R -- R -- R
|    |    |
R -- R -- R
|    |    |
R -- R -- R

plus wraparound links from left edge to right edge
and top edge to bottom edge
```

Advantages:

- lower maximum hop count than mesh,
- better load balance,
- more path diversity.

Disadvantages:

- wraparound wires may be long,
- physical layout is harder,
- routing and deadlock avoidance become more complex.

#### 3. Ring Topology

Ring connects nodes in a loop.

```text
R -- R -- R -- R
|              |
R -- R -- R -- R
```

Advantages:

- simple,
- low area,
- easy to reason about,
- good for moderate number of nodes.

Disadvantages:

- latency grows with number of nodes,
- one hot link can become bottleneck,
- bandwidth limited by ring direction/count.

Use:

- small multicore systems,
- coherent interconnect rings,
- control networks.

#### 4. Star Topology

Star connects all nodes to a central hub.

```text
       R
       |
R ---- H ---- R
       |
       R

H = hub
```

Advantages:

- simple routing,
- small hop count through hub,
- easy central control.

Disadvantages:

- hub bottleneck,
- hub failure/congestion affects all,
- not scalable for large systems.

#### 5. Tree Topology

Tree connects nodes hierarchically.

```text
          R
        /   \
       R     R
      / \   / \
     R  R  R  R
```

Advantages:

- natural hierarchy,
- useful for clustered systems,
- can match memory/peripheral hierarchy.

Disadvantages:

- upper links can become bottlenecks,
- traffic between leaves may go up and down tree,
- root congestion is possible.

#### 6. Fat Tree

Fat tree increases bandwidth near the root.

```text
Lower-level links: narrower
Upper-level links: wider / more parallel
```

Why:

- more traffic aggregates near root,
- wider upper links reduce bottleneck.

Use:

- high-bandwidth hierarchical networks,
- server-style or many-core inspired networks.

#### 7. Crossbar Topology

Crossbar can be treated as a small NoC-like switch fabric for moderate systems.

Advantages:

- low latency for moderate size,
- high parallelism if paths differ.

Disadvantages:

- does not scale well as ports increase,
- wiring and area grow quickly.

#### 8. Hybrid / Application-Specific Topology

Many real SoCs do not use a pure textbook topology. They use hybrid interconnects.

Examples:

- mesh for compute cluster,
- ring for coherent CPU cluster,
- tree for peripheral/control network,
- crossbar near memory controllers,
- separate NoC for high-bandwidth data and low-bandwidth control,
- chiplet interconnect for multi-die systems.

Exam line:

```text
Real SoC NoCs are often application-specific hybrids optimized for traffic, floorplan, power and QoS.
```

<a id="topic-5-routing"></a>

### Routing, Switching And Flow Control

NoC architecture is defined not only by topology, but also by how packets move.

#### Routing

**Routing** decides the path from source to destination.

Types:

| Routing type | Meaning | Example |
|---|---|---|
| Deterministic routing | Same source-destination pair uses fixed path | XY routing in mesh |
| Adaptive routing | Path changes based on congestion/faults | choose less congested direction |
| Source routing | Source encodes path in packet | route stored in header |
| Table-based routing | Routers use lookup table | flexible but table storage needed |

#### XY Routing

In 2D mesh, **XY routing** means:

```text
First move in X direction.
Then move in Y direction.
```

Example:

```text
Source = (0,0)
Destination = (2,1)

(0,0) -> (1,0) -> (2,0) -> (2,1)
```

Why it is used:

- simple,
- predictable,
- low hardware cost,
- can avoid deadlock in regular mesh when designed correctly.

#### Switching

**Switching** defines how packets are forwarded.

| Switching method | Meaning | Tradeoff |
|---|---|---|
| Store-and-forward | Whole packet stored before forwarding | simple but higher latency/buffer |
| Virtual cut-through | packet can advance if next buffer has space | lower latency if path free |
| Wormhole switching | packet split into flits, header leads route | low buffer need, but blocking can hold path |

#### Flow Control

**Flow control** prevents packet/flit loss due to full buffers.

Common methods:

- ready/valid handshake,
- credit-based flow control,
- backpressure,
- virtual-channel flow control.

#### Backpressure

Backpressure means downstream congestion stops upstream sending.

Example:

```text
Router B buffer full.
Router B tells Router A to stop sending.
Router A holds flits until space becomes available.
```

#### Virtual Channels

A **virtual channel** is a logical channel sharing the same physical link.

Why virtual channels help:

- reduce head-of-line blocking,
- separate traffic classes,
- help deadlock avoidance,
- support QoS.

#### Deadlock And Livelock

**Deadlock** means packets wait forever due to circular resource dependency.

Example:

```text
Packet A waits for buffer held by Packet B.
Packet B waits for buffer held by Packet C.
Packet C waits for buffer held by Packet A.
No packet can move.
```

**Livelock** means packets keep moving but never reach the destination.

NoC design must avoid both.

<a id="topic-5-tradeoffs"></a>

### Design Tradeoffs And Challenges

#### 1. Latency

Latency is the time from request injection to response arrival.

NoC latency includes:

- network interface delay,
- router delay,
- link delay,
- arbitration delay,
- queueing delay,
- destination service time.

Bus latency may be lower in a small SoC, but NoC can perform better under heavy parallel traffic.

#### 2. Bandwidth

Bandwidth depends on:

- number of links,
- link width,
- clock frequency,
- topology,
- routing,
- traffic distribution,
- router throughput,
- number of memory controllers.

NoC can scale bandwidth by adding links/routers, while a shared bus has a more fixed bottleneck.

#### 3. Area

NoC area comes from:

- routers,
- buffers,
- virtual-channel logic,
- network interfaces,
- links,
- protocol adapters.

Bus area may be lower for small systems, but wide global buses and crossbars also become expensive.

#### 4. Power

Interconnect consumes power in:

- long wires,
- router switching,
- buffer reads/writes,
- clocking,
- arbitration logic,
- repeated packet hops.

NoC may reduce long global wire problems but adds router/buffer overhead.

#### 5. Scalability

Scalability means the design remains practical as the number of blocks increases.

Bus scalability is limited because all traffic competes for shared resources.

NoC scalability is better because communication is distributed.

#### 6. Routing Congestion

Physical design tools must route wires across the chip. Wide buses and many point-to-point connections create congestion.

NoC can reduce global routing congestion by using structured local links and routers.

#### 7. Clock And Power Domains

Large SoCs have multiple clock and power domains.

The interconnect must handle:

- CDC - Clock Domain Crossing,
- reset-domain crossing,
- isolation when a power domain is off,
- retention or wake-up traffic,
- asynchronous bridges.

#### 8. Ordering And Coherency

Some transactions must be observed in order. Some systems need cache coherence.

Example:

```text
CPU writes data.
DMA reads data.
Interconnect and cache system must ensure DMA sees the correct value.
```

Coherent protocols such as ACE or CHI help manage cache coherence in complex systems.

#### 9. Security

The interconnect may enforce:

- secure vs non-secure access,
- privilege levels,
- firewall rules,
- address-region protection.

Example:

```text
Non-secure DMA must not access secure key storage.
```

#### 10. Verification

NoC verification is difficult because many things can happen concurrently.

Must verify:

- no deadlock,
- no data corruption,
- correct routing,
- correct ordering,
- QoS guarantees,
- clock-domain crossing safety,
- reset behavior,
- security/firewall behavior,
- performance under traffic stress.

<a id="topic-5-final-answer"></a>

### Final Exam-Ready Answer

An on-chip interconnect is the hardware communication fabric that connects different blocks inside a System on Chip. It connects processors, memories, memory controllers, Direct Memory Access engines, accelerators, peripherals, debug blocks and security blocks. It is not only wires; it includes address decoding, arbitration, data routing, response routing, protocol conversion, buffering, clock-domain crossing, security filtering and quality-of-service control. Therefore, the interconnect is the communication backbone of the SoC.

A bus-based interconnect uses a shared communication path carrying address, data and control signals. In a simple bus, multiple masters such as CPU and DMA request access to shared targets such as memory or peripherals. An arbiter decides which master gets the bus. Bus-based systems are simple, low-area and easy to verify for small SoCs. Standard buses such as AMBA AXI, AHB and APB improve IP reuse because different blocks can communicate through standard interfaces.

However, a shared bus does not scale well for large SoCs. Only limited transfers can occur at the same time, so arbitration delay increases as more masters are added. A global bus also creates long wires, high capacitance, routing congestion, timing problems and limited bandwidth. Hierarchical buses and crossbars improve this by separating high-speed and low-speed traffic or allowing multiple independent transfers, but crossbars and large bus matrices also become expensive as the number of masters and slaves grows.

A NoC, or Network on Chip, is a packet-based on-chip communication network. It replaces one large shared bus with routers, links and network interfaces. A network interface converts local bus transactions into packets. Packets are divided into flits and routed through routers to the destination. The destination network interface converts the packet back into a local transaction. Multiple packets can travel through different parts of the NoC at the same time, giving better scalability and bandwidth for multicore and accelerator-rich SoCs.

The main components of a NoC are network interfaces, routers, links, buffers, arbiters, routing logic, flow-control logic, virtual channels and QoS logic. Routers forward packets or flits from input ports to output ports. Links carry flits between routers. Buffers store flits temporarily when the next link is busy. Flow control prevents buffer overflow, while virtual channels reduce head-of-line blocking and can help avoid deadlock.

NoC architecture depends strongly on topology. A mesh topology arranges routers in a 2D grid and is regular, scalable and layout-friendly. A torus is a mesh with wraparound links, reducing hop count but making physical wiring harder. A ring is simple and low-area but latency grows as nodes increase. A star has a central hub but the hub can become a bottleneck. A tree provides hierarchy but upper links can become congested. A fat tree increases bandwidth near the root. Real SoCs often use hybrid topologies optimized for traffic pattern, floorplan, memory-controller placement, power and QoS.

Bus and NoC differ mainly in scalability. A bus is simple and efficient for small systems, but it becomes a bandwidth and wiring bottleneck as the SoC grows. A NoC is more complex, but it supports distributed communication, higher parallelism, scalable bandwidth, traffic classes and better management of large SoC communication. The choice depends on latency, bandwidth, area, power, verification effort, number of masters/slaves, clock domains, security and quality-of-service requirements.

<a id="topic-5-short-answer"></a>

### Short 10-Mark Answer

On-chip interconnect is the hardware communication fabric inside an SoC. It connects CPU, DMA, accelerators, memories, memory controllers and peripherals. It handles address decoding, arbitration, data transfer, responses, protocol conversion, buffering, clock-domain crossing, security and QoS.

A bus is a shared communication path carrying address, data and control signals. It is simple, low-area and useful for small SoCs. AMBA AXI, AHB and APB are common bus/interface standards. But a shared bus has limited parallelism and becomes a bottleneck when many masters compete for bandwidth.

A NoC, or Network on Chip, is a packet-based interconnect using routers, links and network interfaces. The network interface packetizes transactions, routers forward packets/flits, and links carry traffic between routers. NoC improves scalability because multiple packets can move through different network paths in parallel.

Bus is simpler and lower latency for small systems. NoC is more complex but better for large multicore or accelerator-heavy SoCs. NoC architectures include mesh, torus, ring, star, tree, fat tree, crossbar-like and hybrid topologies. Important NoC design issues are routing, switching, flow control, buffering, virtual channels, deadlock avoidance, QoS, latency, bandwidth, power, area and verification.

<a id="topic-5-technical-words"></a>

### Technical Words To Use In Exam

- **On-chip interconnect** (write this because it is the exact communication fabric inside the SoC.)
- **Bus** (write this because the question asks bus vs NoC.)
- **Shared bus** (write this because bus bottleneck comes from shared use.)
- **Arbitration** (write this because multiple masters compete for the same interconnect.)
- **Address decoding** (write this because the interconnect must select the target block.)
- **Master / manager** (write this because request-starting blocks must be named.)
- **Slave / subordinate** (write this because target/responding blocks must be named.)
- **AMBA - Advanced Microcontroller Bus Architecture** (write this because it is a standard SoC interconnect family.)
- **AXI - Advanced eXtensible Interface** (write this because it is a common high-performance AMBA protocol.)
- **AHB - Advanced High-performance Bus** (write this because it is a common embedded SoC bus.)
- **APB - Advanced Peripheral Bus** (write this because low-speed peripherals often use it.)
- **CHI - Coherent Hub Interface** (write this because coherent high-performance systems use coherent interconnect protocols.)
- **Bridge** (write this because SoCs connect different buses, widths and clock domains.)
- **Crossbar** (write this because it is the intermediate structure between bus and NoC.)
- **NoC - Network on Chip** (write this because NOC must be expanded for marks.)
- **Network interface** (write this because it converts local transactions into packets.)
- **Router** (write this because NoC communication is routed through routers.)
- **Link** (write this because routers communicate over links.)
- **Packet** (write this because NoC communication is packet-based.)
- **Flit - Flow control digit** (write this because NoCs often move packets in flits.)
- **Header** (write this because routing information is usually in the header.)
- **Payload** (write this because packet data must be identified.)
- **Topology** (write this because NoC architecture means connection pattern.)
- **Mesh topology** (write this because it is the most common NoC exam topology.)
- **Torus topology** (write this because it shows mesh improvement with wraparound links.)
- **Ring topology** (write this because simple NoCs/coherent interconnects may use rings.)
- **Tree / fat tree** (write this because hierarchy and bandwidth scaling matter.)
- **Routing** (write this because packets need paths.)
- **XY routing** (write this because it is the standard simple mesh-routing example.)
- **Switching** (write this because packets/flits must move through routers.)
- **Wormhole switching** (write this because it is a common NoC switching concept.)
- **Flow control** (write this because buffers and links must not overflow.)
- **Backpressure** (write this because congestion must be signaled upstream.)
- **Virtual channel** (write this because it reduces blocking and helps QoS/deadlock control.)
- **Deadlock** (write this because NoC correctness requires avoiding cyclic waiting.)
- **Livelock** (write this because packets must eventually reach destination.)
- **QoS - Quality of Service** (write this because SoC traffic has different latency/bandwidth needs.)
- **CDC - Clock Domain Crossing** (write this because large interconnects cross clock domains.)
- **Bandwidth** (write this because interconnect must carry enough traffic.)
- **Latency** (write this because each transaction experiences delay.)
- **Congestion** (write this because heavy traffic creates queueing and bottlenecks.)
- **PPA - Power, Performance, Area** (write this because interconnect choice is a PPA tradeoff.)

<a id="topic-5-diagrams"></a>

### Images / Diagrams To Remember

1. **Topic image**: [Screenshot 2026-05-12 230212.png](<images/Screenshot 2026-05-12 230212.png>) contains the syllabus headline **On Chip Interconnect, Bus vs NOC, NOC architectures**.
2. **Syllabus/CLO image**: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) maps this topic to CLO 2 bus architecture and SoC interconnection.

#### Figure 1: On-Chip Interconnect As SoC Backbone

```text
                 System on Chip
+------------------------------------------------+
| CPU       DMA       GPU       Accelerator       |
|  \         |         |          /               |
|   \        |         |         /                |
|        On-chip interconnect / NoC / bus         |
|   /        |         |         \                |
| SRAM   DDR controller   APB bridge   Debug      |
|                         |                      |
|                   UART Timer GPIO SPI          |
+------------------------------------------------+
```

Why this figure is useful: it shows that interconnect is the shared communication backbone connecting all SoC components.

#### Figure 2: Shared Bus

```text
CPU ----\
DMA -----\
GPU ------> shared bus ---> Memory / Peripherals
DSP -----/

Arbiter decides who uses the bus.
```

Why this figure is useful: it explains bus simplicity and the bottleneck caused by shared access.

#### Figure 3: Hierarchical AMBA-Style Bus

```text
CPU / DMA / Accelerator
          |
      AXI high-speed bus
          |
   +------+------+
   |             |
DDR controller  AXI-to-APB bridge
                 |
              APB bus
                 |
          UART Timer GPIO SPI
```

Why this figure is useful: it shows why SoCs use high-speed buses for memory and simple buses for peripherals.

#### Figure 4: NoC Basic Architecture

```text
IP block -> Network Interface -> Router -- Link -- Router -> Network Interface -> IP block
                               |                    |
                              Link                 Link
                               |                    |
                             Router -- Link -- Router
```

Why this figure is useful: it shows the NoC parts: network interface, router and link.

#### Figure 5: Mesh NoC

```text
R -- R -- R
|    |    |
R -- R -- R
|    |    |
R -- R -- R

R = router/node
```

Why this figure is useful: mesh is the easiest NoC topology to draw and explain in an exam.

#### Figure 6: Bus Vs NoC Memory Traffic

```text
Bus:
CPU, DMA, GPU, display -> one shared path -> DDR controller

NoC:
CPU -> routers -> DDR controller 0
DMA -> routers -> DDR controller 1
GPU -> routers -> SRAM
Display -> routers -> DDR controller 0
```

Why this figure is useful: it shows that NoC allows distributed parallel paths while bus traffic concentrates on one shared path.

#### Figure 7: Router Internal View

```text
          North
            |
West -- [ Router ] -- East
            |
          South
            |
          Local IP

Inside router:
input buffers + routing logic + arbiter + switch + output ports
```

Why this figure is useful: it helps explain what a NoC router actually does.

---

<a id="clo2-review-addendum"></a>

## CLO 2 Review Addendum: Factual Integration And Exam Traps

Detailed review sources are kept in [sources/CLO2_review_sources.md](<sources/CLO2_review_sources.md>).

This CLO is now best understood as one connected story:

```text
Processor generates work.
Memory stores instructions and data.
Interconnect moves requests and responses.
Architecture decides how these are organized.
PPA decides whether the organization is practical.
```

### Factual Integration Across CLO 2

#### 1. Processor Choice Is Not Only About Speed

A common mistake is writing that the "best" processor is the fastest processor. In SoC design, the better processor is the one that fits the complete system requirement.

Correct view:

```text
Processor choice = software compatibility + performance + real-time behavior
                 + memory support + interconnect support + power + area + cost.
```

Example:

- A Linux-capable application SoC may need a processor with MMU, caches and rich software ecosystem.
- A motor-control SoC may need a deterministic microcontroller or real-time core.
- A signal-processing SoC may need DSP/SIMD/vector support.
- A security or AI workload may need hardware accelerators in addition to CPU.

#### 2. Architecture, Microarchitecture And System Architecture Are Different

Do not mix these terms.

| Term | Meaning | Example |
|---|---|---|
| ISA / processor architecture | Software-visible processor contract | instructions, registers, exceptions |
| Microarchitecture | Internal implementation of ISA | pipeline, branch predictor, caches |
| System architecture | Whole SoC organization | CPU, memory hierarchy, NoC, accelerators |

Exam line:

```text
ISA decides what software sees; microarchitecture decides how the processor executes it; system architecture decides how the whole SoC is organized.
```

#### 3. Memory Is A System, Not One Block

Another common mistake is writing "memory = RAM." In SoC design, memory includes:

- processor registers,
- caches,
- TCM,
- scratchpad,
- SRAM,
- ROM,
- buffers,
- external DRAM,
- Flash/storage,
- memory-mapped peripheral registers.

Correct view:

```text
Memory hierarchy exists because no single memory gives best speed, capacity, power, area and cost.
```

#### 4. On-Die Memory Is Fast But Limited

On-die memory is physically inside the SoC die. It gives low latency and high local bandwidth, but it consumes silicon area.

Correct comparison:

```text
On-die SRAM/ROM/cache/TCM = fast, close, limited capacity.
Off-die DRAM/LPDDR        = large capacity, higher latency, controller required.
```

Do not say all memory should be on-chip. Large on-chip SRAM increases die area and can reduce yield. The local PPT also notes that DRAM process technology differs from normal processor logic technology, so dense DRAM is not always practical on a standard logic die.

#### 5. Simple DRAM Model Is A Simplification

In Topic 3, the simple DRAM cell and array are explained using row, column, word line, bit line, sense amplifier and refresh. That is correct for concept building.

But real DDR/LPDDR systems add:

- banks,
- ranks,
- channels,
- bursts,
- command/address timing,
- data strobes,
- training/calibration,
- refresh scheduling,
- signal integrity constraints.

Exam line:

```text
Simple DRAM explains the storage cell and array; DDR/LPDDR explains the practical high-speed interface and protocol.
```

#### 6. Processor-Memory Interaction Formula Is About Average Bandwidth

The model:

```text
B = m [1 - (1 - 1/m)^n]
```

does not mean every request completes with this exact speed. It estimates the average number of busy modules when `n` requests are randomly distributed across `m` independent modules.

Correct interpretation:

- `n` = number of request sources or outstanding requests,
- `m` = number of independent modules,
- `B` = average achieved bandwidth in requests per service time,
- contention prevents ideal scaling.

Do not write that bandwidth automatically equals `min(n, m)`. That is only the ideal case.

#### 7. Bus Is Not "Bad" And NoC Is Not Always "Better"

A bus is not obsolete. It is still practical for small SoCs and low-bandwidth peripheral regions.

Correct comparison:

```text
Bus = simple, low overhead, good for small/moderate systems.
NoC = scalable, packet-based, better for large parallel traffic.
```

NoC has overhead:

- routers,
- buffers,
- packetization,
- route computation,
- deadlock avoidance,
- verification complexity.

Therefore, the correct answer is not "NoC is faster." The correct answer is:

```text
NoC is more scalable under many-master traffic, but bus can be lower latency and lower area for small systems.
```

#### 8. Interconnect Is Not Just Wires

On-chip interconnect includes:

- address decoding,
- arbitration,
- routing,
- buffering,
- protocol conversion,
- width conversion,
- response handling,
- QoS,
- security/firewalls,
- clock-domain crossing,
- power-domain handling.

If you write only "interconnect means wires," the answer is incomplete.

#### 9. Coherency Is Conditional

Not every SoC interconnect is coherent.

Correct statement:

```text
Some high-performance multicore SoCs use coherent interconnects/protocols such as ACE or CHI.
Small microcontroller SoCs may be non-coherent and rely on software/cache maintenance.
```

Do not assume DMA always sees latest CPU cache data unless coherency or cache maintenance is handled.

#### 10. CLO 2 Is The Component Layer Between CLO 1 And CLO 3

CLO relationship:

| CLO | Main level | Relationship |
|---|---|---|
| CLO 1 | System approach and design flow | Explains why architecture and tradeoffs are needed |
| CLO 2 | SoC components and interconnection | Explains processors, memories and interconnect |
| CLO 3 | Memory design/controller architecture | Deepens memory technology, controller and scheduling |
| CLO 4 | Design methodologies | Explains TDD, BBD, PBD, HW/SW co-design and modeling |
| CLO 5 | Verification and testing | Checks that the design works and can be manufactured |

### Final CLO 2 Revision Diagram

Draw this when you need to connect the entire CLO:

```text
                SoC Components And Communication

 Software / firmware / drivers
              |
              v
        Processor cores
   CPU / MCU / DSP / ASIP
              |
              v
   On-chip interconnect
   bus / crossbar / NoC
      /        |        \
     v         v         v
  Memory   Peripherals  Accelerators
 cache     UART/SPI     AI/video/crypto
 SRAM      GPIO/timer   DSP datapath
 ROM
 DDR controller -> off-die DRAM
```

Why this figure is useful: it shows that CLO 2 is about the SoC building blocks and the communication paths among them.

### Common Exam Traps

1. **Trap**: "Architecture and microarchitecture are same."
   **Correct**: Architecture/ISA is software-visible; microarchitecture is internal implementation.

2. **Trap**: "Processor selection only depends on clock speed."
   **Correct**: It depends on software, performance, real-time needs, memory, interconnect, power, area and cost.

3. **Trap**: "Memory means only RAM."
   **Correct**: SoC memory includes registers, cache, SRAM, ROM, TCM, scratchpad, buffers, DRAM and storage.

4. **Trap**: "On-die memory is always better."
   **Correct**: It is faster but area-limited and costly per bit.

5. **Trap**: "DRAM can be read like a simple register."
   **Correct**: DRAM needs ACTIVATE, READ/WRITE, PRECHARGE and REFRESH timing.

6. **Trap**: "More memory modules always gives perfect bandwidth."
   **Correct**: Contention reduces achieved bandwidth.

7. **Trap**: "NoC is always faster than bus."
   **Correct**: Bus may be faster/smaller for small systems; NoC is better for scalability.

8. **Trap**: "Interconnect is only wires."
   **Correct**: It also includes protocol, arbitration, routing, buffering and QoS.

9. **Trap**: "DMA and CPU memory sharing is automatically correct."
   **Correct**: Coherency, cache maintenance, ordering and permissions must be handled.

10. **Trap**: "CLO2 topics are separate."
    **Correct**: Processor, memory and interconnect must be explained together for a strong SoC answer.

---

## CLO 2 Coverage Status

- [x] Topic 1: SoC Components - Core Logic, Processors, Choice Of Processors, Processor Architecture/Microarchitecture.
- [x] Topic 2: Memory Design Overview and SoC On-Die Memory Systems.
- [x] Topic 3: Board-Based Off-Die Memory Systems, Simple DRAM and the Memory Array.
- [x] Topic 4: Models of Simple Processor-Memory Interaction.
- [x] Topic 5: On-Chip Interconnect, Bus vs NoC and NoC Architectures.
- [x] Review addendum added for factual integration and common exam traps.
- [x] Full forms and definitions added.
- [x] Local PPT/book references separated into `sources/`.
- [x] Web references separated into `sources/`.
- [x] Exam diagrams added.
