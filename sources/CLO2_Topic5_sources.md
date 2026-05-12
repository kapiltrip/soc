# CLO 2 Topic 5 Sources - On-Chip Interconnect, Bus Vs NoC And NoC Architectures

Main note: [../CLO2.md](<../CLO2.md>)

Topic image: [../images/Screenshot 2026-05-12 230212.png](<../images/Screenshot 2026-05-12 230212.png>)

Syllabus/CLO image: [../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>)

## Local PPT / Book References

### 1. `System on chip/module 1 part 1 introduction to system approach.pdf`

Useful pages:

- p.2: Defines SoC architecture as an ensemble of processors, memories and interconnects tailored to an application domain. Used for the definition of on-chip interconnect as a core SoC component.
- p.31-p.32: Discusses bus hierarchy and memory/interconnect relation. Used for hierarchical bus and high-speed/low-speed bus explanation.
- p.39-p.42: Discusses sizing processor, memory and I/O for real-time constraints and architecture complexity. Used for interconnect bandwidth/latency tradeoffs.

### 2. `System on chip/SOC components -processor.pdf`

Useful pages:

- p.4: Says system performance can model memory and interconnect as delay elements. Used to explain why interconnect delay affects SoC performance.
- p.18: Says faster cache and memory reduce instruction/data fetch cycles. Used to connect processor performance to interconnect and memory traffic.

### 3. `System on chip/Functional Architecture Co Design 2.pdf`

Useful pages:

- p.16: Lists architecture modeling components such as microprocessors, microcontrollers, DSPs, buses, memories, peripherals, RTOS and hardware processing units. Used to show buses/interconnects as architectural elements.

### 4. `System on chip/14-SOC Design Methodologies.pdf`

Useful pages:

- p.18: Lists platform-based design linchpin technologies including system-level architectural tools, hardware/software co-design, bus planning and VC verification. Used to support bus/interconnect planning as a design-methodology concern.

### 5. `Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf`

Useful pages:

- p.37-p.43: Covers memory, addressing and interconnect basics. Used for address decoding and memory-mapped communication.
- p.46: Discusses real-time/throughput constraints and processor-memory-interconnect performance. Used for latency/bandwidth reasoning.
- p.96: Mentions processor core selection context including configurable caches, bus architectures and custom instructions/coprocessors. Used for bus architecture as part of SoC design.
- p.193: Mentions AMBA/on-chip bus context in SoC test access. Used as supporting course-book context that AMBA-style buses are used as SoC infrastructure.

### 6. Existing Related Notes

- [../CLO3.md](<../CLO3.md>) Topic 5 discusses the memory controller receiving requests through AXI/AHB/NoC style interconnects.
- [../CLO4.md](<../CLO4.md>) Topic 1 and Topic 4 discuss platform-based design, architectural modeling and bus/interconnect planning.

## Web References

### 1. Arm AMBA Specifications

URL: https://www.arm.com/architecture/system-architectures/amba/amba-specifications

Used for:

- AMBA defining interfaces and protocols for on-chip and off-chip use.
- AMBA 5 including CHI and AXI.
- Official list of AMBA protocols such as CHI, AXI, ACE, AHB, AXI-Stream and APB.

### 2. Arm Learn The Architecture - Introduction To AMBA AXI

URL: https://documentation-service.arm.com/static/6800e9e95b1a8c5a27aa1a59

Used for:

- AMBA as an open-standard on-chip interconnect specification for connecting and managing functional blocks in SoC designs.
- AMBA protocols defining how functional blocks communicate.
- IP reuse, compatibility and flexibility benefits.
- Bandwidth and latency as core bus-interface performance characteristics.
- AXI transactions, burst transactions and transaction IDs/out-of-order support.

### 3. Cadence Janus NoC System IP

URL: https://www.cadence.com/en_US/home/tools/silicon-solutions/system-ip/cadence-janus-noc-100.html

Used for:

- NoC as a highly configurable network-on-chip IP for complex SoC connectivity.
- Increasing connectivity-fabric complexity in modern systems.
- Configurable bandwidth, latency, clock-domain crossing, clock gating, buffer size and pipeline stages.
- Reduced wire count, reduced congestion and reduced physical-design issues.
- Subsystem-to-full-SoC and chiplet scalability context.

### 4. Intel / Altera Arria 10 HPS System Interconnect Documentation

URL: https://www.intel.com/content/www/us/en/docs/programmable/683711/21-2/system-interconnect-39578.html

Used for:

- Real SoC documentation structure showing system interconnect, master-to-slave connectivity, SDRAM connections, system interconnect architecture, arbitration and QoS.
- Supporting the explanation that practical interconnects include address spaces, clocks, resets, firewalls, rate adapters and QoS/arbitration.

### 5. Benini and De Micheli - Networks on Chips: A New SoC Paradigm

URL: https://www.researchgate.net/publication/2955567_Networks_on_Chips_A_new_SoC_paradigm

Used for:

- Classic NoC research context.
- On-chip physical interconnections becoming limiting factors for performance and energy.
- Layered on-chip micronetwork methodology.
- NoC as a way to provide reliable operation among interacting SoC components.
- Component-based and plug-and-play SoC design motivation.

### 6. Dally and Towles - Route Packets, Not Wires: On-Chip Interconnection Networks

URL: https://ieeexplore.ieee.org/document/935594

Used for:

- Classic packet-based on-chip interconnection network idea.
- The core NoC intuition: route packets through an on-chip network instead of relying on many global wires.
- Packet/flit/router style terminology and packet-switched interconnect motivation.

## Why These Sources Were Used

The local PPT/book material maps the topic to CLO 2 and supports the SoC architecture/interconnect role. Arm AMBA sources support bus/interface standards such as AXI, AHB, APB and CHI. Cadence and Intel documentation support modern industrial NoC/interconnect features such as configurable bandwidth/latency, clock-domain crossing, QoS and arbitration. Benini-De Micheli and Dally-Towles provide the classic research basis for NoC as a scalable packet-based alternative to global wiring.
