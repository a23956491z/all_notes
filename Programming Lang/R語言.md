# R語言 資料視覺化
```ggplot()```

```r=
library(ggplot2)
ggcars <- ggplot(cars, aes(x=speed, y=dist)) + geom_point()
ggcars
```
![](https://i.imgur.com/RZoiatj.png)



台灣銀行歷史匯率
```r=
library(ggplot2)

rate <- read.csv("ExchangeRate.csv", sep = ",")
rate

rate_stat <- ggplot(rate, aes(x = 資料日期, y = 即期)) + 
			geom_point() + stat_smooth()
rate_stat
```
![](https://i.imgur.com/rMDf0NI.png)


```r=
library(ggplot2)

rate <- read.csv("ExchangeRate.csv", sep = ",")
rate

rate_stat <- ggplot(rate, aes(x = 幣別, y = rate$現金.1)) + 
			geom_point() + 
			facet_wrap(~幣別)+
			theme_light()+
			coord_polar(theta='x')
rate_stat
```
![](https://i.imgur.com/PnxrM9B.png)


# 按键精靈

> 中國軟體：資安問題

按鍵精靈vs程式化爬蟲：
* 避免使用頻繁request，而被擋下