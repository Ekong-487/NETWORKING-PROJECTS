### \# Hotel Management Network Design \& Implementation (Cisco Packet Tracer)



**Project Overview**

This project implements a \*\*multi-floor enterprise network\*\* for a modern hotel using \*\*Cisco Packet Tracer\*\*.  

The hotel has three floors, each hosting multiple departments, and requires a scalable, secure, and well-structured network.



The design ensures:  

\- Proper VLAN segmentation per department  

\- Dynamic IP allocation with DHCP  

\- Inter-VLAN communication via routing (OSPF)  

\- Wireless access for mobile devices  

\- Secure remote login (SSH)  

\- Port security for critical departments  



---



Network Requirements

\- \*\*3 routers\*\* (one per floor, connected via Serial DCE links)  

\- \*\*One switch per floor\*\*  

\- \*\*Wi-Fi Access Points\*\* for each floor  

\- \*\*Printers\*\* for each department  

\- \*\*VLAN segmentation\*\*:

&nbsp; - 1st Floor: Reception (VLAN 80), Store (VLAN 70), Logistics (VLAN 60)  

&nbsp; - 2nd Floor: Finance (VLAN 50), HR (VLAN 40), Sales (VLAN 30)  

&nbsp; - 3rd Floor: Admin (VLAN 20), IT (VLAN 10)  



---



IP Addressing

| Department  | VLAN | Network            |

|-------------|------|--------------------|

| IT          | 10   | 192.168.1.0/24     |

| Admin       | 20   | 192.168.2.0/24     |

| Sales       | 30   | 192.168.3.0/24     |

| HR          | 40   | 192.168.4.0/24     |

| Finance     | 50   | 192.168.5.0/24     |

| Logistics   | 60   | 192.168.6.0/24     |

| Store       | 70   | 192.168.7.0/24     |

| Reception   | 80   | 192.168.8.0/24     |



Router interconnections:  

\- `10.10.10.0/30`, `10.10.10.4/30`, `10.10.10.8/30`  



---



Key Configurations

\- \*\*OSPF Routing\*\* → Advertises all VLAN networks across routers.  

\- \*\*DHCP\*\* → Provides dynamic IPs per VLAN.  

\- \*\*SSH\*\* → Enabled for secure remote router access.  

\- \*\*Port Security\*\* → Sticky MAC method applied in IT department.  



---



Repository Contents

\- `Hotel\_Management\_Network.pkt` → Cisco Packet Tracer file  

\- `README.md` → Documentation  





---



&nbsp;How to Use

1\. Open the `.pkt` file in Cisco Packet Tracer (v8 or above).  

2\. Start simulation and test connectivity across VLANs.  

3\. Explore router configurations (`show run`) to see DHCP, OSPF, and SSH setup.  







&nbsp;Future Improvements

\- Add Syslog server for network monitoring.  

\- Add ACLs to restrict inter-department traffic.  

\- Integrate redundancy with HSRP.  



&nbsp; 



