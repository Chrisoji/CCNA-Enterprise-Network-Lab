# Basic Initial Configuration

## Lab 01 – Basic Initial Configuration – Addressing Scheme

This section defines the IP addressing plan for initial device management and connectivity setup.

---

## Device Addressing Table

| Device | Interface | IP Address   | Subnet Mask     | Default Gateway | Purpose |
|--------|----------|-------------|----------------|----------------|---------|
| R1     | G0/0/0   | 192.168.1.1 | 255.255.255.0  | N/A            | Management / connectivity |
| SW1    | VLAN 1   | 192.168.1.2 | 255.255.255.0  | 192.168.1.1    | Management IP |

---


# Vlans & Trunking 
## Lab 02 - VLANs and Trunking – Addressing Scheme

This section defines the IP addressing plan for VLAN segmentation and trunking configuration. Each VLAN represents a separate broadcast domain mapped to specific departments.

---

## VLAN Management and End Devices

| Device | VLAN | Interface | IP Address     | Subnet Mask       | Purpose |
|--------|------|-----------|---------------|------------------|---------|
| SW1    | 99   | VLAN 99   | 192.168.99.1  | 255.255.255.0    | Management |
| SW2    | 99   | VLAN 99   | 192.168.99.2  | 255.255.255.0    | Management |
| PC-A   | 10   | NIC       | 192.168.10.10 | 255.255.255.0    | Sales (connected to SW1) |
| PC-B   | 20   | NIC       | 192.168.20.20 | 255.255.255.0    | Engineering (connected to SW2) |
| PC-C   | 30   | NIC       | 192.168.30.30 | 255.255.255.0    | HR (connected to SW1) |
| PC-D   | 10   | NIC       | 192.168.10.11 | 255.255.255.0    | Sales (connected to SW2) |

---


# Inter-VLAN Routing(Router-on-a-stick)
## Lab 03: Inter-VLAN Routing – Addressing Scheme

This section defines the IP addressing plan for inter-VLAN routing using a router-on-a-stick configuration. Each VLAN has a dedicated subnet, and the router provides Layer 3 gateway functionality for communication between VLANs.

---

## VLAN Gateways and End Devices

| Device | VLAN | Interface     | IP Address     | Subnet Mask       | Default Gateway | Purpose |
|--------|------|---------------|---------------|------------------|----------------|---------|
| R1     | 10   | G0/0/0.10     | 192.168.10.1  | 255.255.255.0    | N/A            | Gateway for VLAN 10 |
| R1     | 20   | G0/0/0.20     | 192.168.20.1  | 255.255.255.0    | N/A            | Gateway for VLAN 20 |
| R1     | 30   | G0/0/0.30     | 192.168.30.1  | 255.255.255.0    | N/A            | Gateway for VLAN 30 |
| SW1    | 99   | VLAN 99       | 192.168.99.1  | 255.255.255.0    | 192.168.99.1  | Switch management |
| SW2    | 99   | VLAN 99       | 192.168.99.2  | 255.255.255.0    | 192.168.99.1  | Switch management |
| PC-A   | 10   | NIC           | 192.168.10.10 | 255.255.255.0    | 192.168.10.1  | Sales (SW1) |
| PC-D   | 10   | NIC           | 192.168.10.11 | 255.255.255.0    | 192.168.10.1  | Sales (SW2) |
| PC-B   | 20   | NIC           | 192.168.20.20 | 255.255.255.0    | 192.168.20.1  | Engineering |
| PC-C   | 30   | NIC           | 192.168.30.30 | 255.255.255.0    | 192.168.30.1  | HR |

---

# Port Security
## Lab 04: Port Security – Addressing Scheme

This section defines the IP addressing plan for demonstrating port security on a Layer 2 switch. All devices are placed in the same VLAN to focus on access control rather than routing.

---

## End Devices

| Device       | VLAN | Interface | IP Address     | Subnet Mask       | Default Gateway | Purpose |
|-------------|------|-----------|---------------|------------------|----------------|---------|
| PC-A        | 10   | NIC       | 192.168.10.10 | 255.255.255.0    | N/A            | Test device |
| PC-B        | 10   | NIC       | 192.168.10.20 | 255.255.255.0    | N/A            | Legitimate user |
| PC-C        | 10   | NIC       | 192.168.10.30 | 255.255.255.0    | N/A            | Legitimate user |
| PC-Attacker | 10   | NIC       | 192.168.10.99 | 255.255.255.0    | N/A            | Test device |


## Switch Ports

| Switch | Interface | Connected Device |
|--------|-----------|------------------|
| SW1    | F0/1      | PC-A             |
| SW1    | F0/2      | PC-B             |
| SW1    | F0/3      | PC-C             |
| SW1    | F0/4      | PC-Attacker      |

---


# DHCP Configuration (Server and Relay)
## Lab 05: DHCP Configuration – Addressing Scheme

This section defines the IP addressing and DHCP allocation plan for dynamic host configuration across multiple VLANs.  
Router R1 functions as both the **default gateway** and **DHCP server** using a router-on-a-stick design.

---

## VLAN and Subnet Plan

