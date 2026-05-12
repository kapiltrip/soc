# CLO 2 Topic 2 Sources - Memory Design Overview and SoC On-Die Memory Systems

Main note: [../CLO2.md](<../CLO2.md>)

Topic image: [../images/Screenshot 2026-05-12 230100.png](<../images/Screenshot 2026-05-12 230100.png>)

Syllabus/CLO image: [../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>)

## Local PPT / Book References

### 1. `System on chip/module 1 part 1 introduction to system approach.pdf`

Useful pages:

- p.20: Explains that SoC applications may use on-chip ROM and RAM for smaller bounded programs, while larger systems may require off-chip memory, memory management and caches. Used in the main note to explain why memory organization depends on application size.
- p.20: Mentions that putting memory on the processor die improves access time and bandwidth. Used to support the on-die memory advantage.
- p.21: Explains practical problems of putting large memory on the processor die, including process differences and memory-size limitation. Used to support why all memory is not kept on-die.
- p.22: Shows the conventional model where main memory is off-die and higher-level cache structures are shared. Used for the hierarchy and off-die discussion.
- p.23: Explains that integrated memory SoCs are practical when the application has bounded memory size. Used to explain application-specific memory design.
- p.24: Discusses centralized and distributed memory and that memory may appear centralized to the programmer even if physically distributed. Used for the centralized/distributed on-die memory section.
- p.25-p.26: Contains SoC embedded memory examples and memory macro context. Used for on-die memory blocks and macro terminology.
- p.27-p.29: Discusses user view of memory, addressing, virtual memory, Memory Management Unit and Translation Lookaside Buffer. Used for the memory map/MMU/TLB section.
- p.31-p.32: Discusses bus hierarchy and memory/interconnect relation. Used to connect memory to SoC interconnect.
- p.39-p.42: Discusses sizing processor/memory/I/O for real-time constraints and design complexity. Used for memory sizing and tradeoff discussion.

### 2. `System on chip/module 1 chip basics.pdf`

Useful pages:

- p.3: Lists major design tradeoffs such as time, area and power. Used for the Power, Performance, Area style explanation.
- p.7: Mentions extra cycles from cache miss and cycle-time concepts. Used for memory latency and cache miss explanation.
- p.10-p.11: Discusses die area/yield concepts. Used for why large on-die memory increases cost and yield risk.
- p.13: Discusses dynamic and leakage power. Used for memory power discussion.

### 3. `Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf`

Useful pages:

- p.13: Frames storage as a SoC design decision involving size, volatility and on-die/off-die placement. Used for the memory hierarchy and memory technology overview.
- p.22: Lists basic SoC elements, including processors and memory. Used for CLO2 component mapping.
- p.37-p.43: Covers memory, addressing and interconnect basics. Used for memory map, address space and interconnect relation.
- p.65: Discusses cache memory as a major die-area/performance factor. Used for cache and area tradeoff explanation.
- p.145-p.160: Useful for on-die memory, cache hierarchy and memory-system organization context. Used for the deeper Level 1/Level 2/Level 3 cache, on-die memory and memory hierarchy explanation.

## Web References

### 1. AMD Versal Adaptive SoC Technical Reference Manual - Tightly Coupled Memories

URL: https://docs.amd.com/r/en-US/am011-versal-acap-trm/Tightly-coupled-Memories

Used for:

- TCM as low-latency memory for predictable instruction execution and data load/store timing.
- TCM being directly connected to processor TCM port interfaces.
- Typical TCM use for interrupt/exception code and data-intensive processing.
- TCM being memory-mapped through the system interconnect but low-latency through local processor access.

### 2. Cadence Artisan Foundation IP - Memory Compilers

URL: https://login.cadence.com/content/cadence-www/global/zh_CN/home/tools/silicon-solutions/artisan-ip.html

Used for:

- Embedded memory IP examples: SRAM, register files, ROM and MRAM.
- Memory compiler features such as single-port, two-port, dual-port, ROM compilers, configurable size/aspect ratio, ECC, redundancy, sleep/retention mode and built-in self-test/repair.
- Supporting the explanation that on-die memories are physical macros with ports, area, timing and power options.

### 3. Cadence Blog - Verifying SoC BootROM Using Standard Verification Techniques

URL: https://community.cadence.com/cadence_blogs_8/b/fv/posts/verifying-soc-bootrom-using-standard-verification-techniques-568647602

Used for:

- BootROM being common in SoC designs.
- Boot code needing to be available immediately after reset.
- On-chip ROM as a common location for early boot code.
- Secure boot and boot-flow complexity motivation.

### 4. Arm Learning Path - Cache Hierarchy And Performance Characteristics

URL: https://learn.arm.com/learning-paths/servers-and-cloud-computing/memory-subsystem/cache-hierarchy/

Used for:

- Cache hierarchy explanation: memory access is served by the closest level containing the data.
- L1 being small and fast, L2 larger and slower, and L3/system cache larger with higher latency.
- The concept that performance changes as the working set moves through cache levels and then to DRAM.
- The beginner explanation of cache levels, hit/miss behavior, working-set movement through Level 1/Level 2/Level 3 caches and why shared last-level cache reduces Dynamic Random Access Memory traffic.

### 5. Cadence Blog - DDR DRAMs In Memory Subsystem Designs

URL: https://community.cadence.com/cadence_blogs_8/b/ip/posts/squeeze-bandwidth-inefficiencies-out-of-ddr-drams-in-memory-subsystem-designs

Used for:

- On-chip memory being efficient for access and bandwidth.
- Distributed on-chip memory reducing memory-resource conflicts.
- On-chip embedded SRAM being much more expensive per bit than external SDRAM/DRAM.
- The memory controller needing to supply bandwidth/latency/quality-of-service to on-chip blocks that share external SDRAM.

## Why These Sources Were Used

This topic is a CLO2 component-level topic, so the main local source is the module 1 SoC introduction material, supported by Flynn/Luk for textbook-level SoC memory concepts. Web references were used only to make the definitions current and concrete: AMD for TCM, Cadence for memory compilers/BootROM/DRAM subsystem tradeoffs, and Arm for cache hierarchy behavior.
