# Lab 01: Basic Initial Configuration

## Overview
This lab covers the essential first step in building any enterprise network: **basic initial configuration** on Cisco routers and switches.

These foundational configurations include hostnames, security settings, management IPs, and remote access setup. This provides the base for all subsequent labs in this repository.

---

## Lab Objectives
- Configure device hostnames and banners
- Secure console and VTY (remote) access
- Assign management IP addresses
- Enable physical interfaces
- Verify local and remote connectivity

---


**Devices Used:**
- R1 (Cisco Router)
- SW1 (Cisco Layer 2 Switch)
- PC

**Connections:**
- R1 G0/0/0 ↔ SW1 G0/1 (Ethernet straight-through cable)
- PC ↔ SW1 (Console connection via rollover cable)

---

## IP Addressing

For the full addressing scheme used across all labs, refer to:

**[Addressing Scheme](/Addressing-scheme.md)**

---

## Configuration Files

The full device configurations for this lab are available below:

- [R1 Configuration](/Labs/01-basic-initial-config/R1-config.txt)
- [SW1 Configuration](/Labs/01-basic-initial-config/SW1-config.txt)

---

## Screenshots 

The [images](/Labs/01-basic-initial-config/images) folder contains evidence of:

- Console connection from PC to devices
- Initial login and privileged mode access
- Successful configuration mode entry
- Telnet remote access to R1 (192.168.1.1)

---

## Verification Commands

After applying configurations, verify using the following commands:

```bash
show ip interface brief
show running-config
show interfaces g0/0/0
show interfaces g0/1
