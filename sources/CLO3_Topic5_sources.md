# Sources - CLO 3 Topic 5

## Topic

Memory Controller

## CLO Mapping

This maps to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **Memory Controller** under **SoC Memory Design**, which maps to CLO 3.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.169](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=169>) shows an asynchronous DRAM memory module with dynamic memory controller, memory timing controller, memory chips and bus drivers.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.169](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=169>) says the dynamic memory controller multiplexes address bits into row and column addresses.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.170](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=170>) says the memory controller creates correct RAS/CAS signals and provides timely refresh.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.173](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=173>) shows SDRAM channels and controller.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.174](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=174>) discusses memory controller managing channels and memory buffers.
- PPT/lecture PDF: [module 1 part 1 introduction to system approach.pdf, p.20](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) mentions large off-chip memory, MMU and cache hierarchy in SoC systems.
- PPT/lecture PDF: [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>) says every processor has a memory system and faster cache/memory reduces instruction/data fetch cycles.

## Web Sources

- [AMD DDR Memory Controller documentation](https://docs.amd.com/r/en-US/pg313-network-on-chip/DDR-Memory-Controller): official AMD documentation for integrated DDR memory controller and QoS configuration context.
- [AMD Integrated Memory Controller - Memory Interleaving](https://docs.amd.com/r/en-US/pg456-integrated-mc/Memory-Interleaving): official AMD documentation explaining memory interleaving across DDR controllers and bandwidth effects.
- [Intel DRAM Burst Scheduling](https://www.intel.com/content/www/us/en/docs/programmable/683841/17-0/dram-burst-scheduling.html): official Intel documentation showing DRAM burst scheduler arbitration and bank behavior.
- [Arm AMBA Specifications](https://www.arm.com/architecture/system-architectures/amba/amba-specifications): official Arm page for AXI/ACE/CHI interconnect protocols used by SoC masters to reach memory controllers.

## Figure References

- For a memory-controller block diagram, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.169](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=169>) because it shows the dynamic memory controller, timing controller, memory chip and bus drivers.
- For SDRAM channels and controller, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.173](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=173>).

