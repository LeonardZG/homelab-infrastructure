---

````md
# DC01 – Samba Active Directory

## Ziel
Dokumentation der Active-Directory-Implementierung mit Samba auf Debian.
Der Server stellt zentrale Identitäts-, Authentifizierungs- und DNS-Dienste bereit.

---

## Überblick

- AD-Implementierung: **Samba Active Directory**
- Server-Rolle: **Domain Controller**
- Domain (Realm): `HOMELAB.LOCAL`
- NetBIOS-Name: `HOMELAB`
- DNS-Backend: **Samba Internal DNS**
- Betriebssystem: Debian 12 (Bookworm)

Dieses Setup ersetzt funktional einen klassischen Windows Server
Active Directory Domain Controller.

---

## Kernkomponenten

### Active Directory
- Zentrale Verwaltung von:
  - Benutzern
  - Gruppen
  - Computern
- Einheitliche Authentifizierung im gesamten Netzwerk
- Grundlage für Rechte- und Zugriffskonzepte

---

### Kerberos
- Zuständig für sichere, ticketbasierte Authentifizierung
- Vergibt zeitlich begrenzte Tickets für Anmeldungen
- Extrem abhängig von:
  - korrektem DNS
  - korrekter Systemzeit

---

### LDAP
- Verzeichnisdienst für alle AD-Objekte
- Speicherung von:
  - Benutzern
  - Gruppen
  - Computern
  - Attributen (z. B. Gruppenmitgliedschaften)
- Wird von Clients und Servern zur Abfrage von Identitäten genutzt

---

### DNS (Samba-integriert)
- Verwaltung der Domain-Zone `homelab.local`
- Bereitstellung aller AD-relevanten DNS-Einträge
- Wichtige SRV-Records:
  - `_kerberos._udp.homelab.local`
  - `_ldap._tcp.homelab.local`

---

## Domain-Provisionierung

Die Domain wurde mit folgendem Befehl initial erstellt:

```bash
samba-tool domain provision \
  --realm=HOMELAB.LOCAL \
  --domain=HOMELAB \
  --server-role=dc \
  --dns-backend=SAMBA_INTERNAL \
  --use-rfc2307
````

### Begründung der wichtigsten Optionen

* `--server-role=dc`
  → Einrichtung eines Domain Controllers

* `--dns-backend=SAMBA_INTERNAL`
  → Nutzung des integrierten Samba-DNS-Servers

* `--use-rfc2307`
  → Vorbereitung für Linux-Clients (Unix-Attribute wie UID/GID)

---

## Dienste

### Aktiver Dienst

* `samba-ad-dc`

### Deaktivierte Dienste

* `smbd`
* `nmbd`
* `winbind`

**Begründung:**
Ein Samba Active Directory Domain Controller darf nicht parallel
als klassischer Samba-Dateiserver betrieben werden.

---

## Wichtige Konfigurationsdateien

* `/etc/samba/smb.conf`
  → Hauptkonfiguration des Samba AD DC

* `/var/lib/samba/`
  → AD-Datenbank, SYSVOL, interne Daten

* `/etc/krb5.conf`
  → Kerberos-Konfiguration (vom Provisioning erzeugt)

---

## Funktionstests

### Kerberos-Test

```bash
kinit administrator@HOMELAB.LOCAL
klist
```

Erwartung:

* Erfolgreiche Anmeldung
* Ticket für `krbtgt/HOMELAB.LOCAL`

---

### DNS-Test

```bash
host -t SRV _kerberos._udp.homelab.local
host -t SRV _ldap._tcp.homelab.local
```

Beide Abfragen müssen auf `dc01.homelab.local` zeigen.

---

### Samba-Tests

```bash
samba-tool domain level show
samba-tool user list
```

---

## Typische Fehlerquellen

* Nutzung eines externen DNS-Servers auf dem Domain Controller
* Zeitabweichungen zwischen Client und DC (Kerberos-Fehler)
* Parallel laufender `smbd`-Dienst
* Falscher Hostname oder FQDN
* Inkonsistente DNS- oder IP-Konfiguration

---
