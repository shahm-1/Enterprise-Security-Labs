# 🏗️ Enterprise Security Labs

Production-style lab environments built for hands-on security operations practice.

These aren't quick tutorials — they're **fully functional enterprise environments** with Active Directory, cloud identity integration, audit logging, and security monitoring. I use them to practice detection engineering, incident response, and identity security.

---

## 🎯 Why I Built These

**To learn by doing.** Reading about Active Directory security is different from actually configuring GPOs, investigating failed authentications, and tracing lateral movement across domain-joined systems.

**What makes them "enterprise-focused":**
- Real infrastructure (not simulations): Windows Server, domain controllers, member servers, workstations
- Production-grade tools: Group Policy, Azure Entra ID, SIEM integration, audit logging
- Actual use cases: These labs support my threat hunting investigations and vulnerability assessments
- Continuous operation: Not one-and-done setups — I maintain and expand them as I learn

---

## 🏛️ Lab Environments

| Lab | Purpose | Key Components |
|-----|---------|----------------|
| **[Active Directory Enterprise Lab](./Active-Directory-Enterprise-Lab/)** | Windows identity & authentication security | Domain controllers, DNS integration, GPOs, security groups, OUs, audit policy configuration |
| **[Azure & Entra ID Identity Lab](./Azure-Entra-ID-Identity-Lab/)** | Hybrid cloud identity management | On-prem AD sync, conditional access policies, MFA enforcement, privileged identity management, identity protection alerts |
| **[Security Operations & Ticketing Lab](./Security-Operations-Ticketing-Lab/)** | SOC workflow simulation | Incident categorization, priority assignment, escalation procedures, metrics tracking, case management |

**→ Each folder contains setup documentation, architecture diagrams, and lessons learned.**

---

## 🛠️ Technologies Used

**Infrastructure:** Windows Server 2019/2022 • Windows 10/11 • VMware / Hyper-V  
**Identity:** Active Directory • Azure Entra ID • Group Policy • DNS  
**Security:** Microsoft Defender for Endpoint • SIEM platforms • Audit logging • Sysmon  
**Cloud:** Azure • Microsoft 365 • Hybrid identity sync

---

## 🎓 What I've Practiced

- Domain controller configuration and hardening
- Group Policy security baselines
- Hybrid identity architecture (on-prem ↔ cloud)
- Conditional access and zero trust policies
- Security event collection and monitoring
- Attack simulation and detection testing
- Incident workflow management

---

## 🔗 Related Work

**[Main Portfolio](https://github.com/shahm-1)** • **[Threat Hunting Portfolio](https://github.com/shahm-1/Threat-Hunting-Portfolio)** • **[Vulnerability Management](https://github.com/shahm-1/Vulnerability-Management-Portfolio)**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/shahzebmasroor)

---

> *These labs are my proving ground for security concepts. Everything I've learned about enterprise security started here.*
