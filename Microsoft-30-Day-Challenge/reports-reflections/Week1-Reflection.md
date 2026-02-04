# Week 1 Reflection

---

![Dashboard](/screenshots-dashboards/Day5-Dashboard1-2.png)
*Number of Failed Logon Attempts based on Account Name*

I learned that Dashboards can help a SOC Analyst monitor patterns without having to run the query.

---

```kql
SecurityEvent_CL
| where TimeGenerated between (todatetime('2026-01-12T20:57:17.010024Z') .. todatetime('2026-01-12T20:58:17.010024Z'))
| where Computer contains "soc-fw-rdp"
| where EventSourceName_s contains "locker"
| project TimeGenerated, Computer, AccountType_s, EventID_s, EventSourceName_s
| order by TimeGenerated desc
```
*KQL Query used to discover which accounts had the most failed login attempts*

I learned that KQL can help a SOC Analyst answer questions they might have by starting with a table then adding operators to filter out the noise.

---

- Learned the importance of using a consistent **naming structure** when architecting a SOC environment.

- Created a **Virtual Machine in Oracle VirtualBox** and built a SOC lab in **Azure** by deploying **Log Analytics Workspaces** and connecting them to **Microsoft Sentinel**.
  - Ingested **Azure Activity** and **Microsoft Defender XDR** logs into Sentinel.
  - Gained an understanding of how different components are **interconnected** to deliver SOC functionality and support real use cases.

- Used **Microsoft Sentinel** to explore ingested telemetry and ran **KQL queries** to identify interesting activity.
  - Learned that logs are like **large datasets/spreadsheets**, and KQL is essential for **narrowing, filtering, and extracting** meaningful information.

- Explored the **Microsoft Defender portal** and built **dashboards** to visualize and interpret data.
  - Created **scheduled analytics rules** based on detection logic.
  - Learned how rules generate **alerts**, which then create **incidents** for investigation.
  - Understood that investigations follow a **layered approach**, starting with defining the activity of interest and building detections around it.

- Found that the most challenging part of Week 1 was **reporting and communicating findings**.
  - Still working on identifying **meaningful connections** in the data and presenting them clearly for **leadership-level reporting**.

- The most valuable lesson from Week 1 is that SOC tools are **only tools**.
  - Their value depends on how effectively they are used.
  - Progress comes from **consistency, practice, and seeking feedback**.

- Most excited to work on **email analysis** in upcoming weeks and continue building projects that **demonstrate learning and growth**.
