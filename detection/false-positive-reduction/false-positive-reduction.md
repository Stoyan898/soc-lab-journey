
# 🔧 False Positive Reduction – Splunk Detection Tuning

## 🎯 Objective
Improve an existing detection by reducing false positives and increasing accuracy.

---

## 🧠 Problem

The initial detection triggered alerts for legitimate activity such as:
- Administrator logins
- User typing mistakes
- System/service accounts

This created unnecessary noise and reduced detection reliability.

---

## 🔍 Step 1 – Investigating False Positives

I analyzed user activity using Splunk:

```spl
index=* (EventCode=4625 OR EventCode=4672)
| eval user=Account_Name
| stats count(eval(EventCode=4625)) as failed_logins 
        count(eval(EventCode=4672)) as privilege_events 
        values(host) as hosts
        by user
| sort -failed_logins
🔎 Findings:
High activity from system accounts (e.g., SYSTEM, LOCAL_SERVICE)
Normal user behavior generating alerts

🔧 Step 2 – Detection Tuning

I improved the detection by:

Excluding known safe users
Adding time-based correlation
Increasing thresholds
index=* (EventCode=4625 OR EventCode=4672)
| eval user=Account_Name
| search NOT user IN ("Administrator","yourusername")
| stats 
    count(eval(EventCode=4625)) as failed_logins 
    count(eval(EventCode=4672)) as privilege_events 
    min(_time) as first_seen 
    max(_time) as last_seen 
    by user, host
| eval time_diff = last_seen - first_seen
| where failed_logins >= 3 AND privilege_events >= 1 AND time_diff <= 86400

✅ Result
Reduced false positives significantly
Focused only on suspicious behavior
Improved signal-to-noise ratio
🧠 Key Learning

Detection engineering is not just about creating alerts —
it’s about tuning them to reflect real-world behavior.

🛡️ MITRE ATT&CK Mapping
T1110 – Brute Force
T1078 – Valid Accounts
