# 🛡️ SOC Home Lab Journey – Splunk SIEM

🚀 Aspiring SOC Analyst building hands-on detection skills using real-world attack simulations and Splunk SIEM.

## 🎯 What This Project Demonstrates

This project simulates real SOC analyst responsibilities:

- Log ingestion and normalization (Splunk SIEM)
- Detection engineering using SPL
- Correlation of security events across attack stages
- Alert creation and tuning
- Investigation of suspicious activity
- Mapping detections to MITRE ATT&CK

The goal is to replicate how a SOC analyst detects, investigates, and responds to threats in a real environment.

🔍 Focus areas:
* Threat detection & log analysis
* Detection engineering (Splunk SPL)
* MITRE ATT&CK mapping
* Attack simulation & validation

---

## 🧰 Technologies Used

* Splunk Enterprise (SIEM)
* Splunk Universal Forwarder
* Windows Event Logs
* Ubuntu (SIEM Server)

---

## 🏗️ Lab Architecture

* Windows VM → Generates security logs
* Splunk Universal Forwarder → Forwards logs
* Ubuntu Server → Hosts Splunk Enterprise

---
## 🧪 SOC Lab Projects

| Lab                                                                | Skills Demonstrated                                    |
| ------------------------------------------------------------------ | ------------------------------------------------------ |
| [Brute Force Detection](./detection/suspicious-login-after-bruteforce/)                     | Log analysis, detection logic, alerting                |
| [Privilege Escalation](./detection/privilege-escalation/)          | Event correlation, admin activity detection            |
| [Lateral Movement (SMB)](lateral-movement/)                        | Network log analysis, authentication patterns          |
| [Persistence – Scheduled Tasks](persistence/schtask-detection/) | Process monitoring, persistence detection              |
| [Phishing / Email Analysis](./detection/phishing/)  | Email threat detection, SPL queries, correlation logic |

---

## 🔍 Detection Use Cases

### 🔹 Brute Force Detection

* Event ID: 4625
* Detects potential brute-force attacks by identifying multiple failed login attempts within a short time window, which may indicate credential guessing activity.

### 🔹 Privilege Escalation Detection

* Event ID: 4672
* Identifies admin-level logins

### 🔹 Process Monitoring

* Event ID: 4688
* Tracks process creation (PowerShell, cmd, etc.)

---

## 🚨 Alerting

Alerts were configured using scheduled searches in Splunk:

* Schedule: Every 5 minutes (`*/5 * * * *`)
* Time range: Last 5 minutes
* Trigger condition: Results > 0

---

## 🔐 Attack Chain Detection

### Scenario

Brute Force → Privilege Escalation

### Key Skills Demonstrated

* Event correlation (4625 → 4672)
* SPL detection logic
* Alert creation
* SOC investigation workflow

### MITRE ATT&CK Mapping

* T1110 – Brute Force
* T1078 – Valid Accounts
* T1068 – Privilege Escalation

---

## 🔄 Latest Progress: Lateral Movement (SMB)

### What I Did

* Simulated SMB authentication from Ubuntu to Windows
* Generated Event IDs 4624 & 4625
* Built detections and alerts

### Key Finding

* Logon Type 3 = Network login (SMB)

### MITRE ATT&CK

* T1021.002 – SMB
* T1110 – Brute Force
* T1078 – Valid Accounts

---

## 🔐 Persistence Detection – Scheduled Tasks

### What I Did

* Simulated scheduled task creation using `schtasks`
* Detected execution via Event ID 4688
* Detected task creation via Event ID 4698

### Key Learning

* Importance of command-line logging
* Difference between process execution vs persistence detection

📁 Full Lab:
👉 [View Detailed Lab](./persistence/schtasks-detection/README.md)

---

## 🧠 SOC Workflow Demonstrated

1. Log ingestion
2. Detection engineering
3. Event correlation
4. Alert creation
5. Visualization
6. Attack simulation

---

## 🔧 False Positive Reduction

* Filtering known users
* Applying thresholds
* Time-based correlation

📂 Details:
👉 [False Positive Reduction](detections/false-positive-reduction.md)

---

📧 Phishing / Email Log Analysis
🧪 What I Did
Ingested simulated email logs into Splunk
Extracted structured fields (sender, subject, URL, attachment)
Built detection queries for phishing scenarios
Created alert for suspicious email activity
🔍 Detection Capabilities
Typosquatting domain detection (micr0soft, paypa1)
Suspicious URL detection (login pages, IP-based links)
Malicious attachment detection (.exe)
Social engineering detection (urgent/financial language)
Correlation of multiple phishing indicators
🧩 MITRE ATT&CK
T1566 – Phishing
T1566.001 – Attachment
T1566.002 – Link
T1071 – Web traffic

## 🧠 Key Skills Developed

- Investigating Windows Security logs (4625, 4672, 4688, 4698)
- Writing Splunk SPL queries for detection use cases
- Correlating multi-stage attacks (brute force → privilege escalation)
- Building alerts based on real attack behavior
- Troubleshooting log ingestion and visibility gaps-

## 🧠 Analyst Mindset

Throughout this lab, I focused not only on detection but also on understanding attacker behavior:

- Identifying patterns instead of single events
- Correlating logs across multiple sources
- Investigating suspicious activity step-by-step
- Reducing false positives

This reflects how real SOC analysts operate in production environments.

## 🚀 Key Highlights

- Built multiple real-world detection use cases (Brute Force, Privilege Escalation, Persistence, Phishing)
- Implemented correlation logic across attack stages
- Created alerts simulating real SOC monitoring workflows
- Simulated attacker techniques in a controlled lab environment
- Applied MITRE ATT&CK mapping to all detections

## 🚨 Incident Investigation – User Compromise

### 🎯 Scenario

Simulated a real-world attack where a user account was compromised after receiving a phishing email.

### 🔗 Attack Chain

Phishing → Credential Access → Execution → Persistence

### 🔍 What I Did

* Identified phishing email indicators from email logs
* Investigated suspicious login activity (Event ID 4624)
* Detected brute-force pattern (4625 → 4624)
* Analyzed process execution (Event ID 4688)
* Confirmed persistence via scheduled task (Event ID 4698)

### 🧠 Skills Demonstrated

* Incident investigation
* Event correlation
* Threat hunting
* Detection engineering

📁 **Full Lab:**
👉 [View Incident Investigation Lab](./detection/incident-response-user-compromise/)

## 🧠 Analyst Mindset

Throughout this project, I focused on thinking like a SOC analyst:

* Investigating alerts instead of just generating them
* Correlating multiple events into attack chains
* Identifying patterns of attacker behavior
* Adapting detection logic based on log limitations

This approach reflects real-world SOC operations where context and investigation are critical.

## 🎯 Career Goal

I am actively developing hands-on SOC Analyst skills through real-world attack simulations and detection engineering.I am seeking an entry-level SOC Analyst role where I can contribute to threat detection, log analysis, and incident investigation while continuing to grow in cybersecurity.


  
