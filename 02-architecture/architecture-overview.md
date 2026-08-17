# BETELGEUSE INFRA (PVT) LTD

# Enterprise Architecture Overview

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

This document provides a high-level overview of the enterprise infrastructure architecture designed for Apex Manufacturing (Private) Limited.

The architecture integrates enterprise networking, security, server infrastructure, virtualisation, monitoring, automation, data-centre technologies and hybrid cloud services into a unified environment.

This document describes the major architectural components and their relationships before detailed technical implementation begins.

---

# 2. Architecture Objectives

The architecture is designed to provide:

* High availability
* Network resilience
* Secure segmentation
* Centralised infrastructure services
* Multi-site connectivity
* Scalable routing
* Secure Internet access
* Data-centre connectivity
* Infrastructure monitoring
* Security visibility
* Configuration automation
* Hybrid cloud integration
* Backup and disaster recovery capability

---

# 3. Enterprise Environment

The Apex Manufacturing infrastructure consists of the following major locations:

* Harare Headquarters
* Harare Data Centre
* Bulawayo Branch
* Mutare Branch
* Gweru Branch
* AWS Cloud Environment

Harare Headquarters acts as the primary enterprise campus and central connectivity location.

---

# 4. High-Level Architecture

The infrastructure follows the logical structure below:

```text
                           INTERNET
                              |
                    +-------------------+
                    |     ISP-A / ISP-B |
                    +-------------------+
                              |
                    +-------------------+
                    |  Internet Edge    |
                    |  Routers / BGP    |
                    +-------------------+
                              |
                    +-------------------+
                    | FortiGate HA      |
                    | Firewall Cluster  |
                    +-------------------+
                              |
              +---------------+---------------+
              |                               |
        Enterprise Campus                Data Centre
              |                               |
       +-------------+                +---------------+
       | Core Layer  |                | Spine-Leaf    |
       +-------------+                | VXLAN / EVPN  |
              |                      +---------------+
       +-------------+                       |
       | Distribution|                 Server / App
       +-------------+                 Infrastructure
              |
       +-------------+
       | Access Layer|
       +-------------+
              |
      Users / Voice / IoT
              |
              |
      +-------+--------+
      | Enterprise WAN|
      +-------+--------+
              |
     +--------+--------+--------+
     |                 |        |
 Bulawayo           Mutare    Gweru
 Branch             Branch    Branch


                Hybrid Cloud Connectivity
                         |
                  Site-to-Site VPN
                         |
                        AWS
```

---

# 5. Campus Architecture

The Harare Headquarters campus will use a hierarchical enterprise design consisting of:

## Core Layer

The core layer will provide:

* High-speed Layer 3 backbone connectivity
* Connectivity between distribution switches
* Connectivity toward security and WAN infrastructure
* Dynamic routing
* Resilient paths

## Distribution Layer

The distribution layer will provide:

* Inter-VLAN routing
* Layer 3 gateway services
* HSRP or VRRP
* Routing policy
* Access-layer aggregation
* Spanning-tree control

## Access Layer

The access layer will provide connectivity for:

* Employee workstations
* IP phones
* Printers
* Wireless devices
* CCTV
* IoT devices
* Other enterprise endpoints

---

# 6. Enterprise Segmentation

The enterprise network will be divided into multiple logical security and operational domains.

Examples include:

* Management
* Finance
* Human Resources
* Information Technology
* Sales
* Procurement
* Manufacturing
* Warehousing
* Logistics
* Voice
* Servers
* Guest
* CCTV / IoT
* Monitoring
* Storage
* DMZ

VLANs and IP subnets will be defined during detailed network design.

---

# 7. WAN Architecture

The enterprise WAN will provide connectivity between headquarters and branch locations.

The laboratory will simulate technologies including:

* Routed WAN links
* MPLS
* Site-to-Site VPN
* SD-WAN
* Primary and backup paths
* Dynamic routing

WAN failover behaviour will be tested during implementation.

---

# 8. Internet Edge Architecture

Apex Manufacturing will use a dual-provider Internet architecture.

The environment will include:

* ISP-A
* ISP-B
* Two Internet-edge routers
* eBGP connectivity
* Route filtering
* Traffic engineering
* Redundant Internet paths

The design will allow Internet connectivity to continue if one provider becomes unavailable.

---

# 9. Security Architecture

The enterprise security perimeter will use FortiGate virtual firewalls operating in a high-availability configuration.

The firewall architecture will provide:

* Internet security
* NAT
* Security zones
* DMZ isolation
* Site-to-Site VPN
* Remote-access VPN
* Application control
* Intrusion prevention
* Web filtering
* Security logging

Firewall rules will follow least-privilege principles.

---

# 10. Data Centre Architecture

The Harare Data Centre will use a Spine-Leaf architecture.

The design will include:

