# DC01 – Netzwerk

## Ziel
Dokumentation der Netzwerkkonfiguration des Domain Controllers.
Eine korrekte Netzwerkkonfiguration ist entscheidend für DNS, Kerberos
und die Stabilität des Active Directory.

---

## Netzwerkinterfaces

| Interface | Zweck | Konfiguration |
|---------|------|---------------|
| enp0s8 | Internet (NAT) | DHCP |
| enp0s9 | Internes Netz (Host-only) | Statisch |

---

## IP-Adressierung

- Internes Netzwerk: `192.168.56.0/24`
- DC01 interne IP: `192.168.56.7`
- Gateway: **nicht gesetzt** auf dem internen Interface

**Begründung:**  
Der Domain Controller fungiert nicht als Router oder Gateway.

---

## Statische IP (Host-only)

Konfiguration in `/etc/network/interfaces`:

```ini
allow-hotplug enp0s9
iface enp0s9 inet static
  address 192.168.56.7/24
Statische IPs sind für Server notwendig, da sich AD-Dienste nicht auf wechselnde IPs verlassen dürfen.

## DNS-Konfiguration (kritisch)
DNS-Server: 127.0.0.1
DNS-Zone: homelab.local
/etc/resolv.conf:
nameserver 127.0.0.1
search homelab.local
Wichtig:
Ein Domain Controller darf keinen externen DNS nutzen,
da Kerberos den KDC über DNS-SRV-Records findet.
/etc/hosts
127.0.0.1       localhost
192.168.56.7   dc01.homelab.local dc01
Der FQDN muss immer auf die interne, statische IP zeigen.

## Typische Fehler & Ursachen
Fehler	Ursache
kinit: KDC not found	falscher DNS-Server
AD startet nicht	IP/DNS inkonsistent
Clients finden DC nicht	falsche SRV-Records
sporadische Login-Fehler	Zeitabweichung

## Tests
ip -br a
getent hosts dc01.homelab.local
host -t SRV _kerberos._udp.homelab.local
Alle Tests müssen die interne IP des DC zurückgeben.

## Merksatz
DNS ist das Fundament von Active Directory.
Eine falsche DNS-Konfiguration führt zwangsläufig
zu Authentifizierungs- und Verbindungsproblemen.

Speichern: **CTRL + O → Enter**  
Beenden: **CTRL + X**

---

## 3️⃣ Kurzcheck
```bash
cat dc01_netzwerk.md


