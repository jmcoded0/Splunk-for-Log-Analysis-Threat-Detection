
# 🛡️ **Splunk for Log Analysis & Threat Detection**

Hey there! Welcome to my detailed documentation for setting up a virtual cybersecurity lab. This isn't just a dry guide; it's a step-by-step journey through building a powerful environment with **Splunk Enterprise** to get hands-on with log collection, threat detection, and incident analysis. Think of it as a peek into how I'm using Splunk as a SIEM solution in a truly practical way.

---

## 🔍 **Project Overview: Why I Built This Lab**

So, what's this whole project about? It's my personal quest to really get to grips with **real-world log collection, threat detection, and incident analysis** using **Splunk Enterprise**. I wanted a safe, controlled space where I could simulate security operations, mess around, break things (and fix them!), and truly understand how a SIEM works. This lab is all about getting those practical skills locked in!

---

## 🧩 **The Awesome Gear I'm Using (Key Components)**

To bring this cybersecurity playground to life, I'm relying on a few core pieces of tech:

* **Splunk Enterprise:** This is the heart of the operation, my central SIEM platform. It's where all the magic happens – collecting, indexing, searching, analyzing, and visualizing tons of log data. In this lab, it's hosted directly on my Kali Linux VM.

* **Kali Linux (My Combined Brain & Attack Machine):** This is where everything comes together! Kali Linux hosts my Splunk Enterprise instance, making it the robust backend that keeps everything humming along. It's also my "threat" machine, used to generate all sorts of juicy security events and logs – everything from network scans to brute-force attempts. It will also host the Splunk Universal Forwarder to send its own logs over to its own Splunk instance.

* **VirtualBox:** My virtualization superhero. This is how I'm running my Kali Linux VM, keeping my lab neatly contained and isolated from my main system.

* **SSH (My Remote Control):** Super handy for securely jumping into my Kali VM from my host machine. It makes running commands and moving files around a breeze.

---

## 🧱 **Lab Setup & Walkthrough: Let's Get Our Hands Dirty!**

Alright, this is the really exciting part – the actual setup! I'm going to walk you through each phase, and I've made sure to point out exactly where your awesome screenshots will fit in to show off your progress.

### 1. 🔧 **Getting My Kali Linux VM Ready & Essential Setup**

This first phase is all about prepping that Kali Linux virtual machine, making sure it's snug and ready for both general use and hosting Splunk, and that I can securely interact with it.

#### 1.1. **Creating and Installing the Kali Linux Virtual Machine**

* **My Action:** The very first step was to fire up VirtualBox and create a brand-new virtual machine specifically for Kali Linux. I made sure to give it enough RAM, CPU, and storage – gotta make Splunk and Kali happy, right? Then, I installed Kali Linux OS, following the prompts, creating my user account, and getting the basic network stuff squared away.


