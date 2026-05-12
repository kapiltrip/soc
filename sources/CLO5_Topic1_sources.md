# Sources - CLO 5 Topic 1

## Topic

Verification Techniques - OVM, UVM and VVM

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>)
- Lecture: [SOC Design Flow.pdf, p.3](<../System on chip/SOC Design Flow.pdf#page=3>) says in bottom-up design, each block is verified first and system verification starts after all blocks are complete.
- Lecture: [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) says top-down design develops system-level models and a verification environment early.
- Lecture: [SOC Design Flow.pdf, p.6](<../System on chip/SOC Design Flow.pdf#page=6>) says a system verification environment includes testbenches, models and a formal test plan, and also stresses DFT strategy.
- Lecture: [Design_Metrics.pdf, p.4](<../System on chip/Design_Metrics.pdf#page=4>) lists SoC integration complexity, interface/synchronization issues, design verification and test as major SoC issues.
- Lecture: [Design_Metrics.pdf, p.18](<../System on chip/Design_Metrics.pdf#page=18>) lists soft IP deliverables such as functional simulation testbench, bus functional models, monitors and verification tests.
- Lecture: [Design_Metrics.pdf, p.19](<../System on chip/Design_Metrics.pdf#page=19>) lists hard IP deliverables such as behavioral model, bus functional model, testbench, verification tests and manufacturing tests.
- Lecture: [Functional Architecture Co Design 2.pdf, p.15](<../System on chip/Functional Architecture Co Design 2.pdf#page=15>) says functional modeling produces a verified executable specification and a virtual testbench.
- Lecture: [14-SOC Design Methodologies.pdf, p.8](<../System on chip/14-SOC Design Methodologies.pdf#page=8>) says RTL functional verification can reduce slow timing-accurate gate-level simulations.
- Lecture: [14-SOC Design Methodologies.pdf, p.11](<../System on chip/14-SOC Design Methodologies.pdf#page=11>) mentions hardware/software co-verification using software simulation or hardware emulation.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.86](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=86>) explains manufacturing testing, validation, DFT and scan chains.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.269](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=269>) says after optimization, the design must be verified so correctness is not affected, and system integration/testing must be planned.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.318](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=318>) identifies verification and testing as major design challenges.
- PYQ: [PVL333_EST-Even-23.pdf, p.1](<../PYQ/PVL333_EST-Even-23.pdf#page=1>) maps test scheduling and test integration to CO5.
- PYQ: [PVL333_EST_E_MAY2025.pdf, p.1](<../PYQ/PVL333_EST_E_MAY2025.pdf#page=1>) again asks SoC test scheduling and test integration under CO5.

## Web Sources

- [Accellera UVM downloads](https://www.accellera.org/downloads/standards/uvm): UVM improves interoperability and reuse of verification components.
- [Accellera UVM Working Group](https://www.accellera.org/activities/working-groups/uvm): UVM defines modular, scalable and reusable generic verification environments.
- [Cadence OVM](https://www.cadence.com/ja_JP/home/alliances/standards-and-languages/open-verification-methodology.html): OVM is an open-source SystemVerilog class library and methodology for reusable VIP and tests.
- [UVVM documentation](https://uvvm.github.io/uvvm_intro.html): UVVM is an open-source VHDL verification methodology/library for structured VHDL testbenches.
- [UVVM Getting Started](https://uvvm.github.io/uvvm_getting_started.html): UVVM has a lighter level using utility library and BFMs, and a complete level with VVC framework, VVCs and command distribution.
- [UVVM VVC Framework](https://uvvm.github.io/vvc_framework.html): VVCs encapsulate interface verification support inside reusable VHDL entities and can combine with BFMs.
- [UVVM Features](https://www.uvvm.org/features): UVVM provides reusable BFMs and VVCs for interfaces such as AXI, AXI-stream, AXI-lite, SPI, UART, SBI, Ethernet, GPIO and Avalon.
- [OSVVM](https://osvvm.org/about-os-vvm): OSVVM provides VHDL verification features such as TLM, constrained random generation, functional coverage, scoreboards and logs.
- [OSVVM GitHub](https://github.com/OSVVM/OSVVM): OSVVM utility library includes packages such as RandomPkg, CoveragePkg, ScoreboardGenericPkg, MemoryPkg, AlertLogPkg, TranscriptPkg and TbUtilPkg.
