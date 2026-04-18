# 🛡️ SOC Lab – Attack Chain Detection (Splunk)

This project demonstrates a real-world SOC detection use case where a brute-force attack is followed by privilege escalation.

I built a correlation rule in Splunk to identify multi-stage attack behavior using Windows Security logs.

## 🔍 Detection Summary
- Event ID 4625 → Failed login attempts
- Event ID 4672 → Privileged access
- Correlation based on user and host
- Time-based detection logic applied

## 🎯 Outcome
Successfully detected a suspicious attack chain involving:
- Multiple failed logins
- Followed by privilege escalation
- Within a defined time window

## 🛡️ MITRE ATT&CK Mapping

- T1110 – Brute Force
- T1078 – Valid Accounts
- T1068 – Privilege Escalation
