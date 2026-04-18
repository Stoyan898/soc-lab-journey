# 🛡️ SOC Home Lab Journey – Splunk SIEM

## 📌 Overview

This repository documents my hands-on journey in building a Security Operations Center (SOC) home lab using Splunk.

The purpose of this lab is to simulate real-world SOC analyst responsibilities such as:

* Log ingestion and monitoring
* Detection engineering
* Alert creation and tuning
* Attack simulation and validation

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

* Event ID: 4672
* Detects when special privileges (admin rights) are assigned

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
## 🔐 Attack Chain Detection (Brute Force → Privilege Escalation)

In this project, I developed a correlation rule in Splunk to detect a potential attack chain involving:

- Multiple failed login attempts (Event ID 4625)
- Followed by privilege escalation (Event ID 4672)

### What I Did
- Collected and analyzed Windows Security logs
- Built a correlation detection using SPL
- Applied thresholds and time-based logic
- Created a dashboard for visualization
- Configured an alert for real-time detection

### Why I Did It
I wanted to understand how real SOC analysts detect multi-stage attacks rather than isolated events. This project helped me learn how to correlate logs and identify suspicious patterns.

### What I Learned
- Event correlation in SIEM
- Detection engineering basics
- MITRE ATT&CK mapping
- Alert creation and tuning

### My Motivation
I am passionate about cybersecurity and continuously learning. I enjoy building hands-on labs and improving my detection skills to prepare for a SOC Analyst role.

### MITRE ATT&CK
- T1110 – Brute Force
- T1078 – Valid Accounts
- T1068 – Privilege Escalation
## 📈 Future Improvements

* Reduce false positives
* Add detections for PowerShell abuse and persistence
* Map detections to MITRE ATT&CK framework
* Build dashboards for visualization

---
