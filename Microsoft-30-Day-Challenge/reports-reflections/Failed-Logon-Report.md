# Failed Logon Attempts Investigation Report

**Scenario:**  
You received an alert on **4/16/2021** for **multiple failed logon attempts**.

---

## Findings

- **Time of Activity:** 8:34:04.098 AM UTC  
- **Hosts Involved:** SOC-FW-RDP, SHIR-Hive  
- **Indicators of Compromise (IOC):**
  - Thousands of failed logon attempts (Event ID **4625**)
  - Multiple admin-style account names used  
- **Suspected Activity:** Possible brute force attack  
- **Notable Event:**  
  - Successful logon (Event ID **4624**) from the host using **NT AUTHORITY\SYSTEM** shortly after 1000+ failed attempts

---

## Investigation Summary

On **4/16/2021 at 8:34:04.098 AM UTC**, a large volume of failed logon attempts targeted multiple administrative-style account names such as:

- `\ADMINISTRATOR`  
- `\admin`  
- `\administrator`

The attempts occurred in **very high volume** and within a **short time frame**, indicating suspicious behavior consistent with a **potential brute force attack**.

The failed attempts primarily originated from two host devices:

- **SOC-FW-RDP**
- **SHIR-Hive**

Shortly after this activity, both hosts recorded a **successful authentication** using the **NT AUTHORITY\SYSTEM** account at **8:38:13.112 AM UTC**.

The combination of **thousands of failed attempts followed by a successful authentication** is concerning and warrants deeper investigation. At this stage, the activity is classified as **suspicious authentication behavior**. Further analysis is required, beginning with identifying the **source IP addresses** and reviewing **post-authentication activity**.

---

## **Who**, **What**, **When**, **Where**, **Why** & **How**

### **Who**
- Hosts: SOC-FW-RDP, SHIR-Hive  
- Account: NT AUTHORITY\SYSTEM  

### **What**
- Thousands of failed logon attempts using various admin account names  
- Subsequent successful authentication  

### **When**
- Failed attempts began: **4/16/2021 – 8:34:04.098 AM UTC**  
- Successful logon: **4/16/2021 – 8:38:13.112 AM UTC**

### **Where**
- Activity originated from: SOC-FW-RDP and SHIR-Hive

### **Why**
- Unknown at this stage

### **How**
- High-volume automated authentication attempts using multiple credentials, triggering the failed logon alert

---

## Recommendations

- If malicious behavior is confirmed:
  - Isolate the affected host(s)
  - Reset credentials
  - Perform full forensic review
  - Reimage systems if necessary
- Implement or review:
  - Account lockout policies  
  - Stronger password requirements  
  - Restricted administrative access  
  - Alerting and monitoring thresholds  

---
