# Dokumentation Übung 6 
- Datum: 21.1.2022
- Name: René Luan Ottenburg
- [Link zur Aufgabenstellung](https://gitlab.com/ch-tbz-it/Stud/m129/-/tree/main/07_GNS3%20Labor%20Anforderungen#7-labor-6-labor-mit-zwei-router-nat-ins-internet-debian-client)

![GNS3 Screenshot meines Labors](images/gns3_wjFA6nqX6N.png)

## MikroTik Konfiguration
### Commands R1
```

/ip address
add address=192.168.23.20/24 interface=ether1 network=192.168.23.0
add address=192.168.255.1/30 interface=ether3 network=192.168.255.0

/ip dhcp-client
add interface=ether1
add interface=ether2

/ip firewall nat
add action=masquerade chain=srcnat out-interface=ether2

/ip route
add dst-address=192.168.46.0/24 gateway=192.168.255.2
```
### Commands R2
```
/ip pool
add name=dhcp_pool0 ranges=192.168.46.10-192.168.46.254

/ip dhcp-server
add address-pool=dhcp_pool0 interface=ether1 name=dhcp1

/ip address
add address=192.168.46.1/24 interface=ether1 network=192.168.46.0
add address=192.168.23.21/24 interface=ether2 network=192.168.23.0
add address=192.168.255.2/30 interface=ether3 network=192.168.255.0

/ip dhcp-client
add interface=ether1

/ip dhcp-server network
add address=192.168.46.0/24 gateway=192.168.46.1

/ip route
add dst-address=0.0.0.0/0 gateway=192.168.255.1
```
## Quellen
- https://help.mikrotik.com/

## Neue Lerninhalte
- NAT aufsetzten in Mikrotik

## Reflexion
Das NAT in Mikrotik ist sehr simpel. Ausserdem konnte ich das GUI für den Debian Client schnell herunterladen dadurch, dass ich den Computer direkt ans NAT angeschlossen habe.
