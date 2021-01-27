## Comprehension

* AVL Tree是一種自平衡[[Binary Search Tree]]
* 若T不為空，必須符合 $-1 \leq (平衡因子=左子樹高-右子樹高) \leq 1$
（$|Hl - Hr| \leq 1$）
* T的左右子樹也是AVL Tree
* 每個節點都會儲存樹高資訊

由於是一顆平衡樹，BST不會退化成Linked List

---
## Height & Balance Factor(BF)
> **Height of node** : Length of the longest path from it to the leaf
> **Height** = max(left_child_height, right_child_height)+1

![](https://i.imgur.com/toluLOs.png)

* Nil 的樹高是-1
* 左右子節點最大的+1，即當前節點高度

![](https://i.imgur.com/7ybIzYJ.png)
* Balance Factor = Left child height - Right child height
	* $BF(T) < -1$ : 右邊子樹更重，往左調整(旋轉)
	* $BF(T) > 1$ : 左邊子樹更重，往右調整(旋轉)
	* $-1 \leq BF(T) \leq 1$ : 平衡

---
## Theroem
* 高度$H$之AVL Tree，所需最多Node數：$(2^H)-1$
* 高度$H$之AVL Tree，所需最少Node數：$F(H+2)-1$
	* $F()$ is Fibonacci functino
	* N(H)表示為 高度H的AVL Tree
	  $N(H)=N(H-1)+N(H-2)+1$
	  ?????
	  
時間複雜度為$\Theta(\Phi ^H), \Phi=1.618(\frac{1+\sqrt 5}{2})$

|        | Average               | Worst                 |
|--------|-----------------------|-----------------------|
| Search | $\mathcal{O}(\log n)$ | $\mathcal{O}(\log n)$ |
| Insert | $\mathcal{O}(\log n)$ | $\mathcal{O}(\log n)$ |
| Delete | $\mathcal{O}(\log n)$ | $\mathcal{O}(\log n)$ |


> **Worst cast** : 所有節點的Hl都比Hr少1
> $N_h = (min.)$
> $N_h = N_{h_1} + N_{h_1}+1$
> $N_h > F_h = \dfrac{φh}{\sqrt 5},φ=1.618$
> $h < \log{φn} =  1.44\lg{n}$

---
## Balanced & Rebalancing
> hight-balanced：
> 1. Empty tree is height-balance
> 2. If T is a nonempty binary tree with TL and TR as left and right subtrees respectively, T is hight-balanced iff
>    1. TL and TR are height-balanced
>    2. Math.abs( HL - HR) <= 1 where HL and HR are the height of TL and TR respectively.


![](https://i.imgur.com/N6hE6eH.png)
**圖三：紅色表示不平衡**

**注意：Rotation前後的樹，in-order traversal必須相同**
### 1. Left Rotation
* A的右節點 = B的左節點
* B的左節點 = A

![](https://i.imgur.com/nAqdRW9.png)
**圖四：向左旋轉**

### 2. Right Rotation

* A的左節點 = B的右節點
* B的右節點 = A

![](https://i.imgur.com/Xlod2N9.png)
**圖五：向右旋轉**

---
### 1. LL型
C新增到A的左->左：對A Right rotation

![](https://i.imgur.com/ae31flZ.png)
**圖六：LL型不平衡**

### 2. LR型
C新增到A的左->右：對B Left rotation，變成LL型

![](https://i.imgur.com/0d0pvMn.png)
**圖七：LR型不平衡**

用LL型：對A Right rotation再跑

![](https://i.imgur.com/nOSf2cB.png)
**圖八：從LR型變LL型**

### 3. RR型
對A Left rotation

![](https://i.imgur.com/srrOBYt.png)
**圖九：RR型**

### 4. RL型
對B Right rotation 變RR型

![](https://imgur.com/4VDWBH5.png)
**圖十：RL型**

![](https://i.imgur.com/aHRR3s7.png)
**圖十一：從RL型變RR型**

用RR型：對A Left rotation

---
## Insert

* 插入後，由新插入的node往上檢查
* 發現某Node的BF>1，往下找兩層**走過的路徑**，並根據其方向做旋轉

## Delete

* 刪除後，從被刪除之Node Parent往上檢查高度差