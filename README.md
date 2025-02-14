# Network Security Groups (NSGs) and Traffic Inspection in Azure

## Overview
This repository provides a structured guide to setting up and analyzing network traffic between Azure Virtual Machines using Network Security Groups (NSGs) and Wireshark.

## Prerequisites
Ensure the following are available before installation:
- Azure Virtual Machines (Windows 10, Ubuntu 20.04)
- Remote Desktop Access (RDP)
- Wireshark for packet analysis
- Basic networking knowledge (ICMP, SSH, DNS, DHCP, RDP)

## Lab Setup
### Part 1: Virtual Machine Deployment
1. **Create a Resource Group in Azure.**
2. **Deploy Virtual Machines:**
   - Windows 10 VM
   - Ubuntu 20.04 VM
   - Ensure both VMs are in the same Virtual Network and Subnet.
   - Use **username/password** authentication for the Linux VM.
3. **Verify Connectivity:**
   - Obtain the private IP address of each VM.
   - Ensure both VMs can communicate within the Virtual Network.

### Part 2: ICMP Traffic Analysis
1. **Use Remote Desktop to access the Windows 10 VM.**
2. **Install Wireshark on Windows 10.**
3. **Start packet capture in Wireshark and filter for ICMP traffic.**
4. **Ping the Ubuntu VM from Windows and observe packets.**
5. **Ping a public website (e.g., `www.google.com`) and analyze traffic.**

### Part 3: Configuring Network Security Groups
1. **Initiate a continuous ping from Windows 10 to Ubuntu.**
2. **Modify the NSG to block inbound ICMP traffic to the Ubuntu VM.**
3. **Observe traffic in Wireshark and note the ping failure.**
4. **Re-enable ICMP traffic and verify pings resume.**

### Part 4: Observing Network Traffic in Wireshark
1. **SSH Traffic:**
   - Filter for SSH traffic in Wireshark.
   - Use PowerShell to SSH into the Ubuntu VM: `ssh labuser@<private-IP>`.
   - Observe SSH packet activity.
2. **DHCP Traffic:**
   - Filter for DHCP traffic.
   - Renew the Windows 10 VM's IP: `ipconfig /renew`.
   - Observe DHCP requests in Wireshark.
3. **DNS Traffic:**
   - Filter for DNS traffic.
   - Use `nslookup google.com` to query DNS.
   - Observe DNS request/response packets.
4. **RDP Traffic:**
   - Filter for RDP traffic (`tcp.port == 3389`).
   - Observe continuous traffic due to live screen streaming.

