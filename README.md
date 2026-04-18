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

### My Goal
I am passionate about cybersecurity and continuously learning to become a SOC Analyst.
## 📈 Future Improvements

* Reduce false positives
* Add detections for PowerShell abuse and persistence
* Map detections to MITRE ATT&CK framework
* Build dashboards for visualization

---
