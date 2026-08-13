# BETELGEUSE INFRA (PVT) LTD

# Enterprise Infrastructure Master Lab  
## Project Charter

| Document Information | Details |
|---|---|
| Project Name | Enterprise Infrastructure Master Lab |
| Client | Apex Manufacturing (Private) Limited |
| Implementation Partner | Betelgeuse Infra (Pvt) Ltd |
| Document Owner | Edmond Chamunorwa |
| Version | 1.0 |
| Status | Draft |
| Classification | Internal |
| Project Start Date | August 2026 |

---

## 1. Project Purpose

The Enterprise Infrastructure Master Lab project has been initiated to design, implement, secure, automate, monitor and document a modern enterprise IT infrastructure for Apex Manufacturing (Private) Limited.

The project will simulate a production-style enterprise environment incorporating campus networking, branch connectivity, firewalls, server infrastructure, data-centre technologies, monitoring, automation, containers and hybrid cloud integration.

Betelgeuse Infra (Pvt) Ltd will act as the infrastructure implementation partner responsible for architecture, deployment, validation, documentation and operational readiness.

---

## 2. Background

Apex Manufacturing operates from a headquarters site in Harare with branch offices in Bulawayo, Mutare and Gweru.

The organisation depends on reliable IT infrastructure to support manufacturing operations, finance, payroll, human resources, sales, logistics, warehousing, communications and business applications.

The current infrastructure requires modernisation to improve availability, security, scalability, monitoring, automation and disaster recovery capability.

---

## 3. Project Objectives

The project objectives are to:

- Design a secure and scalable enterprise infrastructure
- Build a resilient multi-site campus and branch network
- Implement redundant internet and WAN connectivity
- Deploy high-availability firewall services
- Provide centralised identity, DNS and DHCP services
- Deploy enterprise Windows and Linux infrastructure
- Build a modern data-centre environment
- Implement centralised monitoring and security visibility
- Automate network and server administration
- Integrate the on-premises environment with AWS
- Implement backup and disaster recovery procedures
- Produce professional technical and operational documentation

---

## 4. Project Scope

### 4.1 In Scope

The following components are included in the project:

- Enterprise campus network
- Core, distribution and access switching
- VLAN segmentation
- Inter-VLAN routing
- OSPF enterprise routing
- Multi-site branch connectivity
- MPLS and SD-WAN simulation
- Dual-ISP internet edge
- BGP routing
- FortiGate firewall high availability
- Site-to-site IPSec VPN
- Remote-access VPN
- Windows Server 2022
- Active Directory Domain Services
- DNS and DHCP
- Group Policy
- Ubuntu Server
- Rocky Linux
- NGINX and Apache
- PostgreSQL
- DMZ services
- HAProxy load balancing
- TrueNAS storage
- VMware virtualisation
- Data-centre spine-leaf architecture
- VXLAN and EVPN
- Zabbix monitoring
- Grafana dashboards
- Wazuh security monitoring
- Network management services
- Ansible automation
- Python network automation
- Terraform Infrastructure as Code
- Docker containers
- Kubernetes with Minikube
- AWS hybrid cloud connectivity
- Security hardening
- Disaster recovery
- Troubleshooting exercises
- Final testing and portfolio documentation

### 4.2 Out of Scope

The following items are excluded from the initial implementation:

- Production deployment for a real customer
- Purchase of physical enterprise hardware
- Carrier-provided production MPLS services
- Paid enterprise software licences not available for laboratory use
- Production personal or financial data
- Twenty-four-hour operational support
- Formal regulatory certification
- Direct connection to a live customer environment

---

## 5. Major Deliverables

The project will produce:

- Project charter
- Client business profile
- Business requirements document
- Technical requirements document
- Architecture overview
- High-level design
- Low-level design
- IP addressing plan
- VLAN plan
- Device naming standard
- VMware network plan
- Tool and software inventory
- Network and server configurations
- Security policies
- Monitoring dashboards
- Automation scripts and playbooks
- Terraform configurations
- Test plans and test results
- Troubleshooting records
- Disaster recovery runbook
- Final implementation guide
- GitHub portfolio repository
- Final project presentation

