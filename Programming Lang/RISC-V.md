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

## Memory Instructions