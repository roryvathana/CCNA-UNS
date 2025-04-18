
# University Network Setup 🚀
## Overview
>After completing CCNA v7: Enterprise Networking, Security, and Automation — the third and final course in the Cisco CCNA curriculum — we were tasked with designing and deploying a functional enterprise network that meets a defined set of academic and technical requirements.

This project demonstrates the design and secure implementation of a scalable university network using Cisco Packet Tracer. The network architecture features multiple VLANs, dynamic routing with OSPF, inter-VLAN communication via Router-on-a-Stick, and WAN connectivity with PPP. Security is enforced through ACLs and redundancy via HSRP. Essential services like DHCP, DNS, NAT, and NTP are configured, while monitoring is enabled through Syslog, SNMP, and CDP. Spanning Tree Protocol ensures loop-free switching with root bridge control.
## Network Topology
![[Pasted image 20250418010759.png]]
## Project Objectives
✅ Design a campus network with 8 VLANs for segmentation and implement trunking between switches.  
✅ Configure Router-on-a-Stick for inter-VLAN routing.  
✅ Implement OSPF (single area) for dynamic and scalable routing.  
✅ Set up WAN connectivity using PPP between core routers.  
✅ Enforce security using standard and extended Access Control Lists (ACLs).  
✅ Secure switch ports via Port Security and DHCP Snooping.  
✅ Implement HSRP for gateway redundancy between R1 and R2.  
✅ Enable DHCP for dynamic IP addressing and PAT for internet access.  
✅ Set up DNS resolution within the network.  
✅ Synchronize network devices using NTP.  
✅ Monitor and troubleshoot the network with Syslog, SNMP, and CDP.  
✅ Ensure loop prevention and network efficiency using PVST with root bridge election.

## Technologies Used
### Routing Protocols
- Static Routing
- Dynamic Routing Protocol: OSPF (Single Area)  
- Inter-VLAN routing: Router-on-a-stick
### Switching
- VLANs & Trunking: 8 VLANs
- Spanning Tree Protocol: PVST with Root bridge election 
### Security Features
- Access control lists: standard and Extended 
### Network services
- DHCP Configuration
- NAT: PAT
- DNS
- Redundancy: HSRP on R1 & R2
### WAN Technologies
- PPP
### Network Monitoring & mangement
- Syslog
- NTP
- CDP

## Network Configuration
```d
### 1. VLAN & Inter-VLAN Routing
# Configure VLANs on Switch
Switch(config)# vlan 10
Switch(config-vlan)# name BAC_VLAN
Switch(config-vlan)# vlan 20
Switch(config-vlan)# name Staff_VLAN

# Configure Trunk Port
Switch(config)# interface GigabitEthernet0/1
Switch(config-if)# switchport mode trunk

# Configure Router-on-a-Stick
Router(config)# interface GigabitEthernet0/0.10
Router(config-if)# encapsulation dot1Q 10
Router(config-if)# ip address 192.168.0.3 255.255.248.0

### 2. OSPF Configuration
Router(config)# router ospf 1
Router(config-router)# network 192.168.0.0 0.0.7.255 area 0
Router(config-router)# network 192.168.0.0 0.0.7.255 area 0

### 3. Access Control Lists (ACLs)
Router(config)# ip access-list extended Block-vlan60
Router(config-ext-nacl)# permit ip 192.168.13.64 0.0.0.31 192.168.13.0 0.0.0.63
Router(config-ext-nacl)# permit ip 192.168.13.64 0.0.0.31 any
Router(config-ext-nacl)# deny ip any 192.168.13.0 0.0.0.63
Router(config-ext-nacl)# permit ip any any
r
Router(config)# access-list 100 permit ip any any
Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip access-group 100 in

Router(config)# ip access-list standard PERMIT_VLANS_10_20_30_40_50
Router(config-std-nacl)# permit 192.168.0.0 0.0.7.255
Router(config-std-nacl)# permit 192.168.8.0 0.0.3.255
```
## Results & Lessons Learned
Below are key achievements and takeaways from the experience: 
### 🎯 Key Results
✔ Effective VLAN Segmentation
Isolated departments (e.g., BAC_VLAN & Staff_VLAN) into separate **broadcast domains** to enhance performance and security.

✔ Successful Inter-VLAN Routing
Enabled communication between **VLANs** using **Router-on-a-Stick** both R1 and R2, maintaining traffic control and segmentation.

✔ Dynamic Routing with OSPF
Deployed **OSPF** (single-area) to simplify routing updates and support scalability across multiple networks.

✔ Access Control Enforcement
Configured **ACLs** to restrict unnecessary access between departments, demonstrating basic policy enforcement.

✔ Monitoring Enabled
Used **Syslog** for centralized logging and network monitoring, improving administrative visibility.
### 💡 Lessons Learned

🧠 Layer 2 & Layer 3 Troubleshooting
Gained hands-on skills identifying misconfigured VLANs, incorrect trunking, and ACL order issues using CLI. 

🔐 Security by Design
Understood the importance of integrating security into network design from the start—not as an afterthought.

🔄 Routing Protocol Behavior
Learned how OSPF dynamically updates routing tables and adjusts to topology changes in real-time.

📡 Importance of Documentation
Realized how well-documented configs and diagrams improve collaboration and reduce setup/debug time.

🧩 Holistic Network Thinking
Learned to think beyond device configuration—considering scalability, policy enforcement, and visibility as key design goals.
## Repository Structure
```
📂 University Network Project
 ┣ 📂 Diagrams/
 ┣ 📜 README.md
 ┣ 📜 Universit_Network_Setup_Project.pkt 
 ┣ 📜 VLSM table.csv
 ┗ 📜 IP address table.csv
```

## Network Device used
- Router 2911
- Switch 3650-24PS
- Switch 2960-24TT
- WLC 3504
- AP LAP-PT
## Future Improvements
- Configure VPN (IPsec/SSL) for remote access.
- Enable log monitoring with Syslog tools.
- Impletement QoS to VoIP VLAN 
- Apply IPv6 
- Enhance WLAN techonologies
## Reflection