---

## 6. Key Stakeholders

| Stakeholder | Role |
|---|---|
| Apex Manufacturing Executive Management | Project Sponsor |
| Apex Manufacturing IT Management | Business and Technical Owner |
| Apex Manufacturing Department Heads | Business Stakeholders |
| Betelgeuse Infra | Implementation Partner |
| Edmond Chamunorwa | Lead Infrastructure Engineer |
| Systems and Network Administrators | Operational Stakeholders |
| Security Team | Security Review and Monitoring |
| End Users | Consumers of Infrastructure Services |

---

## 7. Assumptions

The project is based on the following assumptions:

- Required software images are legally available for laboratory use
- VMware Workstation Pro is operational
- EVE-NG will support the selected network appliances
- The host system has sufficient CPU, memory and storage
- Internet connectivity is available for software downloads and cloud access
- AWS resources will be deployed within controlled cost limits
- The environment will be built in modules to manage resource usage
- All passwords, secrets and keys will be excluded from Git
- The laboratory will not process production customer data

---

## 8. Constraints

The project is subject to the following constraints:

- Limited host memory and processor resources
- Limited disk capacity
- Software licensing restrictions
- Availability and compatibility of virtual network images
- AWS Free Tier and budget limitations
- Dependence on nested virtualisation
- Laboratory performance may differ from physical hardware
- Not all enterprise features may be available in evaluation versions
- The complete environment cannot remain powered on simultaneously

---

## 9. Project Risks

| Risk | Impact | Mitigation |
|---|---|---|
| Insufficient RAM or CPU | Virtual machines may fail or perform poorly | Run the environment in modules and reduce concurrent workloads |
| Storage exhaustion | VM corruption or inability to deploy systems | Monitor storage and maintain backups |
| Software image incompatibility | Delays in EVE-NG deployment | Test each image independently before integration |
| Licensing limitations | Some features may be unavailable | Use evaluation, community or simulated alternatives |
| AWS cost overruns | Unexpected charges | Use budgets, alerts and destroy temporary resources |
| Configuration errors | Service outages within the lab | Use snapshots, backups and Git version control |
| Loss of project data | Documentation or configuration loss | Maintain local and remote repository backups |
| Exposure of credentials | Security compromise | Use `.gitignore`, vaults and environment variables |
| Scope expansion | Project delays | Follow the approved 36-phase blueprint |
| Resource fatigue | Incomplete implementation | Complete the project phase by phase |

---

## 10. Success Criteria

The project will be considered successful when:

- All planned infrastructure phases have been completed
- Headquarters and branch networks communicate securely
- Redundant network paths and services have been tested
- Enterprise routing protocols operate correctly
- Firewall policies and VPN services are operational
- Active Directory, DNS and DHCP services are available
- Linux and Windows server workloads are functional
- Monitoring and alerting systems detect simulated failures
- Security events are collected and investigated
- Automation tools successfully deploy or validate configurations
- AWS hybrid connectivity is demonstrated
- Backup and recovery procedures are tested
- Technical documentation is complete
- The repository contains clear implementation and verification evidence

---

## 11. Project Governance

The project will follow this engineering workflow:

1. Design
2. Review
3. Build
4. Verify
5. Test
6. Troubleshoot
7. Document
8. Commit to Git

No major phase will be considered complete until its required deliverables and verification evidence have been produced.

Changes to the approved design must be recorded in the project change log.

---

## 12. Project Phases

The project will follow the approved 36-phase Enterprise Infrastructure Master Lab roadmap, beginning with project planning and concluding with final testing and portfolio presentation.

The roadmap will remain the source of truth unless a change is formally approved and documented.

---

## 13. Approval

| Role | Name | Status |
|---|---|---|
| Project Sponsor | Apex Manufacturing Executive Management | Pending |
| Client Technical Owner | Apex Manufacturing IT Management | Pending |
| Implementation Partner | Betelgeuse Infra (Pvt) Ltd | Approved |
| Lead Infrastructure Engineer | Edmond Chamunorwa | Approved |

---

## 14. Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0 | August 2026 | Edmond Chamunorwa | Initial project charter |
