# homelab-infrastructure

Private Homelab-Infrastruktur zum Lernen und Experimentieren im Bereich Linux-Systemadministration, Netzwerktechnik, Monitoring sowie Service-Deployment.  
Die Umgebung bildet typische IT-Infrastruktur in kleinem Maßstab nach und umfasst Active Directory, DNS, Reverse Proxy, Monitoring sowie weitere zentrale Dienste.

---

## Aktuelle Infrastruktur

Die aktuelle Umgebung besteht aus einer grundlegenden Active-Directory-Infrastruktur auf Basis von Samba auf Debian.

### Kernkomponenten

- Debian 12 Server mit Samba Active Directory Domain Controller  
- Integrierter DNS- und Kerberos-Dienst  
- Windows-Client, der der Domäne beigetreten ist  
- Internes Labornetzwerk (192.168.56.0/24, VirtualBox Host-Only)

---

## Infrastruktur-Komponenten

### Virtualisierung

- VirtualBox-basierte Laborumgebung  
- Linux-Server-Infrastruktur  
- Windows-Client-Systeme  

---

### Identity & Access Management

- Samba Active Directory Domain Controller  
- Domain: homelab.local  
- Kerberos-basierte Authentifizierung  
- LDAP-Verzeichnisdienste  
- Benutzer- und Gruppenverwaltung  

---

### Netzwerk

- Segmentiertes Labornetzwerk  
- Host-Only internes Netzwerk  
- NAT-Schnittstelle für externen Zugriff  
- DNS-Auflösung über Domain-Infrastruktur  

---

### Administration

- Linux-Systemadministration über CLI  
- Verwaltung über Windows RSAT-Tools  
- Domain-User- und Gruppenverwaltung  

---

## Domain Controller (DC01)

- Grundsystem und Netzwerkkonfiguration  
- Samba Active Directory Konfiguration  
- DNS- und Kerberos-Integration  
- Windows-Client-Domain-Join  

---

## Client Integration

- Windows Client im Active Directory eingebunden  
- Testumgebung für Benutzer- und Rechteverwaltung  

---

## Troubleshooting & Betrieb

- Analyse und Behebung von Samba-AD-Problemen  
- Netzwerkdiagnose  
- Active Directory Debugging und Fehleranalyse  

---

## Infrastruktur-Erweiterungen (geplant / in Arbeit)

Die Umgebung wird schrittweise zu einer realistischeren Service-Infrastruktur ausgebaut:

- Reverse Proxy / Web Gateway (bereits integriert)  
- Monitoring Stack (Prometheus + Grafana)  
- Zentrales Logging  
- Datenbankserver  
- Automatisierte Backup-Lösung  
- Service-Deployment-Mechanismen  
- Alerting & Benachrichtigungssysteme  

---

## Architekturübersicht

(Architekturdiagramm wird ergänzt)

---

## Services

### Reverse Proxy / Web Gateway

Zentraler Einstiegspunkt für interne und externe Services.

**Mögliche Technologien:**
- NGINX
- Traefik

---

### Monitoring

Überwachung von Infrastruktur und Systemmetriken.

**Tools:**
- Prometheus
- Grafana

---

### Logging

Zentrale Log-Aggregation für Systeme und Services.

**Stacks:**
- Loki
- ELK Stack

---

### Datenbank

Bereitstellung von Datenbankdiensten für interne Anwendungen.

**Technologien:**
- PostgreSQL
- MariaDB

---

### Backup-System

Automatisierte Backup-Strategie für:

- Systemkonfigurationen  
- Datenbanken  
- Servicedaten  

---

## Ziele der Homelab-Infrastruktur

Diese Homelab-Umgebung dient der praxisnahen Entwicklung von Fähigkeiten in:

- Linux-Systemadministration  
- Netzwerkadministration  
- Infrastrukturdesign  
- Monitoring und Observability  
- Service-Betrieb und Deployment  
- Fehleranalyse und Troubleshooting  

---

## Zukünftige Verbesserungen

- Infrastructure as Code (Ansible / Terraform)  
- Containerisierte Services (Docker / Kubernetes)  
- CI/CD-Pipelines  
- Automatisierung von Deployments  
- Erweiterung der Service-Landschaft  
