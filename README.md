# homelab-infrastructure
Personal homelab infrastructure for learning and experimenting with Linux system administration, networking, monitoring and service deployment. Includes Active Directory, DNS, reverse proxy, monitoring stack and other infrastructure services.

---

## Current Infrastructure

The homelab currently contains a minimal Active Directory environment.

Components:

- Debian 12 server running Samba Active Directory
- Integrated DNS and Kerberos
- Windows client joined to the domain
- Internal network: 192.168.56.0/24 (VirtualBox host-only)

### Virtualization

- Virtualized lab environment
- Multiple Linux servers
- Windows client system

### Identity Management

- Samba Active Directory Domain Controller
- DNS and Kerberos integration
- Organizational Units and user management
- Windows client joined to the domain

### Networking

- Segmented lab network
- Host-only and NAT networking
- Domain-based name resolution

### Administration

- Linux CLI administration
- Windows RSAT tools
- Domain user and group management

---

## Documentation

Detailed documentation of the current infrastructure:

- [Network Overview](docs/network-overview.md)
- [Roles and Servers](docs/roles-and-servers.md)

---

## Planned Infrastructure Extensions

The following components will be added to simulate a more realistic service infrastructure:

- Reverse Proxy / Web Gateway
- Monitoring Stack (Prometheus + Grafana)
- Centralized Logging
- Database Server
- Automated Backups
- Service Deployment
- Alerting / Notifications

---

## Architecture Overview

(Architecture diagram will be added)

Example structure:

Internet  
│  
Reverse Proxy  
│  
Service Layer  
├ Application Services  
├ Monitoring  
├ Database  
└ Logging  

---

## Services (Planned)

### Reverse Proxy

Central entry point for internal services.

Possible technologies:

- NGINX
- Traefik

### Monitoring

Infrastructure monitoring and metrics collection.

Tools:

- Prometheus
- Grafana

### Logging

Centralized log aggregation for services and servers.

Possible stack:

- Loki
- ELK

### Database

Database services for internal applications.

Possible technologies:

- PostgreSQL
- MariaDB

### Backup System

Automated backup strategy for:

- system configuration
- databases
- service data

---

## Goals of this Homelab

This homelab is used to practice and demonstrate skills in:

- Linux system administration
- network services
- infrastructure design
- monitoring and observability
- service deployment
- troubleshooting and operations

---

## Future Improvements

- Infrastructure automation
- containerized services
- CI/CD pipelines
- infrastructure as code
