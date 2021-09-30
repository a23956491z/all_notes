---
tags : operating-system
---

Application Program Interface

* Programs mostly use **API** instead of system calls
* Implemented by language library e.g. *C library*
* API usually include system calls
	* e.g. : `malloc()` `free()` use system call `brk()`
	* but math API`abs()` doesn't use system call
	
![](https://i.imgur.com/7B6WfXr.png)

Interface vs Library
![](https://i.imgur.com/1ZOlt4P.png)

Windows : *Win32 API*
POSIX-based system : *POSIX API*
JVM : *Java API*