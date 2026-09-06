# Cybersecurity Lab Environment Setup

Building an isolated virtual lab for penetration testing and ethical hacking practice.

---

## Project Overview

This project focuses on setting up a **virtual cybersecurity and penetration-testing laboratory** using VirtualBox and Kali Linux.

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly.

The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

---

## Objectives

The main objectives of this project are to:

* Install and configure VirtualBox.
* Install/Import Kali Linux as a virtual machine.
* Create a private **NAT Network** for the cybersecurity lab.
* Configure network connectivity for Kali Linux.
* Assign a consistent IP address to the Kali VM.
* Verify network connectivity and DNS resolution.
* Take a clean VM snapshot for recovery.
* Document the complete setup process.
* Prepare the environment for future cybersecurity projects.

---

## 🛡️ Purpose of the Lab

The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing.

It can be used for activities such as:
* Network reconnaissance
* Port scanning
* Vulnerability assessment
* Packet analysis
* Web security testing
* Exploitation practice
* Security-tool experimentation

> ⚠️ **Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.

---

## ⚙️ Lab Configuration

| 🧩 Component | ⚙️ Configuration |
| :--- | :--- |
| **Host OS** | Windows 11 |
| **Host RAM** | 16 GB |
| **Processor** | Intel Core i5-4200M @ 2.50GHz (2 Cores, 4 Threads) |
| **Hypervisor** | VirtualBox 7.0 |
| **Security OS** | Kali Linux |
| **Kali RAM** | 4096 MB |
| **Virtual Network** | NAT Network |
| **Network Address** | 10.0.0.0/24 |
| **Kali IP Address** | 10.0.0.5/24 |
| **Default Gateway** | 10.0.0.1 |
| **DNS Server** | 8.8.8.8 |

---

## 🛠️ Lab Setup Procedure

### Step 1. Install WinRAR
WinRAR was installed and used as the archive extraction utility to extract the Kali Linux virtual machine package (.7z archive).

* **Tool:** WinRAR

### Step 2. Install VirtualBox
VirtualBox was installed as the primary hypervisor to manage virtual machines.

### Step 3. Create the NAT Network
A dedicated NAT Network was created in VirtualBox to allow isolated internal communication between lab VMs while maintaining outbound internet access.

* **Configuration:**
  * Network Name: `NatNetwork`
  * IPv4 Prefix: `10.0.0.0/24`
  * DHCP: `Enabled`
  * IPv6: `Disabled`

<img width="806" height="526" alt="kali-linux " src="https://github.com/user-attachments/assets/fccfb66a-74e8-45c5-a8fd-4849e3b44e6e" />



### Step 4. Import & Configure Kali Linux
The Kali Linux VM was imported into VirtualBox and attached to the custom NAT Network.

* **Network Adapter Settings:**
  * Adapter 1: Attached to `NAT Network`
  * Name: `NatNetwork`
* **RAM Allocated:** 4096 MB

<img width="1365" height="710" alt="kali-linux-setup" src="https://github.com/user-attachments/assets/491a401d-bdcc-44a5-b0df-20f6f6d9110d" />


### Step 5. Configure Kali Linux Network
The Kali Linux network interface was configured and verified with a consistent IPv4 address within the subnet.

* **Configuration Details:**
  * IP Address: `10.0.0.5`
  * Subnet Mask: `255.255.255.0` (`/24`)
  * Gateway: `10.0.0.1`
  * DNS: `8.8.8.8`

 <img width="930" height="471" alt="documentation" src="https://github.com/user-attachments/assets/435e8294-3e3b-4953-b391-27d6a69d7658" />


### Step 6. Create a Clean VM Snapshot
After completing the initial setup and confirming full network connectivity, a clean baseline snapshot was created.

* **Snapshot Name:** `Clean Kali - Network Setup`

The snapshot represents the clean baseline of the laboratory. If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline instantly.

<img width="771" height="250" alt="snapshot" src="https://github.com/user-attachments/assets/addb47c8-4d41-4d43-bb5a-8d99da450276" />


---


## 🔍 Lab Verification

| 🗂️ Test | 💻 Command | 🎯 Expected Result |
| :--- | :--- | :--- |
| **Check IP address** | `ip a` | Correct Kali IP (`10.0.0.5`) displayed |
| **Test gateway** | `ping -c 4 10.0.0.1` | Successful replies |
| **Test Internet connectivity** | `ping -c 4 8.8.8.8` | Successful replies |
| **Test DNS resolution** | `nslookup google.com` | Domain resolves successfully |
| **Verify Nmap** | `nmap --version` | Nmap version displayed |
| **Verify snapshot** | Restore snapshot and run `ip a` | Baseline configuration restored |

### Example Results

* **IP Address:** `10.0.0.5/24`
  
* **Gateway:** `10.0.0.1`
  
* **DNS:** `8.8.8.8`

<img width="671" height="594" alt="gateway, public internet, DNS resolution" src="https://github.com/user-attachments/assets/894022e5-e837-4312-b3b1-a02cc6d0fd2a" />

---

## Problems Encountered & Solutions

### Problem 1. Internet Connectivity After Network Configuration
**Issue:** Kali Linux lost internet connectivity after assigning a static IP configuration via NetworkManager.

<img width="1365" height="420" alt="resetting network to NAT Network from NAT" src="https://github.com/user-attachments/assets/c58795c4-4697-41be-a272-92616d36ed46" />

**Solution:** Adjusted IPv4 settings in NetworkManager, refreshed connection parameters, and restarted the connection using: `sudo nmcli connection reload`

### Problem 2. Hardware Virtualization (VT-x) Disabled
**Issue:** VirtualBox threw an error stating hardware virtualization was disabled in BIOS/UEFI.  
**Solution:** Rebooted system into BIOS settings, enabled **Intel VT-x / Virtualization Technology**, saved changes, and restarted VirtualBox.

---

## 💡 What I Learned

* **NAT vs. NAT Network:** Understood that standard NAT isolates individual VMs from each other, while a NAT Network allows inter-VM communication on a shared subnet while retaining outbound internet access.
* **Virtual Networking Fundamentals:** Gained practical experience configuring virtual adapters, subnet masks (`/24`), routing gateways, and DNS resolvers in Linux.
* **VM Snapshot Strategy:** Learned the critical role of creating clean recovery points before performing active security assessments or system modifications.
* **Troubleshooting & Documentation:** Developed skills in identifying network interface issues, applying CLI fixes, and documenting infrastructure builds professionally.

---

## 🔒 Security & Ethical Use

This laboratory environment is intended strictly for educational and authorized penetration-testing purposes. All testing activities are conducted within an isolated network scope.

---

## 👤 Author

* **Name:** Kehinde Precious Akinyami 
* **Role:** Cybersecurity Student

---

## 📌 Project Information

* **Program Name:** Cybersecurity Internship
* **Week:** 01
* **Project:** Cybersecurity & Pentesting Lab Setup
* **Repository:** GitHub
