---
tags : machine-learning Lee-Hong-Yee
---

## 回歸分析

---
李宏毅

### Step 1：Model
A set of funtions $f_1, f_2...$
assume we use $y = b + wx_{cp}$

-> Linear model：$y = b+ \sum{w_ix_i}$

### Step 2：Goodness of functions
Loss function $L$：
* input：a function
* output：how bad it is
* $L(f)=L(w,b)$
* ex : $= \sum{(y^n - (b + w* x ^n_{cp}))^2}$(Estimation error)

function input & function output(scalar)：
![[Pasted image 20210119163818.png]]

Training Data：10 pokemons
![[Pasted image 20210119163927.png]]

###  3：Best function
Pick the "Best" function in step 2
$f^* = arg(min(L(f)))$
$w^*, b^* = arg(min(L(w,b)))$
$= arg(min(\sum{(y^n-(b+w*x^n_{cp}))^2}))$

如果我們窮舉：
![[Pasted image 20210119164834.png]]

Or **Gradient descent**：
loss function $L(w)$ with one parameter $w$
* pick an initial value $w^0$
* Compute $\cfrac{dL}{dw}\big|_w = w^0$
* $w^1 \leftarrow w^0 - \eta\cfrac{dL}{dw}\big|_w = w^0$
* $\eta$ is **learning rate**
* 多次迭代後會找到 斜率為0的local optimal

如果我們用剛剛的loss function

![[Pasted image 20210119171845.png]]

可能會因為不同的初始點，導致下降後找到的最低點不同
但是在Linear regression中，loss function $L$ is **convex**
Convex：沒有local optimal，找到的最低點必然是Global optimal
 
 ### The result:
 
 ![[Pasted image 20210122050711.png]]
 
 這個結果我們不是很滿意
 
 another model:
 
 加入平方項之後看起來還不錯
 ![[Pasted image 20210122050848.png]]
 
 那如果我們用更複雜的model:
 ![[Pasted image 20210122051129.png]]
 ![[Pasted image 20210122051257.png]]
 
 我們會發現Testing error已經比原本的model更大了
 
 原因很簡單，是因為更複雜的model，通常包含了更多的funtion space
 所以可以讓training的error更低，但是卻不一定可以涵蓋到testing data
 ![[Pasted image 20210122051520.png]]
 
 **Overfitting**：更複雜的model不一定會有更好的結果 
 ![[Pasted image 20210122051607.png]]
 
### Back to step1:
![[Pasted image 20210122052041.png]]
搜集更多資料後，我們發現有其他的因素影響著
那就是寶可夢的物種

所以我們可以重新設計model

此時我們根據物種選擇個別函式
![[Pasted image 20210122052227.png]]
![[Pasted image 20210122052311.png]]

最後的結果：
![[Pasted image 20210122052628.png]]

### Back to step2:
當模型具有一定複雜度的時候，例如：
![[Pasted image 20210122053518.png]]

甚至我們可以對loss function做更動

![[Pasted image 20210122053252.png]]

而這裡的lambda要手動調整
我們期待能拿到更**平滑**的function
對輸入比較不敏感，可以有自然過濾雜訊的能力
而這裡的$b$(bias)，不需要加入考量

![[Pasted image 20210122053612.png]]

當lambda越大function越平滑
而我們可以藉由調整lambda去找出最適合的平滑度

## Prediciton
Prediciton is only for numerical

Simiarity to classification:
* construct a model
Difference from classification:
* classificaiton need categorical label

## Linear regression
$y = w_0 + w_1x$
$w_0$ is y-intercept & $w_1$(slope) is regression coffiicents

* multiple linear regression
	* traning data is the form $(x1,y1),(x2,y2)..$
	* Ex: for 2-D data, we have $y = w_0 + w_1x_1 + w_2x_2$
![](https://i.imgur.com/qpmTizr.png)


* Method of least squares:
> estimates the best-fitting straight line

![](https://i.imgur.com/cVz1LAL.png)

$\large y = ax+b$ 

$\large b = \frac{\sum{xy}}{\sum{x^2}} \quad  a = \frac{\sum{y}}{\sum{n}}-\frac{b\sum{y}}{n}$

* Regression Tree
	* CART: Classification And Regression Trees
	* Each leaf sotres a continuous-valued prediciton(linear)
	* the parent node attribute is the average of child from leaf to root
	* 