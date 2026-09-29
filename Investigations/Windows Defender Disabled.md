**Findings**

1) Time: 2026-09-19 12:47:00 UTC 
- Host: KCD-WEB 
- user: administrator 
- IOC: Successful external logon to the Administrator account 
- IOC IP: 85.215.216.60 geolocated to Germany 

2) Time: 2026-09-19 12:47:37 UTC 
- Host: KCD-WEB
- User: administrator 
- Finding: New local account created 
- Account name: Admin0  

3) Time: 2026-09-19 12:47:46 UTC 
- Host: KCD-WEB 
- User: administrator 
- Finding: Admin0 added to the local Administrators group 
- Event ID: 4732 

4) Time: 2026-09-19 12:48:16 UTC 
- Host: KCD-WEB 
- User: administrator 
- Finding: Microsoft Defender detected Backdoor:Win32/PulsarRat.AR!AMTB 
- File path: C:\Users\administrator\Desktop\boot.exe 

5) Time: 2026-09-19 12:48:25 UTC 
- Host: KCD-WEB 
- user: administrator 
- IOC:  Microsoft Defender real-time protection disabled 
- IOC Event ID:5001 
6) Time: 2026-09-19 12:48:47 UTC 
- Host: KCD-WEB 
- User: administrator 
- Finding: PulsarRAT boot.exe executed 
- Evidence: Sysmon Event ID 1 
- File path: C:\Users\administrator\Desktop\boot.exe 
- SHA256: 76e0fc33fc0f8418c5e1660a54dbec8fcd608ae0850d03e557d6e8b5ee88aa67 

7) Time: 2026-09-19 12:48:50 UTC 
- Host: KCD-WEB 
- User: administrator 
- IOC: System32.exe file on a suspicious file path 
- Filename: System32.exe 
- File path: C:\Windows\System32\Tasks\System\System32.exe 
- SHA256 Hash: Not Available in collected telemetry 
- Persistence: A scheduled task named System was configured to execute the file at user logon. 

**Investigation**

At 2026-09-19 12:47:00 UTC, an external IP 85.215.216.60 (Geolocated to Germany) successfully accessed the KCD-Web host using the Administrator account. Within two minutes, a new administrator-level account (Admin0) was created, Microsoft Defender detected boot.exe as a malicious remote access program before real-time protection was disabled by the attacker, this program was later executed and System32.exe was configured to run automatically whenever a user logs in. The execution of boot.exe gave the attacker remote access capability to the compromised machine. System32.exe has not been executed based on the available telemetry 

Who KCD-Web host, administrator user and 85.215.216.60 IP (Geolocated to Germany) 

- WHAT: 85.215.216.60 successfully logged in as Administrator. This was followed by creation of the privileged Admin0 account, boot.exe file was detected by Microsoft Defender before real-time protection was disabled, creation and execution of boot.exe to gain remote access to the compromised machine and configuration of a system32.exe to execute at user logon. 

- WHEN: Between 2026-09-19 12:47:00 UTC and 2026-09-19 12:48:50 UTC 

- WHERE: KCD-Web host 

- WHY: The observed activity is consistent with an attempt to establish persistent, privileged access to the host. 

- HOW: A successful external login to the Administrator account was observed from 85.215.216.60. Multiple failed login attempts from other external IP addresses occurred beforehand; however, the credential-acquisition method cannot be confirmed from the available telemetry. 

**Recommendations** 
1)Disable newly created Admin0 account immediately and reset/revoke the administrator account credentials 

2)Remove the scheduled task named System and quarantine/remove boot.exe and System32.exe 

3)Re-enable Microsoft Defender real-time protection and verify it remains enabled 

4)Isolate KCD-Web from the network pending remediation and review. 

5)Rebuild KCD-Web from a known-good baseline after preserving forensic evidence, because a PulsarRAT backdoor was confirmed to execute. Removing the detected files alone cannot be trusted to fully remediate the host. 

 
