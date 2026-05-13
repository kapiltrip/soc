# Sources - Memory Comparison: DRAM, SDRAM, DDR1, DDR2, DDR3, DDR4 And DDR5

## Topic

SDRAM Evolution - DRAM to DDR5 comparison.

## CLO Mapping

This supports the memory-design topics already mapped under **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

## Local Course Sources

- Topic image: [Screenshot 2026-05-13 090435.png](<../images/Screenshot 2026-05-13 090435.png>) contains the exact DRAM-to-DDR5 timeline supplied for comparison.
- Topic image: [Screenshot 2026-05-13 123031.png](<../images/Screenshot 2026-05-13 123031.png>) contains the Dynamic Memory Controller core-functions diagram: address multiplexing, RAS/CAS generation, refresh control, bus driver interface, bank/channel management and ECC management.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.167](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=167>) introduces SDRAM, DDR SDRAM and the DRAM row/column array structure.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.168](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=168>) explains DRAM cell storage, refresh, RAS, CAS and row/column multiplexing.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.169](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=169>) explains chip access time, chip cycle time and why the memory controller must obey timing.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.170](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=170>) explains page/nibble modes, burst transfer and SDRAM synchronization.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.171](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=171>) explains DDR SDRAM and double data transfer.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.172](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=172>) explains multiple DRAM arrays/banks, independently activated rows, interleaving and timing parameters.
- Lecture/PPT PDF: [module 1 part 1 introduction to system approach.pdf, p.20](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=20>) discusses large off-chip memory, MMU and cache hierarchy in SoC systems.
- Lecture/PPT PDF: [module 1 part 1 introduction to system approach.pdf, p.21](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=21>) explains that DRAM process technology differs from processor logic technology and that on-die memory capacity is limited.
- Lecture/PPT PDF: [module 1 part 1 introduction to system approach.pdf, p.22](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=22>) discusses processors using shared high-level caches and main memory.

## Web Sources

- [Micron DDR5 DRAM](https://www.micron.com/products/dram/ddr5-sdram): used for DDR4-vs-DDR5 comparison points such as data-rate ranges, 1.2 V to 1.1 V voltage change, 8n to 16n prefetch, DFE, on-die ECC, read/write CRC, bank groups/banks and BL16.
- [Micron DDR5 SDRAM: New Features white paper](https://www.micron.com/content/dam/micron/global/public/products/white-paper/ddr5-new-features-white-paper.pdf): used for DDR5 architectural changes, bank-group increase, BL16, same-bank refresh and performance/reliability details.
- [JEDEC DDR5 standard announcement via Business Wire](https://www.businesswire.com/news/home/20200714005727/en/JEDEC-Publishes-New-DDR5-Standard-for-Advancing-Next-Generation-High-Performance-Computing-Systems): used for the JESD79-5 DDR5 publication context and the point that DDR5 doubles burst length to BL16 and bank count to 32 from 16.
- [JEDEC JESD79-5 / DDR5 SDRAM summary via GlobalSpec](https://standards.globalspec.com/std/14328154/jedec-jesd-79-5): used to confirm the DDR5 standard scope and that it defines features, functionality, AC/DC characteristics, packages and ball/signal assignments.
- [Micron DRAM components](https://www.micron.com/products/memory/dram-components): used as a vendor source for DRAM generations and DDR5 resources.
- [Kingston DDR5 overview PDF](https://media.kingston.com/kingston/articles/MKF_954-DDR5-Collateral_us.pdf): used as a supporting source for DDR5 dual 32-bit subchannels, on-die ECC, PMIC, bank-count and burst-length improvements.

## Figure References

- For the comparison/timeline figure, use [Screenshot 2026-05-13 090435.png](<../images/Screenshot 2026-05-13 090435.png>).
- For the Dynamic Memory Controller core-functions figure, use [Screenshot 2026-05-13 123031.png](<../images/Screenshot 2026-05-13 123031.png>).
- For the DRAM row/column array and RAS/CAS concept, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.167](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=167>) to p.168.
- For burst access, timing and memory-controller behavior, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.169](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=169>) to p.172.

## Notes On Numbers

- DDR speed is best written in **MT/s - mega transfers per second**, not only MHz, because DDR transfers data on both clock edges.
- Exact voltage, timing and data-rate values vary by standard revision, speed bin and vendor product. The main note intentionally uses exam-level ranges and architecture trends rather than one exact datasheet bin.
