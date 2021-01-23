# Cluster Analysis
> Cluster : a collection of data objects
Similarity of another within same cluster


* Find smiliarities between data
* Which is **Unsupervised learning**
* Outline : 
    * K-means
    * EM
    * DBSCAN, OPTICS



# Partition Approach

* Density-bases approach
    * connectivity & density functions
    * i.g. **DBSACN**, **OPTICS**, DenClue
* Hierarchical approach
    * hierarchical decomposition
    * i.g. Diana, **Agnes**, BIRCH, ROCK

* Partition Algorithm
    * Construct a partition of data $D$ of $n$ objects into a set of $k$ cluster
    * Optimizes the partitioning criterion:
        * k-meas
        * Global optimal : exhaustively  enumerate

# K-Means Clustering
![](https://i.imgur.com/B38s4fI.png)

1. 一開始的兩個點是隨機產生 ->被認為是不穩定的演算法，每次跑出來的結果都不會一樣
2. 中心點會持續變動(reassign)
3. 直到instance *不會再增加或減少?*(收斂, local optimal)

* 與中心點的距離是Square Error
* optimal : 
    * Square Error最小
    * k : 3~7
    * 每一個cluster內的個數接近
* Cluster演算法中最廣泛運用的
* $O(tkn),k,t << n$, n objects, k clusters, i iterations. 
* k-means不會忽略距離很遠的點，也不容易找到形狀不規則的cluster
* cluster數量差不多的時候表現比較好

Play是output，跟其他attribute有相關，拿進去算沒有意義