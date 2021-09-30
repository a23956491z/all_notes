---
tags : operating-system
---

when applications request OS services : **System calls**

request to **kernel**  via **software interrupt**

Request some OS service:
* Process control
* File management
* Device Management
* Information maintenace
* Commuinications

when system call occurs, **copy contents** of one file to another file

## Implementation
**a number** with every system call
* System-call interface record the meaning of numbers

### Parameter passing

pass parameters to OS:
* Simplest : pass parameters in **register**
* Store in **block** or memory : **address of block** in register
* Stack : pushed by program, poped by OS