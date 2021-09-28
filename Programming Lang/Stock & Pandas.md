---
tags : python
---


## fectch
匯出TEJ檔案

1. TEJ股價資料庫
2. 未調整股價（日）
3. 時間排序：最早的在上面


## Preprocessing

只留下我們需要的資料
1. 刪除前兩列只留股價與column name
2. 保留前六個column並更名為Date, Open, High, Low, Close, Volume
3. 三位一撇的逗號都要拿掉：
    * 儲存格格式，取消使用千分位符號
4. 另存為.csv檔(每個欄位用`','`分隔)

## Open file
```python=
filename = 'data/' + 'TEJ_0050_2019TO2020_manual' + '.csv'

# 將檔案內容存到串列中，每一列的資料為串列的一個元素
SData = open(filename).readlines()
```

我是熊貓，熊貓不需要convert
```python=
import pandas as pd

ticker = pd.read_csv(filename, index_col='Date', parse_dates=True)
```
## convert CVS string to List
* `strip()`拔掉換行
* `split()`分隔


* Straight
```python=
SData = []

#SData[0]是 column name
for line in SData[1:]:
    line = line.strip('\n').spilt(',')
    SData.append(line)
```
* Comprehension Loop 
```python=
SData = []

SData = [line.strip('\n').spilt(',') for line in SData[1:]]
```

## Indexing

column names
```python=
print(SData[0])
#['Date', 'Open', 'High', 'Low', 'Close', 'Volume']

print(ticker.columns)
#Index(['Open', 'High', 'Low', 'Close', 'Volume'], dtype='object')
```

indexing
```python=

# print 3rd element
print(SData[3])
# print 0~4 element(with column names)
print(SData[:5])

# print  3rd element
print(ticker.iloc[3])

# print 0~4 element(without column names)
print(ticker.iloc[:5])

# get data of '2019-01-02'
print(ticker.loc[pd.Timestamp('2019-01-02')])

# get list of '2020' years
# cause line[0] is type:str not type:datatime so we should convert it
SData2 = [line for line in SData1 if datetime.strptime(line[0], "%Y/%m/%d").year == 2020]

# get table of '2020' years
ticker.loc['2020'].head(3)
```


## Ploting

Plot by Close price
```python
# change the size of output picture
plt.figure(figsize = (20,10))

ticker['Close'].plot()
```
![](https://i.imgur.com/KhjHLI3.png)

Plot mean Close & Close
```python
##ticker['Close'].plot()

monthly_0050 = ticker.resample('M').mean()

ticker['Close'].plot()
monthly_0050['Close'].plot()

plt.legend(['Close','monthly_mean_close'])
```
![](https://i.imgur.com/CBIMIcY.png)

Plot 2 graph at once
```python
plt.figure(figsize = (20,10))

# 2 row 1 column 1th plot
plt.subplot(211)
plt.plot(ticker.index, ticker['Close'])

# 2 row 1 column 1th plot
plt.subplot(212)
plt.bar(ticker.index, ticker['Volume'], color = 'black')
plt.gcf().autofmt_xdate()# autoformat
```
```python
fig = plt.figure(figsize = (20,10))

ax1,ax2 = fig.add_subplot(211), fig.add_subplot(212)

ax1.plot(ticker.index, ticker['Close'])
ax2.bar(ticker.index, ticker['Volume'], color = 'black')

plt.gcf().autofmt_xdate()
```
![](https://i.imgur.com/gvsqsLO.png)

Combine 2 plot with `add_axes()`
```python
fig = plt.figure(figsize = (20, 10))

width = 1
bottom_height = 0.3
uppper_height = 1 - bottom_height
ax1 = fig.add_axes([0, bottom_height, width, uppper_height])
ax2 = fig.add_axes([0, 0            , width, bottom_height])

ax1.plot(ticker.index, ticker['Close'])
ax2.bar(ticker.index, ticker['Volume'], color = 'black')

plt.gcf().autofmt_xdate()
```
![](https://i.imgur.com/rSznCMV.png)

2 graph in 1 plot with `twinx()`
```python
fig = plt.figure(figsize = (12, 6))
       
ax1 = fig.add_subplot(111)
# 設定讓價與量的兩張圖重疊放在一張圖中
ax2 = ax1.twinx() 
#設定y座標，使量的圖顯示在下方：即量的最大數值的4倍會到 y軸的最高點，也就是設定量只畫到 1/4y
ax2.set_ylim([0, max(ticker['Volume'])*4])


ax1.plot(ticker.index, ticker['Close'])
#alpha is transparency
ax2.bar(ticker.index, ticker['Volume'], color = 'black', alpha = 0.6)

plt.gcf().autofmt_xdate()
```
![](https://i.imgur.com/Qfq8jvQ.png)