# Sources - CLO 2 Topic 1

## Topic

SoC Components: CoreLogic - Processors, choice of processors, Basic concepts of processor architecture/microarchitecture.

## CLO Mapping

This maps to **CLO 2: Describe SoC and its Components; Bus Architecture and Interconnection of SoC**.

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **SoC Components: CoreLogic - Processors, choice of processors, Basic concepts of processor architecture/microarchitecture** under the SoC Components section, and maps SoC components to CLO 2.
- Topic image: [Screenshot 2026-05-12 230027.png](<../images/Screenshot 2026-05-12 230027.png>) contains **SoC Components: CoreLogic - Processors, choice of processors, Basic concepts of processor**.
- Topic image: [Screenshot 2026-05-12 230034.png](<../images/Screenshot 2026-05-12 230034.png>) contains **architecture/microarchitecture**.
- PPT: [SOC components -processor.pdf, p.2](<../System on chip/SOC components -processor.pdf#page=2>) introduces processor selection for SoC and notes increasing processor/system complexity.
- PPT: [SOC components -processor.pdf, p.3](<../System on chip/SOC components -processor.pdf#page=3>) explains that the processor may occupy only a few percent of die area, SoCs use different processor types, and noncritical processors may be acquired as IP.
- PPT: [SOC components -processor.pdf, p.4](<../System on chip/SOC components -processor.pdf#page=4>) explains that processor selection is often restricted by system software and that compute-limited applications require configured/parameterized processors.
- PPT: [SOC components -processor.pdf, p.6](<../System on chip/SOC components -processor.pdf#page=6>) defines soft processors and gives reasons for using them in FPGA-based SoC designs.
- PPT: [SOC components -processor.pdf, p.8](<../System on chip/SOC components -processor.pdf#page=8>) explains processor architecture as instruction set and microarchitecture as the implementation influenced by physical limitations and area-time-power tradeoffs.
- PPT: [SOC components -processor.pdf, p.9](<../System on chip/SOC components -processor.pdf#page=9>) explains register sets, floating-point registers, program status word, condition codes and load/store versus register-memory instruction set classes.
- PPT: [SOC components -processor.pdf, p.10](<../System on chip/SOC components -processor.pdf#page=10>) compares load/store/RISC style with register-memory style.
- PPT: [SOC components -processor.pdf, p.11](<../System on chip/SOC components -processor.pdf#page=11>) explains the area-time tradeoff between compact register-memory instruction formats and decode complexity.
- PPT: [SOC components -processor.pdf, p.14](<../System on chip/SOC components -processor.pdf#page=14>) explains branches, conditional branches and condition codes.
- PPT: [SOC components -processor.pdf, p.15](<../System on chip/SOC components -processor.pdf#page=15>) introduces embedded SoC interrupts and exceptions.
- PPT: [SOC components -processor.pdf, p.16](<../System on chip/SOC components -processor.pdf#page=16>) classifies interrupts/exceptions as terminate/resume, asynchronous/synchronous and between/within instructions.
- PPT: [SOC components -processor.pdf, p.17](<../System on chip/SOC components -processor.pdf#page=17>) introduces processor microarchitecture and instruction execution pipelines.
- PPT: [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>) explains memory system, execution unit/datapaths and instruction unit, and how cache/memory/execution units affect cycles.
- PPT: [SOC components -processor.pdf, p.19](<../System on chip/SOC components -processor.pdf#page=19>) explains pipeline execution possibilities and performance-limiting delays such as data conflicts.
- PPT: [SOC components -processor.pdf, p.20](<../System on chip/SOC components -processor.pdf#page=20>) explains resource contention, run-on delays and branch delays in pipelines.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.2](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=2>) defines SoC architecture as an ensemble of processors, memories and interconnects tailored to an application domain.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.4](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=4>) explains software on GPPs and the programmability/performance tradeoff.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.5](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=5>) explains the common strategy of implementing performance-critical application parts in hardware and the rest in software.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.7](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=7>) defines ASIP and explains FPGA as a compromise between software flexibility and custom-hardware performance.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.8](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=8>) says processors can be characterized by application or architecture.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.9](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=9>) explains instruction-level parallelism and other program parallelism levels.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.11](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=11>) explains simple sequential processors.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.12](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=12>) lists pipeline stages: IF, ID, AG, DF, EX and WB.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.13](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=13>) explains pipelining and overlapping instruction phases.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.15](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=15>) explains ILP and multiple operations per cycle.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.17](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=17>) introduces SIMD architectures, array processors and vector processors.
- PPT: [module 1 part 1 introduction to system approach.pdf, p.19](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=19>) explains multiprocessors and MIMD-style execution.
- PPT: [module 1 chip basics.pdf, p.3](<../System on chip/module 1 chip basics.pdf#page=3>) explains the five basic design tradeoffs, including time, area and power.
- PPT: [module 1 chip basics.pdf, p.7](<../System on chip/module 1 chip basics.pdf#page=7>) explains cycle time and unanticipated extra cycles such as cache misses.
- PPT: [module 1 chip basics.pdf, p.9](<../System on chip/module 1 chip basics.pdf#page=9>) explains optimum pipeline and the tradeoff between more segments and clock overhead.
- PPT: [module 1 chip basics.pdf, p.13](<../System on chip/module 1 chip basics.pdf#page=13>) explains power sources including dynamic/switching power and leakage power.

## Textbook Sources

- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.22](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=22>) describes basic SoC elements including heterogeneous processors, memory, reconfigurable logic and analog circuitry.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.23](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=23>) explains the higher-level processor definition as ISA, microarchitecture basics and hardware/software programmability versus performance.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.24](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=24>) explains ASIPs and FPGAs as implementation options between GPP software and custom ASIC hardware.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.25](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=25>) discusses DSPs and processor characterization by application or architecture.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.26](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=26>) explains pipelining, multiple execution units, multiple cores and ILP.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.27](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=27>) explains simple sequential processor stages.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.28](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=28>) explains pipelined processors and overlapping phases.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.29](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=29>) explains ILP, superscalar and VLIW processors.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.32](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=32>) introduces SIMD/vector/array processor concepts.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.94](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=94>) introduces processor selection for SoC and IP choices.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.95](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=95>) discusses reasons for soft processors and examples such as Nios II, MicroBlaze, OpenRISC and LEON.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.96](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=96>) shows processor core selection flow and notes configurable caches, bus architectures and custom instructions/coprocessors.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.99](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=99>) explains the difference between instruction set architecture and microarchitecture.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.100](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=100>) discusses the area-time tradeoff in instruction-set styles.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.102](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=102>) explains branches, condition codes and interrupt/exception handling.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.119](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=119>) explains CPI, executing multiple instructions, concurrent processors and ILP dependencies.

## Web / Standards Sources

- Web: [Arm CPU Architecture](https://www.arm.com/architecture/cpu) explains Arm architecture profiles: A-profile for highest-performance application processors, R-profile for real-time systems and M-profile for small low-power microcontroller devices. It also says implementations vary by microarchitecture and are optimized for different power/performance/area balances.
- Web: [Arm Silicon IP - CPU](https://www.arm.com/products/silicon-ip-cpu) lists Arm CPU processor IP ranges including Cortex-A, Cortex-R, Cortex-M and Neoverse. This supports the processor-choice discussion.
- Web: [RISC-V International Ratified Specifications](https://riscv.org/specifications/ratified/) states that the RISC-V open-standard ISA defines fundamental guidelines for designing and implementing RISC-V processors, and that ISA specifications are free and publicly available.
- Web: [AMD MicroBlaze](https://www.amd.com/en/products/adaptive-socs-and-fpgas/intellectual-property/microblazecore.html) describes MicroBlaze as a 32-bit RISC Harvard architecture soft processor core optimized for embedded applications.
- Web: [AMD MicroBlaze V Processor](https://www.amd.com/en/products/software/adaptive-socs-and-fpgas/microblaze-v.html) describes MicroBlaze V as a soft-core RISC-V processor IP for AMD adaptive SoCs and FPGAs.

## Figure References

- For the exact syllabus topic, use [Screenshot 2026-05-12 230027.png](<../images/Screenshot 2026-05-12 230027.png>) and [Screenshot 2026-05-12 230034.png](<../images/Screenshot 2026-05-12 230034.png>).
- For processor selection flow, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.96](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=96>).
- For basic pipeline stages, use [module 1 part 1 introduction to system approach.pdf, p.12](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=12>).
- For load/store versus register-memory instruction set explanation, use [SOC components -processor.pdf, p.9](<../System on chip/SOC components -processor.pdf#page=9>) to p.11.
- For microarchitecture/pipeline delays, use [SOC components -processor.pdf, p.17](<../System on chip/SOC components -processor.pdf#page=17>) to p.20.
