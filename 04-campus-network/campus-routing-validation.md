# Campus Routing Validation

## Purpose

This document records the validation performed on the EIML campus Layer 3
routing architecture after deployment of the redundant Core and Distribution
layers.

The objective was to prove that the implemented network provides:

- Layer 3 connectivity between the Core and Distribution layers
- OSPF neighbor formation
- Dynamic route propagation
- Equal-cost redundant routing where applicable
- Advertisement of campus VLAN networks
- HSRP gateway redundancy
- Inter-VLAN routing
- Multiple forwarding paths through the campus infrastructure

The validation was performed in the EVE-NG lab environment using Cisco IOS
Layer 3 devices.

---

# 1. Validated Campus Architecture

The Layer 3 campus topology consists of:

CORE1
CORE2
DIST1
DIST2

The Distribution layer also connects to the Access layer and provides Layer 3
SVIs for the campus VLANs.

The routed Core/Distribution topology is:

                    CORE1
                   /     \
                  /       \
              DIST1       DIST2
                  \       /
                   \     /
                    CORE2

Additional connectivity exists between CORE1 and CORE2.

The resulting architecture provides multiple Layer 3 paths between the
Distribution and Core layers.

---

# 2. OSPF Design

OSPF Process ID:

1

OSPF Area:

Area 0

Router IDs:

| Device | OSPF Router ID |
|---|---|
| CORE1 | 1.1.1.1 |
| CORE2 | 2.2.2.2 |
| DIST1 | 3.3.3.3 |
| DIST2 | 4.4.4.4 |

The Core and Distribution routed point-to-point networks use addresses from
the 10.255.0.0 address space.

---

# 3. Routed Transit Networks

The following /30 networks are used by the campus routing infrastructure:

| Network | Purpose |
|---|---|
| 10.255.0.0/30 | Core/Distribution routed link |
| 10.255.0.4/30 | Core/Distribution routed link |
| 10.255.0.8/30 | Core/Distribution routed link |
| 10.255.0.12/30 | Core/Distribution routed link |
| 10.255.0.16/30 | CORE1-to-CORE2 routed link |

Using /30 networks provides two usable addresses per point-to-point link and
keeps the Layer 3 transit addressing separate from user VLAN addressing.

---

# 4. OSPF Neighbor Validation

OSPF neighbor relationships were verified using:

    show ip ospf neighbor

Successful adjacency formation was observed.

Example CORE1 neighbor table showed:

- Router ID 2.2.2.2
- Router ID 3.3.3.3
- Router ID 4.4.4.4

with neighbors reaching FULL state.

Example:

    Neighbor ID     State
    2.2.2.2         FULL/DR
    4.4.4.4         FULL/BDR
    3.3.3.3         FULL/BDR

The FULL state confirms that the devices successfully:

1. Discovered each other using OSPF Hello packets
2. Negotiated adjacency
3. Exchanged database information
4. Synchronized their Link-State Databases
5. Established operational OSPF neighbor relationships

Validation Result:

PASS

---

# 5. Distribution OSPF Neighbor Validation

DIST2 was verified to have OSPF adjacencies with both Core switches.

Observed neighbors included:

    Neighbor ID     State
    2.2.2.2         FULL/DR
    1.1.1.1         FULL/DR

This demonstrated that DIST2 had redundant Layer 3 connectivity into the
Core layer.

A failure of one upstream Core path therefore does not inherently isolate
DIST2 from the routed campus infrastructure.

Validation Result:

PASS

---

# 6. OSPF Route Validation

The OSPF routing table was examined using:

    show ip route ospf

and:

    show ip ospf route

Routes marked with:

    O

in the routing table represent networks learned dynamically through OSPF.

The Core switches successfully learned the campus VLAN networks from the
Distribution layer.

Observed routes included:

    192.168.10.0/24
    192.168.20.0/24
    192.168.30.0/24
    192.168.40.0/24
    192.168.50.0/24
    192.168.99.0/24

Validation Result:

PASS

---

# 7. VLAN Route Advertisement

The following campus networks were advertised into OSPF:

| VLAN | Network |
|---|---|
| VLAN 10 | 192.168.10.0/24 |
| VLAN 20 | 192.168.20.0/24 |
| VLAN 30 | 192.168.30.0/24 |
| VLAN 40 | 192.168.40.0/24 |
| VLAN 50 | 192.168.50.0/24 |
| VLAN 99 | 192.168.99.0/24 |

Both Distribution switches participate in advertising the VLAN networks.

This allows the Core layer to dynamically learn where the campus user
networks are located.

---

# 8. OSPF Passive Interface Design

The Distribution switches use:

    passive-interface default

This prevents OSPF neighbor relationships from forming on interfaces where
OSPF adjacency is unnecessary.

Only the routed Core-facing interfaces are explicitly enabled using:

    no passive-interface <interface>

For example, DIST1 uses its routed uplinks toward CORE1 and CORE2 as
non-passive interfaces.

The VLAN networks can therefore still be advertised into OSPF without
attempting to establish OSPF adjacencies with user devices.

This reduces unnecessary OSPF traffic and improves routing protocol security.

Validation Result:

PASS

---

# 9. Equal-Cost Multipath Validation

OSPF installed multiple next hops for some destinations.

Example behavior observed on CORE1:

    O 192.168.10.0/24 [110/2] via 10.255.0.6
                         via 10.255.0.2

This is Equal-Cost Multipath routing (ECMP).

Both routes have the same OSPF cost.

