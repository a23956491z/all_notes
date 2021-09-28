---
tags : machine-learning
---

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

### 神經網路之乘積

兩個input$X$ 與 $2*3$矩陣做內積
![[Pasted image 20210123114020.png]]
而$X$對應$W$的維度元素一樣要一致

```python
X = np.array([1,2]) 
W = np.array([[1,3,5], [2,4,5]])
print("X shape", X.shape)
print("W shape", W.shape)
print(W)

Y = np.dot(X,W)
print(Y)
```

General：
![[Pasted image 20210123114633.png]]
![[Pasted image 20210123114647.png]]
![[Pasted image 20210123114712.png]]

### 用程式表達神經網路之傳播
第一層
![[Pasted image 20210123115443.png]]
```python
import numpy as np

def sigmoid(x):
    return 1 / ( 1 + np.exp(-x))

X = np.array([1.0,0.5])
W1 = np.array([[0.1,0.3,0.5],[0.2,0.4,0.6]])
B1 = np.array([0.1,0.2,0.3])

print("W1.shape",W1.shape)
print("B1.shape",B1.shape)
print("X.shape",X.shape)

A1 = np.dot(X, W1) + B1
Z1 = sigmoid(A1)

print("A1",A1)
print("Z1",Z1)
```

第二層
![[Pasted image 20210123115533.png]]
```python
W2 = np.array([[0.1,0.4],[0.2,0.5],[0.3,0.6]])
B2 = np.array([0.1,0.2])

print()
print("W2.shape",W2.shape)
print("B2.shape",B2.shape)
print("Z1.shape",Z1.shape)

A2 = np.dot(Z1, W2) + B2
Z2 = sigmoid(A2)

print("A2",A2)
print("Z2",Z2)
```

最後一層的活化函數與前面的隱藏層不同
![[Pasted image 20210123115706.png]]
為了統一每一層都有活化函數，但這一層不需要活化
所以我們使用*恆等函數* ，並以$\sigma$表示輸出層活化函數
```python
def identity_func(x):
    return x

W3 = np.array([[0.1,0.3],[0.2,0.4]])
B3 = np.array([0.1,0.2])

A3 = np.dot(Z2, W3) + B3
Y = identity_func(A3)
```


### 統一處理
**注意**，權重通常以大寫表示，其餘皆用小寫
```python
import numpy as np

def sigmoid(x):
    return 1 / ( 1 + np.exp(-x))

def identity_func(x):
    return x
	
def init_network():
	network = {}
	
	network['W1'] = np.array([[0.1,0.3,0.5],[0.2,0.4,0.6]])
	network['b1'] = np.array([0.1,0.2,0.3])
	network['W2'] = np.array([[0.1,0.4],[0.2,0.5],[0.3,0.6]])
	network['b2'] = np.array([0.1,0.2])
	network['W3'] = np.array([[0.1,0.3],[0.2,0.4]])
	network['b3'] = np.array([0.1,0.2])
	
	return network

def forward(network, x):
	W1, W2, W3 = network['W1'], network['W2'], network['W3']
	b1, b2, b3 = network['b1'], network['b2'], network['b3']
	
	a1 = np.dot(x, W1) + b1
	z1 = sigmoid(a1)
	a2 = np.dot(z1, W2) + b2
	z2 = sigmoid(a2)
	a3 = np.dot(z2, W3) + b3
	y = identity_func(a3)
	
	return y

network = init_network()
x = np.array([1.0, 0.5])
y = forward(network, x)
print(y)
```

## 輸出層之設計

回歸問題通常使用*恆等函數*
分類問題通常使用*Softmax函數*
![[Pasted image 20210123120639.png]]

![[Pasted image 20210123120702.png]]
![[Pasted image 20210123120755.png]]

softmax的輸出，會受到輸入的各神經元影響

用直譯器確認各個結果
```python
>>> a = np.array([0.3, 2.9, 4.0])
>>>
exp_a = np.exp(a)
>>> exp_a
array([ 1.34985881, 18.17414537, 54.59815003])
>>> sum_exp_a = np.sum(exp_a)
>>> sum_exp_a
74.1221542101633
>>>
>>> y = exp_a / sum_exp_a
>>> y
array([0.01821127, 0.24519181, 0.73659691])
```
定義之
```python
def softmax(a):
	exp_a = np.exp(a)
	sum_exp_a = np.sum(a)
	y = exp_a / sum_exp_a
	
	return y
```

