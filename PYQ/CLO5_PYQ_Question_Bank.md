# CLO 5 PYQ-Based Question Bank - Verification Strategies And Test Scheduling

## Clickable Index

- [Source Map](#source-map)
- [Exact PYQ Questions Found](#exact-pyq-questions-found)
- [Most Likely Direct Exam Questions](#most-likely-direct-exam-questions)
- [Test Integration Questions](#test-integration-questions)
- [Test Scheduling Questions](#test-scheduling-questions)
- [Best Combined 10-Mark Answer Structure](#best-combined-10-mark-answer-structure)

<a id="source-map"></a>

## Source Map

This PYQ file is based on the extracted PYQ line:

```text
Discuss the SoC Design Verification strategies and Test Scheduling
```

It also includes the repeated PYQ:

```text
Explain SOC test scheduling and test integration.
```

Source details are kept in [../sources/CLO5_PYQ_sources.md](<../sources/CLO5_PYQ_sources.md>).

Use this file as the question bank for CLO 5. The broad PYQ phrase can be split into three main areas:

```text
Verification strategies -> Verification flow and methodologies
Testing/test integration -> DFT, scan, BIST, JTAG, TAM, wrappers, ATE
Test scheduling -> ordering/parallelism under constraints
```

Main CLO file: [../CLO5.md](<../CLO5.md>)

<a id="exact-pyq-questions-found"></a>

## Exact PYQ Questions Found

| PYQ Question | Marks | Where To Prepare From |
|---|---:|---|
| Explain SOC test scheduling and test integration. | 10 | [CLO5 Topic 3](<../CLO5.md#topic-3>) |
| Discuss the SoC Design Verification strategies and Test Scheduling. | Broad/combined | [CLO5 Topic 1](<../CLO5.md#topic-1>), [Topic 2](<../CLO5.md#topic-2>), [Topic 3](<../CLO5.md#topic-3>) |

<a id="most-likely-direct-exam-questions"></a>

## Most Likely Direct Exam Questions

1. **Discuss SoC design verification strategies and test scheduling.**
   - Write verification vs testing first.
   - Then explain verification strategies: test plan, UVM/OVM/VVM, constrained-random testing, assertions, coverage, regression, block/subsystem/full-chip verification, hardware/software co-verification and gate-level checks.
   - Then explain test scheduling: test integration, DFT, scan, BIST, TAM, constraints and rectangle-packing idea.

2. **Explain SoC verification flow.**
   - Use [CLO5 Topic 2](<../CLO5.md#topic-2>).
   - Draw the flow: specification -> verification plan -> model -> environment -> block verification -> subsystem verification -> hardware/software co-verification -> full-chip verification -> coverage closure -> gate-level/timing/equivalence -> DFT readiness.

3. **Explain verification techniques OVM, UVM and VVM.**
   - Use [CLO5 Topic 1](<../CLO5.md#topic-1>).
   - Define OVM - Open Verification Methodology, UVM - Universal Verification Methodology and VVM - VHDL Verification Methodology.
   - Draw the UVM-style environment: sequence, sequencer, driver, monitor, scoreboard, coverage collector and DUT.

4. **Differentiate verification and testing in SoC.**
   - Verification checks design correctness before fabrication.
   - Testing checks manufactured silicon after fabrication.
   - Mention RTL simulation, coverage and assertions for verification; scan, BIST, ATPG, JTAG, TAM and ATE for testing.

5. **Explain why SoC verification is difficult.**
   - Include integration bugs, interface mismatch, clock-domain crossing, reset-domain crossing, software-hardware interaction, concurrency, power modes, cache/DMA issues, third-party IP reuse and corner-case explosion.

6. **Explain functional coverage, code coverage, assertion coverage and cross coverage.**
   - Functional coverage checks specification scenarios.
   - Code coverage checks RTL statements, branches, conditions, toggles and finite-state-machine states.
   - Assertion coverage checks whether properties were activated.
   - Cross coverage checks combinations of important conditions.

7. **Explain hardware/software co-verification in SoC verification flow.**
   - Include boot sequence, firmware register programming, device drivers, interrupt service routines, DMA setup, RTOS scheduling, memory map, exception handling, power-mode entry/exit and accelerator use.

8. **Explain full-chip SoC verification.**
   - Include top-level reset/boot, clock generation, power modes, memory map, peripheral access, interrupt routing, JTAG/debug, bus/NoC traffic, multi-master contention, security/privilege and real application scenarios.

9. **Explain gate-level, timing and equivalence verification.**
   - Include lint, CDC, RDC, formal equivalence checking, static timing analysis, gate-level simulation and X-propagation.

<a id="test-integration-questions"></a>

## Test Integration Questions

1. **Explain SoC test integration.**
   - Test integration means connecting all core-level and chip-level test structures into one SoC-level test architecture.
   - Include ATE, JTAG, test controller, TAM, core wrappers, scan chains, BIST and ATPG patterns.

2. **Draw and explain SoC test integration architecture.**
   - Draw:

```text
ATE/JTAG -> Test Controller -> TAM/Test Bus -> Core Wrappers -> IP Cores
                                                   |
                                                 BIST
```

3. **Explain ATE, JTAG, test controller, TAM and core wrapper.**
   - **ATE - Automatic Test Equipment** is outside the chip.
   - **JTAG - Joint Test Action Group** is a low-pin test/debug access path.
   - **TAM - Test Access Mechanism** transports test data inside the SoC.
   - **Core wrapper** isolates and connects embedded cores for test.
   - **Test controller** sequences scan, BIST, wrappers and test modes.

4. **Explain scan chains in SoC testing.**
   - Scan chains connect flip-flops into shift registers during test mode.
   - They improve controllability and observability of internal state.
   - They support ATPG structural testing.

5. **Explain BIST and compare MBIST and LBIST.**
   - **BIST - Built-In Self-Test** lets a block test itself.
   - **MBIST - Memory Built-In Self-Test** tests SRAM, ROM, register files and memory macros.
   - **LBIST - Logic Built-In Self-Test** tests random logic using pattern generation and signature compaction.

6. **Explain ATPG and test patterns.**
   - **ATPG - Automatic Test Pattern Generation** creates structural test vectors for stuck-at, transition and bridging faults.
   - Patterns are applied through scan chains, TAM and ATE paths.

<a id="test-scheduling-questions"></a>

## Test Scheduling Questions

1. **Explain SoC test scheduling.**
   - Test scheduling decides when each core test runs and which tests can run in parallel.
   - The objective is to reduce test application time and ATE cost without violating constraints.

2. **What are the objectives of SoC test scheduling?**
   - Minimize test application time.
   - Reduce ATE cost.
   - Reduce test data volume.
   - Avoid exceeding power/thermal limits.
   - Use TAM bandwidth efficiently.
   - Avoid test-resource conflicts.
   - Preserve fault coverage.

3. **Explain constraints in SoC test scheduling.**
   - Power constraint.
   - TAM - Test Access Mechanism bandwidth constraint.
   - Resource conflict constraint.
   - Precedence constraint.
   - Thermal constraint.
   - Clock/frequency constraint.
   - Test mode conflict.
   - Tester memory/data-volume constraint.

4. **Explain TAM bandwidth constraint with example.**
   - If available TAM width is 12 wires, CPU test needs 8 wires and DSP test needs 8 wires, both cannot run together because 16 > 12.

5. **Explain power-constrained test scheduling with example.**
   - If CPU test consumes 40 mW and DSP test consumes 50 mW while the test power limit is 80 mW, they cannot run together because 90 mW exceeds the limit.

6. **Explain rectangle-packing model of SoC test scheduling.**
   - Horizontal axis represents test time.
   - Vertical axis represents TAM - Test Access Mechanism width.
   - Each core test is a rectangle.
   - The scheduler packs rectangles into minimum total time while respecting power, TAM and resource constraints.

7. **Differentiate test integration and test scheduling.**
   - Test integration asks: how are embedded cores made accessible for test?
   - Test scheduling asks: when should each test run?
   - Integration creates infrastructure; scheduling uses it efficiently.

8. **Explain relationship between DFT, test integration and test scheduling.**
   - **DFT - Design for Testability** adds scan, BIST, wrappers, test controller and TAM.
   - Test integration connects these structures.
   - Test scheduling decides how to use them over time.

<a id="best-combined-10-mark-answer-structure"></a>

## Best Combined 10-Mark Answer Structure

If the exam asks the broad PYQ question **"Discuss SoC Design Verification strategies and Test Scheduling"**, write in this order:

1. Define verification and testing.
2. Explain why SoC verification is difficult.
3. Explain verification strategies: plan, coverage, assertions, UVM/OVM/VVM, regression, block/subsystem/full-chip checks.
4. Explain verification flow with a small diagram.
5. Explain testing and DFT structures: scan, BIST, JTAG, TAM, wrappers, ATE and ATPG.
6. Explain test integration.
7. Explain test scheduling objectives and constraints.
8. Draw rectangle-packing test scheduling figure.
9. End with the line:

```text
Verification proves the SoC design is functionally correct before fabrication,
while test integration and test scheduling make manufactured SoC testing
accessible, safe and time-efficient.
```
