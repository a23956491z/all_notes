---
tags : machine-learning  data-mining
---

## Lazy v.s. Eager leanring
* **Lazy** learning :
	* stores simple traning data, wait for sepicific test tuple
	* Less traning time, more predict time
	* multiple hypothesis from linear functions
* **Eager** leanring :
	* given traning set, build a model to classify new data
	* single hypothesis


## Instance-Based
Store training data and compare the new instance(data)
Methods:
* k-nearest neighbor approach
* locally weighted regression
* case-based reasoning

---
## KNN(K-Nearest Neighbor alg.)
* put instance in n-D space
* nearest neighbor defined by Euclidean distance

### 補充：Distnace
1. Euclidean distance：
2. Manhattan distance：

> k-NN return the most common value among the k training examples nearest to $X_q$

example:
	k = 8, there is 6 green & 2 red near black, so the black dot predict to green

>Given a test instance i, find the k closest neighbors and their labels
>Predict i’s label as the majority of the labels of the k nearest neighbors

Example2: 用耐酸性和強度判斷面紙的好壞
![](https://i.imgur.com/hd3alVH.png)
Test data：耐酸性=3，強度=7

1.先計算測試資料和Dataset內所有點的距離
![](https://i.imgur.com/LVem0rD.png)
2.找出最近的K個距離，其他的排除在外，例如這裡K=3
![](https://i.imgur.com/IhXnMXI.png)
3.在這些最近距離的資料中，哪個類別最多，Test data就屬於這個類別

### 在Scikit-learn中使用KNN
#### 基本用法
```python
knn = neighbors.KneighborsClassifier(n_neighbors=k)
knn.fit(data, label)
knn.predict(test_data)
```

#### 參數
```python
class sklearn.neighbors.KNeighborsClassifier(
	n_neighbors=5,
	weights='uniform', 
	algorithm='auto', 
	leaf_size=30, 
	p=2, 
	metric='minkowski', 
	metric_params=None, 
	n_jobs=None, 
	**kwargs)
```
1. algorthm 有auto，ball_tree，kd_tree，brute等等可以選
2. p-value是用哪種距離，p=1用曼哈頓距離，p=2用歐式距離

使用範例：
```python
import pandas as pd
import numpy as np
from sklearn import neighbors

# durability 代表面紙耐酸性
# strength 代表面紙的強度
data = pd.DataFrame({
	"durability" : 	[7,7,3,1],
	"strength":		[7,4,4,4],
})

# 1代表好面紙 0代表壞面紙
label = np.array([0,0,1,1])
k = 3

knn = neighbors.KNeighborsClassifier(n_neighbors=k)
knn.fit(data, label)

# 預測新產品（一定要二維陣列，即使只有一筆資料）
new_product = pd.DataFrame({
	"durability" : 	[3],
	"strength":		[7],
})

# 用np.array也可以
# new_product = np.array([[3,7]])
 
# 用DataFrame的2-array也可以
# new_product = pd.DataFrame(np.array([[3,7]]))

# 用list也可以
# new_product = [[3,7]]

print(knn.predict(new_product))
```

---

## Case-Based reasoning
Need domain knowledge, Store symbolic description.
> Uses a database of problem solutions to solve new problems


---

