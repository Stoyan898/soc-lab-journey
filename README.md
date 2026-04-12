# 🔐 Splunk SIEM Lab – Brute Force Detection

## 📌 Overview
This project demonstrates a SIEM lab built using Splunk to monitor Windows logs and detect brute force login attempts.

---
🧱 Lab Architecture
Windows 11 (Log Source)
        ↓
Splunk Universal Forwarder
        ↓
Splunk Enterprise (Ubuntu)
        ↓
Search, Detection, Alerting

---

## 📊 Data Ingestion

![Data](images/03-index-main-data.png)

---

## 🔍 Detection Queries

### Successful Logins (4624)
![4624](images/04-eventcode-4624.png)

### Failed Logins (4625)
![4625](images/05-eventcode-4625.png)

---

## 📈 Analysis

### Table View
![Table](images/06-login-table.png)

### Brute Force Detection
![Stats](images/07-bruteforce-stats.png)

---

## 🚨 Alert Configuration

![Alert](images/08-bruteforce-alert.png)

---

## 🧠 MITRE ATT&CK Mapping

| Event | Technique | Description |
|------|----------|------------|
| 4624 | T1078 | Valid Accounts |
| 4625 | T1110 | Brute Force |

---

## 🚨 Detection Logic

## 🕵️ Investigation Scenario

A potential brute force attack was simulated using multiple failed login attempts.

Steps:
1. Observed spike in EventCode 4625
2. Identified repeated attempts on same account
3. Correlated activity by host and user
4. Created detection rule for threshold-based alerting

Conclusion:
Suspicious login activity consistent with brute force behavior.

Trigger: More than 5 failed login attempts (EventCode 4625)

Purpose:
Detect brute force attacks targeting user accounts.

How it works:
- Splunk counts failed login attempts per user and host
- If count exceeds threshold (>5), alert is triggered

Result:
The alert successfully detects suspicious login activity consistent with brute force attacks.

A brute force attack scenario was simulated using multiple failed login attempts.

Investigation steps:
1. Observed spike in EventCode 4625 (failed logins)
2. Identified repeated login attempts on same account
3. Checked associated host generating the activity
4. Correlated events using Splunk search queries
5. Created detection rule based on threshold

Conclusion:
This behavior indicates potential brute force attack activity.
