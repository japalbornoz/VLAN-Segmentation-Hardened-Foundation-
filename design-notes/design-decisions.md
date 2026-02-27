# Design Decisions & Architectural Rationale

This document explains the engineering decisions made during the design of Project 01.

---

## 1. Router-on-a-Stick (ROAS) Selection

### Decision
Inter-VLAN routing was implemented using Router-on-a-Stick with 802.1Q subinterfaces.

### Rationale
- Suitable for small branch or lab environments
- Simple to implement and validate
- Clearly demonstrates VLAN tagging and Layer 3 gateway configuration

### Limitation
- Single physical uplink introduces bandwidth bottleneck
- Router becomes a single point of failure
- Does not scale well compared to multilayer switching

---

## 2. Campus Design Function Separation

### Decision
The topology was organized to separate routing, distribution, and access functions:

- Access Layer (SW1, SW3)
- Distribution Layer (SW2)
- Routing Layer (R1)

### Rationale
- Reflects enterprise campus architecture
- Separates access, aggregation, and routing functions
- Improves operational clarity

---

## 3. Management VLAN (VLAN 99)

### Decision
Dedicated VLAN for switch management interfaces.

### Rationale
- Separates management plane from user data traffic
- Reduces exposure of infrastructure devices
- Simulates real enterprise operational standards

---

## 4. Native VLAN 999 (Blackhole VLAN)

### Decision
Configured VLAN 999 as native VLAN with no assigned hosts.

### Rationale
- Prevents user traffic from traversing native VLAN
- Mitigates VLAN hopping risks
- Aligns with trunk hardening best practices

---

## 5. Trunk Hardening

### Decision
- Explicit VLAN allow list
- Native VLAN isolation
- DTP disabled (`switchport nonegotiate`)

### Rationale
- Prevents unauthorized VLAN propagation
- Reduces attack surface
- Ensures predictable trunk behavior

---

## 6. Layer 2 Edge Protection

### Decision
Enabled:
- PortFast
- BPDU Guard
- Shutdown of unused ports

### Rationale
- Accelerates edge device connectivity
- Protects STP topology from rogue switches
- Improves network stability

---

## 7. Why Multilayer Switching Is Preferred in Production

Although ROAS was used for this lab, enterprise environments typically use multilayer switches because:

- Hardware-based routing (ASIC) provides higher throughput
- No router bottleneck
- Better scalability
- Supports redundancy features (HSRP/VRRP/GLBP)

This project establishes foundational inter-VLAN concepts before moving to multilayer switching designs in subsequent projects.

---

## Engineering Summary

This project demonstrates:

- Structured VLAN segmentation
- Controlled Layer 2 domain management
- Basic campus design modeling
- Awareness of scalability limitations
- Application of trunk and edge hardening techniques

The design balances simplicity for lab demonstration with enterprise best practices.