![Kali Linux Desktop After Installation]![VirtualBox_kali linux_19_06_2025_00_36_41](https://github.com/user-attachments/assets/9ae4ee35-03c2-4728-a08d-46ece525b81a)


#### 1.2. **Setting Up My Network & Guest Additions**

* **My Action:** Networking can sometimes be a bit tricky, but it's crucial! I configured the network adapter for my Kali VM. I usually go with a **NAT Adapter** to easily get internet access for updates and downloads. Crucially, I installed **VirtualBox Guest Additions** to enable essential features like automatic screen resizing, bidirectional copy/paste, and shared folders, which are vital for a smooth workflow.


![VirtualBox Kali Network Settings]<img width="960" alt="ubuntu begn1" src="https://github.com/user-attachments/assets/18cf06c6-5587-495e-9ac1-83ec4232c3b5" />


#### 1.3. **Getting SSH Ready (Server Installation and Configuration)**

* **My Action:** SSH is a lifesaver for remote access. I installed `openssh-server` on my Kali VM and then double-checked that it was running smoothly. I also made sure my firewall (UFW) was cool with SSH traffic.
* **Command:** `sudo apt update && sudo apt upgrade -y` (Always a good idea to update!)
* **Command:** `sudo apt install openssh-server -y`
* **Command:** `sudo systemctl status ssh` (Checking that service!)
* **Command:** `sudo ufw allow ssh` (Opening that port!)


### 2. 📦 **Installing Splunk Enterprise (Kali Linux VM) – The Big One!**

This is the core phase: getting Splunk Enterprise up and running directly on my Kali Linux VM.

#### 2.1. **Downloading Splunk Enterprise**

* **My Action:** I used `wget` to grab the Splunk Enterprise Debian package (`.deb`) directly onto my Kali VM. This saves a lot of hassle.
* **Command:** `wget -O splunk-enterprise.deb 'https://download.splunk.com/products/splunk/releases/9.4.3/linux/splunk-9.4.3-237ebbd22314-linux-amd64.deb'` (Always use the specific version downloaded).


![Splunk Download Completion on Kali]<img width="960" alt="ubuntu ss1" src="https://github.com/user-attachments/assets/f712bf31-8cd9-4f86-918e-2fd3d99e2b0d" />


#### 2.2. **Install Splunk Enterprise**

* **My Action:** With the `.deb` file in hand, installing Splunk was straightforward using `dpkg`. I navigated to the directory where the `.deb` file was located (which was my shared folder `/media/sf_Downloads`).
* **Command:** `cd /media/sf_Downloads`
* **Command:** `sudo dpkg -i splunk-9.4.3-237ebbd22314-linux-amd64.deb`


![Splunk dpkg Installation Process on Kali]<img width="960" alt="ubuntu ss3" src="https://github.com/user-attachments/assets/cb893c97-b6f0-437f-a43e-1e657af69388" />

#### 2.3. **Start Splunk and Accepting the License**

* **My Action:** First boot! I started the Splunk service and, of course, had to agree to their license terms.
* **Command:** `sudo /opt/splunk/bin/splunk start --accept-license`


![Splunk Service Start and License Prompt on Kali]![VirtualBox_kali linux_19_06_2025_02_33_53](https://github.com/user-attachments/assets/d35d4f09-3c59-449f-a7f3-79d2aa619853)

#### 2.4. **Setting Up My Splunk Admin & Auto-Start**

* **My Action:** Security first! I set a strong password for my Splunk admin user when prompted during the initial start. Then, I made sure Splunk would automatically kick off every time the server boots up – super convenient.
* **Command:** `/opt/splunk/bin/splunk enable boot-start`


#### 2.5. **Accessing the Splunk Web Interface (Woohoo!)**

* **My Action:** The payoff! I opened my web browser (on my Kali VM itself) and navigated to the Splunk web interface using `localhost:8000`. Then, I logged in with my shiny new admin credentials.


![Splunk Web Login Page on Kali]![VirtualBox_kali linux_18_06_2025_13_46_58](https://github.com/user-attachments/assets/8b1511d5-42e1-460c-ad84-75ca9550a08b)



![Splunk Home Dashboard After Login on Kali]![VirtualBox_kali linux_18_06_2025_13_47_58](https://github.com/user-attachments/assets/32580a41-c479-4c4e-a8ce-58b3c943b7a9)


### 3. 📤 **Setting Up My Log Forwarder (On Kali Linux Itself)**

Now that Splunk's ready, it's time to get some logs flowing from Kali *into its own Splunk instance*! This phase involves deploying the Splunk Universal Forwarder on Kali to send Kali's system and security logs over to the Splunk Enterprise instance running on the same machine.

#### 3.1. **Downloading and Installing the Splunk Universal Forwarder**

* **My Action:** Time to get the forwarder onto Kali! I downloaded the Splunk Universal Forwarder package (using `wget`) and then installed it.
* **Command:** `wget -O splunkforwarder.deb 'https://download.splunk.com/products/universalforwarder/releases/9.x.x/linux/splunkforwarder-9.x.x-amd64.deb'` (Remember to find the correct `9.x.x` version number on the Splunk website for the forwarder).
* **Command:** `sudo dpkg -i splunkforwarder.deb`


![Splunk Universal Forwarder Download and Installation on Kali]![VirtualBox_kali linux_19_06_2025_03_22_09](https://github.com/user-attachments/assets/6bd0384d-1a90-4b54-96ee-5399d0124e79)


#### 3.2. **Configuring the Universal Forwarder to Send Logs**

* **My Action:** This is where I tell the forwarder *where* to send logs (my local Splunk Enterprise instance) and *which* logs to send. It involves editing two crucial configuration files: `outputs.conf` and `inputs.conf`.

* **Editing `outputs.conf` (`/opt/splunkforwarder/etc/system/local/outputs.conf`):** This file tells the forwarder where its data should go. I set the `server` to `localhost` and the standard Splunk forwarder port `9997`, since Splunk Enterprise is on the same machine.
```ini
[tcpout]
defaultGroup = default_group

[tcpout:default_group]
server = 127.0.0.1:9998 # Sending logs to localhost (itself)
```

* **Editing `inputs.conf` (`/opt/splunkforwarder/etc/system/local/inputs.conf`):** This file tells the forwarder *what* logs to monitor and send. I set it up to grab the system logs (`syslog`) and authentication logs (`auth.log`).
```ini
[monitor:///var/log/syslog]
sourcetype = syslog

[monitor:///var/log/auth.log]
sourcetype = linux_auth
```


![Universal Forwarder outputs.conf and inputs.conf Configuration on Kali]![VirtualBox_kali linux_19_06_2025_03_11_26](https://github.com/user-attachments/assets/f1228aee-22e1-4fc7-9b6f-b4ec3ca67295)


#### 3.3. **Start and Enable Universal Forwarder**

* **My Action:** After configuration, I started the Splunk Universal Forwarder service on Kali and made sure it would automatically start on boot.
* **Command:** `/opt/splunkforwarder/bin/splunk start --accept-license`
* **Command:** `/opt/splunkforwarder/bin/splunk enable boot-start`


![Universal Forwarder Start and Enable Boot-Start on Kali]![VirtualBox_kali linux_19_06_2025_03_31_33](https://github.com/user-attachments/assets/e13985e2-1bc3-4d4c-81cb-055c0fa24a62)


#### 3.4. **Configuring Data Input on Splunk Enterprise (The Receiving End on Kali!)**

* **My Action:** My forwarder is sending logs, but Splunk needs to know to *receive* them! On the Splunk Enterprise web interface (which is on Kali itself), I navigated to **Settings > Data Inputs > Forwarded inputs** and added a new TCP input on port `9998` (the same port the forwarder is sending to!).


![Splunk Web UI - Forwarded Input Configuration on Kali]![VirtualBox_kali linux_19_06_2025_03_58_01]![VirtualBox_Kali Linux_25_06_2025_03_11_11](https://github.com/user-attachments/assets/eff55e03-5335-4554-9501-3dd17e70a0eb)


### 4. 📈 **Data Ingestion & Event Simulation: Making Some Noise!**

Now that the pipes are connected, it's time to actually generate some events on Kali Linux and verify that they're showing up in Splunk Enterprise. This is where the fun starts!

#### 4.1. **Generating Sample Logs on Kali**

* **My Action:** To get some data flowing, I performed various actions on Kali Linux that would naturally generate common system logs. Think of it as creating a little digital ruckus!
* **Command (Simulating failed SSH login attempts):** `ssh fakeuser@localhost` (I ran this a few times to generate some "failed password" entries!)
* **Command (Sudo usage):** `sudo whoami` (Simple, but effective for log generation)
* **Command (Running a small Nmap scan):** `nmap -sS -p 1-100 127.0.0.1` (This generates network-related logs, if your forwarder is set up to capture them!)


![Kali Linux Log Generation Commands]![VirtualBox_Kali Linux_25_06_2025_03_33_09](https://github.com/user-attachments/assets/bec308f0-3f36-4b3b-9138-63fce22e6723)

#### 4.2. **Verifying Data Ingestion in Splunk (The Payoff!)**

* **My Action:** After generating logs on Kali, I immediately jumped back to the Splunk Enterprise web interface. I went to the **Search & Reporting** app and searched for `index=main` or `source="/var/log/syslog"` to confirm that logs from my Kali machine were indeed pouring in. It's such a satisfying feeling to see them!


![Splunk Search and Reporting - Raw Events from Kali]![VirtualBox_Kali Linux_25_06_2025_03_06_30](https://github.com/user-attachments/assets/8d0e4163-a104-4c5b-836f-5e1acfb40052)


### 5. 🕵️ **Threat Detection & Analysis with SPL: Becoming a Cyber Sleuth!**

This phase focuses on using Splunk's Search Processing Language (SPL) to analyze the ingested logs and identify potential security threats or anomalies.

#### 5.1. **Basic Log Search and Filtering**

* **My Action:** I started with the fundamentals: practicing basic SPL queries to filter logs by `sourcetype`, `host`, or specific keywords. Gotta learn to walk before you can run, right?
* **Example SPL:** `index=main sourcetype=syslog host=` (Just grabbing all syslog events from Kali)
* **Example SPL:** `index=main "failed password"` (Quickly finding all failed login attempts)


![Splunk Search - Basic Log Filtering]![VirtualBox_Kali Linux_25_06_2025_03_51_19](https://github.com/user-attachments/assets/7af54e48-7f04-4738-9dbb-793e7ae174b6)


#### 5.2. **Detecting Brute-Force Attempts**

* **My Action:** This is a classic! I used SPL to look for multiple failed login attempts coming from the same source within a short time. This is a common indicator of a brute-force attack.
* **Example SPL:** `index=main sourcetype=dpkg_log | timechart count by host` (This query counts failed passwords by source IP and then filters for IPs with more than 5 attempts.)

![Splunk Search - Brute-Force Detection]![VirtualBox_Kali Linux_25_06_2025_03_56_18](https://github.com/user-attachments/assets/40097d98-bf9a-40c7-aba0-9985e3527ae7)

#### 5.3. **Analyzing Package Activity (Illustrative Detection)**

* **My Action:** While actual port scan detection typically requires network-specific logs (which I currently don't have flowing), I used SPL to analyze a different type of activity: package installation and removal events from my `dpkg.log`. This demonstrates the power of SPL for identifying patterns within existing log sources. I looked for instances of "installed" packages and grouped them by host to understand common software changes.
* **Example SPL:** `index=main sourcetype=dpkg_log "installed" | stats count by host` (This query counts how many "installed" events occurred for each host.)


    ![Splunk Search - Package Activity Analysis]![VirtualBox_Kali Linux_25_06_2025_04_10_30](https://github.com/user-attachments/assets/1acca73e-5acf-4357-b0b5-77c4cf9cb32b)


#### 5.4. **Creating Alerts or Dashboards (Optional but Cool!)**

* **My Action:** If I had more time, I'd totally build out some alerts or dashboards. Alerts would notify me immediately of a potential threat, and dashboards would give me a sweet visual overview of my lab's security posture. This is where Splunk really shines for continuous monitoring!


![Splunk Alert Configuration or Basic Dashboard]![VirtualBox_Kali Linux_25_06_2025_04_20_23](https://github.com/user-attachments/assets/9dd9eff7-746b-4277-8a26-0d806abf3d5a)

### 6. 📝 **My Conclusion & What I Learned (Lessons from the Lab!)**

Wrapping up this project, it's cool to reflect on what I achieved and what hitches I ran into. Every challenge was a learning opportunity!

#### 6.1. **My Project Outcomes**

* **Successfully built a virtual cybersecurity lab:** This was a huge win, with Splunk Enterprise and a Universal Forwarder happily talking to each other *on the same Kali Linux VM*.
* **Demonstrated end-to-end log collection:** I got logs flowing from my Kali machine right into my SIEM – super satisfying!
* **Applied SPL for basic log analysis and threat detection:** I got my hands dirty with searches and even some basic threat hunting.


![Splunk App Overview or Final Lab Dashboard]![VirtualBox_Kali Linux_25_06_2025_04_31_20](https://github.com/user-attachments/assets/7318fab7-1650-450c-b3c4-9985f1e8027b)

#### 6.2. **Challenges I Ran Into (And How I Overcame Them!)**

No project is without its bumps, and this lab was no exception!
* **VirtualBox Guest Additions:** This was a significant challenge, with persistent issues around installation, display drivers, copy-paste, and shared folders. Overcoming this required meticulous troubleshooting, manual driver configuration, and ensuring the correct file paths were used for installation.
* **Disk Space Management:** Running out of disk space during critical installation steps was a recurring issue, requiring careful cleanup of package caches and temporary files.
* **Network configuration within VMs:** Getting NAT and Shared Folders to play nice always takes a bit of head-scratching, but it's essential for a smooth workflow and transferring files.
* **Interrupted Installations:** Dealing with `dpkg` when installations were unexpectedly paused (e.g., due to power loss) required specific commands (`dpkg --configure -a`) to resume gracefully.
* **Forwarder config (`outputs.conf` and `inputs.conf`):** Tiny typos here can cause big headaches. Meticulous checking was my friend.
* **Understanding and debugging SPL queries:** This is a whole language in itself! There was a lot of trial and error, but that's how you learn.

#### 6.3. **My Key Takeaways and Lessons Learned**

This lab was packed with learning! Here are some of my biggest takeaways:

* **Centralized Logging is a Game Changer:** Seriously, having all your logs in one place (thanks, Splunk!) makes spotting threats so much easier. It's the core of effective security monitoring.
* **Virtualization Troubleshooting is a Core Skill:** The journey with VirtualBox and Guest Additions taught me invaluable lessons in diagnosing and resolving VM-specific issues that directly impact usability.
* **Threat Hunting Basics are Crucial:** Getting hands-on with searching for indicators of compromise (IOCs) and weird behavior using SPL is invaluable. It's not just theory anymore!
* **Data Normalization Makes Sense:** Seeing how different `sourcetypes` and fields help structure the data for analysis really clicked during this project.
* **Lab Environments are Gold:** Building and experimenting in a controlled environment like this is absolutely the best way to learn and develop skills without risking production systems.
