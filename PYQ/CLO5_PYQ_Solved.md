# CLO 5 PYQ Solved - Verification, Testing, Test Scheduling And Integration

## Clickable Index

- [Q1. SoC Test Scheduling And Test Integration](#q1-soc-test-scheduling-and-test-integration)
- [Q2. SoC Design Verification Strategies And Test Scheduling](#q2-soc-design-verification-strategies-and-test-scheduling)

## CLO Mapping

This file maps to **CLO 5: Discuss the SoC Design Verification strategies and Test Scheduling**.

Use with:

- [CLO5.md](<../CLO5.md>)
- [CLO5 PYQ Question Bank](<CLO5_PYQ_Question_Bank.md>)
- [PYQ Master Index](<PYQ_Master_Index.md>)

## Local PPT / Book References To Use

Use these while revising or writing this CLO5 PYQ answer:

- [SOC Design Flow.pdf, p.4](<../System on chip/SOC Design Flow.pdf#page=4>) supports early system-level models and early verification environment in top-down SoC design.
- [SOC Design Flow.pdf, p.6](<../System on chip/SOC Design Flow.pdf#page=6>) explicitly mentions formal test plan, golden representation and DFT strategy.
- [Design_Metrics.pdf, p.18](<../System on chip/Design_Metrics.pdf#page=18>) lists soft-IP deliverables such as functional simulation testbench, bus functional models, monitors and verification tests.
- [Design_Metrics.pdf, p.19](<../System on chip/Design_Metrics.pdf#page=19>) lists hard-IP deliverables such as behavioral model, testbench, verification tests and manufacturing tests.
- [14-SOC Design Methodologies.pdf, p.8](<../System on chip/14-SOC Design Methodologies.pdf#page=8>) supports RTL functional verification and static timing analysis context.
- [14-SOC Design Methodologies.pdf, p.11](<../System on chip/14-SOC Design Methodologies.pdf#page=11>) supports hardware/software co-verification using software simulation or hardware emulation.
- [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.86](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=86>) supports manufacturing testing, validation, DFT and scan chains.
- Detailed local/web source maps: [CLO5_Topic2_sources.md](<../sources/CLO5_Topic2_sources.md>) and [CLO5_Topic3_sources.md](<../sources/CLO5_Topic3_sources.md>).

<a id="q1-soc-test-scheduling-and-test-integration"></a>

## Q1. Explain SoC Test Scheduling And Test Integration

**PYQ source:** EST 2024 Q6, EST 2025 Q6.

### What The Question Is Asking

This question is not asking only for the definition of testing. It asks two connected things:

1. **Test integration**: how the test infrastructure is inserted into the SoC so embedded cores can be controlled and observed.
2. **Test scheduling**: how the tests are ordered or overlapped so total test time is reduced without violating power, bandwidth or resource constraints.

### Core Definition

**SoC test integration** is the process of connecting all embedded cores, memories, interconnects and logic blocks to a chip-level test architecture. It includes scan chains, BIST, wrappers, TAM, JTAG, test controller and ATE access.

**SoC test scheduling** is the process of deciding when each core or block test should run, considering test time, test power, TAM bandwidth, ATE channels, dependencies and resource conflicts.

Exam line:

```text
Test integration creates the test infrastructure; test scheduling uses that infrastructure efficiently.
```

### Why SoC Testing Is Difficult

A System on Chip contains many embedded blocks: processor cores, SRAM macros, ROM, DMA controllers, interconnect, accelerators, peripherals, clock/reset logic and power domains. These blocks are buried inside the chip. The external tester cannot directly access all internal nodes through chip pins. Therefore, the SoC must include **DFT - Design For Testability** structures.

The difficulty is:

- internal cores are not directly visible from package pins,
- sequential logic has many internal flip-flop states,
- embedded memories are large and numerous,
- test data volume can be very high,
- test power can exceed functional power,
- external ATE time is expensive,
- different cores may need different clocks, modes and test resources.

### Test Integration Architecture To Draw

Draw this in the exam:

```text
                 External ATE
                     |
                  JTAG/TAP
                     |
              Test Controller
                     |
        +------------+-------------+
        |            |             |
       TAM          TAM           TAM
        |            |             |
   Core Wrapper  Core Wrapper   MBIST Controller
        |            |             |
      CPU/DSP     Peripheral      SRAM Macros
        |
    Scan Chains
```

Why this figure is useful: it shows that external tester access is converted into internal test access through JTAG, a test controller, TAM, wrappers, scan and BIST.

### Main Test Integration Elements

**ATE - Automatic Test Equipment** is the external production tester. It applies test patterns through chip pins and compares responses. It is expensive, so test time must be minimized.

**JTAG - Joint Test Action Group / boundary scan** provides standardized test and debug access through a small number of pins. It is used for board-level test, chip access, instruction loading and scan/test control.

**Test controller** is on-chip hardware that configures test modes, starts BIST, controls wrappers and coordinates test execution.

**TAM - Test Access Mechanism** is the internal path that transports test data between external tester/test controller and embedded cores. TAM may be a bus-like set of test wires.

**Core wrapper** surrounds an embedded core and isolates it from the rest of the SoC during test. It provides controllability and observability at the core boundary.

**Scan chain** connects flip-flops into shift registers in test mode. It allows internal states to be loaded and observed.

**BIST - Built-In Self-Test** allows a block to test itself using internal pattern generation and response checking.

**MBIST - Memory Built-In Self-Test** tests SRAM, ROM and register-file memories using memory test algorithms such as March tests.

**LBIST - Logic Built-In Self-Test** tests random logic using pseudo-random patterns and signature compaction.

**ATPG - Automatic Test Pattern Generation** generates structural test patterns for faults such as stuck-at, transition, bridging and delay faults.

### What Actually Happens During Testing

For scan-based logic testing:

```text
1. Put chip or core into test mode.
2. Shift ATPG-generated test pattern into scan chains.
3. Apply one or more capture clocks.
4. Capture circuit response in scan flip-flops.
5. Shift response out.
6. Compare response with expected golden response on ATE.
```

For memory BIST:

```text
1. Test controller starts MBIST.
2. MBIST controller writes and reads memory patterns.
3. Comparator checks read data.
4. Pass/fail or repair information is reported.
```

### Test Scheduling

If an SoC has many cores, testing them one by one is simple but slow. Testing all cores together may be impossible because of power, TAM width and resource conflicts. Test scheduling finds a safe middle path.

Inputs to test scheduling:

- test time of each core,
- TAM bandwidth needed by each test,
- test power of each test,
- fault coverage target,
- ATE channel availability,
- BIST/scan/resource requirements,
- precedence constraints,
- clock and power-domain restrictions.

### Scheduling Constraints

**Power constraint:** testing causes high switching activity. If too many cores are tested together, voltage drop, overheating or damage may occur.

**TAM bandwidth constraint:** if total available TAM width is 16 wires, tests needing 10 and 8 wires cannot run together because 18 wires are required.

**Resource conflict:** two tests cannot run together if both require the same PLL, test bus, test controller, memory, wrapper, clock generator or ATE channel.

**Precedence constraint:** some tests must occur before others. Example: scan-chain integrity check before ATPG patterns, MBIST before software memory tests, PLL test before high-speed logic test.

**Thermal constraint:** nearby cores tested together may create local hotspots even if total power is acceptable.

**Clock/mode constraint:** two tests may require incompatible test clocks or mutually exclusive test modes.

### Example Schedule

Assume:

| Core | Test time | TAM wires | Power |
|---|---:|---:|---:|
| CPU scan | 10 units | 8 | 40 mW |
| SRAM MBIST | 6 units | 4 | 30 mW |
| DSP scan | 8 units | 8 | 50 mW |
| UART scan | 4 units | 2 | 10 mW |

Limits:

```text
Total TAM = 12 wires
Power limit = 80 mW
```

Possible schedule:

```text
Time 0-6:   CPU + SRAM MBIST
            TAM = 8 + 4 = 12, Power = 40 + 30 = 70 mW

Time 6-10:  CPU + UART
            TAM = 8 + 2 = 10, Power = 40 + 10 = 50 mW

Time 10-18: DSP
            TAM = 8, Power = 50 mW
```

CPU and DSP cannot run together:

```text
TAM = 8 + 8 = 16 > 12
Power = 40 + 50 = 90 mW > 80 mW
```

### Final Exam Answer

SoC test integration is required because the embedded cores inside an SoC cannot be tested directly from chip pins. The test architecture therefore includes DFT structures such as scan chains, BIST, MBIST, LBIST, core wrappers, TAM, JTAG, test controller and ATE interface. Scan chains improve controllability and observability of sequential logic. BIST allows memories and logic to test themselves with internal pattern generation and response checking. Core wrappers isolate embedded cores and connect them to chip-level test access. TAM transports test data between the tester and cores, while JTAG and the test controller provide chip-level access and control.

SoC test scheduling decides when these tests should run. The aim is to minimize test application time while satisfying power, TAM bandwidth, thermal, clock, resource, data-volume and precedence constraints. Serial scheduling is simple but slow. Parallel scheduling reduces test time but must not exceed safe power or TAM limits. Therefore, practical SoC test scheduling is constraint-driven. The final result is an optimized test schedule that preserves required fault coverage while reducing ATE time and production cost.

### Technical Words To Use

- **DFT - Design For Testability** (write this because test integration depends on extra test hardware.)
- **ATE - Automatic Test Equipment** (write this because production testing is done externally through tester pins.)
- **JTAG - Joint Test Action Group** (write this because it gives standardized access to chip test/debug logic.)
- **TAM - Test Access Mechanism** (write this because scheduling depends on test-data bandwidth.)
- **Core wrapper** (write this because embedded cores need boundary control and observation.)
- **Scan chain** (write this because internal flip-flops must be controllable/observable.)
- **BIST/MBIST/LBIST** (write this because self-test reduces external test data.)
- **ATPG - Automatic Test Pattern Generation** (write this because structural fault tests are generated automatically.)
- **Power-constrained scheduling** (write this because test power can exceed functional power.)
- **Fault coverage** (write this because testing must detect manufacturing defects.)

<a id="q2-soc-design-verification-strategies-and-test-scheduling"></a>

## Q2. Discuss SoC Design Verification Strategies And Test Scheduling

**PYQ source:** user-provided PYQ extract.

### What The Question Is Asking

This is a combined question. It expects you to distinguish:

- **Verification:** checking design correctness before fabrication.
- **Testing:** checking manufactured silicon for defects after fabrication.
- **Test scheduling:** optimizing production test execution.

### Verification Strategies

**1. Verification plan**

The verification team converts the specification into features, test scenarios, coverage goals and pass/fail criteria. A good verification plan says what must be checked, how it will be checked and when verification is complete.

**2. Simulation-based verification**

RTL simulation runs the design with testbenches. Directed tests check known scenarios. Constrained-random tests generate many legal and corner-case transactions. Simulation is flexible but may be slow for full SoC verification.

**3. UVM-based verification**

**UVM - Universal Verification Methodology** uses reusable testbench components such as agents, drivers, sequencers, monitors, scoreboards and coverage collectors. It is transaction-based, meaning test scenarios are written as reads, writes, packets or bursts instead of manually toggling every signal.

**4. Assertion-based verification**

Assertions specify properties that must always hold, such as protocol rules, handshake timing, FIFO overflow protection or reset behavior. They catch bugs close to the source.

**5. Functional coverage**

Functional coverage checks whether required design features and scenarios were exercised. It answers:

```text
Did we test what the specification requires?
```

**6. Code coverage**

Code coverage checks whether RTL statements, branches, conditions, FSM states and toggles executed. It answers:

```text
Did our tests execute the implementation code?
```

**7. Formal verification**

Formal methods mathematically prove properties or equivalence. They are useful for protocol checking, control logic, deadlock freedom and equivalence checking.

**8. Hardware/software co-verification**

SoC behavior depends on both RTL and embedded software. Co-verification checks boot, firmware register programming, drivers, interrupts, DMA setup, memory map access and low-power control.

**9. Full-chip verification**

Full-chip verification checks interactions after integration: reset, clocks, power modes, NoC traffic, processor access to peripherals, interrupts, debug access and real application scenarios.

**10. Regression and coverage closure**

Regression runs many tests repeatedly after design changes. Coverage closure identifies untested features, unreachable code and missing assertions until the verification plan is satisfied.

### Verification Flow To Draw

```text
Specification
     |
Verification plan and coverage plan
     |
Reference model / executable model
     |
IP/block verification
     |
Subsystem verification
     |
Hardware/software co-verification
     |
Full-chip verification
     |
Coverage closure and regression
     |
Gate-level, timing and equivalence checks
     |
DFT readiness and sign-off
```

### Link To Test Scheduling

Verification proves that the design intends to work. Testing checks that fabricated chips are not defective. After DFT structures are inserted, test scheduling decides how to run production tests efficiently.

For example:

```text
Verification question:
Does the memory controller obey the DDR protocol?

Testing question:
Did this manufactured memory-controller logic contain a stuck-at or delay fault?

Scheduling question:
Can memory BIST run in parallel with CPU scan without exceeding power/TAM limits?
```

### Final Exam Answer

SoC design verification strategies include specification-driven verification planning, simulation, constrained-random testing, UVM testbenches, assertions, functional coverage, code coverage, formal verification, hardware/software co-verification, full-chip verification, regression testing and sign-off checks. These strategies are needed because an SoC contains many interacting processors, memories, buses, accelerators, peripherals, clock domains and power domains. A block may be correct alone but fail after integration.

After verification, manufacturing test is required to detect physical defects in silicon. DFT structures such as scan chains, BIST, MBIST, LBIST, JTAG, wrappers and TAM make embedded cores testable. Test scheduling then determines the safe and efficient order of tests. The objective is to reduce ATE time and cost while satisfying constraints such as power, TAM bandwidth, resource conflicts, thermal limits, test data volume and precedence. Therefore, SoC quality requires both strong design verification before fabrication and optimized test scheduling after fabrication.