Rather than selecting only one route, OSPF can install both routes in the
routing table.

This allows traffic to use multiple equal-cost paths through the campus
network.

Benefits include:

- Better utilization of redundant links
- Increased path availability
- Faster recovery following link failure
- Reduced dependence on a single Distribution switch

Validation Result:

PASS

---

# 10. HSRP Validation

The campus Distribution layer uses HSRP to provide redundant default
gateways.

Verification command:

    show standby brief

The normal design uses:

DIST1:

    Priority 110
    State Active

DIST2:

    Priority 100
    State Standby

The HSRP virtual gateways are:

| VLAN | Virtual Gateway |
|---|---|
| VLAN 10 | 192.168.10.1 |
| VLAN 20 | 192.168.20.1 |
| VLAN 30 | 192.168.30.1 |
| VLAN 40 | 192.168.40.1 |
| VLAN 50 | 192.168.50.1 |
| VLAN 99 | 192.168.99.1 |

This allows hosts to use a gateway that is independent of the physical
Distribution switch currently forwarding traffic.

Validation Result:

PASS

---

# 11. HSRP Failover Observation

During lab testing, HSRP state changes were observed when the preferred
Distribution gateway became unavailable.

DIST2 transitioned from:

    Standby

to:

    Active

Example system message:

    %HSRP-5-STATECHANGE: Vlan10 Grp 10 state Standby -> Active

Equivalent transitions were observed across the configured VLANs.

This demonstrated that the standby Distribution switch was capable of
assuming the first-hop gateway role.

After the preferred router returned, HSRP preemption restored the intended
Active/Standby topology.

Validation Result:

PASS

---

# 12. Inter-VLAN Routing Validation

Layer 3 SVIs exist on the Distribution switches for the campus VLANs.

Examples include:

    interface Vlan10
    interface Vlan20
    interface Vlan30
    interface Vlan40
    interface Vlan50
    interface Vlan99

Inter-VLAN routing was confirmed operational during the campus implementation.

Traffic can therefore move between VLANs through the Distribution layer,
subject to routing and future security policy.

Validation Result:

PASS

---

# 13. Route Redundancy

The routing tables demonstrated multiple possible paths through the campus
infrastructure.

For example, CORE1 learned certain Distribution networks through more than
one next hop.

The topology therefore does not depend on a single routed Core/Distribution
connection.

Conceptually:

                    CORE1
                   /     \
                  /       \
              DIST1       DIST2
                  \       /
                   \     /
                    CORE2

OSPF dynamically calculates paths through this topology.

If one routed link fails, OSPF can recalculate the shortest available path.

---

# 14. Control Plane Redundancy

The campus network now contains several complementary redundancy mechanisms.

STP provides:

    Layer 2 loop prevention and path redundancy

HSRP provides:

    First-hop/default gateway redundancy

OSPF provides:

    Dynamic Layer 3 path redundancy

ECMP provides:

    Concurrent use of equal-cost Layer 3 paths

Together these mechanisms create a substantially more resilient campus
architecture than a single-switch or single-router design.

---

# 15. Troubleshooting Performed During Implementation

Several issues were encountered during implementation.

These included:

- Missing OSPF network advertisements
- Incomplete OSPF network commands
- Incorrect CLI command context
- SVIs temporarily being down
- HSRP state changes during interface failures
- OSPF neighbor expectations being confused with routed reachability
- VLAN networks initially missing from some OSPF configurations

These problems were diagnosed using commands including:

    show ip interface brief
    show ip route
    show ip route ospf
    show ip ospf neighbor
    show ip ospf interface brief
    show running-config | section router ospf
    show standby brief
    show spanning-tree vlan <vlan-id>

The troubleshooting process is documented separately under:

    20-troubleshooting/

---

# 16. Validation Summary

| Test | Result |
|---|---|
| Routed Core interfaces operational | PASS |
| Routed Distribution interfaces operational | PASS |
| CORE1 OSPF operation | PASS |
| CORE2 OSPF operation | PASS |
| DIST1 OSPF operation | PASS |
| DIST2 OSPF operation | PASS |
| OSPF FULL adjacencies observed | PASS |
| VLAN 10 advertised | PASS |
| VLAN 20 advertised | PASS |
| VLAN 30 advertised | PASS |
| VLAN 40 advertised | PASS |
| VLAN 50 advertised | PASS |
| VLAN 99 advertised | PASS |
| OSPF ECMP observed | PASS |
| HSRP Active/Standby operation | PASS |
| HSRP failover observed | PASS |
| Inter-VLAN routing | PASS |

---

# 17. Current Campus Routing Status

The EIML campus routing architecture is operational.

The network currently demonstrates:

- Redundant Core switches
- Redundant Distribution switches
- Routed Core-to-Distribution links
- OSPF Area 0
- Dynamic route advertisement
- Redundant OSPF paths
- ECMP
- HSRP first-hop redundancy
- Inter-VLAN routing
- Layer 2 STP protection

This establishes the Layer 2 and Layer 3 foundation required for subsequent
EIML phases including WAN connectivity, firewall integration, server
infrastructure, monitoring, security controls, and external connectivity.

---

# 18. Evidence

Screenshots and CLI outputs supporting these validation results are stored
under:

    screenshots/campus-routing/

Evidence should include:

- OSPF neighbor tables
- OSPF routing tables
- HSRP status
- Distribution SVI status
- Core routing tables
- ECMP routes
- STP state
- End-to-end ping tests

These artifacts provide evidence that the documented architecture was
actually implemented and validated in the lab.
