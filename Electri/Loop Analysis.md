#circuit_analysis 

Nodal analysis不是不能做，只是很複雜
所以有了利用 KVL 的 Loop Analysis

### Basic form
這種情況不僅需要super node，還需要三個KCL才能解

![](https://i.imgur.com/omTIAqo.jpg)

---
### Mesh v.s. Loop
Mesh是最小單位且無法再分割的Loop
> A mesh is a loop that does not enclose any other loop.

只有黃色與綠色是Mesh
而Loop有三個(黃綠紅)

![](https://i.imgur.com/prQd1Hm.png)


### Loop current
承上圖

> Loop current is a (fictcious) current that is assumed to flow around a loop

圖中的 $\large I_1, I_2, I_3$就是Loop current
**而流經每個元件的電流都可以用Loop current來表示**  

Ex:
我們使用三個Loop去分析 circuit current
$\large I_{af}=-I_1-I_3$
$\large I_{be}=I_1-I_2$
$\large I_{bc}=I_2+I_3$  

Ex2:

![](https://i.imgur.com/Yy5BO27.png)

$\large I_{af}=-I_1-I_3$
$\large I_{be}=I_1$
$\large I_{bc}=I_3$  

---
### Minimal Set to circuit current
計算最少需要多少Loop current才能得到該circuit current

![](https://i.imgur.com/wfJjAV3.png)

Ex:

![](https://i.imgur.com/QOEBvNW.png)

Ex2:

![](https://i.imgur.com/isnr589.jpg)

---
### With Indepentdent current source

![](https://i.imgur.com/N02zKzN.png)

Loop current $\large I_1$ 直接被電流源決定了，$\large I_1= 2mA$


![](https://i.imgur.com/3a5RhWD.png)

**要注意電流源與 Loop current的方向**，此時的$\large I_2= -2mA$
Ans : $V_0=-1.5V$


Practice:

![](https://i.imgur.com/cquW3N2.png)

Ans : $\large V_0=\frac{48}{7}V$ ????

---
### Super Mesh
當兩個mesh共享一個current source時，我們可以將那兩個mesh視作一個super mesh
> Define a supermesh by (mentally) removing  the shared current source

分析circuit current時一樣依照原本的Loop current

![](https://i.imgur.com/2uLo1LF.png)

Loop currents:
* $\large I_2-I_3=4mA$
* $\large I_1=2mA$

KVL for the super mesh
$\large 1kI_3+2kI_2+2k(I_2-I_1)+1k(I_3-I_1)=6$

We can merge 2 Loop current to simplify
* $\large I_1=2$
* $\large I_2=4$

![](https://i.imgur.com/X5eNT7l.png)

### dependent source

Practice:

![](https://i.imgur.com/qxjyCBl.png)

ans : $\large V_0=9V$

dependent current source:

![](https://i.imgur.com/NNOAM5u.jpg)

Practice:

![](https://i.imgur.com/jMODGIK.png)

ans : $\large V_0=12V$