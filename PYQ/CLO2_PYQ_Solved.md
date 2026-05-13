# CLO 2 PYQ Solved - SoC Components, Interconnect, Bus And NoC

## Clickable Index

- [Q1. Bus-Based Intra-Chip Communication](#q1-bus-based-intra-chip-communication)
- [Q2. On-Chip Interconnect: Bus Vs NoC](#q2-on-chip-interconnect-bus-vs-noc)
- [Q3. NoC Architecture](#q3-noc-architecture)
- [Q4. Front-End Chip Design, IP Cores And NoC](#q4-front-end-chip-design-ip-cores-and-noc)

## CLO Mapping

This file maps to **CLO 2: SoC Components - Processors, Memory Systems And On-Chip Interconnect**.

Use with:

- [CLO2.md](<../CLO2.md>)
- [PYQ Master Index](<PYQ_Master_Index.md>)

## Local PPT / Book References To Use

Use these while revising or writing this CLO2 PYQ answer:

- [module 1 part 1 introduction to system approach.pdf, p.2](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=2>) defines SoC architecture as processors, memories and interconnects tailored to an application domain.
- [module 1 part 1 introduction to system approach.pdf, p.31](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=31>) supports system-level interconnection and bus hierarchy.
- [module 1 part 1 introduction to system approach.pdf, p.32](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=32>) supports bus/memory/interconnect organization.
- [SOC components -processor.pdf, p.4](<../System on chip/SOC components -processor.pdf#page=4>) supports treating memory and interconnect as performance delay elements.
- [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>) supports the link between cache/memory/interconnect speed and instruction/data fetch cycles.
- [Functional Architecture Co Design 2.pdf, p.16](<../System on chip/Functional Architecture Co Design 2.pdf#page=16>) lists architecture modeling components such as processors, buses, memories, peripherals and RTOS.
- [14-SOC Design Methodologies.pdf, p.18](<../System on chip/14-SOC Design Methodologies.pdf#page=18>) supports bus planning and verification as platform-based design concerns.
- Detailed source maps: [CLO2_Topic1_sources.md](<../sources/CLO2_Topic1_sources.md>), [CLO2_Topic5_sources.md](<../sources/CLO2_Topic5_sources.md>) and [CLO2_review_sources.md](<../sources/CLO2_review_sources.md>).

<a id="q1-bus-based-intra-chip-communication"></a>

## Q1. Explain Bus-Based Intra-Chip Communication In SoC

**PYQ source:** MST 2024 Q4.

### Definition

**Bus-based intra-chip communication** is an on-chip communication method where multiple SoC components communicate over a shared set of wires or a structured bus protocol. It connects masters such as processors and DMA controllers to slaves such as memories and peripherals.

### Why A Bus Is Needed

An SoC contains many blocks:

- CPU,
- DMA controller,
- memory,
- peripherals,
- interrupt controller,
- accelerators,
- debug blocks.

These blocks must exchange addresses, data and control information. A bus provides a common communication path.

### Basic Bus Diagram

```text
        CPU master
            |
        DMA master
            |
   +------------------+
   | Shared bus       |
   | address/data/ctl |
   +------------------+
      |       |      |
    SRAM    UART   Timer
```

### Bus Signals

A typical bus contains:

- **address lines**: select memory/register location,
- **data lines**: carry read/write data,
- **control lines**: read/write, valid, ready, burst, byte enable,
- **clock/reset**: synchronize bus operation,
- **arbitration signals**: decide which master controls the bus.

### Bus Masters And Slaves

**Master:** initiates a transaction. Example: CPU or DMA.

**Slave:** responds to a transaction. Example: memory, UART, timer or GPIO.

Example:

```text
CPU writes UART register:
master = CPU
slave = UART
operation = write
address = UART register address
data = byte to transmit
```

### Arbitration

If multiple masters request the bus at the same time, an arbiter chooses one.

Common arbitration methods:

- fixed priority,
- round robin,
- weighted round robin,
- QoS-aware arbitration.

### Bus Protocol Examples

**AMBA - Advanced Microcontroller Bus Architecture** is common in SoC design.

Examples:

- **AXI - Advanced eXtensible Interface**: high-performance, pipelined, burst-capable.
- **AHB - Advanced High-performance Bus**: medium/high-performance bus.
- **APB - Advanced Peripheral Bus**: simple low-power peripheral bus.

### Advantages

- simple architecture,
- easy to design for small/medium SoCs,
- low area overhead,
- standard protocols available,
- good for low-bandwidth peripherals.

### Limitations

- shared bandwidth becomes a bottleneck,
- only limited parallel transfers,
- arbitration delay increases with masters,
- wiring and loading increase with SoC size,
- not highly scalable for many-core SoCs.

### Final Exam Answer

Bus-based intra-chip communication connects SoC components through a shared communication structure carrying address, data and control signals. Masters such as CPUs and DMA controllers initiate transactions, while slaves such as memories and peripherals respond. Arbitration is required when multiple masters request the bus. Standard bus protocols such as AMBA AXI, AHB and APB are widely used. Bus-based communication is simple, low-cost and suitable for small or medium SoCs, but it suffers from bandwidth bottlenecks, arbitration delay and poor scalability as the number of cores increases. For larger SoCs, hierarchical buses, crossbars or NoC architectures are used.

<a id="q2-on-chip-interconnect-bus-vs-noc"></a>

## Q2. What Is The Role Of On-Chip Interconnects? Explain Bus Vs NoC

**PYQ source:** MST 2026 Q2.

### Role Of On-Chip Interconnect

The **on-chip interconnect** is the communication backbone of an SoC. It connects processors, memories, DMA controllers, accelerators and peripherals.

It provides:

- address decoding,
- data transfer,
- arbitration,
- ordering,
- QoS support,
- protocol conversion,
- clock-domain crossing support,
- security/privilege routing,
- bandwidth sharing.

Without interconnect, SoC blocks would be isolated and could not work as a system.

### Bus

A bus is a shared communication path. Multiple masters and slaves use the same address/data/control structure.

Strengths:

- simple,
- low area,
- easy for small SoCs,
- good for peripherals.

Weaknesses:

- limited scalability,
- shared bandwidth,
- arbitration bottleneck,
- high loading with many blocks.

### NoC - Network-on-Chip

A **NoC - Network-on-Chip** is a packet-based or network-style interconnect inside the chip. It uses routers, links and network interfaces to move data between blocks.

Strengths:

- scalable for many cores,
- supports parallel communication,
- better bandwidth distribution,
- structured layout,
- QoS and traffic management.

Weaknesses:

- more complex,
- higher area and power,
- router latency,
- verification complexity.

### Bus Vs NoC Table

| Point | Bus | NoC |
|---|---|---|
| Communication | Shared wires | Packets through routers/links |
| Scalability | Low/medium | High |
| Parallelism | Limited | High |
| Area | Lower | Higher |
| Control | Simpler | More complex |
| Best for | Small SoCs/peripherals | Many-core/high-bandwidth SoCs |
| Bottleneck | Shared bus arbitration | Router/link congestion |

### Diagram

```text
Bus:
CPU --+
DMA --+--- Shared Bus --- Memory
ACC --+                  Peripherals

NoC:
CPU -- NI -- R -- R -- NI -- Memory
             |    |
ACC -- NI -- R -- R -- NI -- Peripheral
```

**NI - Network Interface** converts core transactions into network packets and back.

### Final Exam Answer

On-chip interconnect provides the communication infrastructure that connects all SoC blocks. It transfers address, data and control information between masters and slaves and handles arbitration, routing, QoS and protocol conversion. A bus is simple and area-efficient but has limited scalability because all blocks share the same bandwidth. A NoC uses routers, links and network interfaces to support packet-based communication with more parallelism and scalability. Therefore, buses are suitable for smaller SoCs and low-bandwidth peripherals, while NoCs are preferred in large multicore or high-bandwidth SoCs.

<a id="q3-noc-architecture"></a>

## Q3. Explain NoC Architecture In Detail

**PYQ source:** MST 2026 Q3.

### Definition

**NoC - Network-on-Chip** is an on-chip communication architecture that uses networking concepts to connect SoC blocks. Instead of one shared bus, data is divided into packets and transferred through routers and links.

### NoC Components

#### 1. Network Interface

The **NI - Network Interface** connects a core to the NoC. It converts bus/protocol transactions into packets and converts received packets back into core transactions.

#### 2. Router

A router receives packets from input ports and forwards them to output ports based on routing rules.

Router contains:

- input buffers,
- route computation logic,
- arbiter,
- crossbar switch,
- output ports,
- flow-control logic.

#### 3. Links

Links are wires between routers. They carry packet data, flow-control signals and control information.

#### 4. Packets And Flits

A packet is a complete communication unit. A **flit - flow control digit** is a smaller piece of a packet used for flow control.

Packet fields:

- source,
- destination,
- address,
- command,
- data,
- response,
- QoS information.

### NoC Topologies

| Topology | Meaning | Use |
|---|---|---|
| Mesh | routers arranged in grid | common for many-core systems |
| Ring | routers connected in a loop | simple moderate-scale systems |
| Tree | hierarchical routing | clustered systems |
| Torus | mesh with wraparound links | higher connectivity |
| Star | central router/switch | small systems |

### Routing

Routing decides the path from source to destination.

Examples:

- deterministic routing,
- adaptive routing,
- XY routing in mesh.

**XY routing** first moves in X direction, then Y direction. It is simple and helps avoid deadlock in mesh networks.

### Switching

Switching decides how packet data moves through routers.

Common types:

- store-and-forward,
- virtual cut-through,
- wormhole switching.

**Wormhole switching** divides packets into flits. The header flit reserves the path and following flits move behind it. It reduces buffer requirement but can block links if not managed well.

### Flow Control

Flow control prevents buffer overflow.

Mechanisms:

- ready/valid handshake,
- credit-based flow control,
- backpressure,
- virtual channels.

### Design Issues

- latency,
- bandwidth,
- congestion,
- power,
- area,
- deadlock,
- livelock,
- QoS,
- cache coherency,
- verification complexity.

### NoC Diagram

```text
 Core A          Core B
   |               |
  NI              NI
   |               |
  R ---- R ---- R
  |      |      |
  R ---- R ---- R
  |      |      |
  NI     NI     NI
 Memory ACC   Peripheral
```

### Final Exam Answer

NoC architecture is a scalable on-chip communication architecture made of network interfaces, routers and links. Network interfaces convert core transactions into packets. Routers forward packets according to routing algorithms. Links connect routers and carry packet/flit data. NoCs may use mesh, ring, tree, torus or star topology. Routing can be deterministic or adaptive, and switching may be store-and-forward, virtual cut-through or wormhole. Flow control using credits, backpressure and virtual channels prevents buffer overflow and avoids deadlock. NoCs are suitable for large SoCs because they provide parallel communication and better scalability than a shared bus, though they add area, power, latency and verification complexity.

<a id="q4-front-end-chip-design-ip-cores-and-noc"></a>

## Q4. Discuss Front-End Chip Design Components, IP Cores And NoC

**PYQ source:** MST 2025 Q5.

### Front-End Chip Design Components

Front-end chip design converts system requirements into verified RTL and design constraints.

Key components:

- specification,
- architecture design,
- RTL design,
- IP integration,
- memory map,
- interface definition,
- clock/reset planning,
- functional verification,
- synthesis constraints,
- timing/power intent.

### IP Cores

**IP - Intellectual Property** cores are reusable design blocks.

Types:

- **soft IP**: synthesizable RTL, flexible but timing not fixed,
- **firm IP**: partially optimized with constraints/floorplan,
- **hard IP**: fixed physical layout, predictable timing/power/area.

Examples:

- processor core,
- DDR controller,
- USB controller,
- PCIe controller,
- DSP block,
- SRAM macro,
- NoC router,
- crypto accelerator.

Why IP cores are important:

- reduce design time,
- reuse verified blocks,
- improve reliability,
- support platform-based design,
- reduce time-to-market.

Risks:

- integration mismatch,
- license restrictions,
- verification effort,
- clock/reset differences,
- bus protocol mismatch.

### NoC In Front-End Design

The NoC is planned at front-end architecture stage because it affects:

- communication topology,
- address map,
- bandwidth,
- latency,
- QoS,
- number of masters/slaves,
- clock-domain crossing,
- coherency and ordering.

### Final Exam Answer

Front-end chip design includes specification, architecture definition, RTL design, IP integration, memory map creation, interface definition, clock/reset planning and functional verification. IP cores are reusable hardware blocks such as processors, memory controllers, peripherals, accelerators and NoC components. They may be soft, firm or hard IP. IP reuse reduces design time and improves reliability but introduces integration and verification challenges. NoC is an important front-end architecture component because it defines scalable communication between SoC blocks and affects bandwidth, latency, QoS, routing, arbitration and system performance.
