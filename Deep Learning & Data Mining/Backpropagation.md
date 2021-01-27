誤差反向傳播法，可以更有效率地計算權重梯度

## 引入計算圖
### 問題1
買了2顆單價為100元的蘋果，營業稅是10%，請計算出需要支付的金額
![[Pasted image 20210127114842.png]]

分離係數：
![[Pasted image 20210127114925.png]]

### 問題2
買了2顆100元的蘋果，3顆150元的橘子，營業稅10%，計算出需要支付的金額
![[Pasted image 20210127115006.png]]

### 傳播
如問題1,2 由左往右計算的話，稱為**正向傳播**(*forward propagation*)
而既然可以正向傳播，自然也可以反向傳播

### 局部性計算
不論整體執行了什麼，都可以從自己相關的資料中，計算出結果

例如不論我買了多少東西，我只要有前一個輸出和蘋果，就可以計算出輸出
![[Pasted image 20210127115232.png]]

### 反向傳遞微分
當蘋果的價格上漲，最後的金額會產生什麼變化？
相對於是蘋果價格對於支付金額的微分

![[Pasted image 20210127115533.png]]
而反向傳播是傳播*局部性微分*

這裡$y=f(x)$，下面的$E$代表下層傳回的微分值
![[Pasted image 20210127142632.png]]

而可以連續傳遞微分值的奠基就是*連鎖律*
![[Pasted image 20210127142751.png]]

## 反向傳播

### 加法Perceptron
假設$z = x+y$，各對$x,y$做偏微分
![[Pasted image 20210127143154.png]]
![[Pasted image 20210127143213.png]]
也就是說，遇到加法節點，直接把上一層微分傳遞下去

### 乘法Perceptron
假設$z = xy$，各對$x,y$做偏微分
![[Pasted image 20210127143337.png]]
![[Pasted image 20210127143406.png]]


```python
class MulLayer:
    def __init__(self):
        self.x = None
        self.y = None

    def forward(self, x, y):
        self.x = x
        self.y = y
        out = x*y

        return out
    def backward(self, dout):
        dx = dout * self.y
        dy = dout * self.x

        return dx, dy
```

原本的蘋果範例：
![[Pasted image 20210127143457.png]]

```python
# input
apple = 100
nums = 2
tax_rated = 1.1

# Forward
apple_layer = MulLayer()
tax_layer = MulLayer()

total_price = apple_layer.forward(apple, nums)
taxed_price = tax_layer.forward(total_price, tax_rated)

print(taxed_price)

# Backward
dprice = 1
dtaxed_price, dtax = tax_layer.backward(dprice)
dtotal_price, dnum = apple_layer.backward(dtaxed_price)

print(dtotal_price)
```

### 活化函數層
* ReLU
![[Pasted image 20210127144740.png]]

```python
class Relu:
    def __init__(self):
        # mask is numpy boolean array
        self.mask = None
    def forward(self, x):
        self.mask = (x <= 0)
        out = x.copy()
        out[self.mask] = 0

        return out

    def backward(self, dout):
        dout[self.mask] = 0
        dx = dout

        return dx
```

* Sigmoid
$\large y = \cfrac{1}{1+e^{-x}}$
$\large \cfrac{\partial y}{\partial x} = \cfrac{\partial (\cfrac{1}{1+e^{-x}})}{\partial x} =  \cfrac{\cfrac{-\partial(1+e^{-x})}{\partial x}}{(1+e^{-x})^2} =  \cfrac{e^{-x}}{(1+e^{-x})^2}$
$\large \cfrac{\partial y}{\partial x} = y^2\times(\cfrac{1}{y}-1) = y(1-y)$

當然也可以用組合Perceptron的方式
![[Pasted image 20210127150925.png]]

最後：
![[Pasted image 20210127151019.png]]
```python
class Sigmoid:
	def __init__（self):
		self.out = None
	
	def forward(self, x):
		out =  1 / (1 + np.exp(-x))
		self.out = out
		
		return out
	
	def backward(self, dout):
		dx = dout * (1.0 - self.out) * self.out
		
		return dx
```

### Affine
Affine層即是利用矩陣計算權重訊號的總和
也就是利用正向傳播，計算矩陣乘積，在幾何學中稱作**仿射轉換**(*Affine Transfromation*)

![[Pasted image 20210127151450.png]]

![[Pasted image 20210127151544.png]]
![[Pasted image 20210127152011.png]]
這裡的$X$與$\cfrac{\partial L}{\partial X}$形狀相同
$W$與$\cfrac{\partial L}{\partial W}$形狀相同
![[Pasted image 20210127152218.png]]

```python
class Affine:
    def __init__(self, W, b):
        self.W = W
        self.b = b
        self.x = None
        self.dW = None
        self.db = None

    def forward(self, x):
        self.x = x
        out = np.dot(x, self.W) + self.b

        return out

    def backward(self, dout):
        dx = np.dot(dout, self.W.T)
        self.dW = np.dot(self.x.T, dout)
        self.db = np.sum(dout, axis=0)

        return dx
```
處理整個批次的Affine
![[Pasted image 20210127164052.png]]

```python

class Affine:
    def __init__(self, W, b):
        self.W =W
        self.b = b
        
        self.x = None
        self.original_x_shape = None
        # 重み・バイアスパラメータの微分
        self.dW = None
        self.db = None

    def forward(self, x):
        # テンソル対応
        self.original_x_shape = x.shape
        x = x.reshape(x.shape[0], -1)
        self.x = x

        out = np.dot(self.x, self.W) + self.b

        return out

    def backward(self, dout):
        dx = np.dot(dout, self.W.T)
        self.dW = np.dot(self.x.T, dout)
        self.db = np.sum(dout, axis=0)
        
        dx = dx.reshape(*self.original_x_shape)  # 入力データの形状に戻す（テンソル対応）
        return dx
```

### Softmax-with-Loss

> 神經網路的處理分成推論(inference)與學習，在推論階段一般不會用到softmax，而直接把最後的affine層當做辨識結果，但是神經網路的學習需要用到softmax層，而沒有經過正規化的輸出結果稱作評分(score)

這裡的softmax層，包含損失函數的交叉熵誤差
![[Pasted image 20210127165044.png]]

而結論是：
![[Pasted image 20210127165105.png]]
而softmax的反向傳播結果，其實就是*softmax層的輸出與訓練資料的差*，而這個差分會傳遞給上一層
```python
class SoftmaxWithLoss:
    def __init__(self):
        self.loss = None
        self.y = None
        self.t = None

    def forward(self, x, t):
        self.t = t
        self.y = softmax(x)
        self.loss = cross_entropy_error(self.y, self.t)

        return self.loss
    def backward(self, dout=1):
        batch_size = self.t.shape[0]
        dx = (self.y - self.t) / batch_size

        return dx

```

》 交叉熵誤差+Softmax與均方誤差+恆等函數，都可以讓反向傳播時，傳回Output與實際Label間的誤差，這是這些誤差函數的特別設計

## 實際執行

神經網路的學習步驟：
* 前提：神經網路有可適應資料的權重與偏權值，藉由調整這些參數可以適應訓練資料，這個過程稱作學習
* 步驟一：**小批次**，從訓練資料中隨機取出部分資料
* 步驟二：**計算梯度**，計算與各權重有關的損失函數梯度
* 步驟三：**更新參數**，往梯度方向少量更新權重參數
* 步驟四，重複步驟一二三