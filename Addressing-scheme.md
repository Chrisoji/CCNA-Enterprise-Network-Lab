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
| PC-D   | 10   | NIC           | 192.168.10.20 | 255.255.255.0    | 192.168.10.1  | Sales (SW2) |
| PC-B   | 20   | NIC           | 192.168.20.20 | 255.255.255.0    | 192.168.20.1  | Engineering |
| PC-C   | 30   | NIC           | 192.168.30.30 | 255.255.255.0    | 192.168.30.1  | HR |

---

