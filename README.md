## 🛡️ SOC Home Lab Journey – Splunk SIEM

## 📌 Overview

This project demonstrates a hands-on SOC (Security Operations Center) lab built using Splunk SIEM.
It focuses on detecting real-world attack techniques through log analysis, detection engineering, and alerting.

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

| Lab                                                                | Description                                            |
| ------------------------------------------------------------------ | ------------------------------------------------------ |
| [Brute Force Detection](#)                                         | Detect multiple failed login attempts (Event ID 4625)  |
| [Privilege Escalation Detection](#)                                | Detect admin privilege assignment (Event ID 4672)      |
| [Lateral Movement (SMB)](#)                                        | Detect network logins and SMB activity                 |
| [Persistence – Scheduled Tasks](./persistence/schtasks-detection/) | Detect persistence via schtasks (Event ID 4688 & 4698) |

---

## 🔍 Detection Use Cases

### 🔹 Brute Force Detection

* Event ID: 4625
* Detects multiple failed login attempts

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

## 📈 Future Improvements

* Phishing / Email log analysis
* Advanced MITRE ATT&CK mapping
* Enhanced dashboards

---

## 🎯 Career Goal

I am building hands-on SOC skills through real-world simulations and detection engineering.
My goal is to become a SOC Analyst and contribute to security monitoring and incident detection.

---

---
