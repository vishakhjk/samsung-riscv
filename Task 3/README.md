## RISC-V Instruction Set

This document provides a brief overview of the different instruction formats used in RISC-V.

### Instruction Formats

![RISC-V Instruction Formats](https://devopedia.org/images/article/110/3808.1535301636.png)

RISC-V instructions are encoded using various formats, each tailored for specific types of operations. The main formats are:

**1. R-type (Register-Register)**

* **Format:** `[funct7] rs2 rs1 funct3 rd opcode`
* **Description:** Used for register-to-register operations, such as addition, subtraction, and logical operations.
* **Fields:**
    - `funct7` (7 bits): Specifies the high-order bits of the operation.
    - `rs2` (5 bits): Source register 2.
    - `rs1` (5 bits): Source register 1.
    - `funct3` (3 bits): Specifies the low-order bits of the operation.
    - `rd` (5 bits): Destination register.
    - `opcode` (7 bits): Specifies the instruction type (R-type).

**2. I-type (Immediate)**

* **Format:** `imm[11:0] rs1 funct3 rd opcode`
* **Description:** Used for operations involving an immediate value, such as addition with an immediate, loads, and stores.
* **Fields:**
    - `imm[11:0]` (12 bits): Immediate value.
    - `rs1` (5 bits): Source register.
    - `funct3` (3 bits): Specifies the operation.
    - `rd` (5 bits): Destination register.
    - `opcode` (7 bits): Specifies the instruction type (I-type).

**3. S-type (Store)**

* **Format:** `imm[11:5] rs2 rs1 funct3 imm[4:0] opcode`
* **Description:** Used for store instructions, such as `sb`, `sh`, and `sw`.
* **Fields:**
    - `imm[11:5]` (7 bits): High-order bits of the immediate offset.
    - `rs2` (5 bits): Source register (value to be stored).
    - `rs1` (5 bits): Base register.
    - `funct3` (3 bits): Specifies the store operation (byte, halfword, word).
    - `imm[4:0]` (5 bits): Low-order bits of the immediate offset.
    - `opcode` (7 bits): Specifies the instruction type (S-type).

**4. B-type (Branch)**

* **Format:** `[12] imm[10:5] rs2 rs1 funct3 imm[4:1] [11] opcode`
* **Description:** Used for branch instructions, such as `beq`, `bne`, `blt`, etc.
* **Fields:**
    - `imm[10:5]` (6 bits): High-order bits of the immediate offset.
    - `rs2` (5 bits): Source register 2.
    - `rs1` (5 bits): Source register 1.
    - `funct3` (3 bits): Specifies the branch condition.
    - `imm[4:1]` (4 bits): Low-order bits of the immediate offset.
    - `[12]`, `[11]`: Sign bits for the immediate offset.
    - `opcode` (7 bits): Specifies the instruction type (B-type).

**5. J-type (Jump)**

* **Format:** `[20] imm[10:1] [11] imm[19:12] rd opcode`
* **Description:** Used for jump instructions, such as `jal` (jump and link).
* **Fields:**
    - `imm[19:12]` (8 bits): High-order bits of the immediate offset.
    - `imm[10:1]` (10 bits): Low-order bits of the immediate offset.
    - `[20]`, `[11]`: Sign bits for the immediate offset.
    - `rd` (5 bits): Destination register (for `jal`, this is the return address register).
    - `opcode` (7 bits): Specifies the instruction type (J-type).

**6. U-type (Upper Immediate)**

* **Format:** `imm[31:12] rd opcode`
* **Description:** Used for instructions that load an immediate value into a register, such as `lui` (load upper immediate).
* **Fields:**
    - `imm[31:12]` (20 bits): Immediate value.
    - `rd` (5 bits): Destination register.
    - `opcode` (7 bits): Specifies the instruction type (U-type).

### Instruction Examples

**1. `addi sp, sp, -48`**

* **Type:** I-type
* **Opcode:** 0010011
* **imm[11:0]:** 111111111100 (-48 in 2's complement)
* **rs1:** 00010 (sp)
* **funct3:** 000
* **rd:** 00010 (sp)

**2. `sd ra, 40(sp)`**

* **Type:** S-type
* **Opcode:** 0100011
* **imm[11:5]:** 0101000
* **rs2:** 00001 (ra)
* **rs1:** 00010 (sp)
* **funct3:** 011
* **imm[4:0]:** 00000

**3. `sd s0, 32(sp)`**

* **Type:** S-type
* **Opcode:** 0100011
* **imm[11:5]:** 0010000
* **rs2:** 10000 (s0)
* **rs1:** 00010 (sp)
* **funct3:** 011
* **imm[4:0]:** 00000

**4. `sd s1, 24(sp)`**

* **Type:** S-type
* **Opcode:** 0100011
* **imm[11:5]:** 0011000
* **rs2:** 10001 (s1)
* **rs1:** 00010 (sp)
* **funct3:** 011
* **imm[4:0]:** 00000

**5. `sd s2, 16(sp)`**

* **Type:** S-type
* **Opcode:** 0100011
* **imm[11:5]:** 0010000
* **rs2:** 10010 (s2)
* **rs1:** 00010 (sp)
* **funct3:** 011
* **imm[4:0]:** 00000

**6. `addi s0, sp, 48`**

* **Type:** I-type
* **Opcode:** 0010011
* **imm[11:0]:** 000000110000 (48 in binary)
* **rs1:** 00010 (sp)
* **funct3:** 000
* **rd:** 10000 (s0)

**7. `addi a0, s0, -688`**

* **Type:** I-type
* **Opcode:** 0010011
* **imm[11:0]:** 111011111000 (-688 in 2's complement)
* **rs1:** 10000 (s0)
* **funct3:** 000
* **rd:** 00001 (a0)

**8. `jal ra, printf`**

* **Type:** J-type
* **Opcode:** 1101111
* **rd:** 00001 (ra)
* **imm[19:12]:** (Calculated based on target)
* **imm[10:1]:** (Calculated based on target)
* **[20], [11]:** (Sign bits, calculated based on target)

**9. `lw s0, 32(sp)`**

* **Type:** I-type
* **Opcode:** 0000011
* **imm[11:0]:** 000000100000 (32 in binary)
* **rs1:** 00010 (sp)
* **funct3:** 010
* **rd:** 10000 (s0)

**10. `blez s1, <main+offset>`**

* **Type:** B-type
* **Opcode:** 1100011
* **rs1:** 10001 (s1)
* **rs2:** 00000 (zero)
* **funct3:** 110
* **imm[10:5]:** (Calculated based on offset)
* **imm[4:1]:** (Calculated based on offset)
* **[12], [11]:** (Sign bits, calculated based on offset)

**11. `add s1, s1, 1`**

* **Type:** R-type
* **Opcode:** 0110011
* **rs1:** 10001 (s1)
* **rs2:** 00001 (1)
* **funct3:** 000
* **rd:** 10001 (s1)
* **funct7:** 0000000

**12. `li s2, 1`**

* **Type:** I-type (Pseudo-instruction)
* **Opcode:** 0010011
* **imm[11:0]:** 000000000001 (1 in binary)
* **rs1:** 00000 (zero)
* **funct3:** 000
* **rd:** 10010 (s2)

**13. `jal ra, __muldi3`**

* **Type:** J-type
* **Opcode:** 1101111
* **rd:** 00001 (ra)
* **imm[19:12]:** (Calculated based on target)
* **imm[10:1]:** (Calculated based on target)
* **[20], [11]:** (Sign bits, calculated based on target)

**14. `addi sp, sp, 48`**

* **Type:** I-type
* **Opcode:** 0010011
* **imm[11:0]:** 000000110000 (48 in binary)
* **rs1:** 00010 (sp)
* **funct3:** 000
* **rd:** 00010 (sp)

**15. `ret`**

* **Type:** Pseudo-instruction (Equivalent to jalr zero, ra, 0)
* **Opcode:** 1100111
* **rd:** 00000 (zero)
* **funct3:** 000
* **rs1:** 00001 (ra)
* **imm[11:0]:** 000000000000 (0 in binary) 
