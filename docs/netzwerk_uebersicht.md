# Netzwerkübersicht – Homelab

## Ziel
Dokumentation der Netzwerkstruktur und der Aufgaben der einzelnen Komponenten.
Der Fokus liegt auf Verständlichkeit und realistischen Unternehmensstandards.

---

## Netzwerksegment

- Netzwerk: `192.168.56.0/24`
- Typ: internes Host-only Netzwerk (VirtualBox)
- Zweck: Kommunikation zwischen Servern und Clients im Homelab

Dieses Netzwerk ist vom Internet getrennt und dient ausschließlich
der internen Infrastruktur.

---

## Zentrales Gateway

- Gateway / Internetzugang:
  - VirtualBox NAT
  - bzw. physischer Router (z. B. FritzBox)

**Wichtig:**  
Der Domain Controller fungiert **nicht** als Gateway oder Router.

Clients greifen direkt über das Gateway auf das Internet zu.

---

## DNS-Konzept

- Zentraler DNS-Server: **DC01**
- DNS-Typ: Samba-integrierter AD-DNS
- DNS-IP für Domain-Mitglieder: `192.168.56.7`

Aufgaben des DNS:
- Auflösung von AD-Diensten (Kerberos, LDAP, DC)
- Bereitstellung von SRV-Records für Clients

Externe DNS-Anfragen werden bei Bedarf weitergeleitet (DNS-Forwarder).

---

## IP-Adressierung

| System | IP-Adresse | Typ |
|------|-----------|-----|
| DC01 | 192.168.56.7 | statisch |
| Clients | dynamisch oder statisch | DHCP / manuell |

Statische IPs werden für Server verwendet, um stabile Dienste zu gewährleisten.

---

## Kommunikation im Netzwerk

- Client ↔ Client:
  - Direkt über Switch / internes Netzwerk
- Client ↔ Server:
  - Über internes Routing (Layer 2 / Layer 3)
- Client ↔ Internet:
  - Über zentrales Gateway (nicht über DC01)

---

## Typische Fehlerquellen

- Falscher DNS-Server am Client
- Nutzung eines externen DNS auf dem Domain Controller
- Fehlende oder falsche statische IPs
- Zeitabweichungen (Kerberos)

---