* Two spine switches
* Multiple leaf switches
* Layer 3 underlay
* BGP
* MP-BGP EVPN
* VXLAN overlay networking
* VTEPs
* VNIs
* Anycast gateways

The data-centre environment will host enterprise applications, databases, storage, monitoring platforms and virtualised workloads.

---

# 11. Server Infrastructure

The enterprise server environment will contain both Microsoft and Linux infrastructure.

## Microsoft Services

Microsoft infrastructure will include:

* Active Directory Domain Services
* DNS
* DHCP
* Group Policy
* Certificate services where applicable
* File services

## Linux Services

Linux systems will provide:

* Web hosting
* Reverse proxy services
* Database services
* Monitoring
* Automation
* Container platforms
* Infrastructure management

---

# 12. Virtualisation Architecture

VMware Workstation Pro will act as the primary laboratory virtualisation platform.

It will host:

* EVE-NG
* Windows Server
* Windows clients
* Linux servers
* Monitoring systems
* Security systems
* Storage platforms
* Automation systems

Enterprise virtualisation concepts will later be demonstrated using VMware ESXi and vCenter where system resources permit.

---

# 13. Storage Architecture

TrueNAS will provide shared enterprise storage services.

Storage services will include:

* SMB
* NFS
* iSCSI
* Backup targets
* Snapshots
* Shared virtualisation storage

Storage traffic will be logically separated from standard user traffic.

---

# 14. Application Delivery Architecture

Enterprise applications will use NGINX and HAProxy where appropriate.

The application delivery architecture will provide:

* Reverse proxy services
* Load balancing
* Health checks
* TLS termination
* Application publishing
* High availability

Public-facing applications will be hosted through a dedicated DMZ architecture.

---

# 15. Monitoring Architecture

Zabbix will act as the primary infrastructure monitoring system.

Monitoring will include:

* Routers
* Switches
* Firewalls
* Windows servers
* Linux servers
* Storage systems
* Web services
* Applications

Grafana will provide infrastructure dashboards and metrics visualisation.

Prometheus may provide additional metrics collection for application and container environments.

---

# 16. Security Monitoring Architecture

Wazuh will provide security monitoring and endpoint visibility.

Security monitoring will include:

* Windows events
* Linux events
* Authentication activity
* Privilege escalation
* File integrity
* Vulnerability information
* Security alerts
* Firewall logs

---

# 17. Automation Architecture

The infrastructure automation platform will use:

* Ansible
* Python
* Terraform
* Git
* GitHub

Ansible will provide configuration management.

Python will provide custom network automation and operational tooling.

Terraform will provide Infrastructure as Code for cloud resources.

Git and GitHub will provide version control and configuration history.

---

# 18. Container Architecture

Docker will provide application containerisation.

Kubernetes using Minikube will provide container orchestration capabilities including:

* Deployments
* Services
* Scaling
* Ingress
* Persistent storage
* ConfigMaps
* Secrets
* Rolling updates

---

# 19. Hybrid Cloud Architecture

AWS will extend the Apex Manufacturing environment into a hybrid cloud architecture.

Cloud infrastructure may include:

* Amazon VPC
* Public and private subnets
* EC2
* RDS
* S3
* IAM
* Route 53
* Site-to-Site VPN

AWS address space shall not overlap with the on-premises enterprise IP addressing plan.

---

# 20. Management Architecture

Infrastructure management will be separated from normal user traffic.

Management services will include:

* SSH
* HTTPS
* SNMPv3
* Syslog
* NTP
* AAA
* Centralised monitoring
* Configuration backup
* Jump-server access

Management-plane access will be restricted using network security controls.

---

# 21. High Availability Strategy

High availability will be implemented across multiple infrastructure layers.

Examples include:

* Redundant core switches
* Redundant distribution switches
* HSRP / VRRP
* EtherChannel
* Multiple routed paths
* Dual Internet providers
* Firewall HA
* Multiple domain controllers
* Multiple web servers
* Load balancer redundancy
* Data-centre spine redundancy
* Backup infrastructure

Failure scenarios will be deliberately simulated and documented.

---

# 22. Security Design Principles

The architecture will follow:

* Defence in depth
* Least privilege
* Network segmentation
* Secure management
* Centralised visibility
* Controlled administrative access
* Logging and auditing
* Secure remote access
* Infrastructure hardening

---

# 23. Architecture Evolution

This document represents the initial high-level architecture.

Detailed designs will subsequently define:

* IP addressing
* VLAN allocation
* Routing
* Switching
* WAN connectivity
* Firewall policies
* Server placement
* Data-centre fabrics
* Monitoring
* Automation
* AWS connectivity

The architecture may evolve during implementation where justified by testing or technical constraints.

Any significant architecture change must be documented through the project change-management process.

---

# Revision History

| Version | Date        | Author            | Description                              |
| ------- | ----------- | ----------------- | ---------------------------------------- |
| 1.0     | August 2026 | Edmond Chamunorwa | Initial enterprise architecture overview |
