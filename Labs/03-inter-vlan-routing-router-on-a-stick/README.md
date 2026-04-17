# Lab 03: Inter-VLAN Routing (Router-on-a-Stick)

## Overview
This lab is a **continuation and addition to Lab 02 (VLANs and Trunking)**. 

In Lab 02 we configured VLANs and trunking between SW1 and SW2. In this lab, we extend that setup by adding a router (R1) to enable **Inter-VLAN Routing**. 

We use the **Router-on-a-Stick (ROAS)** method, where a single physical router interface carries traffic for multiple VLANs using subinterfaces and 802.1Q encapsulation. Only the new configurations required for inter-VLAN routing are shown here (router subinterfaces and the new trunk port on SW1).

---

## Lab Objectives
- Configure a trunk link from SW1 to the router
- Create subinterfaces on the router with proper 802.1Q encapsulation
- Assign IP addresses to subinterfaces as default gateways for each VLAN
- Set default gateways on PCs
- Verify routing between different VLANs
- Understand how Router-on-a-Stick enables inter-VLAN communication

---

## Devices & Connections
**Devices Used:**
- R1 (Cisco Router)
- SW1 (Cisco Layer 2 Switch)
- SW2 (Cisco Layer 2 Switch)
- PC-A (VLAN 10), PC-B (VLAN 20), PC-C (VLAN 30), PC-D (VLAN 10)

**Connections:**
- Same connections as Lab 02:
  - PC-A → SW1 GigabitEthernet0/1 (VLAN 10)
  - PC-C → SW1 FastEthernet0/1 (VLAN 30)
  - PC-B → SW2 GigabitEthernet0/2 (VLAN 20)
  - PC-D → SW2 FastEthernet0/1 (VLAN 10)
  - SW1 GigabitEthernet0/2 ↔ SW2 GigabitEthernet0/1 (Trunk)
- **New connection**: R1 GigabitEthernet0/0/0 ↔ SW1 **FastEthernet0/2** (Trunk to Router)

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**

**Default Gateways:**
- PCs use the router subinterface IP in their VLAN as the default gateway.

---

## Configuration Files
Only the **new configurations** for inter-VLAN routing are provided:

- [R1 Configuration](/Labs/03-inter-vlan-routing-router-on-a-stick/R1-config.txt) ← Subinterfaces on G0/0/0
- [SW1 Configuration](/Labs/03-inter-vlan-routing-router-on-a-stick/SW1-config.txt) ← New trunk port to R1 (FastEthernet0/2)

**Note:** SW2 configuration remains the same as Lab 02.

---

## Screenshots
To show successful completion of this lab, include the following screenshots in the [images](/Labs/03-inter-vlan-routing-router-on-a-stick/images) folder:

- Full lab topology showing R1 connected to SW1 via FastEthernet0/24
- `show ip interface brief` on R1 (showing all subinterfaces up/up)
- `show running-config | section interface` on R1 (showing subinterfaces and encapsulation)
- `show interfaces trunk` on SW1 (showing trunk to R1 and allowed VLANs)
- Successful inter-VLAN ping tests:
  - PC-A (192.168.10.10) → PC-B (192.168.20.20)
  - PC-A (192.168.10.10) → PC-C (192.168.30.30)
  - PC-D (192.168.10.11) → PC-B (192.168.20.20)
  - PC-D (192.168.10.11) → PC-C (192.168.30.30)
- `show ip route` on R1
- Ping from PC in one VLAN to PC in another VLAN (multiple examples)

---

## Verification Commands
Use these commands after applying the configurations:

```bash
! On Router R1
show ip interface brief
show ip route
show running-config | section interface

! On SW1
show interfaces trunk
show vlan brief

! Inter-VLAN connectivity tests (run from PCs)
ping 192.168.20.20     ! From PC-A or PC-D to PC-B (VLAN 10 to VLAN 20)
ping 192.168.30.30     ! From PC-A to PC-C (VLAN 10 to VLAN 30)
