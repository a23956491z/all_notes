
# Homework

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

## 8.5
![](https://i.imgur.com/dNcYKm0.png)

## 8.11
![](https://i.imgur.com/0gXdj71.png)

## 8.12
![](https://i.imgur.com/QohmAjW.png)


## 8.15
![](https://i.imgur.com/7fr4ZtP.png)

## 8.16
![](https://i.imgur.com/SHOQI5y.png)

## 8.20
![](https://i.imgur.com/PXfKMZA.png)

## 8.23
![](https://i.imgur.com/oPQ86Dy.png)








