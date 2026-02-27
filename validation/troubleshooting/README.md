# Common Troubleshooting and Failure Scenarios

This section documents common failure scenarios encountered in VLAN-based campus environments and the structured troubleshooting approach used to resolve them.

---

## Troubleshooting Methodology

The following layered approach was applied:

1. Verify physical and link status
2. Validate Layer 2 configuration (VLAN / trunking / STP)
3. Validate Layer 3 configuration (subinterfaces / gateway IPs)
4. Perform targeted ping testing
5. Inspect configuration consistency across devices

---

## Scenario 1 – Host Cannot Reach Default Gateway

### Symptoms
- Host unable to ping its configured default gateway
- `Request timed out` during testing

### Root Cause
Incorrect VLAN assignment on access interface.

### Validation Commands
    show vlan brief
    show running-config interface fa0/x

### Resolution
    interface fa0/x
    switchport mode access
    switchport access vlan <correct VLAN>

---

## Scenario 2 – Inter-VLAN Routing Failure

### Symptoms
- Hosts can reach their own gateway
- Cannot communicate with hosts in other VLANs

### Root Cause
Missing or incorrect 802.1Q encapsulation on router subinterface.

### Validation Commands
    show ip interface brief
    show vlan brief
    show interfaces trunk
    show running-config interface g0/0.X

### Resolution
    interface g0/0.<VLAN_ID>
    encapsulation dot1Q <VLAN_ID>
    ip address <gateway IP> <subnet mask>
    
---

## Scenario 3 – Native VLAN Mismatch

### Symptoms
- STP warnings
- Unstable trunk behavior
- Inconsistent connectivity

### Root Cause
Native VLAN not aligned across trunk links.

### Validation Commands
    show interfaces trunk

### Resolution    
    switchport trunk native vlan 999


Applied consistently across all trunk links.

---

## Scenario 4 – VLAN Not Passing Across Trunk

### Symptoms
- Devices in same VLAN on different switches cannot communicate

### Root Cause
VLAN missing from trunk allowed list.

### Validation Commands
    show interfaces trunk


### Resolution
    switchport trunk allowed vlan 10,20,30,99,999

Explicit VLAN allow-list configured.

---

## Scenario 5 – Management VLAN Unreachable

### Symptoms
- Unable to SSH/ping switch management IP
- Vlan99 interface up/down inconsistently

### Root Cause
VLAN 99 not created or not allowed on trunk links.

### Validation Commands
    show vlan brief
    show interfaces trunk
    show ip interface brief

### Resolution
- Create VLAN 99
- Assign IP to `interface Vlan99`
- Ensure VLAN 99 is allowed on trunk links
- Configure correct `ip default-gateway`

---

## Scenario 6 – STP Edge Port Protection Triggered

### Symptoms
- Port enters err-disabled state
- BPDU Guard violation message

### Root Cause
Rogue switch connected to PortFast-enabled interface.

### Validation Commands
    show spanning-tree summary
    show interfaces status

### Resolution
- Remove unauthorized device
- Re-enable interface:
```plaintext
shutdown
no shutdown
```

---

## Observations

- Consistency across trunk links is critical.
- VLAN database and trunk configuration must always be validated together.
- Router-on-a-Stick designs introduce a single point of failure.
- Management plane separation improves operational security.

---

## Engineering Takeaways

- Always validate Layer 2 before troubleshooting Layer 3.
- Use structured command verification rather than guessing.
- Harden trunks early to prevent broadcast domain leakage.
- Native VLAN should never carry production traffic.

    
