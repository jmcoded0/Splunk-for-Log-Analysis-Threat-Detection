# 🛡️ **My Splunk Cybersecurity Lab: A Deep Dive into Log Analysis & Threat Detection**

Hey there! Welcome to my detailed documentation for setting up a virtual cybersecurity lab. This isn't just a dry guide; it's a step-by-step journey through building a powerful environment with **Splunk Enterprise** to get hands-on with log collection, threat detection, and incident analysis. Think of it as a peek into how I'm using Splunk as a SIEM solution in a truly practical way.

---

## 🔍 **Project Overview: Why I Built This Lab**

So, what's this whole project about? It's my personal quest to really get to grips with **real-world log collection, threat detection, and incident analysis** using **Splunk Enterprise**. I wanted a safe, controlled space where I could simulate security operations, mess around, break things (and fix them!), and truly understand how a SIEM works. This lab is all about getting those practical skills locked in!

---

## 🧩 **The Awesome Gear I'm Using (Key Components)**

To bring this cybersecurity playground to life, I'm relying on a few core pieces of tech:

* **Splunk Enterprise:** This is the heart of the operation, my central SIEM platform. It's where all the magic happens – collecting, indexing, searching, analyzing, and visualizing tons of log data.

* **Ubuntu Server (My Splunk Brain):** This virtual machine is dedicated to hosting my Splunk Enterprise instance. It's the robust backend that keeps everything humming along.

* **Kali Linux (My Attack Machine):** This is where the "threat" part of "threat detection" comes in! I'm using Kali to generate all sorts of juicy security events and logs – everything from network scans to brute-force attempts. It also hosts the Splunk Universal Forwarder, sending those logs over to Splunk.

* **VirtualBox:** My virtualization superhero. This is how I'm running both my Ubuntu server and Kali Linux, keeping my lab neatly contained and isolated from my main system.

* **SSH (My Remote Control):** Super handy for securely jumping into my Ubuntu and Kali VMs from my host machine. It makes running commands and moving files around a breeze.

---

## 🧱 **Lab Setup & Walkthrough: Let's Get Our Hands Dirty!**

Alright, this is the really exciting part – the actual setup! I'm going to walk you through each phase, and I've made sure to point out exactly where your awesome screenshots will fit in to show off your progress.

### 1. 🔧 **Getting My Splunk Server Ready & SSHing In (Ubuntu VM)**

This first phase is all about prepping that Ubuntu virtual machine, making sure it's snug and ready for Splunk, and that I can securely SSH into it whenever I need.

#### 1.1. **Creating the Ubuntu Virtual Machine**

* **My Action:** The very first step was to fire up VirtualBox and create a brand-new virtual machine specifically for Ubuntu. I made sure to give it enough RAM, CPU, and storage – gotta make Splunk happy, right?



#### 1.2. **Installing Ubuntu OS**

* **My Action:** After setting up the VM, I installed Ubuntu Server. I just followed the prompts, created my user account, and got the basic network stuff squared away.



#### 1.3. **Setting Up My Network**

* **My Action:** Networking can sometimes be a bit tricky, but it's crucial! I configured the network adapter for my Ubuntu VM. I usually go with a **Host-Only Adapter** or **Internal Network** to keep my lab isolated, and then add a **NAT Adapter** if I need internet access for updates.

