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

## Step 1 - Configure VLAN Access Ports on SW-2960

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

## Step 2 - Configure Trunk Port on SW-2960

### Configure the uplink interface connected to the router:

```bash
interface g0/1
switchport mode trunk
switchport trunk allowed vlan 100,200,300
```

---

Verify trunk configuration:

<img width="747" height="235" alt="0" src="https://github.com/user-attachments/assets/2d2dd664-36e4-4b0c-8b4c-86306bfd1dec" />

## Step 3 - Configure IP Addresses on PCs

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

## Step 4 - Configure Router-on-a-Stick (ROAS)

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

## Step 5 - Populate the ARP Table

Generate traffic to populate the ARP table.

From each PC, ping the default gateway for its subnet. **Note: .1 of each subnet is the default gateway**

```bash
ping 192.168.10.1
```

---

## Step 6 - View the ARP Table

On Router1, display the ARP table:

```bash
show arp or show ip arp
```

<img width="882" height="385" alt="1" src="https://github.com/user-attachments/assets/e3aa4911-f61b-4875-b7d3-c67d335452d5" />

## Step 7 - View the ARP Cache Timeout

Display interface information for G0/0/0:

```bash
show interface g0/0/0
```

<img width="762" height="238" alt="2 1" src="https://github.com/user-attachments/assets/2fa08e63-2967-443b-8db2-75455b996e2c" />

---

# Step 9 - Configure ARP Cache Timeout

Enter global configuration mode:

```bash
configure terminal
```

Enter interface configuration mode:

```bash
interface g0/0/0
```

Set the ARP timeout to 60 seconds:

```bash
arp timeout 60
```

<img width="438" height="80" alt="3" src="https://github.com/user-attachments/assets/22291b3f-60d7-472e-9b79-d3f3b6881c86" />

This sets the ARP cache timeout to 1 minute.

---

# Step 10 - Verify the ARP Timeout Configuration

Display interface information again:

```bash
show interface g0/0/0
```

<img width="772" height="225" alt="4" src="https://github.com/user-attachments/assets/65a38aae-fde3-487b-89ef-60391ef99304" />


