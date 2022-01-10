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

有empty frame或候選page 8ms 

## 9.8
![](https://i.imgur.com/9ty23IN.png)

## 9.9
![](https://i.imgur.com/u1pWc0o.png)
![](https://i.imgur.com/XJUyPVE.png)
![](https://i.imgur.com/rFjN8mR.png)


## 9.12
![](https://i.imgur.com/sVNPzUo.png)

## 9.14
![](https://i.imgur.com/9O1p8Bv.png)

## 9.17
![](https://i.imgur.com/f10VpQG.png)

## 9.19
![](https://i.imgur.com/UoEWExD.png)

## 9.21
![](https://i.imgur.com/HQ7UWZX.png)
