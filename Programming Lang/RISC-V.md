# Computer Organization Final Term Report
Author
* Student id : 410821238
* Name : 余慶龍
* Grade : 資工二

Last Modified Date: 2021/6/13

# RISC-V Review
## Preview
Have 31 registers (x1-x31)
* x0: constant 0
* x1: return addr(standard software calling convention)
* additional user-visible register *pc*  addr of current instruction

XLEN <- register bits wide
RV32 : registers are 32bits wide
RV64: 64bits wide

## Base Instruction Formats
4 base foramts with **32 bits** (aligned on four-byte)

![](https://i.imgur.com/N0yZdNU.png)

*rs1* *rs2* is source
*rd* is destination
*imm[x]* is immediated field with bit position

The **Sign bit** is alyways in *bit 31*

## Immediate Formats Variant
Which is the Foramt B-tpye and J-type

Diffierence between S/B type:
These are both 12-bit immediate field and B-type with one-bit left shift of immediate value.

* Every formats can present different bits and type immediate value.
* This figure shows how we put the bits of immediate value to instruction format (Label with instruction bit *inst[y]*)

![](https://i.imgur.com/M37pNaH.png)

## Integer Computation
1. I-type as register-immediate operation
2. R-type as rigster-register operation


* MIPS would throws overflow exception and RISC-V won't.
To deal with overflow problem, implementing by ourself.
e.g. We can check unsigned overflow like this
```
add 	t0, t1, t2;
bltu 	t0, t1, overflow; # branch less than unsigned
```

---
## Register Instructions
### I-type
![](https://i.imgur.com/TLRJBhu.png)

Arthmetic:
* Use `ADDI rd, rs1, 0` to implement `MV rd, rs1` 
* `SLTI` (set less than immediate )put 1 in register *rd* if *rs1* less than immeidate. And `SLITU` is for unsigned.

Logic operation:
* `ANDI` `ORI` `XORI` are logical operations
* Using `XORI rd, rs1, -1` to performs bitwise inversion instead of `NOT`

Shifts:
* `SLLI` and `SRLI` is both logical shift.
* `SRAI` is an arithmetic shift. The sign bit wouldn't be shifted.
* *We dont have `SLAR` because the maximum bits we can shfift is 31 bits. And Even if we shift 31 bits, still won't shift the sign bit. That's why we do't need `SLAR` to preserve the sign bit*

![](https://i.imgur.com/1KhqhSf.png)

Jump:
* `JALR` is jump and link register.
* Offset is 12 bits signed I-immediate value, not encoded in multiple of 2 bites like `JAL`.
* Target addrs is obtained by add offset to *sr1*
* The addr of instruction following the jump store to register *rd*
* *x0* also can be used in *rd* here if no other usage.

Combine `JALR` and `LUI` can jump anywhere in 32-bit absolute addr range.
`LUI` load top 20 bits to register.
`JARL` add in lower bits

See [[RISC-V#J-type instrcutions]] for `JAL` information.
### U-type 

![](https://i.imgur.com/5ZqpAc6.png)

* `LUI` , Load upper immediate:
	 * load top 20 bits of 32-bit to destination (U-immediate value)  *rd*
	 * fill leaving 12 bits with zeros
	* Combine with `ADDI` can compose a 32bit immediate value.

* `AUIPC` , add upper immediate to *pc* :
	* adds offset to *pc* and place result to destination *rd*
	* offset is U-immediate value (load top 20 bits, fill leaving with zero)

### R-type 
![](https://i.imgur.com/kYSDMyg.png)

*rs1* & *rs2* registers as source operands
write result in to register *rd*
*funct7* & *funct3* select the type of operation

Arthmetic:
* `ADD` & `SUB` perform addition and substraction
* Overflow are ignored.

Logic:
* `AND` `OR` `XOR` perform bitwise logical operations

Compares:
* `SLT` & `SLTU` is signed and unsigned compares
* Set *rd* to 1 if *rs1* < *rs2*
* Set 0 otherwise

Shift:
* `SLL` `SRL` is logical left and right shift
* `SRA` is arithmetic right shift.
* Shift value in *rs1* by the **lower 5** bits of register *rs2*.

`NOP`: basically does nothing. Only increase the *pc*
Equal to `ADDI x0, x0, 0`.
By the way, *x0* is write-only.

### J-type 
![](https://i.imgur.com/Xb5Uz7n.png)

`JAL` is jump and link
* J-immediate are a **signed** offset encoded in multiple of 2.
	(J-Imme乘二之後才是正確的相對位址)
* Jumps can target a $\pm1$ MiB range.
* Store the addr of the instruction follwing `JAL` into register *rd*

Standard software calling convention:
* *x1* as return addr register.
* *x5* as an alternate link register.
* Alternate link register is used to perform calling milicode routine like epilogue and prologue


**Misaligned instruction fetch exception** would be generate if addr is not aligned to a four-byte boundary.

### B-type
![](https://i.imgur.com/2Oba8QS.png)

For all branch instructions:
* 12-bit B-immediate encodes signed offset in multiples of 2.
* Target addrs is offset add to current *pc*.
* Branch can target a $\pm4$ KiB range.

Equal & Negative:
* `BEQ` `BNE` take the branch if register *rs1* *rs2* are equal or unequal respectively.

Great & Less:
* `BLT` `BLTU` take the branch if register *rs1* < *rs2*
* `BGE` `BGEU` take the branch if register *rs1* < *rs2*
* "U" is for unsigned comparison

Greater/Less and Equal : 
* **Not support** `BLE` & `BLEU`
* Both can be synthesized by instructions above

Branch design:
RISC-V : Include arithmetic comparison operations between two registers.
x86, ARM : used condition codes
MIPS : Compare one register against zero , compare two registers  inequality 

---
## Memory Instructions
### Load and Store Instructions
RV32I : load-store architecture
provide 32-bit user addr space and **byte-addressed **and **little-endian**

> bi-endianness: MIPS
> can switch to big-endian and little-endian

![](https://i.imgur.com/VMLTOml.png)

* load and store transfer a value between the registers and memory
* 12-bit sign-extended offset is adding to register *rs1* 

Load:
* **I-type**
* Copy a value from memory to register *rd*
* `LW` load a 32-bit value.
* `LH` load a 16-bit value and sign-extends to 32-bit.
* `LHU` loads a 16-bit value but zero extends to 32-bit. 
* `LB` & `LBU` loads a 8-bit value with sign-extends and zero extends respectively.

Store:
* **S-type**
* Copy the value in register *rs2* to memory.
* `SW` store 32-bit value
* `SH` store 16-bit value from the low bits
* `SB` store 8-bit value from the low bits

Note:
Misaligned accesses is supported in base ISA, but might run extremely slowly.


### Memory Model
![](https://i.imgur.com/N1YxHYT.png)

RISC-V ISA supports multiple concurrent threads within single addr space.
Each RISC-V hardware thread *hart*, has it's user register state .

the `FENCE` instruction is used to order device I/O and memory accesses as viewed by other RISC-V harts and external devices or coprocessors.

>Informally, no other RISC-V hart or external device can observe any operation
in the successor set following a FENCE before any operation in the predecessor set preceding the


## Contorl and Status Register
### CSR instructions
SYSTEM instructions
* access system functionality that need privilege.
* Using I-type format.

![](https://i.imgur.com/TseXCWa.png)

`CSRRW` (Atomic read/write CSR)
* atomically swaps values in CSRs and integer registers.
* Reads the value of CSR, zero-extends to XLEN bits, writing it to integer register *rd*.
* Initial value in *rs1* is written to CSR.


`CSRRS`(Atomic Read and Set Bits in CSR)
* reads the value of CSR, zero-extends to XLEN bits, writing it to integer register *rd*.
* Initial value in *rs1* is a bit mask specifies bit positions to be **set** in CSR.
* Any bit that is High  in *rs1* would make corresponding bit to be set in CSR, other bits are unaffected.

`CSRRC`(Atomic Read and Clear Bits in CSR)
* reads the value of CSR, zero-extends to XLEN bits, writing it to integer register *rd*.
* Initial value in *rs1* is a bit mask specifies bit positions to be **clear** in CSR.
* Any bit that is High  in *rs1* would make corresponding bit to be clear in CSR, other bits are unaffected.

`CSRRWI` `CSRRSI` `CSRRCI` 
* Immediate version to other CSR instructions.
* zero-extending 5-bit unsigned immediate 

> if *rd*=*x0* instruction would not read CSR and stop.
> if *rs1=x0*, would not cause any side effects even to read-only CSRs.
> if immediate field in `CSRRSI` `CSRRCI` is zero, would not cause any side effects as *rs1=x0*

### Timer and Counters
![](https://i.ibb.co/sK71QZq/Screenshot-32.png)


`RDCYCLE` pseudo-instruction:
* reads the low XLEN bits of *cycle* CSR
* *cycle* CSR : a count of the number of clock cycles executed by the processor core
* `RDCYCLEH` reads bits 63-32 of same cycle counter.

`RDTIME` pseudo-instruction:
* reads the low XLEN bits of *time* CSR
* *time* CSR : counts clock real time (from arbitrary start time)
* `RDCYCLEH` reads bits 63-32 of same time counter.

`RDINSTRET` pseudo-instruction:
* reads the low XLEN bits of *instret* CSR
* *instret* CSR : count the number of instructions retired by this hart(from arbitrary start time).

### Environment call and break point
![](https://i.imgur.com/LxCGv9W.png)

`ECALL` is make a system call.
`EBREAK` is used by debuggers to create a break point.

# Compare to MIPS
Instruction Set Architecture of MIPS and RISC-V are both RISC, and x86 and ARM are CISC.


## General
### Open source
RISC-V is open source and MIPS isn't.



### Architecutre
Length of Instruction in RISV-V are variable and has multiple instruction length version to deal with instruction unaligned problem.

Instruction length in MIPS is fixed.


For resource-constrained embedded applications, RICS-V have RV32E subset to RV32, which only has 16 registers.

MIPS is always 32 registers.

### Register names
![](https://www.researchgate.net/profile/David-Fang-3/publication/34498148/figure/tbl7/AS:669422343684132@1536614132657/1-MIPS-register-conventions.png)
**Figure. MIPS register convention**

![](https://d3i71xaburhd42.cloudfront.net/097d9b196e215e2b65fabf8c94271d4075571c55/96-Table18.2-1.png)
**Figure. RISC-V register convention**

In user convention, RISC-V has more saved register & function arguments. And MIPS has more temporaries.

### Arithmetic Overflow 
MIPS produce overflow exception for signed addition instruciton.
RISC-V would not check overflow and user should check it manually.

---
## Format
### Function code 
MIPS only has function code in **R-format**
RISC-V has function code in most formats(except for U-type and J-type)

In R-foramt:
RISC-V has two stage of function code and provide 10 bits in total.
MIPS has one function code.

### Immediate
MIPS only has immediate value in **I-format**
RISC-V has immediate value in most formats (except for R-type)

In MIPS J-format, we have 26 bit addr value

### Register to Register format
MIPS has shift amount in R-format
RISC-V hasn't.


---
## Memory

### Endian
RISC-V is little-endian

MIPS in early is big-endian
Recent MIPS is bi-endianness.

### Memory access
MIPS only allow pc-relative access.

RISC-V have both pc-relative access and absolute address access.
Abosulut access can be achived by combining `LUI` and `JALR` to access any address in 32-bit range.

### Jump
In `JAL`, MIPS always save return addr to *ra*.
However, RISC-V allows user to assign register to store save return addr, which make calling milicode routine possible(like epilogue & prologue).

### Alignment
RISC-V allows unaligned memory access.
Memory access in MIPS is always had to be aligned.

---
### Pros & Cons
MIPS
* Pros:
	1. Convention : jump instructions wouldn't need to assign register to place return address.
	2. Newbie friendly : MIPS would check overflow by itself and we don't need to check it by ourself.
* Cons:

RISC-V
* Pros:
	1. Flexibility : We can decide whether to use overflow check or not and have capibility to construct milicode routine.
* Cons:


---
# Reference
https://riscv.org/wp-content/uploads/2017/05/riscv-spec-v2.2.pdf
https://www.csie.ntu.edu.tw/~cyy/courses/assembly/07fall/assignments/final/reports/arm_mips.pdf
https://www.tutortecho.com/post/ic-design-%E4%BD%95%E8%AC%82control-status-register-csr
https://max.cs.kzoo.edu/cs230/Resources/MIPS/MachineXL/InstructionFormats.html
https://www.zhihu.com/question/325968121