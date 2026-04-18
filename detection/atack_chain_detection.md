# 🚨 Attack Chain Detection: Brute Force → Privilege Escalation

## Overview
This detection identifies suspicious behavior where multiple failed login attempts are followed by privilege escalation.

---

## Data Sources
- Windows Security Logs
- Event ID 4625 → Failed Login
- Event ID 4672 → Privileged Access

---

## Detection Logic
- Group events by user and host
- Count failed logins
- Count privilege escalation events
- Calculate time difference between events

---

## SPL Query
```spl
index=* (EventCode=4625 OR EventCode=4672)
| eval user=Account_Name
| stats count(eval(EventCode=4625)) as failed_logins 
        count(eval(EventCode=4672)) as privilege_events 
        min(_time) as first_seen 
        max(_time) as last_seen 
        by user, host
| eval time_diff = last_seen - first_seen
| where failed_logins >= 3 AND privilege_events >= 1 AND time_diff <= 86400
