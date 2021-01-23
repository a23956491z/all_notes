## Spanning Tree
1. 由**深度優先**或**廣度優先法**進行走訪
2. 可以得到**最少的邊**來連接所有頂點，且不會形成迴路，
3. 這種子圖會是一種樹狀結構（任何兩個頂點間路徑唯一）
4. 這樣的樹可以成為**擴張樹**或**生成樹**

![](https://i.imgur.com/5xZPu4m.png)
![](https://i.imgur.com/WANEv2z.png)

> 假設$G=(V,E)$，而$S=(V,T)$是$G$的擴張樹，其中$T$是追蹤時所拜訪過的邊，此時有以下特性：
> 1. $E=T+K$，$K$表示追蹤後未被拜訪的邊
> 2. 任兩頂點$V_1$及 $V_2$，在擴張樹$S$中唯一Path
> 3. 加入$K$中任何一個邊於$S$，會造成循環



![](https://i.imgur.com/L5nGLnJ.png)
## Minimum Cost Spanning Tree

若擴張樹之**權重總和為最小**，我們可稱其為 最小成本擴張樹

1. Kruskal：
![[Kruskal's Algorithm#Concept]]

2. Prim：
![[Prim's Algorithm#Concept]]