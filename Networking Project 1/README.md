# SOHO Network Design

## 📌 Project Overview
This project implements a **VLAN-based SOHO network** for **XYZ Company**, designed in **Cisco Packet Tracer**.  
The network supports:
- Departmental segmentation via VLANs.
- Inter-VLAN routing (Router-on-a-Stick).
- Automatic IP assignment via DHCP.
- Both wired and wireless access.
- Redundancy readiness using Cisco equipment.

---




2. Requirements

Based on the provided specifications:

One router and one switch (core/central) to be used.

Three departments:

Admin/IT (VLAN 10)

Finance/HR (VLAN 20)

Customer Service/Reception (VLAN 30)

Each department assigned its own VLAN.

Wireless connectivity for each department.

Automatic IP address assignment via DHCP.

Devices must be able to communicate across VLANs.

3. Network Design

VLAN Assignments:

VLAN	Department	Subnet	         Gateway  IP
10	Admin/IT	192.168.1.0/26	 192.168.1.1
20	Finance/HR	192.168.1.64/26	 192.168.1.65
30	CS/Reception	192.168.1.128/26 192.168.1.129

Core Devices:

Cisco 2911 Router (Router-on-a-Stick configuration).

Cisco 2960 Switch (configured with VLANs and trunk ports).

PCs, Printers, and Access Points for each department.

Connectivity:

Router-on-a-Stick for inter-VLAN routing.

Trunk links between router and switch.

Access ports for end devices.

DHCP server for automatic addressing.

4. Implementation Steps

A. VLAN & Port Configuration on Switch

Switch> enable
Switch# configure terminal

! Create VLANs
vlan 10
 name ADMIN_IT
vlan 20
 name FINANCE_HR
vlan 30
 name CS_RECEPTION

! Assign access ports
interface range fa0/2-4
 switchport mode access
 switchport access vlan 10

interface range fa0/5-7
 switchport mode access
 switchport access vlan 20

interface range fa0/8-10
 switchport mode access
 switchport access vlan 30

! Configure trunk port to router
interface fa0/1
 switchport trunk encapsulation dot1q
 switchport mode trunk


B. Router Subinterfaces

Router> enable
Router# configure terminal

! VLAN 10
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.1.1 255.255.255.192

! VLAN 20
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.1.65 255.255.255.192

! VLAN 30
interface g0/0.30
 encapsulation dot1Q 30
 ip address 192.168.1.129 255.255.255.192

no shutdown


C. DHCP Configuration

ip dhcp pool VLAN10
 network 192.168.1.0 255.255.255.192
 default-router 192.168.1.1

ip dhcp pool VLAN20
 network 192.168.1.64 255.255.255.192
 default-router 192.168.1.65

ip dhcp pool VLAN30
 network 192.168.1.128 255.255.255.192
 default-router 192.168.1.129

5. Testing

Ping between VLANs: Ensure inter-VLAN routing works.

DHCP: Verify devices get IP addresses automatically.

Wireless: Check SSIDs per VLAN.

Printing: Test printer connectivity in each VLAN.

6. Skills Demonstrated

VLAN creation & segmentation.

Router-on-a-stick configuration.

DHCP server setup.

Inter-VLAN routing.

Cisco switch trunk configuration.

Subnetting & IP addressing.
