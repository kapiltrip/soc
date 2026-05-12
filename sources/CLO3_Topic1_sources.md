# Sources - CLO 3 Topic 1

## Topic

SoC Memory Design: Memory Technology

## CLO Mapping

This maps to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **SoC Memory Design: Memory Technology** under the memory-design part of the syllabus.
- Topic image: [Screenshot 2026-05-12 124230.png](<../images/Screenshot 2026-05-12 124230.png>) contains the exact topic headline.
- Related next-topic image: [Screenshot 2026-05-12 124327.png](<../images/Screenshot 2026-05-12 124327.png>) contains **Memory design Hierarchy and Tradeoffs**, which is related but should be treated as the next topic if asked separately.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.13](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=13>) shows storage as a key SoC design decision: size, volatility and on-die/off-die placement.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.22](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=22>) shows SoC systems as heterogeneous processors connected to one or more memory elements.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.146](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=146>) discusses how much memory can be put on a die, eDRAM area and scratchpad/cache memory.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.147](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=147>) discusses scratchpads, caches and locality.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.148](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=148>) explains cache miss rate, miss penalty and why cache is an important SoC memory-hierarchy component.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.157](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=157>) lists cache types and notes that cache storage is built from SRAM cells.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.158](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=158>) gives size/access-time limits for L1/L2/L3 cache arrays.
- Lecture: [module 1 part 1 introduction to system approach.pdf, p.20](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) explains that SoC applications vary from on-chip ROM/RAM systems to OS-based systems using off-chip memory, MMU and cache hierarchy.
- Lecture: [module 1 part 1 introduction to system approach.pdf, p.21](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=21>) explains that DRAM process technology differs from microprocessor process technology and that on-die memory capacity is limited.
- Lecture: [module 1 part 1 introduction to system approach.pdf, p.22](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=22>) explains the conventional model of multiple processors sharing high-level caches with main memory off-die.
- Lecture: [module 1 part 1 introduction to system approach.pdf, p.25](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=25>) says SoC designers must consider whether RAM and ROM should be on-die or off-die.
- Lecture: [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>) says every processor has a memory system and faster cache/memory reduces instruction/data fetch cycles.
- Lecture: [understanding IP.pdf, p.4](<../System on chip/understanding IP.pdf#page=4>) mentions SRAM as a hard IP example and links memory choice to physical optimization and timing.

## Web Sources

- [JEDEC home / technology focus areas](https://www.jedec.org/): official standards-body source listing main memory focus areas such as DDR SDRAM and HBM, flash memory focus areas such as UFS and e.MMC, and mobile memory focus areas such as LPDDR.
- [Micron DDR5 DRAM](https://in.micron.com/products/memory/dram-components/ddr5-sdram): official DRAM/DDR5 source for bandwidth, density, voltage and feature differences.
- [Micron LPDDR](https://www.micron.com/products/memory/dram-components/lpddr): official source defining LPDDR as low-power double-data-rate memory and explaining lower-voltage / power-conscious use cases for mobile, automotive and embedded systems.
- [Micron NAND flash memory types](https://www.micron.com/products/storage/nand-flash/choosing-the-right-nand): official source for SLC/MLC/TLC/QLC NAND, low cost per bit, ECC, bad-block management, wear leveling, managed NAND, e.MMC and UFS.
- [Micron NOR flash](https://www.micron.com/products/storage/nor-flash): official source for NOR flash use in reliable code storage, boot, OS/application code and execute-in-place (XIP) embedded-system applications.
- [Infineon memories portfolio](https://www.infineon.com/products/memories): official source listing SRAM, NOR flash, pSRAM, nvSRAM and F-RAM families.
- [Infineon synchronous SRAM](https://www.infineon.com/products/memories/sram-static-ram/synchronous-sram): official source for high-speed SRAM, QDR SRAM, random transaction rate, low-latency networking, packet lookup/classification and packet-buffer style applications.
- [Linux kernel ARM TCM documentation](https://docs.kernel.org/arch/arm/tcm.html): technical source explaining that some ARM SoCs have TCM - Tightly Coupled Memory, with ITCM and DTCM often embedded inside the CPU. Used to support the TCM definition and on-chip real-time memory explanation.

## Figure References

- For a course figure showing storage as a SoC design decision, look at [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.13](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=13>).
- For on-die/off-die memory discussion, look at [module 1 part 1 introduction to system approach.pdf, p.20](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) to p.22.
- For cache/scratchpad memory context, look at [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.146](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=146>) to p.158.
