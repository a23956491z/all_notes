---
tags : data-mining
---

# Data Object

data object = entity

Data object described by **attribute**

attribute : data field which is characteristic/feature of data object
* **Discrete Attribute**, e.g. gender
* **Continuous Attribute**, e.g. height

Attribute types:
* Binary
	* Symmetric binary, e.g. gender
	* Asymmetric bynary, e.g. medical test positive/negative
* Ordinal, e.g. *Size={small, medium, large}*
* Quantity 
	* Interval , on equal-sized units, e.g. : temperature
	* Ratio, nonlinear scale
	
## Ratio-Scaled Variable
apply **logarithmic transformation** to calculate distance
![](https://i.imgur.com/ZW6Dmpd.png)


## Ordinal Variable
**order is important**, e.g. *rank*

### Distance
can be treated as Interval-Scaled

map the range of each variable onto $[0,1]$:
* $M$ is the biggest rank
* $r$ is $n^{th}$ rank
* $z=\cfrac{r-1}{M-1}$

## Mixed types 
sometimes using weighted formula to calculate distance
![](https://i.imgur.com/UGa0YX5.png)
