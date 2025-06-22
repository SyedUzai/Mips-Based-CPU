# VHDL CPU Design Enhancement – ENGG3380 Project

## 📘 Overview

This project enhances a simple VHDL CPU design developed in a previous lab (Lab 5), focusing on adding data and instruction memory, program counters, and implementing more advanced instruction handling. The final design supports execution of a set of instructions automatically, including branching (`BNE`) and jumping (`JMP`) operations. The aim was to improve the CPU’s control and execution capabilities, allowing for more complex and realistic binary programs.

---

## 🧠 Problem Statement

The original CPU lacked memory modules and control flow instructions. This project introduces:

- **Data Memory Block**
- **Instruction Memory Block**
- **Program Counter**
- **Advanced Instructions**: `BNE` and `JMP`

With these additions, the CPU gains the ability to run full instruction sets, make conditional decisions, and perform iterations using loops and branches. The goal was to simulate realistic program execution on a custom-built CPU architecture in VHDL.

---

## ⚙️ System Overview

### Part 1 – Base CPU Enhancements:
- **Data Memory Block**: Enables data storage and retrieval.
- **3-to-1 MUX**: Selects between ALU result, data memory, or `SLT` result to write back into registers.
- **Instruction Memory**: Stores the instruction sequence loaded from a text file.
- **Program Counter**: Automatically increments to step through the instruction sequence.
- **Signal Routing**: Connected new blocks to existing modules to facilitate complete instruction execution.

### Part 2 – Control Flow Instructions:
- **BNE (Branch Not Equal)**:
  - Compares two registers (`rd` and `rs`)
  - If not equal, PC updates to PC + Immediate value
  - Required a **Zero Detection** logic and PC update path
- **JMP (Jump)**:
  - Updates PC with a 12-bit address concatenated with the upper 4 bits of the current PC
  - Implemented using an additional **3-to-1 MUX** and new control signals
- These enhancements enabled conditional and looping behavior.

---

## 📐 Assumptions and Constraints

- Limited to modifying provided code structure
- Register addresses and opcodes are **4 bits wide**, allowing for **16 operations**
- All data operations limited to **16-bit values**
- Test cases were derived from predefined instruction sets and verified using waveform analysis
- BNE implementation assumed inclusion of **ALU zero detection logic**

---

## ✅ Verification

Waveform simulations were used to validate instruction execution, memory usage, and control flow.

### 🔹 Part 1 – Basic Execution:
- Verified correct ALU operations and memory interactions
- Instruction address increased by `0x0002` after each step, indicating successful PC increments
- Instruction sequence processed linearly

### 🔹 Part 2 – Branching and Jumping:
- Verified `BNE` branches only when registers are unequal
- Verified `JMP` jumps unconditionally to the specified address
- Output signal (`Program Counter`) reflected changes in control flow
- Waveform clearly showed jumps from e.g., `0x001C → 0x0010`

---

## 🧾 Final Implementation Notes

- The final VHDL code includes:
  - Top-level module
  - ALU, Data Memory, Instruction Memory, Register File
  - Program Counter and all MUX modules
- All signals were organized and traced during simulation
- Screenshots captured key waveform behaviors, particularly for branch/jump tests

---

## 🛠️ How to Run

1. Load the VHDL files into a simulator like ModelSim or Vivado
2. Load the instruction text file into the instruction memory
3. Run the simulation and observe:
   - Program Counter behavior
   - Register and memory contents
   - ALU output and control signals
4. Match waveform results with expected output described above

---

## 📚 Skills Learned

- Structural VHDL design
- Instruction memory and data memory integration
- Multiplexer and control signal implementation
- Branching and jump instruction logic
- CPU control flow and instruction sequencing
- Signal-level debugging with waveform tools

---

## 📁 File Structure

```
.
├── cpu.vhd                 # Top-level CPU design
├── alu.vhd                 # Arithmetic Logic Unit
├── reg_file.vhd            # Register file
├── data_memory.vhd         # RAM for data
├── instr_memory.vhd        # ROM for instruction set
├── program_counter.vhd     # Program counter logic
├── mux_3to1.vhd            # Multiplexer for register writeback
├── testbench.vhd           # Simulation testbench
├── instructions.txt        # Instruction memory input
└── waveform_screenshots/   # Simulation result images
```

---

## 🔚 Conclusion

This project offered a deep dive into designing and simulating a CPU at the hardware description level. From memory access to conditional execution, the VHDL CPU is now equipped to handle realistic program structures and sets a strong foundation for future expansion, such as pipelining or additional instruction sets.
