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

Below are the key tasks completed during the project. The **detailed answers and results** will be provided in the **Project Questions and Answers section**.

1. **Verify Network Connectivity**  
   Use the CEO PC’s Firefox browser to open [seclab.net](http://www.seclab.net). Troubleshoot any issues if the website fails to load.
   - Use Linux commands (e.g., `ping`) to diagnose network connectivity issues between machines.
## Project Tasks

### 1. Verify Network Connectivity  
Use the CEO PC’s Firefox browser to open [seclab.net](http://www.seclab.net). If the page fails to load, troubleshoot the issue using Linux commands (e.g., `ping`) and check the network configuration.

---

#### **Step 1:** Attempt to Access seclab.net via Firefox  
- **Action:** Launched Firefox on the CEO PC and navigated to **`www.seclab.net`**.  
- **Result:** Firefox displayed a **"Server not found"** error, indicating a potential connectivity issue.  
![Firefox Error - Server Not Found](images/ceo-pc/ceo_pc_seclab_not_reachable.png)

---

#### **Step 2:** Ping the Web Server (10.200.0.12)  
- **Action:** Executed `ping 10.200.0.12` from the CEO PC to test connectivity to the web server.  
- **Result:** Received **"Destination Host Unreachable"**, confirming the web server was not accessible from the CEO PC.  
![Ping to Web Server - Unreachable](images/ceo-pc/ceo_pc_web_not_reachable.png)

---

#### **Step 3:** Ping the DNS Server (10.200.0.11)  
- **Action:** Ran `ping 10.200.0.11` to check connectivity with the DNS server.  
- **Result:** Received **"Destination Host Unreachable"**, indicating that the DNS server was also inaccessible.  
![Ping to DNS Server - Unreachable](images/ceo-pc/ceo_pc_dns_server_not_Reachable.png)

---

#### **Step 4:** Inspect the IP Configuration  
- **Action:** Used the command `ip addr` on the CEO PC to review the network interface settings.  
- **Result:**  
  - The **IP address** was incorrectly set to **203.0.113.69/24**, which does not align with the expected **192.168.0.0/24** trusted network.  
  - This incorrect IP address caused the CEO PC to be isolated from the DMZ and other internal resources.  
![Incorrect IP Address](images/ceo-pc/ceopc_incorrect_ip.png)

---

#### **Step 5:** Analyze and Adjust IP Settings  
- **Action:** Checked the **IPv4 settings** of the **Auto eth2** connection.  
- **Result:**  
  - The **IP address**, **default gateway**, and **DNS server** were incorrectly set within the **203.0.113.0/24 subnet**, preventing proper communication.  
  - According to the **network diagram**:
    - The CEO PC should have an IP address within the **192.168.0.0/24 trusted network**.
    - The **default gateway** should also be within the **trusted network** (192.168.0.x) for correct routing.
    - The **DNS server** should be accessible within the **DMZ (10.200.0.8/29)**, allowing name resolution for internal services.  
![Incorrect Network Settings](images/ceo-pc/ceo_pc_edit_ip_Setting.png)

---

#### **Step 6:** Switch to Automatic DHCP Configuration  
- **Decision:**  
  - **Option 1:** Manually assign the correct IP, gateway, and DNS settings for the trusted network.  
  - **Option 2:** Switch to **Automatic DHCP** to dynamically receive the correct configuration.  

- **Chosen Solution:** Switched the **IPv4 method** to **Automatic DHCP** to ensure proper IP assignment. This approach minimized the risk of configuration errors since all VM **MAC addresses** were correctly imported.  
![Changed Method to DHCP](images/ceo-pc/ceo_pc_changed_method.png)

---

#### **Step 7:** Test Connectivity to Web and DNS Servers  
- **Action:**  
  - Ran `ping -c6 10.200.0.12` to verify communication with the web server.  
  - Ran `ping -c4 10.200.0.11` to check connectivity with the DNS server.  

- **Result:** Both pings were **successful**, confirming that communication with the servers had been restored.  
![Ping to Web Server - Successful](images/ceo-pc/ceo_pc_web_reachable.png)  
![Ping to DNS Server - Successful](images/ceo-pc/ceo_pc_dns_server_reachable.png)

---

#### **Step 8:** Reopen Firefox and Confirm Access to seclab.net  
- **Action:** Launched Firefox again and navigated to **`www.seclab.net`**.  
- **Result:** The page loaded successfully, confirming the network issue was resolved.  
![Successful Access to seclab.net](images/ceo-pc/ceo_seclba_reachable.png)

---


2. **Document IP Configuration**  
   Record the OS version, IP address, subnet mask, default gateway, and DNS server address for the following:
   - CEO PC  
   - Web Server  
   - DNS Server

3. **Download Social Media Security Policy via FTP**  
   From the CEO PC, use FTP to download the policy document from the web server.

4. **Create a New User on the Web Server**  
   Add a new user with a chosen username and password on the web server.

5. **Perform Port Scans Using Nmap**  
   Use Nmap from a Kali Linux machine to scan the DNS and Web servers. Document all open ports and associated protocols.

6. **Capture FTP Traffic with Wireshark**  
   Use Wireshark on Kali Linux to monitor an FTP session between the CEO PC and the Web Server. Capture the username and password transmitted during the session.

---

## Network Diagram
Below is the network diagram showcasing the design and setup of the virtualized network.

![Network Diagram](images/network-diagram/network_diagram.png)

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

3. **Project Questions and Answers**  
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


