Findings

-Affected host: KCD-Web (172.16.1.7); account used: administrator.
-Inbound RDP connection (Sysmon EID 3) from malicious IP 195.210.107.2 (United States) was followed by a successful network authentication (4624).
-Network Discovery: Created and Executed Advanced IP Scanner.
-Defense Evasion: Real-time protection was disabled. Exclusions were added for the Administrator Desktop folder, the lsass.exe and kvc.exe processes, the .dmp extension, and the kvc.exe file path.
-Credential-dumping tools related with kvc.exe and KvcForensic.exe were created on the host.
-Credential access: kvc.exe executed kvc dump lsass and accessed lsass.exe; KvcForensic.exe was executed afterward. Dump creation was not confirmed.
-Investigation Summary

On 29 September 2026, an external malicious connection from IP 195.210.107.2 to KCD-Web’s RDP service was followed by successful network authentication with the administrator user. Over the next several minutes, Advanced IP Scanner executed, Microsoft Defender real-time protection was disabled, and exclusions were added. Files associated with the KVC toolset were created on the host. A credential-dumping command then executed through kvc.exe, which accessed LSASS, the Windows security process that handles credentials. KvcForensic.exe, a tool used to extract credentials from memory dumps, launched shortly afterward.

This sequence is strongly consistent with attempted credential theft and presents a risk of credential exposure. The available evidence does not confirm successful memory-dump creation, credential recovery, or subsequent credential misuse.

Who

Affected host: KCD-Web (172.16.1.7).
Source of activity: malicious external IP 195.210.107.2 (United States).
Account used: administrator.

What

External authentication was followed by scanner execution, changes that weakened Defender protection, creation of KVC-related files, execution of a credential-dumping command, confirmed LSASS access, and KvcForensic execution.

When

The observed activity occurred between 2026-09-29 19:14:53 and 19:20:22 UTC. This is the documented activity window; the available evidence does not establish whether the activity continued afterward.

Where

KCD-Web.kerningcitydental.ca, with internal IP address 172.16.1.7. The observed tools were located in the Administrator profile’s Downloads and Desktop directories.

Why

The activity is consistent with an attempt to obtain credentials available on the host. The actor’s broader objective could not be determined.

How

A connection from 195.210.107.2 to destination port 3389 preceded successful network authentication. Defender protection was subsequently weakened, and kvc.exe executed the command kvc dump lsass, followed by confirmed access to LSASS. How the credentials used for the initial authentication were obtained remains unknown.

Recommendations:

Escalate the suspected credential-access incident to the incident-response team and isolate KCD-Web according to response procedures. Terminate suspicious remote sessions.

Preserve relevant logs, tool files, Defender configuration changes, and any memory dumps or extraction outputs before cleanup.

Reset the administrator credentials. Because LSASS was accessed, assess whether other accounts that logged on to KCD-Web could be exposed, and revoke active sessions where applicable.

Re-enable Microsoft Defender real-time protection, remove unauthorized exclusions, restore approved security settings, and verify that protection remains enabled.

Quarantine the unauthorized KVC toolset and related artifacts after preserving evidence. Verify host integrity and assess rebuilding from a known-good baseline if integrity cannot be established.

Review other hosts for related tool execution, suspicious credential use, and lateral movement. Validate whether the external access was authorized and review the controls protecting the RDP service.