| VLAN | VLAN Name   | Subnet            | Default Gateway | DHCP Pool Range                | Excluded Addresses          |
|------|-------------|------------------|-----------------|-------------------------------|-----------------------------|
| 10   | Sales       | 192.168.10.0/24  | 192.168.10.1    | 192.168.10.6 – 192.168.10.254 | 192.168.10.1 – 192.168.10.5 |
| 20   | Engineering | 192.168.20.0/24  | 192.168.20.1    | 192.168.20.6 – 192.168.20.254 | 192.168.20.1 – 192.168.20.5 |
| 30   | HR          | 192.168.30.0/24  | 192.168.30.1    | 192.168.30.6 – 192.168.30.254 | 192.168.30.1 – 192.168.30.5 |
| 99   | Management  | 192.168.99.0/24  | 192.168.99.1    | N/A                           | N/A                         |


## Router (R1) Subinterfaces

| Interface              | VLAN | IP Address      | Subnet Mask     | Purpose                         |
|------------------------|------|-----------------|-----------------|---------------------------------|
| G0/0/0.10              | 10   | 192.168.10.1    | 255.255.255.0   | Gateway + DHCP Server           |
| G0/0/0.20              | 20   | 192.168.20.1    | 255.255.255.0   | Gateway + DHCP Server           |
| G0/0/0.30              | 30   | 192.168.30.1    | 255.255.255.0   | Gateway + DHCP Server           |


## Switch Management Interfaces

| Device | VLAN | Interface | IP Address     | Subnet Mask       | Default Gateway |
|--------|------|-----------|---------------|------------------|----------------|
| SW1    | 99   | VLAN 99   | 192.168.99.1  | 255.255.255.0    | 192.168.99.1   |
| SW2    | 99   | VLAN 99   | 192.168.99.2  | 255.255.255.0    | 192.168.99.1   |


## End Devices (DHCP Clients)

| Device | VLAN | Interface | IP Assignment | Default Gateway |
|--------|------|-----------|---------------|----------------|
| PC-A   | 10   | NIC       | DHCP          | 192.168.10.1   |
| PC-D   | 10   | NIC       | DHCP          | 192.168.10.1   |
| PC-B   | 20   | NIC       | DHCP          | 192.168.20.1   |
| PC-C   | 30   | NIC       | DHCP          | 192.168.30.1   |

---


# Etherchannel
## Lab 06: EtherChannel (Layer 2 with LACP) – Addressing Scheme

This section defines the IP addressing plan for demonstrating Layer 2 EtherChannel between switches using LACP.  
All devices are placed in a single VLAN to focus on link aggregation, redundancy, and load balancing.

---

## VLAN and Subnet Plan

| VLAN | VLAN Name | Subnet            | Default Gateway | Purpose                        |
|------|-----------|------------------|-----------------|--------------------------------|
| 10   | Users     | 192.168.10.0/24  | N/A             | End-user devices and testing   |


## End Devices

| Device | VLAN | Interface | IP Address     | Subnet Mask       | Default Gateway | Purpose              |
|--------|------|-----------|---------------|------------------|----------------|----------------------|
| PC-A   | 10   | NIC       | 192.168.10.10 | 255.255.255.0    | N/A            | Connected to SW1     |
| PC-B   | 10   | NIC       | 192.168.10.20 | 255.255.255.0    | N/A            | Connected to SW2     |

---


# ACLs and NAT
## Lab 07: ACLs and NAT – Addressing Scheme

This section defines the IP addressing plan for inter-VLAN routing, access control using ACLs, and Network Address Translation (NAT/PAT).  
Router R1 acts as the default gateway for internal VLANs and translates private IP addresses to a public IP for external access.

---

## VLAN and Subnet Plan

| VLAN | VLAN Name   | Subnet            | Default Gateway |
|------|-------------|------------------|-----------------|
| 10   | Sales       | 192.168.10.0/24  | 192.168.10.1    |
| 20   | Engineering | 192.168.20.0/24  | 192.168.20.1    |


## Inside Network (End Devices)

| Device | VLAN | Interface | IP Address     | Subnet Mask       | Default Gateway | Purpose          |
|--------|------|-----------|---------------|------------------|----------------|------------------|
| PC1    | 10   | NIC       | 192.168.10.10 | 255.255.255.0    | 192.168.10.1   | Sales PC         |
| PC2    | 20   | NIC       | 192.168.20.20 | 255.255.255.0    | 192.168.20.1   | Engineering PC   |


## Router (R1) Interfaces

| Interface     | VLAN | IP Address     | Subnet Mask       | Role                          |
|---------------|------|---------------|------------------|-------------------------------|
| G0/0/0.10     | 10   | 192.168.10.1  | 255.255.255.0    | Inside (Gateway VLAN 10)      |
| G0/0/0.20     | 20   | 192.168.20.1  | 255.255.255.0    | Inside (Gateway VLAN 20)      |
| G0/0/1        | N/A  | 203.0.113.1   | 255.255.255.240  | Outside (Public/NAT interface)|


## Outside Network (Simulated Internet)

| Device        | Interface | IP Address     | Subnet Mask       | Purpose                      |
|---------------|-----------|---------------|------------------|------------------------------|
| Cloud/Server  | Ethernet6 | 203.0.113.10  | 255.255.255.240  | External web/server endpoint |


## NAT Configuration Summary

| Type            | Value |
|-----------------|-------|
| Inside Local    | 192.168.10.0/24, 192.168.20.0/24 |
| Inside Global   | 203.0.113.1 (PAT overload) |
| Outside Global  | 203.0.113.10 |


## Switch Management (Optional)

| Device | VLAN | Interface | IP Address     | Subnet Mask       | Default Gateway |
|--------|------|-----------|---------------|------------------|----------------|
| SW1    | 99   | VLAN 99   | 192.168.99.1  | 255.255.255.0    | N/A            |

---

