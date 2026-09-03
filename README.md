# 🎓 College Network Infrastructure – Cisco Packet Tracer

A complete **college network infrastructure project** designed and simulated using **Cisco Packet Tracer**.

The project demonstrates a structured, scalable network connecting multiple college departments through **VLAN segmentation, Inter-VLAN Routing, DHCP, RIP v2, and server connectivity**.

---

## 📌 Project Overview

The goal of this project is to design a practical college network that separates departments into logical networks while maintaining controlled communication between them.

### Main technologies implemented

- 🧩 VLAN segmentation
- 🔀 Inter-VLAN Routing using Router-on-a-Stick
- 🚦 802.1Q trunking
- 🌐 IPv4 addressing and subnetting
- 📡 DHCP for automatic IP assignment
- 🛣️ RIP Version 2 dynamic routing
- 🖥️ Server connectivity
- 📧 Email Server configuration
- 🔎 Connectivity and configuration verification
- 💾 Cisco IOS configuration and saving

---

## 🏫 Network Departments & VLANs

The network is divided into **13 logical VLANs**, one for each department:

| VLAN | Department | Network | Default Gateway |
|---:|---|---|---|
| 10 | Administration | `192.168.1.0/24` | `192.168.1.1` |
| 20 | HR | `192.168.2.0/24` | `192.168.2.1` |
| 30 | Mathematics / SIM | `192.168.3.0/24` | `192.168.3.1` |
| 40 | Chemistry | `192.168.4.0/24` | `192.168.4.1` |
| 50 | Student Affairs | `192.168.5.0/24` | `192.168.5.1` |
| 60 | Student Lab | `192.168.6.0/24` | `192.168.6.1` |
| 70 | Labs | `192.168.7.0/24` | `192.168.7.1` |
| 80 | Plant Lab | `192.168.8.0/24` | `192.168.8.1` |
| 90 | Library | `192.168.9.0/24` | `192.168.9.1` |
| 100 | IT Department | `192.168.10.0/24` | `192.168.10.1` |
| 110 | Mathematics & CS | `192.168.11.0/24` | `192.168.11.1` |
| 120 | Physics Lab | `192.168.12.0/24` | `192.168.12.1` |
| 130 | Botany Lab | `192.168.13.0/24` | `192.168.13.1` |

This segmentation reduces broadcast domains and provides a cleaner, more manageable network architecture.

---

## 🗺️ Network Topology

The topology was first planned on paper and then implemented in Cisco Packet Tracer.

![Initial Network Plan](screenshots/01_initial_network_plan.png)

![Topology Overview](screenshots/02_topology_overview.png)

---

## 🔧 Network Architecture

### Core / Main Layer

The project uses a **Main Router** and a **Layer 3 Main Switch** as the central infrastructure.

The router provides:

- Inter-VLAN routing through subinterfaces
- DHCP services
- Dynamic routing using RIP v2
- WAN/serial connectivity
- Connectivity to the server network

### Access Layer

Department switches connect end devices and assign access ports to the appropriate VLAN.

Example:

```text
interface range fa0/1-24
 switchport mode access
 switchport access vlan <VLAN-ID>
```

---

## 🔀 Inter-VLAN Routing

Router-on-a-Stick is used to route traffic between the 13 VLANs.

Example configuration:

```text
interface gig0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.0
```

The same design is repeated for VLANs 20 through 130.

This allows devices in different departmental VLANs to communicate through the router while keeping each department logically separated.

---

## 🛣️ RIP Version 2

Dynamic routing is configured using **RIP v2**.

The routing configuration advertises:

```text
10.10.10.0
192.168.1.0
192.168.2.0
192.168.3.0
...
192.168.13.0
```

RIP v2 was selected to provide dynamic route exchange and simplify routing management within the simulated network.

---

## 📡 DHCP Configuration

DHCP pools are configured on the Main Router so that hosts can automatically receive:

- IPv4 address
- Subnet mask
- Default gateway
- DNS server information

Example:

```text
ip dhcp pool admin-pool
 network 192.168.1.0 255.255.255.0
 default-router 192.168.1.1
 dns-server 192.168.1.1
```

Separate DHCP pools are created for the different departmental networks.

---

## 🖥️ Server Network

A dedicated server network is connected through the router.

### Server addressing

```text
Server IP:       20.0.0.2
Subnet Mask:     255.255.255.252
Default Gateway: 20.0.0.1
```

