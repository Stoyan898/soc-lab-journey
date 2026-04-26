🛡️ Incident Investigation – User Compromise
🎯 Scenario

Simulated a phishing-based compromise leading to unauthorized access and persistence.

🔗 Attack Chain

Phishing → Credential Access → Execution → Persistence

🔍 Investigation Steps
1. Phishing Email Detection

Detected suspicious email with phishing indicators.

2. Suspicious Login Activity

Identified network logons (Event ID 4624 – Logon Type 3).

3. Brute Force Pattern

Multiple failed logins followed by success (4625 → 4624).

4. Suspicious Process Execution

Detected PowerShell/cmd usage (Event ID 4688).

5. Persistence Mechanism

Scheduled task creation detected (Event ID 4698).

🧩 MITRE ATT&CK Mapping
T1566 – Phishing
T1110 – Brute Force
T1078 – Valid Accounts
T1059 – Command Execution
T1053 – Scheduled Task
🧠 Key Learning
Incident investigation requires correlating multiple events
Single alerts are not enough — patterns matter
Detection improves when combining logs from multiple sources
✅ Outcome

Successfully simulated and investigated a full attack chain from phishing to persistence using Splunk SIEM.
