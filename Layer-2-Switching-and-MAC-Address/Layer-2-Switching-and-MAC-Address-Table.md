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

---

# Step 4 - Configure Router-on-a-Stick (ROAS)

### Enter global configuration mode on Router1:

```bash
enable
configure terminal
```

### Configure subinterface for VLAN 100:

```bash
interface g0/0/0.100
encapsulation dot1Q 100
ip address 192.168.10.1 255.255.255.0
```

### Configure subinterface for VLAN 200:

```bash
interface g0/0/0.200
encapsulation dot1Q 200
ip address 192.168.20.1 255.255.255.0
```

### Configure subinterface for VLAN 300:

```bash
interface g0/0/0.300
encapsulation dot1Q 300
ip address 192.168.30.1 255.255.255.0
```

### Enable the physical interface:

```bash
interface g0/0/0
no shutdown
```

---

# Step 5 - Configure a Static MAC Address Entry

Click on PC7 > Config > FastEthernet0 > configure MAC address or leave it

<img width="738" height="350" alt="0" src="https://github.com/user-attachments/assets/428fd423-239d-4bb1-bd97-d29438ac1487" />

On SW-2960, configure a static MAC address entry for PC7:

```bash
mac address-table static 2222.0DDD.2222 vlan 300 interface f0/7
```

---

# Step 6 - Populate the MAC Address Table

Generate traffic to populate the MAC address table.

From each PC, ping a non-existing IP address:

```bash
ping 10.0.0.1
```
---

# Step 7 - View the MAC Address Table

Display the MAC address table:

<img width="716" height="333" alt="1" src="https://github.com/user-attachments/assets/a13d7f84-fdd0-4429-9ccb-5954b1028433" />
<img width="610" height="173" alt="1 1" src="https://github.com/user-attachments/assets/d8bd699b-1e9c-4f38-bbc6-cbb75419eeec" />

Other show commands:
- show mac address-table static
- show mac address-table dynamic
- show mac address-table interface
