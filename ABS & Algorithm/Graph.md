## Defination

Graph由頂點Vertices和邊Edges組成：
	Graph$G=(V,E)$

* 有向圖(Directed Graph) :
	* 邊有方向性
	* 邊<V1, V2>和邊<V2, V1>是不同的
* 無向圖(Undirected Graph) : 
* 非圖形結構：如含自迴圈(Self Loop)或重邊(Multi Edges)圖

* 路徑(Path)：相異兩點間所經過不重複的邊成為路徑
* 緊密連通(Strongly Connected) : 在有向圖中，任一點具有從 $V_i$到$V_j$的路徑，也有$V_j$到$V_i$的路徑
* 相鄰(Adjacent) : A, B間有邊(A->B只有單向邊，A相鄰自B)
* 分支度(Degree) : 附著於A的總邊數
  * 有向圖還分入分支度(In-Degree)及出分支度(Out-Degree)

尤拉循環：
> 從圖形中任何一個頂點，經過所有的邊，而且只能經過一次，最後再回到原出發點

尤拉路徑：
> 從圖形中任何一個頂點，經過所有的邊，而且只能經過一次，最後不一定要會到出發點

哈密頓迴路：由指定起點到指定終點，途中經過所有其他節點且只經過一次，含有哈密頓迴圈的圖就出哈密頓圖
NP Complete問題

---
### Complete Graph
每一個頂點間都有雙向的邊

無向圖：恰好有 $\frac{n(n-1)}{2}$個邊
有向圖：$n(n-1)$

---
## Representation

![](https://i.imgur.com/OIBGjyn.png)

1. Adjacency Matrix:
   * 若 vertex(A)到vertex(B)有edge，則矩陣[A][B]的值為該edge的權重
   * 新增vertex 很慢

1. Adjacency List:
   * 先以陣列列出所有vertex，再將vertex的鄰居接在後面
   * 較節省記憶體
   * 新增 刪除edge較慢
   * 新增 vertex很快
   ```C++=
	typedef struct gnode{

		int vertex;
		int weight;
		struct gnode *Link;
	}Gnode;
   ```
	
---
## Traversal

1. Depth-First-Search : 
   * Stack，先找到再說，找不到再回來
   * 記得要標記走過的點
   * 

2. Breadth-First-Search :
   * Queue, 所有能找的都找