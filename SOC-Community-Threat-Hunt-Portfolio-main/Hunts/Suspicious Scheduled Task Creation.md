**Technique: T1053.005 – Scheduled Task / Job: Scheduled Task**

**Summary**:
Adversaries may abuse Windows Scheduled Tasks to establish persistence, gain elevated privileges, or execute malicious programs at specific times. Scheduled tasks allow attackers to automate execution without user interaction, ensuring their payload continues to run even after reboots or logouts. Common abuse involves creating new tasks that launch PowerShell, scripts, or malware binaries.

**Detection Strategy**:

**Log sources**:

- DeviceProcessEvents (look for schtasks.exe or powershell.exe creating tasks)

- Windows Event ID 4698 (Task created)

- Sysmon Event ID 1 (process creation) with schtasks.exe

**Suspicious indicators**:

- Use of schtasks.exe /create with unusual task names (random strings, updates, helpers)

- Tasks pointing to executables/scripts in temp or user directories

- Encoded PowerShell or command-line obfuscation in task actions

**KQL**:

``DeviceProcessEvents
| where FileName == "schtasks.exe"
| where ProcessCommandLine has "/create"
| project Timestamp, DeviceName, AccountName, ProcessCommandLine, InitiatingProcessFileName
| order by Timestamp asc``


**Triage & Investigation**:

- Check task name and path - is it a standard system task or something unusual?

- Identify the account that created the task - is it a legitimate admin or an unexpected user?

- Review command-line arguments for encoded or obfuscated commands.

- Investigate what binary/script is being launched by the task.

- Pivot: Were similar tasks created on other endpoints around the same time?

**Mitigation & Remediation**:

Mitigation:

- Restrict permissions to create scheduled tasks to administrators only.

- Implement application control to prevent execution of unauthorized scripts.

Remediation:

- Disable or delete the malicious scheduled task.

- Quarantine or remove associated binaries/scripts.

- Reset credentials for the account that created the task if compromised.
