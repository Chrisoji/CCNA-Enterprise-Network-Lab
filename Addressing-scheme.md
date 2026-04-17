# Basic Initial Configuration

## Lab 01 – Basic Initial Configuration – Addressing Scheme

This section defines the IP addressing plan for initial device management and connectivity setup.

---

## Device Addressing Table

| Device | Interface | IP Address   | Subnet Mask     | Default Gateway | Purpose |
|--------|----------|-------------|----------------|----------------|---------|
| R1     | G0/0/0   | 192.168.1.1 | 255.255.255.0  | N/A            | Management / connectivity |
| SW1    | VLAN 1   | 192.168.1.2 | 255.255.255.0  | 192.168.1.1    | Management IP |



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

