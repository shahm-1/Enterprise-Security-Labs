# PowerShell Network Activity Threat Hunt

## Hypothesis
PowerShell is rarely used by normal users to download files. If PowerShell is observed—whether directly launched or spawned by another process—reaching out to external IPs or URLs, it may indicate command and control (C2) or malicious download activity.

## Key Findings

### Timeline
**Date/Time:** 2026-01-27T16:07:59.0830705Z UTC  
**Affected Host:** `sha-vm`  
**Action Type:** ConnectionSuccess

### Indicators of Compromise (IOCs)

| Indicator Type | Value |
|----------------|-------|
| Remote IP | `140.82.114.4` |
| Remote Port | `443` (HTTPS) |
| Remote URLs | `codeload[.]github[.]com`<br>`https://raw[.]githubusercontent[.]com/S3cur3Th1sSh1t` |
| Process | `PowerShell.exe` |

### Parent Process Chain
PowerShell was spawned by the following parent processes:
- `svchost.exe`
- `explorer.exe`
- `cmd.exe`

## Analysis

The hypothesis predicted that PowerShell connecting to external IPs and URLs could indicate C2 or malicious download activity. During the hunt, I identified multiple suspicious network connections originating from `PowerShell.exe`.

**Unusual Behavior Detected:**
- PowerShell was spawned by processes like `svchost.exe`, `explorer.exe`, and `cmd.exe`—methods not typically used by standard users for legitimate software installation
- External connections to GitHub infrastructure (`codeload.github.com` and `raw.githubusercontent.com`) were observed
- The specific repository path `/S3cur3Th1sSh1t` is associated with known red team tools

**External Validation:**
- File hashes and the remote IP (`140.82.114.4`) were checked against VirusTotal and returned clean results
- GitHub IP addresses are legitimate, but the content hosted there may still be malicious

## Conclusion

While the remote IP and domain are legitimate GitHub infrastructure, the connections validate the hypothesis that **unusual PowerShell network activity was detected**. The behavior deviates from normal user patterns and warrants further investigation.

**Determination:** The malicious nature of these connections cannot be conclusively determined at this time, but the activity is **suspicious** and aligns with tactics used in credential theft, lateral movement, or post-exploitation tooling.

## Recommended Next Steps

1. **Investigate File Creation Events**
   - Query `DeviceFileEvents` to identify files created during or after the PowerShell connections
   - Correlate any downloaded files with the GitHub URLs identified

2. **Expand Scope**
   - Search for similar PowerShell network activity across other endpoints
   - Check for persistence mechanisms (scheduled tasks, registry keys, startup items)

3. **User Context**
   - Verify if the user account has a legitimate reason to download tools from GitHub
   - Interview the user or system owner to determine intent

4. **Threat Intelligence**
   - Research the repository `/S3cur3Th1sSh1t` for known malicious tools or frameworks
   - Cross-reference with recent threat intelligence reports
