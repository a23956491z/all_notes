# Operating System Homework chap.9
## 410821238 資工三 余慶龍

todo tick:
- [x] 9.2
- [x] 9.4
- [x] 9.6
- [x] 9.8
- [ ] 9.9
- [x] 9.12
- [x] 9.14
- [ ] 9.17
- [x] 9.19
- [x] 9.21


## 9.2
![](https://i.imgur.com/DM5RnZ2.png)

a. page fault 代表需要I/O操作來將page從硬碟讀取到記憶體，所以需要進入**block**狀態。

b. TLB missing時，到page table尋找address不需要太多時間，不需要切換狀態，可以繼續執行 (running)

c. 在TLB內尋找address需要的時間更少，也不需要切換狀態，繼續執行(running)



## 9.4
![](https://i.imgur.com/PNQPs0Q.png)

爲了共享虛擬記憶體，copy-on-write可以在process寫入時才復制，取代每個process復制一份，當我們大量讀取、而不寫入時，就可以減少很多的副本來節省空間。  

硬體上，TLB內需要標記那些目前是read only，並且持續計算有多少process需要使用，當有process需要寫入時，再復制一份出來並改成取消read only的標記。

## 9.6
![](https://i.imgur.com/IAS3YJB.png)

有empty frame或候選page沒被更動： 8ms  （$8*10^{-3}$）
候選page被更動過：20ms （$2*10^{-2}$）
記憶體存取：100ns （$1*10^{-7}$）

$200ns =2*10^{-7} s$

$1*(1-p)*10^{-7} + p * (0.3 * 3*10^{-3} + 0.7 * 2*10^{-2}) < 2 * 10^{-7}$
$(1-p) + p * (0.3 * 8*10^{4} + 0.7 * 2*10^{5}) < 2$
$(1-p) + p * (24000 + 140000) < 2$
$(1-p) + 164000*p < 2$
$163900*p < 1$
$p < 0.0000061..$



page fault的機率要低於0.006%

## 9.8
![](https://i.imgur.com/9ty23IN.png)

### LRU
<span style="color:tomato;">7，2，3：1</span>
<span style="color:green;">2，3，1：2</span>
<span style="color:tomato;">3，1，2：5</span>
<span style="color:tomato;">1，2，5：3</span>
<span style="color:tomato;">2，5，3：4</span>
<span style="color:tomato;">2，4，3：6</span>
<span style="color:tomato;">2，6，3：7</span>
<span style="color:green;">2，7，3：7</span>
<span style="color:tomato;">2，3，7：1</span>
<span style="color:tomato;">3，7，1：0</span>
<span style="color:tomato;">7，1，0：5</span>
<span style="color:tomato;">1，0，5：4</span>
<span style="color:tomato;">0，5，4：6</span>
<span style="color:tomato;">5，4，6：2</span>
<span style="color:tomato;">4，6，2：3</span>
<span style="color:tomato;">6，2，3：0</span>
<span style="color:tomato;">2，3，0：1</span>

18次page fault

### FIFO
<span style="color:tomato;">7，2，3：1</span>
<span style="color:green;">2，3，1：2</span>
<span style="color:tomato;">3，1，2：5</span>
<span style="color:tomato;">1，2，5：3</span>
<span style="color:tomato;">2，5，3：4</span>
<span style="color:tomato;">5，3，4：6</span>
<span style="color:tomato;">3，4，6：7</span>
<span style="color:green;">4，6，7：7</span>
<span style="color:tomato;">4，6，7：1</span>
<span style="color:tomato;">6，7，1：0</span>
<span style="color:tomato;">7，1，0：5</span>
<span style="color:tomato;">1，0，5：4</span>
<span style="color:tomato;">0，5，4：6</span>
<span style="color:tomato;">5，4，6：2</span>
<span style="color:tomato;">4，6，2：3</span>
<span style="color:tomato;">6，2，3：0</span>
<span style="color:tomato;">2，3，0：1</span>

18次page fault

### Optimal
<span style="color:tomato;">7，2，3：1</span>
<span style="color:tomato;">2，3，1：2</span>
<span style="color:tomato;">3，1，5：5</span>
<span style="color:green;">3，1，5：3</span>
<span style="color:tomato;">4，1，5：4</span>
<span style="color:tomato;">6，1，5：6</span>
<span style="color:tomato;">7，1，5：7</span>
<span style="color:green;">7，1，5：7</span>
<span style="color:green;">7，1，5：1</span>
<span style="color:tomato;">7，1，5：0</span>
<span style="color:green;">0，1，5：5</span>
<span style="color:tomato;">0，1，5：4</span>
<span style="color:tomato;">0，1，4：6</span>
<span style="color:tomato;">0，1，6：2</span>
<span style="color:tomato;">0，1，2：3</span>
<span style="color:green;">0，1，3：0</span>
<span style="color:green;">2，3，0：1</span>

14次 page fault

## 9.9
![](https://i.imgur.com/u1pWc0o.png)
![](https://i.imgur.com/XJUyPVE.png)
![](https://i.imgur.com/rFjN8mR.png)


## 9.12
![](https://i.imgur.com/sVNPzUo.png)

最常使用的page不代表使用時間最長，例如OS的每日定期更新，在更新期間，會非常頻繁地訪問特定pages，但是更新完後就不再訪問，這種情況就屬於 頻繁使用，但是使用時間不長，而LRU則是利用page的未使用時間來判斷，這種情況下用 MFU 的page fault率就更低。

相反地，如果使用的不頻繁，但是定期會使用一次，或是每次使用時間超長，例如linux的Daemon會一直在背景執行，造訪次數不一定多，但是可能會定期監控某些狀態，這種情況下，用最後參考時間來做替換的LRU就不會把這些背景process替換掉。

## 9.14
![](https://i.imgur.com/9O1p8Bv.png)

a. CPU利用率不會更高，可能更低，因爲原本需要CPU的資源可以更快速地執行完
b. 使用更大的 paging disk沒辦法提升CPU利用率，也不會改變 pageing disk的使用率
c. 增加multiprogramming degree會降低CPU使用率，因爲 paging的時間本來就多，代表每個process的frames可能不夠，更多的process再進來，只會使資源更加匱乏
d. 會增加CPU使用率，因爲每個process能用的Frame變多了，就可以減少swapping的次數
e. 增加CPU使用率，更大的記憶體就可以分配給process更多的Frame，同樣可以減少swapping的次數
f. 增加CPU使用率，更快的Disk可以讓swapping速度加快，降低 I/O 所造成的pending狀態
g. 略微增加CPU使用率，因爲disk的使用率本來就很高，Disk空閒下來讓CPU fetch的時間也會變得很少，不過仍然會增加CPU的使用率
h. 降低CPU使用率，增加page size會增大內外部碎片化的機率，使得本來就不夠用的memory/frames更加不夠用，進而需要增加swapping的次數

會提升CPU使用率： **d e f g**

## 9.17
![](https://i.imgur.com/f10VpQG.png)

### a.
i. counter初始值是0
ii. 每次被使用就會增加counter
iii. 隨時間減少counter
iv. 選擇counter最低的，換掉使用次數少的


### b.
| in  | value   | counter     |
| --- | ------- | ----------- |
| 1   |         |             |
| 2   | 1       | 1           |
| 3   | 1 2     | 0 1         |
| 4   | 1 2 3   | -1 0 1      |
| 5   | 1 2 3 4 | -2 -1 0 1   |
| 3   | 5 2 3 4 | 1 -2 0 0    |
| 4   |         | -2 -3 -1 0  |
| 1   | 5 2 3 4 | -3 -4 -2 -1 |
| 6   | 1 2 3 4 | 1 0 -4 -3   |
| 7   | 1 2 6 4 | 0 -1 1 -4   |
| 8   | 1 2 6 7 | -1 -2 0 1   |
| 7   | 1 8 6 7 | -2 1 -1 0   |
| 8   |         | -3 1 -2 -1  |
| 9   |         | 1 0 -3 -2   |
| 7   | 9 8 7 6 | 0 -1 -3 -3  |
| 8   |         | -1 -1 -4 -4 |
| 9   |         | -1 -2 -5 -5 |
| 5   |         | -2 -3 -6 -6 |
| 4   | 9 8 7 5 | -3 -4 -7 1  |
| 5   | 9 8 4 5 | -4 -5 1 0   |
| 4   |         | -5 -6 0 0   |
| 2   |         | -6 -7 0 -1  |

## 9.19
![](https://i.imgur.com/UoEWExD.png)

Thrashing源自process一直花時間進行paging
而需要一直paging代表 page fault rate很高
* 如果同時執行太多process，也就是multiprogramming degree很高的話，會使每個process能分到的frame變少，就需要一直頻繁訪問虛擬記憶體
* 在使用 Global replacement policy 來決定 swapping區塊時，有可能會導致process搶走其他process的Frame，造成其他process產生page fault
* 當 page fault rate上升，CPU 利用率會下降，在multiprogramming的環境下，OS會在載入更多process造成 page fault rate更高惡性循環。

## 9.21
![](https://i.imgur.com/HQ7UWZX.png)

window太小，一次性存入記憶體的資料也會很少，如果process需要很多資料時，就會一直閒置CPU來執行I/O操作，導致CPU利用率降低，而每次放入記憶體內的資料又很少，就需要更頻繁地操作，導致Thrashing