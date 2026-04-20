
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
