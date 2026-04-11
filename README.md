# 🔐 Splunk SIEM Lab – Brute Force Detection

## 📌 Overview
This project demonstrates a SIEM lab built using Splunk to monitor Windows logs and detect brute force login attempts.

---

## 🏗️ Lab Setup

- Windows 11 (Log Source)
- Splunk Universal Forwarder
- Splunk Enterprise (Ubuntu)

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
