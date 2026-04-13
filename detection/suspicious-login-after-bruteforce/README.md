# 🔍 Detection: Suspicious Login After Multiple Failed Attempts

## 📌 Description

This detection identifies accounts with multiple failed login attempts followed by a successful login.

This behavior may indicate:

* Brute force attack success
* Credential compromise

---

## 🛠️ Lab Setup

* Splunk Enterprise (Ubuntu)
* Windows machine with Universal Forwarder
* Windows Security Event Logs

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

* Account: soc101
* Source IP: 127.0.0.1
* Failed attempts: 10
* Successful logins: 8

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

This activity is suspicious and may indicate account compromise.

---

## 🔧 Recommendations

* Implement account lockout policies
* Enable multi-factor authentication
* Monitor repeated login failures
