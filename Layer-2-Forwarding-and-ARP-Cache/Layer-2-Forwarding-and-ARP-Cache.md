# Layer 2 Forwarding and ARP Cache

## Lab Overview
This lab demonstrates Layer 2 forwarding operations, ARP table population, ARP cache management, VLAN configuration, trunking, and Router-on-a-Stick (ROAS) configuration using Cisco devices.

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


---


