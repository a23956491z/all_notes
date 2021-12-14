# Operating System Week5 HW
* 410821238
* 資工三
* 余慶龍

## 5.3
![](https://i.imgur.com/lK5YBt0.png)

how BTV can ensure higher-priority have more attention?
 give more tickets to higher-priority processes so they would get higher probability to get schedule in.
 
 
## 5.4 
![](https://i.imgur.com/88SMysu.png)

### a. each processor have ther own run queue
advantages: 
* faster
	* because don't need  access to a shared memory
* easier to implement
	* each processor maintain their own queue & doesnt need to bother the other jobs in the rest of processors.
disadvantages:
* Not efficient
	* some processors may in idle but other processor have heavier works.

### b. shared run queue
advantages: 
* all processor can equally get jobs in their queue by a global scheduler to make a dynamic load balancer.
disadvantages:
* They need shared memory to store the run queue
	* transmit data are slower
* More complex to design


## 5.6
![](https://i.imgur.com/dyKRNzf.png)

CPU-bound programs are better for regressive round-robin
* I/O-bound jobs would get interrupt by I/O request resulting get lower priority
* CPU-bound jobs can keep using CPU and continuously increase the time quantum & priority.


## 5.7
![](https://i.imgur.com/V3S7E11.png)
![](https://i.imgur.com/LiUThfI.png)


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

## 5.8
![](https://i.imgur.com/vS433Yw.png)

### a. gantt
[![](https://mermaid.ink/img/eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSByb3VuZC1yb2JpblxuICAgIGRhdGVGb3JtYXQgIERERFxuICAgIGF4aXNGb3JtYXQgICVqXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMSwgMTlkXG4gICAgc2VjdGlvbiBQMlxuICAgIFAyIDogMjUsIDEwZFxuICAgIFAyIDogNDUsIDEwZFxuICAgIFAyIDogNzAsIDVkXG4gICAgc2VjdGlvbiBQM1xuICAgIFAzIDogMzUsIDEwZFxuICAgIFAzIDogNTUsIDVkXG4gICAgUDMgOiA3NSwgMTBkXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogNjAsIDEwZFxuICAgIFA0IDogODUsIDVkXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogMTAwLCA1ZFxuICAgIFA1IDogMTE1LCA1ZFxuICAgIHNlY3Rpb24gUDZcbiAgICBQNiA6IDEwNSwgMTBkXG4gICAgc2VjdGlvbiBpZGxlXG4gICAgaWRsZSA6IDIwLCA1ZFxuICAgIGlkbGUgOiA5MCwgMTBkIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)](https://mermaid.live/edit/#eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSByb3VuZC1yb2JpblxuICAgIGRhdGVGb3JtYXQgIERERFxuICAgIGF4aXNGb3JtYXQgICVqXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMSwgMTlkXG4gICAgc2VjdGlvbiBQMlxuICAgIFAyIDogMjUsIDEwZFxuICAgIFAyIDogNDUsIDEwZFxuICAgIFAyIDogNzAsIDVkXG4gICAgc2VjdGlvbiBQM1xuICAgIFAzIDogMzUsIDEwZFxuICAgIFAzIDogNTUsIDVkXG4gICAgUDMgOiA3NSwgMTBkXG4gICAgc2VjdGlvbiBQNFxuICAgIFA0IDogNjAsIDEwZFxuICAgIFA0IDogODUsIDVkXG4gICAgc2VjdGlvbiBQNVxuICAgIFA1IDogMTAwLCA1ZFxuICAgIFA1IDogMTE1LCA1ZFxuICAgIHNlY3Rpb24gUDZcbiAgICBQNiA6IDEwNSwgMTBkXG4gICAgc2VjdGlvbiBpZGxlXG4gICAgaWRsZSA6IDIwLCA1ZFxuICAgIGlkbGUgOiA5MCwgMTBkIiwibWVybWFpZCI6IntcbiAgXCJ0aGVtZVwiOiBcImRlZmF1bHRcIlxufSIsInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)

### b&c turnaround time & waiting time
|       | turnaround time | waiting time |
|:-----:|:---------------:|:------------:|
| $P_1$ |       20        |      0       |
| $P_2$ |       50        |      25      |
| $P_3$ |       50        |      25      |
| $P_4$ |       30        |      15      |
| $P_5$ |       20        |      10      |
| $P_6$ |       10        |      0       |

### d. CPU util rate
$\cfrac{120-15}{120}*100\%=87.5\%$

---

## 5.10
![](https://i.imgur.com/H0JJOxi.png)
![](https://i.imgur.com/vonLmUH.png)


ANS:
* **SJF**
	* system keep execute the short jobs and Long jobs may not be execute
* **Priority**
	* low priority jobs may not get scheduled in by always have a higher priority jobs.

---

## 5.22
![](https://i.imgur.com/AOjMXxC.png)

### a. rate-monotonic

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSByb3VuZC1yb2JpblxuICAgIGRhdGVGb3JtYXQgIERERFxuICAgIGF4aXNGb3JtYXQgICVqXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMSwgMjRkXG4gICAgUDEgOiA1MCwgMjVkXG4gICAgUDEgOiAxMDAsIDI1ZFxuICAgIHNlY3Rpb24gUDJcbiAgICBQMiA6IDI1LCAyNWRcbiAgICBQMiA6IDc1LCA1ZFxuICAgIFAyIDogODAsIDIwZFxuICAgIFAyIDogMTI1LCAxMGRcblxuIiwibWVybWFpZCI6eyJ0aGVtZSI6ImRlZmF1bHQifSwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)](https://mermaid.live/edit/#eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSByb3VuZC1yb2JpblxuICAgIGRhdGVGb3JtYXQgIERERFxuICAgIGF4aXNGb3JtYXQgICVqXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMSwgMjRkXG4gICAgUDEgOiA1MCwgMjVkXG4gICAgUDEgOiAxMDAsIDI1ZFxuICAgIHNlY3Rpb24gUDJcbiAgICBQMiA6IDI1LCAyNWRcbiAgICBQMiA6IDc1LCA1ZFxuICAgIFAyIDogODAsIDIwZFxuICAgIFAyIDogMTI1LCAxMGRcblxuIiwibWVybWFpZCI6IntcbiAgXCJ0aGVtZVwiOiBcImRlZmF1bHRcIlxufSIsInVwZGF0ZUVkaXRvciI6ZmFsc2UsImF1dG9TeW5jIjp0cnVlLCJ1cGRhdGVEaWFncmFtIjpmYWxzZX0)

### b. EDF

[![](https://mermaid.ink/img/eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSByb3VuZC1yb2JpblxuICAgIGRhdGVGb3JtYXQgIERERFxuICAgIGF4aXNGb3JtYXQgICVqXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMSwgMjRkXG4gICAgUDEgOiA1NSwgMjVkXG4gICAgUDEgOiAxMDAsIDI1ZFxuICAgIFAxIDogMTUwLCAyNWRcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAyNSwgMzBkXG4gICAgUDIgOiA4MCwgMjBkXG4gICAgUDIgOiAxMjUsIDEwZFxuICAgIFAxIDogMTc1LCAzMGRcblxuXG4iLCJtZXJtYWlkIjp7InRoZW1lIjoiZGVmYXVsdCJ9LCJ1cGRhdGVFZGl0b3IiOmZhbHNlLCJhdXRvU3luYyI6dHJ1ZSwidXBkYXRlRGlhZ3JhbSI6ZmFsc2V9)](https://mermaid.live/edit/#eyJjb2RlIjoiZ2FudHRcbiAgICB0aXRsZSByb3VuZC1yb2JpblxuICAgIGRhdGVGb3JtYXQgIERERFxuICAgIGF4aXNGb3JtYXQgICVqXG4gICAgc2VjdGlvbiBQMVxuICAgIFAxIDogMSwgMjRkXG4gICAgUDEgOiA1NSwgMjVkXG4gICAgUDEgOiAxMDAsIDI1ZFxuICAgIFAxIDogMTUwLCAyNWRcbiAgICBzZWN0aW9uIFAyXG4gICAgUDIgOiAyNSwgMzBkXG4gICAgUDIgOiA4MCwgMjBkXG4gICAgUDIgOiAxMjUsIDEwZFxuICAgIFAxIDogMTc1LCAzMGRcblxuXG4iLCJtZXJtYWlkIjoie1xuICBcInRoZW1lXCI6IFwiZGVmYXVsdFwiXG59IiwidXBkYXRlRWRpdG9yIjpmYWxzZSwiYXV0b1N5bmMiOnRydWUsInVwZGF0ZURpYWdyYW0iOmZhbHNlfQ)