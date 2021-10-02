---
tags : data-mining
---

Similarity
* how alike are 2 data objects
* usually in $[0,1]$

**Proximity** measure : Similarity or Dissimilarity measure

Dissimilarity matrix : only contains distances
![](https://i.imgur.com/6yb1gD5.png)

## Binary Variable
if we have a 2 data object like this which are binary variable(binary attribute):
![](https://i.imgur.com/BJzWPvo.png)

we can get a table like this:
* for amount of $(i,j) = (1,1)$ is $q$
* for amount of $(i,j) = (1,0)$ is $r$
* ...
![](https://i.imgur.com/qsKwKYD.png)


### Dissimilarity (Distance)
* Distance with **symmetric** :
![](https://i.imgur.com/GYF9NeR.png)
* Distance with **asymmetric**:
![](https://i.imgur.com/xwTIxWs.png)

Example: sickness & medical tests
* Gender is a **symmetric** attribute
* fever, cough, tests are asymmetric
![](https://i.imgur.com/UWfgSMk.png)

in calculation
* ignore the symmetric attr. here
* Y or P is 1
* N is 0
![](https://i.imgur.com/Xs4v6WJ.png)

### Similarity
Jaccard coefficient : **similarity** for asymmetric binary variable
![](https://i.imgur.com/jLWLeaO.png)

## Proximity of Nominal Attributes 
for more variables
e.g. *red, yellow, blue...*

### Method 1 : Simpl