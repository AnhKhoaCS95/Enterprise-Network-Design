Enterprise Network Design with pfSense, Suricata, and Squid
Overview

This project demonstrates the design, implementation, and configuration of a secure enterprise network using GNS3.
The network is designed to simulate a real corporate environment, featuring:

VLAN Segmentation to separate traffic between departments for better performance and security.

pfSense Firewall acting as the core gateway with firewall rules, routing, IDS/IPS, and proxy services.

DMZ Zone for hosting public-facing services while isolating internal networks.

Wi-Fi Network for wireless users and guests.

Windows Server for centralized file sharing and automated backups.

This design follows enterprise-grade network security practices and introduces monitoring, access control, and defense against cyberattacks.

Network Topology

The network is divided into four main zones: Department VLANs, DMZ, Wi-Fi, and the pfSense Core Firewall.

1. VLAN Configuration (Department Networks)

Note: Switches in these VLANs are Layer 2 devices and do not have IP addresses.
They are used only to forward traffic between devices within the same VLAN.

VLAN 11 – Accounting Department (192.168.11.0/24)
Device	IP Address	Subnet Mask
Windows10x64-1	192.168.11.10	255.255.255.0
PC1	192.168.11.1	255.255.255.0
PC5	192.168.11.2	255.255.255.0

Purpose:

Secure environment for financial data.

Strict access control with limited communication to other VLANs.

VLAN 12 – Server Room (192.168.12.0/24)
Device	IP Address	Subnet Mask
Windows Server 2022	192.168.12.10	255.255.255.0
PC3	192.168.12.1	255.255.255.0
Safe Deposit System	192.168.12.2	255.255.255.0

Purpose:

Provides shared folders for all departments.

Runs scheduled backup jobs to secure company data.

Accessible only by authorized VLANs.

VLAN 13 – Business Department (192.168.13.0/24)
Device	IP Address	Subnet Mask
Windows10-PC2	192.168.13.10	255.255.255.0
PC2	192.168.13.1	255.255.255.0
PC6	192.168.13.2	255.255.255.0

Purpose:

Workstations for the sales and marketing team.

Limited access to sensitive resources such as Accounting VLAN or backup systems.

2. Wi-Fi Network (192.168.230.0/24)
Device	IP Address	Subnet Mask
WiFi-PC-1	192.168.230.10	255.255.255.0
Router WiFi-1	192.168.230.1	255.255.255.0

Purpose:

Provides wireless access for employees and guests.

Traffic is filtered through Squid Proxy to enforce access policies.

3. DMZ – Demilitarized Zone (192.168.200.0/24)
Device	IP Address	Subnet Mask
Web Server	192.168.200.2	255.255.255.0
Mail Server	192.168.200.3	255.255.255.0
PC4	192.168.200.4	255.255.255.0
Switch4 (Mgmt)	192.168.200.254	255.255.255.0

Purpose:

Public-facing services such as:

Web Server for company website.

Mail Server for internal and external communication.

Isolated to prevent external attacks from reaching the internal LAN.

4. pfSense Firewall Configuration
Interface	IP Address	Subnet Mask
LAN	192.168.100.1	255.255.255.0
WAN	192.168.100.2	255.255.255.0
DMZ	192.168.200.1	255.255.255.0
Wi-Fi	192.168.230.1	255.255.255.0
Roles of pfSense

Firewall Rules:

Controls communication between VLANs and external Internet.

Blocks unauthorized access to the Accounting VLAN.

NAT:

Allows internal devices to access the Internet securely.

DHCP (Optional):

Provides automatic IP address allocation.

Integration with Security Tools:

Suricata IDS/IPS.

Squid Proxy filtering.

5. Security Solutions
Suricata IDS/IPS

Suricata is deployed inside pfSense to protect the network in real-time:

Detects and blocks:

Port scanning (e.g., Nmap).

DoS/DDoS attacks.

Malicious or suspicious traffic.

Generates alerts and logs for security monitoring.

Squid Proxy

Squid is used to filter and control Internet access:

Access Control Lists (ACLs):

Block harmful or inappropriate websites.

Control guest Wi-Fi browsing activity.

Traffic Reporting:

Logs user activity for auditing.

Helps administrators optimize bandwidth.

6. Windows Server Role

The Windows Server in VLAN 12 serves as the company's central file storage and backup system:

Shared Folder Access:

Each department has dedicated shared folders.

Permissions are managed based on department and role.

Automated Backup:

Scheduled backup tasks to secure business-critical data.

Protects against accidental deletion or hardware failure.

7. Traffic Flow and Security Layers

Internal to Internet Traffic:

User → VLAN → pfSense → Suricata scans → Squid filters → Internet.

External to DMZ:

External users can only access web or mail servers.

Cannot reach internal VLANs directly.

Inter-VLAN Communication:

Controlled by firewall rules.

Accounting VLAN has the strictest restrictions for sensitive data.

Project Goals

Build a virtual enterprise network for testing and learning.

Simulate real-world IT security practices:

VLAN segmentation.

DMZ isolation.

IDS/IPS with Suricata.

Proxy filtering with Squid.

Backup and disaster recovery strategy.

Tools Used
Tool/Technology	Purpose
GNS3	Network simulation
pfSense	Firewall, router, VLAN management
Suricata	Intrusion detection and prevention
Squid Proxy	Web traffic filtering
Windows Server 2022	File sharing and backup
Virtual PCs	End-user simulation
Virtual Switches	Layer 2 traffic forwarding
Future Enhancements

Integrate Wazuh SIEM for centralized log collection and advanced analytics.

Add VPN Gateway for secure remote work access.

Deploy High Availability pfSense cluster to prevent downtime.

Use a Load Balancer to improve DMZ service performance.

How to Run This Project

Install GNS3 and import the following:

pfSense VM

Windows Server VM

Windows 10 Clients

Create VLANs and connect devices according to the topology.

Configure pfSense interfaces and firewall rules.

Install Suricata and Squid packages in pfSense.

Test:

Run Nmap scans to validate IDS detection.

Access blocked websites to verify Squid rules.

Verify inter-VLAN restrictions.

Configure shared folders and backup schedules on Windows Server.

Perform a full network connectivity and security test.

Demo:
https://www.youtube.com/playlist?list=PLFb35DC5uB-pdBY27LXny0KMYQsVUNmV_
