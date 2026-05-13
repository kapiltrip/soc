# Sources - CLO 5 Topic 3

## Topic

SoC Test Scheduling and Test Integration

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **SoC Test Scheduling and Test Integration** under **SoC Verification and Testing**, which maps to CLO 5.
- PYQ: [PVL333_EST-Even-23.pdf, p.1](<../PYQ/PVL333_EST-Even-23.pdf#page=1>) asks **Explain SOC test scheduling and test integration** under CO5.
- PYQ: [PVL333_EST_E_MAY2025.pdf, p.1](<../PYQ/PVL333_EST_E_MAY2025.pdf#page=1>) again asks **Explain SOC test scheduling and test integration** under CO5.
- Lecture: [SOC Design Flow.pdf, p.6](<../System on chip/SOC Design Flow.pdf#page=6>) includes **Develop a design for test (DFT) strategy** as a top-down design principle.
- Lecture: [Design_Metrics.pdf, p.18](<../System on chip/Design_Metrics.pdf#page=18>) lists soft IP deliverables including functional simulation testbench, bus functional models, monitors, verification tests and test methodology notes.
- Lecture: [Design_Metrics.pdf, p.19](<../System on chip/Design_Metrics.pdf#page=19>) lists hard IP deliverables including behavioral models, bus functional models, testbenches, verification tests and manufacturing tests.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.86](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=86>) explains manufacturing testing, validation, DFT and scan chains.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.193](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=193>) mentions optional on-chip test access in AMBA that reuses bus infrastructure for testing connected modules.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.269](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=269>) states that system integration and testing issues must be addressed after design iterations.

Review-addendum use:

- The CLO5 full-form review addendum uses Flynn/Luk p.86 for manufacturing testing, validation, DFT and scan-chain context.
- It uses `SOC Design Flow.pdf` p.6 for why DFT strategy is part of the design flow rather than an afterthought.
- It uses the wrapper/TAM research sources below for the test scheduling, TAM width and rectangle-packing explanation.

## Web / Research Sources

- [Wrapper/TAM Co-Optimization and constrained Test Scheduling for SOCs Using Rectangle Bin Packing](https://arxiv.org/abs/1008.4448): describes an integrated SoC test automation framework using wrapper/TAM co-optimization and rectangle-packing test scheduling with power constraints.
- [Efficient Wrapper/TAM Co-Optimization for SOC Using Rectangle Packing](https://arxiv.org/abs/1008.3320): states that SoC testing time largely depends on test wrappers and TAM design, so wrapper/TAM co-optimization is needed.
- [An Efficient Approach to SoC Wrapper Design, TAM Configuration and Test Scheduling - Lund University](https://portal.research.lu.se/en/publications/an-efficient-approach-to-soc-wrapper-design-tam-configuration-and/): identifies test application time and core accessibility as major SoC testing issues; discusses wrapper design, TAM architecture, test schedule, power dissipation, test conflicts and precedence constraints.
- [Test access mechanism optimization, test scheduling, and tester data volume reduction for system-on-chip - TU Eindhoven](https://research.tue.nl/en/publications/test-access-mechanism-optimization-test-scheduling-and-tester-dat/): describes integrated SoC test automation with flexible-width TAM buses, test wrappers, rectangle-packing scheduling, precedence constraints and power constraints.
- [Test-access mechanism optimization for core-based three-dimensional SOCs - Microelectronics Journal / ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0026269210001175): explains that embedded cores are not easily accessible through chip I/O pins, defines TAM as on-chip test data transport from pattern source to core and response sink, and discusses test-time minimization under TAM-bitwidth and thermal constraints.
- [A Reconfigurable Power Conscious Core Wrapper and its Application to System-on-Chip Test Scheduling - Springer](https://link.springer.com/article/10.1007/s10836-008-5074-2): discusses power-constrained test scheduling and explains the relationship between core tests, test time and TAM wires.

## Figure References

- For the **test architecture diagram**, use the local DFT/scan-chain context from the textbook p.86 and the SoC design-flow DFT strategy from `SOC Design Flow.pdf`, p.6.
- For the **rectangle-packing test schedule diagram**, use the web/research sources on wrapper/TAM co-optimization and rectangle packing. This figure is useful because it visually shows how test time, TAM width and power constraints affect scheduling.
