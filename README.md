# 🛡️ SOC Home Lab Journey – Splunk SIEM

## 📌 Overview

- Overview of the lab
- Architecture (diagram)
- Use cases (brute force detection, failed logins)
- Sample queries (Splunk SPL)
- MITRE ATT&CK mapping
---

## 🧰 Technologies Used

* Splunk Enterprise (SIEM)
* Splunk Universal Forwarder
* Windows Event Logs
* Ubuntu (SIEM server)

---

## 🏗️ Lab Architecture

* Windows VM → Generates security logs
* Splunk Universal Forwarder → Collects and forwards logs
* Ubuntu Server → Hosts Splunk Enterprise (SIEM)

---

## 🔍 Detection Use Cases

### 🔹 Brute Force Detection

* Event ID: 4625
* Detects multiple failed login attempts

### 🔹 Privilege Escalation Detection

🔹 Privilege Escalation Detection
Simulated privileged access and detected Event ID 4672 in Splunk.
- Identified admin-level activity
- Built detection queries
- Created alert for privileged logins

### 🔹 Process Monitoring

* Event ID: 4688
* Tracks process creation (e.g., PowerShell, cmd execution)

---

## 🚨 Alerting

Alerts were configured using scheduled searches in Splunk:

* Cron schedule: `*/5 * * * *` (every 5 minutes)
* Time range: Last 5 minutes
* Trigger condition: Results > 0

This ensures near real-time detection of suspicious activity.

---

## 🧪 Attack Simulation

To validate detections, I simulated real-world attack behavior:

* Created a new user
* Added user to administrators group
* Executed commands to generate logs

This allowed me to verify that alerts were working correctly.

---

## 🧠 What I Learned

* How to configure log ingestion using Splunk Forwarder
* How to analyze Windows Event Logs (Security logs)
* How to build detection queries in Splunk
* How to create and validate alerts
* How to simulate attacker behavior in a lab environment
* How to troubleshoot log ingestion issues

---

## 🚀 My Motivation

I am passionate about cybersecurity and continuously improving my skills through hands-on practice.

I enjoy learning by building real-world labs and solving practical problems.
I am highly motivated, eager to learn, and committed to growing into a SOC Analyst role.

---
## 🔐 Attack Chain Detection

This project demonstrates a real SOC detection use case:

### Scenario
Brute Force → Privilege Escalation

### What I Did
- Analyzed Windows Security logs
- Correlated Event ID 4625 and 4672
- Built SPL detection logic
- Applied thresholds and time window
- Created dashboard and alert

### Why I Did It
I wanted to learn how SOC analysts detect multi-stage attacks instead of single events.

### What I Learned
- Correlation is key in detection
- Attack chains provide better insights
- Splunk SPL can be used for detection engineering

### MITRE ATT&CK
- T1110 – Brute Force
- T1078 – Valid Accounts
- T1068 – Privilege Escalation

  ## 🧠 SOC Workflow Demonstrated

1. Log ingestion from Windows machine
2. Detection engineering using Splunk SPL
3. Correlation of multiple events (4625 + 4672)
4. Alert creation and monitoring
5. Visualization using dashboards
6. Validation through attack simulation

## 🔧 False Positive Reduction

Improved detection accuracy by:
- Filtering known safe users
- Applying time-based correlation
- Increasing thresholds
📂 See full details: [false-positive-reduction.md](detections/false-positive-reduction.md)

### My Goal
I am passionate about cybersecurity and continuously learning to become a SOC Analyst.

## 🔄 Latest Progress: Lateral Movement Detection (SMB)

### 🧪 What I Did

- Created a shared folder on Windows using SMB
- Connected to it from Ubuntu using `smbclient`
- Generated authentication logs (Event ID 4624 & 4625)
- Verified connectivity between VMs (ping test)
- Built Splunk searches, dashboards, and alerts

---

### 🧠 Key Findings

- Logon Type **3** indicates **network-based logins (SMB)**
- Source IP (`Source_Network_Address`) shows where login originated
- Multiple failed logins followed by success may indicate **brute force**
- SMB activity is a common method for **lateral movement**

---
🚨 Alerts Created
Brute Force Detection
Privilege Escalation Detection
High SMB Activity (Possible Lateral Movement)
Successful Login After Multiple Failures
🧩 MITRE ATT&CK Mapping
T1021.002 – SMB/Windows Admin Shares
T1110 – Brute Force
T1078 – Valid Accounts
📈 What I Learned
How attackers move laterally using SMB
How to identify suspicious login patterns in logs
How to build detections using Splunk
How to turn raw logs into dashboards and alerts
⚠️ Issues I Faced
Authentication failures (NT_STATUS_LOGON_FAILURE)
Incorrect SMB username formatting
Understanding domain vs local user syntax
Troubleshooting connectivity between VMs
✅ Outcome

Successfully simulated lateral movement and built:

Detection queries
Dashboards
Alerts

This lab improved my understanding of real SOC monitoring scenarios.

## 📈 Future Improvements
* Add detections for PowerShell abuse and persistence
* Phishing / email log analysis (basic)
* Map detections to MITRE ATT&CK framework
* Build dashboards for visualization



---