### 簡單Softmax之問題

上面的softmax函數並沒有錯
但是當我們輸入很大的時候
會導致指數函數的值變很大，例如$e^{1000}$
進行除法時，可能會很不穩定

改良後的softmax（防止溢位或結果過大）
![[Pasted image 20210123121351.png]]
簡而言之就是，softmax運算時，加上某個常數$C$後，結果不變

所以我們可以對原本的輸入做平移，保證softmax執行時的正確性
```python
a = np.array([1010, 1000, 900])
print(np.exp(a) / np.sum(np.exp(a))) #exploded

c = np.max(a)
y = np.exp(a - c) / np.sum(np.exp(a-c))
print(y)
```

此時我們可以將softmax改寫成
```python
def softmax(a):
	c = np.max(a)
	exp_a = np.exp(a-c)
	sum_exp_a = np.sum(exp_a)
	
	y = exp_a / sum_exp_a
	return y
```

### Softmax特色

![[Pasted image 20210123153354.png]]
softmax函數的輸出是0~1.0之間的實數
且其輸出總和是1，使我們能解讀softmax的結果為**機率**

所以這張圖中的結果就是，有73.6%的機率是第2類別
且各元素的大小關係不變，最大的經過softmax仍然是最大

### 輸出層的數量
我們可以根據需要的類別數量
來決定輸出層的數量

例如手寫數字辨識的輸出層就是十個(0~9)

## 使用初始參數辨識手寫數字
利用學習完的參數執行神經網路，我們會稱作是**推論處理**
也稱作神經網路的正向傳播(forward propagation)

> 解決機器學習的步驟有分學習和推論，學習是進行參數權重調整，推論則是用學習到的參數進行分類

### MNIST
MNIST的手寫數字影像集，0~9構成
60000張訓練集，10000張測試集

這個影像資料是28x28的灰階影像，每一個像素是0~255的數值
每個影像資料都有其對應標籤

![[Pasted image 20210123154547.png]]
* normalize 把輸入的影像正規化成0.0~1.0
* flatten是平坦化成一維陣列
* one-hot-label是one-hot編碼，也就是`[0,0,1,0,0,0,0,0,0]`代表這個圖片標籤是2(只有第2個是1其餘都是0)

用PIL顯示影像：
![[Pasted image 20210123154904.png]]
![[Pasted image 20210123154913.png]]

進行推論處理：
![[Pasted image 20210123155100.png]]

計算正確度：
![[Pasted image 20210123155235.png]]

### 批次處理

原本我們辨識MNIST的神經網路形狀：
![[Pasted image 20210123155746.png]]
中間層是50與100個神經元
輸入是28x28形成的一維陣列
輸出層是辨識的推論結果，每一個代表各個數字的機率

那如果一次處理100張
輸出就是100x10的矩陣，儲存了100個推論結果
![[Pasted image 20210123160138.png]]

>因為處理數值運算的函式庫通常進行過最佳化，可以有效處理大型陣列


![[Pasted image 20210123160423.png]]
`argmax()`取得最大值的索引
`axis=1`代表100x10的陣列中，在第一維的陣列中找

## 神經網路之學習
學習，也就是自動取得最適當的權重參數
而神經網路的學習，是以損失函數為指標
找出損失函數最小的權重參數

> 感知器收斂定理告訴我們，可以藉由有限的學習，解決線性分離的問題，但是非線性分離問題無法自動學習

### 特徵量
要辨識數字，可以從影像中截取特徵量
也就是從輸入資料中，截取出本質資料的轉換器(常常是向量)
例如*SIFT SURF HOG* 這些特徵量
就可以利用機器學習的SVM KNN來學習這些向量

而這種機器學習的處理方式
問題在於辨識狗與數字的特徵向量提取方式不同
不同的問題需要思考不同的特徵向量

而深度學習就比較沒有人為介入的因素
![[Pasted image 20210123161411.png]]

### 訓練與測試
通常先用訓練資料，尋找最佳參數
再利用測試資料，評估訓練後的模型

