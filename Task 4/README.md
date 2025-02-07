# Functional Simulation of RISC-V Instructions using Verilog Netlist

## Overview
This document provides step-by-step instructions on performing the functional simulation of RISC-V instructions modeled as a Verilog netlist. The simulation will be carried out using Icarus Verilog (`iverilog`) for compiling and simulating the design, and GTKWave for visualizing the waveform outputs.

## Prerequisites
Ensure you have the required tools installed on your system:

```sh
sudo apt install iverilog gtkwave
```

## Steps to Perform Functional Simulation

### 1. Create a Project Directory
Create a new directory using your name as the identifier:

```sh
mkdir <your_name>
cd <your_name>
```

### 2. Create Verilog and Testbench Files
Use the `touch` command to create the required Verilog and testbench files:

```sh
touch rv32i_core.v rv32i_tb.v
```

### 3. Clone the Reference Verilog Code
Instead of writing the Verilog code manually, clone the reference GitHub repository and copy the relevant Verilog and testbench code into the files created in Step 2.

**Reference GitHub Repository:** `iiitb_rv32i`

![main_code](C:/Users/visha/Downloads/maincode.png)

![testbench](C:/Users/visha/Downloads/testbench.png)

### 4. Compile the Verilog Code
Run the following command to compile the Verilog design and generate a Value Change Dump (VCD) file:

```sh
iverilog -o rv32i_core rv32i_core.v rv32i_tb.v
vvp rv32i_core
```

### 5. Open GTKWave for Analysis
GTKWave is used to analyze the waveform of the RISC-V instruction execution. Run the following command to open the generated `.vcd` file:

```sh
gtkwave rv32i_core.vcd
```

## Instruction Encoding
The provided Verilog file uses hard-coded instruction encodings instead of the standard RISC-V encoding. Below is a comparison:

| Operation | Description | Standard RISC-V Encoding | Hard-Coded Encoding |
|-----------|------------|-------------------------|---------------------|
| ADD R6, R2, R1 | Adds R2 and R1, stores result in R6 | `32'h00110333` | `32'h02208300` |
| SUB R7, R1, R2 | Subtracts R2 from R1, stores in R7 | `32'h402083b3` | `32'h02209380` |
| AND R8, R1, R3 | Bitwise AND between R1 and R3, stores in R8 | `32'h0030f433` | `32'h0230a400` |
| OR R9, R2, R5 | Bitwise OR between R2 and R5, stores in R9 | `32'h005164b3` | `32'h02513480` |
| XOR R10, R1, R4 | Bitwise XOR between R1 and R4, stores in R10 | `32'h0040c533` | `32'h0240c500` |
| SLT R1, R2, R4 | Set R1 to 1 if R2 < R4, else 0 | `32'h0045a0b3` | `32'h02415580` |
| ADDI R12, R4, 5 | Adds immediate value 5 to R4, stores in R12 | `32'h004120b3` | `32'h00520600` |
| BEQ R0, R0, 15 | Branch if R0 == R0 | `32'h00000f63` | `32'h00f00002` |
| SW R3, R1, 2 | Store word at memory address (R1 + 2) | `32'h0030a123` | `32'h00209181` |
| LW R13, R1, 2 | Load word from memory address (R1 + 2) | `32'h0020a683` | `32'h00208681` |
| SRL R16, R14, R2 | Shift right logical | `32'h0030a123` | `32'h00271803` |
| SLL R15, R1, R2 | Shift left logical | `32'h002097b3` | `32'h00208783` |

## Verifying Instructions in GTKWave
Once the simulation is complete, you can observe the execution of each instruction in GTKWave. Below is the expected verification process:

1. **ADD R6, R2, R1**
   - Observing the `EX_MEM_ALU_OUT` signal in GTKWave to verify the sum of R2 and R1.

2. **SUB R7, R1, R2**
   - Checking the waveform to confirm the subtraction operation.

3. **AND R8, R1, R3**
   - Verifying bitwise AND operation output in the ALU result.

4. **OR R9, R2, R5**
   - Checking OR operation results in the `EX_MEM_ALU_OUT` signal.

5. **XOR R10, R1, R4**
   - Observing `EX_MEM_ALU_OUT` for bitwise XOR result.

6. **SLT R1, R2, R4**
   - Ensuring correct comparison result in R1.

7. **ADDI R12, R4, 5**
   - Observing immediate addition result in R12.

8. **SW R3, R1, 2**
   - Ensuring memory storage of R3 at computed memory address.

9. **SRL R16, R11, R2**
   - Checking logical right shift result.

10. **BEQ R0, R0, 15**
    - Verifying branch decision logic and PC update.

11. **BNE R0, R1, 15**
    - Checking branch execution if values are not equal.

12. **SLL R15, R1, R2**
    - Observing logical left shift output in `EX_MEM_ALU_OUT`.

## Conclusion
This document provides a structured approach to performing functional simulations of RISC-V instructions using Icarus Verilog and GTKWave. The verification process ensures that the hard-coded instruction encodings execute correctly and match expected results. Use this guide to set up and analyze your Verilog-based RISC-V implementation efficiently.
