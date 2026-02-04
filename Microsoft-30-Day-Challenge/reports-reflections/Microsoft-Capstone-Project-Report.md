# Incident Report
## ID 164: Multi-stage incident involving Execution & Lateral movement on one endpoint

**Date:** 2026-01-30

---

## Findings

**Initial Phishing Email Time:** 2026-01-30 16:17:44 UTC

**Initial Remote Logon:** 2026-01-30 16:59:57 UTC

**Victim Host:** MSDFIR-SHA-VM

**Victim Host IP:** 10[.]0[.]0[.]xx (Toronto, Canada)

**Victim User:** Michael S****

**Victim User Email:** mich***[@]sham***[.]onmicrosoft[.]com

**Attacker Email:** john[.]bob[.]bi*****[@]outlook[.]com

**Attacker Host:** DESKTOP-M**** (Observed Device: Unknown Device)

**Attacker IP:** 185[.]245[.]xx[.]xx (London, UK)

**Attacker Infrastructure:** SurfShark VPN, ASN AS62240

**Phishing Email Subject:** "Overdue Invoice #87234 - Action Required"

**Malicious URLs:**

- hxxps://github[.]com/gentilkiwi/mimikatz/releases/download/2.2.0-20220919/mimikatz_trunk[.]zip
- hxxps://raw[.]githubusercontent[.]com/redcanaryco/atomic-red-team/master/atomics/T1059.001/src/test[.]ps1

**File IOCs:**

- **mimikatz[.]exe**
    - SHA256: 61c0810a23580cf492a6ba4f7654566108331e7a4134c968c2d6a05261b2d8a1
    - Confirms file as malicious mimikatz[.]exe
    - Location: C:\Users\MichaelS****\AppData\Local\Temp\mimikatz_extracted\x64\mimikatz[.]exe
- **mimikatz[.]zip**
    - SHA256: 7accd179e8a6b2fc907e7e8d087c52a7f48084852724b03d25bebcada1acbca5
    - Confirms zip as malicious mimikatz[.]zip
    - Location: C:\Users\MichaelS****\AppData\Local\Temp\mimikatz[.]zip

**Malware Detected & Blocked:**

- HackTool:Win32/Mimikatz!pz (Detected during execution)
- Trojan:Win32/Kovter.L (Blocked)
- Trojan:Win32/Powessere.K (Blocked)
- Trojan:PowerShell/Sacepos.C (Blocked)
- VirTool:Win32/PsDnsTxtExec.B!MTB (Blocked)

---

## Investigation Summary

On 2026-01-30 16:17:44 UTC, the user Michael S**** received an email for a billing invoice from an unfamiliar account (john[.]bob[.]bi*****[@]outlook[.]com) with a link to pay the invoice. The user pressed the link and entered their credentials, allowing the attacker to successfully capture the information.

The attacker then remotely logged into a company device (MSDFIR-SHA-VM at 10[.]0[.]0[.]xx) from the UK at 16:59:57 UTC, in which the company does not operate. The attacker connected from device DESKTOP-M**** using IP address 185[.]245[.]xx[.]xx via SurfShark VPN. On the victim device, the attacker downloaded and executed mimikatz[.]exe at 17:08:28 UTC. Microsoft Defender successfully detected mimikatz while it began execution and stopped it.

The attacker attempted to execute additional malware including "Kovter.L", "Powessere.K", "Sacepos.C", and "PsDnsTxtExec.B!MTB" between 17:14:46 and 17:14:47 UTC, which Microsoft Defender successfully blocked.

---

## 5W1H

**Who:**

- **Victim:**
    - Hostname: MSDFIR-SHA-VM
    - Host IP: 10[.]0[.]0[.]xx
    - User: Michael S****
    - User Email: mich***[@]sham***[.]onmicrosoft[.]com
- **Attacker:**
    - Attacker Host: DESKTOP-M**** (Unknown Device)
    - Attacker IP: 185[.]245[.]xx[.]xx (London, UK - SurfShark VPN, ASN AS62240)
    - Attacker Email: john[.]bob[.]bi*****[@]outlook[.]com

