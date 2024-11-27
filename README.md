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
```
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
```

### LuminaSquare
```
#A3
route add -net 192.246.2.0 netmask 255.255.255.128 gw 192.246.2.195

#A7
route add -net 192.246.2.224 netmask 255.255.255.252 gw 192.246.2.217

#A8
route add -net 192.246.2.128 netmask 255.255.255.192 gw 192.246.2.217

#A9
route add -net 192.246.2.208 netmask 255.255.255.248 gw 192.246.2.217
```

### BalletTwins
```
#A4
route add -net 192.246.0.0 netmask 255.255.254.0 gw 192.246.2.193

#A7
route add -net 192.246.2.224 netmask 255.255.255.252 gw 192.246.2.193

#A8
route add -net 192.246.2.128 netmask 255.255.255.192 gw 192.246.2.193

#A9
route add -net 192.246.2.208 netmask 255.255.255.248 gw 192.246.2.193
```

### SixStreet
```
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
```

### OuterRing
```
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
```

### ScootOutpost
```
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
```