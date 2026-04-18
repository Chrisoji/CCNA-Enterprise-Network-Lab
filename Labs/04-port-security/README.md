# Lab 04: Port Security

## Overview
This lab demonstrates **Port Security**, a key Layer 2 security feature on Cisco switches. 

Port Security restricts the number of MAC addresses allowed on a switch port and protects the network from unauthorized devices. In this lab, we configure port security with sticky MAC learning on access ports and then deliberately introduce an **Attacker PC** to observe violation behavior in both **Restrict** and **Shutdown** modes.

---

## Lab Objectives
- Configure port security with sticky MAC address learning
- Limit ports to a maximum of 1 MAC address
- Apply different violation modes (Restrict and Shutdown)
- Demonstrate the effect of connecting an unauthorized device
- Understand how to recover from port security violations

---

## Devices & Connections
**Devices Used:**
- SW1 (Cisco Layer 2 Switch)
- PC-A, (test device)
- PC-B, PC-C (Legitimate users)
- PC-Attacker (Test device)

**Connections:**
- PC-A → SW1 FastEthernet0/1 (VLAN 10)
- PC-B → SW1 FastEthernet0/2 (VLAN 10)
- PC-C → SW1 FastEthernet0/3 (VLAN 10)
- PC-Attacker → SW1 FastEthernet0/4 (VLAN 10)

---

## IP Addressing
For the complete IP addressing scheme used across all labs, refer to:  
**[Addressing Scheme](/Addressing-scheme.md)**

All devices are in VLAN 10 – 192.168.10.0/24

---

## Configuration Files
The port security configuration for this lab is available here:

- [SW1 Configuration](/Labs/04-port-security/SW1-config.txt)

---

## Testing Port Security Violations

To demonstrate port security violations, we used **PC-A** and **PC-Attacker** as **test devices**. 

Since all ports were configured with sticky MAC learning (maximum 1 MAC address), we tested violations by **swapping the positions** of these two test devices after the switch had already learned their MAC addresses on the original ports.

### Test Procedure:

1. **Initial MAC Learning**
   - Connected PC-A to FastEthernet0/1, PC-B to FastEthernet0/2, PC-C to FastEthernet0/3 and pc-attacker to FastEthernet0/4.
   - Allowed the switch to dynamically learn and save the MAC addresses using **sticky** learning.
   - Verified that all PCs (PC-A, PC-B, PC-C and PC-Attacker) could successfully ping each other.

2. **Violation Testing by Swapping Test Devices**
   - Swapped the positions of the two test devices:
     - Connected **PC-Attacker** to FastEthernet0/1 (port configured with `violation shutdown`)
     - Connected **PC-A** to FastEthernet0/4 (port configured with `violation restrict`)
   - Attempted pings from PC-Attacker to PC-A and PC-A to PC-C.

3. **Observed Results**
   - On FastEthernet0/4 (**Restrict mode**): The security violation count increased, and pings from the attacker were dropped, but the port remained up.
   - On FastEthernet0/1 (**Shutdown mode**): The port immediately entered the **err-disabled** state, blocking all traffic on that port.

4. **Recovery**
   - Recovered the err-disabled port using:
     ```ios
     interface FastEthernet0/1
      shutdown
      no shutdown


