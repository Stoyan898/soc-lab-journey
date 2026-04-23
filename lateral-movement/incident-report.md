# 🚨 Incident Report: SMB Lateral Movement Simulation

## 📅 Date
April 2026

---

## 🧪 Scenario

Simulated lateral movement from an Ubuntu machine to a Windows 11 machine using SMB shares.

---

## 🎯 Objective

To detect suspicious authentication activity and identify lateral movement using Splunk.

---

## 🖥️ Environment

- Source: Ubuntu (192.168.1.10)
- Target: Windows 11 (192.168.1.3)
- SIEM: Splunk Enterprise

---

## 🔍 Detection Details

### Event IDs Used
- 4624 → Successful logon
- 4625 → Failed logon

### Key Indicator
- Logon Type 3 (Network logon via SMB)

---

## 📊 Observations

- Multiple authentication attempts detected from:
  - `192.168.1.10`
- Successful logins after failed attempts observed
- SMB share (`testshare`) accessed remotely

---

## 🧠 Analysis

This behavior is consistent with:
- Credential-based lateral movement
- Potential brute force followed by successful login

---

## 🧩 MITRE ATT&CK Mapping

- T1021.002 – SMB Lateral Movement
- T1110 – Brute Force
- T1078 – Valid Accounts

---

## 🚨 Alerts Triggered

- High SMB Activity
- Brute Force Detection
- Successful Login After Failures

---

## ⚠️ Challenges Faced

- Authentication errors (`NT_STATUS_LOGON_FAILURE`)
- Incorrect username format
- SMB connection troubleshooting

---

## ✅ Conclusion

The lab successfully demonstrated:
- Lateral movement via SMB
- Detection using Splunk queries
- Alerting and dashboard creation

---

## 🚀 Recommendation

Monitor:
- High volume of Logon Type 3 events
- Repeated failed logins
- Unusual source IP activity
