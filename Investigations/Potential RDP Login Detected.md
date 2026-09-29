**Findings**

1) Time: 2026-09-19 4:00:59PM GMT and 2026-09-21 6:02:22PM GMT  
- Host: KCD-Web  
- Event Code: 3 (Network Connection)  
- Src_ip: 1.14.203.76 IP geolocated to China 
- Destination Port: 3389 (RDP)  

2) Time: 2026-09-19 4:01:30PM GMT and 2026-09-21 6:02:29PM GMT  
- Host: KCD-Web  
- User: administrator  
- Src_ip: 1.14.203.76 
- Event Code: 4624 (Successful login) 
- Logon Type: 3  


**Investigation**

Network connection happened on KCD-Web by 1.14.203.76 IP geolocated to China at 2026-09-19 4:00:59PM GMT and 2026-09-21 6:02:22PM GMT followed by a successful login both times with administrator account, no malicious activity detected around the time the login happened in the available telemetry  

- Disposition: True Positive — external RDP activity confirmed; authorization unknown. 

- WHO: KCD-Web affected host, administrator account used and source ip 1.14.203.76 IP geolocated to China, remote actor unknown 

- WHAT: 1.14.203.76 Successfully logged on KCD-Web using administrator account via RDP  

- WHEN: Network connection at  2026-09-19 4:00:59PM GMT and 2026-09-21 6:02:22PM GMT, Successful login at 2026-09-19 4:01:30PM GMT and 2026-09-21 6:02:29PM GMT 

- WHERE: KCD-Web host  

- WHY: the user’s intent could not be determined from available telemetry  

- HOW: the successful login happened via network connection on destination port 3389, confirming an RDP connection  

**Recommendations**  

-Confirm whether the administrator login from 1.14.203.76 was authorized. If unauthorized, escalate for containment and reset/revoke the administrator credentials according to incident-response procedures. 

 

 

 

 

 
