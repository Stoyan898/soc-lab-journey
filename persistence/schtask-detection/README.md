
# Persistence Detection - Scheduled Tasks (schtasks)

## 🎯 Objective
Detect persistence activity using scheduled tasks (`schtasks.exe`) in Splunk.

---

## 🧪 Attack Simulation

A scheduled task was created using:
schtasks /create /sc minute /mo 5 /tn "UpdaterTask" /tr "notepad.exe"


This simulates MITRE ATT&CK:
- T1053 - Scheduled Task/Job

---

## 📊 Log Source

- Windows Security Logs
- Event ID: **4688 (Process Creation)**

---

## 🔍 Detection Queries

### Basic Detection (Working)
index=* EventCode=4688 New_Process_Name="*schtasks.exe"
| table _time Account_Name New_Process_Name


---

### Attempted Command-Line Detection (Failed)


index=* EventCode=4688 Process_Command_Line="schtasks"


❌ No results due to missing command-line logging.

---

## 🚨 Alert Configuration

- Trigger condition: Number of results > 0
- Schedule: Cron-based
- Action: Add to Triggered Alerts

---

## 📸 Screenshots

### schtasks detection in Splunk
![schtasks events](screenshots/schtasks_events_4688.png)

### Detection query
![query](screenshots/schtasks_search_query.png)

### Missing command line
![no cmd](screenshots/schtasks_no_commandline.png)

### Alert configuration
![alert](screenshots/schtasks_detection_alert.png)

---

## ⚠️ Challenges

- `Process_Command_Line` field was empty
- Limited detection visibility

---

## 🧠 Key Learning

- Process creation logs (4688) can detect execution
- Command-line logging must be enabled for deeper detection
- Detection engineering often requires improving telemetry

---

## 🚀 Next Improvements

- Enable command-line logging
- Detect suspicious task names
- Monitor Event ID 4698 (task creation)
