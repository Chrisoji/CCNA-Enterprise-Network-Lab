# Lab 06: EtherChannel (Layer 2 with LACP)

## Overview
This lab covers **EtherChannel**, a link aggregation technology that bundles multiple physical links between switches to provide increased bandwidth and redundancy.

In this lab, we configure **Layer 2 EtherChannel using LACP (Link Aggregation Control Protocol)** between SW1 and SW2. 

---

## Lab Objectives
- Configure Layer 2 EtherChannel using LACP (Active mode)
- Create a Port-Channel interface
- Assign the Port-Channel to a VLAN
- Verify EtherChannel formation and load balancing
- Test redundancy by shutting down one physical link

---

## Devices & Connections
**Devices Used:**
- SW1 and SW2 (Cisco Layer 2 Switches)
- PC-A and PC-B

**Connections:**
- EtherChannel Bundle: SW1 f0/1 + f0/2 ↔ SW2 f0/1 + f0/2
- PC-A → SW1 f0/3 (VLAN 10)
- PC-B → SW2 f0/3 (VLAN 10)

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**

- PC-A: 192.168.10.10/24 (VLAN 10)
- PC-B: 192.168.10.20/24 (VLAN 10)

---

## Configuration Files
The EtherChannel configurations are available here:

- [SW1 Configuration](/Labs/06-etherchannel/SW1-config.txt)
- [SW2 Configuration](/Labs/06-etherchannel/SW2-config.txt)

---

## Screenshots
The [images](/Labs/06-etherchannel/images) folder should contain:

- Full lab topology showing the EtherChannel bundle and both PCs
- `show etherchannel summary` on SW1 and SW2 (should show Po1(SU) and physical ports as (P))
- `show etherchannel 1 summary` and `show port-channel 1`
- `show running-config | section interface` on both switches
- Successful pings between PC-A and PC-B
- Redundancy test: One physical link shut down, ping still successful

---

## Verification Commands

**On both switches:**
```bash
show etherchannel summary
show etherchannel 1 summary
show port-channel 1
show interfaces port-channel 1
