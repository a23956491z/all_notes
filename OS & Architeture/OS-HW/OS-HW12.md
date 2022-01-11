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

blocking vs non-blocking：
* Blocking的I/O傳輸在等待資料傳輸時，CPU會直接卡在I/O操作上，無法做其他事情，而Non-blocking類似於busy-waiting，會直接回傳資料的傳輸狀態，但是process需要一直詢問kernel資料傳好了沒。

什麼情況要用non-Blocking：
* 如果I/O設備很多（例如sockets），可以使用non-blocking來達到多工的效果（I/O multiplexing），每個設備輪流詢問CPU I/O的資料狀況，使得單一thread同時監控多個設備的作用，而不需要使用多個thread/process造成系統資源的浪費。
* 斷斷續續的資料傳輸（例如UDP協定的傳輸或串流），可以使用non-blocking來解決I/O設備不連續傳送的狀況，如果用 blocking，就會需要等到收到一份完整的資料（例如UDP封包）後，才會回傳狀態，這時CPU就會浪費很多時間在等待I/O設備發送資料。
* 用於實現資料同步，如果使用blocking來實現同步就會需要等待一個資料傳完，再傳下一個，此時可能其餘的I/O設備都是空閒的，所以可以使用non-blocking來實現多個來源的資料同步處理。


## 13.8
- Q: Some **DMA controllers** support **direct virtual memory access**, where the targets of I/O operations are specified as virtual addresses and **a translation from virtual to physical address** is performed **during the DMA**. ==How does this designed complicate the design of the DMA controller?== What are the **advantages** of providing such functionality?
