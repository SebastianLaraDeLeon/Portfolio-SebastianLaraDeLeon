**Objective**: Hunt for unusual process creation events initiated by accounts ending in “administrator” within a defined timeframe.
**Suspicious indicators**: Look for any LOLBINs being executed (cmd, powershell, rundll, wmic, mshta, etc.) and review its commandline arguments and any child processes.

**KQL**:

```
WindowsEvent
|where TimeGenerated between (datetime(yyyy-mm-dd HH:MM:SS) .. datetime(yyyy-mm-dd HH:MM:SS))
|where EventData.User endswith "administrator"
|where EventID == "1"
|project TimeGenerated,EventData.Image,EventData.ProcessGuid,EventData.CommandLine,EventData.CurrentDirectory,EventData.User,EventData.OriginalFileName,EventData.ParentImage,EventData.ParentCommandLine
|sort by TimeGenerated desc
```
