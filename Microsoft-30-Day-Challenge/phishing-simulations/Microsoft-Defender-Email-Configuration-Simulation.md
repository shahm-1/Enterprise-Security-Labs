# Microsoft Defender for Office 365 - Security Configuration & Testing

## Overview

Implementation and testing of Microsoft Defender for Office 365 security features across Days 10-14.

**Environment:** Microsoft 365 E5 (no Teams) | **Location:** Canada

---

## Day 10: User Provisioning

### Users Created

**Michael Scott**
- Username: Michael[@][redacted][.]onmicrosoft[.]com
- License: Microsoft 365 E5 (no Teams)
- Role: User (no admin access)

**Kenny**
- Username: kenny[@][redacted][.]onmicrosoft[.]com
- License: Microsoft 365 E5 (no Teams)
- Role: User (no admin access)

Both users successfully provisioned with active Outlook mailboxes and Attack Simulation Training access enabled.

---

## Day 12: Safe Links Policy

**Policy Name:** Sha-SafeLinks-Policy  
**Scope:** Organization-wide

### Configuration

✅ Safe Links checks malicious links when users click in email  
✅ Apply Safe Links to internal emails  
✅ Real-time URL scanning for suspicious links  
✅ Wait for URL scanning before delivering message  
❌ URL rewriting enabled (API-only mode disabled)

### Results

**Before Safe Links:**
- Links display as: hxxps://google[.]com
- Direct click-through to destination

**After Safe Links:**
- URLs rewritten to: `cad01[.]safelinks[.]protection[.]outlook[.]com/?url=...`
- Hover tooltip shows original URL with warning
- Real-time scanning before redirect

---

## Day 13: Anti-Phishing Policy

**Policy Name:** Sha-AntiphishingPolicy  
**Scope:** Organization-wide

### Configuration

- **Phishing Threshold:** 1 - Standard
- **User Impersonation Protection:** On for 2 users
- **Domain Impersonation Protection:** Off for owned domains
- **Mailbox Intelligence:** On
- **Mailbox Intelligence for Impersonations:** On

---

## Day 14: Phishing Report Testing

### Test Scenario

**Email Details:**
- Subject: "Cool Website" / "Greetings!"
- From: External Gmail account
- To: Michael Scott
- Content: Casual message with link to hxxps://google[.]com

### Workflow

1. **User Action:** Michael right-clicks email → Report → Report phishing
2. **Defender Analysis:** Email submitted and analyzed
3. **Classification:** Marked as phishing threat
4. **User Notification:** Michael receives confirmation that email was phishing

### Results

**Submission Dashboard:**
- Threats: 1
- Spam: 0
- Result: Being analyzed → Confirmed phishing

**Email Explorer showed:**
- Delivery details and timeline
- Sender information
- URL analysis (1 link detected)
- No initial threats detected, user report triggered review

**User received notification:**
> "The message you reported was found to be phishing."

---

## Summary

| Component | Status | Result |
|-----------|--------|--------|
| User Provisioning | ✅ Complete | 2 test accounts with active mailboxes |
| Safe Links | ✅ Active | URLs rewritten and scanned in real-time |
| Anti-Phishing | ✅ Active | Mailbox intelligence and impersonation protection enabled |
| Reporting Workflow | ✅ Validated | User report → Analysis → Classification → Notification working |

All security policies successfully implemented and tested. Users can report suspicious emails, Defender correctly analyzes threats, and reporters receive feedback.

---

## Supporting Evidence

### Day 10: User Setup
![User Creation - Michael](/screenshots-dashboards/Day10-Adding-Users.png)

![User Creation - Kenny](/screenshots-dashboards/Day10-Adding-Users2.png)

![Email Accounts Activated](/screenshots-dashboards/Day10-Activate-Both-Emails.png)

![Defender Email Explorer Access](/screenshots-dashboards/Day10-Defender-Email-Explorer.png)

![Defender Simulation Training](/screenshots-dashboards/Defender-Simulation-Training.png)

### Day 12: Safe Links
![Email Without Safe Links](/screenshots-dashboards/Day12-no-safelink.png)

![Email With Safe Links Active](/screenshots-dashboards/Day12-safelink-policy-active.png)

![Safe Links Policy Configuration](/screenshots-dashboards/Day12-safe-links-policy.png)

### Day 13: Anti-Phishing
![Anti-Phishing Policy Configuration](/screenshots-dashboards/Day13-Anti-Phishing-Policy.png)

### Day 14: Phishing Testing
![Report Phishing Menu](/screenshots-dashboards/Day14-report-phishing.png)

![Defender Submissions Dashboard](/screenshots-dashboards/Day14-defender-submissions.png)

![Email Marked as Phishing](/screenshots-dashboards/Day14-marked-as-phishing.png)

![Email Explorer - Reported Email](/screenshots-dashboards/Day14-email-explorer.png)

![User Notification - Phishing Confirmed](/screenshots-dashboards/Day14-michaels-result.png)
