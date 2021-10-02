---
tags : data-mining
---

Similarity
* how alike are 2 data objects
* usually in $[0,1]$


Dissimilarity matrix : only contains distances
![](https://i.imgur.com/6yb1gD5.png)

## binary variable
if we have a 2 data object like this (binary attribute):
![](https://i.imgur.com/BJzWPvo.png)

we can get a table like this:
* for amount of $(i,j) = (1,1)$ is $q$
* for amount of $(i,j) = (1,0)$ is $r$
* ...
![](https://i.imgur.com/qsKwKYD.png)


### Dis
* Distance for **symmetric** binary variable:
![](https://i.imgur.com/GYF9NeR.png)
* Distance for **asymmetric** binary variable:
![](https://i.imgur.com/xwTIxWs.png)


Jaccard coefficient : **similarity** for asymmetric binary variable
![](https://i.imgur.com/jLWLeaO.png)
