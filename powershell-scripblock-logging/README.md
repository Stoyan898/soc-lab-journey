# 🧪 Lab: PowerShell Script Block Logging Detection (Splunk)

## 🎯 Objective

Detect PowerShell activity using Script Block Logging (Event ID 4104) and visualize it in Splunk.

---

## 🧰 Tools Used

* Splunk Enterprise
* Splunk Universal Forwarder
* Windows 11 VM
* PowerShell Logging (GPO)

---

## 🏗️ Lab Setup

* Windows machine generates PowerShell logs
* Universal Forwarder sends logs to Splunk
* Splunk indexes and parses events

---

## 🔧 Configuration

### Enable PowerShell Logging (GPO)

* Module Logging
* Script Block Logging

### Splunk Forwarder

**inputs.conf**

```
[WinEventLog://Microsoft-Windows-PowerShell/Operational]
disabled = 0
index = main
```

**outputs.conf**

```
[tcpout]
defaultGroup = default-autolb-group

[tcpout:default-autolb-group]
server = 192.168.56.102:9997
```

---

## 🔍 Detection Query

```
index=* EventCode=4104
| rex field=_raw "Creating Scriptblock text.*?:\s*\r?\n(?<ScriptBlockText>.+)"
| table _time, host, ScriptBlockText
```

---

## 📊 Example Results

* `whoami`
* `ipconfig`
* `Invoke-Expression "whoami"`

---

## 🧠 Detection Logic

* Extract PowerShell commands from raw logs
* Identify suspicious or reconnaissance activity
* Normalize into readable fields

---

## 🎯 MITRE ATT&CK Mapping

* **T1059.001 – PowerShell**
* **TA0002 – Execution**
* **TA0007 – Discovery**

---

## 📸 Screenshots

### Splunk detection working

![Detection](screenshots/05-final-detection-working.png)

### Aggregated results

![Stats](screenshots/06-stats-view.png)

### Windows Event Viewer (4104)

![Event Viewer](screenshots/07-event-viewer-4104.png)

---

## 🚧 Challenges Faced

* Disk space issues blocking ingestion
* Forwarder connectivity errors (port 9997)
* Missing ScriptBlockText due to multiline logs
* Regex parsing issues

---

## ✅ Key Learnings

* Troubleshooting log ingestion pipelines
* Configuring Windows logging via GPO
* Writing regex for multiline log parsing
* Building practical detection queries in Splunk

---

## 🚀 Outcome

Successfully built a working detection for PowerShell execution using Script Block Logging and validated it in Splunk.

---
