# CLO 2 Review Sources - Factual Integration And Exam Traps

Main note: [../CLO2.md](<../CLO2.md>)

## Local PPT / Book References

### 1. `System on chip/module 1 part 1 introduction to system approach.pdf`

Useful pages:

- p.2: Defines SoC architecture as an ensemble of processors, memories and interconnects. Used to connect all CLO2 topics together.
- p.20-p.25: Explains on-die/off-die memory choices, memory requirements and memory examples. Used to review the memory sections.
- p.31-p.35: Explains system-level interconnection, bus-based approach and Network-on-Chip approach. Used to review bus vs NoC and correct the "NoC is always better" misconception.
- p.39-p.43: Discusses design iteration, system architecture complexity, multiple processors, caches and interconnection. Used for the integrated SoC view.

### 2. `System on chip/SOC components -processor.pdf`

Useful pages:

- p.4: Says system performance can model memory and interconnect as delay elements. Used to connect processor performance to memory/interconnect performance.
- p.18: Says faster cache and memory reduce instruction/data fetch cycles. Used to review processor-memory interaction.

### 3. `System on chip/module 1 chip basics.pdf`

Useful pages:

- p.3-p.4: Lists time, area, power, reliability and configurability as major chip tradeoffs.
- p.7: Notes cache misses can create unanticipated extra cycles.
- p.10-p.13: Explains die area/yield and power, used for the on-die memory and PPA review.

### 4. `Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf`

Useful pages:

- p.20-p.24: Explains system components, hardware/software, and system architecture.
- p.76-p.96: Covers processor selection and processor/core architecture context.
- p.145-p.160: Covers on-die memory, off-die memory, DRAM and processor-memory interaction models.
- p.165-p.205: Covers interconnect, bus models, NoC, layered architecture, bus vs NoC and interconnect evaluation.

## Web References

### 1. Arm AMBA Specifications

URL: https://www.arm.com/architecture/system-architectures/amba/amba-specifications

Used for:

- AMBA protocol family and coherent/non-coherent interconnect context.
- AXI, AHB, APB, ACE and CHI terminology.

### 2. Cadence Janus NoC System IP

URL: https://www.cadence.com/en_US/home/tools/silicon-solutions/system-ip/cadence-janus-noc-100.html

Used for:

- NoC as configurable SoC connectivity fabric.
- Bandwidth, latency, clock-domain crossing, buffer/pipeline configuration and physical-design concerns.

### 3. AMD Integrated Memory Controller - Memory Interleaving

URL: https://docs.amd.com/r/en-US/pg456-integrated-mc/Memory-Interleaving

Used for:

- Practical example of interleaving across memory controllers.
- Supports processor-memory interaction model interpretation using independent modules/channels.

### 4. Micron - How DRAM Memory Works

URL: https://www.micron.com/educatorhub/courses/how-dram-memory-works

Used for:

- Practical DRAM cell/array explanation.
- Supports the review distinction between simple DRAM concept and real DRAM device behavior.

### 5. Synopsys - What is PPA?

URL: https://www.synopsys.com/glossary/what-is-power-performance-area-ppa.html

Used for:

- Power, Performance and Area as key silicon chip design metrics.
- Supports the review point that processor/memory/interconnect choices are PPA tradeoffs.

## Why This Review File Exists

CLO2 contains several long topics. This review source file supports the final addendum that connects those topics and prevents common factual mistakes in exams: confusing architecture and microarchitecture, treating memory as only RAM, assuming all SoCs are coherent, assuming NoC is always faster than bus, or using the processor-memory bandwidth formula as a perfect-bandwidth formula instead of an average-contention model.
