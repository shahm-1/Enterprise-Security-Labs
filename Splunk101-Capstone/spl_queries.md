# Splunk Queries Used in Investigation

## Query 1 - Data Source Discovery
```
index="sha-soc" extracted_host="FRONTDESK-PC1" (user="Ryan.Adams" OR User="KCD\\Ryan.Adams")
| stats count by sourcetype, EventCode
| sort -count
```

## Query 2 - Failed Login Attempts
```
index="sha-soc" extracted_host="FRONTDESK-PC1" EventCode=4625
```

## Query 3 - Successful Logins from DESKTOP-924H12
```
index="sha-soc" extracted_host="FRONTDESK-PC1" Workstation_Name="DESKTOP-924H12" action=* src_ip=*
| table _time, action, Workstation_Name, src_ip, user, Logon_Type
| sort -_time
```

## Query 4 - File Creation Events
```
index="sha-soc" extracted_host="FRONTDESK-PC1" (user="Ryan.Adams" OR User="KCD\\Ryan.Adams") earliest="10/15/2025:12:45:00" latest="10/15/2025:13:15:00" EventCode=11 source="sysmon.csv" sourcetype="WinEvent:Sysmon"
| table _time, TargetFilename, action, file_name, file_path, process_exec, signature
| sort _time
```

## Query 5 - Process Execution
```
index="sha-soc" extracted_host="FRONTDESK-PC1" (user="Ryan.Adams" OR User="KCD\\Ryan.Adams") earliest="10/15/2025:12:45:00" latest="10/15/2025:13:15:00" EventCode=1 source="sysmon.csv" sourcetype="WinEvent:Sysmon"
| table _time parent_process_exec process_exec
| sort +_time
```

## Query 6 - Python Network Connections (Generic)
```
index="sha-soc" host="FRONTDESK-PC1" src_ip="172.16.0.110" python
```

## Query 7 - Network Connection Details
```
index="sha-soc" extracted_host="FRONTDESK-PC1" (user="Ryan.Adams" OR User="KCD\\Ryan.Adams") earliest="10/15/2025:12:45:00" latest="10/15/2025:13:15:00" EventCode=3 source="sysmon.csv" sourcetype="WinEvent:Sysmon"
| table _time process_exec src_port src_ip DestinationPort dest_ip user
| sort +_time
```

## Query 8 - PowerShell Execution
```
index="sha-soc" extracted_host="FRONTDESK-PC1" (user="Ryan.Adams" OR User="KCD\\Ryan.Adams") earliest="10/15/2025:12:45:00" latest="10/15/2025:13:15:00" EventCode=1 source="sysmon.csv" sourcetype="WinEvent:Sysmon" process_exec="powershell.exe"
```

## Query 9 - Scheduled Task Creation
```
index="sha-soc" extracted_host="FRONTDESK-PC1" earliest="10/15/2025:13:04:00" latest="10/15/2025:13:06:44" sourcetype="WinEvent:Sysmon" EventCode=1
| table _time, process, CommandLine, parent_process_exec
```

## Query 10 - Sysmon Events During Persistence Phase
```
index="sha-soc" extracted_host="FRONTDESK-PC1" earliest="10/15/2025:13:04:00" latest="10/15/2025:13:06:44" sourcetype="WinEvent:Sysmon"
| sort -_time
```

## Query 11 - Windows Defender Disabled
```
index="sha-soc" extracted_host="FRONTDESK-PC1" earliest="10/15/2025:13:04:00" latest="10/15/2025:13:06:44" sourcetype="WinEvent:Application"
```

## Query 12 - Account Logoff and SYSTEM Login
```
index="sha-soc" extracted_host="FRONTDESK-PC1" earliest="10/15/2025:13:04:00" latest="10/15/2025:13:06:44" sourcetype="WinEvent:Security"
```

---

### DESKTOP-924H12 Investigation
```
index="sha-soc" extracted_host="DESKTOP-924H12"
| stats count by sourcetype, EventCode
```

```
index="sha-soc" extracted_host="DESKTOP-924H12"
| stats count by user
| sort -count
```

### Logon Type Analysis
```
index="sha-soc" extracted_host="FRONTDESK-PC1" EventCode=4624 action="success" TargetUserName="Ryan.Adams"
earliest="10/15/2025:12:52:00" latest="10/15/2025:13:05:00"
| table _time, TargetUserName, LogonType, Workstation_Name, src_ip
```

### Zone.Identifier Investigation
```
index="sha-soc" extracted_host="FRONTDESK-PC1" EventCode=15
TargetFilename="*python.exe:Zone.Identifier*"
| table _time, TargetFilename, Image, Contents
```
