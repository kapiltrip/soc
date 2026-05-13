# Sources - CLO 4 Topic 1

## Topic

SoC Design Essentials: Design Methodologies - TDD, BBD and PBD

## CLO Mapping

This maps to **CLO 4: Analyze the Design Methodologies of SoC; TLM and its need in SoC Design**.

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **SoC Design Essentials: Design Methodologies - TDD, BBD, PBD, Hardware-Software Co-Design, Codesign vs Co-simulation, Architectural models** and maps the design-methodology content to CLO 4.
- Topic image: [Screenshot 2026-05-12 174644.png](<../images/Screenshot 2026-05-12 174644.png>) contains **SoC Design Essentials: Design Methodologies - TDD**.
- Topic image: [Screenshot 2026-05-12 174710.png](<../images/Screenshot 2026-05-12 174710.png>) contains **BBD, PBD**.
- PPT: [14-SOC Design Methodologies.pdf, p.2](<../System on chip/14-SOC Design Methodologies.pdf#page=2>) defines SoC as a system on an IC integrating software and hardware IP using more than one design methodology.
- PPT: [14-SOC Design Methodologies.pdf, p.3](<../System on chip/14-SOC Design Methodologies.pdf#page=3>) explains the evolution from area-driven design to timing-driven design, block-based design and platform-based design.
- PPT: [14-SOC Design Methodologies.pdf, p.5](<../System on chip/14-SOC Design Methodologies.pdf#page=5>) lists **Timing Driven Design (TDD)**, **Block Based Design (BBD)** and **Platform Based Design (PBD)** as the primary design methods.
- PPT: [14-SOC Design Methodologies.pdf, p.6](<../System on chip/14-SOC Design Methodologies.pdf#page=6>) defines **linchpin technology** as indispensable procedures/rules vital to a design process.
- PPT: [14-SOC Design Methodologies.pdf, p.7](<../System on chip/14-SOC Design Methodologies.pdf#page=7>) explains Timing Driven Design and its relation to moderately sized ASICs, new logic and timing/power constraints.
- PPT: [14-SOC Design Methodologies.pdf, p.8](<../System on chip/14-SOC Design Methodologies.pdf#page=8>) lists TDD linchpin technologies including interactive floorplanning and static timing analysis.
- PPT: [14-SOC Design Methodologies.pdf, p.10](<../System on chip/14-SOC Design Methodologies.pdf#page=10>) lists TDD benefits and challenges.
- PPT: [14-SOC Design Methodologies.pdf, p.11](<../System on chip/14-SOC Design Methodologies.pdf#page=11>) introduces Block Based Design and explains system-level behavior, hardware/software tradeoffs and mapping into RTL blocks with timing, power and area constraints.
- PPT: [14-SOC Design Methodologies.pdf, p.12](<../System on chip/14-SOC Design Methodologies.pdf#page=12>) explains BBD block-level floorplanning and budgets.
- PPT: [14-SOC Design Methodologies.pdf, p.13](<../System on chip/14-SOC Design Methodologies.pdf#page=13>) lists symptoms indicating BBD is appropriate, including subsystem complexity, multiple teams and interface timing errors.
- PPT: [14-SOC Design Methodologies.pdf, p.14](<../System on chip/14-SOC Design Methodologies.pdf#page=14>) lists BBD linchpin technologies including high-level system algorithmic analysis and integrated synthesis/physical design.
- PPT: [14-SOC Design Methodologies.pdf, p.16](<../System on chip/14-SOC Design Methodologies.pdf#page=16>) introduces Platform Based Design as reuse-oriented and hierarchical.
- PPT: [14-SOC Design Methodologies.pdf, p.17](<../System on chip/14-SOC Design Methodologies.pdf#page=17>) explains PBD separation into block authoring/creation and system-chip integration.
- PPT: [14-SOC Design Methodologies.pdf, p.18](<../System on chip/14-SOC Design Methodologies.pdf#page=18>) lists PBD linchpin technologies including system-level architectural tools, hardware/software co-design, bus planning and VC verification.
- PPT: [14-SOC Design Methodologies.pdf, p.20](<../System on chip/14-SOC Design Methodologies.pdf#page=20>) compares TDD, BBD and PBD.
- PPT: [SOC Design Flow.pdf, p.2](<../System on chip/SOC Design Flow.pdf#page=2>) explains SoC design-flow pressure from design size, deep sub-micron effects and shorter predictable implementation time.
- PPT: [SOC Design Flow.pdf, p.3](<../System on chip/SOC Design Flow.pdf#page=3>) explains bottom-up design flow and the risk of late system-level design errors.
- PPT: [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) explains top-down design with system-level models, performance tradeoff analysis, partitioning and early system-level verification.
- PPT: [SOC Design Flow.pdf, p.5](<../System on chip/SOC Design Flow.pdf#page=5>) explains that top-down design helps discover and manage system-level issues up front and supports reuse/re-verification for related products.
- PPT: [SOC Design Flow.pdf, p.6](<../System on chip/SOC Design Flow.pdf#page=6>) lists top-down principles including HDL/high-level models, early system-level verification, DFT strategy and consistent logical/physical design data flow.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.44](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=44>) explains SoC requirements and specifications as the start of system design.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.45](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=45>) explains design iteration and initial/straw-man design.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.48](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=48>) explains that system architecture adds complexity and reuse helps manage it.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.52](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=52>) discusses design cost/complexity tradeoffs and design reuse.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.53](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=53>) discusses hard, firm and soft IP and reuse tradeoffs.

Review-addendum use:

- The CLO4 full-form review addendum uses `14-SOC Design Methodologies.pdf` p.5-p.20 for the deeper TDD, BBD and PBD distinctions.
- It uses `SOC Design Flow.pdf` p.4-p.6 for top-down modeling, early verification and DFT strategy context.
- It uses the Flynn/Luk textbook p.44-p.53 for requirements, design iteration, reuse and IP tradeoffs.

## Web / Standards Sources

- Web: [Accellera IP-XACT downloads](https://www.accellera.org/downloads/standards/ip-xact) provides the official Accellera page for IP-XACT, the IEEE 1685 standard for IP metadata and integration descriptions. This supports the PBD explanation that platform reuse benefits from standardized IP packaging and integration information.
- Web: [Arm AMBA specifications](https://www.arm.com/architecture/system-architectures/amba/amba-specifications) provides the official Arm page for AMBA interface specifications. This supports the explanation that standard SoC bus protocols such as AXI/APB make platform and IP integration more predictable.
- Web/research: [Design-Reuse, Defining platform-based design](https://www.design-reuse.com/article/56860-defining-platform-based-design/) explains platform-based design as abstraction layers/platform stacks, highlights reuse, time-to-market pressure, NRE cost and hardware/software platform examples. This supports the platform-stack and derivative-product explanation.
- Web/research: [EURASIP Journal on Embedded Systems, A Platform-Based Methodology for System-Level Mixed-Signal Design](https://jes-eurasipjournals.springeropen.com/articles/10.1155/2010/261583) explains PBD as a meet-in-the-middle system-level methodology that assembles new designs from precharacterized library components and prioritizes design reuse, correct assembly and efficient flow from specification to implementation.

## Figure References

- For methodology evolution, use [14-SOC Design Methodologies.pdf, p.3](<../System on chip/14-SOC Design Methodologies.pdf#page=3>).
- For TDD/BBD/PBD as the main three methods, use [14-SOC Design Methodologies.pdf, p.5](<../System on chip/14-SOC Design Methodologies.pdf#page=5>).
- For the comparison of TDD, BBD and PBD, use [14-SOC Design Methodologies.pdf, p.20](<../System on chip/14-SOC Design Methodologies.pdf#page=20>).
- For requirements/specifications and iteration, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.44](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=44>) and p.45.
- For top-down system modeling and early verification, use [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) to p.6.
