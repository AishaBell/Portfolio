From Logs to Alerts: Building an SSH Brute-Force Detection System with Splunk <br>
<br>
Project Type: Brute Force Attack · SOC Fundamentals <br>
Tools: Kali, Hydra, Splunk, Splunk Forwarder <br>
Date: January 18, 2026 <br>

Analyst: Aisha B. Bello <br>

Confidentiality Notice:<br>

This project is a simulation of a Brute Force Attack on Virtual Machine to achieve a real-world SOC investigation scenario. All precautions were taken to execute this project and findings are based on controlled lab data and used strictly for educational and portfolio purposes. <br>

<br>
Project Overview <br>
<br>
This project demonstrates the end‑to‑end deployment of a Security Information and Event Management (SIEM) solution using Splunk Enterprise to detect SSH brute‑force attacks in a Linux environment. The lab covers the installation and configuration of Splunk Enterprise and the Splunk Universal Forwarder, forwarding authentication logs from a Kali Linux system, simulating brute‑force login attempts using Hydra, and creating a real‑time alert to identify malicious behavior. Mitigation techniques were applied using Fail2Ban, firewall rules, and SSH hardening. <br>

The objective is to replicate a real SOC workflow: log ingestion → detection → alerting → response → verification. <br>

Tools and Requirements <br>

Software Tools <br>

Splunk Enterprise — SIEM platform for log ingestion, search, correlation, and alerting. <br>
Splunk Universal Forwarder — Forwards authentication logs to Splunk Enterprise. <br>
Kali Linux — Acts as both the victim system and attack simulation environment. <br>
Hydra — Used to simulate SSH brute‑force attacks. <br>
Rsyslog — Generates and manages authentication logs (auth.log). <br>
OpenSSH Server — Provides the SSH service. <br>

System Requirements <br>

Virtualization platform (VMware or VirtualBox) <br>
At least 2 GB RAM allocated to each VM <br>
Open TCP ports: <br>
8000 — Splunk Web Interface <br>
9997 — Splunk receiving port <br>
22 / custom SSH port — SSH service <br>

<br>
STEP 1: Installation of Splunk Enterprise on Kali <br>

1. Using the Kali browser, navigate to www.splunk.com, log in, and download Splunk Enterprise for Linux (.deb). <br>
2. Open a terminal and navigate to the Downloads directory: <br>
 
            cd Downloads 
            ls
3. Install Splunk: Run the script <br>

            sudo dpkg -i splunk-10.0.0-e8eb0c4654f8-linux-amd64.deb
4. Change to the Splunk binary directory: <br>

            cd /opt/splunk/bin
5. Start Splunk: <br>

            sudo ./splunk start
6. Accept the license agreement when prompted and create Username and password <br>

7. Copy the displayed IP address and port (default 8000). Login with credentials created during startup and Confirm that the Splunk Enterprise Dashboard loads successfully <br>

            http://127.0.0.1:8000

STEP 2: Installion and Configuration of Splunk Universal Forwarder <br>

Splunk Universal Forwarder is installed and configureed to send Linux authentication logs to Splunk instance. <br>

Log in to splunk.com and download the Splunk Universal Forwarder (.deb) or copy the wget link into Kali. <br>
Verify the downloaded file size (30–50 MB): <br>

            ls -lh splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.deb
3. Install the forwarder: <br>

            sudo dpkg -i splunkforwarder-10.0.2-e2d18b4767e9-linux-amd64.deb
4. Start the forwarder and accept the license and create Username and password <br>

            sudo /opt/splunkforwarder/bin/splunk start --accept-license
5. Point the forwarder to the Splunk server: The IP required in the stage is the IP address of the Victim machine. <br>

            sudo /opt/splunkforwarder/bin/splunk add forward-server 192.168.123.20:9997
6. Add monitoring for authentication logs: This command instructs the Splunk Universal Forwarder to monitor the system’s authentication log file in real time and store them in /var/log/auth.log <br>

            sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/auth.log