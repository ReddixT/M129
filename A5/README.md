# Dokumentation Übung 5 
- Datum: 14.1.2022
- Name: René Luan Ottenburg
- [Link zur Aufgabenstellung](https://gitlab.com/ch-tbz-it/Stud/m129/-/tree/main/07_GNS3%20Labor%20Anforderungen#6-labor-5-labor-mit-zwei-router-und-dhcp-server)

![GNS3 Screenshot meines Labors](images\gns3_cvIpU3mkrr.png)

## Windows Konfiguration
```
Im CMD als Admin
route -p ADD 192.168.46.0 MASK 255.255.255.0 192.168.23.20
route -p ADD 192.168.47.0 MASK 255.255.255.0 192.168.23.41
```

## MikroTik Konfiguration
### Commands R1
```
/interface bridge
add name=bridge_vlan

/interface bridge port
add bridge=bridge_vlan interface=ether3
add bridge=bridge_vlan interface=ether4

/interface vlan
add interface=bridge_vlan name=vlan1 vlan-id=1

/ip pool
add name=dhcp_pool0 ranges=192.168.47.10-192.168.47.254

/ip dhcp-server
add address-pool=dhcp_pool0 interface=bridge_vlan name=dhcp1

/ip dhcp-server network
add address=192.168.47.0/24 gateway=192.168.47.1

/ip address
add address=192.168.47.1/24 interface=bridge_vlan network=192.168.47.0
add address=192.168.255.1/30 interface=ether2 network=192.168.255.0
add address=192.168.23.20/24 interface=ether1 network=192.168.23.0

/ip firewall address-list
add address=192.168.23.0/24 list=diable_ping_23

/ip firewall filter
add action=drop chain=forward dst-address=192.168.47.0/24 protocol=icmp src-address=192.168.23.0/24
```
### Commands R2
```
/interface bridge
add name=bridge_vlan

/interface bridge port
add bridge=bridge_vlan interface=ether3
add bridge=bridge_vlan interface=ether4

/interface vlan
add interface=bridge_vlan name=vlan1 vlan-id=1

/ip pool
add name=dhcp_pool0 ranges=192.168.47.10-192.168.47.254

/ip dhcp-server
add address-pool=dhcp_pool0 interface=bridge_vlan name=dhcp1

/ip dhcp-server network
add address=192.168.47.0/24 gateway=192.168.47.1

/ip address
add address=192.168.47.1/24 interface=bridge_vlan network=192.168.47.0
add address=192.168.255.2/30 interface=ether2 network=192.168.255.0
add address=192.168.23.21/24 interface=ether1 network=192.168.23.0
```
## VPC Konfiguration
### Commands PC1
```
dhcp
```
### Commands PC2
```
dhcp
```
### Commands PC3
```
dhcp
```
### Commands PC4
```
dhcp
```
## Quellen
- https://help.mikrotik.com/

## Neue Lerninhalte
- IP setzten mit Mikrotik
- DHCP Server aufsetzten mit Mikrotik
- Firewallrules setzten mit Mikrotik

## Reflexion
Ich habe nicht erwartet, dass Mikrotik so gut ist. Das beste an Mikrotik ist eigentlich deren help Seite, denn da steht ziemlich alles kurz und knapp und nicht wie bei Cisco sehr komplex. Das Problem mit dem DHCP Server aktivieren konnte ich nicht herrausfinden, weswegen ich auf Mikrotik wechselte.
