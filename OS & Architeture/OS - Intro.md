
## Distributed system
### Client-Server
* Server is **bottleneck** & **single failure point**
![](https://i.imgur.com/Uo9f5uS.png)


### Peer-to-Peer 
* Ex: ppStream, bitTorrent, *Internet*
![](https://i.imgur.com/TORnqEq.png)

## Embedded Systems
* Limited memory & Slow processor
* **Battery** consumption
* Hardware specialized OS


# Hardware Protection
## Dual-mode operation
Sharing system resources:
* Programs can't effect each other

Hardware support for 2 mode of operations:
* **User mode** 
* **Monitor mode** (Kernel mode) : done by operating system

Mode BIT:
* kernel is 0
* user is 1

### Monitor mode
![](https://i.imgur.com/2IuU2lX.png)

* Switch to monitor mode when **interrupt/trap** occurs
* Monitor mode have **Privileged instructions**, also can request by users(**System calls**)
	* System call changes mode to kernel, and reset the mode after return 


## I/O Protection
I/O instructions are **privileged instructions**

make sure user program cannot gain control in monitor mode

## Memory Protection

Protect
* Interrupt vector
* Interrupt service routine
* Data access
* over-write from other programs

![](https://i.imgur.com/9CjCrDe.png)

Hardware support : 2 registers
* **Base register** : smallest physical memory address
* **Limit register** : range or size


Addressing Error : is *trap* to operating system monitor

## CPU Protection
Prevent user program cause **infinite loop**

Hardware support : **Timer**
* interrupt program after a time period
* Use Clock Tick (physical clock)
* timer reaches 0, interrupt the program

* **Load-timer** is provileged instruction
* **Time Sharing** is implement by *Timer*

# OS Structure
## Multiprogramming (Batch system)
* Organize jobs & **Job Scheduling**
* Subset of total jobs are in *memory*
* **switch to another job** when *have to wait*  (e.g. I/O operation)

## Timesharing (multitasking)
* CPU switch jobs frequently like they are running in the same time
	* Response time should be < 1s
	* **Swap** : if process cannot fit in memory
	* **Virtual memory** : Execute process from Disk + Memory (*Simulate disk to memory*)
	* **CPU scheduling** : If jobs are going to run in the same time

![](https://i.imgur.com/hW5pizi.png)

# OS operation
## Interrupt driven
* Hardware interrupt by devices
* Software interrupt (**Exception**/**Trap**)
	* **Software logical error** : e.g. divided by zero
	* **Process problem** : e.g. infinite loop, process modifying each other
	* Request for operating system service : **System call**
![](https://i.imgur.com/o3uIQMV.png)

## Dual-mode
* User mode & Kernel mode
* **Mode bit** provided by hardware

## Virtual Machine Manager (VMM)
for guest VMs

## Process
Process is a running program
* Program is **passive entity**
* Process is **active entity**

Process termiation:
* Reclaim resources

Program Counter:
* Specifying location of next instruction to execute (Sqeuentially)
* Single-threaded process has one program counter
* Multi-threaded one program counter *per thread*

Operating system's responsibility
* Create/Delete user & system processes
* Suspend/Resume process
* Synchronize process
* Commicate process
* Deadlock handle

## Memory
* Execute a program : instructions must be in memory
* data needed by program also need to be in memory

**Memory management** : *what in memory & when*
* keeping tracking where is being used & by who is using
* Which process and data need to move in / move out memory
* Allocating & De-allocating

## Stroage
* Physical proterty -> logical storage unit : file

Disk:
* Free-space management
* Sotrage allocation
* Disk scheduling

Tertiary storage : e.g. optical storage(CD), magnetic tape
* some are WORM(write-once, read-many-times), RW(read-write)



**File-System** management:
* Control who can access what
* Create/Delete files & directories
* Mapping files onto another storage
* ??*Primitives to Manipulate files & directories*??

## I/O
Res


# Kernel Data Structure
List:
* Linked List
* Doubly Linked List
* Circular Linked List

Tree:
* Binary Search Tree : Search $O(n)$
* Balanced binary search Tree : Search $O(\lg n)$

Hash map
* with Hash function

**Bitmap**
* string of *n* binary digits : *n* status

## Linux data structure
* defined in 
	* `<linux/list.h>`
	* `<linux/kfifo.h>`
	* `<linux/rbtree.h>`

# Homeworks
![](https://i.imgur.com/NJl9oQ1.png)
