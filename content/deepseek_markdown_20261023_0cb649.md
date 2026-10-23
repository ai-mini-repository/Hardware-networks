# CPU & Memory: How Instructions Become Actions

> **Project:** Computational Science & AI — Hardware + Networks  
> **Related files:** `application-launch-professional.md`, `computer-startup.md`, `how-data-travels.md`

---

## 1. Overview

When you double-click an application, the operating system loads its executable file from disk into **RAM (Random Access Memory)**. The **CPU (Central Processing Unit)** then begins fetching instructions from that memory, decoding them, and executing them — billions of times per second. This document explains the hardware mechanisms behind that process: the instruction cycle, the memory hierarchy, and why the CPU is rarely the only bottleneck.

---

## 2. The Instruction Cycle: Fetch → Decode → Execute

Every CPU operates on a simple but powerful loop. Princeton's computer architecture course describes it as: **FETCH** the next instruction from memory → **DECODE** what it does → **EXECUTE** the operation → repeat.

Modern processors refine this into five classic stages:

| Stage | What Happens |
|-------|--------------|
| **Fetch (F)** | The CPU reads the instruction at the address stored in the **Program Counter (PC)**. |
| **Decode (D)** | The instruction bits are decoded into control signals. Operands are read from the **register file**. |
| **Execute (X)** | The **ALU (Arithmetic Logic Unit)** performs the computation (add, shift, compare, etc.). |
| **Memory Access (M)** | Only load/store instructions access RAM here. |
| **Write-back (W)** | Results are written back into the register file. |

**Key insight:** The PC is a special register that holds the address of the *next* instruction. After each fetch, it increments (or jumps, for branches), so the CPU always knows where to go next.

### Pipeline: Why Your CPU Is Faster Than One Instruction at a Time

A naive CPU would complete all five stages for one instruction before starting the next. A **pipelined** processor overlaps stages: while one instruction is being decoded, the next is being fetched, and the one before is executing.
