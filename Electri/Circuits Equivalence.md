#circuit_analysis 
#superposition

Example of former equivalence we leart
![](https://i.imgur.com/jhHh12e.png)

---
## Linearity

The model $\huge y = Tu$ is **Linear** IFF 
* additivity : $\huge T (u_1+u_2)=Tu_1+Tu_2,\forall u_1,u_2$
* homogeneity : $\huge T(\alpha u)=\alpha Tu, \forall \alpha,\forall u$

---
## 利用Homogeneity 進行假設

![](https://i.imgur.com/tMRl9Yf.png)

Assume：
* $\large V_{out} = V_2 = 1[V]$

$\large V_1 = 4kI_2 + V_2$
$\large =4k\frac{V_2}{2k}+V2 = 3[V]$....

$\large V_0 = 2kI_0+V_1=6[V]$

however $\large V_0$ is $\large -12V$
Now use homogeneity：
* $\large V_0=6$->$\large V_{out}=1$
* $\large V_0=-12$->$\large V_{out}=-2$

Practice:
![](https://i.imgur.com/Njfk2U3.png)

$\large I_0 = 3mA$

---
## Source Superposition

![](https://i.imgur.com/5VTLrEA.png)

Due to Linearity
$\huge V_L=a_1V_s+a_2I_s$

![](https://i.imgur.com/gU9xuEJ.png)

$\huge i_L=I_L^1+I_L^2$
$\huge V_L=V_L^1+V_L^2$

>Notice : The approach will be useful if solving the two circuits is simpler, or more convenient, than solving a circuit with two sources

![](https://i.imgur.com/aOrTkUJ.png)

![](https://i.imgur.com/CdoFpIf.jpg)

Practice:

![](https://i.imgur.com/8yakZTy.png)

$\large I_0=-3mA$

With Non-reference Node : We can see the **Linearity** of the result

![](https://i.imgur.com/BPlVwMb.png)