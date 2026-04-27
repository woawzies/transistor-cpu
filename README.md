# Transistor CPU Design Specification
## Project Goals:
1. build a transistor computer out of discrete transistors only, no ICs
2. 4-bit word
3. modular and repeatable building blocks where possible
4. single shared bus
5. 2 cycle instruction execution
6. repeatability and stability over efficiency
7. dedicated alu input and output registers
## Registers
| Register | Purpose   |
|----------|-----------|
| A        | ALU IN A  |
| B        | ALU IN B  |
| C        | ALU OUT   |
| R0       | GPR       |
| R1       | GPR       |
| IR       | Inst. Reg |  

A and B are ALU registers, so they are write-only.  
C is an ALU output register, so it is read-only.  
R0 and R1 are general purpose registers, so they are read-write.
## CPU Block Diagram
<img width="629" height="346" alt="cpu-block-diagram" src="https://github.com/user-attachments/assets/e0be72de-ee7a-4012-a880-993bd7e96235" />
## Instructions
| Mnemonic                     | Description                                                  |
|------------------------------|--------------------------------------------------------------|
| lda r0/r1                    | load A register with either r0 or r1                         |
| ldb r0, r1                   | load B register with either r0 or r1                         |
| ildb imm                     | load B register with immediete                               |
| mov r0/r1, r0/r1 (dest, src) | move r0 or r1 to r0 or r1                                    |
| stoc r0/r1                   | store C register to either r0 or r1                          |
| add                          | add A register and B register and write result to C register |
| xor                          | xor A register and B register and write result to C register |  

Each instruction comes in on an 8 bit line. (S: src, D: dest, I: imm) in the form:  
```[ OPCODE (4) | DEST (2) | SRC (2) ]```
