# Sources - CLO 3 Topic 2

## Topic

Memory Design Hierarchy and Tradeoffs

## CLO Mapping

This maps to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

## Local Course Sources

- Topic image: [Screenshot 2026-05-12 124327.png](<../images/Screenshot 2026-05-12 124327.png>) contains the exact topic headline **Memory design Hierarchy and Tradeoffs**.
- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) places this under **SoC Memory Design**, which maps to CLO 3.
- PPT/lecture PDF: [module 1 part 1 introduction to system approach.pdf, p.20](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) says SoC applications vary significantly in memory requirements, from on-chip ROM/RAM to large off-chip memory with MMU and cache hierarchy; it also lists advantages of on-die memory: improved access time, bandwidth and memory-intensive performance.
- PPT/lecture PDF: [module 1 part 1 introduction to system approach.pdf, p.21](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=21>) explains limitations of on-die memory: DRAM process mismatch with processor logic and limited capacity.
- PPT/lecture PDF: [module 1 part 1 introduction to system approach.pdf, p.22](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=22>) explains the conventional model of processors sharing higher levels of two- or three-level cache structures with main memory off-die.
- PPT/lecture PDF: [module 1 part 1 introduction to system approach.pdf, p.25](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=25>) says SoC designers must consider whether RAM and ROM should be on-die or off-die.
- PPT/lecture PDF: [module 1 chip basics.pdf, p.7](<../System on chip/module 1 chip basics.pdf#page=7>) explains cycle time and notes that cache misses can add unexpected extra cycles.
- PPT/lecture PDF: [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>) says every processor has a memory system and faster cache/memory reduces instruction fetch and data fetch cycles.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.13](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=13>) shows storage decisions as part of SoC design: size, volatility and on-die/off-die placement.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.37](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=37>) discusses SoC memory/addressing and states that SoC applications vary significantly in memory requirements.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.39](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=39>) provides SoC memory considerations including memory placement, addressing and operating-system implications.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.146](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=146>) discusses on-die memory capacity, scratchpads and cache memory.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.147](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=147>) explains scratchpad memory, cache memory and locality.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.148](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=148>) explains cache hit/miss behavior, miss rate and miss penalty.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.157](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=157>) lists common cache types including unified, split I/D, sectored and multilevel cache.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.158](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=158>) discusses L1/L2/L3 cache array size and access-time limits.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.159](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=159>) explains two-level cache behavior, local/global/solo miss rates and L1-L2-memory hierarchy.

## Web Sources

- [Intel OpenCL SDK Developer Guide - Memory Hierarchy](https://www.intel.com/content/www/us/en/docs/opencl-sdk/developer-guide-processor-graphics/2019-4/memory-hierarchy.html): official Intel source showing a SoC memory hierarchy including local/shared memory, LLC/eDRAM and system DRAM.
- [Arm Learning Path - Cache hierarchy and performance characteristics](https://learn.arm.com/learning-paths/servers-and-cloud-computing/memory-subsystem/cache-hierarchy/): official Arm learning material explaining cache hierarchy and how memory access is satisfied by the closest level containing data.
- [Intel - Memory Performance in a Nutshell](https://www.intel.com/content/www/us/en/developer/articles/technical/memory-performance-in-a-nutshell.html): official Intel technical article explaining memory latency, bandwidth and performance effects.
- [Linux Kernel Documentation - ARM TCM](https://docs.kernel.org/arch/arm/tcm.html): explains tightly coupled memory and why deterministic timing can be required for interrupt handlers and real-time code.

## Figure References

- For the **on-chip/off-chip hierarchy diagram**, use [module 1 part 1 introduction to system approach.pdf, p.20](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22.
- For the **cache hierarchy diagram**, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.159](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=159>) which shows a two-level cache: processor, L1, L2 and memory.
- For the **tradeoff explanation**, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.146](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=146>) to p.158 and [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>).

