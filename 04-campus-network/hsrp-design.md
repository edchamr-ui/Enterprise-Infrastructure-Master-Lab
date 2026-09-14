# HSRP First-Hop Redundancy Design

## Overview

The Enterprise Infrastructure Master Lab (EIML) implements Hot Standby Router Protocol (HSRP) at the campus Distribution layer.

HSRP provides first-hop gateway redundancy for end-user and infrastructure VLANs.

Instead of configuring hosts to use the physical IP address of DIST1 or DIST2 as their default gateway, hosts use a shared HSRP Virtual IP (VIP).

This allows either distribution switch to provide Layer 3 gateway services without requiring endpoint configuration changes during a distribution-switch failure.

---

## Distribution Layer Gateway Architecture

Each VLAN has three gateway-related IP addresses:

- HSRP Virtual IP: `.1`
- DIST1 SVI: `.2`
- DIST2 SVI: `.3`

Example for VLAN 10:

| Device / Function | Address |
|---|---|
| HSRP Virtual Gateway | 192.168.10.1 |
| DIST1 | 192.168.10.2 |
| DIST2 | 192.168.10.3 |

End devices therefore use:

`192.168.10.1`

as their default gateway.

They do not depend directly on either physical distribution switch.

---

## HSRP VLAN Design

| VLAN | HSRP Group | Virtual IP |
|---|---:|---|
| VLAN 10 | 10 | 192.168.10.1 |
| VLAN 20 | 20 | 192.168.20.1 |
| VLAN 30 | 30 | 192.168.30.1 |
| VLAN 40 | 40 | 192.168.40.1 |
| VLAN 50 | 50 | 192.168.50.1 |
| VLAN 99 | 99 | 192.168.99.1 |

The HSRP group number matches the VLAN number where practical.

This makes the configuration easier to understand, troubleshoot, and document.

---

## HSRP Roles

Under normal operation:

DIST1 is the HSRP Active router.

DIST2 is the HSRP Standby router.

The configured priorities are:

| Device | Priority | Normal Role |
|---|---:|---|
| DIST1 | 110 | Active |
| DIST2 | 100 | Standby |

Because DIST1 has the higher HSRP priority, it becomes the preferred Active gateway.

---

## Preemption

HSRP preemption is enabled.

Example:

`standby 10 preempt`

Preemption allows the preferred distribution switch to reclaim the Active role after recovering from a failure.

Without preemption, DIST2 could remain Active even after DIST1 returned.

With preemption enabled:

1. DIST1 operates as Active.
2. DIST1 fails.
3. DIST2 becomes Active.
4. DIST1 recovers.
5. DIST1 detects its higher priority.
6. DIST1 preempts DIST2.
7. DIST1 returns to the Active role.

This restores the network to its intended steady-state architecture automatically.

---

## Example VLAN 10 Configuration

### DIST1

`interface Vlan10`

`ip address 192.168.10.2 255.255.255.0`

`standby 10 ip 192.168.10.1`

`standby 10 priority 110`

`standby 10 preempt`

### DIST2

`interface Vlan10`

`ip address 192.168.10.3 255.255.255.0`

`standby 10 ip 192.168.10.1`

`standby 10 priority 100`

`standby 10 preempt`

The same design pattern is applied to the remaining VLANs.

---

## HSRP Operation

During normal operation, endpoint traffic is sent to the virtual gateway.

Example:

IT-PC1

↓

192.168.10.1

↓

HSRP Active Router

↓

DIST1

↓

Campus routing infrastructure

Although both distribution switches have Layer 3 interfaces in the VLAN, only the HSRP Active router actively forwards traffic destined for the virtual gateway.

DIST2 remains ready to assume the gateway role.

---

## Failure Scenario

If DIST1 becomes unavailable, DIST2 detects the loss of the Active HSRP router.

DIST2 transitions:

`Standby → Active`

The virtual gateway remains:

`192.168.x.1`

Therefore endpoints do not require a new default gateway.

Conceptually:

Before failure:

`PC → VIP → DIST1`

After failure:

`PC → VIP → DIST2`

The logical gateway remains unchanged.

---

## Recovery Scenario

When DIST1 returns to service, HSRP preemption allows it to reclaim the Active role because it has the higher configured priority.

The topology returns to:

DIST1 = Active

DIST2 = Standby

This provides deterministic gateway ownership during normal operation.

---

## Relationship Between HSRP and OSPF

HSRP and OSPF solve different redundancy problems.

HSRP provides:

**First-hop redundancy**

It protects the endpoint default gateway.

OSPF provides:

**Layer 3 path redundancy**

It determines how routers and Layer 3 switches reach remote networks.

Together they provide two layers of resiliency.

Example traffic flow:

`Endpoint`

↓

`HSRP Virtual Gateway`

↓

`Active Distribution Switch`

↓

`OSPF`

↓

`Core Layer`

This means the campus architecture can survive both gateway and routed-path failures.

---

## Relationship Between HSRP and STP

Spanning Tree Protocol protects the Layer 2 topology from switching loops.

HSRP protects the Layer 3 default gateway.

OSPF protects Layer 3 routed reachability.

Therefore:

`STP = Layer 2 path control`

`HSRP = Default gateway redundancy`

`OSPF = Layer 3 routing redundancy`

These technologies work together to create a resilient campus network.

---

## Verification

HSRP status is verified using:

`show standby brief`

Expected normal state:

DIST1:

`Active`

DIST2:

`Standby`

The output also verifies:

- HSRP group
- priority
- preemption
- Active router
- Standby router
- virtual IP address

---

## Observed Lab Behavior

During implementation, HSRP state transitions were observed directly.

When an SVI or participating device became unavailable, HSRP changed state and the surviving distribution switch assumed the Active role.

Example state transition:

`Standby -> Active`

After connectivity was restored and the preferred router became available, preemption restored the intended Active/Standby roles.

This demonstrated that gateway redundancy was functioning dynamically rather than existing only as a static configuration.

---

## Current Status

HSRP is operational across the campus VLANs.

Validated functionality includes:

- Virtual default gateways
- Active/Standby election
- Priority-based Active router selection
- Preemption
- Gateway failover
- Gateway recovery
- Integration with the redundant Distribution layer

Formal failure and convergence testing will be documented separately in the EIML testing section.
