# Sources - CLO 3 Topic 6

## Topic

Models of Simple Processor-Memory Interaction

## CLO Mapping

This maps to **CLO 3: Understand the Memory Design in SoC and Memory controller architecture**.

## Local Course Sources

- Syllabus/CLO image: [WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg](<../WhatsApp Image 2026-05-11 at 10.01.43 PM.jpeg>) lists **Models of Simple Processor-Memory Interaction** under **SoC Memory Design**, which maps to CLO 3.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.174](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=174>) introduces memory buffers, outstanding memory references and how insufficient buffering stalls processors.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.175](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=175>) introduces models of simple processor-memory interaction, contention, bandwidth and access time.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.176](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=176>) explains equivalence between n simple processors making one request each and one processor making n requests per memory service time.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.176](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=176>) defines achieved bandwidth B and Bw and relates service time to cache misses.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.177](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=177>) explains the Strecker-Ravi model assumptions and bandwidth formula.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.178](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=178>) gives examples showing relative performance degradation due to memory contention.
- Textbook: [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.179](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=179>) concludes that off-die memory access overhead and hundred-cycle memory access require large multilevel caches to match processor request rate.
- PPT/lecture PDF: [SOC components -processor.pdf, p.4](<../System on chip/SOC components -processor.pdf#page=4>) says system performance can model memory and interconnect as delay elements.
- PPT/lecture PDF: [SOC components -processor.pdf, p.18](<../System on chip/SOC components -processor.pdf#page=18>) says faster cache and memory reduce instruction/data fetch cycles.
- PPT/lecture PDF: [module 1 chip basics.pdf, p.7](<../System on chip/module 1 chip basics.pdf#page=7>) notes that cache misses can cause unanticipated extra cycles.

## Web Sources

- [AMD Integrated Memory Controller - Memory Interleaving](https://docs.amd.com/r/en-US/pg456-integrated-mc/Memory-Interleaving): official AMD documentation explaining that interleaving can provide 2x or 4x bandwidth of a single pipe.
- [Interference in multiprocessor computer systems with interleaved memory - Communications of the ACM](https://cacm.acm.org/research/interference-in-multiprocessor-computer-systems-with-interleaved-memory/): classic research context for contention in multiprocessor systems with interleaved memory.
- [CADS: Core-Aware Dynamic Scheduler for Multicore Memory Controllers](https://arxiv.org/abs/1907.07776): research context showing memory-controller scheduling is important when multicore processors share DRAM bandwidth.

## Figure References

- For simple-processor equivalence, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.176](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=176>) because Figure 4.28 shows n processors making one request each versus one processor making n requests.
- For Strecker-Ravi model formula, use [Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf, p.177](<../Computer System Design System-On-Chip by Michael J. Flynn and Wayne Luk.pdf#page=177>).

