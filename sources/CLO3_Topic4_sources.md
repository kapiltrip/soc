# Sources - CLO 3 Topic 4

## Topic

Quality-Aware Scheduling

## CLO Mapping

This maps to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **Quality aware scheduling** under **SoC Memory Design**.
- PPT/lecture PDF: [SOC components -processor.pdf, p.4](<../System on chip/SOC components -processor.pdf#page=4>) says processor performance and system performance can treat memory and interconnect components as delay elements.
- PPT/lecture PDF: [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>) says faster cache and memory reduce instruction-fetch and data-fetch cycles.
- PPT/lecture PDF: [SOC components -processor.pdf, p.20](<../System on chip/SOC components -processor.pdf#page=20>) discusses resource contention and delays when successive instructions need the same resource.
- PPT/lecture PDF: [module 1 part 1 introduction to system approach.pdf, p.39](<../System on chip/module 1 part 1 introduction to system approach.pdf#page=39>) says processor, memory or I/O should be sized to meet high-priority real-time constraints.
- Lecture: [Functional Architecture Co Design 2.pdf, p.16](<../System on chip/Functional Architecture Co Design 2.pdf#page=16>) lists memory components, buses, RTOS and hardware processing units as part of architecture modeling.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.46](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=46>) discusses real-time/throughput constraints and processor-memory-interconnect performance.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.171](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=171>) and p.172 explain banked SDRAM access, row activation, interleaving and timing behavior that memory scheduling exploits.

## Web / Research Sources

- [AMD Versal Adaptive SoC Technical Reference Manual - Quality of Service](https://docs.amd.com/r/en-US/am011-versal-acap-trm/Quality-of-Service): official AMD documentation explaining AXI QoS signals and traffic classes such as low latency, isochronous and best effort.
- [Arm AMBA Specifications](https://www.arm.com/architecture/system-architectures/amba/amba-specifications): official Arm page for AMBA protocols including AXI, used for QoS-capable SoC interconnect traffic.
- [Arm Community - Quality of Service in Arm Systems](https://developer.arm.com/community/arm-community-blogs/b/soc-design-and-simulation-blog/posts/quality-of-service-in-arm-systems-an-overview): explains QoS in SoC interconnects and memory controllers for low-latency, real-time and bandwidth-demanding masters.
- [Architecture and analysis of a dynamically-scheduled real-time memory controller](https://link.springer.com/article/10.1007/s11241-015-9235-y): research source on real-time memory-controller scheduling, transaction timing and worst-case response time.
- [SQUASH: Simple QoS-Aware High-Performance Memory Scheduler for Heterogeneous Systems with Hardware Accelerators](https://arxiv.org/abs/1505.07502): research source on QoS-aware memory scheduling for heterogeneous systems with accelerators.
- [Power/performance trade-offs in real-time SDRAM command scheduling](https://research.tue.nl/en/publications/powerperformance-trade-offs-in-real-time-sdram-command-scheduling/): research source connecting SDRAM command scheduling with power/performance tradeoffs.

## Figure References

- For a quality-aware scheduling diagram, draw CPU/GPU/DMA/real-time masters feeding a QoS-aware memory scheduler, then SDRAM banks.
- For traffic-class wording, cite AMD Versal QoS documentation: low latency, isochronous and best effort.
- For bank/row-buffer scheduling context, cite Flynn/Luk p.171-p.172 and the real-time memory-controller paper.

