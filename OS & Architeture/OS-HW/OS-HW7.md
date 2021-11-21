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
		*  Available = (0,3,0,1) + (3,1,2,1)
2. `Available = (3,4,2,2)`
	* $P_1$符合條件，執行並歸還資源
	* Available = (3,4,2,2) + (2,2,1,0)
3. `Available = (5,6,3,2)`
	*  $P_3$符合條件，執行並歸還資源
	*  Available = (5,6,3,2) + (0,5,1,0)
4. `Available = (5,11,4,2)`
	* $P_4$符合條件，執行並歸還資源
	*  Available = (5,11,4,2) + (4,2,1,2)
5. `Available = (9,13,5,4)`
	* $P_0$符合條件，執行並歸還資源
	*  Available = (9,13,5,4) + (3,0,1,4)
總共資源：(12,13,6,8)
順序 $P_2 \rightarrow P_1 \rightarrow P_3 \rightarrow P_4 \rightarrow P_0$
state : safe

### b. Avaliable = (1,0,0,2)
1. `Avaliable = (1,0,0,2)`
	* 先確認resource A
		* 需要滿足條件：$Available_A + Allocation_A >= Max_A$
		* 只有$P_1$符合條件
	* 確認resource B,C,D
		* $P_1$符合條件，執行並歸還資源
		* Available =  (1,0,0,2) + (2,2,1,0)
2. `Avaliable = (3,2,1,2)`
	* $P_2$符合條件，執行並歸還資源
	*  Available =  (3,2,1,2) + (3,1,2,1)
3. `Avaliable = (6,3,3,3)`
	* $P_0$符合條件，執行並歸還資源
	*  Available =  (6,3,3,3) + ()
4. `Avaliable = (12,6,4,11)`
	* $P_3$符合條件，執行並歸還資源
	*  Available = (12,6,4,11) + (4,6,1,2)
5. `Avaliable = (16,12,5,13)`
	* $P_4$符合條件，執行並歸還資源
	*  Available = (16,12,5,13) + (6,3,2,5)

總共資源：(22,15,7,18)
順序 $P_1 \rightarrow P_2 \rightarrow P_0 \rightarrow P_3 \rightarrow P_4$
state : safe

## Problem 7.13
![](https://i.imgur.com/EeUlJUA.png)

|       | Available  | (3,3,2,1) |           |
| ----- | ---------- | --------- | --------- |
|       | Allocation | Max       | Need      |
| $P_0$ | (2,0,0,1)  | (4,2,1,2) | (2,2,1,1) |
| $P_1$ | (3,1,2,1)  | (5,2,5,2) | (2,1,3,1) |
| $P_2$ | (2,1,0,3)  | (2,3,1,6) | (0,2,1,3) |
| $P_3$ | (1,3,1,2)  | (1,4,2,4) | (0,1,1,2) |
| $P_4$ | (1,4,3,2)  | (3,6,6,5) | (2,2,3,3) |

### a. process completion order

1. $Available>Need_{P_0}$
	* 執行$P_0$並釋放資源
	* Available = (3,3,2,1) + (2,0,0,1) = (5,3,2,2)
1. $Available>Need_{P_3}$
	* 執行$P_3$並釋放資源
	* Available = (5,3,2,2) + (1,3,1,2) = (6,6,3,4)
3. 目前的 Available已大於所有Process的需求，剩下的Process依序執行下去

順序 $P_0 \rightarrow P_3 \rightarrow P_1 \rightarrow P_2 \rightarrow P_4$

### b. $P_1$ allocation = (1,1,0,0)

|       | Available  | (3,3,2,1) |           |
| ----- | ---------- | --------- | --------- |
|       | Allocation | Max       | Need      |
| $P_0$ | (2,0,0,1)  | (4,2,1,2) | (2,2,1,1) |
| $P_1$ | (1,1,0,0)  | (5,2,5,2) | (4,1,5,2) |
| $P_2$ | (2,1,0,3)  | (2,3,1,6) | (0,2,1,3) |
| $P_3$ | (1,3,1,2)  | (1,4,2,4) | (0,1,1,2) |
| $P_4$ | (1,4,3,2)  | (3,6,6,5) | (2,2,3,3) |

1. $Available>Need_{P_0}$
	* 執行$P_0$並釋放資源
	* Available = (3,3,2,1) + (2,0,0,1) = (5,3,2,2)
2. $Available>Need_{P_3}$
	* 執行$P_3$並釋放資源
	* Available = (5,3,2,2) + (1,3,1,2) = (6,6,3,4)
3. $Available>Need_{P_2}$
	* 執行$P_2$並釋放資源
	* Available = (6,6,3,4) + (2,1,0,3) = (8,7,3,7)
4. $Available>Need_{P_4}$
	* 執行$P_4$並釋放資源
	* Available = (8,7,3,7) + (1,4,3,2) = (9,11,6,9)
5. 目前的 Available已大於所有Process的需求，剩下的Process依序執行下去

順序 $P_0 \rightarrow P_3 \rightarrow P_2 \rightarrow P_4 \rightarrow P_1$
safe state，可以直接執行

### c. $P_4$ allocation = (0,0,2,0)

|       | Available  | (3,3,2,1) |           |
| ----- | ---------- | --------- | --------- |
|       | Allocation | Max       | Need      |
| $P_0$ | (2,0,0,1)  | (4,2,1,2) | (2,2,1,1) |
| $P_1$ | (3,1,2,1)  | (5,2,5,2) | (2,1,3,1) |
| $P_2$ | (2,1,0,3)  | (2,3,1,6) | (0,2,1,3) |
| $P_3$ | (1,3,1,2)  | (1,4,2,4) | (0,1,1,2) |
| $P_4$ | (0,0,2,0)  | (3,6,6,5) | (3,6,4,5) |

1. $Available>Need_{P_0}$
	* 執行$P_0$並釋放資源
	* Available = (3,3,2,1) + (2,0,0,1) = (5,3,2,2)
2. $Available>Need_{P_3}$
	* 執行$P_3$並釋放資源
	* Available = (5,3,2,2) + (1,3,1,2) = (6,6,3,4)
3. $Available>Need_{P_1}$
	* 執行$P_1$並釋放資源
	* Available =  (6,6,3,4) + (3,1,2,1) = (9,7,5,5)
3. $Available>Need_{P_2}$
	* 執行$P_2$並釋放資源
	* Available = (9,7,5,5) + (2,1,0,3) = (11,8,5,8)
4. 目前的Available = (11,8,5,8) 無法滿足$P_4$的需求

unsafe state，**無法直接執行**
