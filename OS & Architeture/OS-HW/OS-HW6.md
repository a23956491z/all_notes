---
title: Operating System HW5
---

## Problem 6.1
![](https://i.imgur.com/IJRosRQ.png)

## Problem 6.2
![](https://i.imgur.com/ZWwze8T.png)

requirements:
* Mutual exclusion
	* when the flag is on & the it turn to the process, others can not enter the cirtical section
	* `flag[i]==1` and another flag would be `flag[j]==0`
* progress                                                                                                                                                                                      
* 
* bounded-wait


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
