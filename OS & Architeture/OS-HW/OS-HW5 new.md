---
title: Operating System HW5
---

## Problem 6.1
![](https://i.imgur.com/IJRosRQ.png)

2 functions:
* `deposit(amount)`
* `withdraw(amount)`

if they deplsit & withdraw at nearly the same time
* both function load the same balance to register
* but store `balance + deposit` or `balance - withdraw` to database depending on which one is first request instead of  `balance + deposit - withdraw`

we can put the load balance & change balance to critical secion using Peterson algorithm to deal with this problem.
## Problem 6.2
![](https://i.imgur.com/ZWwze8T.png)

requirements:
* Mutual exclusion
	* when the `turn` variable is not equal to the process id, it won't enter the critical section
	* only one process's id would equal to the `turn` variable
* progress
	* we put down our flag if other process have entering the critical section and after they finished we put the flag back.
	* we continuously check the flag so anyone return the access back and we can use it right away.
* bounded-wait
	* after the end of critical section, we would change the turn and pass the access to other process.


## Problem 6.3
![](https://i.imgur.com/MApH1fM.png)
requirements:
* Mutual exclusion
	* when the `turn` variable is not equal to the process id, it won't enter the critical section
	* only one process's id would equal to the `turn` variable
* progress
	* it would check every process is in critical section or not, if there is a process in crtical section -> keep set `j = turn` & waiting
	* because we keep spinning in while loop, if any process return the access we can enter the critical section right away.
* bounded-wait
	* after the end of critical section, we would change the turn and pass the access to other process.


## Problem 6.4
![](https://i.imgur.com/XzDYL80.png)

if we disabling interrupt
* programs(user-level) cannot use **system call** any more, so they can't using some priviliged function or using the I/O resources.
* kernel-level programs doesn't have these kind of problem, they dont need to use interrupt to switch mode however user-level programs need to switch the mode from user to kernel by interrupt

## Problem 6.5
![](https://i.imgur.com/yp9RSCx.png)

if we interrupt all processes in the other processors to enter the critical section , which is directly waste the resource of other processors.  

## Problem 6.8
![](https://i.imgur.com/tITafU5.png)

 `compare_and_swap()`
because it is atomic, when we execute this function, it would be finished immediately.

There is no race condition in this function because we load value & change value immediately would not happen the situation that 2 process use this function at the same time & causing race condition.

after we finished critical seciton, we just need to change the value back to provide bounded-waiting.
## Problem 6.9
![](https://i.imgur.com/LJAitG4.png)

## Problem 6.14
![](https://i.imgur.com/ipcgl2p.png)

### a. race condition
* if they compare the value & both get into the `else` section & the `number_of_processes` is 254 currently.
	* it would cause `number_of_processes` greater than `MAX_PROCESSES` because they both pass the if condition & both make `number_of_processes` plus one.
* if they execute the `allocate_process` at the same time
	* they may compete to allocate the same pid.

### b. where to put acquire() & release()

* put `acquire`() before `if-else` clause
* put  `release()` before return

### c. atomic is work or not
even if we can change the pid in atomic
* it only solve the same pid compete 
