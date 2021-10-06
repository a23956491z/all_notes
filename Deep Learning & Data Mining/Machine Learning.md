---
tags : machine-learning Lee-Hong-Yee
---

#data-science

# 簡介
## 機器學習的種類
是否需要人類監督：
* 監督式學習
* 非監督式學習
* 半監督式學習
* 增強學習

資料的處理方式：
* 批次學習
* 線上學習

### 監督式學習
* 訓練集
	* 由**輸入內容**與**期望輸出**組成
	* 輸出可以是數值或是類別
* 以訓練集(training dataset)建立模型
* 並用該模型預測新案例

### 非監督式學習
* 資料集沒有經過標記
* 自動對資料**分類**或**分群**
![](https://i.imgur.com/dgmCteZ.png)


### 半監督式學習
* 資料集中部分有標記過
* 使用有標記的部分訓練模型
* 未標記的資料用來改善模型

### 增強式學習
* 通常應用與無法事先標記的資料：如遊戲
* 針對機器的行爲做出回饋（處罰、獎勵）
![](https://i.imgur.com/EpFqfsZ.png)

### 批次學習 vs 線上學習
* 批次學習
	* 又稱爲離線學習
	* 模型訓練時，一次使用一整個資料集
* 線上學習
	* 一筆新的資料輸入，即立刻更新模型

## 建構專案
1. 專案問題解析
	* 確定問題
	* 評估可行性
2. 資料前處理
	* 資料補齊
	* 資料過濾
	* 資料結構化
	* 資料正規化
3. 特徵工程
	* 特徵向量化，如ID、性別
	* 特徵衍生，用現有特徵組合新特徵
	* 特徵重要性評估，特徵對目標的影響程度
	* 特徵維度縮減
4. 選擇演算法
	* 常規演算法：分類、分羣、回歸
	* 深度學習演算法：深度學習網路、卷積
5. 模型訓練
	* 設定模型參數，如：輸入大小、模型結構
6. 模型評估
	* 評估指標
		* 正確率 Accuracy
		* 精確率 Precision
		* 召回率 Recall
		* F值 F-measure



# 常見演算法
## 決策樹 & 隨機森林
![[Decision Tree]]

## 線性回歸 & 羅吉斯回歸

## 支援向量機


## KNN(K臨近演算法)
![[Lazy learning#KNN K-Nearest Neighbor alg]]

## 貝氏分類器

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

