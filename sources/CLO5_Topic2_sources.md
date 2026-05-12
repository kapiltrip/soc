# Sources - CLO 5 Topic 2

## Topic

SoC Verification Flow

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **SoC Verification Flow** under **SoC Verification and Testing**, which maps to CLO 5.
- Lecture: [SOC Design Flow.pdf, p.3](<../System on chip/SOC Design Flow.pdf#page=3>) explains bottom-up design: each block is verified based on its own requirements and system verification begins after block completion.
- Lecture: [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) explains top-down design: system-level models and verification environment are developed early.
- Lecture: [SOC Design Flow.pdf, p.5](<../System on chip/SOC Design Flow.pdf#page=5>) says system-level issues should be discovered up front and subsystems should be verified in the system verification environment.
- Lecture: [SOC Design Flow.pdf, p.6](<../System on chip/SOC Design Flow.pdf#page=6>) lists top-down principles: HDL/high-level models, reusable cores, early validation, testbenches, models, formal test plan, golden representation, DFT strategy.
- Lecture: [Functional Architecture Co Design 2.pdf, p.12](<../System on chip/Functional Architecture Co Design 2.pdf#page=12>) explains top-down stepwise refinement from requirements to functional model, architectural model and RTL.
- Lecture: [Functional Architecture Co Design 2.pdf, p.15](<../System on chip/Functional Architecture Co Design 2.pdf#page=15>) explains verified executable specification, verification environment and virtual testbench.
- Lecture: [Functional Architecture Co Design 2.pdf, p.18](<../System on chip/Functional Architecture Co Design 2.pdf#page=18>) discusses hardware/software implementation, system integration, emulators and rapid prototypes.
- Lecture: [14-SOC Design Methodologies.pdf, p.8](<../System on chip/14-SOC Design Methodologies.pdf#page=8>) says RTL functional verification with simpler timing views reduces slow timing-accurate gate-level simulations, while static timing analysis catches timing errors.
- Lecture: [14-SOC Design Methodologies.pdf, p.11](<../System on chip/14-SOC Design Methodologies.pdf#page=11>) mentions hardware/software co-verification using software simulation and/or hardware emulation.
- Lecture: [Design_Metrics.pdf, p.18](<../System on chip/Design_Metrics.pdf#page=18>) lists soft IP verification deliverables: functional simulation testbench, bus functional models, monitors, sample verification tests, cycle-based simulation or emulation models.
- Lecture: [Design_Metrics.pdf, p.19](<../System on chip/Design_Metrics.pdf#page=19>) lists hard IP verification/test deliverables: behavioral model, bus functional models, emulation model, testbench, verification tests, manufacturing tests.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.86](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=86>) explains validation, testing, DFT and scan chains.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.269](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=269>) says designs must be verified after optimization to ensure correctness, and system integration/testing issues must be planned.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.318](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=318>) identifies verification and testing as major design challenges.

## Web Sources

- [AMD Vitis Unified Software Platform](https://www.amd.com/en/products/software/adaptive-socs-and-fpgas/vitis.html): official AMD page describing embedded software development, exporting hardware from Vivado, using hardware platform information in software development, system-level verification and heterogeneous hardware/software simulation flows.
- [Arm Armv8-M Exception Model User Guide](https://documentation-service.arm.com/static/64c7832738511951cb7a246e): official Arm guide explaining exceptions, interrupts, NVIC behavior, ISR execution, priorities, vector tables, BusFault, UsageFault, SVC, PendSV and SysTick.
- [FreeRTOS documentation](https://docs.freertos.org/): official FreeRTOS documentation page describing FreeRTOS as an embedded RTOS for microcontrollers and small microprocessors.
- [FreeRTOS kernel scheduler documentation](https://docs.amazonaws.cn/en_us/freertos/latest/userguide/freertos-kernel-scheduler.html): official FreeRTOS documentation explaining that an RTOS application is structured as tasks and the scheduler decides when each task runs.
- [FreeRTOS Reference Manual V8.2.1](https://www.freertos.org/media/2025/FreeRTOS_Reference_Manual_V8.2.1.pdf): official FreeRTOS reference manual, including scheduler startup, tasks, semaphores, ISR interaction APIs and tickless idle behavior.
- [Zephyr power-state binding](https://docs.zephyrproject.org/latest/build/dts/api/bindings/power/zephyr%2Cpower-state.html): official Zephyr documentation listing power-state names and properties such as minimum residency and exit latency.
- [Arm AMBA Specifications](https://www.arm.com/architecture/system-architectures/amba/amba-specifications): official Arm page listing AMBA protocols such as CHI, AXI, AHB, APB, AXI-Stream and AMBA low-power interfaces used for SoC interconnect verification context.
- [Arm CoreSight basics](https://developer.arm.com/community/arm-community-blogs/b/architectures-and-processors-blog/posts/how-to-debug-coresight-basics-part-1): official Arm developer article explaining debug/trace, Debug Access Port, JTAG bridge, ROM tables and multi-processor debug context.
- [Accellera IEEE 1801-2024 UPF announcement](https://eda.org/news/press-releases/414-accellera-announces-ieee-standard-1801-2024-is-available-through-ieee-get-program): official Accellera announcement describing Unified Power Format as a standard for specifying and verifying low-power intent, including power domains, supply networks, power shutoff and multi-voltage designs.
- [Synopsys Formality Equivalence Checking](https://www.synopsys.com/implementation-and-signoff/signoff/formality-equivalence-checking.html): official Synopsys page for formal equivalence checking used to verify that transformed netlists preserve RTL functionality.
- [Synopsys ESP Formal Equivalence Checking](https://www.synopsys.com/implementation-and-signoff/signoff/esp.html): official Synopsys page describing formal equivalence checking between design representations such as behavioral Verilog, RTL, gate, switch, SPICE or db netlist views.
- [Siemens Questa RDC verification](https://www.siemens.com/en-gb/products/ic/questa-one/design-solutions/reset-domain-crossing/): official Siemens page explaining reset-domain crossing verification and noting that RDCs can expose data loss or control-signal corruption like CDCs.
- [Intel Clock Domain Crossing and Reset Domain Crossing Rules](https://www.intel.com/content/www/us/en/docs/programmable/683369/current/clock-domain-crossing-and-reset-domain.html): official Intel FPGA documentation describing CDC/RDC timing-closure rules and reset synchronizer constraints.
- [Accellera Standards](https://www.accellera.org/downloads/standards): official standards page for verification-related standards including SystemVerilog, SystemC, UVM, UPF and related EDA standards.

## Figure References

- For a course-slide basis for the flow diagram, look at [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) and [SOC Design Flow.pdf, p.6](<../System on chip/SOC Design Flow.pdf#page=6>). These slides justify the early system-level model, verification environment, formal test plan and golden representation.
- For the higher-abstraction-to-RTL refinement idea, look at [Functional Architecture Co Design 2.pdf, p.12](<../System on chip/Functional Architecture Co Design 2.pdf#page=12>) and [Functional Architecture Co Design 2.pdf, p.15](<../System on chip/Functional Architecture Co Design 2.pdf#page=15>).
