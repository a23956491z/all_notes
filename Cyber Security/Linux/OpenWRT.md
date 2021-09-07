# Tutorial

## 設備
使用設備：x86 PC
![](https://i.imgur.com/bSLokcQ.jpg)

![](https://i.imgur.com/ssKUVjg.jpg)

主板：ASRock H87 Pro4
CPU：Intel core i5-4440
RAM：ASint DDR3 2GB-1333
電源：靜音王？ 350W
SSD：Crucial M500 2.5 SSD 120GB
機殼：？
網卡：Intel i340-T4 Ethernet server adapter 1Gbps

### 機殼&主板
ASRock的H87 pro這塊板最大的缺點就是，只有一個PCIE x16，而ASUS的H87-pro就有兩個 PCIEx16 ，如果未來需要再加裝網卡的話，可能需要PCIEx4轉x1，或是PCIE轉PCI，就會比較麻煩。

而現在的PCI插槽也因爲頻寬不足，所以現代的擴展卡幾乎都沒辦法用（我想的到的），例如音效卡，無線網卡，m.2轉PCIE卡，擷取卡，幾乎都已經走PCIE界面了，更不用說頻寬更大的RAID陣列卡和有線網卡，像是Gigabyte級別（千兆）的單孔網卡，全雙工滿載時就已經到x64的PCI頻寬（266MB/s）的頂了，更不用說雙孔千兆甚至是萬兆網卡了。

電源則是自帶的一體式電源，所以線材長的有點奇葩。

### 風扇
除了後板自帶的風扇外，也在前板加上吸風的風扇幫助對流，
而CPU的負載率不高，也不會需要超頻，所以原廠風扇應該就綽綽有餘了。

### 儲存空間
路由器的系統可以存放在 隨身碟、HDD、SSD。

我一開始是選擇直接裝在隨身碟內，這樣其實相當省事，只要把系統img檔刷到隨身碟內，開機就可以直接用，不需要任何額外的安裝步驟，只是作爲需要24小時運行的路由器，隨身碟感覺還是有點不適合，除了穩定性問題外，沒特別分配空間的話，隨身碟內預設的可用空間會只有250MB供OpenWRT安裝軟體，這也是一個比較棘手的地方。

選用HDD也是可以的，只是一來我擔心HDD可能會造成效能瓶頸，二來是機殼硬碟架不見了，所以要加裝一顆HDD會麻煩不少，而且1TB的硬碟只使用10GB的空間感覺也是哪裏怪怪的，所以最好選擇100GB左右的SSD，裝在機殼的整線背板內，正面的空間也看起來乾淨整齊不少。

### 網路卡
![](https://i.imgur.com/i9awRXU.jpg)

![](https://i.imgur.com/WgERnt1.png)

這次使用的網路卡是二手版本的 intel的i340-T4，原價約US\$250，Amazon上也有二手價US\$170 ，不過我只用臺幣600左右就收到了，也算是相當幸運吧，而網路卡這種伺服器的零組件，通常都具有相當高的耐用性，而且即使損壞了，對系統的影響也不大，只需要更換一張就好，不像是硬碟的壽命那麼短，而且壞掉的處理流程麻煩許多，所以在這上面省錢也是可行的。

而等級更高的Intel i350 除了價位貴了不少外，其SR-IOV功能也更適合用在虛擬機上，而不是實體路由器，因爲這項技術可以直接讓虛擬機專享網卡中的其中一個port，而不是直接佔掉整個PCIE槽，算是一種相當實用的虛擬化解決方案。

而如果有更大的頻寬需求，HP 331T也算是CP值相當高的近2.5Gbps方案，而售價也比intel的產品便宜不少。

## 前置作業
需要一個 隨身碟，大小不限
並在裏面刷入一個輕量化的liveCD作業系統。可以用 Finnix（僅有400MB），不過我這裏用arch linux做範例。
制作可開機的隨身碟可以使用 rufus這個程式。

插上隨身碟開機後
可以利用 `ping 1.1.1.1`來測試網路狀態
利用 `ip addr`檢查網路卡是否有成功運作

![](https://i.imgur.com/usoOG0V.jpg)


## 下載openWRT並安裝
在下載之前，arch linux沒有內建下載的工具（wget）
所以我們需要先 用pacman 來安裝 wget
pacman 是arch linux自帶的套件管理工具
```bash
sudo pacman -Sy wget
```

然後就可以利用 wget來下載 openWRT的系統映像檔
可以去openWRT 的官方網站找自己需要的軔體來安裝
我這裏是使用 openWRT 21.02.0版本 x86/64 架構的 generic-ext4-combined檔案

```bash
wget https://downloads.openwrt.org/releases/21.02.0/targets/x86/64/openwrt-21.02.0-x86-64-generic-ext4-combined.img.gz
```
> * **squashfs-combined** 是傳統的openWRT配置，openWRT系統會存在唯讀(read-only)的squashfs檔案系統中，而另外會有230MB左右的可讀寫空間來安裝額外套件，**如果openWRT要run在隨身碟上，用這個比較好**
> * **ext4-combined**整塊都是可讀寫空間，要重新分配空間比較輕鬆，不過會把整塊硬碟清除。**如果openWRT要run在硬碟上，用這個比較好**

下載完之後， `ls`可以看目前目錄內的檔案
```bash
ls
```

再使用`gzip`解壓縮，打完open後，就可以按`TAB`自動補全名稱了，不需要把整串名字都打完
```bash
gzip -d openwrt-21.02.0-x86-64-generic-ext4-combined.img.gz
```
![](https://i.imgur.com/t64ToTF.jpg)

接着用 `lsblk` 列出硬碟與磁碟區
```bash
lsblk
```

可以看到 `sdb` 112.6G的磁碟，就是我們的隨身碟
而 `sda` 111.8G的磁碟是我們的SSD
![](https://i.imgur.com/ffTDzW2.png)

所以接着用 `dd`把剛剛的映像檔（軔體）裝到硬碟內
來源是剛剛解壓縮出來的那個檔案
目的地是我們的SSD `sda` （/dev/sda）
```bash
dd if=openwrt-21.02.0-x86-64-generic-ext4-combined.img of=/dev/sda
```

裝完後 `lsblk`可以看到 一個16MB的開機磁區，和104MB的系統磁區

## 分配額外空間
接下來我們要使用`fdisk`來分配剩下空間到系統磁區
fdisk 後面接要更改的磁碟，也就是SSD
```bash
fdisk /dev/sda
```

輸入 `p` 顯示目前的磁碟分割表
可以看到確實只有兩個磁區，一個16M，一個104M
然後這裏要把第二個磁區，104M的系統磁區的開始位置記下來，這裏是 *33792*
![](https://i.imgur.com/BQUsHQn.png)

輸入 `d` 刪除磁區
再輸入 `2`選擇刪除第二個磁區，也就是104M的系統磁區
輸入 `p` 顯示磁碟分割表，確認
![](https://i.imgur.com/NMTsz5T.png)

我們可以看到第二個磁區（/dev/sda2）確實不見了
輸入 `n` 新增磁區
輸入 `p` 選擇新增主要磁區
輸入 `2` 指定新磁區的編號爲2
這裏的 Fisrt Sector也就是磁區開始位置，填入剛剛的磁區開始位置，我的例子是 *33792*
Last Sector可以按空白，直接使用預設的，也就是**分配全部空間**
輸入 `N` 拒絕刪除原有的ext4磁碟簽章
![](https://i.imgur.com/00hAoew.png)

輸入 `p` 顯示磁碟分割表，確認，這裏可以看到第二個磁區變成 111.8G了
輸入 `w` 確認寫入剛剛的更動
![](https://i.imgur.com/RwLo2VP.png)

到這裏，安裝OpenWRT進硬碟的步驟就全部完成了
接着就可以關機，拔除隨身碟再開機了

## 設定 openWRT
開機後可以使用 `df`來檢查可用空間
```bash
df -h
```

![](https://i.imgur.com/c9Q5LfG.jpg)

可以看到 /dev/root的可用空間是 110.3G

`ifconfig` 可以看到我們有兩張網路界面，一張內建的網卡一張外接的
```bash
ifconfig
```
![](https://i.imgur.com/SjjODsJ.png)

用`ip addr`檢查網路界面和網路位置
可以看到有五個 eth的網路孔
可以從這裏看到 eth4是內建的網路卡，其他eth0~eth3是intel的網卡
因爲他們的MAC地址不同，eth4的MAC 是`bc:5f:f4:...` 其他的都是 `90:e2:ba:...`
```bash
ip addr
```
![](https://i.imgur.com/KRsSA9r.png)

用 `passwd`設定root的密碼
```bash
passwd
```
用 `ping`確認連線狀態
```bash
ping 1.1.1.1
```
![](https://i.imgur.com/6jAUyw2.png)

結果是沒有網路
所以需要指定一下 `WAN`跟`LAN`
用 `vim`編輯 `/etc/config/network`

我們剛剛得知， `eth4`是內建的網路卡，而網路供應商(ISP)出來的網路線，我是選擇插在內建的網卡上，所以`WAN`要分配到 `eth4`上
![](https://i.imgur.com/IxbbIOl.png)

白色的是網路供應商出來的網路線，黑色的是內網連接其他電腦的線
而我把 `eth0`~`eth3`都分配到 `LAN`，最後的 config file會長這樣
```bash
config interface 'loopback'
	option device 'lo'
	option proto 'static'
	option ipaddr '127.0.0.1'
	option netmask '255.0.0.0'
	
config globals 'globals'
	option ula_prefix 'fdc4:9196:705b::/48'
	
config interface 'lan'
	option ifname 'eth0 eth1 eth2 eth3'
	option proto 'static'
	option ipaddr '192.168.3.1'
	option netmask '255.255.255.0'
	option ip6assign '60'
	
config interface 'wan'
	option ifname 'eth4'
	option proto 'static'
	option ipaddr 'x.x.x.x'
	option netmask '255.255.255.0'
	option gateway 'x.x.x.x'
	option dns  '8.8.8.8'
	
```

也可以改成 lan bridge的方式
```bash
config device
	option name 'br-lan'
	option type 'bridge'
	list ports 'eth0 eth1 eth2 eth3'
	
config interface 'lan'
	option device 'br-lan'
	option proto 'static'
	option ipaddr '192.168.3.1'
	option netmask '255.255.255.0'
	option ip6assign '60'
```

最後`ping`一下，有網路就大功告成了
```bash
ping 1.1.1.1
```

接着只要在其他有連接到openWRT的電腦上
在瀏覽器輸入 openWRT的 `LAN`地址（上面的範例是 `192.168.3.1`，預設是`192.168.1.1`），就可以看到 openWRT的網頁管理界面了
密碼是剛剛上面自己用`passwd`設定的
![](https://i.imgur.com/JoxYxXz.png)

## 後話
![](https://i.imgur.com/KB8p2rM.png)

目前這臺路由器直連兩臺Server
不過這裏的設備當然遠不止4臺啦
所以之後會再把交換機（Switch）連到路由器上面
如果不計冗餘設計，隨便連4臺24port的交換機，也能讓路由器處理近百臺設備呢
而且以這個CPU和RAM，要處理這麼巨量的設備也應該沒問題


# 其他
check DHCP devices
```bash
cat /tmp/dhcp.leases
```


## Setting in SWITCH (VLAN)
802.1Q VLAN
* VLAN ID : 10, VLAN NAME : WAN
	* not member : port 3~8
	* tag (trunk) : port 1, 2
* VLAN ID : 1, VLAN NAME : LAN
	* not member : port 1
	* Untagged : port 2~8

802.1Q PVID setting
* port 1 : PVID 10

```bash
$ vi /etc/config/network
```
 
```bash
config interface 'wan'
	option ifname 'eth0.10'
	option proto 'static'
	option ipaddr '134.208.3.198'
	option netmask '255.255.255.0'
	option gateway '134.208.3.254'
	option dns  '8.8.8.8'
```

## Configure WIFI
MSI laptop example: Intel AC9560
Intel Wireless 8260


```bash
$ lspci
```

```bash
$ opkg update
$ opkg install pciutils
```

install firmware & driver on OpenWRT
```bash
$ opkg install ath10k-firware...
$ opkg install ath10k-ct
```

Enable WPA wifi security:
* install `hostapd`

## Benchmark
from inside wireless router to wired:
 134.208.3.184 (inside router) -> 134.208.3.186
 `58.9 Mbits/s`

wired to wired from switch:
134.208.3.198 -> 134.208.3.186
 `94.2 Mbits/s`
 
by wireless to wireless inside router LAN:
from 192.168.0.147 -> 192.168.0.150
`60.5 Mbits/s`



## OpenVPN
https://openwrt.org/docs/guide-user/services/vpn/openvpn/server
```bash
# Install packages
opkg update
opkg install openvpn-openssl openvpn-easy-rsa
 
# Configuration parameters
OVPN_DIR="/etc/openvpn"
OVPN_PKI="/etc/easy-rsa/pki"
OVPN_PORT="1194"
OVPN_PROTO="udp"
OVPN_POOL="192.168.8.0 255.255.255.0"
OVPN_DNS="${OVPN_POOL%.* *}.1"
OVPN_DOMAIN="$(uci get dhcp.@dnsmasq[0].domain)"
 
# Fetch WAN IP address
. /lib/functions/network.sh
network_flush_cache
network_find_wan NET_IF
network_get_ipaddr NET_ADDR "${NET_IF}"
OVPN_SERV="${NET_ADDR}"
 
```


```bash
# Configuration parameters
export EASYRSA_PKI="${OVPN_PKI}"
export EASYRSA_REQ_CN="ovpnca"
export EASYRSA_BATCH="1"
 
# Remove and re-initialize the PKI directory
easyrsa init-pki
 
# Generate DH parameters
easyrsa gen-dh
 
# Create a new CA
easyrsa build-ca nopass
 
# Generate a key pair and sign locally for a server
easyrsa build-server-full server nopass
 
# Generate a key pair and sign locally for a client
easyrsa build-client-full client nopass
 
# Generate TLS PSK
openvpn --genkey --secret ${OVPN_PKI}/tc.pem
```

```bash
# Configure firewall
uci rename firewall.@zone[0]="lan"
uci rename firewall.@zone[1]="wan"
uci del_list firewall.lan.device="tun+"
uci add_list firewall.lan.device="tun+"
uci -q delete firewall.ovpn
uci set firewall.ovpn="rule"
uci set firewall.ovpn.name="Allow-OpenVPN"
uci set firewall.ovpn.src="wan"
uci set firewall.ovpn.dest_port="${OVPN_PORT}"
uci set firewall.ovpn.proto="${OVPN_PROTO}"
uci set firewall.ovpn.target="ACCEPT"
uci commit firewall
/etc/init.d/firewall restart
```

```bash
# Configuration parameters
OVPN_DH="$(cat ${OVPN_PKI}/dh.pem)"
OVPN_TC="$(sed -e "/^#/d;/^\w/N;s/\n//" ${OVPN_PKI}/tc.pem)"
OVPN_CA="$(openssl x509 -in ${OVPN_PKI}/ca.crt)"
NL=$'\n'
 
# Configure VPN service and generate client profiles
umask go=
ls ${OVPN_PKI}/issued \
| sed -e "s/\.\w*$//" \
| while read -r OVPN_ID
do
OVPN_KEY="$(cat ${OVPN_PKI}/private/${OVPN_ID}.key)"
OVPN_CERT="$(openssl x509 -in ${OVPN_PKI}/issued/${OVPN_ID}.crt)"
OVPN_EKU="$(openssl x509 -in ${OVPN_PKI}/issued/${OVPN_ID}.crt -purpose)"
OVPN_CONF_SERVER="\ user nobody
group nogroup
dev tun
port ${OVPN_PORT}
proto ${OVPN_PROTO}
server ${OVPN_POOL}
topology subnet
client-to-client
keepalive 10 60
persist-tun
persist-key
push \"dhcp-option DNS ${OVPN_DNS}\"
push \"dhcp-option DOMAIN ${OVPN_DOMAIN}\"
push \"redirect-gateway def1\"
push \"persist-tun\"
push \"persist-key\"
<dh>${NL}${OVPN_DH}${NL}</dh>"
OVPN_CONF_CLIENT="\ dev tun
nobind
client
remote ${OVPN_SERV} ${OVPN_PORT} ${OVPN_PROTO}
auth-nocache
remote-cert-tls server"
OVPN_CONF_COMMON="\ <tls-crypt>${NL}${OVPN_TC}${NL}</tls-crypt>
<key>${NL}${OVPN_KEY}${NL}</key>
<cert>${NL}${OVPN_CERT}${NL}</cert>
<ca>${NL}${OVPN_CA}${NL}</ca>"
case ${OVPN_EKU} in
(*"SSL server : Yes"*) cat << EOF > ${OVPN_DIR}/${OVPN_ID}.conf ;;
${OVPN_CONF_SERVER}
${OVPN_CONF_COMMON}
EOF
(*"SSL client : Yes"*) cat << EOF > ${OVPN_DIR}/${OVPN_ID}.ovpn ;;
${OVPN_CONF_CLIENT}
${OVPN_CONF_COMMON}
EOF
esac
done
/etc/init.d/openvpn restart
ls ${OVPN_DIR}/*.ovpn
```

LUCI:
```bash
# Install packages
opkg update
opkg install luci-app-openvpn
/etc/init.d/rpcd restart
```
```bash
# Provide VPN instance management
ls /etc/openvpn/*.conf \
| while read -r OVPN_CONF
do
OVPN_ID="$(basename ${OVPN_CONF%.*} | sed -e "s/\W/_/g")"
uci -q delete openvpn.${OVPN_ID}
uci set openvpn.${OVPN_ID}="openvpn"
uci set openvpn.${OVPN_ID}.enabled="1"
uci set openvpn.${OVPN_ID}.config="${OVPN_CONF}"
done
uci commit openvpn
/etc/init.d/openvpn restart
```