因為我們需要的是模型的**一般化能力**
而過度對應某個資料集，卻無法適用其他資料集的情況
我們也成為過擬合(overfitting)

## Loss function
 神經網路以一個指標為根據，去尋找最佳參數
 而這個指標就是損失函數
 
 
### 均方誤差
![[Pasted image 20210123161826.png]]
$y_k$代表神經網路的輸出
$t_k$代表訓練資料
$k$代表資料的維度

以手寫數字為例，$y_k$ $t_k$可能是這些資料
![[Pasted image 20210123162034.png]]

也就是說數字是2的機率是60%
而答案也是2，這裡的答案使用的就是*one hot*標記

```python
def mean_squared_error(y, t):
	return 0.5 * np.sum((y-t)**2)
```

![[Pasted image 20210123162308.png]]
這個圖中可以看到，例1的損失函數結果比較小，更適合訓練資料

### 交叉熵誤差

![[Pasted image 20210123162406.png]]
這裡的$log$是以$e$為底，也就是自然對數$log_e$

![[Pasted image 20210123162621.png]]

```python
def cross_entropy_error(y, t):
	delta = 1e-7
	return -np.sum(t * np.log(y + delta))
```
注意，$log0$時會變成無限大，為了避免這種情況，所以我們加上一個極小值

![[Pasted image 20210123162826.png]]

### 小批次學習
當我們需要求出訓練資料所有的損失函數和
可能會長這樣(用交叉熵的例子)：
![[Pasted image 20210124141723.png]]
訓練資料有$N$，$t_{nk}$代表n個資料的第k個訓練資料
最後除以$N$時進行正規化，求出平均損失函數

例如MNIST有60000個訓練資料
一次以所有資料為對象計算損失函數似乎不太實際
所以我們可以抽取出一些sample近似成整體來使用

而我們挑選出一小塊就稱作是小批次(mini-batch)
例如60000張一次挑選出100張做訓練

隨機取出10張的程式可能會長這樣：
```python
train_size = x_train.shap[0]
batch_size = 10
batch_mask = np.random.choice(train_size, batch_size)

x_batch = x_train[batch_mask]
t_batch = t_train[batch_mask]
```

計算一整個批次的交叉熵誤差
```python
# t is traning data(one hot)
# y is output of neural network
def cross_entropy_error(y, t):
	if y.ndim ==1:
		t = t.reshape(1, t.size)
		y = y.reshape(1, y.size)
	
	batch_size = y.shape[0]
	return -np.sum(t * np.log(y)) / batch_size

```

如果訓練資料的Label不是one-hot，而是像*2* *7* 這種標籤時
那我們要提取出對應的output
```python
def cross_entropy_error(y, t):
	if y.ndim == 1:
		t = t.reshape(1, t.size)
		y = y.reshape(1, y.size)
		
	batch_size = y.shape[0]
	y_one_hot = y[np.arange(batch_size), t]
	
	return -np.sum(t * np.log(y_one_hot)) / batch_size
```
這裡可以特別留意`y[np.arange(batch_size), t]`這個用法
`np.arange(batch_size)`產生`0`到`batch_size-1`的陣列
若`batch_size = 5`
`np.arange(batch_size)`產生`[0, 1, 2, 3, 4]`
假設`t`儲存`[2, 7, 0, 9, 4]`

`y[np.arange(batch_size), t]`就會取出對應的第0維度與第1維度元素
`也就是產生[ y[0,2], y[1,7], y[2,0]...]`  
也就是說，我們只取出輸出中，index是Label值的那個output格子
one-hot不需要這樣做是因為，測試資料`t`中，不是Label值的其他格子放的都是0，計算出來也是0，直接加起來也無妨，所以不需要再特別取出

### 把Acc作為指標的話？
* 參數略微變化，辨識準確度可能會不變，參數微分會是0
* 即使準確度改變了，變化也會是不連續的
* 但是Loss function的變化與參數的變動都是連續的
* 連續的變化可以進行微分去做梯度下降，快速尋找

![[Pasted image 20210124145434.png]]
這裡也可以理解為什麼不用階梯函數做Loss function
因為階梯函數大部分位置微分都是0

