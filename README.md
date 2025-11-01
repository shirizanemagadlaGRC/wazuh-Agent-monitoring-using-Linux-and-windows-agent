Wazuh Deployment Guide

Overview
This repository provides a step-by-step guide for deploying Wazuh, an open-source security monitoring platform, on various endpoints. It covers:
Installing the Wazuh Server on a Virtual Machine (OVA format or Ubuntu VM).
Deploying Wazuh agents on Linux endpoints.
Deploying Wazuh agents on Windows endpoints.
Implementing File Integrity Monitoring (FIM) as a detective control.
Verifying risk monitoring and control effectiveness via the Wazuh dashboard.
Whether you're a beginner or experienced IT professional, this guide simplifies the process of setting up Wazuh for endpoint monitoring and demonstrates how technical controls support GRC (Governance, Risk, and Compliance) objectives.
Features
Centralized Security Monitoring: Set up Wazuh to monitor endpoints in real-time and provide a centralized audit trail.
Multi-Platform Support: Deploy Wazuh agents on both Linux and Windows systems.
Scalability and Customization: Modify configurations to meet your infrastructure’s requirements.
GRC Integration: Demonstrate risk monitoring, control effectiveness, and compliance reporting.
Table of Contents
Prerequisites
Step 1: Installing Wazuh Server
Step 2: Deploying Wazuh Agent on Linux
Step 3: Deploying Wazuh Agent on Windows
Step 4: Implementing File Integrity Monitoring
Step 5: Risk Monitoring & Control Verification
Troubleshooting
References
Contributing
Prerequisites
A host system capable of running a 64-bit virtual machine.
Hardware virtualization enabled in your host’s BIOS/UEFI settings.
Virtualization platform installed, such as VirtualBox or VMware Workstation.
Ubuntu Server 20.04+ installed in VirtualBox (with bridged networking enabled).
Internet access on the Ubuntu VM.
Administrative access on your Windows host machine.
Network connectivity between Wazuh server and endpoint systems.
Step 1: Installing Wazuh Server
Follow these steps to set up a Wazuh server using the pre-built OVA or Ubuntu VM:
Summary:
Download the Wazuh OVA (v4.9.2) or use the installation script on Ubuntu.
Import the OVA into your virtualization platform, or run the install script:
bash


curl -sO https://packages.wazuh.com/4.12/wazuh-install.sh && sudo bash ./wazuh-install.sh -a -i
Start the Wazuh server and access the dashboard through the web interface at https://<UBUNTU_VM_IP_ADDRESS>.
Log in using the credentials provided at the end of the installation script (default username: admin).
Step 2: Deploying Wazuh Agent on Linux
Summary:
Add the Wazuh repository and install the agent package.
Configure the agent to communicate with the Wazuh Manager.
Start and enable the Wazuh agent service.
Step 3: Deploying Wazuh Agent on Windows
Summary:
Download the Windows agent installer:
Wazuh Agent MSI
Install the agent using either the CLI or GUI method.
Register the agent with the manager using the agent key.
Start the Wazuh agent service and verify the connection to the Wazuh Manager.
Step 4: Implementing File Integrity Monitoring
Summary:
Edit the agent configuration (ossec.conf) to monitor a sensitive folder (e.g., C:\Users\<YourName>\SensitiveFiles).
Add the following line in the <syscheck> section:
xml


<directories realtime="yes">C:\Users\<YourName>\SensitiveFiles</directories>
Restart the agent to apply changes.
Step 5: Risk Monitoring & Control Verification
Summary:
Create and modify files in the monitored folder to simulate unauthorized activity.
Use the Wazuh dashboard to view File Integrity Monitoring alerts.
Filter for rule.groups: "syscheck" to see relevant events.
Analyze alerts for file path, action (added/modified/deleted), timestamp, and checksums.
Troubleshooting
Ensure the Wazuh Manager IP address is correctly configured in the agent setup.
Check network connectivity between endpoints and the Wazuh server.
Review agent logs for errors:
Linux: /var/ossec/logs/ossec.log
Windows: C:\Program Files (x86)\ossec-agent\ossec.log
References
Wazuh Documentation
Wazuh GitHub Repository
Wazuh Community Forum
Contributing
Contributions are welcome! If you have suggestions or find issues, please submit a pull request or open an issue.
GRC Workshop & Analysis Questions:
(Include these in your /exercises/grc-analysis-questions.md for learners to reflect on risk, control effectiveness, and compliance.)