**What:**

- Phishing attack leading to credential compromise
- Attempt to execute mimikatz[.]exe for credential dumping
- Multiple malware execution attempts (all blocked)

**When:**

- Initial phishing email: 2026-01-30 16:17:44 UTC
- Credential compromise (impossible travel): 2026-01-30 16:57:42 UTC
- Initial remote logon: 2026-01-30 16:59:57 UTC
- Mimikatz execution: 2026-01-30 17:08:28 UTC
- Additional malware attempts: 2026-01-30 17:14:46 - 17:14:47 UTC

**Where:**

- User account: mich***[@]sham***[.]onmicrosoft[.]com
- Victim host: MSDFIR-SHA-VM (10[.]0[.]0[.]xx)
- Attack origin: London, UK (185[.]245[.]xx[.]xx)

**Why:**

- Attackers targeted a company employee to capture passwords for lateral movement and privilege escalation
- Goal was to dump credentials and potentially move laterally through the network

**How:**

- Attacker successfully phished the user with fake billing invoice email
- User credentials were captured when entered on malicious link
- Attacker gained remote access to victim's machine from UK location
- Attacker downloaded and attempted to execute mimikatz[.]exe for credential dumping
- Attacker attempted to execute 4 additional malware payloads identified as "Kovter.L", "Powessere.K", "Sacepos.C", and "PsDnsTxtExec.B!MTB"
- Microsoft Defender successfully detected and blocked all malware execution attempts

---

## Recommendations

1. **Review email security policies and rules** meant to prevent phishing attempts to understand how this email from john[.]bob[.]bi*****[@]outlook[.]com bypassed the system. Strengthen email filtering and implement additional controls.
2. **Immediately isolate MSDFIR-SHA-VM** to prevent any further spread of the breach and allow a thorough investigation into determining how much access the attackers gained and whether lateral movement occurred.
3. **Force password reset** for mich***[@]sham***[.]onmicrosoft[.]com and verify MFA is enabled for all users, especially privileged accounts. Review all accounts for signs of credential compromise.
4. **Restore the infected device** MSDFIR-SHA-VM** from a known good backup dated prior to 2026-01-30 16:17:44 UTC.
5. **Assign phishing awareness training** to Michael S**** and all employees to improve recognition of phishing attempts and social engineering tactics.
6. **Block attacker infrastructure** - Add IP 185[.]245[.]xx[.]xx and email domain john[.]bob[.]bi*****[@]outlook[.]com to block lists.

---

## Attack Timeline (Summarized)

- **16:17:44** - Phishing email received by Michael S**** from john[.]bob[.]bi*****[@]outlook[.]com
- **16:28:06** - Legitimate user logon by Michael S**** (10[.]0[.]0[.]xx)
- **16:41:59** - User account modified in Core Directory
- **16:51:31** - Failed network logon attempt to MSDFIR-SHA-VM
- **16:57:42** - Impossible travel: Successful logon from London, UK (185[.]245[.]xx[.]xx) - credentials compromised
- **16:58:35** - Suspicious remote session alert triggered
- **16:59:57** - RemoteInteractive session established: Attacker from DESKTOP-M**** connected to MSDFIR-SHA-VM
- **17:07:30** - Attacker downloaded Mimikatz via PowerShell
- **17:07:37** - Mimikatz[.]zip file created on MSDFIR-SHA-VM
- **17:08:28** - Mimikatz[.]exe executed on MSDFIR-SHA-VM
- **17:08:29** - Microsoft Defender detected and blocked Mimikatz (HackTool:Win32/Mimikatz!pz)
- **17:14:34** - Attacker executed Atomic Red Team PowerShell test script
- **17:14:46-17:14:47** - Microsoft Defender blocked multiple malware execution attempts (Kovter.L, Powessere.K, Sacepos.C, PsDnsTxtExec.B!MTB)

