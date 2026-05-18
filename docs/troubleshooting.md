# Troubleshooting – Samba Active Directory

## Ziel
Sammlung typischer Fehler, Ursachen und Lösungen aus dem praktischen Aufbau
des Samba Active Directory Domain Controllers.
Diese Datei dient als Nachschlagewerk und Lernhilfe.

---

## DNS-Probleme (häufigste Fehlerquelle)

### Problem

kinit: KDC für Realm nicht gefunden

### Ursache

* Domain Controller nutzt externen DNS (z. B. Router/FritzBox)
* `/etc/resolv.conf` zeigt nicht auf den DC selbst

### Lösung

nameserver 127.0.0.1
search homelab.local

---

## Samba AD startet nicht

### Problem

samba-ad-dc.service: Condition failed

### Ursache

* `smbd`, `nmbd` oder `winbind` liefen parallel
* `smb.conf` war nur eine Beispiel-Datei
* Provisioning vor Installation von Samba

### Lösung

systemctl stop smbd nmbd winbind
systemctl disable smbd nmbd winbind

Provisioning ggf. erneut ausführen:

samba-tool domain provision ...

---

## Kerberos-Login schlägt fehl

### Problem

kinit: Passwort falsch

### Ursache

* Passwort inkonsistent (mehrfaches Provisioning)
* Tippfehler / falsches Tastaturlayout

### Lösung

samba-tool user setpassword administrator

Danach:

kinit administrator@HOMELAB.LOCAL

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

hostname -f
getent hosts dc01.homelab.local

---

## resolv.conf wird überschrieben

### Problem

Nach Neustart steht wieder externer DNS in `/etc/resolv.conf`

### Ursache

* NetworkManager oder DHCP überschreibt Resolver

### Lösung

chattr +i /etc/resolv.conf

---

## DNS-Warnungen beim Start von Samba

### Meldung

ERROR: Record already exists

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

