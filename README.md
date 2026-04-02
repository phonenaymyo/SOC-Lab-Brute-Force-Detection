# SOC-Lab-Brute-Force-Detection
A project demonstrating SMB Brute Force attack simulation with Kali Linux (Hydra) and detection using Splunk SIEM.
# Windows Brute Force Attack Detection Lab (Splunk)

## 🎯 Objective
To simulate an SMB Brute Force attack on a Windows 11 machine and analyze the resulting logs in Splunk to demonstrate SOC Analyst detection skills.

## 🛠️ Tools Used
* **Target:** Windows 11 Home (with SMB enabled)
* **Attacker:** Kali Linux (M3 MacBook / VMware Fusion)
* **Security Monitoring:** Splunk Enterprise
* **Tool:** Hydra (v9.6)

## 🧨 Attack Phase
Using Hydra to attack the SMB protocol:
`hydra -l JOXOE -P pass.txt 192.168.87.128 smb -V -f`

![](Image2026-04-02at14.55.png)

## 🔍 Detection Phase (Splunk)
Detected multiple failed login attempts using the following SPL:
```spl
index=main EventCode=4625 | stats count by src_ip, TargetUserName
