# Rollen und Server – Homelab

## Ziel
Übersicht über alle Server und Clients im Homelab,
inklusive ihrer Aufgaben und Verantwortlichkeiten.

---

## Serverübersicht

| Name | Betriebssystem | IP-Adresse | Rolle |
|-----|----------------|------------|-------|
| DC01 | Debian 12 | 192.168.56.7 | Samba Active Directory Domain Controller + DNS |
| APP01 | Debian 12 | 192.168.56.10 | Reverse Proxy / Web Gateway |

---

## DC01 – Domain Controller

**Aufgaben:**
- Zentrale Benutzer- und Gruppenverwaltung (Active Directory)
- Authentifizierung (Kerberos)
- Verzeichnisdienst (LDAP)
- DNS für die Domain
- Bereitstellung von SYSVOL und NETLOGON

**Besonderheiten:**
- Statische IP-Adresse
- Nutzt ausschließlich internen DNS
- Kein Routing, kein Gateway, keine Firewall-Funktion

---

## APP01 – Reverse Proxy / Web Gateway

Aufgaben:

- zentraler Zugriffspunkt für interne Webservices
- Weiterleitung von HTTP/HTTPS an Backend-Server
- Verwaltung von virtuellen Hosts
- Grundlage für zukünftige TLS-Termination

Typische Services hinter dem Proxy:

- gitea.homelab.local
- wiki.homelab.local
- grafana.homelab.local
- uptime.homelab.local

Software:

- Nginx

---

## Clients

### Windows Clients
- Windows 10 / 11
- Mitglied der Domain `HOMELAB.LOCAL`
- Anmeldung mit Domain-Benutzern
- Nutzung zentraler Ressourcen (Shares, Policies)

---

## Rollenkonzept

- **Domain Controller:** Identitäten, Authentifizierung, DNS
- **Server:** Dienste (z. B. Fileservices)
- **Clients:** Benutzerarbeitsplätze

Dieses Rollenkonzept trennt Verantwortlichkeiten
und entspricht gängigen Unternehmensstandards.

---
