# Homeworks
![](https://i.imgur.com/NJl9oQ1.png)

## 1.8
What the purpose of interrupt?
%3E Protection.
> e.g.
> * Protecting CPU from infinite loop so we arise interruption by timer.
> * Protecting process from modify each other
> * Separate the process & kernel by system call interruption

How does an interrupt differ from trap?
> There are 2 types of interrupt, hardware interrupt & software interrupt. And software interrupt is also called **trap**.
>
> But interrupt sometimes also mentioned to hardware interrupt.


Can traps be generated intentionally by as user program? If so, for what purpose?
> Yes, requesting for operating system service like system call

## 1.10
It's not possible:
* The kernel instructions and user insructions might get mixed, casuing user programs are allowed to modify other programs resulting unstable operating system for a multi-user scene or open server.

It's possible:
* If we are the only one using the system, we can make sure our programs do not effect the kernel's and other processes is running
* We may need to do the hardware isolation by ourselves or taking care about using hardware devices. Because every program we wroten are allowed to use the whole system resource, by mistake, we might detroty our running environment.
## Why dual mode operation can protect system?
> Dual-mode allowed as sharing resources without effect each other.
>
> By switch between user mode & monitor mode, user program are not allowed to have privileged instruction>)