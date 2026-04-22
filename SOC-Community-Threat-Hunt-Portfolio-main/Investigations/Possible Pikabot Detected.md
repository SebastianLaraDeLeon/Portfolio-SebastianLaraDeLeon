**Findings**

- Time: 2024-03-11 14:21:18 UTC
- Host: 192.168.10.34
- IOC Domain: evil[.]com
- IOC IP: 1.1.1.1
- Possible Malware Family: Pikabot
- Filename: Pikachu.exe
- SHA256 Hash: aaabbbccc

**Investigation**

On 2024-03-11 14:21:18 UTC, the user on host: 192.168.10.34 was seen accessing a domain: evil[.]com which led to a download of a file on 2024-03-11 14:22:58 UTC named Pikachu.exe. Based on our investigation, this file has been reported in the wild as malicious and related to Pikabot. Pikabot is a downloader/installer meaning that its purpose is to download and/or install additional malware onto the host. Based on the PCAP provided and evidence available, we cannot say with confidence if the activity is still on-going. 

- WHO - Host: 192.168.10.34 
- WHAT - Downloaded a malicious file named: Pikachu.exe after accessing the domain: evil[.]com 
- WHEN: Based on the PCAP, user accessed the site on 2024-03-11 14:21:18 UTC & downloaded the file on 2024-03-11 14:22:58 UTC – we cannot determine if the activity is still on-going nor was the file executed. 
- WHERE: The activity took place on a computer with the IP address 192.168.10.34 
- WHY: The intent behind accessing the malicious domain and downloading the file is not provided. 
- HOW: The user presumably navigated to the domain and initiated a download, either knowingly or unknowingly, which resulted in the Pikachu.exe file being downloaded onto the host machine. 

**Recommendations** 

1) Check for evidence of execution of Pikachu.exe on the host: 192.168.10.34, if the application had been executed, Immediately isolate this host and consider a forensic investigation to determine the impact of this incident. Otherwise perform a complete wipe of this machine to ensure complete removal of additional artifacts that may be left behind. 

2) Run a query searching for the domains, IPs & file hash of the file downloaded to identify other hosts exhibiting similar behaviors. If additional hosts were found, immediately isolate them as well. 

3) Although domains are relatively easy to change for an attacker, consider placing these domains in a blocklist to prevent additional compromise.

**INCLUDE SCREENSHOTS HERE**
