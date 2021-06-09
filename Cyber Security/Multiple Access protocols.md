## Links 的種類
1. 點對點(point-to-point)：Ethernet
2. 廣博(broadcast)：802.11 LAN


## Multiple Access protocols
決定不同node間如何共享channel

* 中央集控室分配資源
	single shared boradcast channel

* 碰撞(collision)：同時收到好幾個要求訊號


## Media Access Control(MAC)
1. Channel partitioning
2. random access
3. taking turns

### TDMA
Time Division Multiple Access

### Slotted ALOHA
random access protocols

Collision : node retransmits frame in each subsequent slot

* Pure(unslotted) ALOHA
	1. no synchronization
	2. collision probability increase


### CSMA
Carrier Sense Multiple Access

* Listen before transmit
* Collision ： 兩個node同時判斷網路可用(idle)


* CSMA/CD (with collision detection)
**Stop sending** after detect collision


* CSMA/CD (with collision avoiding)

### Taking turns MAC protocol
2 classes:
* polling : 每一個node都問，需要排隊
* token passing：有token的人可以傳資料，並把token傳下去