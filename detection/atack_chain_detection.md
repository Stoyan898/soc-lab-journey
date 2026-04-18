# Attack Chain Detection: Brute Force → Privilege Escalation

## Overview
This detection identifies suspicious behavior where multiple failed login attempts are followed by privilege escalation activity.

## Data Source
- Windows Security Logs (Splunk)
- Event ID 4625 – Failed login
- Event ID 4672 – Special privileges assigned

## Detection Logic
- Count failed login attempts per user
- Count privilege escalation events per user
- Calculate time difference between first and last event
- Trigger if:
  - Failed logins ≥ 3
  - Privilege events ≥ 1
  - Occurs within defined time window

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
