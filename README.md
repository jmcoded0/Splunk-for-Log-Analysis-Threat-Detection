# Splunk-Cybersecurity-Lab-
Setting up a cybersecurity lab with Splunk for log analysis and threat detection.


# Cybersecurity Project: Splunk Log Analysis & Threat Detection Lab

## Project Overview

This repository documents the setup and configuration of a virtualized cybersecurity lab environment utilizing Splunk Enterprise. The project aims to demonstrate end-to-end security monitoring, from log collection to threat detection and analysis, using industry-standard tools.

### Key Components:
* **Splunk Enterprise:** For SIEM capabilities, log indexing, searching, and visualization.
* **Ubuntu Server:** Hosts the Splunk Enterprise instance.
* **Kali Linux:** Used as an attacker machine and a source for security logs.
* **VirtualBox:** The virtualization platform for creating the lab environment.
* **SSH:** For reliable remote access and management of VMs.

## Detailed Lab Setup & Walkthrough

For a comprehensive, step-by-step guide on setting up this lab, including all commands, configurations, and screenshots, please refer to the main guide:

👉 [**Go to the Full Setup Guide**](docs/FULL_SETUP_GUIDE.md) 👈

---

## Project Phases:

This project is structured into the following phases:

1.  **Splunk Server Preparation & SSH Access:** Setting up the Ubuntu VM, updating the OS, installing SSH server, and configuring VirtualBox for remote access.
2.  **Splunk Enterprise Installation:** Downloading, installing, and performing initial configuration of Splunk Enterprise on the Ubuntu server.
3.  **Universal Forwarder Deployment:** Installing and configuring Splunk Universal Forwarder on the Kali Linux VM to collect logs.
4.  **Data Ingestion & Event Generation:** Configuring Splunk to receive data and simulating security events from Kali Linux.
5.  **Threat Detection & Analysis:** Utilizing Splunk Search Processing Language (SPL) to identify, analyze, and visualize security incidents.
6.  **Conclusion & Learnings:** Summarizing the project outcomes and key takeaways.

---
