# CLO 1 Topic 1 Sources - Systems Approach, System Architecture, Components, Hardware/Software And Chip Basics

Main note: [../CLO1.md](<../CLO1.md>)

Topic image part 1: [../images/Screenshot 2026-05-12 231802.png](<../images/Screenshot 2026-05-12 231802.png>)

Topic image part 2: [../images/Screenshot 2026-05-12 231845.png](<../images/Screenshot 2026-05-12 231845.png>)

Syllabus/CLO image: [../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>)

## Local PPT / Book References

### 1. `System on chip/module 1 part 1 introduction to system approach.pdf`

Useful pages:

- p.1: Introduces the module topic as **Introduction to System Approach**.
- p.2: Defines SoC architecture as an ensemble of processors, memories and interconnects tailored to an application domain. Also says architecture denotes operational structure and user view, and system architecture defines building blocks and interconnection.
- p.3: States that a fundamental SoC design decision is choosing which components are implemented in hardware and which in software.
- p.4: Explains that software on a GPP gives flexibility/adaptability and resource sharing, but instruction fetch/decode overhead can make it slower and more power-hungry than direct hardware for the same function.
- p.5: Explains combining hardware and software benefits; performance-critical parts can be implemented in hardware and the rest in software. It also uses the common idea that if 90% of execution time is spent in 10% of code, accelerating that part can give major speedup.
- p.6-p.7: Introduces ASIPs and FPGAs as middle options between software on GPP and fixed custom hardware.
- p.20-p.25: Discusses SoC memory requirements, on-die/off-die memory choices and the importance of memory in system architecture.
- p.31-p.35: Discusses system-level interconnection, bus-based approach and Network-on-Chip approach.
- p.36-p.40: Explains requirements/specifications and design iteration from initial design to optimized design.
- p.41-p.43: Explains system architecture complexity, multiple processors, caches, memory consistency and design reuse/interconnection.
- p.44: Discusses design complexity and use of predesigned components/reconfigurable devices.

### 2. `System on chip/module 1 chip basics.pdf`

Useful pages:

- p.1: Introduces chip basics: time, area, power, reliability and configurability.
- p.2: Explains cost/performance as a fundamental system design tradeoff and notes technology advancement as a driver.
- p.3-p.4: Lists five basic design tradeoffs: time, area, power, reliability and configurability.
- p.5-p.6: Connects SoC requirements to tradeoffs such as high performance, low cost, low power and reliability.
- p.7-p.9: Explains cycle time, cycles and pipelining. Notes that cache misses can add unexpected extra cycles.
- p.10-p.12: Explains die area, cost and yield. Large chips require defect-free area and may have low yield.
- p.13: Explains power and its two major sources: dynamic/switching power and static/leakage power.
- p.14-p.15: Discusses reliability/dependability and fault tolerance.
- p.16: Discusses configurability and why reconfigurable designs such as FPGAs can help manage risk and fabrication delay.

### 3. `Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf`

Useful pages:

- p.19: Chapter 1 begins **Introduction to the Systems Approach** and explains system architecture and design as distinct from only processor/memory details.
- p.20-p.22: Explains system architecture, system components, processors, memories and interconnects, and a high-level functional view of an SoC.
- p.23-p.24: Discusses hardware and software tradeoffs: programmability versus performance, GPP flexibility, custom hardware and intermediate technologies.
- p.41-p.43: The chapter contents and text connect SoC design approach to requirements, design iteration, system architecture and complexity.
- p.47-p.50: Discusses die area, cost, yield and defect probability.
- p.57-p.60: Discusses power, dynamic/switching and leakage components, and area-time-power tradeoffs.
- p.62: Discusses reliability as dependability/fault tolerance and relates it to die area, clock frequency and power.

Review-addendum use:

- The CLO1 full-form review addendum uses the local module 1 slides p.2-p.5 for System on Chip architecture, hardware/software partitioning and component roles.
- It uses p.20-p.35 for memory/interconnect examples such as SRAM, DRAM, ROM, buses and Network on Chip.

## Web References

### 1. NASA Systems Engineering Handbook - Fundamentals of Systems Engineering

URL: https://www.nasa.gov/reference/2-0-fundamentals-of-systems-engineering/

Used for:

- Systems engineering as a methodical, multidisciplinary approach.
- A system as a combination of elements working together to produce required capability.
- System elements including hardware, software, equipment, facilities, personnel, processes and procedures.
- Systems engineering focusing on the big picture, requirements, tradeoffs, interfaces, verification and validation.
- The systems engineer role in defining boundaries, allocating requirements and evaluating design tradeoffs.

### 2. ISO/IEC/IEEE 42010 Architecture Definition Page

URL: https://www.iso-architecture.org/ieee-1471/defining-architecture.html

Used for:

- Architecture as fundamental concepts/properties of a system in its environment, embodied in elements, relationships and design/evolution principles.
- Supporting the distinction between architecture as high-level organization and implementation as detailed realization.

### 3. Synopsys - What is PPA?

URL: https://www.synopsys.com/glossary/what-is-power-performance-area-ppa.html

Used for:

- PPA as Power, Performance and Area in silicon chip design.
- Power, performance and area as key design quality/efficiency metrics.
- Practical tradeoff: improving performance may increase power or area, while reducing area or power may reduce performance.

### 4. Semiconductor Industry Association - Semiconductor FAQ

URL: https://www.semiconductors.org/semiconductors-101/frequently-asked-questions/

Used for:

- Semiconductor manufacturing on wafers.
- ICs/chips being formed in many copies on a wafer.
- Wafer fabrication steps such as oxidation, patterning, etching, doping and metallization.
- Testing, rejecting bad chips and packaging good chips.
- Wafer/die/yield context used in chip basics.

## Why These Sources Were Used

The local module 1 slides directly match the syllabus headline. The Flynn/Luk textbook gives the deeper explanation of the systems approach, components, hardware/software tradeoffs and chip basics. NASA gives a general engineering source for systems approach, Synopsys gives current industry wording for PPA, and SIA gives factual semiconductor manufacturing/yield context.
