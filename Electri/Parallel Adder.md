#logic_circuit 

Terms:
* Most significant bit (**MSB**)：最重要位元(最大or最左位元)
* Least significant bit (**LSB**): 最不重要位元(最小or最右位元)
* nibble : a group of 4bits

4-bit parallel adder symbol:
![](https://i.imgur.com/1dKu1SV.png)

Adder Expansion: *Cascading of two 4-bit to form an 8-bit*
![](https://i.imgur.com/sIUyGFn.png)

## Detail in adders:
* **Ripple Carry** : Put $C_{out}$ into the next  $C_{in}$
> carry out of each full-adder is onnected to the carry input of the next higher-order stage.

However, it causes a **time delay** in each addition process.
![](https://i.imgur.com/mINBDgT.png)

---

* **Look-Ahead Carry** : 利用遞迴關係式把高層的$C_{in}$以低層的計算結果表示
	Terms:
	* Carry generation : 這個Carry bit是純粹由A與B進位提供*(produced internally)*
	$C_g = AB$
	* Carry propagation : 加上$C_{in}$後，需不需要再進位(增值)
	$C_p = A+B$
	* Final $C_{out}$ : $C_{out} = C_g + C_pC_{in}$
	類似串接兩個half-adder 時的 Output Carry
	![](https://i.imgur.com/vbTpBQY.png)
	
我們可以只用這些 $C_g \& C_p$算出$C_{out}$
當一次得出所有bit的 $C_g \& C_p$時，意味著可以一次得出所有 $C_{out}$

![](https://i.imgur.com/pXrdcfm.png)
![](https://i.imgur.com/YUrLbqI.png)

Implement:
從此圖可以發現，
若通過AND及OR邏輯閘時間趨進0，
adder operation基本上同步

![](https://i.imgur.com/z2becqw.png)
