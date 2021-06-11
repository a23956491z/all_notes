Link Layer Services：
1. Error dectection、Correction
2. Link layer addressing
3. Multiple access(Broadcast)
4. Local area networks：Ethernet, VLANs

Nodes：hosts & router
Links：wired link & wireless & LANs
Frame：encapsulate datagram into frame

* Layer implemented：in HOST，網路卡(adaptor)

## Error detection
EDC : Error detection and Correction bits
D : Data 

* not 100% reliable

### Parity checking
1. single bit parity
2. ![](https://i.imgur.com/mTA5aJ9.png)

### CRC

r的數字可以自己訂，這裏 r=3

![](https://i.imgur.com/chBjCzl.png)

$D*2^r \oplus R$：
就是把R串在D後面而已

![](https://i.imgur.com/vH5Fduo.png)

做除法運算時
相減的部份，不需要借位和進位，只需要做XOR即可


