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
<img width="1538" height="990" alt="Image 2026-04-02 at 14 55" src="https://github.com/user-attachments/assets/99a62923-969c-4939-9751-3470df29ef3d" />



## 🔍 Detection Phase (Splunk)
Detected multiple failed login attempts using the following SPL:
index=main EventCode=4625 | stats count by src_ip, TargetUserName
<img width="3390" height="1900" alt="Image 2026-04-02 at 15 01" src="https://github.com/user-attachments/assets/130b4401-2f46-42e9-83da-e9af777860e2" />
<img width="1606" height="1708" alt="Image 2026-04-02 at 15 03" src="https://github.com/user-attachments/assets/63ff71cb-bb5f-4a66-8f86-c71cf103c96f" />
<img width="3360" height="724" alt="Image 2026-04-02 at 15 07" src="https://github.com/user-attachments/assets/41fec5bb-6e37-4610-a819-8835f7aa7843" />
<img width="3394" height="888" alt="Image 2026-04-02 at 15 04" src="https://github.com/user-attachments/assets/dc22eb08-f81d-4305-986f-a4d88c37a3e9" />
<img width="3376" height="892" alt="Image 2026-04-02 at 15 05" src="https://github.com/user-attachments/assets/9d4707bf-9537-4e88-a1a3-3b65a8c63700" />
