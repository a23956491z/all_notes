#logic_circuit

Multiplexers(數據多工器) are a.k.a. data selectors，簡稱MUX
Allow many sources to be **routed onto** single output.
With data-select input, allowing to switch single source to output line.

![](https://i.imgur.com/2lklbai.png)
1-of-4 data selector

When S is 0 as $(S_1, S_2) = (0,0)$ we select input $D_0$
and S is 1 as $(S_1, S_2) = (0,1)$ select input $D_1$
and so on...
![](https://i.imgur.com/QdPsaHR.png)  

implement:
Output is $D_0$ only if $S_1=0$ and $S_2=0$ => $Y = D_0\bar S_1 \bar S_0$
Output is $D_1$ only if $S_1=0$ and $S_2=1$ => $Y = D_0\bar S_1 S_0$
Output is $D_2$ only if $S_1=1$ and $S_2=0$ => $Y = D_0 S_1 \bar S_0$
Output is $D_3$ only if $S_1=1$ and $S_2=1$ => $Y = D_0 S_1 S_0$

$Y_{out}$ = $Y = D_0\bar S_1 \bar S_0 + D_0\bar S_1 S_0 + D_0 S_1 \bar S_0 + D_0 S_1 S_0$

![](https://i.imgur.com/bOXHiiB.png)

74HC151
![](https://i.imgur.com/XP55DFF.png)

串接兩個MUX(74151)：
![](https://i.imgur.com/k2evFzh.png)