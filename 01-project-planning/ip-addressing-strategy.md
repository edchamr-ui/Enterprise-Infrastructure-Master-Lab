# BETELGEUSE INFRA (PVT) LTD

# Enterprise IP Addressing Strategy

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

This document defines the high-level IPv4 addressing strategy for the Enterprise Infrastructure Master Lab.

The objective is to establish a scalable and structured addressing hierarchy before individual VLANs, subnets, point-to-point networks and infrastructure addresses are allocated.

Detailed subnet allocation will be completed during the IP Addressing and VLAN Design phase.

---

# 2. Private Address Space

The enterprise will primarily use RFC1918 private IPv4 addressing.

The principal enterprise address space will be derived from:

`10.0.0.0/8`

The address space will be divided logically according to site, infrastructure function and operational purpose.

---

# 3. Addressing Design Principles

The addressing architecture shall support:

* Hierarchical addressing
* Geographic separation
* Route summarisation
* Operational simplicity
* Predictable subnet allocation
* Infrastructure growth
* Network automation
* Hybrid cloud integration
* Simplified troubleshooting
* Clear separation of infrastructure functions

---

# 4. Site Address Allocation

| Location / Function       | Address Block | Purpose                              |
| ------------------------- | ------------- | ------------------------------------ |
| Harare Headquarters       | 10.10.0.0/16  | Headquarters campus infrastructure   |
| Bulawayo Branch           | 10.20.0.0/16  | Bulawayo branch infrastructure       |
| Mutare Branch             | 10.30.0.0/16  | Mutare branch infrastructure         |
| Gweru Branch              | 10.40.0.0/16  | Gweru branch infrastructure          |
| Harare Data Centre        | 10.50.0.0/16  | Data-centre workloads and networks   |
| Enterprise Services       | 10.60.0.0/16  | Shared infrastructure services       |
| Remote Access / VPN       | 10.70.0.0/16  | Remote-access and VPN address pools  |
| Infrastructure Management | 10.80.0.0/16  | Management infrastructure            |
| Reserved / Future Growth  | 10.90.0.0/16  | Future enterprise expansion          |
| WAN / Transit             | 10.250.0.0/16 | Routed point-to-point infrastructure |
| Infrastructure Loopbacks  | 10.255.0.0/16 | Router and infrastructure loopbacks  |

---

# 5. Headquarters Addressing

Harare Headquarters will use:

`10.10.0.0/16`

Individual subnets will later be allocated for functions including:

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
* Wireless
* Servers
* Infrastructure management
* Guest access

The exact subnet sizes and VLAN mappings will be defined during detailed network design.

---

# 6. Branch Addressing

Each branch receives an independent `/16` address block.

Bulawayo:

`10.20.0.0/16`

Mutare:

`10.30.0.0/16`

Gweru:

`10.40.0.0/16`

This structure allows branch routes to be summarised at the WAN routing boundary.

---

# 7. Data Centre Addressing

The primary data centre will use:

`10.50.0.0/16`

This block may contain networks for:

* Application servers
* Database servers
* Web servers
* Virtualisation
* Storage
* Load balancers
* DMZ services
* Container workloads
* Infrastructure services
* VXLAN tenant networks

Detailed data-centre subnet allocation will be completed during the data-centre design phase.

---

# 8. Enterprise Services

Shared enterprise services will use addresses derived from:

`10.60.0.0/16`

This range may support centralised services that are logically separated from site-specific user networks.

---

# 9. Remote Access and VPN

Remote-access address pools and selected VPN infrastructure will use addresses derived from:

`10.70.0.0/16`

This provides clear separation between remote users and internal endpoint networks.

---

# 10. Management Networks

Infrastructure management networks will use:

`10.80.0.0/16`

Management networks may include:

* Network-device management
* Hypervisor management
* Storage management
* Monitoring systems
* Security platforms
* Out-of-band management where simulated

Management access will be restricted through security policy.

---

# 11. WAN and Transit Networks

Point-to-point routed links will use addresses derived from:

`10.250.0.0/16`

Appropriately sized subnets will be selected during detailed WAN design.

The WAN addressing space shall remain separate from user and server networks.

---

# 12. Infrastructure Loopbacks

Infrastructure loopback addresses will be allocated from:

`10.255.0.0/16`

Loopback addresses may be assigned to:

* Core routers
* Distribution devices
* WAN routers
* Internet-edge routers
* Data-centre switches
* Other routed infrastructure

Loopbacks will provide stable addresses for routing protocols, management and device identification.

---

# 13. Cloud Addressing

AWS infrastructure shall use address space that does not overlap with the on-premises enterprise network.

The final AWS CIDR allocation will be defined during the AWS Hybrid Cloud Integration phase.

Non-overlapping addressing is mandatory to support routed Site-to-Site VPN connectivity.

---

# 14. Route Summarisation

The addressing architecture is intentionally hierarchical.

For example, all Bulawayo networks can potentially be represented by:

`10.20.0.0/16`

while all Mutare networks can potentially be represented by:

`10.30.0.0/16`

This design allows routing boundaries to advertise summary routes rather than large numbers of individual VLAN networks where technically appropriate.

---

# 15. Address Assignment Principles

The following principles shall apply:

* Static addresses for core infrastructure
* Static addresses for servers where appropriate
* DHCP for standard client endpoints
* Dedicated management addressing
* Dedicated loopback addressing
* Separate WAN transit addressing
* Non-overlapping cloud addressing
* Reserved capacity for growth
* Consistent default-gateway conventions

---

# 16. IPv6

IPv4 will be implemented first.

IPv6 may subsequently be introduced as an extension of the enterprise design without replacing the IPv4 architecture.

---

# 17. Documentation Requirements

Every allocated subnet shall eventually be documented with:

* Network address
* CIDR prefix
* Subnet mask
* Default gateway
* VLAN ID where applicable
* Site
* Purpose
* DHCP range where applicable
* Reserved addresses
* Broadcast address
* Usable host range

The authoritative detailed allocation will be maintained in the IP Addressing Plan.

---

# 18. Governance

IP addresses shall not be allocated arbitrarily.

New networks must follow the approved addressing hierarchy and be recorded in project documentation.

Any deviation from this strategy must be documented through the project change-management process.

---

# Revision History

| Version | Date        | Author            | Description                               |
| ------- | ----------- | ----------------- | ----------------------------------------- |
| 1.0     | August 2026 | Edmond Chamunorwa | Initial enterprise IP addressing strategy |
