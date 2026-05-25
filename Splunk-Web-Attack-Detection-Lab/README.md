# Splunk Web Attack Detection Lab

## Overview

This project demonstrates a SOC-style web attack detection lab using:

- Splunk Enterprise on Ubuntu
- Windows 11 IIS Web Server
- Splunk Universal Forwarder
- IIS Log Monitoring
- SQL Injection Detection
- Command Injection Detection
- Alert Creation and Investigation

The objective was to simulate common web attacks and detect them using Splunk SPL queries and alerts.

---

# Lab Architecture

- Ubuntu VM running Splunk Enterprise
- Windows 11 VM running IIS
- Splunk Universal Forwarder installed on Windows
- IIS logs forwarded into Splunk

---

# Technologies Used

- Splunk Enterprise
- Splunk Universal Forwarder
- Ubuntu Linux
- Windows 11
- IIS Web Server
- PowerShell
- VirtualBox

---

# Skills Demonstrated

- SIEM administration
- Log ingestion troubleshooting
- Detection engineering
- SPL query writing
- SOC alert creation
- Threat hunting
- Web attack detection

---

# Initial Setup

## Splunk Enterprise Installation

Installed Splunk Enterprise on Ubuntu and verified services were running.

![Splunk Running](screenshots/01-splunk-running.png)

---

## Splunk Universal Forwarder Configuration

Configured the Universal Forwarder on Windows to send logs to the Splunk server.

![Forwarder Configured](screenshots/02-forwarder-configured.png)

---

# Challenges Faced

## Connectivity Issues Between Forwarder and Splunk

Initially the Universal Forwarder could not connect to Splunk on port 9997.

Problems identified:
- Incorrect forwarding IP configuration
- Port communication issues
- TCP connection failures

Troubleshooting performed:
- Verified VM networking
- Tested connectivity using:
  ```powershell
  Test-NetConnection <Splunk-IP> -Port 9997
  ```
- Corrected forwarding server configuration
- Restarted Splunk services

This was one of the most exciting parts of the lab because it felt like solving a real SOC infrastructure issue.

![Connectivity Troubleshooting](screenshots/03-connectivity-troubleshooting.png)

---

# IIS Log Ingestion

After fixing connectivity issues, IIS logs successfully appeared inside Splunk.

![IIS Logs](screenshots/04-iis-logs-ingested.png)

---

# Simulated Attacks

## SQL Injection Simulation

Generated SQL injection attempts against the IIS web server using:

```text
http://localhost/index.php?id=1' OR '1'='1
```

Splunk successfully detected the attack pattern inside IIS logs.

![SQL Injection Detection](screenshots/05-sql-injection-detected.png)

---

## Command Injection Simulation

Generated command injection attempts using:

```text
http://localhost/test?cmd=whoami
```

Splunk detected suspicious command execution attempts.

![Command Injection Detection](screenshots/06-command-injection-detected.png)

---

# Detection Engineering

Created a Splunk SPL query to identify suspicious web attack indicators.

## Detection Query

```spl
index=main sourcetype=iis
("UNION SELECT" OR "' OR '1'='1" OR "xp_cmdshell" OR "../" OR "cmd=whoami")
| table _time c_ip cs_method cs_uri_stem cs_uri_query sc_status
```

![Detection Query](screenshots/07-detection-query.png)

---

# Alerting

Created a high severity scheduled alert inside Splunk.

Alert configuration:
- Trigger condition: Number of results > 0
- Schedule: Every 5 minutes
- Severity: High

Successfully triggered alerts from simulated attacks.

![Triggered Alert](screenshots/08-triggered-alert.png)

---

# Lessons Learned

This project improved my understanding of:

- SIEM workflows
- Log ingestion pipelines
- Web attack indicators
- Threat detection engineering
- Splunk troubleshooting
- SOC investigation processes

I also learned the importance of troubleshooting infrastructure issues before detections can work properly.

---

# Future Improvements

- Add PowerShell attack detections
- Integrate Sysmon
- Create dashboards
- Add MITRE ATT&CK mapping
- Forward Windows Event Logs
- Recreate detections in Microsoft Sentinel

---

# MITRE ATT&CK Mapping

| Technique | Description |
|---|---|
| T1190 | Exploit Public-Facing Application |
| T1059 | Command and Scripting Interpreter |
| T1505 | Server Software Component |

---

# Author

Stoyan Vlahov

GitHub:
https://github.com/Stoyan898
