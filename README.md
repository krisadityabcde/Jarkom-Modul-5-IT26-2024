# Jarkom-Modul-5-IT26-2024
**Salsabila Rahmah (5027231005)** <br>
**Rafael Ega Krisaditya (5027231025)**
## Topologi Jaringan dan Pembagian Subnet
![Topologi Jaringan](./Topologi.jpg)

## Spreadsheet Pembagian IP Subnet
[Spreadsheet Pembagian IP Subnet](https://docs.google.com/spreadsheets/d/1RsyGUHDkX6PORwnmuhoLswWwZUOwpgX8823EpeLFQxM/edit?usp=sharing)

## Network Configuration
### NewEridu
```
#NAT
auto eth0
iface eth0 inet dhcp

#A1
auto eth1
iface eth1 inet static
	address 192.246.2.217
	netmask 255.255.255.252

#A5
auto eth2
iface eth2 inet static
	address 192.246.2.221
	netmask 255.255.255.252
```

### LuminaSquare
```
#A1
auto eth0
iface eth0 inet static
	address 192.246.2.218
	netmask 255.255.255.252
    gateway 192.246.2.217

#A2
auto eth1
iface eth1 inet static
	address 192.246.2.193
	netmask 255.255.255.248

#A4
auto eth2
iface eth2 inet static
	address 192.246.0.1
	netmask 255.255.254.0
```

### BalletTwins
```
#A2
auto eth0
iface eth0 inet static
	address 192.246.2.195
	netmask 255.255.255.248
    gateway 192.246.2.193

#A3
auto eth1
iface eth1 inet static
	address 192.246.2.1
	netmask 255.255.255.128
```

### SixStreet
```
#A5
auto eth0
iface eth0 inet static
	address 192.246.2.222
	netmask 255.255.255.252
    gateway 192.246.2.221

#A6
auto eth2
iface eth2 inet static
	address 192.246.2.201
	netmask 255.255.255.248

#A9
auto eth1
iface eth1 inet static
	address 192.246.2.209
	netmask 255.255.255.248
```

### ScootOutpost
```
#A6
auto eth0
iface eth0 inet static
	address 192.246.2.203
	netmask 255.255.255.248
    gateway 192.246.2.201

#A7
auto eth1
iface eth1 inet static
	address 192.246.2.225
	netmask 255.255.255.252
```

### OuterRing
```
#A6
auto eth0
iface eth0 inet static
	address 192.246.2.202
	netmask 255.255.255.248
    gateway 192.246.2.201

#A8
auto eth1
iface eth1 inet static
	address 192.246.2.129
	netmask 255.255.255.192
```

### HIA
```
auto eth0
iface eth0 inet static
	address 192.246.2.194
	netmask 255.255.255.248
    gateway 192.246.2.193
```

### HDD
```
auto eth0
iface eth0 inet static
	address 192.246.2.210
	netmask 255.255.255.248
    gateway 192.246.2.209
```

### Fairy
```
iface eth0 inet static
	address 192.246.2.211
	netmask 255.255.255.248
    gateway 192.246.2.209
```

### HollowZero
```
auto eth1
iface eth1 inet static
	address 192.246.2.226
	netmask 255.255.255.252
    gateway 192.246.2.225
```

### Client (Caesar, Burnice, Jane, Policeboo, Ellen, Lycaon)
```
auto eth0
iface eth0 inet dhcp
```

## .bashrc + routing
### NewEridu
```bash
#A2
route add -net 192.246.2.192 netmask 255.255.255.248 gw 192.246.2.218

#A3
route add -net 192.246.2.0 netmask 255.255.255.128 gw 192.246.2.218

#A4
route add -net 192.246.0.0 netmask 255.255.254.0 gw 192.246.2.218

#A7
route add -net 192.246.2.224 netmask 255.255.255.252 gw 192.246.2.222

#A8
route add -net 192.246.2.128 netmask 255.255.255.192 gw 192.246.2.222

#A9
route add -net 192.246.2.208 netmask 255.255.255.248 gw 192.246.2.222

#Otomasi iptables awal
IP_ETH0=$(ip -4 addr show eth0 | grep -oP '(?<=inet\s)\d+(\.\d+){3}')
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source $IP_ETH0
```

### LuminaSquare (DHCP Relay)
```bash
#A3
route add -net 192.246.2.0 netmask 255.255.255.128 gw 192.246.2.195

#A7
route add -net 192.246.2.224 netmask 255.255.255.252 gw 192.246.2.217

#A8
route add -net 192.246.2.128 netmask 255.255.255.192 gw 192.246.2.217

#A9
route add -net 192.246.2.208 netmask 255.255.255.248 gw 192.246.2.217

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.246.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### BalletTwins (DHCP Relay)
```bash
#A4
route add -net 192.246.0.0 netmask 255.255.254.0 gw 192.246.2.193

#A7
route add -net 192.246.2.224 netmask 255.255.255.252 gw 192.246.2.193

#A8
route add -net 192.246.2.128 netmask 255.255.255.192 gw 192.246.2.193

#A9
route add -net 192.246.2.208 netmask 255.255.255.248 gw 192.246.2.193

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.246.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### SixStreet (DHCP Relay)
```bash
#A2
route add -net 192.246.2.192 netmask 255.255.255.248 gw 192.246.2.221

#A3
route add -net 192.246.2.0 netmask 255.255.255.128 gw 192.246.2.221

#A4
route add -net 192.246.0.0 netmask 255.255.254.0 gw 192.246.2.221

#A7
route add -net 192.246.2.224 netmask 255.255.255.252 gw 192.246.2.203

#A8
route add -net 192.246.2.128 netmask 255.255.255.192 gw 192.246.2.202

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.246.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### OuterRing (DHCP Relay)
```bash
#A2
route add -net 192.246.2.192 netmask 255.255.255.248 gw 192.246.2.201

#A3
route add -net 192.246.2.0 netmask 255.255.255.128 gw 192.246.2.201

#A4
route add -net 192.246.0.0 netmask 255.255.254.0 gw 192.246.2.201

#A7
route add -net 192.246.2.224 netmask 255.255.255.252 gw 192.246.2.203

#A9
route add -net 192.246.2.208 netmask 255.255.255.248 gw 192.246.2.201

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt install isc-dhcp-relay -y

echo 'SERVERS="192.246.2.211"
INTERFACES="eth0 eth1 eth2 eth3"
OPTIONS=""
' > /etc/default/isc-dhcp-relay

echo 'net.ipv4.ip_forward=1' >> /etc/sysctl.conf

service isc-dhcp-relay restart
```

### ScootOutpost
```bash
#A2
route add -net 192.246.2.192 netmask 255.255.255.248 gw 192.246.2.201

#A3
route add -net 192.246.2.0 netmask 255.255.255.128 gw 192.246.2.201

#A4
route add -net 192.246.0.0 netmask 255.255.254.0 gw 192.246.2.201

#A8
route add -net 192.246.2.128 netmask 255.255.255.192 gw 192.246.2.202

#A9
route add -net 192.246.2.208 netmask 255.255.255.248 gw 192.246.2.201

echo 'nameserver 192.168.122.1' > /etc/resolv.conf
```

### Fairy (DHCP Server)
```bash
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install isc-dhcp-server -y

echo 'INTERFACES="eth0"' > /etc/default/isc-dhcp-server

echo '#A8
subnet 192.246.2.128 netmask 255.255.255.192 {
        range 192.246.2.130 192.246.2.190;
        option routers 192.246.2.129; # Gateway
        option broadcast-address 192.246.2.191;
        option domain-name-servers 192.246.2.210; #IP HDD
        default-lease-time 600;
        max-lease-time 7200;
}

#A4
subnet 192.246.2.0 netmask 255.255.254.0 {
        range 192.246.0.2 192.246.1.254;
        option routers 192.246.0.1;
        option broadcast-address 192.246.1.255;
        option domain-name-servers 192.246.2.210;
        default-lease-time 600;
        max-lease-time 7200;
}

#A3
subnet 192.246.2.0 netmask 255.255.255.128 {
        range 192.246.2.2 192.246.2.126;
        option routers 192.246.2.1;
        option broadcast-address 192.246.2.127;
        option domain-name-servers 192.246.2.210;
        default-lease-time 600;
        max-lease-time 7200;
}

subnet 192.246.2.216 netmask 255.255.255.252 {}
subnet 192.246.2.192 netmask 255.255.255.248 {}
subnet 192.246.2.220 netmask 255.255.255.252 {}
subnet 192.246.2.200 netmask 255.255.255.248 {}
subnet 192.246.2.224 netmask 255.255.255.252 {}
subnet 192.246.2.208 netmask 255.255.255.248 {}
' > /etc/dhcp/dhcpd.conf

service isc-dhcp-server restart
```

### HDD (DNS Server)
```bash
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install bind9 -y

echo 'options {
        directory "/var/cache/bind";

        forwarders {
                192.168.122.1;
        };

        // dnssec-validation auto;
        allow-query{any;};
        auth-nxdomain no;
        listen-on-v6 { any; };
}; ' >/etc/bind/named.conf.options

service bind9 restart
```

### HIA & HollowZero (Apache Worker)
```bash
echo 'nameserver 192.168.122.1' > /etc/resolv.conf
apt-get update
apt-get install apache2 -y

service apache2 start

echo '<?php
$hostname = gethostname();
echo "Welcome to $hostname";
?>' > /var/www/html/index.html

service apache2 restart
```

## Misi 2
1. Agar jaringan NewEridu terhubung ke internet menggunakan iptables tanpa MASQUERADE
```bash
iptables -t nat -A POSTROUTING -o eth0 -j SNAT --to-source [IP eth0]
```

2. 