---

---

## Appendix

### MITRE ATT&CK Techniques Observed

- **T1003** - OS Credential Dumping
- **T1059.001** - PowerShell
- **T1082** - System Information Discovery
- **T1083** - File and Directory Discovery
- **T1105** - Ingress Tool Transfer
- **T1218.005** - Mshta
- **T1550** - Use Alternate Authentication Material
- **T1555** - Credentials from Password Stores
- **T1570** - Lateral Tool Transfer

---

### Evidence & KQL Queries

#### Email Investigation
```kql
union EmailEvents, EmailPostDeliveryEvents, EmailUrlInfo, MessageEvents, MessagePostDeliveryEvents, MessageUrlInfo, UrlClickEvents
| where * has "mich***"
| project TimeGenerated, SenderFromAddress, RecipientEmailAddress, Subject
```

![](screenshots-dashboards/Day29-phishing.png)

---

#### Sign-in Analysis
```kql
SigninLogs
| project TimeGenerated, Identity, IPAddress, LocationDetails, UserPrincipalName, RiskState, TokenIssuerType
| sort by TimeGenerated asc
```
![](screenshots-dashboards/Day29-signin-logs.png)

---

#### Directory Changes
```kql
AuditLogs
| where TargetResources contains "mich***"
| project TimeGenerated, OperationName, Category, LoggedByService, Result, ActivityDisplayName, TargetResources
| sort by TimeGenerated asc
```
![](screenshots-dashboards/Day29-audit-logs.png)

---

#### Failed Logon Attempts
```kql
DeviceLogonEvents
| where TimeGenerated between (datetime(2026-01-30 16:45) .. datetime(2026-01-30 17:20))
| where ActionType contains "failed"
| project TimeGenerated, DeviceName, ActionType, AccountName, RemoteIP
```
![](screenshots-dashboards/Day29-failed-logon.png)

---

#### Successful Remote Logons
```kql
DeviceLogonEvents
| where TimeGenerated between (datetime(2026-01-30 16:45) .. datetime(2026-01-30 17:20))
| where ActionType contains "success" and LogonType contains "remote"
| project TimeGenerated, DeviceName, ActionType, AccountName, RemoteIP, AdditionalFields, LogonType
```
![](screenshots-dashboards/Day29-success-logon.png)

---

#### Mimikatz File Activity
```kql
DeviceFileEvents
| where FileName contains "mimikatz"
| project TimeGenerated, RequestAccountName, ActionType, FileName, FolderPath, InitiatingProcessFileName, InitiatingProcessCommandLine
| sort by TimeGenerated desc
```
![](screenshots-dashboards/Day29-success-logon.png)

---

#### Mimikatz Process Execution
```kql
DeviceProcessEvents
| where ProcessCommandLine contains "mimi" or InitiatingProcessCommandLine contains "mimi" or AdditionalFields contains "mimi"
| sort by TimeGenerated desc
```
![](screenshots-dashboards/Day29-mimikatzipexe.png)

---

#### Atomic Red Team Activity
```kql
DeviceProcessEvents
| where ProcessCommandLine contains "1059" and ProcessCommandLine contains "src"
```
![](screenshots-dashboards/Day29-av3.png)

---

#### Antivirus Detections - Mimikatz
```kql
DeviceEvents
| where ActionType startswith "antivirus"
| where AdditionalFields contains "mimi"
| project TimeGenerated, ActionType, FileName, FolderPath, AccountName, InitiatingProcessParentFileName, AdditionalFields
```
![](screenshots-dashboards/Day29-antivirus.png)

---

#### Multiple Malware Detections
```kql
DeviceEvents
| where ActionType startswith "antivirus"
| sort by TimeGenerated desc
| where AdditionalFields contains "PsDnsTxtExec" or AdditionalFields contains "kovter" or AdditionalFields contains "sacepos" or AdditionalFields contains "powessere"
```
![](screenshots-dashboards/Day29-av2.png)

---
