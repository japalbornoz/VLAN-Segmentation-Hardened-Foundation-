# Validation

## Purpose
This folder contains validation, design rationale, and troubleshooting documentation for Project 01: a VLAN-segmented campus LAN using Router-on-a-Stick (ROAS).

The goal of validation was to confirm that:

- VLAN segmentation was operating correctly
- trunk links were carrying the required VLANs
- Router-on-a-Stick inter-VLAN routing was functioning
- management VLAN connectivity was working
- Layer 2 hardening and structured troubleshooting concepts were documented

## Folder Contents

- `baseline/`  
  Baseline validation outputs and summary of normal network operation.

- `design-notes.md`  
  Engineering decisions and architectural rationale for the lab design.

- `failure-scenarios.md`  
  Common troubleshooting scenarios, validation commands, and corrective actions relevant to the topology.

## Validation Summary
Baseline validation confirmed:

- VLANs were created and assigned correctly
- trunk links carried the required VLANs
- router subinterfaces provided inter-VLAN routing
- hosts could reach their default gateways
- hosts in different VLANs could communicate successfully
- management VLAN connectivity was operational

## Result
Project 01 successfully demonstrated foundational campus LAN concepts using VLAN segmentation, Router-on-a-Stick, trunk hardening, and management plane separation.