* **Screenshot:** ![image](https://github.com/user-attachments/assets/9e4119d6-cfbb-43a4-a327-6e343358c1b9)

  
After configuring in VirtualBox, I jumped into the Ubuntu terminal to confirm everything was set up as expected from the OS side.
* **Screenshot:** ![VirtualBox_Splunk_Server_Ubuntu_06_06_2025_03_44_37](https://github.com/user-attachments/assets/5d2180d5-536f-4ed7-9186-e33c44b45dda)

    ![Ubuntu ip a command output]

#### 1.4. **Getting SSH Ready (Server Installation and Configuration)**

* **My Action:** SSH is a lifesaver for remote access. I installed `openssh-server` on my Ubuntu VM and then double-checked that it was running smoothly. I also made sure my firewall (UFW) was cool with SSH traffic.
    * **Command:** `sudo apt update && sudo apt upgrade -y` (Always a good idea to update!)
    * **Command:** `sudo apt install openssh-server -y`
    * **Command:** `sudo systemctl status ssh` (Checking that service!)
    * **Command:** `sudo ufw allow ssh` (Opening that port!)


#### 1.5. **My First Remote SSH Connection**

* **My Action:** The moment of truth! From my host machine (or even my Kali VM later), I tested SSH connectivity to my Ubuntu VM. Success feels good!

* **Screenshot:**<img width="960" alt="image" src="https://github.com/user-attachments/assets/3f9435bc-05f5-4ead-8ade-d392f609ff70" />

    Successful SSH Login to Ubuntu

### 2. 📦 **Installing Splunk Enterprise (Ubuntu VM) – The Big One!**

This is the core phase: getting Splunk Enterprise up and running on my freshly prepared Ubuntu server.

#### 2.1. **Downloading Splunk Enterprise**

* **My Action:** I used `wget` to grab the Splunk Enterprise Debian package (`.deb`) directly onto my Ubuntu VM. This saves a lot of hassle.
    * **Command:** `wget -O splunk-enterprise.deb 'https://download.splunk.com/products/splunk/releases/9.x.x/linux/splunk-9.x.x-amd64.deb'` (Just remember to swap out `9.x.x` for the actual version you're using!)

* **Screenshot:**<img width="960" alt="ubuntu ss2" src="https://github.com/user-attachments/assets/615fbdfe-5375-4001-bda1-9800910c4262" />
 This visual confirms the file is being pulled down.
    Splunk Download Progress

* **Screenshot:** And then the completion! This separate screenshot should show the **terminal prompt after the `wget` command has finished downloading**, indicating the Splunk `.deb` file is now fully present in your directory and ready for installation. This verifies the file is locally available.
    ![Splunk Download Completion](YOUR_SCREENSHOT_URL_HERE)

#### 2.2. **Install Splunk Enterprise**

* **My Action:** With the `.deb` file in hand, installing Splunk was straightforward using `dpkg`.
    * **Command:** `sudo dpkg -i splunk-enterprise.deb`

* **Screenshot:** Show that installation in action! This screenshot should capture the **terminal output** as the `dpkg` command executes, displaying all those satisfying messages indicating successful package unpacking and setup progress. This confirms the Splunk files are being laid down.
    ![Splunk dpkg Installation Process](YOUR_SCREENSHOT_URL_HERE)

#### 2.3. **Start Splunk and Accepting the License**

* **My Action:** First boot! I started the Splunk service and, of course, had to agree to their license terms.
    * **Command:** `/opt/splunk/bin/splunk start --accept-license`

* **Screenshot:** Get this moment! This screenshot should capture the **terminal output** showing Splunk spinning up, including the prompt to read and **accept the license agreement**. This is a critical step in getting Splunk operational.
    ![Splunk Service Start and License Prompt](YOUR_SCREENSHOT_URL_HERE)

#### 2.4. **Setting Up My Splunk Admin & Auto-Start**

* **My Action:** Security first! I set a strong password for my Splunk admin user. Then, I made sure Splunk would automatically kick off every time the server boots up – super convenient.
    * **Command:** `/opt/splunk/bin/splunk enable boot-start`

* **Screenshot:** Show those commands and their output! This screenshot should display the **terminal commands and their output** where you set the Splunk admin password (the interactive prompt) and confirm that Splunk has been configured to start on boot (e.g., "boot-start has been enabled"). This secures your Splunk instance and ensures persistence.
    ![Splunk Admin Password and Boot-Start Configuration](YOUR_SCREENSHOT_URL_HERE)

#### 2.5. **Accessing the Splunk Web Interface (Woohoo!)**

* **My Action:** The payoff! I opened my web browser (on my host machine or Kali) and navigated to the Splunk web interface using my Ubuntu VM's IP address (usually `https://your_ubuntu_vm_ip:8000`). Then, I logged in with my shiny new admin credentials.

* **Screenshot:** Capture the moment of truth! This screenshot should display the **Splunk Web Login page** as it appears in your browser, clearly showing the fields for username and password. This indicates the web interface is reachable.
    ![Splunk Web Login Page](YOUR_SCREENSHOT_URL_HERE)

* **Screenshot:** And the ultimate victory! Show the **Splunk Home Dashboard** or initial landing page immediately after successfully logging into the web interface. This confirms Splunk is fully operational and you have access to its powerful features.
    ![Splunk Home Dashboard After Login](YOUR_SCREENSHOT_URL_HERE)

### 3. 📤 **Setting Up My Log Forwarder (Kali Linux VM)**

Now that Splunk's ready, it's time to get some logs flowing! This phase involves getting Kali Linux set up and deploying the Splunk Universal Forwarder to send logs over to my Splunk Enterprise instance.

#### 3.1. **Creating My Kali VM & OS Installation**

* **My Action:** Just like Ubuntu, I spun up a new VM for Kali Linux and got the operating system installed. Ready to generate some logs!

* **Screenshot:** This screenshot should show the **Kali Linux desktop** after a successful installation, displaying its familiar interface, or the **Kali login screen** prompting for credentials. This marks the Kali VM as ready for configuration.
    ![Kali Linux Desktop or Login Screen](YOUR_SCREENSHOT_URL_HERE)

#### 3.2. **Network Configuration for Kali**

* **My Action:** Again, network setup is key. I made sure Kali's network adapters were on the *same isolated network* as my Ubuntu VM. This lets them talk to each other without exposing them to the wider internet (unless I specifically want that for updates).

* **Screenshot:** Show your VirtualBox settings for Kali here. This screenshot should display the **VirtualBox VM settings for the Kali VM**, specifically the "Network" section, illustrating how its adapters are configured (e.g., the Host-Only or Internal Network adapter for communication with Ubuntu). This ensures Kali can reach the Splunk server.
    ![VirtualBox Kali Network Settings](YOUR_SCREENSHOT_URL_HERE)

* **Screenshot:** Confirm it in the terminal! This screenshot should show the **output of the `ip a` command** executed in the Kali terminal, clearly displaying its assigned IP addresses. This verifies Kali's network connectivity within the lab.
    ![Kali ip a command output](YOUR_SCREENSHOT_URL_HERE)

#### 3.3. **Downloading and Installing the Splunk Universal Forwarder**

* **My Action:** Time to get the forwarder onto Kali! I downloaded the Splunk Universal Forwarder package (again, using `wget`) and then installed it.
    * **Command:** `wget -O splunkforwarder.deb 'https://download.splunk.com/products/universalforwarder/releases/9.x.x/linux/splunkforwarder-9.x.x-amd64.deb'`
    * **Command:** `sudo dpkg -i splunkforwarder.deb`

* **Screenshot:** This screenshot should capture the **terminal output** showing both the `wget` command downloading the forwarder package (showing progress) and the subsequent `dpkg` command installing it. This visual confirms the forwarder software is being deployed on Kali.
    ![Splunk Universal Forwarder Download and Installation](YOUR_SCREENSHOT_URL_HERE)

#### 3.4. **Configuring the Universal Forwarder to Send Logs**

* **My Action:** This is where I tell the forwarder *where* to send logs (my Splunk Enterprise instance) and *which* logs to send. It involves editing two crucial configuration files: `outputs.conf` and `inputs.conf`.

    * **Editing `outputs.conf` (`/opt/splunkforwarder/etc/system/local/outputs.conf`):** This file tells the forwarder where its data should go. I set the `server` to my Ubuntu VM's IP address and the standard Splunk forwarder port `9997`.
        ```ini
        [tcpout]
        defaultGroup = default_group

        [tcpout:default_group]
        server = <Ubuntu_Splunk_IP>:9997  # Don't forget to replace this with your Ubuntu VM's actual IP!
        ```

    * **Editing `inputs.conf` (`/opt/splunkforwarder/etc/system/local/inputs.conf`):** This file tells the forwarder *what* logs to monitor and send. I set it up to grab the system logs (`syslog`) and authentication logs (`auth.log`).
        ```ini
        [monitor:///var/log/syslog]
        sourcetype = syslog

        [monitor:///var/log/auth.log]
        sourcetype = linux_auth
        ```

* **Screenshot:** This is an important one! Show the content of both the **`outputs.conf` and `inputs.conf` files** open in a text editor (like `nano` or `vi`) within the Kali terminal. The screenshot should clearly display the configured stanzas, especially the `server` IP in `outputs.conf` and the `monitor` paths in `inputs.conf`. This is key to getting logs flowing.
    ![Universal Forwarder outputs.conf and inputs.conf Configuration](YOUR_SCREENSHOT_URL_HERE)

#### 3.5. **Start and Enable Universal Forwarder**

* **My Action:** After configuration, I started the Splunk Universal Forwarder service on Kali and made sure it would automatically start on boot.
    * **Command:** `/opt/splunkforwarder/bin/splunk start --accept-license`
    * **Command:** `/opt/splunkforwarder/bin/splunk enable boot-start`

* **Screenshot:** Capture the terminal confirming the forwarder is alive and set to auto-start. This screenshot should show the **terminal output** on Kali showing the forwarder service starting up, including the license acceptance, and the confirmation that it has been enabled to start on boot. This ensures your Kali logs will continuously be sent to Splunk.
    ![Universal Forwarder Start and Enable Boot-Start](YOUR_SCREENSHOT_URL_HERE)

#### 3.6. **Configuring Data Input on Splunk Enterprise (The Receiving End!)**

* **My Action:** My forwarder is sending logs, but Splunk needs to know to *receive* them! On the Splunk Enterprise web interface, I navigated to **Settings > Data Inputs > Forwarded inputs** and added a new TCP input on port `9997` (the same port the forwarder is sending to!).

* **Screenshot:** Show how you set this up in Splunk's GUI. This screenshot should display the **Splunk Web UI** showing the steps or a summary of the configuration for creating a new "Forwarded inputs" on port `9997` on the Splunk Enterprise server. This is the crucial step on the Splunk server side to accept incoming logs.
    ![Splunk Web UI - Forwarded Input Configuration](YOUR_SCREENSHOT_URL_HERE)

* **Screenshot:** The ultimate validation! Show a view within Splunk (perhaps the **"Receive data"** section in the Data Inputs settings, or a quick search in `index=_internal` for forwarder health status, like `sourcetype=splunkd group=thruput host=<kali_hostname>`) confirming that data is actively being received from your Kali forwarder. It's working!
    ![Splunk Web UI - Data Receive Confirmation](YOUR_SCREENSHOT_URL_HERE)

### 4. 📈 **Data Ingestion & Event Simulation: Making Some Noise!**

Now that the pipes are connected, it's time to actually generate some events on Kali Linux and verify that they're showing up in Splunk Enterprise. This is where the fun starts!

#### 4.1. **Generating Sample Logs on Kali**

* **My Action:** To get some data flowing, I performed various actions on Kali Linux that would naturally generate common system logs. Think of it as creating a little digital ruckus!
    * **Command (Simulating failed SSH login attempts):** `ssh fakeuser@localhost` (I ran this a few times to generate some "failed password" entries!)
    * **Command (Sudo usage):** `sudo whoami` (Simple, but effective for log generation)
    * **Command (Running a small Nmap scan):** `nmap -sS -p 1-100 127.0.0.1` (This generates network-related logs, if your forwarder is set up to capture them!)

* **Screenshot:** Show those commands in action! This screenshot should capture your **Kali terminal** showing the execution of several commands designed to generate security-relevant logs. You might see the commands being typed, and their immediate output, signifying activity on the system.
    ![Kali Linux Log Generation Commands](YOUR_SCREENSHOT_URL_HERE)

#### 4.2. **Verifying Data Ingestion in Splunk (The Payoff!)**

* **My Action:** After generating logs on Kali, I immediately jumped back to the Splunk Enterprise web interface. I went to the **Search & Reporting** app and searched for `index=main` or `source="/var/log/syslog"` to confirm that logs from my Kali machine were indeed pouring in. It's such a satisfying feeling to see them!

* **Screenshot:** This is the proof! Display the **Splunk Search & Reporting interface** with your search query (e.g., `index=main host=<kali_hostname>`). The screenshot should clearly show the resulting raw events or a filtered list of events specifically originating from your Kali machine, demonstrating successful log ingestion. Highlight those Kali logs!
    ![Splunk Search and Reporting - Raw Events from Kali](YOUR_SCREENSHOT_URL_HERE)

### 5. 🕵️ **Threat Detection & Analysis with SPL: Becoming a Cyber Sleuth!**

This phase focuses on using Splunk's Search Processing Language (SPL) to analyze the ingested logs and identify potential security threats or anomalies.

#### 5.1. **Basic Log Search and Filtering**

* **My Action:** I started with the fundamentals: practicing basic SPL queries to filter logs by `sourcetype`, `host`, or specific keywords. Gotta learn to walk before you can run, right?
    * **Example SPL:** `index=main sourcetype=syslog host=<kali_hostname>` (Just grabbing all syslog events from Kali)
    * **Example SPL:** `index=main "failed password"` (Quickly finding all failed login attempts)

* **Screenshot:** This screenshot should show the **Splunk Search interface** with a basic SPL query in the search bar (e.g., `index=main sourcetype=syslog`) and the corresponding search results below, demonstrating the ability to filter and view specific log data.
    ![Splunk Search - Basic Log Filtering](YOUR_SCREENSHOT_URL_HERE)

#### 5.2. **Detecting Brute-Force Attempts**

* **My Action:** This is a classic! I used SPL to look for multiple failed login attempts coming from the same source within a short time. This is a common indicator of a brute-force attack.
    * **Example SPL:** `index=main "failed password" | stats count by src_ip | where count > 5` (This query counts failed passwords by source IP and then filters for IPs with more than 5 attempts.)

* **Screenshot:** Show your brute-force detection query and its results! This screenshot should display the **Splunk Search interface** with the SPL query for detecting brute-force attempts in the search bar. The results should show a statistical table or a visualization (like a bar chart) highlighting source IPs with a high count of failed logins.
    ![Splunk Search - Brute-Force Detection](YOUR_SCREENSHOT_URL_HERE)

#### 5.3. **Identifying Port Scans**

* **My Action:** Another common threat: port scanning. If I had network logs properly captured and forwarded (which is a bit more advanced but totally doable!), I'd use SPL to spot patterns indicative of port scanning. Even with system logs, you can sometimes see remnants.
    * **Example SPL (requires network logs like Zeek or other firewall/IDS logs):** `index=main sourcetype=zeek_conn | stats distinct_count(dest_port) by src_ip | where distinct_count(dest_port) > 10` (This looks for source IPs that have tried to connect to many different destination ports.)

* **Screenshot:** This screenshot should show the **Splunk Search interface** with an SPL query designed to identify port scanning activity (or a similar network-related anomaly) in the search bar. The results should ideally display a table or visualization that helps confirm the suspicious activity.
    ![Splunk Search - Port Scan Identification](YOUR_SCREENSHOT_URL_HERE)

#### 5.4. **Creating Alerts or Dashboards (Optional but Cool!)**

* **My Action:** If I had more time, I'd totally build out some alerts or dashboards. Alerts would notify me immediately of a potential threat, and dashboards would give me a sweet visual overview of my lab's security posture. This is where Splunk really shines for continuous monitoring!

* **Screenshot:** If you tried this, show it! This screenshot should capture either the **configuration page for a Splunk Alert** (showing the trigger conditions and actions) based on one of your threat detection queries, or a **simple Splunk Dashboard** displaying relevant security metrics or visualizations you've created (e.g., log counts over time, top source IPs for failed logins).
    ![Splunk Alert Configuration or Basic Dashboard](YOUR_SCREENSHOT_URL_HERE)

### 6. 📝 **My Conclusion & What I Learned (Lessons from the Lab!)**

Wrapping up this project, it's cool to reflect on what I achieved and what hitches I ran into. Every challenge was a learning opportunity!

#### 6.1. **My Project Outcomes**

* **Successfully built a virtual cybersecurity lab:** This was a huge win, with Splunk Enterprise and a Universal Forwarder happily talking to each other.
* **Demonstrated end-to-end log collection:** I got logs flowing from my Kali machine right into my SIEM – super satisfying!
* **Applied SPL for basic log analysis and threat detection:** I got my hands dirty with searches and even some basic threat hunting.

* **Screenshot:** Let's end with a visual summary! This concluding screenshot could be an **overview of the Splunk Apps page** (showing the various installed apps), or even a **final custom dashboard** you've made that sums up the data and insights gained from your lab, providing a sense of completion.
    ![Splunk App Overview or Final Lab Dashboard](YOUR_SCREENSHOT_URL_HERE)

#### 6.2. **Challenges I Ran Into (And How I Overcame Them!)**

No project is without its bumps, and this lab was no exception!
* **Network configuration between VMs:** Getting NAT, Host-Only, and Internal networks to play nice always takes a bit of head-scratching, but it's essential for a secure lab.
* **Firewall rules:** Sometimes you forget a port, and things just won't connect! Double-checking UFW on Ubuntu and Kali was key.
* **Forwarder config (`outputs.conf` and `inputs.conf`):** Tiny typos here can cause big headaches. Meticulous checking was my friend.
* **Understanding and debugging SPL queries:** This is a whole language in itself! There was a lot of trial and error, but that's how you learn.

#### 6.3. **My Key Takeaways and Lessons Learned**

This lab was packed with learning! Here are some of my biggest takeaways:

* **Centralized Logging is a Game Changer:** Seriously, having all your logs in one place (thanks, Splunk!) makes spotting threats so much easier. It's the core of effective security monitoring.
* **Threat Hunting Basics are Crucial:** Getting hands-on with searching for indicators of compromise (IOCs) and weird behavior using SPL is invaluable. It's not just theory anymore!
* **Data Normalization Makes Sense:** Seeing how different `sourcetypes` and fields help structure the data for analysis really clicked during this project.
* **Lab Environments are Gold:** Building and experimenting in a controlled environment like this is absolutely the best way to learn and develop skills without risking production systems.
