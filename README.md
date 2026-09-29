
# Core

- A CPU core is just a machine that does one thing on a loop
- Fetch-> decode->execute-> writeback
- All cores work this same loop.The difference between different cores is that how fast and how big they do each step
- Example:
laptop's CPU does this loop billions of times a second, using huge circuits that work on 32 or 64 bits simultaneously.
While SERV does the exact same loop but slower and smaller
# SERV architecture
- The base ISA is minimal, SERV only has to build hardware for ~40 instructions.
## ISA fundamentals
### RV32I
- RV32 = RISC-V, 32-bit (registers and addresses are 32 bits wide)
- I = the base Integer instruction set — the minimum required set, roughly 40 instructions
- Compare it to x86, which has hundreds of instructions . RV32I fits on a couple of pages because the philosophy is: keep the hardware simple
- What RV32I can do?

Arithmetic: add, sub

Logic: and, or, xor

Shifts: sll, srl, sra

Comparisons: slt, sltu

Loads/stores: lw, sw, lb, sb, etc.

Branches: beq, bne, blt, bge

Jumps: jal, jalr

Upper immediate: lui, auipc
- Here, we can see that RV32I can't do multiplication and division
- if a specific core choses to perform multiplication or divisions they can make the use of extensions, for example ext M
### Instruction Formats
- Every RV32I instruction is exactly 32 bits wide
#### 6 Formats
1. R-type (Register) — for register-to-register ops like add, sub, and, xor

- Needs: two source registers, one destination register, an operation code
2. I-type (Immediate) — for ops with a constant baked into the instruction, like addi, loads (lw), and jalr
- Needs: one source register, one destination register, a 12-bit immediate constant
3. S-type (Store) — for stores like sw, sb

Needs: two source registers (base address + value to store) and an immediate offset
Notably has no destination register — stores don't write back to a register, they write to memory

4. B-type (Branch) — for conditional branches like beq, bne, blt

Needs: two source registers to compare, and an immediate offset (the branch target)
Also has no destination register — branches don't produce a value, they just redirect the PC

5. U-type (Upper immediate) — for lui, auipc

Needs: one destination register and a large 20-bit immediate
Used to build big constants, since a normal 12-bit immediate can't hold much

6. J-type (Jump) — for jal

Needs: one destination register (to save the return address) and a large jump offset
### The core idea behind serv:
- a bit-serial architecture processes multi-bit data one bit per clock cycle through a single-bit-wide datapath, instead of processing all bits simultaneously through a wide datapath.
- If we are building a tiny chip, lets say for a light sensor in a smartwatch, we do not need the chip to work very fast instead we prefer that chip to be made at a lower cost and occupying very less area.Hence, in designing such a chip we perfer serv
  
## SERV ALU
- Serv ALU is of 1 bit
- it performs all the arithmatic functions
- The circuit repeats the cycle 32 times
## Register file
### RAM based storage-
- SERV uses RAM to store bits as compared to any other CPU that uses flip flops to store bits
- fetching data from RAM is much slower than fetching data from RAM
- This type of architecture is not suitable for any complex cpu as speed is very slow
- But it solves SERV's agenda of occupying less space
  
 
