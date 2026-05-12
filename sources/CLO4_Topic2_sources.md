# Sources - CLO 4 Topic 2

## Topic

Hardware-Software Co-Design

## CLO Mapping

This maps to **CLO 4: Analyze the Design Methodologies of SoC; TLM and its need in SoC Design**.

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **Hardware-Software Co-Design** under the SoC Design Essentials section.
- Topic image: [Screenshot 2026-05-12 174733.png](<../images/Screenshot 2026-05-12 174733.png>) contains the exact syllabus headline **Hardware-Software Co-Design**.
- PPT: [Functional Architecture Co Design 2.pdf, p.2](<../System on chip/Functional Architecture Co Design 2.pdf#page=2>) explains ESL and why abstraction above RTL supports early exploration.
- PPT: [Functional Architecture Co Design 2.pdf, p.3](<../System on chip/Functional Architecture Co Design 2.pdf#page=3>) explains why RTL methods alone do not scale and why modern chips include both hardware and software.
- PPT: [Functional Architecture Co Design 2.pdf, p.5](<../System on chip/Functional Architecture Co Design 2.pdf#page=5>) defines HW/SW co-design as integrated design of systems using hardware and software components with performance goals and implementation technology.
- PPT: [Functional Architecture Co Design 2.pdf, p.6](<../System on chip/Functional Architecture Co Design 2.pdf#page=6>) lists co-design activities: characterizing hardware/software performance, identifying partitioning and synthesizing hardware/software.
- PPT: [Functional Architecture Co Design 2.pdf, p.8](<../System on chip/Functional Architecture Co Design 2.pdf#page=8>) explains HW/SW partitioning criteria such as dynamic properties, static execution-time differences and hardware cost.
- PPT: [Functional Architecture Co Design 2.pdf, p.10](<../System on chip/Functional Architecture Co Design 2.pdf#page=10>) gives co-design framework examples such as Ptolemy and Xilinx SDSoC/Zynq.
- PPT: [Functional Architecture Co Design 2.pdf, p.11](<../System on chip/Functional Architecture Co Design 2.pdf#page=11>) explains function-architecture co-design above RTL/C-code level and the use of functional and abstract architecture models.
- PPT: [Functional Architecture Co Design 2.pdf, p.12](<../System on chip/Functional Architecture Co Design 2.pdf#page=12>) explains top-down refinement from functional model to architectural model, transaction-level communication and RTL refinement.
- PPT: [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) explains the top-down approach using system-level models to analyze performance, partitioning and packaging.
- PPT: [Software_Design-in-SOC  and architectural .pdf, p.4](<../System on chip/Software_Design-in-SOC  and architectural .pdf#page=4>) explains embedded software layers, device drivers, RTOS and hardware/software interfaces.
- PPT: [Software_Design-in-SOC  and architectural .pdf, p.10](<../System on chip/Software_Design-in-SOC  and architectural .pdf#page=10>) shows multilayer SoC software architecture including application software, middleware, OS and HAL.
- PPT: [Software_Design-in-SOC  and architectural .pdf, p.12](<../System on chip/Software_Design-in-SOC  and architectural .pdf#page=12>) defines HAL as software directly dependent on the underlying hardware.
- PPT: [Software_Design-in-SOC  and architectural .pdf, p.14](<../System on chip/Software_Design-in-SOC  and architectural .pdf#page=14>) explains HAL usefulness for software portability and concurrent hardware/software design.
- PPT: [Software_Design-in-SOC  and architectural .pdf, p.19](<../System on chip/Software_Design-in-SOC  and architectural .pdf#page=19>) explains hardware/software definition, tradeoffs, partitioning and modeling at system level.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.23](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=23>) discusses the hardware/software tradeoff between programmability and performance.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.24](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=24>) discusses general-purpose processors, ASIPs, FPGAs and hardware/software implementation tradeoffs.

## Web / Standards Sources

- Web: [Accellera SystemC TLM Working Group](https://www.accellera.org/activities/working-groups/systemc-tlm) says TLM is important for architectural exploration, performance analysis, virtual platforms for software development and functional verification, and supports loosely-timed and approximately-timed modeling.
- Web: [SystemC.org SystemC Transaction Level Modeling overview](https://systemc.org/overview/systemc-tlm/) explains that TLM provides standard interfaces for model exchange, architecture analysis, software development, performance analysis and hardware verification. It also describes loosely timed and approximately timed modeling styles, temporal decoupling and direct memory interface.
- Web: [Accellera SystemC downloads](https://www.accellera.org/downloads/standards/systemc) lists SystemC releases including TLM and the IEEE SystemC standards, including IEEE Std. 1666-2023.
- Web: [Accellera TLM 2.0 whitepaper](https://accellera.org/images/downloads/standards/systemc/TLM2_Whitepaper.pdf) explains TLM APIs, memory-mapped bus modeling, loosely timed and approximately timed coding styles, direct memory interface and temporal decoupling.

## Figure References

- For HW/SW co-design definition and partitioning, use [Functional Architecture Co Design 2.pdf, p.5](<../System on chip/Functional Architecture Co Design 2.pdf#page=5>) and p.8.
- For ESL and function-architecture co-design, use [Functional Architecture Co Design 2.pdf, p.11](<../System on chip/Functional Architecture Co Design 2.pdf#page=11>) and p.12.
- For software layers including HAL and OS/RTOS, use [Software_Design-in-SOC  and architectural .pdf, p.10](<../System on chip/Software_Design-in-SOC  and architectural .pdf#page=10>) to p.14.
- For top-down system-level modeling and partitioning, use [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>).
