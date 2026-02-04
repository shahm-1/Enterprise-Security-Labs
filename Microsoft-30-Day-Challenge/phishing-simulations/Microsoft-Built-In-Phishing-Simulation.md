# Phishing Simulation Campaign - Day 15

## Campaign Overview

**Campaign Name:** sha-phishing-test2  
**Status:** Completed  
**Technique:** Social Engineering - Credential Harvest  
**Delivery Platform:** Email  
**Target:** All users in organization

## Campaign Results

### Simulation Impact
- **Users Compromised:** 0 out of 3 (0%)
- **Users Who Reported:** 0 out of 3 (0%)
- **Successfully Delivered:** 3 out of 3 (100%)
- **Messages Read:** 1 out of 3 (33%)
- **Training Assigned:** No users were assigned training as part of this simulation

### User Activity Breakdown
- **Clicked message link:** 0/3
- **Supplied credentials:** 0/3
- **Read message:** 1/3
- **Deleted message:** 0/3
- **Replied to message:** 0/3
- **Forwarded message:** 0/3
- **Out of office:** 0/3

## Campaign Configuration

### Simulation Details
- **Payload:** Expense report sharing
- **Target Users:** All users (no exclusions)
- **Scheduled Launch:** 2026-01-21 at 12:41:57 PM
- **End Date:** 2026-01-23 at 12:41:57 PM

### Attack Scenarios

#### Scenario 1: Banking Details Phishing
**Subject:** Banking Details URGENT  
**Sender:** Generic sender (Gmail)  
**Content:** Urgent request to change financial information with a malicious link  
**Technique:** Urgency + Link manipulation

#### Scenario 2: File Sharing Phishing
**Subject:** inloop Expenses Report.xlsx has been shared with you  
**Sender:** inloop Account Department <user[@]officence[.]com>  
**Content:** Fake file sharing notification prompting user to click "Open" button  
**Technique:** Trusted service impersonation (Office 365/OneDrive style)

## URL Click Analysis

### Malicious Domains Used
The simulation employed typosquatted domains designed to mimic legitimate services:

1. **www[.]officences[.]com** (typosquatted "Office")
2. **www[.]officenced[.]com** (typosquatted "Office")
3. **hxxps://google[.]com/** (legitimate domain for testing)

### Click Activity
**Total URL Clicks:** 2 clicks from 1 user  
**User:** kenny[@][redacted][.]onmicrosoft[.]com

#### Click Details:
1. **Jan 21, 2026 12:43 PM** - Clicked: hxxps://www[.]officenced[.]com/can/01a6faf0-cf9c-4b63-91...
   - Action: Allowed
   - Clicked Through: false

2. **Jan 21, 2026 12:37 PM** - Clicked: hxxps://www[.]officences[.]com/can/01a6faf0-cf9c-4b...
   - Action: Allowed
   - Clicked Through: false

### Advanced Hunting Queries

#### Query 1: URLs Containing "office"
```kql
UrlClickEvents
| where Url contains "office"
```
**Results:** 2 items identified

#### Query 2: URLs Containing "google.com"
```kql
EmailUrlInfo
| where Url contains "google[.]com"
```
**Results:** 3 items identified (timestamps: 11:38 AM, 11:37 AM, 11:46 AM)

## Landing Page Experience

When users clicked the malicious links, they were redirected to an educational landing page with the message:

> **"${DisplayName}, you were just phished by your security team."**
> 
> **"It's okay! You're human. Let's learn from this."**
> 
> Rather than stealing your login credentials like a cyber criminal, we have redirected you to this educational page instead and assigned you some training courses.

The landing page included:
- Tips to identify phishing messages
- Email header details showing the simulated phish
- Options to "Go to training" or "Add to calendar"

## Key Findings

### Positive Outcomes
1. **Zero Credential Submissions** - No users entered their credentials on the fake landing pages
2. **Email Security Controls Working** - Some content was blocked because sender wasn't in Safe Senders list
3. **User Awareness** - Despite clicking links, no users proceeded to enter credentials

### Areas for Improvement
1. **Zero Reports** - No users reported the suspicious emails to the security team
2. **Low Detection Rate** - Users didn't identify the obvious typosquatted domains
3. **Link Clicking Behavior** - One user clicked on links without verifying sender authenticity

## Recommendations

1. **Enhance Reporting Training**
   - Conduct targeted training on how to report suspicious emails using the built-in "Report Phishing" button
   - Emphasize that reporting suspicious emails is critical even if no action was taken

2. **Domain Verification Education**
   - Train users to hover over links before clicking to verify the actual destination URL
   - Teach users to recognize typosquatted domains (e.g., "officences" vs "office365")
   - Create a reference guide of legitimate company domains and services

3. **Sender Validation Awareness**
   - Educate users to verify sender email addresses, especially for urgent requests
   - Highlight the warning: "You don't often get email from..." as a red flag

4. **Implement Additional Controls**
   - Consider implementing URL rewriting/sandboxing for external links
   - Strengthen Safe Links policies in Microsoft Defender
   - Add banners to external emails indicating they originated outside the organization

5. **Continuous Simulation Program**
   - Run regular phishing simulations with varying difficulty levels
   - Track individual user performance over time
   - Provide immediate feedback and micro-learning opportunities

---

## Supporting Evidence

### Campaign Results Dashboard
![Campaign Results](/screenshots-dashboards/Day15-campaign-results.png)

*Overall simulation impact showing 0% users compromised and detailed activity metrics*

### Simulation Review and Configuration
![Creating Simulation Test](/screenshots-dashboards/Day15-creating-sim-test-org.png)

*Review page showing simulation configuration including delivery platform, technique, payloads, and target users*

### URL Click Analysis - Kenny's Activity
![Kenny Clicked Links](/screenshots-dashboards/Day15-kenny-clicked-links.png)

*Advanced hunting results showing kenny clicked on malicious URLs twice, with both actions allowed but not clicked through*

### URL Click Investigation - Office Domains
![Seeing Who Clicked URL](/screenshots-dashboards/Day15-seeing-who-clicked-url.png)

*KQL query results for URLs containing "office" showing the typosquatted domains used in the simulation*

### Email Investigation - Google Links
![Seeing Who Received Google Email](/screenshots-dashboards/Day15-seeing-who-received-google-email.png)

*EmailUrlInfo query results showing three instances of emails containing google.com URLs*

### Simulation Email Delivery Interface
![Sending Suspicious Email](/screenshots-dashboards/Day15-sending-suspicious-email.png)

*Email composition showing recipient and subject line "Banking Details URGENT"*

### Phishing Email - File Sharing Variant
![Simulation Email](/screenshots-dashboards/Day15-sim-email.png)

*The file sharing phishing email impersonating inloop Account Department with an "Expenses Report.xlsx" lure*

### Recipient View - Banking Phishing Email
![What the Receiver Sees](/screenshots-dashboards/Day15-what-the-receiver-sees.png)

*How the banking details phishing email appeared to recipients, with urgency tactics and malicious link*

### Educational Landing Page
![You've Been Phished](/screenshots-dashboards/Day15-youve-been-phished.png)

*The landing page users saw after clicking the malicious link, explaining the simulation and offering training resources*
