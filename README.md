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

1. **Verify Network Connectivity**  
   The CEO PC must be able to access [seclab.net](http://www.seclab.net). If the page fails to load, troubleshoot using Linux commands (e.g., `ping`) to diagnose network issues between machines.

---

#### **Solution: Verify Network Connectivity**

1. **Attempt to Access seclab.net via Firefox**  
   - **Action:** Launched Firefox on the CEO PC and navigated to **`www.seclab.net`**.  
   - **Result:** Firefox displayed a **"Server not found"** error, indicating a potential connectivity issue.  
   ![Firefox Error - Server Not Found](images/ceo-pc/ceo_pc_seclab_not_reachable.png)

2. **Ping the Web Server (10.200.0.12)**  
   - **Action:** Executed `ping 10.200.0.12` from the CEO PC to test connectivity to the web server.  
   - **Result:** Received **"Destination Host Unreachable"**, confirming the web server was not accessible from the CEO PC.  
   ![Ping to Web Server - Unreachable](images/ceo-pc/ceo_pc_web_not_reachable.png)

3. **Ping the DNS Server (10.200.0.11)**  
   - **Action:** Ran `ping 10.200.0.11` to check connectivity with the DNS server.  
   - **Result:** Received **"Destination Host Unreachable"**, indicating that the DNS server was also inaccessible.  
   ![Ping to DNS Server - Unreachable](images/ceo-pc/ceo_pc_dns_server_not_Reachable.png)

4. **Inspect the IP Configuration**  
   - **Action:** Used the command `ip addr` on the CEO PC to review the network interface settings.  
   - **Result:**  
     - The **IP address** was incorrectly set to **203.0.113.69/24**, which does not align with the expected **192.168.0.0/24** trusted network.  
     - This incorrect IP address caused the CEO PC to be isolated from the DMZ and other internal resources.  
   ![Incorrect IP Address](images/ceo-pc/ceopc_incorrect_ip.png)

5. **Analyze and Adjust IP Settings**  
   - **Action:** Checked the **IPv4 settings** of the **Auto eth2** connection.  
   - **Result:**  
     - The **IP address**, **default gateway**, and **DNS server** were incorrectly set within the **203.0.113.0/24 subnet**, preventing proper communication.  
     - According to the **network diagram**:
       - The CEO PC should have an IP address within the **192.168.0.0/24 trusted network**.
       - The **default gateway** should also be within the **trusted network** (192.168.0.x) for correct routing.
       - The **DNS server** should be accessible within the **DMZ (10.200.0.8/29)**, allowing name resolution for internal services.  
   ![Incorrect Network Settings](images/ceo-pc/ceo_pc_edit_ip_Setting.png)

6. **Switch to Automatic DHCP Configuration**  
   - **Decision:**  
     - **Option 1:** Manually assign the correct IP, gateway, and DNS settings to align with the trusted network.  
     - **Option 2:** Switch to **Automatic DHCP** to dynamically receive the appropriate network configuration.

   - **Chosen Solution:**  
     The decision to use **Automatic DHCP** ensured that the CEO PC would receive the correct IP address, gateway, and DNS settings without manual intervention.  
     
     During the import of virtual machines into **VirtualBox**, the option to **"Include all network adapter MAC addresses"** was enabled. This choice guaranteed that each virtual machine, including the CEO PC, would receive a unique MAC address, avoiding potential conflicts.  
     
     Using DHCP reduced the risk of human error and ensured that network settings aligned with the trusted network configuration. This approach provided a more reliable, scalable solution for maintaining proper connectivity across all virtual machines.  
   ![Changed Method to DHCP](images/ceo-pc/ceo_pc_changed_method.png)

7. **Test Connectivity to Web and DNS Servers**  
   - **Action:**  
     - Ran `ping -c6 10.200.0.12` to verify communication with the web server.  
     - Ran `ping -c4 10.200.0.11` to check connectivity with the DNS server.  

   - **Result:** Both pings were **successful**, confirming that communication with the servers had been restored.  
   ![Ping to Web Server - Successful](images/ceo-pc/ceo_pc_web_reachable.png)  
   ![Ping to DNS Server - Successful](images/ceo-pc/ceo_pc_dns_server_reachable.png)

8. **Reopen Firefox and Confirm Access to seclab.net**  
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


