check DHCP devices
```bash
cat /tmp/dhcp.leases
```

check internet inferface
```bash
ifconfig
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