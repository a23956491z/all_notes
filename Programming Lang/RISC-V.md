Have 31 registers (x1-x31)
* x0: constant 0
* x1: return addr(standard software calling convention)

XLEN <- register bits wide
RV32 : registers are 32bits wide
RV64: 64bits wide

### Base Instruction Formats
4 base foramts with **32 bits** (aligned on four-byte)

![](https://i.imgur.com/N0yZdNU.png)

*rs1* *rs2* is source
*rd* is destination
*imm[x]* is immediated field with bit position

The **Sign bit** is alyways in *bit 31*

### Immediate Formats Variant
Which is the Foramt B-tpye and J-type

Diffierence between S/B type:
These are both 12-bit immediate field and B-type with one-bit left shift of immediate value.

* Every formats can present different bits and type immediate value.
* This figure shows how we put the bits of immediate value to instruction format (Label with instruction bit *inst[y]*)

![](https://i.imgur.com/M37pNaH.png)

### Integer Computation
1. I-type as register-immediate operation
2. R-type as rigster-register operation


* MIPS would throws overflow exception and RISC-V won't.
To deal with overflow problem, implementing by ourself.
e.g. We can check unsigned overflow like this
```
add 	t0, t1, t2;
bltu 	t0, t1, overflow; # branch less than unsigned
```

#### I-type instructions
![](https://i.imgur.com/TLRJBhu.png)

Arthmetic:
* Use `ADDI rd, rs1, 0` to implement `MV rd, rs1` 
* `SLTI` (set less than immediate )put 1 in register *rd* if *rs1* less than immeidate. And `SLITU` is for unsigned.

Logic operation:
* `ANDI` `ORI` `XORI` are logical operations
* Using `XORI rd, rs1, -1` to performs bitwise inversion instead of `NOT`

Shifts:
* `SLLI` and `SRLI` is both logical shift.
* `SRAI` is an arithmetic shift.