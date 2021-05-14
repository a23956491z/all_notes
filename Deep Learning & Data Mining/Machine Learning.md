# 資料科學

### 機器學習的種類
1. 監督式學習
2. 非監督式學習
3. 半監督式學習
4. 增強學習

### KNN(K臨近演算法)
常見的機器學習分類預測做法：
1. Logistic回歸
2. 決策樹
3. K臨近演算法
[[Lazy learning#k-Nearest Neighbor alg]]

# 機器學習(李宏毅)
Framework

首先有一堆funtions（function set）
再去評估每一個function有多好
最後找出那個最佳funtion $*f$
![](https://i.imgur.com/6WKZZgs.png)

![](https://i.imgur.com/nUE5bdT.png)

這些都是TASK:
* Regression: Output是一個數值(scalar)
   * 預測PM 2.5，預測明天上午的PM2.5，是一個數值
   藉由每一天的PM2.5的資料，預測下一天的PM2.5
* Classification: 分類
	* Binary: 是or不是
	* Multi-class: 數個選項



Scenario（學習情境）：
* Supervised learning：需要大量Label
* Semi-supervised：藉由少量labeled的資料學習，去label其他資料
* Tansfer learning：一樣是少量labeled，但是其他未labeled資料與原本資料沒有關聯
* Unsupervised learning
* Structured learning：在Supervised的領域內，大部分都是它
* Reinforcement learning：Learning from critics，它只會知道自己做的好or不好，通常是沒辦法做supervised才會用reinforcement

$\huge \sum i$

