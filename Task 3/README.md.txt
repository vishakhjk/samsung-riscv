1. Instruction: addi sp, sp, -48
Type: I-type
Opcode: 0010011 (7 bits)
Immediate: 111111111100 (12 bits, -48 in 2's complement)
Source Register (rs1): 00010 (sp, 5 bits)
Destination Register (rd): 00010 (sp, 5 bits)
Function (funct3): 000 (3 bits)

2. Instruction: sd ra, 40(sp)
Type: S-type
Opcode: 0100011 (7 bits)
Immediate: 0101000 (40, split into imm[11:5])
Source Register (rs1): 00010 (sp, 5 bits)
Source Register (rs2): 00001 (ra, 5 bits)
Function (funct3): 011 (3 bits)

3. Instruction: sd s0, 32(sp)
Type: S-type
Opcode: 0100011 (7 bits)
Immediate: 0010000 (32, split into imm[11:5])
Source Register (rs1): 00010 (sp, 5 bits)
Source Register (rs2): 10000 (s0, 5 bits)
Function (funct3): 011 (3 bits)

4. Instruction: sd s1, 24(sp)
Type: S-type
Opcode: 0100011 (7 bits)
Immediate: 0011000 (24, split into imm[11:5])
Source Register (rs1): 00010 (sp, 5 bits)
Source Register (rs2): 10001 (s1, 5 bits)
Function (funct3): 011 (3 bits)

5. Instruction: sd s2, 16(sp)
Type: S-type
Opcode: 0100011 (7 bits)
Immediate: 0010000 (16, split into imm[11:5])
Source Register (rs1): 00010 (sp, 5 bits)
Source Register (rs2): 10010 (s2, 5 bits)
Function (funct3): 011 (3 bits)

6. Instruction: addi s0, sp, 48
Type: I-type
Opcode: 0010011 (7 bits)
Immediate: 000000110000 (12 bits, 48 in binary)
Source Register (rs1): 00010 (sp, 5 bits)
Destination Register (rd): 10000 (s0, 5 bits)
Function (funct3): 000 (3 bits)

7. Instruction: addi a0, s0, -688
Type: I-type
Opcode: 0010011 (7 bits)
Immediate: 111011111000 (12 bits, -688 in 2's complement)
Source Register (rs1): 10000 (s0, 5 bits)
Destination Register (rd): 00001 (a0, 5 bits)
Function (funct3): 000 (3 bits)

8. Instruction: jal ra, printf
Type: J-type
Opcode: 1101111 (7 bits)
Immediate: printf_offset (20 bits, calculated based on target)
Destination Register (rd): 00001 (ra, 5 bits)

9. Instruction: lw s0, 32(sp)
Type: I-type
Opcode: 0000011 (7 bits)
Immediate: 000000100000 (12 bits, 32 in binary)
Source Register (rs1): 00010 (sp, 5 bits)
Destination Register (rd): 10000 (s0, 5 bits)
Function (funct3): 010 (3 bits)

10. Instruction: blez s1, <main+offset>
Type: B-type
Opcode: 1100011 (7 bits)
Immediate: offset (12 bits, calculated as branch offset)
Source Register (rs1): 10001 (s1, 5 bits)
Source Register (rs2): 00000 (zero, 5 bits)
Function (funct3): 110 (3 bits)

11. Instruction: add s1, s1, 1
Type: R-type
Opcode: 0110011 (7 bits)
Function (funct7): 0000000 (7 bits)
Source Register (rs1): 10001 (s1, 5 bits)
Source Register (rs2): 00001 (1, 5 bits)
Destination Register (rd): 10001 (s1, 5 bits)
Function (funct3): 000 (3 bits)

12. Instruction: li s2, 1
Type: Pseudo (Expanded to addi)
Opcode: 0010011 (7 bits)
Immediate: 000000000001 (12 bits, 1 in binary)
Source Register (rs1): 00000 (zero, 5 bits)
Destination Register (rd): 10010 (s2, 5 bits)
Function (funct3): 000 (3 bits)

13. Instruction: jal ra, __muldi3
Type: J-type
Opcode: 1101111 (7 bits)
Immediate: muldi3_offset (20 bits, calculated based on target)
Destination Register (rd): 00001 (ra, 5 bits)

14. Instruction: addi sp, sp, 48
Type: I-type
Opcode: 0010011 (7 bits)
Immediate: 000000110000 (12 bits, 48 in binary)
Source Register (rs1): 00010 (sp, 5 bits)
Destination Register (rd): 00010 (sp, 5 bits)
Function (funct3): 000 (3 bits)

15. Instruction: ret
Type: Pseudo (Equivalent to jalr zero, ra, 0)
Opcode: 1100111 (7 bits)
Immediate: 000000000000 (12 bits, 0 in binary)
Source Register (rs1): 00001 (ra, 5 bits)
Destination Register (rd): 00000 (zero, 5 bits)
Function (funct3): 000 (3 bits)