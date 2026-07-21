# TryHackMe — SOC Role in Blue Team

**Path:** SOC Level 1 — Module 1: Blue Team Introduction
**Date completed:** [11/07/2026]
**Room link:** [https://tryhackme.com/room/socroleinblueteam]

---

## 🎯 What I Learned

- How security priorities and team structure differ by company/industry
- The typical security hierarchy, from executives down to technical roles
- The main security departments: Red Team, GRC, Blue Team
- The structure within an efficient SOC
- What a CIRT/CSIRT is and when it gets involved
- Specialised defensive roles beyond the core SOC
- The difference between running security in-house vs using an MSSP

## 🧠 In My Own Words

Cybersecurity priorities aren't the same for every company — a law firm
cares most about the **privacy** of legal documents, a factory cares about
the **availability** of production lines, and a hospital cares most about
**patient safety**. Because of this, every company builds a security
approach and team structure suited to its own priorities.

### The typical security hierarchy

1. **Executives (CEO/CFO/Owner)** — focused on global business objectives
2. **Security Leadership (CTO/CIO/CISO)** — lead company-wide IT or security
   programs
3. **Security Managers (Team Lead/SOC Manager)** — manage a single team or
   department
4. **Technical roles (Analyst/Engineer)** — perform the actual hands-on
   technical work, e.g. SOC Analysts, GRC Engineers, SOC Engineers

### The three main security departments

- **Red Team** — offensive security experts, pentesters, and ethical
  hackers who actively look for security issues before attackers do
- **GRC Team** (Governance, Risk, and Compliance) — specialists managing
  policy and ensuring compliance with regulations (e.g. PCI DSS)
- **Blue Team** — defensive security experts (SOC analysts, engineers,
  incident responders) who constantly monitor for attacks and respond
  quickly. Depending on company size/sector, a Blue Team can range from
  **3 to 50 members**, made up of several sub-departments.

### Common SOC roles within the Blue Team

- **L1 Analysts** — junior members who triage alerts and escalate complex
  cases to L2
- **L2 Analysts** — experienced members who investigate more advanced
  attacks
- **Engineers** — experts in configuring security tools like EDR or SIEM
- **Manager** — manages the whole SOC team

### CIRT / CSIRT / CERT

When a SOC's expertise isn't enough, or an incident spirals out of control,
the **Cyber Incident Response Team (CIRT)** — also called **CSIRT** or
**CERT** — gets called in as the "firefighters." Members need broad
knowledge of cyber threats and must be able to handle breaches without
relying heavily on tools like EDR or SIEM. It's a high-stress but highly
rewarding role. Real examples include:
- **JPCERT** — Japan's national CERT, handling nationwide breaches
- **Mandiant** — a private team responding to global cyber incidents
- **AWS CIRT** — investigates security incidents for AWS customers

### Specialised defensive roles beyond core SOC

- **Digital Forensics Analyst** — uncovers hidden threats in disk and
  memory
- **Threat Intelligence Analyst** — gathers data on emerging threat groups
- **AppSec Engineer** — maintains a secure software development lifecycle
- **AI Researcher** — studies AI-specific threats and defences against them

### Internal SOC vs MSSP

Not every organisation has the in-house expertise to run its own SOC, so
many rely on an **MSSP (Managed Security Services Provider)** — a company
that delivers outsourced security services, most commonly SOC functions, to
clients. Working at an MSSP is typically high-pressure, but it's also a
strong way to **quickly kickstart a career** in the field, given the volume
and variety of exposure it offers.

## 🛠️ Key Terms Introduced

- Red Team, GRC Team, Blue Team
- L1/L2 Analyst, SOC Engineer, SOC Manager
- CIRT / CSIRT / CERT
- Digital Forensics Analyst, Threat Intelligence Analyst, AppSec Engineer,
  AI Researcher
- MSSP (Managed Security Services Provider)

## ❓ Questions I Had / Things to Revisit

- Want to understand more concretely what triggers a SOC to escalate to
  CIRT rather than handling an incident internally
- Curious whether starting at an MSSP vs an internal company SOC makes a
  real difference for someone breaking into the field — worth researching
  as I get closer to job hunting
- Want to look into GRC a bit more, since it's mentioned as a separate
  department but I don't yet have a clear picture of the day-to-day work

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I understand
the hierarchy, the three main departments, SOC's internal structure, and
where CIRT and MSSPs fit into the bigger picture.

---

*This builds well on Junior Security Analyst Intro — now I can see exactly
where the L1 role I'm aiming for sits within the much bigger security
organisation, and what paths (L2, engineer, CIRT, specialised roles) could
open up from there later.*
