# Layer 2 Switching and MAC Address Table

## Lab Overview
This lab demonstrates Layer 2 switching concepts using VLANs, trunking, Router-on-a-Stick (ROAS), MAC address table, and static MAC address configuration on Cisco devices.

## Devices Used
- Cisco ISR 4331 Router
- Cisco WS-C2960 Switch
- 7 PCs

## Reference Topology

<img width="893" height="545" alt="TFR" src="https://github.com/user-attachments/assets/16ff1518-f810-4359-9ac2-e40f0400ff54" />

---

# Step 1 - Configure VLAN Access Ports on SW-2960

### Enter global configuration mode:

```bash
enable
configure terminal
```

### Configure VLAN 100 access ports:

```bash
interface range f0/1-2
switchport mode access
switchport access vlan 100
```

### Configure VLAN 200 access ports:

```bash
interface range f0/3-4
switchport mode access
switchport access vlan 200
```

### Configure VLAN 300 access ports:

```bash
interface range f0/5-7
switchport mode access
switchport access vlan 300
```

---

# Step 2 - Configure Trunk Port on SW-2960

### Configure the uplink interface connected to the router:

```bash
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 100,200,300
```

Verify trunk configuration:

<img width="747" height="235" alt="0" src="https://github.com/user-attachments/assets/2d2dd664-36e4-4b0c-8b4c-86306bfd1dec" />

# Step 3 - Configure IP Addresses on PCs

### Configure IP addresses manually on each PC.

Go to:

```text
PC > Desktop > IP Configuration
```

## VLAN 100
| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| PC1 | 192.168.10.10 | 255.255.255.0 | 192.168.10.1 |
| PC2 | 192.168.10.20 | 255.255.255.0 | 192.168.10.1 |

## VLAN 200
| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| PC3 | 192.168.20.10 | 255.255.255.0 | 192.168.20.1 |
| PC4 | 192.168.20.20 | 255.255.255.0 | 192.168.20.1 |

## VLAN 300
| Device | IP Address | Subnet Mask | Default Gateway |
|---|---|---|---|
| PC5 | 192.168.30.10 | 255.255.255.0 | 192.168.30.1 |
| PC6 | 192.168.30.20 | 255.255.255.0 | 192.168.30.1 |
| PC7 | 192.168.30.30 | 255.255.255.0 | 192.168.30.1 |



