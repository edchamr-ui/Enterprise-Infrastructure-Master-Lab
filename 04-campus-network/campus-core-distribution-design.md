# Campus Core and Distribution Layer Design

## Overview

The Enterprise Infrastructure Master Lab (EIML) campus network uses a hierarchical enterprise network architecture consisting of Access, Distribution, and Core layers.

The design provides redundant Layer 3 paths between the distribution and core layers to improve availability and eliminate single points of failure.

## Architecture

The campus infrastructure currently consists of:

- CORE1
- CORE2
- DIST1
- DIST2
- ACC1
- ACC2

End-user devices connect to the access layer, while Layer 3 routing and default gateway services are provided at the distribution layer.

The core layer provides high-speed Layer 3 transport between distribution infrastructure and will later provide connectivity toward additional enterprise services, WAN infrastructure, security zones, and other network domains.

## Redundancy Design

Both distribution switches have redundant routed connections toward the core layer.

The design provides the following logical paths:

DIST1 → CORE1
DIST1 → CORE2

DIST2 → CORE1
DIST2 → CORE2

CORE1 and CORE2 are also interconnected.

This architecture allows traffic to use alternate Layer 3 paths when an individual routed link becomes unavailable.

## Layer 3 Transit Addressing

Point-to-point infrastructure links use /30 networks from the `10.255.0.0` infrastructure address space.

Examples include:

| Transit Network | Purpose |
|---|---|
| 10.255.0.0/30 | CORE1 ↔ DIST1 |
| 10.255.0.4/30 | CORE1 ↔ DIST2 |
| 10.255.0.8/30 | CORE2 ↔ DIST1 |
| 10.255.0.12/30 | CORE2 ↔ DIST2 |
| 10.255.0.16/30 | CORE1 ↔ CORE2 |

Using /30 networks provides two usable addresses per point-to-point connection while maintaining clear separation between routed links.

## Routing Architecture

OSPF is used as the Interior Gateway Protocol for the campus Layer 3 infrastructure.

All current routed infrastructure links participate in OSPF Area 0.

OSPF router IDs are:

| Device | Router ID |
|---|---|
| CORE1 | 1.1.1.1 |
| CORE2 | 2.2.2.2 |
| DIST1 | 3.3.3.3 |
| DIST2 | 4.4.4.4 |

The distribution switches advertise the campus VLAN networks into OSPF so that the core layer can dynamically learn routes toward user and service networks.

## Default Gateway Redundancy

HSRP is implemented between DIST1 and DIST2.

End devices therefore use a virtual IP address as their default gateway instead of depending directly on either physical distribution switch.

This allows gateway services to survive the failure of one distribution device.

## Current VLAN Networks

The current campus design includes:

- VLAN 10 — 192.168.10.0/24
- VLAN 20 — 192.168.20.0/24
- VLAN 30 — 192.168.30.0/24
- VLAN 40 — 192.168.40.0/24
- VLAN 50 — 192.168.50.0/24
- VLAN 99 — 192.168.99.0/24

The HSRP virtual gateway follows the `.1` addressing convention for each VLAN.

## Design Objectives

The campus architecture was designed to demonstrate:

- Hierarchical enterprise network design
- Layer 2 and Layer 3 segmentation
- Redundant default gateways
- Dynamic routing
- Multiple Layer 3 forwarding paths
- OSPF Equal-Cost Multi-Path routing
- Failure recovery
- Infrastructure scalability
- Enterprise troubleshooting methodology

## Validation

The routing design has been validated using:

`show ip ospf neighbor`

`show ip route`

`show ip route ospf`

`show ip ospf route`

`show standby brief`

OSPF adjacencies successfully reached the FULL state, and the core switches learned the campus VLAN networks dynamically from the distribution layer.

Where equal-cost paths exist, OSPF installs multiple next hops, providing Equal-Cost Multi-Path (ECMP) forwarding.

## Next Validation Stage

The next stage of the implementation will perform controlled failure testing to verify:

1. OSPF convergence after an uplink failure.
2. Continued reachability through redundant paths.
3. HSRP gateway failover.
4. Recovery when failed infrastructure is restored.
