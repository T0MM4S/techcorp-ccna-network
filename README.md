# TechCorp Enterprise Network (Cisco Packet Tracer CCNA Project)

## Overview
This project simulates an enterprise network for a fictional company called TechCorp using Cisco Packet Tracer. The network demonstrates core enterprise networking concepts including VLAN segmentation, inter-VLAN routing, OSPF dynamic routing, NAT overload, ACL security policies, and secure device management using SSH.

The topology includes an internal corporate LAN, a core routing layer, and a simulated ISP connection to represent Internet access.

---

## Network Architecture

The network is designed in a three-layer structure:

- Access Layer: SW1 and SW2 handling end devices and VLAN segmentation
- Distribution/Core Layer: R2 handling inter-VLAN routing
- Edge Layer: R1 handling NAT and ISP connectivity
- ISP Layer: External router simulating Internet connectivity

R1 connects to R2 using a point-to-point link. R1 connects to the ISP using a /30 WAN link.

---

## VLAN Design

| VLAN | Department | Subnet | Default Gateway |
|------|------------|--------|-----------------|
| 10 | HR | 192.168.10.0/24 | 192.168.10.1 |
| 20 | IT | 192.168.20.0/24 | 192.168.20.1 |
| 30 | Sales | 192.168.30.0/24 | 192.168.30.1 |
| 40 | Guest | 192.168.40.0/24 | 192.168.40.1 |
| 99 | Management | 192.168.99.0/24 | 192.168.99.1 |

---

## WAN / ISP Connectivity

- R1 connects to a simulated ISP router using network 203.0.113.0/30
- R1 acts as the edge router for the internal network
- ISP router simulates external Internet connectivity
- NAT overload (PAT) is configured on R1 to allow internal private IPs to access external networks

---

## Routing

- OSPF is configured between R1 and R2
- Internal VLAN networks are advertised dynamically
- Default route is injected from R1 into OSPF
- Full internal route propagation is achieved across the network

---

## Security Implementation

### ACL (Access Control List)
- Guest VLAN (VLAN 40) is restricted from accessing internal VLANs:
  - HR
  - IT
  - Sales
  - Management
- Guest VLAN is allowed external access only

### SSH Access
- SSH is enabled on all routers and switches
- Telnet is disabled
- Local user authentication is configured for secure remote management

---

## NAT Configuration

- NAT overload (PAT) configured on R1
- Translates all internal private IP addresses to a single public IP
- Enables Internet access for all internal VLANs

---

## Management Network

- VLAN 99 is used for device management
- Switch management IPs:
  - SW1: 192.168.99.10
  - SW2: 192.168.99.11
- SSH used for secure administrative access

---

## DHCP Configuration

DHCP is configured on the network to automate IP address assignment for end devices in all VLANs.

Each DHCP pool includes:
- Network address
- Default gateway (R2 subinterface IP)
- Subnet mask
- Excluded addresses for network infrastructure devices

This improves scalability and reduces manual configuration effort in the network.



## Files in this repository

configs/
- R1-config.txt
- R2-config.txt
- SW1-config.txt
- SW2-config.txt
- ISP-config.txt

docs/
- network-design.md
- troubleshooting.md

topology/
- techcorp.pkt

README.md

---

## Skills Demonstrated

- VLAN design and segmentation
- Router-on-a-stick inter-VLAN routing
- OSPF dynamic routing
- NAT overload (PAT)
- ACL-based traffic control
- SSH secure device management
- ISP simulation and WAN design
- Enterprise network architecture


## Key Design Decisions

- /30 subnet used for point-to-point links to optimize IP usage
- VLAN 99 used for management instead of VLAN 1 for security reasons
- Router-on-a-stick used for scalable inter-VLAN routing
- OSPF used to enable dynamic routing between core and edge layers