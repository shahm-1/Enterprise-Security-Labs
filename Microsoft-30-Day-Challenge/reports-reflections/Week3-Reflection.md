# Week 3 Reflection

## 1. What surprised you about the data Defender for Endpoint captures?
What surprised me is just how much information it captures. It really seems like it doesn't miss much.

![](/screenshots-dashboards/Day23-incident-graph.png)
*Incident Story*

---

## 2. Did your hunting hypothesis surface anything meaningful?
My hunting hypothesis returned evidence of remote IP connections to URLs. However, it is still undetermined whether this was legitimate or malicious activity.

![](/screenshots-dashboards/Day22-query2.png)
*Cmd.exe was found spawning powershell.exe which was found connecting to Remote IP connections to URLs.*

---

## 3. What challenges did you face when trying to validate your hypothesis?
I wouldn't say I found it too difficult because using a structured hunting hypothesis let me know where to begin my search. I think had I used an unstructured or situational approach I may have experienced challenges.

---

## 4. Do you feel more comfortable investigating endpoint threats now?
I do feel comfortable investigating endpoint threats. With the amount of different alerts I have the opportunity to investigate, I believe I will become confident fairly quickly in my ability to triage endpoint-related alerts.
