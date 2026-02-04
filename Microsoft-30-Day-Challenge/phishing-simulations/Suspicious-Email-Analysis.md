# Suspicious Email Analysis

## Findings

**Time:** 2026-01-21 19:38:20 UTC  
**Host/Recipient Email:** k\*\*\*y[@]s\*\*\*3[.]onmicrosoft[.]com

### IOCs - Header Analysis

* **IOC IP:** 114[.]29[.]236[.]247;CTRY:HK;LANG:en;SCL:8;SRV:;IPV:NLI;SFV:SPM
* **IOC Email:** K\*\*\*n[.]M\*\*\*e[@]usa[.]dund0rmiffl1n[.]bg
* **IOC Domain:** dund0rmiffl1n[.]bg
* **IOC Auth:** spf=none, dmarc=none, dkim=none, compauth=fail reason=001
* **IOC Date:** 2025-01-11 19:07:06 UTC
* **IOC Attacker's Real Email:** n\*\*\*l[.]g\*\*\*vp[@]gmail[.]com
* **IOC Message ID:** 20260121193816[.]C84A53B0E[@]emkei[.]cz

## Investigation

Header analysis revealed multiple red flags indicative of a phishing attempt. The source IP (114[.]29[.]236[.]247) geolocates to Hong Kong (CTRY:HK), while the spoofed sender domain shows a Bulgarian country code (BG) - both inconsistent with our Scranton, PA-based supplier. The message ID contains emkei[.]cz, a known email spoofing service commonly used by threat actors. Additionally, the Reply-To address differs from the sender address, likely the attacker's relay email. All authentication checks (SPF, DMARC, DKIM) failed.

The email was automatically quarantined by our system before reaching the recipient. No user interaction occurred.

### 5 W's Summary

* **WHO:** Host: k\*\*\*y[@]s\*\*\*3[.]onmicrosoft[.]com
* **WHAT:** Received a suspicious email named "Billing URGENT" from a spoofed third-party paper vendor.
* **WHEN:** Email received at 2026-01-21 19:38:20 UTC; email creation time was spoofed to 2025-01-11 19:07:06 UTC.
* **WHERE:** Email was quarantined before reaching k\*\*\*y[@]s\*\*\*3[.]onmicrosoft[.]com inbox.
* **WHY:** Phishing attempt leveraging supplier impersonation and urgency tactics.
* **HOW:** Attacker used email spoofing technology (emkei[.]cz) to impersonate a legitimate vendor with a typosquatted domain and embedded malicious payment link.

## Actions Taken

1. Confirmed email as phishing attempt
2. Reported incident to Microsoft
3. Deleted email from quarantine
4. Conducted tenant-wide scope check for similar sender/subject combinations - no additional instances found

## Recommendations

1. Conduct a targeted review of emails received by k\*\*\*y[@]s\*\*\*3[.]onmicrosoft[.]com to determine if this is an isolated incident or part of a broader targeting pattern. If multiple instances are identified, immediately review and strengthen email filtering policies.
2. Perform a vendor security audit to identify potential gaps or vulnerabilities within the supply chain that could be exploited for social engineering attacks.
3. Escalate findings to stakeholders for vendor review. If the audit identifies significant security gaps with the third-party paper supplier, leadership should assess the risk-benefit of continuing the relationship.
4. If this incident is determined to be part of a broader phishing campaign, re-conduct user awareness training with emphasis on vendor impersonation and urgency-based social engineering tactics.

---

## Supporting Evidence

### Quarantine Overview
![Quarantine List View](../screenshots-dashboards/Day16-quarantine1.png)

*The phishing email captured in Microsoft Defender quarantine, showing high confidence phish classification*

### Email Details and Delivery Information
![Email Delivery Details](../screenshots-dashboards/Day16-details.png)

*Delivery details showing the email was blocked and quarantined before reaching the recipient*

### Authentication Failures
![Authentication Results](../screenshots-dashboards/Day16-auth.png)

*All email authentication checks (DMARC, SPF, DKIM) failed, with composite authentication showing "Fail"*

### Message Header Analysis
![Message Header](../screenshots-dashboards/Day16-quarantine.png)

*Complete message header showing the quarantined email and metadata*

![Microsoft Header Analyzer](../screenshots-dashboards/Day16-microsoft-header-analyzer.png)

*Detailed header analysis revealing the spoofed sender information and authentication failures*

### Phishing Email Content
![Email Preview](../screenshots-dashboards/Day16-defender-quarantine.png)

*The phishing email claiming to be from the billing department with urgent payment demands*

![Email Body Text](../screenshots-dashboards/Day16-Email-Spoofing.png)

*Plain text view of the phishing email showing urgency tactics and threat language*

### Malicious Attachment
![Fake Invoice](../screenshots-dashboards/Day16-fake-invoice.png)

*The fraudulent invoice attached to the phishing email, designed to appear legitimate*

### Remediation Actions
![Delete Confirmation](../screenshots-dashboards/Day16-delete.png)

*Permanent deletion of the phishing email from quarantine*
