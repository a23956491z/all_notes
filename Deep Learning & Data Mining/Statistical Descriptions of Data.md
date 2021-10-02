---
tags : data-mining
---

# Statistical Descriptions of Data
* Motivation : to stand for data
	* central tendency
	* variation & spread
* Data dispersion
	* median
	* max
	* min
	* quantiles
	* outliers
	* variance

## Central Tendency
* Mean
	* Weighted arthmetic mean
	* Trimmed mean
* Median
* Mode :  most frequently value
	* Unimodal
	* bimodal
	* trimodal

### Trimmed mean
ex: `1 2 6 7 7 9 11 11 11 19`

$X_{tri(10)}$ which means trimming 10% smallest & largest data and
* result : `(2+6+7+7+9+11+11+11)/8`moodle/course/view.php?id=88443

if we have remaining: **interpolation**
$X_{tri(14)} = (X_{tri(20)}-X_{tri(10)})*\cfrac{14-10}{20-10}$

### Symmetric vs Skewed Data
![](https://i.imgur.com/4g9lN2y.png)

![](https://i.imgur.com/294QVUG.png)

## Data Dispersion
### Variance 
![](https://i.imgur.com/3bMrFIC.png)


### Standard deviation
sqrt of variance


### Quartile
* $Q_1$ ($25^{th}$ percentile)
* $Q_3$ ($75^{th}$ percentile)

### Inter-quartile range
$IQR=Q_3 - Q_1$

### Five number summary
* min
* $Q_1$
* median
* $Q_3$
* max


### Outlier
values higer/lower than $IQR*1.5$


## Graphic Display

### Boxplot
based on **five number summary**
![](https://i.imgur.com/OOKBgww.png)


### Histogram
* x-axis : values
* y-axis : frequency

![](https://i.imgur.com/4NhJdmo.png)

sometimes Historgrams can show more information than boxplot
e.g. this 2 distrubtuion have same boxplot
![](https://i.imgur.com/8paRLwP.png)


### Quantile plot

### Quantile-quantile(q-q) plot
Comparing **2 dataset**


We can see only have 9 unit on both axis
* 3rd unit is $Q_1$
* 7rd unit is $Q_3$

![](https://i.imgur.com/N6QIRGk.png)
* $Q_1$ of first dataset is 60
* $Q_1$ of second dataset is about 65

### Scatter plot
![](https://i.imgur.com/bGMqzbi.png)

Positively correlated:
![](https://i.imgur.com/rUsGuSb.png)

Negatively correlated:
![](https://i.imgur.com/KnAY7yr.png)

both:
![](https://i.imgur.com/vt6nuPs.png)

unrelated
![](https://i.imgur.com/8COwlNK.png)
