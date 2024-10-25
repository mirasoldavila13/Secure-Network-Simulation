# Secure-Network-Simulation

## Overview
This project simulates the setup, configuration, and security of a virtualized network environment as part of the **UC Santa Barbara Professional and Continuing Education Cybersecurity Program**. The objective is to deploy a network that meets a client’s needs within budget and space constraints. Virtual machines (VMs) are used to implement essential components, including firewalls, web servers, DNS servers, and monitoring systems.

This project demonstrates practical skills in deploying, configuring, and securing IT systems. Through troubleshooting, network analysis, and security baselining, this simulation provides hands-on experience in establishing network solutions tailored to operational and budgetary requirements.

---
## Scenario
You have been hired by an **IT company** as an **IT subject matter expert**. The management team has a **client who wants to upgrade their IT systems**, but the client has a **limited budget** and **no more physical space** to install new equipment. 

To solve this issue, you suggest implementing **virtual machines** instead of additional hardware to help **reduce costs** and meet the client’s operational needs. As part of the upgrade, the following components will be installed:
- **Firewall**
- **CEO's PC**
- **Internal Webserver**
- **Internal DNS server**
- **Linux machines** for monitoring and conducting cybersecurity tasks

Once the new network is installed, your task is to **document configurations** and create a **security baseline** by scanning for **open ports**.


---

## Technologies and Tools Used
- **VirtualBox:** Used to create and manage virtual machines.
- **Kali Linux and Other Linux Distributions:** Utilized for security testing, network monitoring, and diagnostic tasks (e.g., ping, FTP).
- **Wireshark:** Used for capturing and analyzing network traffic.
- **VMs Deployed:** Router-FW, DNS Server, Web Server, CEO PC, and Kali Linux (Trusted/Untrusted).

---

## Tasks and Deliverables

### Project Tasks
1. **Install VirtualBox and Extensions**  
   Follow the "Project 1 Getting Started" guide to install VirtualBox along with its necessary extensions.

2. **Install Virtual Machines**  
   Deploy the following VMs using VirtualBox:
   - Router-FW  
   - DNS Server  
   - Web Server  
   - CEO PC  
   - Three Kali Linux machines (Kali-Trusted, Kali-Untrusted, and one within the DMZ)

3. **Verify Network Connectivity**  
   Use the CEO PC’s Firefox browser to open [seclab.net](http://www.seclab.net). Troubleshoot any issues if the website fails to load.  
   - Use Linux commands (e.g., `ping`) to diagnose network connectivity issues between machines.

4. **Document IP Configuration**  
   Record the OS version, IP address, subnet mask, default gateway, and DNS server address for the following:
   - CEO PC  
   - Web Server  
   - DNS Server

5. **Download Social Media Security Policy via FTP**  
   From the CEO PC, use FTP to download the policy document from the web server.

6. **Create a New User on the Web Server**  
   Add a new user with a chosen username and password on the web server.

7. **Perform Port Scans Using Nmap**  
   Use Nmap from a Kali Linux machine to scan the DNS and Web servers. Document all open ports and associated protocols.

8. **Capture FTP Traffic with Wireshark**  
   Use Wireshark on Kali Linux to monitor an FTP session between the CEO PC and the Web Server. Capture the username and password transmitted during the session.

---

## Network Diagram


---

## Deliverables

1. **Presentation**  
   Create a PowerPoint presentation with at least 12 slides, including:
   - **Executive Summary**  
   - **Services Performed for the Client**  
   - **Network Issues Identified and Resolved**  
   - **Security Recommendations and Closing Remarks**

2. **Demonstration**  
   Record a live demonstration of the CEO PC successfully opening [seclab.net](http://www.seclab.net) to verify network functionality. This recording will accompany the presentation.

3. **Project Questions**  
   Submit the answers to the following questions:

   - What style or type of DMZ is being deployed?  
       - <details>  
           <summary>Expand to view the answer</summary>  

          The DMZ being deployed is a **Three-Homed Firewall DMZ**, which is a type of **Single Firewall DMZ**.

          ---

          #### **Type: Single Firewall DMZ**  
          A **Single Firewall DMZ** uses one firewall device (Router-FW) to manage and control traffic between the trusted network, the untrusted network, and the DMZ. This centralizes control over all traffic flows through a single point, simplifying management.

          ---

          #### **Design: Three-Homed Firewall DMZ**  
          This design connects the firewall to **three separate networks**:

          1. **Trusted Network (192.168.0.0/24):**  
             Contains internal **virtual machines (VMs)**, including the **CEO PC** and **Kali Linux (Trusted)**, which must be protected from external threats.

          2. **Untrusted Network (172.30.0.0/24):**  
             Contains a **single Kali Linux (Untrusted) VM**, simulating external threats or attackers.

          3. **DMZ (10.200.0.8/29):**  
             Hosts public-facing **VMs**, including the **DNS Server**, **Web Server**, and **Kali Linux (DMZ)**. These VMs are accessible from the untrusted network but are **isolated from the trusted network** to protect sensitive internal systems.

          ---

          #### **Style: Isolated DMZ**  
          The **Isolated DMZ style** ensures limited or no direct access between the DMZ and the trusted network. Here’s how the **Router-FW** enforces traffic control and isolation:

          1. **No direct path between the trusted network and the DMZ:**  
             - All communication between these networks must go **through the Router-FW**, ensuring strict control.  
             - The **DMZ** acts as a buffer zone, allowing public-facing services (like the web and DNS servers) to interact with the untrusted network but **blocking access to sensitive systems** in the trusted network.

          2. **Firewall as the single control point:**  
             - The **Router-FW** allows or denies traffic between networks based on **predefined rules**.  
             - **By default**, traffic between the **DMZ and trusted network** is **blocked**, unless specific rules explicitly allow it (e.g., to permit the CEO PC to access a web service in the DMZ).

          3. **Best Practice for Security:**  
             - Public services like **web and DNS servers** are placed in the **isolated DMZ** to ensure that if these services are compromised, they **cannot directly access the internal network**.

          ---

          #### **Summary:**  
          This deployment uses a **Three-Homed Firewall design** with an **Isolated DMZ style**. It is classified as a **Single Firewall DMZ type** because all traffic is managed by one firewall. This approach enhances security by:
          - **Controlling access** between trusted, untrusted, and DMZ networks.
          - **Isolating the DMZ** to protect sensitive internal systems.
          - **Limiting exposure** to external threats.

      </details>


   - Describe any issues encountered on the CEO PC and how you resolved them.
   - List the OS version and IP configuration (IP address, subnet mask, gateway, and DNS server) of the CEO PC.
   - List the OS version and IP configuration of the Web Server.
   - List the OS version and IP configuration of the DNS Server.
   - List the open ports and protocols on the Web Server.
   - List the open ports and protocols on the DNS Server.
   - What is the purpose of a security baseline for a server
   - What are the contents of the file you transferred with FTP to the CEO computer?
   - What credentials were captured by Wireshark during the FTP session?


