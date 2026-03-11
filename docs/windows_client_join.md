# Windows Client – Domain Join

## Ziel
Integration eines Windows-Clients in das Samba Active Directory
der Domäne HOMELAB.LOCAL.

## Umgebung
- Client OS: Windows 10 / 11 Pro
- Host: macOS (Apple Silicon)
- Virtualisierung: VirtualBox
- Netzwerk: Host-only (192.168.56.0/24)

## Netzwerkkonfiguration
- IP: 192.168.56.20
- DNS: 192.168.56.7 (DC01)
- Gateway: nicht gesetzt

## Domain Join
- Domäne: HOMELAB.LOCAL
- Erfolgreicher Beitritt nach DNS-Verifikation
- Neustart erforderlich

## Tests
- Domain-Login erfolgreich
- whoami → homelab\administrator
- nltest bestätigt DC01
- Anmeldung mit AD-Benutzer erfolgreich

## Ergebnis
Der Windows-Client ist vollständig in das Samba Active Directory
integriert und authentifiziert Benutzer zentral über DC01.

