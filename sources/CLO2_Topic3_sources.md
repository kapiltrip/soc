# CLO 2 Topic 3 Sources - Board-Based Off-Die Memory Systems, Simple DRAM And The Memory Array

Main note: [../CLO2.md](<../CLO2.md>)

Topic image: [../images/Screenshot 2026-05-12 230119.png](<../images/Screenshot 2026-05-12 230119.png>)

Syllabus/CLO image: [../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>)

## Local PPT / Book References

### 1. `System on chip/module 1 part 1 introduction to system approach.pdf`

Useful pages:

- p.20: Discusses cases where program/data can fit in on-chip ROM/RAM versus systems needing large off-chip memory, memory management and cache hierarchy. Used to explain why board/off-die memory exists.
- p.21: Explains problems of putting large memory on the processor die, including process mismatch and limited memory size. Used to justify off-die DRAM.
- p.22: Shows the conventional model where processors share higher-level cache and main memory is off-die. Used for the board-based/off-die memory organization.
- p.24: Discusses centralized and distributed memories. Used to connect off-die memory to the larger memory-system organization.
- p.25: Says SoC designers must consider RAM/ROM on-die or off-die. Used to map the topic to SoC component design.
- p.31-p.32: Discusses interconnect hierarchy and bandwidth near the processor. Used to explain how memory traffic flows through SoC interconnect.

### 2. `Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf`

Useful pages:

- p.13: Presents storage as a SoC design decision involving size, volatility and on-die/off-die placement. Used for the overall memory-placement discussion.
- p.167: Introduces SDRAM and DRAM row/column organization. Used for the simple DRAM and memory-array explanation.
- p.168: Explains DRAM cells, refresh, row/column multiplexing and RAS/CAS style access. Used for word line, bit line, refresh and access-sequence explanation.
- p.169: Shows a DRAM module/controller style figure and memory access timing ideas. Used for controller and timing explanation.
- p.171-p.172: Explains DDR SDRAM internal organization, arrays/banks and independently activated rows. Used for bank and row-buffer discussion.
- p.173: Shows SDRAM channels/controller context. Used for board/off-die connection and controller relationship.
- p.179: Discusses off-die memory access overhead and need for cache hierarchy. Used for the latency/capacity tradeoff.

### 3. Existing Related Notes

- [../CLO3.md](<../CLO3.md>) Topic 3 has detailed SDRAM banked architecture and latency explanation.
- [CLO3_Topic3_sources.md](<CLO3_Topic3_sources.md>) has local source pointers for SDRAM row/column/bank timing.

## Web References

### 1. Micron - How DRAM Memory Works

URL: https://www.micron.com/educatorhub/courses/how-dram-memory-works

Used for:

- DRAM as a key memory technology.
- DRAM architecture basics.
- DRAM arrays using repeated capacitor/transistor storage structures.
- Simple explanation of how DRAM stores and accesses data.

### 2. Micron - DDR SDRAM Product Documentation

URL: https://www.micron.com/products/memory/dram-components/ddr-sdram

Used for:

- DDR SDRAM as a real off-die DRAM component family.
- DDR memory requiring system power and technical design resources.
- Reinforces that external memory is a board/system design component, not only a logic block.

### 3. Micron - DDR5 DRAM

URL: https://my.micron.com/products/memory/dram-components/ddr5-sdram

Used for:

- DDR DRAM terms such as bank groups/banks, command/address interface, ODT, burst length and refresh commands.
- Board/system-level concerns such as timing robustness, signaling and bandwidth.
- Supporting the technical words DQ, DQS, CA, ODT, bank and refresh.

### 4. JEDEC

URL: https://www.jedec.org/

Used for:

- JEDEC as the standards body for main memory technologies such as DDR SDRAM, HBM, LPDDR, eMMC and UFS.
- Supporting that DDR-style board memories are standardized industry interfaces.

### 5. Cadence Blog - DDR DRAMs In Memory Subsystem Designs

URL: https://community.cadence.com/cadence_blogs_8/b/ip/posts/squeeze-bandwidth-inefficiencies-out-of-ddr-drams-in-memory-subsystem-designs

Used for:

- Explaining the tradeoff between efficient on-chip memory and external SDRAM capacity/cost.
- The need for memory-controller bandwidth, latency and quality-of-service handling.
- Distributed on-chip memory versus shared external memory resource conflicts.

## Why These Sources Were Used

This topic needs both physical SoC placement and DRAM-array understanding. The local PPT explains the on-die/off-die SoC design decision. Flynn/Luk gives the textbook DRAM row/column/bank foundation. Micron and JEDEC provide current industry context for DDR/DRAM memories, while Cadence supports the system-level memory-subsystem tradeoff.
