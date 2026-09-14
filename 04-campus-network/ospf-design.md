# OSPF Campus Routing Design

## Overview

The Enterprise Infrastructure Master Lab (EIML) uses Open Shortest Path First (OSPF) as the Interior Gateway Protocol between the campus Distribution and Core layers.

OSPF provides dynamic route exchange, redundant path calculation, automatic convergence following failures, and support for Equal-Cost Multi-Path (ECMP) forwarding.

The current campus routing domain operates entirely within OSPF Area 0.

---

## OSPF Topology

Four Layer 3 infrastructure devices currently participate in OSPF:

| Device | Router ID | Role |
|---|---|---|
| CORE1 | 1.1.1.1 | Core |
| CORE2 | 2.2.2.2 | Core |
| DIST1 | 3.3.3.3 | Distribution |
| DIST2 | 4.4.4.4 | Distribution |

The routed topology provides redundant paths between the Core and Distribution layers.

---

## Layer 3 Transit Networks

Dedicated /30 networks are used for point-to-point infrastructure links.

| Network | Connection |
|---|---|
| 10.255.0.0/30 | CORE1 ↔ DIST1 |
| 10.255.0.4/30 | CORE1 ↔ DIST2 |
| 10.255.0.8/30 | CORE2 ↔ DIST1 |
| 10.255.0.12/30 | CORE2 ↔ DIST2 |
| 10.255.0.16/30 | CORE1 ↔ CORE2 |

The `10.255.0.0/24` address space is reserved for infrastructure transit addressing.

---

## OSPF Area Design

All current campus routing links participate in:

`Area 0`

Area 0 forms the OSPF backbone.

A single-area design is appropriate for the current lab size while maintaining a foundation that can later be expanded into a multi-area OSPF architecture.

---

## Distribution Layer Advertisements

DIST1 and DIST2 advertise the campus VLAN networks into OSPF:

| VLAN | Network |
|---|---|
| VLAN 10 | 192.168.10.0/24 |
| VLAN 20 | 192.168.20.0/24 |
| VLAN 30 | 192.168.30.0/24 |
| VLAN 40 | 192.168.40.0/24 |
| VLAN 50 | 192.168.50.0/24 |
| VLAN 99 | 192.168.99.0/24 |

This allows the Core layer to dynamically learn reachability toward all campus networks.

---

## Passive Interface Strategy

The distribution switches use:

`passive-interface default`

OSPF neighbor formation is then explicitly enabled only on the routed uplinks using:

`no passive-interface <interface>`

This prevents unnecessary OSPF Hello packets from being transmitted toward user-facing VLANs while still allowing those VLAN networks to be advertised into OSPF.

This approach also reduces the possibility of unintended OSPF neighbor formation on access-facing networks.

---

## OSPF Neighbor Relationships

OSPF adjacency was validated using:

`show ip ospf neighbor`

Successful adjacencies reached the `FULL` state.

For example, CORE1 successfully formed OSPF relationships with:

- CORE2 — Router ID 2.2.2.2
- DIST1 — Router ID 3.3.3.3
- DIST2 — Router ID 4.4.4.4

This verifies Layer 3 connectivity and successful OSPF neighbor establishment across the redundant campus topology.

---

## Dynamic Route Learning

Routing information was validated using:

`show ip route ospf`

and:

`show ip ospf route`

The Core layer dynamically learned the campus VLAN networks from the Distribution layer.

Example:

`O 192.168.10.0/24`

The `O` route code indicates that the network was learned through OSPF.

---

## Equal-Cost Multi-Path Routing

The topology provides multiple equal-cost paths for selected destinations.

Where two OSPF paths have identical calculated costs, Cisco IOS can install both routes into the routing table.

This provides Equal-Cost Multi-Path (ECMP) forwarding.

Example concept:

CORE1 can reach a campus destination through:

CORE1 → DIST1

or

CORE1 → DIST2

when both paths have equal OSPF cost.

ECMP improves path utilization and provides immediate alternate forwarding options if one path becomes unavailable.

---

## Routing Resiliency

The redundant topology allows OSPF to recalculate forwarding paths when a routed link fails.

The intended behavior is:

Normal operation:

Multiple OSPF paths are available.

Link failure:

OSPF detects the topology change.

Convergence:

The failed path is removed and an alternate path is selected.

Recovery:

When the link returns, OSPF re-establishes adjacency and recalculates the shortest-path tree.

Controlled failure testing will be performed separately and documented in the testing section of the project.

---

## Verification Commands

The following commands are used during OSPF validation:

`show ip ospf neighbor`

Displays established OSPF neighbor relationships.

`show ip ospf interface brief`

Displays OSPF-enabled interfaces, areas, costs, and neighbor counts.

`show ip route ospf`

Displays routes installed into the routing table by OSPF.

`show ip ospf route`

Displays the OSPF routing topology.

`show running-config | section router ospf`

Displays the active OSPF configuration.

---

## Current Status

The campus OSPF backbone is operational.

Validated functionality includes:

- OSPF Area 0 operation
- Explicit router IDs
- Core-to-distribution neighbor formation
- Core-to-core neighbor formation
- Distribution VLAN advertisement
- Dynamic route learning
- Redundant routed paths
- ECMP route installation

The next engineering stage is controlled high-availability and convergence testing.
