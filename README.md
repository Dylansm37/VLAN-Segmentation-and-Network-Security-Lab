# VLAN Segmentation and Network Security Lab

## Overview

This lab demonstrates network segmentation and access control using Cisco VLANs, router-on-a-stick, DHCP, and extended access control lists (ACLs).

The network contains three departments: Sales, IT, and Guest. Each department is assigned its own VLAN and IP subnet. Extended ACLs are used to control communication between VLANs and restrict access to specific network services.

## Objectives

- Create VLANs 10, 20, and 30 for Sales, IT, and Guest.
- Configure switch access ports for each VLAN.
- Configure an 802.1Q trunk between the switch and router.
- Configure router subinterfaces for inter-VLAN routing.
- Configure DHCP pools to automatically assign IP addresses to clients.
- Configure extended ACLs to control traffic between VLANs.
- Allow Sales to access the company server using HTTP (TCP port 80).
- Block Guest access to the IT network.
- Verify ACL behavior using connectivity tests and ACL match counters.

## IP Addressing

| **VLAN** | **Department** | **Network** | **Default Gateway** |
|---|---|---|---|
| 10 | Sales | 192.168.10.0/24 | 192.168.10.1 |
| 20 | IT | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Guest | 192.168.30.0/24 | 192.168.30.1 |

### Company Server

| **Setting** | **Address** |
|---|---|
| IP Address | 192.168.20.12 |
| Subnet Mask | 255.255.255.0 |
| Default Gateway | 192.168.20.1 |
| VLAN | 20 |

## Technologies

- Cisco IOS
- Cisco Packet Tracer
- VLAN segmentation
- DHCP
- Router-on-a-stick
- 802.1Q trunking
- Extended Access Control Lists (ACLs)
- TCP and HTTP

## Network Security

Extended ACLs were configured on the router to control traffic between departments.

The primary security requirement was to allow Sales devices to access the company server using HTTP while restricting other traffic.

Example ACL configuration:

```cisco
access-list 110 permit tcp 192.168.10.0 0.0.0.255 host 192.168.20.12 eq 80
```

ACL 110 was applied outbound on the VLAN 20 router subinterface:

```cisco
interface GigabitEthernet0/0.20
ip access-group 110 out
```
<img width="700" height="714" alt="PC1" src="https://github.com/user-attachments/assets/e350e6bb-5c96-4451-bcab-1f0b4dba02e5" />
<img width="703" height="711" alt="PC3" src="https://github.com/user-attachments/assets/d10d0bf1-3755-43ae-86da-d71f5a2b57d0" />



This filters traffic routed toward VLAN 20. Additional permit and deny statements are required to define the intended access for other departments and destinations.

## Verification

The following commands were used to verify VLAN assignments, trunk configuration, routing, DHCP operation, and ACL behavior.

### VLAN Configuration

```cisco
show vlan brief
```

### Trunk Configuration

```cisco
show interfaces trunk
```

### Interface Status

```cisco
show ip interface brief
```

### Routing Table

```cisco
show ip route
```

### DHCP Bindings

```cisco
show ip dhcp binding
```

### ACL Configuration and Match Counters

```cisco
show access-lists 110
```

### ACL Interface Assignment

```cisco
show ip interface GigabitEthernet0/0.20
```

### Running Configuration

```cisco
show running-config
```

## Files

- `lab.pkt`: Packet Tracer topology
- `configs/`: Router and switch configuration files
- `topology.png`: Network topology diagram
- `troubleshooting.md`: Troubleshooting notes
