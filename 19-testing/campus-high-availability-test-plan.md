# Campus Network High Availability Test Plan

**Project:** Enterprise Infrastructure Master Lab (EIML)
**Environment:** EVE-NG Enterprise Network Lab
**Test Area:** Campus Distribution Layer
**Technologies:** HSRP, OSPF, VLANs, Inter-VLAN Routing
**Status:** In Progress

---

## 1. Purpose

The purpose of this test plan is to validate high availability within the
campus network distribution and core layers.

The network has been designed so that the failure of a distribution switch
does not permanently remove the default gateway used by end-user devices.

High availability is provided through:

- HSRP for redundant default gateways.
- OSPF for dynamic Layer 3 routing.
- Dual distribution switches.
- Dual core switches.
- Redundant Layer 3 uplinks between the distribution and core layers.

---

## 2. Relevant Devices

| Device | Role | OSPF Router ID |
|---|---|---|
| DIST1 | Primary Distribution Switch | 3.3.3.3 |
| DIST2 | Secondary Distribution Switch | 4.4.4.4 |
| CORE1 | Core Switch | 1.1.1.1 |
| CORE2 | Core Switch | 2.2.2.2 |

---

## 3. HSRP Gateway Design

The VLAN interfaces use HSRP virtual IP addresses as the default gateways
for client devices.

| VLAN | HSRP Virtual Gateway | DIST1 | DIST2 |
|---|---|---|---|
| VLAN 10 | 192.168.10.1 | 192.168.10.2 | 192.168.10.3 |
| VLAN 20 | 192.168.20.1 | 192.168.20.2 | 192.168.20.3 |
| VLAN 30 | 192.168.30.1 | 192.168.30.2 | 192.168.30.3 |
| VLAN 40 | 192.168.40.1 | 192.168.40.2 | 192.168.40.3 |
| VLAN 50 | 192.168.50.1 | 192.168.50.2 | 192.168.50.3 |
| VLAN 99 | 192.168.99.1 | 192.168.99.2 | 192.168.99.3 |

DIST1 is configured with HSRP priority **110**.

DIST2 is configured with HSRP priority **100**.

HSRP preemption is enabled so that DIST1 automatically resumes the Active
role after recovering from a failure.

---

# HA-01 - Distribution Switch Failure and Recovery

## Objective

Verify that the campus network can automatically recover from failure of
the primary distribution switch without requiring client gateway
reconfiguration.

---

## Initial State

Before introducing the failure:

- DIST1 was HSRP Active.
- DIST2 was HSRP Standby.
- DIST1 HSRP priority was 110.
- DIST2 HSRP priority was 100.
- Preemption was enabled.
- OSPF adjacencies were established.
- The client used 192.168.10.1 as its default gateway.
- The HSRP virtual gateway was reachable.

Verification command:

```text
show standby brief
