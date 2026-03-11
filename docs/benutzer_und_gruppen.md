```md
# Benutzer und Gruppen – Active Directory

## Ziel
Dokumentation des Benutzer-, Gruppen- und Rechtekonzepts im Samba
Active Directory.  
Das Ziel ist eine zentrale, nachvollziehbare und skalierbare Verwaltung
von Identitäten und Zugriffsrechten.

---

## Grundprinzip

Im Active Directory werden:
- **Benutzer** authentifiziert
- **Gruppen** zur Rechtevergabe genutzt
- **Ressourcen** (z. B. Fileserver) über Gruppen abgesichert

---

## Organisational Units (OU)

Empfohlene OU-Struktur:

```

HOMELAB.LOCAL
│
├── OU=Users
├── OU=Groups
├── OU=Computers
└── OU=Servers

```

**Vorteile:**
- Übersichtliche Struktur
- Vorbereitung für Gruppenrichtlinien (GPOs)
- Trennung von Objekttypen

---

## Benutzerkonten

### Beispiel-Benutzer

| Benutzername | Zweck |
|-------------|------|
| admin.it | IT-Administration |
| max.mustermann | Standard-Domain-User |
| test.user | Testzwecke |

**Grundsätze:**
- Keine Anmeldung mit dem Domain-Administrator im Alltag
- Klare Namenskonventionen
- Benutzer liegen in `OU=Users`

---

## Gruppen

### Gruppentypen

- **Security Groups**  
  → für Rechte & Zugriffskontrolle
- (Distribution Groups sind im Homelab nicht relevant)

---

### Beispiel-Gruppen

| Gruppe | Zweck |
|------|------|
| GRP_FS_READ | Leserechte auf Fileserver |
| GRP_FS_WRITE | Schreibrechte auf Fileserver |
| GRP_IT_ADMIN | Administrative Rechte |
| GRP_USERS | Standardbenutzer |

---

## Rechtekonzept (Best Practice)

**Prinzip:**
```

Benutzer → Gruppe → Ressource

````

Beispiel:
- Benutzer `max.mustermann`
- Mitglied in `GRP_FS_READ`
- Zugriff auf Fileserver-Freigabe mit Leserechten

**Vorteile:**
- Skalierbar
- Einfach wartbar
- Änderungen ohne Anpassung an Ressourcen

---

## Verwaltung

### Tools

- `samba-tool` (direkt auf dem DC)
- RSAT (Remote Server Administration Tools) auf Windows-Client

**Beispiel (CLI):**
```bash
samba-tool user create max.mustermann
samba-tool group add GRP_FS_READ
samba-tool group addmembers GRP_FS_READ max.mustermann
````

---

## Sicherheit

* Administrator-Konten sparsam einsetzen
* Passwortrichtlinien über AD
* Trennung von Benutzer- und Administrationskonten
* Logging über AD-Dienste

---

## Typische Fehler

* Rechte direkt an Benutzer vergeben
* Unstrukturierte OU-Hierarchie
* Nutzung des Domain-Admins für tägliche Arbeit
* Fehlende Namenskonventionen

---
