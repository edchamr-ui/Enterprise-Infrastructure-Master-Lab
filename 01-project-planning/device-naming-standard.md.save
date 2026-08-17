# BETELGEUSE INFRA (PVT) LTD

# Device & Infrastructure Naming Standard

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

This document defines the standard naming convention for network devices, servers, security appliances, infrastructure platforms and other technology assets deployed within the Enterprise Infrastructure Master Lab.

The objective is to ensure that infrastructure names are consistent, predictable, scalable and operationally meaningful.

---

# 2. Naming Format

Infrastructure devices shall generally follow the format:

`<ORG>-<SITE>-<ROLE>-<TYPE><NUMBER>`

Example:

`APX-HQ-CORE-SW01`

Where:

* `APX` identifies Apex Manufacturing.
* `HQ` identifies the Harare Headquarters.
* `CORE` identifies the infrastructure role.
* `SW` identifies the device as a switch.
* `01` identifies the individual device.

---

# 3. Organisation Code

| Organisation       | Code |
| ------------------ | ---- |
| Apex Manufacturing | APX  |
| Betelgeuse Infra   | BTI  |

`APX` shall be used for client infrastructure.

`BTI` shall be reserved for Betelgeuse Infra-owned engineering or management infrastructure where required.

---

# 4. Site Codes

| Site                | Code |
| ------------------- | ---- |
| Harare Headquarters | HQ   |
| Harare Data Centre  | DC   |
| Bulawayo Branch     | BYO  |
| Mutare Branch       | MTA  |
| Gweru Branch        | GWE  |
| AWS Cloud           | AWS  |

---

# 5. Infrastructure Role Codes

| Role          | Code  |
| ------------- | ----- |
| Core          | CORE  |
| Distribution  | DIST  |
| Access        | ACC   |
| Internet Edge | EDGE  |
| WAN           | WAN   |
| Spine         | SPINE |
| Leaf          | LEAF  |
| Management    | MGMT  |
| Monitoring    | MON   |
| Security      | SEC   |
| Application   | APP   |
| Database      | DB    |
| Storage       | STOR  |
| Web           | WEB   |
| Automation    | AUTO  |

---

# 6. Device Type Codes

| Device Type           | Code |
| --------------------- | ---- |
| Router                | RTR  |
| Switch                | SW   |
| Firewall              | FW   |
| Server                | SRV  |
| Domain Controller     | DC   |
| Load Balancer         | LB   |
| Wireless Access Point | AP   |
| Storage Appliance     | NAS  |
| Hypervisor            | HV   |
| VPN Gateway           | VPN  |

---

# 7. Network Device Examples

## Headquarters Core

`APX-HQ-CORE-SW01`

`APX-HQ-CORE-SW02`

## Headquarters Distribution

`APX-HQ-DIST-SW01`

`APX-HQ-DIST-SW02`

## Headquarters Access

`APX-HQ-ACC-SW01`

`APX-HQ-ACC-SW02`

## Internet Edge

`APX-HQ-EDGE-RTR01`

`APX-HQ-EDGE-RTR02`

## Firewalls

`APX-HQ-FW01`

`APX-HQ-FW02`

---

# 8. Branch Device Examples

## Bulawayo

`APX-BYO-WAN-RTR01`

`APX-BYO-ACC-SW01`

`APX-BYO-FW01`

## Mutare

`APX-MTA-WAN-RTR01`

`APX-MTA-ACC-SW01`

`APX-MTA-FW01`

## Gweru

`APX-GWE-WAN-RTR01`

`APX-GWE-ACC-SW01`

`APX-GWE-FW01`

---

# 9. Data Centre Device Examples

## Spine Switches

`APX-DC-SPINE-SW01`

`APX-DC-SPINE-SW02`

## Leaf Switches

`APX-DC-LEAF-SW01`

`APX-DC-LEAF-SW02`

`APX-DC-LEAF-SW03`

`APX-DC-LEAF-SW04`

---

# 10. Windows Server Examples

## Domain Controllers

`APX-HQ-DC01`

`APX-HQ-DC02`

## File Servers

`APX-HQ-FILE-SRV01`

## Application Servers

`APX-HQ-APP-SRV01`

---

# 11. Linux Server Examples

## Web Servers

`APX-HQ-WEB-SRV01`

`APX-HQ-WEB-SRV02`

## Database Server

`APX-HQ-DB-SRV01`

## Automation Server

`APX-HQ-AUTO-SRV01`

---

# 12. Monitoring and Security Platforms

## Zabbix

`APX-HQ-MON-SRV01`

## Grafana

`APX-HQ-MON-SRV02`

## Wazuh

`APX-HQ-SEC-SRV01`

---

# 13. Virtualisation Infrastructure

## ESXi Hosts

`APX-DC-HV01`

`APX-DC-HV02`

## vCenter

`APX-DC-VC01`

## Storage

`APX-DC-STOR-NAS01`

---

# 14. Load Balancers

`APX-DC-LB01`

`APX-DC-LB02`

---

# 15. AWS Resources

Cloud resources should follow a similar logical naming structure where supported.

Examples:

`apx-prod-vpc`

`apx-prod-public-subnet-01`

`apx-prod-private-subnet-01`

`apx-prod-web-ec2-01`

`apx-prod-db-01`

---

# 16. Naming Rules

Infrastructure names shall:

* Be unique within their management domain.
* Clearly identify the organisation.
* Clearly identify the site.
* Clearly identify the infrastructure role.
* Clearly identify the device or service type.
* Use consistent abbreviations.
* Use sequential numbering where multiple devices perform the same role.
* Avoid personal names.
* Avoid ambiguous names.
* Avoid spaces.
* Avoid unnecessarily long descriptions.

---

# 17. DNS Naming

Where DNS records are created, infrastructure hostnames should follow the approved device naming standard.

The final internal DNS namespace will be defined during the enterprise DNS design phase.

---

# 18. Automation Considerations

Naming consistency is mandatory because infrastructure automation will rely on predictable device identities.

The naming standard will support:

* Ansible inventory groups
* Python automation
* Monitoring discovery
* Configuration backups
* DNS management
* Logging
* Asset identification
* Troubleshooting

---

# 19. Exceptions

Any infrastructure component that cannot follow this naming convention because of vendor, protocol or platform restrictions shall be documented as an exception.

Exceptions must not introduce ambiguity into the environment.

---

# 20. Governance

All infrastructure deployed after approval of this standard shall follow the naming convention defined in this document.

Changes to the naming standard shall be documented through the project change-management process.

---

# Revision History

| Version | Date        | Author            | Description                                       |
| ------- | ----------- | ----------------- | ------------------------------------------------- |
| 1.0     | August 2026 | Edmond Chamunorwa | Initial device and infrastructure naming standard |
