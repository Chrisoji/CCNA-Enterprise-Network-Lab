# Lab 02: VLANs and Trunking

## Overview
This lab covers two fundamental CCNA topics: **VLANs** and **Trunking**. 

Virtual Local Area Networks (VLANs) are used to logically segment a physical network into separate broadcast domains. Trunking allows multiple VLANs to travel over a single link between switches using the 802.1Q protocol. This lab demonstrates how to create VLANs, assign access ports, and configure a trunk link so that devices in the same VLAN can communicate across switches.

---

## Lab Objectives
- Create and name VLANs on multiple switches
- Assign access ports to specific VLANs
- Configure an 802.1Q trunk link between switches
- Configure management SVIs on a dedicated VLAN
- Verify VLAN propagation and trunk operation
- Test intra-VLAN connectivity across switches

---

## Devices & Connections
**Devices Used:**
- SW1 (Cisco Layer 2 Switch)
- SW2 (Cisco Layer 2 Switch)
- PC-A (VLAN 10 - Sales)
- PC-B (VLAN 20 - Engineering)
- PC-C (VLAN 30 - HR)
- PC-D (VLAN 10 - Sales)

**Connections:**
- PC-A → SW1 GigabitEthernet0/1
- PC-C → SW1 FastEthernet0/1
- PC-B → SW2 GigabitEthernet0/2
- PC-D → SW2 FastEthernet0/1
- SW1 GigabitEthernet0/2 ↔ SW2 GigabitEthernet0/1 (Trunk link)
- Straight-through cables from PCs to Switches 

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**


---

## Configuration Files
The full device configurations for this lab are available here:

- [SW1 Configuration](/Labs/02-vlans-and-trunking/SW1-config.txt)
- [SW2 Configuration](/Labs/02-vlans-and-trunking/SW2-config.txt)

---

## Screenshots
The [images](/Labs/02-vlans-and-trunking/images) folder contains screenshots showing:
- Full lab topology
- `show vlan brief` output on SW1 and SW2
- `show interfaces trunk` output on both switches
- Successful ping from PC-A (VLAN 10 on SW1) to PC-D (VLAN 10 on SW2)
- Management ping between SW1 and SW2 (VLAN 99)
- VLAN separation test (ping failure between different VLANs)

---

## Verification Commands
After applying the configurations, use these commands to verify:

show vlan brief

show interfaces trunk

show interfaces switchport

show running-config | section vlan|interface

ping 192.168.10.11

ping 192.168.99.2    
