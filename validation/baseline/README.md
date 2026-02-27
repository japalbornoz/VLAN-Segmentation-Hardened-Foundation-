# Baseline Validation

## Objective
Confirm that the VLAN-segmented Router-on-a-Stick topology is operating normally before evaluating troubleshooting scenarios and design limitations.

## Scope
Baseline validation was performed to verify:

- VLAN presence on the switches
- trunk operation between switching devices and the router uplink
- router subinterface status
- host connectivity to default gateways
- inter-VLAN communication
- management VLAN reachability

## VLAN Verification
The following VLANs were validated in the topology:

- VLAN 10 - IT_ADMIN
- VLAN 20 - ENGINEERING
- VLAN 30 - HR
- VLAN 99 - MANAGEMENT
- VLAN 999 - NATIVE_BLACKHOLE

## Trunk Verification
Trunk links were validated to confirm:

- 802.1Q trunking was operational
- required VLANs were present on trunks
- native VLAN was set correctly
- trunk behavior matched the intended design

## Router-on-a-Stick Verification
Router subinterfaces were validated to confirm:

- each VLAN had a corresponding 802.1Q subinterface
- default gateway IP addresses were configured correctly
- Layer 3 inter-VLAN routing was operational

## Connectivity Verification
Baseline testing confirmed:

- hosts could reach their configured default gateways
- hosts in different VLANs could communicate successfully
- management VLAN connectivity was functional

## Commands Used
The following commands were used during baseline validation:

```plaintext
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
ping <default-gateway>
ping <remote-host>
```
