
# Homework

todo tick:
- [x] 8.1
- [x] 8.3
- [x] 8.4
- [x] 8.5
- [ ] 8.11
- [x] 8.12
- [x] 8.15
- [ ] 8.16
- [x] 8.20
- [ ] 8.23

## 8.1
![](https://i.imgur.com/7R81JRg.png)

內部破碎和外部破碎的內外是對於 process而言
process外的破碎就叫外部破碎
* 連續的記憶體空間不夠分配給其他process，造成記憶體碎片化，而且這些碎片也無法使用
process內的破碎即內部破碎
* process被分配到的記憶體過多，不需要這麼多資源，而其他prcess也無法存取這些資源

## 8.3
![](https://i.imgur.com/eIGzXIj.png)

### Fisrt-fit
with avaliable list:

| Space(KB) | allocated(KB) | iteration |
|:---------:|:-------------:|-----------|
|    300    |      115      | 1         |
|    600    |      500      | 1         |
|    350    |      200      | 1         |
|    200    |               |           |
|    700    |      358      | 1         |
|    125    |               |           |
| no space  |      375      | 2         |
| total     |      1173     | 6         |

總共分配：1173 KB，只需要 6次iteration
* 效率最好、空間利用率最大

### best-fit:
with avaliable list:

| Space(KB) | allocated(KB) | iteration |
|:---------:|:-------------:| --------- |
|    300    |               |           |
|    600    |      500      | 5         |
|    350    |               |           |
|    200    |      200      | 3         |
|    700    |      358      | 4         |
|    125    |      115      | 6         |
| no space  |      375      | 2         |
|   total   |     1173      | 20        |

if we sort it first

| Space(KB) | allocated(KB) | iteration |
|:---------:|:-------------:|-----------|
|    125    |      115      | 2         |
|    200    |      200      | 2         |
|    300    |               |           |
|    350    |               |           |
|    600    |      500      | 5         |
|    700    |      358      | 4         |
| no space  |      375      | 2         |
| total     |      1173     | 15        |

總共分配：1173 KB，沒排序需要20次，排序後15次
* 效率中等，空間利用率最大

### worst-fit:
with avaliable list:

| Space(KB) | allocated(KB) | iteration |
|:---------:|:-------------:| --------- |
|    300    |               |           |
|    600    |      500      | 5         |
|    350    |      200      | 4         |
|    200    |               |           |
|    700    |      115      | 6         |
|    125    |               |           |
| no space  |   358, 375    | 4+3       |
|   total   |      815      | 22        |

if we sort it first:

| Space(KB) | allocated(KB) | iteration |
|:---------:|:-------------:|-----------|
|    125    |               |           |
|    200    |               |           |
|    300    |               |           |
|    350    |      200      | 1         |
|    600    |      500      | 1         |
|    700    |      115      | 1         |
| no space  |    358, 375   | 4+3       |
| total     |      815      | 10        |

總共分配：815 KB，沒排序需要22次，排序後10次
* 排序後效率接近最好，空間利用率最小
* 沒排序的效率則最差

空間利用率： $\textrm{best-fit} = \textrm{first-fit} > \textrm{worst-fit}$
未排序效率： $\textrm{first-fit} > \textrm{best-fit} > \textrm{worst-fit}$
已排序效率： $\textrm{first-fit} > \textrm{worst-fit} > \textrm{best-fit}$

## 8.4
![](https://i.imgur.com/Tfd4Rof.png)

* 連續記憶體分配：需要，否則需要更多空間時，要重新分配整個程式的記憶體空間
* 純segmentation：需要，單一sementation內的記憶體用完就沒了，也要分配一個更大的segmentation替代
* 純paging：**不需要額外的dynamic memory allocation**，page本身的機制就支援分配新的page，而不需要重新分配舊的空間


## 8.5
![](https://i.imgur.com/dNcYKm0.png)

| Memory allocation |              External fragmentation             | Internal fragmentation                    | Share Code                          |
|:-----------------:|:-----------------------------------------------:|-------------------------------------------|-------------------------------------|
|    Contiguous     |  會發生，因爲到後面連續的大塊記憶體會越來越少   | 會發生，有些process有資源過剩的情況       | 無法，每個process會有一份code的副本 |
| Pure Segmentation |       會，Segmentation也是一塊塊連續記憶體      | 會，limit邊界無法自由調整，分配完就固定了 | 可以，藉由共用單一segmentation      |
|    Pure Paging    | 不會發生，Page size夠小，可以完整利用整個記憶體 | 幾乎不會產生，因爲每個page的大小都很小    | 可以，藉由共用單一frame             |

## 8.11
![](https://i.imgur.com/0gXdj71.png)

## 8.12
![](https://i.imgur.com/QohmAjW.png)

$1KB = 1024 byte= 2^{10} byte$
一個offset由 10 個 bits 組成
* 除以 page size 的商即是 page number
* 除以 page size 的餘即是 page offset

### a. 3085
$3085 \div 1024 = 3 \ldots 13$

* page number = **0**
* page offset = **3085**

### b. 42095
$42095 \div 1024 = 41 \ldots 111$

* page number = **10**
* page offset = **111**

### c.215201
$215201 \div 1024 = 210 \ldots 161$

* page number = **210**
* page offset = **161**

### d.650000
$650000 \div 1024 = 634 \ldots 784$

* page number = **634**
* page offset = **784**

### e.2000001
$650000 \div 1024 = 1953 \ldots 129$

* page number = **1953**
* page offset = **129**


## 8.15
![](https://i.imgur.com/7fr4ZtP.png)

64 frames = $2^6$ frames
256 pages = $2^8$ pages
4 KB page size = $2^{12}$ byte 

### a. bits for logical addr
total bits for logical address : 8+12 =  **20 bits**

### b. bits for physical addr
total bits for physical address : 6+12 = **18 bits**

## 8.16
![](https://i.imgur.com/SHOQI5y.png)

## 8.20
![](https://i.imgur.com/PXfKMZA.png)

### a. 0,430



219 + 430 = 649
ans: 649

### b. 1,10

2300 + 10=2310
ans: 2310

### c. 2,500

500 > limit
ans: illegal address，trap

### d. 3,400

1327+400 = 1727
ans: 1727
### e. 4,112

112 > 96
ans: illegal address, trap

## 8.23
![](https://i.imgur.com/oPQ86Dy.png)

segmented paging vs hashed page table


