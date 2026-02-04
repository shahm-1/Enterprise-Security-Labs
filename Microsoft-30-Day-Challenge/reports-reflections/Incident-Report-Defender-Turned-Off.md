# Incident Report ; Alert - Attempt to turn off Microsoft Defender Antivirus Protection.

Findings:

- Time: 2026-01-29 01:25:45 UTC
- Alert Title: Attempt to turn off Microsoft Defender Antivirus Protection
- Severity: High
- Host: MyDFIR-ShaVM
- Device Ip 10.0.0.53
- User: SM-Admin
- Initiating Processes: (Parent)explorer.exe > (Parent)powershell.exe > (Child)PowerShell.EXE
- File path: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
- SHA 256: 0ff6f2c94bc7e2833a5f7e16de1622e5dba70396f31c7d5f56381870317e8c46
- Command Line: "powershell.exe" & {Set-ItemProperty \""HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender\"" -Name DisableAntiSpyware -Value 1}
- RegistryValueName: DisableAntiSpyware
- New Registry Value: HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\DisableAntiSpyware 1
- Original Registry Value: HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\DisableAntiSpyware “ “
- MITRE Tactic: Defense Evasion; Technique: T1562.001 Disable Or Modify Tools

Investigation Summary:

On 2026-01-29 01:25:45 UTC, Microsoft Defender for XDR generated an alert for an attempt to turn off the Microsoft Defender Antivirus security feature on host MyDFIR-ShaVM which has an IP of 10.0.0.53. The process PowerShell.EXE attempted to change a registry value located in “HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender\”. This attempt to change the registry value of DisableAntiSpyware from 0 to 1 would have disabled the Microsoft Defender Antivirus. This technique is used by adversaries to modify or disable security tools to avoid detection of their malware and activities.

This alert became part of the incident ID 152: Hands-on keyboard attack was launched from a compromised account (attack disruption), which first saw activity on 2026-01-26 17:06:53 UTC. I looked into the events that took place immediately after this alert and found that at 2026-01-29 01:25:46 UTC another alert named “Tamper protection in Microsoft Defender for Endpoint ignored the modification of the DisableAntiSpyware registry key's value to Unknown”. This tells us that Tamper protection prevented the modification attempt.

5W1H:

- WHO - Host: MyDFIR-ShaVM, Device Ip 10.0.0.53, User: SM-Admin
- WHAT - Attempt to disable Defender Antivirus.
- WHEN: Based on the investigation the modification was made at 2026-01-29 01:25:45 UTC.
- WHERE: The activity took place in the Device Registry at: HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows Defender\DisableAntiSpyware
- WHY: Potential defense evasion technique part of Incident ID: 152.
- HOW: Explorer.exe spawned powershell.exe which spawned PowerShell.EXE which executed the command "powershell.exe" & {Set-ItemProperty \""HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender\"" -Name DisableAntiSpyware -Value 1}.

Recommendations:

1. Because this alert is part of an Incident that hasn’t been resolved I suggest to isolate the host until further investigation can reveal the scope of the incident and the full attack chain.

Alert Timeline:

- 2026-01-29 01:14:32 UTC → explorer.exe process created.
- 2026-01-29 01:20:30 UTC → explorer.exe spawns powershell.exe.
- 2026-01-29 01:20:30 UTC → powershell.exe spawns PowerShell.EXE.
- 2026-01-29 01:25:45 UTC → powershell.EXE runs the command "powershell.exe" & {Set-ItemProperty \""HKLM:\SOFTWARE\Policies\Microsoft\Windows Defender\"" -Name DisableAntiSpyware -Value 1}
