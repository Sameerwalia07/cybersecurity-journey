# TryHackMe — SOC Fundamentals

**Path:** Cyber Security 101
**Date completed:** [15/06/2026]
**Room link:** https://tryhackme.com/room/socfundamentals

---

## 🎯 What I Learned

- What a SOC is and its core purpose
- The categories of activity a SOC is focused on detecting
- The three pillars a SOC is built on: People, Process, Technology
- Common SOC roles and how responsibilities are split across tiers
- What alert triage is, and the "5 Ws" framework used to investigate an alert

## 🧠 In My Own Words

A **Security Operations Centre (SOC)** is a dedicated facility operated by a
security team whose job is to **continuously monitor** a company's network
and resources for anything suspicious, aiming to catch issues before they
cause real damage. The main focus is **detection and response, as fast as
possible** — the faster a threat is caught and acted on, the less damage it
can do.

Specifically, a SOC is focused on detecting:
- **Vulnerabilities** — weaknesses that could be exploited
- **Unauthorized activity** — access or actions that shouldn't be happening
- **Intrusions** — active breaches or attacker presence
- **Policy violations** — internal rule-breaking that could introduce risk

On the response side, the SOC works closely with **incident response** to
actually act on what's been detected.

**The three pillars of a SOC:**
1. **People** — the humans who interpret what security tools flag, decide
   which alerts represent genuine threats, and enable a fast, correct
   response. This includes roles like:
   - SOC Analyst Level 1 (SOC L1)
   - SOC Analyst Level 2 (SOC L2)
   - SOC Analyst Level 3 (SOC L3)
   - SOC Engineer
   - SOC Manager
   - CISO (Chief Information Security Officer)
   - Security Engineer
   - Detection Engineer

   Each of these roles has its own responsibilities and processes — for
   example, L1 typically handles initial triage, while L3 handles deeper
   investigation and more complex threats.

2. **Process** — the defined workflows the team follows, with **alert
   triage** being the foundation of SOC work. Triage is the *first* response
   to any alert, where an analyst determines whether it's a real threat and
   how urgent it is. A useful framework for this investigation is the
   **5 Ws**:
   - **What** happened?
   - **When** did it happen?
   - **Where** did it happen?
   - **Who** was involved?
   - **Why** did it happen?

3. **Technology** — the actual security tools that make detection and
   response possible, including:
   - **SIEM** (Security Information and Event Management) — aggregates and
     analyses logs/events across the environment
   - **EDR** (Endpoint Detection and Response) — monitors and responds to
     threats at the device/endpoint level
   - **Firewalls** — control and filter network traffic based on rules

## 🛠️ Key Terms Introduced

- SOC (Security Operations Centre)
- Three pillars: People, Process, Technology
- SOC tiers: L1, L2, L3, SOC Engineer, SOC Manager, CISO, Security Engineer,
  Detection Engineer
- Alert triage
- The 5 Ws (What, When, Where, Who, Why)
- SIEM, EDR, Firewalls

## ❓ Questions I Had / Things to Revisit

- Want to understand exactly where the line is between L1 and L2 work — at
  what point does an L1 analyst escalate an alert rather than handle it
  themselves?
- Curious how the 5 Ws framework looks in practice against a real alert —
  want to try applying it to a sample alert once I start hands-on SOC labs
- Want to explore how SIEM and EDR data actually feed into each other during
  an investigation

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
the SOC's purpose, the three pillars, the role hierarchy, and the 5 Ws
triage framework confidently.

---

*This is probably the most directly relevant room to my goal so far — SOC
L1 is exactly the entry point I'm aiming for, and the 5 Ws framework feels
like something I'll want to practically apply the moment I start working
with real alerts in a SIEM.*
