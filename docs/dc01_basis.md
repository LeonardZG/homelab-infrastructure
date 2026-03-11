# DC01 – Basisinformationen

## Ziel
Dokumentation der grundlegenden Systemparameter des Domain Controllers (DC01).
Diese Basis ist Voraussetzung für einen stabilen Betrieb von Samba AD.

---

## System

- Hostname: `dc01`
- FQDN: `dc01.homelab.local`
- Betriebssystem: Debian 12 (Bookworm)
- Architektur: arm64
- Virtualisierung: VirtualBox (macOS Host)

---

## Benutzer & Zugriff

- Initiale Administration erfolgt als `root`
- SSH-Zugriff aktiv
- Spätere Erweiterung möglich:
  - zusätzlicher Admin-User
  - sudo-Konzept

**Begründung:**  
Für die Initialinstallation ist der direkte Root-Zugriff üblich.
Im laufenden Betrieb wird mit eingeschränkten Rechten gearbeitet.

---

## Zeit & Synchronisation

- Zeitzone: Europe/Berlin
- NTP aktiv (chrony)
- Zeit-Synchronisation ist zwingend erforderlich für Kerberos

---

## Netzwerk-Grundlagen

- Internes Netzwerk: `192.168.56.0/24`
- Statische IP-Adresse: `192.168.56.7`
- DNS zeigt auf den lokalen Domain Controller (`127.0.0.1`)

Der DC nutzt ausschließlich seinen eigenen DNS,
um AD- und Kerberos-Dienste zuverlässig bereitzustellen.

---

## Wichtige Konfigurationsdateien

- `/etc/hostname`
- `/etc/hosts`
- `/etc/network/interfaces`
- `/etc/resolv.conf`
- `/etc/krb5.conf`

---
