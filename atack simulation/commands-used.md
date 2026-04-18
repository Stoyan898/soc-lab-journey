
# 🧪 Commands Used in Attack Simulation

## 👤 Create a New User

```powershell
net user attacker Password123! /add
```

Creates a new local user account.

---

## 🔑 Add User to Administrators Group

```powershell
net localgroup administrators attacker /add
```

Grants administrative privileges to the user.

This action generates:

* Event ID 4672 (Privilege assignment)

---

## 📊 Check Audit Policy

```powershell
auditpol /get /category:*
```

Verifies which logging categories are enabled.

---

## ⚙️ Enable Process Creation Logging

```powershell
auditpol /set /subcategory:"Process Creation" /success:enable
```

Ensures process creation events (Event ID 4688) are logged.

---

## 🧾 Enable Command Line Logging

```powershell
reg add "HKLM\Software\Microsoft\Windows\CurrentVersion\Policies\System\Audit" /v ProcessCreationIncludeCmdLine_Enabled /t REG_DWORD /d 1
```

Allows visibility into command-line arguments used in processes.

---

## 🧠 Purpose of These Commands

These commands simulate attacker behavior such as:

* Privilege escalation
* Account manipulation
* Command execution

They are used to generate logs that can be detected and analyzed in Splunk.

---
