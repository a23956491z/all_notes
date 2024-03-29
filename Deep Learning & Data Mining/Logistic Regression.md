---
tags : machine-learning
---
### 邏吉斯回歸
類似於線性回歸，不過自變數與應變數間的相關性以**指數**的方式變動
* 邏輯斯回歸常用於應變數是離散資料的問題，如分類問題
![](https://i.imgur.com/2NUEYuz.png)

線性分析希望資料盡可能貼近紅線：
![](https://i.imgur.com/aDnH74b.png)

邏輯斯回歸希望資料盡可能被分成兩類：
![](https://i.imgur.com/p3Lu6EH.png)

與Perceptron的差異：
* 激活函數：Sigmoid Function
* 損失函數：Cross entropy Error Function
* 具有正規化項(Regularization Term)，或懲罰項，避免overfitting

優點：
* 實現簡單
* 計算量小、運算快、儲存資源低
缺點：
* 特徵空間大時，性能不好
* 容易underfitting
* 通常只能處理二分類問題
* 非線性特徵需要進行轉換

### 交叉熵誤差函數
Cross entropy error function
* $N$ ：資料數
* $y_i$：預測值
* $t_i$：正確值（標籤）
![](https://i.imgur.com/5mycRvf.png)

### 正規化
Regulation，在學習時給予懲罰，讓決策分界線更平滑
* Loss function = 原Loss function + 正規化項
* L2 正規化：**權重的平方**作爲懲罰項
* L1 正規化：**權重的絕對值**作爲懲罰項


---

## Step 1 : function set
用什麼機率分佈模型都可以(例如高斯分佈)

而我們要求$x$在這個機率分佈中
有多少的機率是$C_1$，也就是$\large P_{w,b}(C_1|x)$

![[Pasted image 20210126014659.png]]

Function set:
$\large f_{w,b}(x)=P_{w,b}(C_1|x)$的所有$w,b$

這樣線性的模型套入sigmoid後，我們就可以說他是Logistic regression

## Goodness of a Function
假設Traning data，是由我們定義出的機率模型產生出來的
那我們可以計算，某一組$w,b$產生出這些Training data的機率有多高
而最好的$w,b$也就是$w^*,b^*$可以有最高機率
可以產生出Traning data

也可以說是likelihood
![[Pasted image 20210126015541.png]]

而這個算式的意思，也就是找出使得likelihood最大的$w,b$
我們也可以將其變換成右式
![[Pasted image 20210126015609.png]]

Formal化，我們可以引入新的符號代表類別
![[Pasted image 20210126015819.png]]
![[Pasted image 20210126015756.png]]
![[Pasted image 20210126015851.png]]

最後就可以用一個sumation來表達：
![[Pasted image 20210126015927.png]]

而我們也可以發現，這個sumation的掛號內
是兩個Bernoulli distribution的交叉熵
也就是這兩個distribution有多接近
如果太接近，也就意味著無法分類出類別1與類別2
![[Pasted image 20210126020036.png]]

那剛剛的likelihood，就可以用交叉熵的形式表達
![[Pasted image 20210126020226.png]]

## Find the best function
也就是用Gradient descent找出他的最小
![[Pasted image 20210126020650.png]]

他的偏微分就是一大堆數學：
![[Pasted image 20210126020837.png]]
![[Pasted image 20210126020950.png]]
![[Pasted image 20210126021110.png]]

這兩項的差距就是實際的Output與模型的Output差距
![[Pasted image 20210126021217.png]]
## 與Linear Regression的比較

![[Pasted image 20210126021358.png]]

### 為什麼不能用SquareError 在Logistic上
做gradient descent時
當你離target很近，微分是0
離target很遠，微分也是0
![[Pasted image 20210126021905.png]]

我們可以發現，距離目標很遠時，Square Error幾乎平坦
微分很小很小，Gradient descent不太能work
![[Pasted image 20210126022019.png]]

## Discriminative v.s. Generative

Generative是找出機率模型的參數
再用他們算出$w,b$
![[Pasted image 20210126022434.png]]

但是算出來的結果會是不一樣的
![[Pasted image 20210126022642.png]]

文獻上會說，discriminative的表現通常會比較好
而在training data很少時，Generative的表現反而比較好
因為Generative會做某些*假設*
或者是說，data中噪音的情況比較多，Generative做的假設
也可以把噪音過濾掉

## Multi-class Classification
從Sigmoid改成Softmax
![[Pasted image 20210126024739.png]]

## Limitation
![[Pasted image 20210126024840.png]]
一條直線沒辦法

不然就是需要做Feature Transformation
![[Pasted image 20210126025147.png]]

但是Feature transformation不好找
然而我們可以層疊Logistic Regression來找Feature
![[Pasted image 20210126025402.png]]

![[Pasted image 20210126025602.png]]