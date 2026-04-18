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

## 🔎 Analysis

This pattern indicates a possible brute-force attack followed by account compromise.

Multiple failed login attempts suggest password guessing, while the subsequent privilege escalation indicates potential attacker success.

This detection helps identify early-stage compromise before lateral movement.

## 🧠 Real-World Relevance

This detection simulates a real SOC scenario where attackers attempt to gain access through brute force and escalate privileges.

Such patterns are commonly monitored in enterprise environments.
