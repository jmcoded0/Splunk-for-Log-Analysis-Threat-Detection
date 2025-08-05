# 🛡️ Splunk for Log Analysis & Threat Detection

## 🔍 Project Overview

This project documents the setup of a **virtual cybersecurity lab** using **Splunk Enterprise** to simulate real-world **log collection**, **threat detection**, and **incident analysis**. The lab showcases how to use Splunk as a SIEM solution in a controlled, hands-on environment.

---

## 🧩 Key Components

- **Splunk Enterprise** – Central SIEM platform for indexing and analyzing logs  
- **Kali Linux** – Hosts the Splunk Enterprise instance and acts as an attacker/log generator  
- **VirtualBox** – Used to virtualize the lab environment  
- **SSH** – Enables secure remote access into the VM

---

## 🧱 Lab Setup & Walkthrough

📘 **Full Lab Documentation with Screenshots & Commands:**  
👉 [View Full Lab Guide](https://github.com/jmcoded0/Splunk-Cybersecurity-Lab-/blob/main/docs/Splunk-Cybersecurity-Lab.md)
Includes:
- Kali VM setup
- Network configuration
- Splunk installation
- Log forwarding
- SPL-based threat detection

---

## 🧪 Project Phases

1. **🔧 Splunk Server Setup & SSH Access**  
   Configured Kali Linux, enabled SSH, updated packages, and prepared for Splunk install.

2. **📦 Splunk Enterprise Installation**  
   Downloaded and installed Splunk. Set up admin credentials and enabled the web UI.

3. **📤 Log Forwarder Setup**  
   Deployed **Splunk Universal Forwarder** on Kali and configured it to send logs locally.

4. **📈 Data Ingestion & Event Simulation**  
   Simulated system events and attacks (e.g., SSH brute-force, nmap scans) and verified ingestion.

5. **🕵️ Threat Detection & Analysis**  
   Used **SPL (Search Processing Language)** to analyze logs and detect suspicious behavior.

6. **📝 Conclusion & Learnings**  
   Reflected on key outcomes, issues faced, and lessons learned during the lab build.

---

## 📌 Technologies Used

- Kali Linux  
- Splunk Enterprise 9.x  
- Splunk Universal Forwarder  
- VirtualBox  
- SSH

---

## 🧠 Lessons Learned

- Hands-on experience with SIEM tools and log ingestion  
- Importance of **centralized logging** for visibility  
- Writing & interpreting **SPL queries** for security analysis  
- Emulating attacker behavior in a safe lab environment

---

> 🚀 This lab was created for personal learning, portfolio development, and demonstration of cybersecurity skills using real-world tools.
