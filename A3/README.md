# Dokumentation Übung 2 
- Datum: 03.12.2021
- Name: René Luan Ottenburg
- [Link zur Aufgabenstellung](https://gitlab.com/ch-tbz-it/Stud/m129/-/tree/main/07_GNS3%20Labor%20Anforderungen#4-labor-3-ping-%C3%BCber-router-3-subnetze-und-lokalem-pc)

![GNS3 Screenshot meines Labors](images\gns3_P2UYCK7UI9.png)

## Windows Konfiguration
```
Im CMD als Admin
route -p ADD 192.168.21.0 MASK 255.255.255.0 192.168.23.24
route -p ADD 192.168.11.0 MASK 255.255.255.0 192.168.23.24
```

## Cisco Konfiguration
### Commands R2
```
enable
config t
    int f0/0
        ip add 192.168.255.1 255.255.255.0
        no shut 
    exit
    int e4/0
        ip add 192.168.11.1 255.255.255.0
        no shut 
    exit
    int e4/1
        ip add 192.168.23.24 255.255.255.0
        no shut 
    exit
    ip route 192.168.21.0 255.255.255.0 192.168.255.2
exit
```
### Commands R3
```
enable
config t
    int f0/0
        ip add 192.168.255.2 255.255.255.0
        no shut 
    exit
    int e4/0
        ip add 192.168.21.1 255.255.255.0
        no shut 
    exit
    ip route 192.168.11.0 255.255.255.0 192.168.255.1
    ip route 192.168.23.0 255.255.255.0 192.168.255.1
exit
```

## VPC Konfiguration
### Commands PC4
```
ip 192.168.11.10 255.255.255.0 192.168.11.1
```
### Commands PC5
```
ip 192.168.21.10 255.255.255.0 192.168.21.1
```

## Quellen
- https://www.howtogeek.com/howto/windows/adding-a-tcpip-route-to-the-windows-routing-table/

## Neue Lerninhalte
- 

## Reflexion
Ich machte eine solche Übung schonmals mit 2 Netzwerken welche über 2 Router verbunden sind, weswegen mir die Aufgabe leicht gefallen ist. Als Repetition konnte ich die Übung gut gebrauchen.
