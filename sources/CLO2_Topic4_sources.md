# CLO 2 Topic 4 Sources - Models Of Simple Processor-Memory Interaction

Main note: [../CLO2.md](<../CLO2.md>)

Topic image part 1: [../images/Screenshot 2026-05-12 230134.png](<../images/Screenshot 2026-05-12 230134.png>)

Topic image part 2: [../images/Screenshot 2026-05-12 230141.png](<../images/Screenshot 2026-05-12 230141.png>)

Syllabus/CLO image: [../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>)

## Local PPT / Book References

### 1. `Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf`

Useful pages:

- p.174: Discusses memory buffers, outstanding memory references and how insufficient buffering can stall processors. Used for outstanding request and buffering explanation.
- p.175: Introduces simple processor-memory interaction models, contention, access time and bandwidth. Used for the main topic structure.
- p.176: Shows the equivalence between `n` simple processors making one request each and one processor making `n` requests per memory service time. Used for the pipelined processor equivalence diagram.
- p.176: Defines achieved bandwidth and relates memory service time to cache misses. Used for service-time and bandwidth explanation.
- p.177: Explains the Strecker-Ravi model assumptions and bandwidth formula. Used for `B = m [1 - (1 - 1/m)^n]`.
- p.178: Gives examples showing relative performance degradation due to memory contention. Used for the example and interpretation section.
- p.179: Explains that off-die memory access overhead and long memory access time require large multilevel caches to match processor request rate. Used for cache and memory-bottleneck explanation.

### 2. `System on chip/SOC components -processor.pdf`

Useful pages:

- p.4: Says system performance can model memory and interconnect as delay elements. Used for why processor-memory interaction models matter.
- p.18: Says faster cache and memory reduce instruction/data fetch cycles. Used for the cache relation section.

### 3. `System on chip/module 1 chip basics.pdf`

Useful pages:

- p.7: Notes that cache misses can cause unanticipated extra cycles. Used for memory stalls and miss penalty.
- p.13: Discusses power categories, useful when connecting extra memory traffic to power.

### 4. `System on chip/module 1 part 1 introduction to system approach.pdf`

Useful pages:

- p.20-p.22: Discusses off-chip memory, memory management and cache hierarchy. Used for the relationship between processor-memory interaction and on/off-die memory hierarchy.
- p.31-p.32: Discusses interconnect hierarchy and bandwidth close to the CPU. Used for the request path through interconnect.
- p.39-p.42: Discusses sizing processor/memory/I/O for constraints and design complexity. Used for system-level memory sizing and performance reasoning.

### 5. Existing Related Notes

- [../CLO3.md](<../CLO3.md>) Topic 6 already contains the CLO3 memory-controller version of this topic.
- [CLO3_Topic6_sources.md](<CLO3_Topic6_sources.md>) contains detailed source pointers for the memory-design mapping.

## Web References

### 1. AMD Integrated Memory Controller - Memory Interleaving

URL: https://docs.amd.com/r/en-US/pg456-integrated-mc/Memory-Interleaving

Used for:

- Real hardware example of memory interleaving.
- Interleaving making participating memory controllers appear as one large memory pool.
- Traffic balancing across DDR controllers.
- Explaining how the simple `m memory modules` model appears in practical memory-controller designs.

### 2. Arm Learning Path - Memory Subsystem

URL: https://learn.arm.com/learning-paths/servers-and-cloud-computing/memory-subsystem/

Used for:

- Current Arm learning material on CPU topology, cache hierarchy, memory latency, multicore bandwidth and loaded latency.
- Supporting the idea that memory performance must be analyzed separately from raw CPU execution speed.

### 3. Intel Advisor - Remove Memory Bottlenecks

URL: https://www.intel.com/content/www/us/en/developer/articles/technical/remove-memory-bottlenecks-using-advisor.html

Used for:

- Practical explanation that loops/workloads can be memory-bound and limited by memory bandwidth.
- Supporting the compute-bound versus memory-bound discussion.
- Supporting memory hierarchy bandwidth as a performance concern.

### 4. Communications of the ACM - Interference in Multiprocessor Computer Systems With Interleaved Memory

URL: https://cacm.acm.org/research/interference-in-multiprocessor-computer-systems-with-interleaved-memory/

Used for:

- Classic research context for multiprocessor contention in interleaved memory systems.
- Supports the idea that multiple processors competing for memory modules create interference/contention.

### 5. CADS: Core-Aware Dynamic Scheduler For Multicore Memory Controllers

URL: https://arxiv.org/abs/1907.07776

Used for:

- Research context showing that memory-controller scheduling remains important when multiple cores share DRAM bandwidth.
- Supports the link between simple interaction models and real multicore memory scheduling.

## Figure References

- For the pipelined equivalence diagram, look at [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.176](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=176>).
- For the Strecker-Ravi model formula, look at [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.177](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=177>).

## Why These Sources Were Used

This topic is mathematically based in Flynn/Luk, especially pages 175-178. The local PPTs explain why memory/interconnect delay matters in SoC performance. Web sources were used to connect the simple model to current real systems: AMD for memory interleaving, Arm and Intel for memory hierarchy/bottleneck analysis, and research sources for multicore contention and memory-controller scheduling.
