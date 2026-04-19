# Lab 09: HSRP (Hot Standby Router Protocol)

## Overview
This lab demonstrates **HSRP (Hot Standby Router Protocol)** for first-hop gateway redundancy.

Two PCs are connected to a single switch with different VLANs. Two routers (R1 and R2) provide redundant default gateways using HSRP. R1 acts as the active router by default. If R1 fails, R2 automatically takes over using the shared HSRP virtual IP. We verify redundancy by pinging the ISP router’s G0/2 interface (200.10.10.10).

---

## Lab Objectives
- Configure HSRP on multiple VLANs with virtual IP addresses
- Set HSRP priority and enable preemption
- Demonstrate active/standby roles and automatic failover
- Verify that PCs use the HSRP virtual IP as their default gateway
- Test end-to-end connectivity and redundancy using the ISP’s test interface (200.10.10.10)

---

## Devices & Connections
**Devices Used:**
- SW1 (Layer 2 Switch)
- R1 and R2 (Routers)
- PC1 (VLAN 10 - Sales)
- PC2 (VLAN 20 - Engineering)
- ISP Router

**Connections:**
- PC1 → SW1 FastEthernet0/1 (VLAN 10)
- PC2 → SW1 FastEthernet0/2 (VLAN 20)
- SW1 g0/1 → R1 GigabitEthernet0/0 (trunk)
- SW1 g0/2 → R2 GigabitEthernet0/0 (trunk)
- R1 GigabitEthernet0/1 → ISP GigabitEthernet0/0
- R2 GigabitEthernet0/1 → ISP GigabitEthernet0/1

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**

**HSRP Virtual IPs:**
- VLAN 10: 192.168.10.1
- VLAN 20: 192.168.20.1

**Test Destination:**
- ISP G0/2: 200.10.10.10 (used to test connectivity and failover)

---

## Configuration Files
- [R1 Configuration (Active)](/Labs/09-hsrp/R1-config.txt)
- [R2 Configuration (Standby)](/Labs/09-hsrp/R2-config.txt)
- [SW1 Configuration](/Labs/09-hsrp/SW1-config.txt)

---

## Screenshots
The [images](/Labs/09-hsrp/images) folder should contain visual evidence of:

- Full lab topology showing SW1, R1, R2, PCs, and ISP connections (including ISP G0/2)
- `show standby brief` on R1 (Active) and R2 (Standby)
- PC1 and PC2 IP configuration windows showing the HSRP virtual IP as default gateway
- Successful ping from PC1 and PC2 to 200.10.10.10 under normal conditions
- Failover demonstration:
  - Shut down R1’s G0/1 interface
  - R2 becomes Active
  - PCs can still successfully ping 200.10.10.10

---

## Verification Commands

**On R1 and R2:**
```bash
show standby brief
show standby
