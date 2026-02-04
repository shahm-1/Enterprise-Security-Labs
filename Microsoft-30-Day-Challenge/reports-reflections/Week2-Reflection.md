# Week 2 Reflection

- The most surprising thing I learned was the level of **visibility and customization** Microsoft provides in the **Defender portal for email security**.
  - You can see who **opened an email**, who **clicked a URL**, and how messages move through the environment.

 ![Dashboard](/screenshots-dashboards/Day15-kenny-clicked-links.png)
*In Defender you can view which users clicked which link*

---

- Learned about running **phishing simulations** to identify users who may need **additional training**.
  - Explored the wide range of **policies and rules** available to enforce different **levels of protection** across the organization.

- I now feel **confident navigating many areas** of the Defender portal.
  - At the same time, I recognize there are many **details and deeper configurations** that will take time to fully master.
 
  ![Dashboard](/screenshots-dashboards/Day15-campaign-results.png)
*Microsoft's Built-In Phishing Simulation Results*

  ---

- What’s still unclear is **how Defender determines whether an email is phishing**.
  - There are configurable **confidence thresholds** that control whether mail is allowed or quarantined.
  - I want to better understand the **back-end decision process**, such as:
    - Indicators of compromise (IOCs)
    - Wording and email structure
    - Domain reputation
    - Attachments and embedded links
    - Sender relationships and contact history
  - Knowing how these factors are **prioritized** would strengthen investigations and detections.

- How I would explain these controls to a teammate:
  - **Safe Links policies** protect users by scanning URLs **at the time of click** and blocking access to malicious sites.
  - **Anti-phishing policies** help detect **impersonation and spoofing attempts**.
  - Both allow us to **define actions** when a threat is detected and enforce email security at scale.


| Without Safe Links | With Safe Links Policy |
|:------------------:|:----------------------:|
| ![Dashboard](/screenshots-dashboards/Day12-no-safelink.png) | ![Another Dashboard](/screenshots-dashboards/Day12-safelink-policy-active.png) |

- If I wrote another phishing report today, I would include **deeper analysis in the summary section** to better define the **scope and impact** of the attack.

