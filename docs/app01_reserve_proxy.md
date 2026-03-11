# APP01 – Reverse Proxy

Der Server `app01` fungiert als zentraler Reverse Proxy für interne Webservices.

## Architektur

Client → DNS → Reverse Proxy → Backend Service

## Aktive Services

### Test Service

Hostname  
test.homelab.local

DNS  
test.homelab.local → 192.168.56.10

Nginx Proxy  
test.homelab.local → localhost:9000

Backend  
Python HTTP Server
python3 -m http.server 9000

### Portal

Hostname  
portal.homelab.local

DNS  
portal.homelab.local → 192.168.56.10

Nginx Proxy  
portal.homelab.local → localhost:9001

Backend  
Python HTTP Server
python3 -m http.server 900

## Nginx Struktur

Debian verwendet folgende Struktur für virtuelle Hosts:
/etc/nginx/
├─ nginx.conf
├─ sites-available/
│ ├─ test.homelab.local
│ └─ portal.homelab.local
└─ sites-enabled/
├─ test.homelab.local
└─ portal.homelab.local

Sites werden in `sites-available` definiert und über Symlinks in `sites-enabled` aktiviert.

## Konfigurationsänderungen

Die Standardseite wurde deaktiviert:
sudo rm /etc/nginx/sites-enabled/default

Nginx Konfiguration testen:
sudo nginx -t

Service neu laden:
sudo systemctl reload nginx

## Zweck

Der Reverse Proxy dient als zentraler Einstiegspunkt für Webservices im Homelab und ermöglicht:

- zentrale Zugriffskontrolle
- vereinheitlichte Hostnames
- spätere HTTPS Terminierung
- Weiterleitung an Backend Services
- einfache Erweiterung um weitere Dienste

## Aktueller Aufbau
Windows Client
│
▼
dc01 (AD + DNS)
│
▼
app01 (Nginx Reverse Proxy)
│
├─ test.homelab.local → localhost:9000
└─ portal.homelab.local → localhost:9001

