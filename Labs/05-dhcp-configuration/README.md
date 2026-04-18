# Lab 05: DHCP Configuration (Server and Relay)

## Overview
This lab covers **DHCP (Dynamic Host Configuration Protocol)** configuration. 

R1 is configured as a DHCP Server to automatically assign IP addresses, default gateways, and DNS servers to devices across multiple VLANs. This eliminates manual IP configuration on end devices and demonstrates a very common real-world enterprise network task.

---

## Lab Objectives
- Configure multiple DHCP pools on a router for different VLANs
- Exclude router interface IPs from DHCP assignment
- Set default gateway and DNS server options in DHCP pools
- Verify that PCs automatically receive IP addresses via DHCP
- Test connectivity after DHCP assignment

---

## Devices & Connections
**Devices Used:**
- R1 (Router – DHCP Server)
- SW1 and SW2 (Layer 2 Switches)
- PC-A (VLAN 10), PC-B (VLAN 20), PC-C (VLAN 30), PC-D (VLAN 10)

**Connections:**
- Same Router-on-a-Stick topology as Lab 03
- R1 GigabitEthernet0/0/0 ↔ SW1 FastEthernet0/2 (Trunk link)
- SW1 trunked to SW2
- PCs connected to their respective access ports

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**

PCs receive IP addresses dynamically from R1’s DHCP pools.

---

## Configuration Files
The DHCP server configuration is available here:

- [R1 Configuration (DHCP Server)](/Labs/05-dhcp-configuration/R1-config.txt)

**Note:** SW1 and SW2 use the trunk configurations from previous labs.

---

## Screenshots
The [images](/Labs/05-dhcp-configuration/images) folder contains visual evidence of:

- Full lab topology showing R1, SW1, SW2, and all PCs
- DHCP configuration on R1 (`show running-config | section dhcp` and `show ip dhcp pool`)
- DHCP bindings on R1 (`show ip dhcp binding`)
- PCs successfully receiving IP addresses via DHCP (IP Configuration windows for PC-A, PC-B, PC-C, PC-D)
- Ping tests from **PC-A** to all other PCs:
  - PC-A to PC-B (VLAN 10 → VLAN 20)
  - PC-A to PC-C (VLAN 10 → VLAN 30)
  - PC-A to PC-D (VLAN 10 → VLAN 10 across switches)
- `show ip interface brief` on R1

---

## Verification Commands

**On Router R1:**
```bash
show ip dhcp binding
show ip dhcp pool
show ip interface brief
show running-config | section dhcp
