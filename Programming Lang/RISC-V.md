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