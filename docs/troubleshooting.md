````md
# Troubleshooting – Samba Active Directory

## Ziel
Sammlung typischer Fehler, Ursachen und Lösungen aus dem praktischen Aufbau
des Samba Active Directory Domain Controllers.
Diese Datei dient als Nachschlagewerk und Lernhilfe.

---

## DNS-Probleme (häufigste Fehlerquelle)

### Problem
```text
kinit: KDC für Realm nicht gefunden
````

### Ursache

* Domain Controller nutzt externen DNS (z. B. Router/FritzBox)
* `/etc/resolv.conf` zeigt nicht auf den DC selbst

### Lösung

```bash
nameserver 127.0.0.1
search homelab.local
```

---

## Samba AD startet nicht

### Problem

```text
samba-ad-dc.service: Condition failed
```

### Ursache

* `smbd`, `nmbd` oder `winbind` liefen parallel
* `smb.conf` war nur eine Beispiel-Datei
* Provisioning vor Installation von Samba

### Lösung

```bash
systemctl stop smbd nmbd winbind
systemctl disable smbd nmbd winbind
```

Provisioning ggf. erneut ausführen:

```bash
samba-tool domain provision ...
```

---

## Kerberos-Login schlägt fehl

### Problem

```text
kinit: Passwort falsch
```

### Ursache

* Passwort inkonsistent (mehrfaches Provisioning)
* Tippfehler / falsches Tastaturlayout

### Lösung

```bash
samba-tool user setpassword administrator
```

Danach:

```bash
kinit administrator@HOMELAB.LOCAL
```

---

## Netzwerkprobleme

### Problem

* Clients finden den Domain Controller nicht
* DNS-Abfragen liefern falsche IPs

### Ursache

* Keine statische IP auf dem DC
* Falscher Eintrag in `/etc/hosts`
* Interface nicht aktiv

### Lösung

* Statische IP setzen
* FQDN prüfen:

```bash
hostname -f
getent hosts dc01.homelab.local
```

---

## resolv.conf wird überschrieben

### Problem

Nach Neustart steht wieder externer DNS in `/etc/resolv.conf`

### Ursache

* NetworkManager oder DHCP überschreibt Resolver

### Lösung

```bash
chattr +i /etc/resolv.conf
```

---

## DNS-Warnungen beim Start von Samba

### Meldung

```text
ERROR: Record already exists
```

### Erklärung

* DNS-Einträge existieren bereits
* Samba versucht sie erneut anzulegen

### Bewertung

* **Harmlos**
* Kein funktionaler Fehler

---

## Generelle Best Practices

* DNS immer zuerst prüfen
* Zeit-Synchronisation sicherstellen
* Dienste sauber trennen (DC ≠ File Server ≠ Gateway)
* Änderungen dokumentieren
* Nach stabilen Meilensteinen Snapshots erstellen

---

## Merksatz

90 % aller Active-Directory-Probleme
sind DNS- oder Zeitprobleme.

````

