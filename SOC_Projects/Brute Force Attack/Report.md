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
4. Change to the Splunk binary directory: