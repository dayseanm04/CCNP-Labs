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
