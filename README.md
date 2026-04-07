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
---

## 🛡️ Project 2: Privilege Escalation & Persistence Detection

### 🎯 Objective
To simulate a post-exploitation scenario where an attacker creates a backdoor administrator account and to detect this activity using Splunk.

### 🛠️ Attack Steps (Kali Linux)
Once a reverse shell was established, the following commands were executed to maintain persistence:
1. **Create User:** `net user hacker_admin Password123 /add`
2. **Escalate Privileges:** `net localgroup administrators hacker_admin /add`

![Privilege Escalation Attack]<img width="635" height="450" alt="Screenshot 2026-04-07 at 13 38 30" src="https://github.com/user-attachments/assets/3e15996f-b39c-48fc-a094-3b3d9e19961e" /><img width="624" height="222" alt="Screenshot 2026-04-07 at 13 38 48" src="https://github.com/user-attachments/assets/92544cdb-b183-4239-9b97-a2e82ace34ac" />

<img width="633" height="277" alt="Screenshot 2026-04-07 at 13 50 52" src="https://github.com/user-attachments/assets/7800a5ed-ac0f-40ef-bcfc-c6ddee2cac5d" />


### 🔍 Detection in Splunk
I monitored the Windows Security event logs and identified the following critical Event IDs:
* **Event ID 4720:** A user account was created.
* **Event ID 4732:** A member was added to a security-enabled local group.

**SPL Query used:**
index=main (EventCode=4720 OR EventCode=4732)
| table _time, host, EventCode, TargetUserName, MemberName, SubjectUserName
<img width="932" height="930" alt="Screenshot 2026-04-07 at 13 53 11" src="https://github.com/user-attachments/assets/37549c8b-b055-4344-b0fc-58f47ad8b38b" />
<img width="681" height="714" alt="Screenshot 2026-04-07 at 13 57 45" src="https://github.com/user-attachments/assets/75c4e31c-8282-4a4d-b6b0-d4e6541f5b44" />

💡 SOC Analyst Takeaway

Detecting the creation of unauthorized local administrators is a critical task. In a production environment, this should trigger an High-Priority Alert to investigate the SubjectUserName (the account that performed the action) for potential compromise.












