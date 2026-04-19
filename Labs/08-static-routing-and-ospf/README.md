# Lab 08: Static Routing (IPv4 & IPv6) + OSPFv2

## Overview
This lab demonstrates routing between two routers (R1 and R2). 

We configure **static IPv4 and IPv6 routing** as well as **OSPFv2** so that both routers can reach each other’s networks and share routing information dynamically.

---

## Lab Objectives
- Configure static IPv4 and IPv6 routes
- Configure OSPFv2 (single area) between two routers
- Observe OSPF adjacency and DR/BDR election
- Verify that routers can reach remote networks using both static and dynamic routing
- Compare static routing versus OSPF

---

## Devices & Connections
**Devices Used:**
- R1
- R2

**Connections:**
- R1 GigabitEthernet0/0/0 ↔ R2 GigabitEthernet0/0/0

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**

---

## Configuration Files
- [R1 Configuration](/Labs/08-static-routing-and-ospf/R1-config.txt)
- [R2 Configuration](/Labs/08-static-routing-and-ospf/R2-config.txt)

---

## Screenshots
The [images](/Labs/08-static-routing-and-ospf/images) folder should contain:

- Full topology showing R1 and R2 connected
- `show ip route` and `show ipv6 route` on both routers
- `show ip ospf neighbor` on both routers (showing FULL state and DR/BDR roles)
- Successful pings:
  - From R1 to R2 Loopback0 (172.16.2.1 and 2001:db8:aaaa::1)

---

## Verification Commands

**On both routers:**
```bash
show ip route
show ipv6 route
show ip ospf neighbor
show ip ospf interface
ping 172.16.2.1          ! From R1
ping 2001:db8:aaaa::1   ! From R1 (IPv6)
