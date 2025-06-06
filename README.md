# 🛡️ Splunk Cybersecurity Lab  
**Setting up a cybersecurity lab with Splunk for log analysis and threat detection**

---

## 🔍 Project Overview

This project documents the setup of a **virtual cybersecurity lab** using **Splunk Enterprise** to simulate real-world **log collection**, **threat detection**, and **incident analysis**. The lab showcases how to use Splunk as a SIEM solution in a controlled, hands-on environment.

---

## 🧩 Key Components

- **Splunk Enterprise** – Central SIEM platform for indexing and analyzing logs  
- **Ubuntu Server** – Hosts the Splunk Enterprise instance  
- **Kali Linux** – Acts as an attacker/log generator machine  
- **VirtualBox** – Used to virtualize the entire lab environment  
- **SSH** – Enables secure remote access to Ubuntu and Kali VMs

---

## 🧱 Lab Setup & Walkthrough

📘 **Full Guide Available:**  
👉 [View Full Setup Instructions](docs/FULL_SETUP_GUIDE.md)

Includes:
- VM creation
- Network configs
- Splunk installation
- Data forwarding setup
- SPL queries for analysis

---

## 🧪 Project Phases

1. **🔧 Splunk Server Setup & SSH Access**  
   Configure Ubuntu VM, enable SSH, update packages, and prep for Splunk install.

2. **📦 Splunk Enterprise Installation**  
   Download and install Splunk on Ubuntu. Set up admin access and enable the web interface.

3. **📤 Log Forwarder Setup**  
   Deploy **Splunk Universal Forwarder** on Kali Linux. Configure it to send logs to the Splunk server.

4. **📈 Data Ingestion & Event Simulation**  
   Simulate system events and attacks (e.g., port scanning, brute force) on Kali and forward logs.

5. **🕵️ Threat Detection & Analysis**  
   Use **SPL (Search Processing Language)** in Splunk to detect anomalies and generate insights.

6. **📝 Conclusion & Learnings**  
   Summarize outcomes, challenges, and what you learned from the setup and threat detection.

---

## 📌 Technologies Used

- Ubuntu 22.04 / 24.04  
- Splunk Enterprise 9.x  
- Kali Linux  
- Splunk Universal Forwarder  
- VirtualBox  
- SSH

---

## 🧠 Lessons Learned

- Hands-on experience with SIEM tools and log management  
- Importance of **centralized logging** in threat detection  
- Understanding of **SPL** queries and dashboarding  
- Basic attacker behavior emulation in a safe lab setup

---

> 🚀 This lab was created for personal learning, portfolio development, and demonstration of cybersecurity skills using industry tools.

