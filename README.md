# 🛡️ Wazuh SIEM Home Lab – End-to-End Security Monitoring

A complete **SIEM Home Lab implementation using Wazuh**, demonstrating centralized security monitoring, log collection, file integrity monitoring (FIM), and cross-platform agent deployment on **Windows, Linux, and macOS** systems.

This project simulates a **real-world SOC environment** and showcases hands-on blue team skills such as endpoint monitoring, alert analysis, and SIEM configuration.

---

## 📌 Project Objectives

- Install and configure **Wazuh Manager**
- Deploy **Wazuh Agents** on:
  - Windows
  - Linux
  - macOS
- Monitor a **specific directory/path** using File Integrity Monitoring
- Generate and analyze security alerts
- Visualize events using the **Wazuh Dashboard**

---

## 🧰 Tools & Technologies

- **Wazuh SIEM**
- Elastic Stack / OpenSearch
- Ubuntu Server (Wazuh Manager)
- Windows 10 / 11
- Linux (Ubuntu / Kali)
- macOS
- VirtualBox / VMware
- SSH, PowerShell, Terminal

---

## 🏗️ Lab Architecture

[ Windows Agent ] ─┐
[ Linux Agent ] ─┼──▶ [ Wazuh Manager + Dashboard ]
[ macOS Agent ] ─┘


---

## 🚀 Wazuh Manager Installation (Ubuntu)

```bash
curl -sO https://packages.wazuh.com/4.7/wazuh-install.sh
sudo bash wazuh-install.sh -a
```
After installation, access the dashboard:
```bash
https://<WAZUH_MANAGER_IP>
```
🖥️ Agent Installation & Configuration
🔹 Linux Agent
```bash
curl -sO https://packages.wazuh.com/4.x/wazuh-agent.sh
sudo bash wazuh-agent.sh
```
Start agent service:
```bash
sudo systemctl enable wazuh-agent
sudo systemctl start wazuh-agent
```
🔹 Windows Agent
Download Wazuh Agent for Windows

Install and configure:

Manager IP

Agent Name

Start the agent service:

Services → Wazuh Agent → Start
🔹 macOS Agent
```bash
curl -so wazuh-agent.pkg https://packages.wazuh.com/4.x/macos/wazuh-agent-4.x.pkg
sudo installer -pkg wazuh-agent.pkg -target /
```
Start agent:
```bash
sudo /Library/Ossec/bin/wazuh-control start
```
📂 File Integrity Monitoring (Monitoring a Specific Path)
🔹 Linux Example (/var/www/html)
Edit agent configuration:
```bash
sudo nano /var/ossec/etc/ossec.conf
```
```bash
<syscheck>
  <directories check_all="yes" realtime="yes">/var/www/html</directories>
</syscheck>
```
Restart agent:
```bash
sudo systemctl restart wazuh-agent
```
🔹 Windows Example (C:\SensitiveData)
```bash
<syscheck>
  <directories check_all="yes" realtime="yes">C:\SensitiveData</directories>
</syscheck>
```
🔹 macOS Example (/Users/emmanuel/Documents)
```bash
<syscheck>
  <directories check_all="yes" realtime="yes">/Users/emmanuel/Documents</directories>
</syscheck>
```
🔔 Alert Testing
Trigger alerts by creating or modifying files:

touch testfile.txt
echo "unauthorized change" >> testfile.txt
Alerts generated:

File creation

File modification

File deletion

All alerts are visible in the Wazuh Dashboard.

📊 Use Cases Demonstrated
File integrity monitoring

Unauthorized change detection

Endpoint visibility

Log correlation

Compliance monitoring (CIS, PCI DSS)

SOC alert analysis

📁 Project Structure
wazuh-siem-homelab/
└── README.md
🧠 Skills Demonstrated
SIEM deployment & configuration

Blue Team / SOC operations

Endpoint security monitoring

Log analysis & alert investigation

Cross-platform security integration

🚀 Future Enhancements
Custom Wazuh detection rules

Active response automation

Malware detection integration

Log ingestion from web servers

Attack simulation (Atomic Red Team)

