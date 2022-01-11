# Operating System Homework chap.12
## 410821238 資工三 余慶龍



## 13.2
- Q: What are the ==advantages and disadvantages== of supporting **memory-mapped I/O** to device control registers?

Memory-mapped不需要和Port-mapped一樣使用額外的指令來存取I/O設備，可以直接將I/O設備映射到記憶體內，將I/O設備看成是Memory來使用

優點：
* 對I/O存取需求大的設備有幫助，例如顯卡
* 可以直接以DMA的方式存取資料，不需要使用額外的指令來傳入CPU內


缺點：
* 如果I/O和RAM在Memory中的邊界定義不清楚，就可能造成錯誤定位，修改到錯誤位置的資料
* Cache的設計會變得很麻煩，因爲RAM跟I/O設備都混在記憶體中了

## 13.5
- Q: What are the various kinds of performance overhead associated with **servicing an interrupt**?

利用Interrupt來跟I/O設備傳輸資料時，需要中斷CPU內的程序，流程如下：
1. 儲存原本執行中的Process狀態
2. 因爲Process被中斷：清空Pipeline上的指令
3. ..傳輸傳輸傳輸..
4. 恢復之前的Process狀態
5. 把之前的指令放回Pipeline

所以overhead會取決於：
* 儲存和回復Process的速度
* 清空和回復Pipeline的速度

## 13.6
- Q: Describe three circumstance under which blocking I/O should be used.


## 13.8
- Q: Some **DMA controllers** support **direct virtual memory access**, where the targets of I/O operations are specified as virtual addresses and **a translation from virtual to physical address** is performed **during the DMA**. ==How does this designed complicate the design of the DMA controller?== What are the **advantages** of providing such functionality?