Connectivity was tested successfully using ICMP ping.

![Server IP Configuration](screenshots/34_email_server_ip_configuration.png)

![Connectivity Test](screenshots/35_connectivity_test.png)

---

## 🔌 WAN / Serial Link

The main router uses a point-to-point serial connection:

```text
Network: 10.10.10.0/30
Router 1: 10.10.10.1
Router 2: 10.10.10.2
```

This link provides connectivity between routing devices in the topology.

---

## 🧪 Verification & Testing

The project includes several verification steps to confirm that the network is working correctly.

### DHCP verification

A client successfully receives an address dynamically, for example:

```text
IP Address:      192.168.10.2
Subnet Mask:     255.255.255.0
Default Gateway: 192.168.10.1
DNS Server:      192.168.10.1
```

### Connectivity testing

Ping tests were performed between hosts and network gateways.

Example successful result:

```text
Packets: Sent = 4, Received = 4, Lost = 0 (0% loss)
```

A cross-network ping also demonstrated successful routed communication.

---

## 📸 Configuration & Implementation Screenshots

### VLAN & Switch Configuration

![Switch Configuration](screenshots/11_switch_configuration.png)

![VLAN Configuration](screenshots/12_switch_configuration_vlan.png)

![Topology VLAN Labels](screenshots/14_topology_vlan_labels.png)

### Router Subinterfaces

![Router Subinterfaces](screenshots/16_router_subinterfaces_01.png)

![Router Subinterfaces](screenshots/17_router_subinterfaces_02.png)

![Router Subinterfaces](screenshots/18_router_subinterfaces_03.png)

![Router Subinterfaces](screenshots/19_router_subinterfaces_04.png)

### DHCP

![DHCP Configuration](screenshots/28_dhcp_configuration_01.png)

![DHCP Configuration](screenshots/29_dhcp_configuration_02.png)

![DHCP Configuration](screenshots/30_dhcp_configuration_03.png)

![DHCP Configuration](screenshots/31_dhcp_configuration_04.png)

### Routing & Verification

![Routing Configuration](screenshots/36_routing_configuration.png)

![Verification](screenshots/37_verification_commands_01.png)

![Verification](screenshots/38_verification_commands_02.png)

![Verification](screenshots/39_verification_commands_03.png)

![Final Verification](screenshots/42_final_verification.png)

---

## 📁 Project Structure

```text
College-Network-Design/
│
├── College_Network_Design.pkt
├── README.md
│
└── screenshots/
    ├── 01_initial_network_plan.png
    ├── 02_topology_overview.png
    ├── 03_switch_physical_setup.png
    ├── ...
    └── 42_final_verification.png
```

---

## 🧰 Tools & Technologies

| Technology | Purpose |
|---|---|
| Cisco Packet Tracer | Network simulation |
| Cisco IOS CLI | Device configuration |
| VLAN | Network segmentation |
| 802.1Q | VLAN trunking |
| Router-on-a-Stick | Inter-VLAN routing |
| DHCP | Automatic IP assignment |
| RIP v2 | Dynamic routing |
| IPv4 | Network addressing |
| ICMP / Ping | Connectivity testing |

---

## 🎯 Learning Outcomes

Through this project, I practiced:

- Designing a multi-department network
- Translating a physical network plan into a logical topology
- Creating and assigning VLANs
- Configuring trunk and access ports
- Implementing Router-on-a-Stick
- Creating DHCP pools
- Configuring dynamic routing with RIP v2
- Connecting and configuring a server
- Troubleshooting CLI configuration errors
- Verifying end-to-end connectivity
- Documenting a network project professionally

---

## 🚀 How to Use

1. Download or clone this repository.
2. Open `College_Network_Design.pkt` using **Cisco Packet Tracer**.
3. Switch to **Simulation** or **Realtime** mode.
4. Inspect the VLANs, routing, DHCP and server configuration.
5. Use commands such as:

```text
show vlan brief
show interfaces trunk
show ip interface brief
show ip route
show ip protocols
show ip dhcp binding
```

to verify the configuration.

---

## 👩‍💻 Author

**Roua Hamada**

Computer Networks / Cisco Packet Tracer Project

---

## ⭐ Project Highlights

> A complete simulated college network built from an initial hand-drawn design into a functional Cisco Packet Tracer topology, using VLAN segmentation, inter-VLAN routing, DHCP, RIP v2 and server connectivity.

If you find this project useful, feel free to ⭐ the repository.
