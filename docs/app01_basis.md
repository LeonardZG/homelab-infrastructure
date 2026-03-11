# APP01 – Basisinstallation

## System

Hostname: app01  
FQDN: app01.homelab.local  
Betriebssystem: Debian 12

## Rolle

Application Gateway / Reverse Proxy für interne Services.

Der Server dient als zentraler Einstiegspunkt für Webservices im
Homelab und leitet HTTP/HTTPS Traffic an Backend-Server weiter.

## Netzwerk

Internes Netzwerk: 192.168.56.0/24

| Interface | Zweck | IP |
|-----------|------|----|
| enp0s8 | NAT (Internet) | DHCP |
| enp0s9 | Internes Homelab-Netz | 192.168.56.10 |

## DNS

DNS-Server: dc01.homelab.local

Der Server nutzt den Domain Controller als DNS-Server
für interne Namensauflösung.

## Status

Server installiert und erreichbar im internen Netzwerk.
Weitere Services werden später über diesen Server bereitgestellt.
