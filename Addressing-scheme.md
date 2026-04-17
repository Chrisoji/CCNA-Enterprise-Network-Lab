# Basic Initial Configuration

## Lab 01 – Basic Initial Configuration

This section defines the IP addressing plan for initial device management and connectivity setup.

---

## Device Addressing Table

| Device | Interface | IP Address   | Subnet Mask     | Default Gateway | Purpose |
|--------|----------|-------------|----------------|----------------|---------|
| R1     | G0/0/0   | 192.168.1.1 | 255.255.255.0  | N/A            | Management / connectivity |
| SW1    | VLAN 1   | 192.168.1.2 | 255.255.255.0  | 192.168.1.1    | Management IP |
