雖然感知器能為我們處理複雜的計算
但是我們卻需要人工調整其參數

所以神經網路就是為了解決這個問題

最左邊是輸入層，右邊是輸出層
而中間是隱藏層，顧名思義我們看不到隱藏層的神經元
![[Pasted image 20210122235804.png]]
**圖3.1 神經網路的範例**

而這張圖雖然有三層，但只有兩層有權重
所以我們會叫他雙層網路而非三層

而我們過去的網路並沒有真正將偏權值$b$當做 參數來看

![[Pasted image 20210123000143.png]]
**圖3.3 清楚顯示偏權值**

## 活化函數(Activation function)


而下一步，我們把算式簡化成另一個形式
![[Pasted image 20210123000321.png]]
**圖3.31 式3.2以及式3.3**

而這裡的$h(x)$這種函數稱為活化函數
也就是決定訊號總合如何發火的功能

也可以寫成這樣
![[Pasted image 20210123001022.png]]
**圖3.31 式3.4以及式3.5**

而這種類型的活化函數我們會成為**階梯函數**(Step function)
而其他的函數，就是從感知器到神經網路的關鍵

### Sigmoid

![[Pasted image 20210123001316.png]]

$exp(-x)$就代表$e^{-x}$

### 程式化

```python
def step_function(x):
	if x > 0:
		return 1
	return 0
```

改成numPy的版本增加泛用性
```python
def step_function(x):
	y = x > 0 #Bool array
	return y.astype(np.int)
```

畫出階梯函數
```python
import matplotlib.pylab as plt

x = np.arange(-5,5,0.1)
y = step_function(x)
plt.plot(x,y)
plt.ylim(-0.1,1.1)
plt.show()
```
![[Pasted image 20210123002817.png]]
**圖3.6 階梯函數的圖表**

Sigmoid
```python
def sigmoid(x):
    return 1 / ( 1 + np.exp(-x))
```

![[Pasted image 20210123003117.png]]
**圖3.7 Sigmoid函數的圖表**

### 兩者差異
主要是平滑度
sigmoid可以產生連續性的輸出
輸出這個訊息的重要程度，而不是單單的二元輸出


### 非線性函數的特色
非線性函數讓我們做層疊變得有意義
否則我們 層疊後，也僅僅多了幾次計算
跟單層沒什麼兩樣
也就是無法讓感知器疊加，來達到我們要的目的

### ReLU(Rectified Linear Unit)
而最近更常使用ReLU做激活
```python
def relu(x):
    return np.maximum(0, x)
```
![[Pasted image 20210123003352.png]]


## Blocks of Neural Network
```python
from keras import models
from keras import layers

network = models.Sequential()
network.add(layers.Dense(512, activation='relu', input_shape(28*28,)))
network.add(layers.Dense(10, activation='softmax'))
```

神經網路由*Layer* 組成
通常 layers是為了提取出 *representations*
而這裡我們可以看到這個模型包含兩個*Dense* layers
意即Densely connected(fully connected)

而第二層是*softmax* layer，回傳一個機率，代表信心分數

接下來我們還需要
* Loss function， ![[Regression#Step 2：Goodness of functions]]
* optimizer
* Metrcs to monitor during traning and testing

於是就可以執行compile
```python
network.compile(optimizer='rmsprop',
				loss='categorical_crossentropy',
				metrics=['accuracy'])
```

### Mini-batch Stochatic Gradient descent


## 多維陣列運算

我們可以利用`np.ndim()`取得該array的維度
`A.shape`可以取得他的形狀(長度)
```python
>>> import numpy as np
>>> A = np.array([1,2,3,4])
>>> print(A)
[1 2 3 4]
>>> np.ndim(A)
1
>>> np.shape
(4,)
```

矩陣乘積
![[Pasted image 20210123113305.png]]

用`np.dot()`來做兩個矩陣間的內積
```python
A = np.array([[1,2], [3,4]])
print(A.shape)

B = np.array([[5,6], [7,8]])
print(B.shape)

print(np.dot(A,B))
```

內積時要符合其 相連維度 元素數量相同
![[Pasted image 20210123113707.png]]
![[Pasted image 20210123113753.png]]