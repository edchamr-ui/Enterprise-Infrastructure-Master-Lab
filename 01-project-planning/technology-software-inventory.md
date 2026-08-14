# BETELGEUSE INFRA (PVT) LTD

# Technology & Software Inventory

| Document Information   | Details                              |
| ---------------------- | ------------------------------------ |
| Project                | Enterprise Infrastructure Master Lab |
| Client                 | Apex Manufacturing (Private) Limited |
| Implementation Partner | Betelgeuse Infra (Pvt) Ltd           |
| Document Owner         | Edmond Chamunorwa                    |
| Version                | 1.0                                  |
| Status                 | Draft                                |
| Classification         | Internal                             |

---

# 1. Purpose

This document defines the primary technologies, platforms and software components selected for the Enterprise Infrastructure Master Lab.

The inventory provides a central reference for the technologies that will be used throughout the design, implementation, testing, monitoring, automation and operation of the enterprise infrastructure.

---

# 2. Network Emulation

## EVE-NG Community Edition

**Purpose:** Enterprise network emulation platform.

EVE-NG will provide the virtual environment used to deploy and interconnect routers, switches, firewalls and data-centre networking appliances.

Primary use cases include:

* Campus network simulation
* Enterprise routing
* Branch networking
* WAN simulation
* Firewall integration
* BGP
* OSPF
* Data-centre networking
* VXLAN / EVPN

---

# 3. Enterprise Routing

## Cisco vIOS Router

**Purpose:** Enterprise routing platform.

The Cisco virtual router platform will be used for:

* Static routing
* OSPF
* BGP
* WAN connectivity
* Branch routing
* Internet edge simulation
* Route redistribution
* Route filtering
* Traffic engineering

---

# 4. Enterprise Switching

## Cisco vIOS L2 Switch

**Purpose:** Enterprise campus switching.

The switching platform will provide:

* VLANs
* 802.1Q trunking
* Spanning Tree
* EtherChannel
* Access switching
* Port security
* DHCP Snooping
* Dynamic ARP Inspection

---

# 5. Data Centre Networking

## Cisco Nexus 9300v

**Purpose:** Data-centre switching and overlay networking.

The Nexus platform will be used to implement:

* Spine-Leaf architecture
* Layer 3 underlay
* BGP
* MP-BGP EVPN
* VXLAN
* VNI mappings
* VTEPs
* Anycast gateways

---

# 6. Enterprise Firewall

## FortiGate VM

**Purpose:** Primary enterprise security gateway.

FortiGate will provide:

* Firewall policies
* Network Address Translation
* High Availability
* IPSec VPN
* Remote-access VPN
* Network segmentation
* Application control
* Intrusion prevention
* Web filtering
* Security logging
* SD-WAN

---

# 7. Secondary Firewall Platform

## pfSense Community Edition

**Purpose:** Secondary firewall and routing platform.

pfSense will be used for selected comparative exercises involving:

* Firewall policies
* NAT
* Routing
* VPN connectivity
* Network segmentation

---

# 8. Virtualisation

## VMware Workstation Pro

**Purpose:** Primary host virtualisation platform.

VMware Workstation Pro will host:

* EVE-NG
* Windows Server
* Windows clients
* Linux servers
* Monitoring platforms
* Security platforms
* Automation servers
* Storage appliances

## VMware ESXi

**Purpose:** Enterprise hypervisor simulation.

ESXi will be used during the server-farm phase to demonstrate enterprise virtualisation concepts.

## VMware vCenter

**Purpose:** Centralised VMware infrastructure management.

Where host resources permit, vCenter will be used to demonstrate:

* Centralised host management
* Virtual machine management
* Clustering
* High availability
* vMotion concepts

---

# 9. Microsoft Infrastructure

## Windows Server 2022

**Purpose:** Enterprise Microsoft infrastructure services.

Windows Server will provide:

* Active Directory Domain Services
* DNS
* DHCP
* Group Policy
* Identity management
* Authentication
* File services
* Certificate services where applicable

## Windows 11

**Purpose:** Enterprise endpoint simulation.

Windows 11 clients will be used to test:

* Domain membership
* User authentication
* Group Policy
* DNS
* DHCP
* File services
* Enterprise application access

---

# 10. Linux Infrastructure

## Ubuntu Server 24.04 LTS

**Purpose:** Primary Linux server platform.

Ubuntu Server will support:

* Web services
* Automation
* Monitoring
* Containers
* Network tools
* Infrastructure management

## Rocky Linux 9

**Purpose:** Enterprise Linux platform.

Rocky Linux will provide experience with a Red Hat-compatible enterprise Linux environment.

---

# 11. Web Infrastructure

## NGINX

**Purpose:** Web server and reverse proxy.

NGINX will be used for:

