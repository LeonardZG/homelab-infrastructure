# APP01 – Reverse Proxy

Der Server `app01` fungiert als zentraler Reverse Proxy für interne Webservices.

## Architektur

Client → DNS → Reverse Proxy → Backend Service

## Beispiel Service

Hostname:
test.homelab.local

DNS:
test.homelab.local → 192.168.56.10

Nginx Proxy:
test.homelab.local → localhost:9000

## Zweck

Der Reverse Proxy dient als zentraler Einstiegspunkt für Webservices
im Homelab und ermöglicht:

- zentrale Zugriffskontrolle
- vereinheitlichte Hostnames
- spätere HTTPS Terminierung
- Weiterleitung an Backend Services
