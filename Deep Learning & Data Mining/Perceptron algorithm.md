---
tags : machine-learning
---

感知器(perceptron)是神經網路的根基

## What is perceptron
收到多個訊號後，計算並輸出單一訊號

例如圖一的這個單純感知器(或稱人工神經元artificial neuron)

![[Pasted image 20210122230148.png]]
**圖2.1，接受兩個輸入訊號的感知器**

$x1,x2$作為輸入訊號
$y$是輸出訊號
$w1,w2$代表權重
神經元計算出的值要超過 *臨界值$\theta$* 才會輸出1

也就是以下算式
![[Pasted image 20210122230445.png]]
**式2.1**

## 用感知器實現邏輯電路

### AND Gate

![[Pasted image 20210122230654.png]]
**圖2.2，AND閘的真值表**

此時我們要決定$w1,w2,\theta$的值
然而滿足這個真值表的參數有無限多種
我們可以隨便舉幾個 $(w1,w2,\theta)=(0.5,0.5,0.7)=(1,1,1)$

### NAND Gate

![[Pasted image 20210122230935.png]]
**圖2.3，NAND閘的真值表**

隨便舉幾個 $(w1,w2,\theta)=(-0.5,-0.5,-0.7)$

### OR Gate

![[Pasted image 20210122231013.png]]
**圖2.4，OR閘的真值表**

隨便舉幾個 $(w1,w2,\theta)=(0.5,0.5,0.3)$

### XOR Gate

![[Pasted image 20210122231201.png]]
**圖2.5，XOR閘的真值表**

假設我們參數設 $(w1,w2,\theta)=(-0.5,1,1)$
![[Pasted image 20210122231341.png]]
**式2.3**

再把XOR的真值表畫出來
根據上面的算式我們可以發現$-0.5+x_1+x_2=0$這條算式
*應該* 要將輸出0與1劃分開來

![[Pasted image 20210122231517.png]]
**圖2.6 感知器視覺化，三角形與圓形是0**

但是我們會發現，單一個線性的感知器不論如何
都沒辦法完成我們的任務

但是我們可以藉由組合感知器來達到我們的目的

## 多層感知器

我們可以藉由組合多個邏輯閘來實現XOR

![[Pasted image 20210122232026.png]]
**圖2.11，搭配OR閘 NAND閘 AND閘 完成XOR閘**

單層感知器無法表現的部分，只要多增加幾層常常就能完成

## 程式呈現
```python
def AND(x1, x2):
    w1, w2, theta = 0.5, 0.5, 0.9

    if w1*x1 + w2*x2 > theta:
        return 1
    return 0
```

或是我們可以把$\theta$改成偏權值$b$(bias)
![[Pasted image 20210122234033.png]]
**式2.2**

將$\theta$改成偏權值，並利用矩陣運算
```python
def AND2(x1, x2):
    w = np.array([0.5, 0.5])
    x = np.array([x1, x2])
    b = -0.9

    if (np.sum( w*x ) + b) > 0:
        return 1
    return 0
```

組合多個傳感器
```python
def perceptron(w, b, x):
    if(np.sum( w*x) + b) > 0:
        return 1
    return 0

def OR(x1, x2):
    x = np.array([x1, x2])
    return perceptron(np.array([0.5, 0.5]), -0.3, x)

def NAND(x1, x2):
    x = np.array([x1, x2])
    return perceptron(np.array([-0.5, -0.5]), 0.7, x)


def XOR(x1, x2):
    y1 = NAND(x1,x2)
    y2 = OR(x1,x2)

    return AND(y1,y2)
```


