Inter-VLAN Routing with Multilayer Switches, OSPF & DHCP
📌 Project Overview

This project demonstrates how to configure multilayer switches in Cisco Packet Tracer to:

Perform inter-VLAN routing.

Establish inter-switch connectivity using routed ports.

Use OSPF (Open Shortest Path First) for dynamic routing between VLANs and switches.

Provide automatic IP addressing using a dedicated DHCP server.

The setup replaces traditional routers with multilayer switches that act as both switches and routers.

🖧 Network Topology

VLANs for end devices:

VLAN 10 → 192.168.1.0/24

VLAN 20 → 192.168.2.0/24

VLAN 30 → 192.168.3.0/24

Inter-switch routed links:

Switch1 ↔ Switch2 → 10.0.12.0/24

Switch2 ↔ Switch3 → 10.0.23.0/24

Switch1 ↔ Switch3 → 10.0.13.0/24

DHCP Server connected to VLAN 10. It assigns IP addresses to PCs across all VLANs.

⚙️ Configuration Steps
1. Enable Routing on Switch
Switch(config)# ip routing

2. Create VLAN Interfaces (SVIs)
Switch(config)# interface vlan 10
Switch(config-if)# ip address 192.168.1.1 255.255.255.0
Switch(config-if)# no shut

Switch(config)# interface vlan 20
Switch(config-if)# ip address 192.168.2.1 255.255.255.0
Switch(config-if)# no shut

Switch(config)# interface vlan 30
Switch(config-if)# ip address 192.168.3.1 255.255.255.0
Switch(config-if)# no shut

3. Configure Inter-switch Routed Links

Example (Switch1 side towards Switch2):

Switch1(config)# interface fa0/1
Switch1(config-if)# no switchport
Switch1(config-if)# ip address 10.0.12.1 255.255.255.0
Switch1(config-if)# no shut


Do the same on the other switches with matching subnets.

4. Configure OSPF

Enable OSPF on each switch:

Switch(config)# router ospf 1
Switch(config-router)# network 192.168.1.0 0.0.0.255 area 0
Switch(config-router)# network 192.168.2.0 0.0.0.255 area 0
Switch(config-router)# network 192.168.3.0 0.0.0.255 area 0
Switch(config-router)# network 10.0.12.0 0.0.0.255 area 0
Switch(config-router)# network 10.0.13.0 0.0.0.255 area 0
Switch(config-router)# network 10.0.23.0 0.0.0.255 area 0

5. Configure DHCP Server

On the DHCP server device:

Go to Services > DHCP.

Add a pool for each VLAN:

VLAN 10 Pool

Default Gateway: 192.168.1.1

DNS: 8.8.8.8 (or any)

Start IP: 192.168.1.100

Subnet Mask: 255.255.255.0

VLAN 20 Pool

Default Gateway: 192.168.2.1

Start IP: 192.168.2.100

VLAN 30 Pool

Default Gateway: 192.168.3.1

Start IP: 192.168.3.100

Enable DHCP service.

6. Configure DHCP Relay on Switch

Since the DHCP server is only in VLAN 10, the switch must forward DHCP requests from VLAN 20 and VLAN 30 using ip helper-address:

Switch(config)# interface vlan 20
Switch(config-if)# ip helper-address 192.168.1.50   ! DHCP server IP

Switch(config)# interface vlan 30
Switch(config-if)# ip helper-address 192.168.1.50

✅ Verification

PCs in VLAN 10, 20, and 30 should get IPs automatically.

Ping test: PCs across VLANs should reach each other.

OSPF check:

Switch# show ip route ospf
Switch# show ip ospf neighbor

📂 Files Included

.pkt file with the Packet Tracer topology.

This README with step-by-step setup.