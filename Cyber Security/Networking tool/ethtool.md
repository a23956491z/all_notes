
speed above 1 gbps : **autoneg are required**
if set autoneg to off, it won't work!
```bash
sudo ethtool --change  enp3s0 autoneg on speed 1000 duplex full
```