# Packet Tracer Lab: Port-Channeling with LACP

## Overview
This lab demonstrates how to configure **EtherChannel using LACP (Link Aggregation Control Protocol)** between two Cisco switches in Cisco Packet Tracer.  
EtherChannel bundles multiple physical links into a single logical link, providing redundancy and load-balancing.

---

## Topology
PC1 ----- SW1 ====== SW2 ----- PC2



==== represents two Gigabit Ethernet links bundled into Port-Channel 1


---

## Objectives
1. Configure LACP-based EtherChannel between SW1 and SW2.  
2. Assign EtherChannel to a trunk, allowing VLAN 10.  
3. Verify redundancy and load balancing.  
4. Test connectivity before and after shutting down one physical link.  

---

## Configuration Steps

### SW1
configure terminal

# Create Port-Channel 1 with LACP
interface range g0/1 - 2
 channel-group 1 mode active
 no shutdown

# Configure trunk on Port-Channel
interface port-channel 1
 switchport mode trunk
 switchport trunk allowed vlan 10


SW2
enable
configure terminal

# Create Port-Channel 1 with LACP
interface range g0/1 - 2
 channel-group 1 mode active
 no shutdown

# Configure trunk on Port-Channel
interface port-channel 1
 switchport mode trunk
 switchport trunk allowed vlan 10

PCs
PC1: IP = 192.168.1.10 /24, Gateway = 192.168.1.1

PC2: IP = 192.168.1.20 /24, Gateway = 192.168.1.1


Verification Commands
On both switches:
show etherchannel summary
show interfaces trunk
show spanning-tree interface po1 detail
Expected output:

Po1(SU) = Port-channel is up and bundled.

Member interfaces show (P) = participating in the bundle.

Trunk allows VLAN 10.

Testing Redundancy
Start a continuous ping from PC1 → PC2.

On SW1, shut down one link:

interface g0/1
shutdown


✅ Ping continues, traffic flows over the remaining link.

Bring it back up with no shutdown.

Optional Enhancements
Add VLAN 20 and test multi-VLAN trunking.

Configure different load-balancing methods:
port-channel load-balance src-dst-mac
Demonstrate a mismatch scenario (e.g., one side on on, the other active) and show why it fails.


Key Takeaways
LACP bundles links dynamically (active/passive modes).

EtherChannel improves bandwidth utilization and provides redundancy.

Trunking works seamlessly over a port-channel interface.

