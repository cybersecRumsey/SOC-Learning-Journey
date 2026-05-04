# Investigation 001 - DNS Query Analysis
**Date:** May 3 2026
**Tool:** Sysmon via Windows Event Viewer
**Event ID:** 22 - DNS Query

## What I Did
Opened Event Viewer in my Windows 10 SOC lab and 
navigated to the Sysmon Operational logs. I was 
looking through events to practice identifying 
normal versus suspicious activity.

## What I Found
- Process: Windows Search
- Domain queried: fp-afd.azureedge.net
- Query Status: 0 - successful
- Resolved IP: 13.107.246.40
- User: SOC Analyst

<img width="400" height="430" alt="image" src="https://github.com/user-attachments/assets/59456e64-a8ef-450b-a742-85ea9b075a4a" />


## What I Figured Out
The domain azureedge.net is Microsoft Azure CDN 
infrastructure. Windows Search contacting Microsoft 
servers in the background is completely normal 
behavior on a Windows 10 machine so I marked 
this as legitimate.

## What Would Have Made This Suspicious
- A unexpected process like powershell.exe or 
  cmd.exe making this query
- An unknown or newly registered domain
- Query happening at unusual hours
- IP flagged as malicious on threat intel feeds

## What I Would Do If It Was Suspicious
1. Isolate the machine immediately
2. Check the domain and IP on VirusTotal
3. Review all other Sysmon events from that process
4. Look for persistence mechanisms
5. Escalate to Tier 2 with full findings

## Lesson Learned
Not every DNS query is suspicious. Context matters - 
who made the query, what domain, and does it make 
sense for that process to contact that domain.
