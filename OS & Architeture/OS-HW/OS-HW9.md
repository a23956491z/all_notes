# Homework

todo tick:
- [ ] 9.2
- [ ] 9.4
- [ ] 9.6
- [ ] 9.8
- [ ] 9.9
- [ ] 9.12
- [ ] 9.14
- [ ] 9.17
- [ ] 9.19
- [ ] 9.21


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

## 9.9
![](https://i.imgur.com/u1pWc0o.png)
![](https://i.imgur.com/XJUyPVE.png)
![](https://i.imgur.com/rFjN8mR.png)


## 9.12
![](https://i.imgur.com/sVNPzUo.png)

最常使用的page不代表使用時間最長，例如OS的每日定期更新，在更新期間，會非常頻繁地訪問特定pages，但是更新完後就不再訪問，這種情況就屬於 頻繁使用，但是使用時間不常，而LRU則是利用page的未使用時間來判斷，這種情況下用 MFU 的page fault率就更低。

## 9.14
![](https://i.imgur.com/9O1p8Bv.png)

## 9.17
![](https://i.imgur.com/f10VpQG.png)

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