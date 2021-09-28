---
tags : machine-learning
---

## 微分
![[Pasted image 20210124152408.png]]
如果我們用程式執行*數值微分*
```python
def numerical_diff(f, x):
	h = 10e-50
	return (f(x+h) - f(x)) / h
```
兩個主要問題：
* 10e-50 太小，會被python執行*捨入誤差*後變成0
* 可以利用**中央差分**，改善$h$不夠小造成的誤差
![[Pasted image 20210124152726.png]]

```python
def numerical_diff(f, x):
    h = 1e-4
    return (f(x+h) - f(x-h)) / (2*h)

```

> 利用微小差分計算微分的方式稱作**數值微分**
> 展開算式計算微分的方式成為解析(analytic)
> 而解析解可以算出不含誤差的真微分

使用範例：
```python
def numerical_diff(f, x):
    h = 1e-4
    return (f(x+h) - f(x-h)) / (2*h)

def func1(x):
    return 0.01*x**2 + 0.1*x

import numpy as np
import matplotlib.pylab as plt

x = np.arange(0.0, 20.0, 0.1)
y = func1(x)

plt.xlabel('x')
plt.ylabel('f(x)')
plt.plot(x, y)

print(numerical_diff(func1, 5))
print(numerical_diff(func1, 10))
plt.show()
```
![[Pasted image 20210124152949.png]]
![[Pasted image 20210124152940.png]]
## 梯度
梯度就是，把所有變數的偏微分看做向量的表示方式

```python
#assume we have multiple x ([x0, x1, x2...])
def numerical_gradient(f, x):
	
	h = 1e-4
	grad = np.zeros_like(x)
	
	for idx in range(x.size):
		
		tmp_val = x[idx]

		# f(x+h)
		x[idx] = tmp_val + h #only change one variable
		fxh1 = f(x)
		# f(x-h)
		x[idx] = tmp_val - h
		fxh2 = f(x)
		
		grad[idx] = (fxh1- fxh2) / (2*h)
		x[idx] = tmp_val
		
	return grad
```

Generic:
```python
def numerical_gradient(f, x):
    h = 1e-4 # 0.0001
    grad = np.zeros_like(x)
    
    it = np.nditer(x, flags=['multi_index'], op_flags=['readwrite'])
    while not it.finished:
        idx = it.multi_index
        tmp_val = x[idx]
        x[idx] = tmp_val + h
        fxh1 = f(x) # f(x+h)
        
        x[idx] = tmp_val - h 
        fxh2 = f(x) # f(x-h)
        grad[idx] = (fxh1 - fxh2) / (2*h)
        
        x[idx] = tmp_val # 値を元に戻す
        it.iternext()   
        
    return grad
```

梯度可能指向最低位置
但其實梯度指向的是 **函數值減少最多的地方**

## 梯度法

損失函數通常很複雜，而利用梯度，盡可能快地找出函數的最小值，便是梯度法。
* 從目前的位置往梯度方向走特定距離
* 計算移動後的梯度，再往梯度方向移動

以算式表示：
![[Pasted image 20210127100240.png]]
學習率$\eta$：更新的量

以程式表示：
```python
def gradient_descent(f, init_x, lr=0.01, step_num=100):
    x = init_x

    for i in range(step_num):
        grad = numerical_diff(f, x)
        x -= lr*grad

    return x
```
* `init_x`代表從哪個點開始
* `lr`代表學習率
* `step_num`代表最多執行幾次

## 神經網路的梯度
假設有個形狀2x3權重為$W$的神經網路，$L$代表Loss func
其梯度則是：
![[Pasted image 20210127102414.png]]