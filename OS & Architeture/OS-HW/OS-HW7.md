## Problem 7.7
![](https://i.imgur.com/7x3Z9FG.png)

requirements of deadlock
* mutual exclusion
* hold & wait
* no preemption
* circular wait

Because every type of resources are the same.
So it won't wait for the particular resource, resulting would not cause circular wait.

## Problem 7.8
![](https://i.imgur.com/QXRMywd.png)

## Problem 7.9
![](https://i.imgur.com/qO8JL4i.png)

## Problem 7.12
![](https://i.imgur.com/mXCTIX2.png)
![](https://i.imgur.com/TW6AfC4.png)

### a. Available = (0,3,0,1)
1. `Available = (0,3,0,1)`
	* 先從resource A開始確認
		* 需要滿足條件：$Available_A + Allocation_A >= Max_A$
		* $P_0$ ~ $P_4$ 都是候選人
		* 只有 $P_2$ 符合條件
	* 確認resource B,C,D
		* $P_2$ 都符合條件，執行並歸還資源
		*  Available = (0,3,0,1) + (3,3,2,1)
2. `Available = (3,6,2,2)`
	* $P_1$符合條件，執行並歸還資源
	* Available = (3,6,2,2) + (3,2,1,1)
3. `Available = (6,8,3,3)`
	*  $P_3$符合條件，執行並歸還資源
	*  Available = (6,8,3,3) + (4,6,1,2)
4. `Available = (10,14,4,5)`
	* $P_0$符合條件，執行並歸還資源
	*  Available = (10,14,4,5) + (5,1,1,7)
* `Available = (15,15,5,11)`
	*  $P_4$符合條件，執行並歸還資源
	* Available = (15,15,5,11) + (6,3,2,5)

總共資源：(21,18,7,16)
順序 $P_2 \rightarrow P_1 \rightarrow P_3 \rightarrow P_0 \rightarrow P_4$

### b. Avaliable = (1,0,0,2)
1. `Avaliable = (1,0,0,2)`
	* 先確認resource A
		* 需要滿足條件：$Available_A + Allocation_A >= Max_A$
		* 只有$P_1$符合條件
	* 確認resource B,C,D
		* $P_1$符合條件，執行並歸還資源
		* Available =  (1,0,0,2) + (3,2,1,1)
2. `Avaliable = (4,2,1,3)`
	* $P_2$符合條件，執行並歸還資源
	*  Available =  (4,2,1,3) + （3,3,2,1)
3. `Avaliable = (7,5,3,4)`
	* $P_0$符合條件，執行並歸還資源
	*  Available =  (7,5,3,4) + (5,1,1,7)
4. `Avaliable = (12,6,4,11)`
	* $P_3$符合條件，執行並歸還資源
	*  Available = (12,6,4,11) + (0,5,1,0)
5. `Avaliable = (12,11,5,11)`
	* $P_4$符合條件，執行並歸還資源
	*  Available = (12,11,5,11) + (6,3,2,5)

總共資源：(18,14,7,16)
順序 $P_2 \rightarrow P_1 \rightarrow P_3 \rightarrow P_0 \rightarrow P_4$


## Problem 7.13
![](https://i.imgur.com/EeUlJUA.png)
