# Lab 07: ACLs and NAT

## Overview
This lab demonstrates the combined use of **Access Control Lists (ACLs)** and **Network Address Translation (NAT/PAT)**.

Two VLANs (10 - Sales and 20 - Engineering) are allowed to communicate with the outside server using NAT.  
VLAN 30 (Test Device) is deliberately **denied** by both the Standard ACL and Extended ACL to clearly show traffic control and its impact on NAT translation.

---

## Lab Objectives
- Configure Standard and Extended ACLs to control traffic
- Configure NAT Overload (PAT) for selected VLANs only
- Use VLAN 30 (Test Device) to demonstrate ACL blocking
- Show how ACLs affect both outbound traffic and NAT translation
- Understand the interaction between ACLs and NAT in enterprise networks

---

## Devices & Connections
**Devices Used:**
- R1 (Router)
- SW1 (Layer 2 Switch)
- PC1 (VLAN 10 - Sales)
- PC2 (VLAN 20 - Engineering)
- PC3 (VLAN 30 - Test Device)
- Server-PT (Outside server)

**Connections:**
- R1 G0/0/0 → SW1 F0/1 (Trunk)
- R1 G0/0/1 → Server-PT FastEthernet0 (Outside)
- PC1 → SW1 F0/2 (VLAN 10)
- PC2 → SW1 F0/3 (VLAN 20)
- PC3 → SW1 F0/4 (VLAN 30)

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**

---

## Configuration Files
- [R1 Configuration (ACLs + NAT)](/Labs/07-standard-and-extended-acls-with-nat/R1-config.txt)
- [SW1 Configuration](/Labs/07-standard-and-extended-acls-with-nat/SW1-config.txt)

---

## Testing Scenarios (Using VLAN 30 as Test Device)

We will demonstrate the following key behaviors:

1. **NAT Translation Behavior**
   - VLAN 10 (PC1) and VLAN 20 (PC2) are permitted by Extended ACL 101 → They receive NAT translation.
   - VLAN 30 (PC3 - Test Device) is **not** permitted by Extended ACL 101 → No NAT translation occurs.

2. **Standard ACL Blocking (on VLAN 30)**
   - Standard ACL 10 explicitly denies VLAN 30 on interface G0/0/0.30.
   - This blocks outbound traffic from the Test Device.

3. **Extended ACL Blocking (on VLAN 30)**
   - Extended ACL 101 denies traffic from 192.168.30.0/24.
   - PC3 cannot reach the Server and receives no NAT translation.

4. **Overall ACL + NAT Interaction**
   - Only permitted VLANs (10 and 20) can successfully communicate with the outside server using NAT.
   - VLAN 30 is blocked at both the Standard and Extended ACL levels.

---

## Screenshots
The [images](/Labs/07-standard-and-extended-acls-with-nat/images) folder should contain visual evidence of:

- Full lab topology showing all devices and VLANs
- `show access-lists` on R1 (showing both ACL 10 and ACL 101)
- `show ip nat translations` while PC1 and PC2 are pinging the server (showing active translations)
- `show ip nat translations` while PC3 (Test Device) tries to ping the server (no translation entries)
- Ping results from each PC to the Server (203.0.113.10):
  - PC1 (VLAN 10) → Successful
  - PC2 (VLAN 20) → Successful
  - PC3 (VLAN 30 - Test Device) → Failed
- `show running-config | section access-list|nat|interface`

---

## Verification Commands (on R1)

```bash
show access-lists
show ip nat translations
show ip nat statistics
show ip interface GigabitEthernet0/0/0.30
