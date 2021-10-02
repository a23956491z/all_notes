---
tags : data-mining
---

# Data Similarity
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

### Method 1 : Simple matching
* $m$ : how many matches
* $p$ : how many variables
![](https://i.imgur.com/1fz7Ljx.png)

Example:
![](https://i.imgur.com/B6JMiI4.png)
![](https://i.imgur.com/zklid4P.png)

### Method 2 : Large number of binary attr
Create a **new binary attribute** for *each M nomial states*
* asymmetric

Example:
![](https://i.imgur.com/9MpJe87.png)
![](https://i.imgur.com/K5BnYxH.png)

## Distance on Numberic Data
### Metric
Must statify following properties
* Symmetry : $d(i,j)=d(j,i)$
* Triangle Inequality : $d(i,j)>0$ if $i \neq j$ and $d(i,i)=0$
* Positive definiteness : $d(i,j) \leq d(i,k) + d(k,j)$

### [[Minkowski Distance]]