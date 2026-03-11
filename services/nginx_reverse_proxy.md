# Nginx Reverse Proxy

Server: app01.homelab.local

## Zweck

Der Reverse Proxy dient als zentraler Einstiegspunkt für interne Webservices.

Statt direkt auf einzelne Server zuzugreifen, werden Services über DNS-Namen
bereitgestellt und vom Reverse Proxy an die entsprechenden Backend-Server
weitergeleitet.

Beispiele:

gitea.homelab.local → srv01  
wiki.homelab.local → srv02  
grafana.homelab.local → mon01  

## Vorteile

- zentrale Zugriffsschicht
- einfache Erweiterung neuer Services
- bessere Übersicht der Infrastruktur
- Vorbereitung für TLS
- zentrales Logging

## Architektur

Client  
↓  
Reverse Proxy (app01)  
↓  
Backend Service

## Software

Nginx
