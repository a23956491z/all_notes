# Operating System Homework chap.12
## 410821238 資工三 余慶龍



## 13.2
- Q: What are the ==advantages and disadvantages== of supporting **memory-mapped I/O** to device control registers?

Memory-mapped不需要和Port-mapped一樣使用額外的指令來存取I/O設備，可以直接將I/O設備映射到記憶體內，將I/O設備看成是Memory來使用

優點：
* 對I/O存取需求大的設備有幫助，例如顯卡
* 可以直接以DMA的方式存取資料，不需要使用額外的指令來傳入CPU內
* 可以使用其他的神奇Memory技巧、例如page table等等

缺點：
* 如果I/O和RAM在Memory中的邊界定義不清楚，就可能造成錯誤定位，修改到錯誤位置的資料

## 13.5
- Q: What are the various kinds of performance overhead associated with **servicing an interrupt**?


## 13.6
- Q: Describe three circumstance under which blocking I/O should be used.


## 13.8
- Q: Some **DMA controllers** support **direct virtual memory access**, where the targets of I/O operations are specified as virtual addresses and **a translation from virtual to physical address** is performed **during the DMA**. ==How does this designed complicate the design of the DMA controller?== What are the **advantages** of providing such functionality?
