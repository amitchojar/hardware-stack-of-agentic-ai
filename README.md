# The Hardware Stack of Agentic AI

### From Transistors to Tokens

**Amit Chojar** · First Edition · Two Volumes

A handbook for engineers who build, operate, and debug LLM and agentic AI
systems, and who want to understand what the hardware underneath is actually
doing. The book follows a single agentic request from the moment a user
presses Enter: through the CPU orchestrator, system memory, storage and
retrieval, the GPU, the network fabric, and back. Along the way it derives
the arithmetic that tells you *why* a system is slow, *which* resource is the
bottleneck, and *what* will actually help.

Enduring principles come first. Current silicon (H100, B200, Rubin) appears
as case studies, not as the foundation, so the reasoning still holds when the
next generation ships.

---

## Book Releases & Stats

**Total Project Reach:** ![Total Readers](https://img.shields.io/github/downloads/amitchojar/hardware-stack-of-agentic-ai/total?label=Total%20Readers&color=blue&style=flat-square)

| Volume | Contents | Version | Status | Individual Downloads | Download Link |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Part One: Following a Request Through the Stack** | Chapters 1–10 · Appendices A–G | `part-one-v1.0` | ✅ Available | ![Part One](https://img.shields.io/github/downloads/amitchojar/hardware-stack-of-agentic-ai/part-one-v1.0/total?label=Downloads&color=green) | [Get Part One PDF](https://github.com/amitchojar/hardware-stack-of-agentic-ai/releases/latest/download/The_Hardware_Stack_of_Agentic_AI_Part_1_ed_1.pdf) |
| **Part Two: Training and Bottlenecks** | Chapters 11–19 · Appendix A | — | 🕓 Forthcoming | — | — |

**Part One is available now; Part Two is in preparation and will be released
separately.** Part One stands on its own: it includes its own Decision Map
and Notation and Symbols reference, and explains every concept it uses.
Chapter numbering is continuous across the two volumes, so references in
Part One of the form "Part Two, Chapter N" point ahead to the forthcoming
volume.

---

## Who This Book Is For

- **ML and inference engineers** who serve models and need to reason about
  latency, throughput, and cost from first principles.
- **Backend and platform engineers** building agent systems who want to know
  why an agent loop stalls, where the time goes, and which knob to turn.
- **Infrastructure and capacity planners** sizing GPU fleets, KV-cache
  memory, and interconnects for production agentic workloads.
- **Anyone** who has read that "decode is memory-bound" and wants the
  derivation, not the slogan.

Prerequisites: comfort with Python, basic linear algebra, and a working
familiarity with transformers. Every hardware concept is explained in the
book where it is first used.

---

## What's Inside

### Part One — Following a Request Through the Stack

1. **Anatomy of an Agentic Request** — the end-to-end path of one request and its latency budget
2. **The CPU — Orchestrator of the Stack** — why agent loops are CPU-heavy: Python overhead, async, serialization
3. **RAM and the Memory Hierarchy** — DDR5, LPDDR5X, HBM anatomy; where weights and the KV cache actually live
4. **Storage and Retrieval** — NVMe, PCIe, vector-index physical layout, the latency budget of RAG
5. **The GPU — Parallel Compute Engine** — SMs, CUDA and tensor cores, MMA/WGMMA, occupancy, the on-chip memory hierarchy
6. **Number Formats, Quantization, and Precision** — FP32 to FP4, BF16 vs FP16, MXFP, PTQ/QAT, KV-cache quantization
7. **Prefill — The Compute-Bound Phase** — full FlashAttention forward and WGMMA kernel walkthroughs
8. **Decode — The Memory-Bound Phase** — KV-cache sizing, paged attention, speculative decoding
9. **Tool Calls, Networks, and Fabrics** — NVLink, PCIe, InfiniBand/RoCE, GPUDirect RDMA, orchestration amplification
10. **Agent Memory and Context Compaction** — memory classes, compaction strategies, prefix-cache interactions

**Appendices (Part One)**

- A. Back-of-Envelope Sizing Math for Agentic Deployments
- B. Hopper → Blackwell → Rubin: What Changed and Why the Principles Didn't
- C. Inference Serving Engines: vLLM and SGLang in Depth
- D. Hardware Beyond NVIDIA: TPU, AMD, and Trainium
- E. Cluster-Scale Inference Orchestration: Dynamo as Reference Architecture
- F. The Mathematics of Attention-Weight Concentration
- G. Beyond Autoregression: Non-Autoregressive Decision Models

### Part Two — Training and Bottlenecks as First Principles *(forthcoming)*

*Training: A Different Beast*

11. **The Forward-Backward Pass and Training Memory** — the 18P rule, activation checkpointing, FlashAttention backward
12. **Parallelism Strategies** — DP, TP, PP, SP, EP; ZeRO and FSDP; the pipeline-bubble formula
13. **Collective Communication and Topology** — all-reduce bounds, ring vs. tree, NCCL algorithm selection

*Bottlenecks as First-Class Principles*

14. **Compute-Bound: The Roofline Model** — roofline derivation and ridge points from V100 to B200
15. **Memory-Bandwidth-Bound: The Memory Wall** — the decode latency law, kernel fusion, quantization
16. **Latency-Bound: Little's Law and Queueing** — M/M/1, Pollaczek–Khinchine, TTFT, admission control
17. **Capacity-Bound: When It Doesn't Fit** — the capacity equation, sharding decisions, CPU/NVMe offload
18. **I/O-Bound: When the Bits Are Somewhere Else** — cold starts, streaming RAG, GPUDirect Storage
19. **Scheduling, Batching, and End-to-End Performance** — continuous batching, chunked prefill, KV-aware routing

**Appendix (Part Two)**

- A. Reading Nsight and nvtop Output

---

## How Each Chapter Is Built

Every chapter follows the same structure:

- **An opening problem** drawn from a real production symptom
- **A gentle introduction** before the formalism
- **Full derivations**, with generic examples first and agentic examples second
- **Production code and kernels**, not pseudocode
- **Failure modes** and how to recognize them in a profiler
- **Questions Worth Reviewing**, with worked answers
- **A summary box** and **further reading**

The running example throughout is a representative clinical chart-review
agent, used to ground every number in a realistic workload.

---

## Companion Book

*Linear Algebra for Large Language Models, Part One* develops the
mathematics behind attention, embeddings, and the transformer in depth. The
two books are independent; each explains every concept it uses.

---

## License

This work is licensed under the Creative Commons
Attribution-NonCommercial-ShareAlike 4.0 International License
(CC BY-NC-SA 4.0).

**You are free to:**

- **Share** — copy and redistribute the material in any medium or format,
  including downloading the PDF and sharing it with colleagues, students, or
  online communities.
- **Adapt** — remix, transform, and build upon the material.

**Under the following terms:**

- **Attribution** — You must give appropriate credit, provide a link to the
  license, and indicate if changes were made.
- **NonCommercial** — You may not use the material for commercial purposes.
  No one may sell this book, place it behind a paywall, or use it to generate
  revenue in any form.
- **ShareAlike** — If you remix, transform, or build upon the material, you
  must distribute your contributions under the same license.

Classroom and educational use is expressly encouraged: teachers and
instructors may freely distribute this book to students at no charge without
requesting permission.

Full license text: https://creativecommons.org/licenses/by-nc-sa/4.0/

---

## Citation

```bibtex
@book{chojar2026hardwarestack,
  author    = {Amit Chojar},
  title     = {The Hardware Stack of Agentic AI: From Transistors to Tokens},
  edition   = {First},
  year      = {2026},
  note      = {Part One},
  url       = {https://github.com/amitchojar/hardware-stack-of-agentic-ai}
}
```

---

## Feedback

Found an error, or have a suggestion? Please open an
[issue](https://github.com/amitchojar/hardware-stack-of-agentic-ai/issues).
Corrections are credited in subsequent editions.

© 2026 Amit Chojar