* Web hosting
* Reverse proxy services
* Application publishing
* TLS termination
* DMZ services

## Apache HTTP Server

**Purpose:** Secondary web platform.

Apache will provide an additional application server for testing and load-balancing scenarios.

---

# 12. Database Platform

## PostgreSQL

**Purpose:** Enterprise relational database platform.

PostgreSQL will provide database services for laboratory applications and infrastructure services where required.

---

# 13. Load Balancing

## HAProxy

**Purpose:** Application load balancing and high availability.

HAProxy will provide:

* Backend server pools
* Health checks
* Load distribution
* Session persistence
* TLS termination

---

# 14. Enterprise Storage

## TrueNAS CORE

**Purpose:** Shared enterprise storage.

TrueNAS will provide:

* SMB
* NFS
* iSCSI
* Storage pools
* Snapshots
* Backup targets
* Shared VMware storage

---

# 15. Infrastructure Monitoring

## Zabbix

**Purpose:** Primary infrastructure monitoring platform.

Zabbix will monitor:

* Network devices
* Windows servers
* Linux servers
* Firewalls
* Storage
* Applications
* Availability
* Performance

---

# 16. Metrics and Dashboards

## Grafana

**Purpose:** Infrastructure visualisation and dashboards.

Grafana will provide dashboards for:

* Network utilisation
* Server performance
* WAN performance
* Security metrics
* Application health
* Infrastructure availability

## Prometheus

**Purpose:** Metrics collection.

Prometheus will primarily support container and application monitoring where appropriate.

---

# 17. Security Monitoring

## Wazuh

**Purpose:** Security monitoring and endpoint visibility.

Wazuh will provide:

* Log analysis
* File integrity monitoring
* Authentication monitoring
* Vulnerability visibility
* Security alerts
* Endpoint monitoring

---

# 18. Infrastructure Automation

## Ansible

**Purpose:** Configuration management and automation.

Ansible will automate:

* Network configuration
* Configuration backups
* Linux administration
* Compliance checks
* Standardised infrastructure deployment

## Python

**Purpose:** Custom infrastructure and network automation.

Python will be used to develop:

* Network backup tools
* Device health checks
* Configuration generators
* Network audits
* Operational utilities

---

# 19. Infrastructure as Code

## Terraform

**Purpose:** Declarative infrastructure provisioning.

Terraform will primarily be used to provision AWS infrastructure including:

* VPCs
* Subnets
* Route tables
* Security groups
* EC2
* S3
* IAM
* RDS

---

# 20. Version Control

## Git

**Purpose:** Local source and configuration version control.

Git will track:

* Documentation
* Infrastructure code
* Automation
* Configuration templates
* Project changes

## GitHub

**Purpose:** Remote repository and portfolio platform.

GitHub will provide:

* Remote version control
* Repository hosting
* Portfolio presentation
* Change history
* Infrastructure code storage

---

# 21. Containers

## Docker

**Purpose:** Application containerisation.

Docker will be used to demonstrate:

* Container images
* Container networking
* Persistent storage
* Docker Compose
* Application deployment

---

# 22. Container Orchestration

## Kubernetes

**Purpose:** Container orchestration.

Kubernetes will demonstrate:

* Deployments
* Services
* Scaling
* ConfigMaps
* Secrets
* Persistent storage
* Ingress
* Rolling updates

## Minikube

**Purpose:** Local Kubernetes laboratory platform.

Minikube will provide the Kubernetes environment without requiring a production cluster.

---

# 23. Cloud Platform

## Amazon Web Services (AWS)

**Purpose:** Hybrid cloud platform.

AWS services used within the project will include:

* Amazon VPC
* Amazon EC2
* Amazon S3
* AWS IAM
* Amazon RDS
* Route 53
* Site-to-Site VPN
* Transit Gateway where appropriate

---

# 24. Administrative Tools

The engineering workstation may use:

* MobaXterm
* PuTTY
* WinSCP
* Wireshark
* Visual Studio Code
* draw.io
* Git CLI
* AWS CLI
* Terraform CLI
* Ansible CLI
* Python

---

# 25. Technology Selection Principles

Technologies used throughout the project are selected based on:

* Enterprise relevance
* Industry adoption
* Laboratory availability
* Interoperability
* Automation capability
* Security
* Scalability
* Operational value
* Professional development value

---

# 26. Inventory Management

Software versions and significant configuration changes shall be documented as the project progresses.

Where possible, exact versions used within the laboratory shall be recorded to support reproducibility and troubleshooting.

---

# Revision History

| Version | Date        | Author            | Description                               |
| ------- | ----------- | ----------------- | ----------------------------------------- |
| 1.0     | August 2026 | Edmond Chamunorwa | Initial technology and software inventory |
