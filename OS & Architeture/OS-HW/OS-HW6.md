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
	* 
* bounded-wait
	* after the end of critical section, we would change the turn and pass the access to other process.


## Problem 6.3
![](https://i.imgur.com/MApH1fM.png)

## Problem 6.4
![](https://i.imgur.com/XzDYL80.png)

if we directly disable the interrupt in single-processor system, it might results **infinite loop** when waiting another job.
So the **interrupt** is necessary to jump to other process when another process get in the critical section.

## Problem 6.5
![](https://i.imgur.com/yp9RSCx.png)

when we in critaical section,
if we use interrupt it might unintentionally change the registers we are using by another processes.

## Problem 6.8
![](https://i.imgur.com/tITafU5.png)

 `compare_and_swap()`
because it is atomic
so when we execute this function, it would be finished immediately.
## Problem 6.9
![](https://i.imgur.com/LJAitG4.png)

## Problem 6.14
![](https://i.imgur.com/ipcgl2p.png)
