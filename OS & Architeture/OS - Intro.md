
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
* Use Clock Tick
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
# OS operation