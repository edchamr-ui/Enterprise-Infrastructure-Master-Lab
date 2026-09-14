# Campus Routing Troubleshooting Log

## Enterprise Infrastructure Master Lab

This document records routing and high-availability issues encountered
during implementation of the EIML campus network.

The purpose is to preserve the troubleshooting methodology, diagnostic
commands, root causes, and resolutions discovered during the lab.

---

# Incident CR-01 - Missing OSPF Routes

## Symptoms

OSPF neighbour relationships were successfully established between the
distribution and core switches, but some campus VLAN networks were not
appearing in the OSPF routing tables.

The affected networks included:

- 192.168.30.0/24
- 192.168.40.0/24
- 192.168.50.0/24
- 192.168.99.0/24

## Investigation

OSPF configuration was inspected using:

```text
show running-config | section router ospf


```

## Root Cause

The remaining SVI networks had not been added to OSPF process 1.

OSPF adjacency alone does not automatically advertise every connected
network. The appropriate interfaces or networks must participate in the
OSPF process before those networks can be advertised.

## Resolution

The missing VLAN networks were added to OSPF area 0:

```text
router ospf 1
 network 192.168.30.0 0.0.0.255 area 0
 network 192.168.40.0 0.0.0.255 area 0
 network 192.168.50.0 0.0.0.255 area 0
 network 192.168.99.0 0.0.0.255 area 0
```

## Verification

The following commands were used:

```text
show ip ospf neighbor
show ip ospf route
show ip route ospf
```

The missing networks subsequently appeared in OSPF.

**Incident Status: RESOLVED**

---

# Incident CR-02 - HSRP Gateway Temporarily Unreachable During Failover

## Symptoms

During high-availability testing, a VPCS client was continuously pinging
the VLAN 10 HSRP virtual gateway:

```text
VPCS> ping 192.168.10.1
```

The gateway initially responded successfully.

When the primary distribution switch, DIST1, was taken offline, several
consecutive ICMP requests timed out.

## Investigation

HSRP state was checked on DIST2:

```text
show standby brief
```

DIST2 transitioned from the Standby state to the Active state and assumed
ownership of the HSRP virtual gateway.

The virtual gateway remained:

```text
192.168.10.1
```

OSPF operation was also checked using:

```text
show ip ospf neighbor
show ip route ospf
```

DIST2 maintained FULL OSPF adjacencies with both core switches:

```text
1.1.1.1
2.2.2.2
```

This confirmed that the surviving distribution switch retained Layer 3
connectivity into the redundant core.

## Root Cause

The temporary packet loss was caused by the convergence period following
failure of the current HSRP Active router.

HSRP had to detect the loss of DIST1 and transition DIST2 from Standby to
Active before the virtual gateway could resume forwarding through DIST2.

The virtual gateway IP address itself did not change.

## Resolution

No client-side intervention was required.

After HSRP convergence:

```text
DIST2 = Active
Virtual Gateway = 192.168.10.1
```

Connectivity automatically resumed.

Approximately five consecutive ICMP requests were observed timing out
during the failover event.

**Incident Status: EXPECTED FAILOVER BEHAVIOUR / RESOLVED**

---

# Incident CR-03 - Primary Distribution Recovery and HSRP Preemption

## Scenario

After validating operation through DIST2, DIST1 was restored.

The expected design behaviour was for DIST1 to become the preferred HSRP
Active router again.

## Investigation

The configured priorities were:

```text
DIST1 priority = 110
DIST2 priority = 100
```

HSRP preemption was enabled on both distribution switches.

The state was verified using:

```text
show standby brief
```

## Observed Behaviour

After DIST1 recovered:

1. DIST1 interfaces returned to service.
2. OSPF neighbour relationships were re-established.
3. Dynamic routing reconverged.
4. HSRP detected the higher-priority DIST1 router.
5. DIST1 preempted DIST2.
6. DIST1 became Active.
7. DIST2 returned to Standby.

Final state:

```text
DIST1 = Active
DIST2 = Standby
```

Client connectivity was then tested:

```text
VPCS> ping 192.168.10.1
```

Successful ICMP replies were received.

**Incident Status: SUCCESSFUL RECOVERY**

---

# Troubleshooting Lessons Learned

The campus implementation and failure testing demonstrated several
important operational principles.

1. OSPF adjacency does not mean every connected network is automatically
   advertised.

2. `show running-config | section router ospf` can be used to verify
   which networks have been included in the routing process.

3. `show ip ospf neighbor` verifies OSPF adjacency, while
   `show ip route ospf` verifies the routes actually learned through OSPF.

4. HSRP separates the client default gateway from the IP address of a
   specific physical distribution switch.

5. High availability does not necessarily mean zero packet loss.

6. Convergence behaviour should be actively tested rather than assuming
   redundancy works because the configuration appears correct.

7. OSPF and HSRP solve different redundancy problems:
   OSPF provides dynamic Layer 3 path selection while HSRP provides
   first-hop gateway redundancy for end hosts.

8. HSRP preemption allows the preferred higher-priority router to reclaim
   the Active role following recovery.

9. Continuous ICMP testing is a simple but effective method of observing
   service interruption and recovery during a controlled failure test.

10. A redundant architecture should be validated through failure,
    convergence, recovery, and restoration to its intended steady state.

---

# Current Campus Routing Status

At completion of this testing phase:

- OSPF adjacencies are operational.
- Campus VLAN networks are participating in OSPF.
- DIST1 is the preferred HSRP Active router.
- DIST2 operates as the HSRP Standby router.
- HSRP virtual gateways are operational.
- Distribution-layer failover has been successfully tested.
- Automatic recovery and HSRP preemption have been successfully tested.
- Client connectivity through the virtual gateway has been verified.

The campus routing and first-hop redundancy implementation is therefore
considered operational and ready for the next EIML implementation phase.
