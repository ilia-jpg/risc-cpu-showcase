# 32-bit RISC CPU — Project Showcase

A team-designed FPGA processor built in Verilog and SystemVerilog for ECE241 at the University of Toronto. The project combines a five-stage, 32-bit CPU, a custom instruction set, byte-addressable memory, a VGA debug display, and a programmable audio subsystem.

**This repository is a portfolio showcase. Course source code and shared project documents remain private.**

## My contribution

I'm **Ilia Javan**. My work spanned instruction design, RTL, memory integration, and the software tools needed to program the processor.

| Area | My contribution |
| --- | --- |
| Audio subsystem | Implemented the custom audio master and slave modules, including channel control and waveform generation/mixing |
| Instruction set and decode | Designed the final opcode format and instruction-decoder design, building on the team's earlier prototypes |
| Assembler | Built C++ assembly tools to encode instructions and generate memory initialization files |
| Data memory | Implemented byte-addressable memory with hardware support for unaligned accesses |
| FPGA RAM integration | Led configuration and integration of Intel RAM IP for instruction and data memory |
| Pipeline integration | Contributed extensively to finalizing and debugging the pipeline and connecting modules as part of the team |
| Hazard handling | Helped develop and debug the hazard detection unit |

## System overview

| Component | Purpose |
| --- | --- |
| Five-stage pipeline | Instruction fetch, decode, execute, memory access, and writeback |
| 32-bit datapath | Register data processing and arithmetic operations |
| Custom instruction set | Arithmetic, register moves, memory operations, and audio-control encodings |
| Hazard detection | Detects register dependencies and stalls instruction flow |
| Instruction memory | Stores encoded programs using FPGA RAM resources |
| Byte-addressable data memory | Supports data storage and load/store operations |
| VGA debug display | Shows register values, pipeline instructions, the program counter, and a memory view |
| Audio subsystem | Provides programmable waveform channels and a mixed audio sample output |

The instruction set is custom and inspired by RISC concepts. The processor is not presented as compatible with standard RISC-V binaries.

## Audio hardware

The custom master module handles commands for channel selection, enable state, period, amplitude, and pulse duty cycle. The slave module generates and mixes four channels:

- Two pulse-wave channels with selectable duty cycles.
- One triangle-wave channel.
- One noise channel.

I also developed the sample-request state machine used to interface with the supplied audio-controller hardware. It generates a single-cycle request when the controller is ready, avoiding repeated requests while readiness remains asserted.

The custom synthesis and control modules sit above the supplied Altera/Intel audio interface components. The course milestone report documents ModelSim waveform checks of the generator and handshake timing.

## Verification and implementation

Used ModelSim waveforms to verify pipeline control and debug hazard stalls and synchronous memory timing, and synthesized the RTL in Quartus Prime. The C++ assembler generated instruction-memory images and test programs for the custom ISA.

## Engineering decisions and challenges

**Keep the assembler and decoder consistent.** The final instruction format had to agree across assembly tools, operand selection, operation decoding, and the control signals propagated through the pipeline.

**Connect byte addressing to FPGA RAM.** Implementing the memory interface required coordinating address interpretation, data placement, and RAM IP behavior for instruction and data storage.

**Debug the processor as a system.** Correct modules still need compatible timing and control signals when connected. I worked with the team to debug pipeline wiring, memory interactions, and hazard handling during final integration.

**Make internal state visible.** The team's VGA display exposed processor state during instruction stepping, helping trace how instructions and values moved through the design.

## Teamwork and attribution

Built by **Ilia Javan, Avery Lor, and Linus**.

- **Ilia:** custom audio master/slave modules, final opcode format and decoder design, assembler, byte-addressable memory, Intel RAM IP setup, and substantial contributions to pipeline integration/debugging and hazard handling.
- **Avery:** VGA display development and system integration.
- **Linus:** initial pipeline implementation, register file, ALU, and hazard detection work.
- **Shared work:** final integration, debugging, and refinement of the processor. Early instruction/decoder prototypes were team work and are not claimed as Ilia's sole contribution.

The original source repository is maintained by Avery. Contributions were also exchanged through shared files and direct integration, so Git commit counts do not represent the full division of work.

## Tools and platform

**Verilog · SystemVerilog · C++ · Intel Quartus · ModelSim · Intel FPGA RAM IP · DE1-SoC · Computer architecture**

This repository contains a high-level project summary only. It does not distribute RTL, assembly programs, build artifacts, or course reports.
