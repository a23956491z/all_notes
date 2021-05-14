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



---

## Case-Based reasoning
Need domain knowledge, Store symbolic description.
> Uses a database of problem solutions to solve new problems


---

