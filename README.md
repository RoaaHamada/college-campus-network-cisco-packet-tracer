[README.md](https://github.com/user-attachments/files/31800941/README.md)
# College Network Design – Cisco Packet Tracer

A complete Cisco Packet Tracer networking project designed to model a college/university network with multiple departments, VLAN segmentation, inter-VLAN routing, DHCP, WAN connectivity, and server services.

## Project Overview

This project demonstrates the design and configuration of a segmented college network using Cisco networking concepts and Packet Tracer.

### Main Technologies

- VLAN segmentation
- Access and trunk switchports
- Layer 3 switching
- Router-on-a-Stick / 802.1Q subinterfaces
- DHCP
- Static IP addressing for infrastructure/server devices
- Serial WAN connectivity
- Basic routing and connectivity testing
- Email server configuration
- Cisco IOS CLI configuration

## VLAN / Department Structure

| VLAN | Department / Network | Gateway |
|---:|---|---|
| 10 | Administration | 192.168.1.1 |
| 20 | HR | 192.168.2.1 |
| 30 | Simulation | 192.168.3.1 |
| 40 | Chemistry | 192.168.4.1 |
| 50 | Student Affairs | 192.168.5.1 |
| 60 | Student Lab | 192.168.6.1 |
| 70 | Lab B | 192.168.7.1 |
| 80 | Plant Lab | 192.168.8.1 |
| 90 | Library | 192.168.9.1 |
| 100 | IT Department | 192.168.10.1 |
| 110 | Math & CS Department | 192.168.11.1 |
| 120 | Physics Lab | 192.168.12.1 |
| 130 | Botany Lab | 192.168.13.1 |

> The exact device-to-port mapping can be verified directly in the `.pkt` project file and the configuration screenshots.

## Addressing

Each department uses a dedicated `/24` subnet:

```text
192.168.<VLAN>.0/24
```

The default gateway follows:

```text
192.168.<VLAN>.1
```

The WAN/Server segment shown in the documentation uses:

```text
20.0.0.0/30
Router:       20.0.0.1
Email Server: 20.0.0.2
```

A point-to-point serial link is also configured between routers using:

```text
10.10.10.0/30
```

## DHCP

DHCP pools were configured on the main router for the department networks, including:

- Admin
- HR
- Simulation
- Chemistry
- Student Affairs
- Student Lab
- Lab B
- Plant Lab
- Library
- IT
- Math & CS
- Physics
- Botany

Each pool provides the appropriate network, default gateway, and DNS/server information for its subnet.

## Inter-VLAN Routing

Inter-VLAN communication is implemented using 802.1Q subinterfaces on the router.

Example:

```text
interface GigabitEthernet0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.0
```

The same design is repeated for the required VLANs.

## Switching

Access switches are configured with department-specific VLAN assignments.

Typical access-port configuration:

```text
interface range FastEthernet0/1-24
 switchport mode access
 switchport access vlan <VLAN-ID>
```

The main Layer 3 switch also includes trunk connectivity toward the router/network core.

## Server

An Email Server is configured on:

```text
IP Address: 20.0.0.2
Subnet Mask: 255.255.255.252
Default Gateway: 20.0.0.1
```

Connectivity is verified with ICMP testing.

## Verification

One of the documented tests confirms successful connectivity to the router:

```text
C:\>ping 20.0.0.1

Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

This provides evidence that the server-to-router connection is operational.

## Screenshots

The `screenshots/` folder contains the configuration and verification evidence collected during the project.

### Configuration Evidence

![Configuration evidence 01](screenshots/01-configuration-evidence.jpg)

![Configuration evidence 02](screenshots/02-configuration-evidence.jpg)

![Configuration evidence 03](screenshots/03-configuration-evidence.jpg)

![Configuration evidence 04](screenshots/04-configuration-evidence.jpg)

![Configuration evidence 05](screenshots/05-configuration-evidence.jpg)

![Configuration evidence 06](screenshots/06-configuration-evidence.jpg)

![Configuration evidence 07](screenshots/07-configuration-evidence.jpg)

![Configuration evidence 08](screenshots/08-configuration-evidence.jpg)

![Configuration evidence 09](screenshots/09-configuration-evidence.jpg)

![Configuration evidence 10](screenshots/10-configuration-evidence.jpg)

![Configuration evidence 11](screenshots/11-configuration-evidence.jpg)

![Configuration evidence 12](screenshots/12-configuration-evidence.jpg)

![Configuration evidence 13](screenshots/13-configuration-evidence.jpg)

![Configuration evidence 14](screenshots/14-configuration-evidence.jpg)

![Configuration evidence 15](screenshots/15-configuration-evidence.jpg)

![Configuration evidence 16](screenshots/16-configuration-evidence.jpg)

![Configuration evidence 17](screenshots/17-configuration-evidence.jpg)

![Configuration evidence 18](screenshots/18-configuration-evidence.jpg)

![Configuration evidence 19](screenshots/19-configuration-evidence.jpg)

![Configuration evidence 20](screenshots/20-configuration-evidence.jpg)

![Configuration evidence 21](screenshots/21-configuration-evidence.jpg)

![Configuration evidence 22](screenshots/22-configuration-evidence.jpg)

![Configuration evidence 23](screenshots/23-configuration-evidence.jpg)

![Configuration evidence 24](screenshots/24-configuration-evidence.jpg)

![Configuration evidence 25](screenshots/25-configuration-evidence.jpg)

![Configuration evidence 26](screenshots/26-configuration-evidence.jpg)

![Configuration evidence 27](screenshots/27-configuration-evidence.jpg)

![Configuration evidence 28](screenshots/28-configuration-evidence.jpg)

![Configuration evidence 29](screenshots/29-configuration-evidence.jpg)

![Configuration evidence 30](screenshots/30-configuration-evidence.jpg)

![Configuration evidence 31](screenshots/31-configuration-evidence.jpg)

![Configuration evidence 32](screenshots/32-configuration-evidence.jpg)

![Configuration evidence 33](screenshots/33-configuration-evidence.jpg)

![Configuration evidence 34](screenshots/34-configuration-evidence.jpg)

![Configuration evidence 35](screenshots/35-configuration-evidence.jpg)

![Configuration evidence 36](screenshots/36-configuration-evidence.jpg)

![Configuration evidence 37](screenshots/37-configuration-evidence.jpg)

## Project Structure

```text
College-Network-Design-GitHub-Package/
├── README.md
└── screenshots/
    ├── 01-configuration-evidence.jpg
    ├── 02-configuration-evidence.jpg
    ├── ...
    └── configuration-evidence files
```

## Learning Outcomes

This project demonstrates practical understanding of:

- Designing a multi-department enterprise/college LAN
- VLAN segmentation and access-port configuration
- Trunking between network devices
- Inter-VLAN routing with 802.1Q
- DHCP implementation
- IP addressing and subnetting
- Router and switch CLI configuration
- WAN/serial connectivity
- Server addressing and connectivity verification
- Troubleshooting configuration errors and interface states

## Notes

Some screenshots intentionally show IOS command-line messages and configuration corrections. They are retained as part of the project evidence and demonstrate the troubleshooting process during implementation.

---

**Project Type:** Cisco Packet Tracer Networking Project  
**Focus:** College Network Infrastructure & Segmentation
