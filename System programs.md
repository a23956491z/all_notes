---
tags : operating-system
---

System programs provide system  service wrapped as progrmas.

* Manage Files
	* create
	* delete ...
* Modify Files
* get Status
	* date,  time
	* avaliable memoery, disk usage
    * or implement **registry** : store system informations
* Programming-lang. support
	* Compiler, assemblers
* Program loading & execution
	* using loaders
* Communications
	* Creating virtual connection among process/user

#### Background service
aka services, **daemon**

* Launch at boot
* *Run in user context instead of kernel*
* e.g. loggin or disk checking