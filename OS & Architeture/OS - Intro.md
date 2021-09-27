
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


## I/O protection
I/O instructions are **privileged instructions**

make sure user program cannot gain control in monitor mode

## Memory protection

Protect
* Interrupt vector
* Interrupt service routine
* Data access
* over-write from other programs

