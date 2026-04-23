🔍 Lateral Movement Detection Lab
📌 Overview

This lab simulates lateral movement between two virtual machines:

Windows 11 (target)
Ubuntu (attacker)

Logs are collected and analyzed in Splunk to detect suspicious activity.

🧪 Lab Setup
VirtualBox NAT Network
Windows IP: 192.168.1.3
Ubuntu IP: 192.168.1.10
Splunk running on Ubuntu
⚙️ Techniques Simulated
SMB enumeration
Network logons (Logon Type 3)
Failed login attempts
Successful authentication after failures
🧠 MITRE ATT&CK Mapping
Technique	ID	Description
Lateral Movement via SMB	T1021.002	Remote services using SMB
Brute Force	T1110	Repeated login attempts
Valid Accounts	T1078	Successful login using credentials
📊 Splunk Detection Queries
SMB Lateral Movement
index=* EventCode=4624 Logon_Type=3
| stats count by Source_Network_Address
| where count > 3
Failed Logins
index=* EventCode=4625
| stats count by Account_Name
Success After Failures
index=* (EventCode=4624 OR EventCode=4625)
| stats count(eval(EventCode=4625)) as failures 
        count(eval(EventCode=4624)) as success 
        by Source_Network_Address
| where failures > 3 AND success > 0

🖥️ Commands Used
🔹 Ubuntu (Attacker)
smbclient -L //192.168.1.3 -U desktop-t56g8m2\\soc101

👉 Lists shared folders on the Windows machine

ping 192.168.1.3

👉 Checks connectivity to target

🔹 Windows (Target)
ipconfig

👉 Shows IP address

netstat -an | findstr 445

👉 Confirms SMB service is listening

net share testshare=C:\share /grant:Everyone,FULL

👉 Creates a shared folder

whoami

👉 Displays current logged-in user

🎯 Key Learnings
How lateral movement appears in logs
Difference between Logon Types (2, 3, 10)
How to detect brute force attempts
How to build alerts in Splunk
