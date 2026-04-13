
# 🔍 Detection: Suspicious Login After Multiple Failed Attempts

## 📌 Description

This detection identifies accounts that experience multiple failed login attempts (EventCode 4625) followed by successful authentication (EventCode 4624).

This behavior may indicate:

* Brute force attack success
* Credential compromise

---

## 🧪 Lab Setup

* Splunk Enterprise (Ubuntu)
* Universal Forwarder (Windows)
* Windows Event Logs ingested (Security logs)

---

## 🔎 SPL Query

```spl
index=main (EventCode=4624 OR EventCode=4625)
| stats count(eval(EventCode=4625)) as failed 
       count(eval(EventCode=4624)) as success 
       by Account_Name Source_Network_Address
| where failed > 5 AND success > 0
```

---

## 📊 Findings

| Account          | Source IP | Failed Attempts | Successful Logins |
| ---------------- | --------- | --------------- | ----------------- |
| soc101           | 127.0.0.1 | 10              | 8                 |
| DESKTOP-TS6Q8M2$ | 127.0.0.1 | 10              | 8                 |

---

## 🧠 Analysis

* Multiple failed attempts indicate brute force behavior
* Successful login confirms access was eventually gained
* Source IP is localhost (lab simulation)

---

## 🎯 MITRE ATT&CK

* T1110 — Brute Force

---

## 🚨 Conclusion

This activity is suspicious and may indicate:

* Account compromise
* Weak password policy
* Automated attack tools

---

## 🔧 Recommendations

* Enforce account lockout policies
* Enable MFA
* Monitor repeated login failures
* Alert on this detection in real environments
