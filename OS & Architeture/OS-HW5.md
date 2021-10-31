---
title: Operating System HW5
---

## Problem 5.3
![](https://i.imgur.com/lrZijof.png)
![](https://i.imgur.com/qZ0iyEK.png)

### a. FCFS
$P_1$ takes 8 units
$P_2$ takes (8-0.4)+4 = 11.6 units
$P_3$ takes (8+4-1)+1 = 12 units

average turnaround time = (8+11.6+12)/3= *10.53 units*
### b. SJF
$P_1$ takes 8 units
$P_3$ takes (8-1)+1 = 8 units
$P_2$ takes (8+1-0.4)+4 = 12.6 units

average turnaround time = (8+8+12.6)/3= *9.53 units*
### c. SJF & idle for first unit
$P_3$ takes 1 units
$P_2$ takes (1+1-0.4)+4 = 5.6 units
$P_1$ takes (1+1+4)+8 = 14 units

---

average turnaround time = (1+5.6+14)/3= *6.86 units*
## Problem 5.4
![](https://i.imgur.com/juLx2LS.png)

### a. Gantt charts
Following algorithm:
* FCFS
* SJF
* non-preemptive priority
* RR

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBGQ0ZTXG4gICAgZGF0ZUZvcm1hdCAgc1xuICAgIGF4aXNGb3JtYXQgICVTXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMCwgMnNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAyLCAxc1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDMsIDhzXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogMTEsIDRzXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogMTUsIDVzIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)](https://mermaid.live/edit#eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBGQ0ZTXG4gICAgZGF0ZUZvcm1hdCAgc1xuICAgIGF4aXNGb3JtYXQgICVTXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMCwgMnNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAyLCAxc1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDMsIDhzXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogMTEsIDRzXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogMTUsIDVzIiwibWVybWFpZCI6IntcbiAgXCJ0aGVtZVwiOiBcImRlZmF1bHRcIlxufSIsInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)


[![](https://mermaid.ink/img/eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBTSkZcbiAgICBkYXRlRm9ybWF0ICBzXG4gICAgYXhpc0Zvcm1hdCAgJVNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAwLCAxc1xuICAgIHNlY3Rpb24gUDFcbiAgICBQMSA6IDEsIDJzXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogMywgNHNcbiAgICBzZWN0aW9uIFA1XG4gICAgUDUgOiA3LCA1c1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDEyLCA4c1xuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)](https://mermaid.live/edit#eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBTSkZcbiAgICBkYXRlRm9ybWF0ICBzXG4gICAgYXhpc0Zvcm1hdCAgJVNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAwLCAxc1xuICAgIHNlY3Rpb24gUDFcbiAgICBQMSA6IDEsIDJzXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogMywgNHNcbiAgICBzZWN0aW9uIFA1XG4gICAgUDUgOiA3LCA1c1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDEyLCA4c1xuIiwibWVybWFpZCI6IntcbiAgXCJ0aGVtZVwiOiBcImRlZmF1bHRcIlxufSIsInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBub24tcHJlZW1wdGl2ZSBwcmlvcml0eVxuICAgIGRhdGVGb3JtYXQgIHNcbiAgICBheGlzRm9ybWF0ICAlU1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDAsIDhzXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogOCwgNXNcbiAgICBzZWN0aW9uIFAxXG4gICAgUDEgOiAxMywgMnNcbiAgICBzZWN0aW9uIFA0XG4gICAgUDQgOiAxNSwgNHNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAxOSwgMXMiLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)](https://mermaid.live/edit#eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBub24tcHJlZW1wdGl2ZSBwcmlvcml0eVxuICAgIGRhdGVGb3JtYXQgIHNcbiAgICBheGlzRm9ybWF0ICAlU1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDAsIDhzXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogOCwgNXNcbiAgICBzZWN0aW9uIFAxXG4gICAgUDEgOiAxMywgMnNcbiAgICBzZWN0aW9uIFA0XG4gICAgUDQgOiAxNSwgNHNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAxOSwgMXMiLCJtZXJtYWlkIjoie1xuICBcInRoZW1lXCI6IFwiZGVmYXVsdFwiXG59IiwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBSUihxdWFudHVtPTIpXG4gICAgZGF0ZUZvcm1hdCAgc1xuICAgIGF4aXNGb3JtYXQgICVTXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMCwgMnNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAyLCAxc1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDMsIDJzXG4gICAgUDMgOiA5LCAyc1xuICAgIFAzIDogMTUsMnNcbiAgICBQMyA6IDE4LDJzXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogNSwgMnNcbiAgICBQNCA6IDExLDJzXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogNywgMnNcbiAgICBQNSA6IDEzLDJzXG4gICAgUDUgOiAxNywxcyIsIm1lcm1haWQiOnsidGhlbWUiOiJkZWZhdWx0In0sInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)](https://mermaid.live/edit#eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSBSUihxdWFudHVtPTIpXG4gICAgZGF0ZUZvcm1hdCAgc1xuICAgIGF4aXNGb3JtYXQgICVTXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMCwgMnNcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAyLCAxc1xuICAgIHNlY3Rpb24gUDNcbiAgICBQMyA6IDMsIDJzXG4gICAgUDMgOiA5LCAyc1xuICAgIFAzIDogMTUsMnNcbiAgICBQMyA6IDE4LDJzXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogNSwgMnNcbiAgICBQNCA6IDExLDJzXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogNywgMnNcbiAgICBQNSA6IDEzLDJzXG4gICAgUDUgOiAxNywxcyIsIm1lcm1haWQiOiJ7XG4gIFwidGhlbWVcIjogXCJkZWZhdWx0XCJcbn0iLCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)



### b. turnaround time
| unit(second) | FCFS | SJF | Non-Preemptive Priority |  RR  |
|:------------:|:----:|:---:|:-----------------------:|:----:|
|    $P_1$     |  2   |  3  |           15            |  2   |
|    $P_2$     |  3   |  1  |           20            |  3   |
|    $P_3$     |  11  | 20  |            8            |  20  |
|    $P_4$     |  15  |  7  |           19            |  13  |
|    $P_5$     |  20  | 12  |           13            |  18  |
|   Average    | 10.2 | 8.6 |           15            | 11.2 |
### c. waiting time
| unit(second) | FCFS | SJF | Non-Preemptive Priority | RR  |
|:------------:|:----:|:---:|:-----------------------:|:---:|
|    $P_1$     |  0   |  0  |           13            |  0  |
|    $P_2$     |  2   |  1  |           19            |  2  |
|    $P_3$     |  3   | 12  |            0            | 12  |
|    $P_4$     |  11  |  3  |           15            |  9  |
|    $P_5$     |  15  |  7  |            8            | 12  |
|   Average    | 6.2  | 4.6 |           11            |  7  |
### d. minimum average waiting time
in part c. we can see the *minimum average waiting time is 4.6* which is *SJF algorithm* in this case.

---

## Problem 5.6
![](https://i.imgur.com/gwhxmNc.png)
Move process between various queues with different time-quantum size can make a implementation of aging

1. can solve starvation problem
2. FCFS lower the average turnaround time 
3. Solve the propblem of fixed time-quatum size
    * large time-quatum : waste time for short burst time task
    * small time-quatum : too many interrupts
4. In short, it can make RR more efficient.

---
## Problem 5.7
![](https://i.imgur.com/XhgKlst.png)

### a. Priority & SJF
SJF is Priority Scheduling which the shortest job has the highest priority.
### b. Multilevel feedback queues & FCFS
FCFS is Multilevel queues when it only have 1 queue which is using FCFS.
### c. Priority & FCFS
FCFS is Priority Scheduling which all the priority of processes is the same.
### d. RR & SJF
they both have preemptive scheduling.

---

## Problem 5.8
![](https://i.imgur.com/Zt0AAgw.png)
This algorithm favor I/O-bound programs because they use less CPU resources(Process time).

In CPU-bound programs, the one never get schedule in would be execute first. So it won't starve these programs.

---

## Problem 5.10
![](https://i.imgur.com/vtjbGyA.png)

|       | CPU usage | Priority |
|:-----:|:---------:|:--------:|
| $P_1$ |    40     |    80    |
| $P_2$ |    18     |    69    |
| $P_3$ |    10     |    65    |

CPU-bound process use more CPU resources.
But if it use more CPU resources it would get lower priority(higher priorty number), resulting to *lower the relative priority of a CPU-bound process*.

## Problem 5.22
![](https://i.imgur.com/6d7545h.png)
tasks:
* 10 I/O-bound 
* 1  CPU-bound

### a. time quantum is 1 ms
* I/O operations totally task need 10 ms
* Get different I/O opertation every ms(Need CPU to compute)
    * for both I/O-bound job or CPU-bound job, takes 1 ms to do work (use CPU)
    * 0.1ms to do context-switch

$\cfrac{10}{1.1}=90.9\%$

CPU utilization is *90.9%*

### b. time quantum is 10 ms

* switch all I/O tasks 
    * 1.1 * 10
* CPU task and switch
    * 10.1

$\cfrac{20}{(1.1*10+10.1)}=94.78\%$

CPU utilization is *94.78%*
