Enterprise Network Design with pfSense, Suricata, and Squid
Overview

This project demonstrates the design and implementation of an enterprise network using GNS3. The network is built to simulate a real-world company infrastructure, including multiple VLANs, a DMZ, Wi-Fi access, and integrated security mechanisms.

The network is protected by pfSense, which acts as the main firewall and router. It also integrates:

Suricata for intrusion detection and prevention (IDS/IPS).

Squid Proxy for web traffic monitoring and access control.

Additionally, a Windows Server is configured to provide shared folders and automated backup solutions for all departments.

Network Topology

The network consists of four main areas: Departments (VLANs), DMZ, Wi-Fi, and Core Network.

1. VLAN Configuration
VLAN 11 – Accounting Department (192.168.11.0/24)
Device	IP Address	Subnet Mask
Windows10x64-1	192.168.11.10	255.255.255.0
PC1	192.168.11.1	255.255.255.0
PC5	192.168.11.2	255.255.255.0
Switch1	192.168.11.3	255.255.255.0
VLAN 12 – Server Room (192.168.12.0/24)
Device	IP Address	Subnet Mask
Windows Server 2022	192.168.12.10	255.255.255.0
PC3	192.168.12.1	255.255.255.0
Safe Deposit System	192.168.12.2	255.255.255.0
Switch2	192.168.12.254	255.255.255.0
VLAN 13 – Business Department (192.168.13.0/24)
Device	IP Address	Subnet Mask
Windows10-PC2	192.168.13.10	255.255.255.0
PC2	192.168.13.1	255.255.255.0
PC6	192.168.13.2	255.255.255.0
Switch3	192.168.13.254	255.255.255.0
2. Wi-Fi Network (192.168.230.0/24)
Device	IP Address	Subnet Mask
WiFi PC-1	192.168.230.10	255.255.255.0
Router WiFi-1	192.168.230.1	255.255.255.0
3. DMZ – Demilitarized Zone (192.168.200.0/24)
Device	IP Address	Subnet Mask
Web Server	192.168.200.2	255.255.255.0
Mail Server	192.168.200.3	255.255.255.0
PC4	192.168.200.4	255.255.255.0
Switch4	192.168.200.254	255.255.255.0
4. pfSense Firewall Configuration
Interface	IP Address	Subnet Mask
LAN	192.168.100.1	255.255.255.0
WAN	192.168.100.2	255.255.255.0
DMZ	192.168.200.1	255.255.255.0
Wi-Fi	192.168.230.1	255.255.255.0
Features
Security

Suricata IDS/IPS

Monitors network traffic in real-time.

Blocks suspicious activities such as:

Port scanning (e.g., Nmap).

DoS attacks and large packet floods.

Spam and other malicious network behaviors.

Squid Proxy

Access Control:
Administrators can define policies to allow or restrict access to specific websites, protecting the internal network from inappropriate or harmful content.

Traffic Monitoring & Reporting:
Provides detailed reports and analytics on user web activity, helping to optimize network performance and enforce usage policies.

File Sharing and Backup

The Windows Server provides shared folders accessible by all departments.

Automatic data backup is configured to prevent data loss in case of hardware failure or cyber incidents.

Project Goals

Design and implement a secure enterprise network using open-source and virtualized tools.

Demonstrate segmentation with VLANs to isolate departments and improve network security.

Implement DMZ architecture for safe external access to public services such as web and mail servers.

Deploy pfSense with advanced security tools (Suricata & Squid) to provide:

Intrusion detection and prevention.

Web proxy filtering and access control.

Centralize file storage and data backup for business continuity.

Tools Used

GNS3 – Network simulation.

pfSense – Firewall and routing.

Suricata – Intrusion detection and prevention system (IDS/IPS).

Squid Proxy – Web traffic filtering and monitoring.

Windows Server 2022 – File sharing and data backup.

Virtual PCs & Routers – Simulating user endpoints and network devices.

Future Improvements

Integration with Wazuh or ELK Stack for centralized log management and advanced security analytics.

Implement VPN access for secure remote connectivity.

Add Load Balancer to enhance web server performance and availability.

Demo:
https://www.youtube.com/playlist?list=PLFb35DC5uB-pdBY27LXny0KMYQsVUNmV_
