# TryHackMe — Unified Kill Chain

**Path:** SOC Level 1 — Module 4: Cyber Defence Frameworks
**Date completed:** [20/07/2026]
**Room link:** [https://tryhackme.com/room/unifiedkillchain]

---

## 🎯 What I Learned

- What threat modelling is and how the UKC supports it
- How the Unified Kill Chain (UKC) differs from Lockheed Martin's Cyber
  Kill Chain and MITRE ATT&CK — complementing rather than competing
- The three high-level goals of the UKC: **In, Through, Out**
- The individual phases within each goal, mapped to MITRE Tactics
- How persistence, defence evasion, and pivoting fit into the bigger
  picture

## 🧠 In My Own Words

A **"Kill Chain"** — originally a military term — describes the stages of
an attack. In cybersecurity, it maps the path an attacker takes to
approach and intrude a target (e.g. scanning → exploiting a vulnerability
→ escalating privileges). Understanding this path lets defenders build
proactive protections or disrupt an attack mid-progress.

### Threat Modelling

**Threat modelling** is the broader practice of improving a system's
security by:
1. Identifying which systems/applications need securing and their
   function/criticality
2. Assessing their vulnerabilities and how they could be exploited
3. Creating a plan to secure them
4. Implementing policies to prevent recurrence (e.g. SDLC processes,
   phishing awareness training)

The UKC supports threat modelling by helping identify potential attack
surfaces and how they might be exploited. Other threat modelling
frameworks include **STRIDE, DREAD, and CVSS**.

### The Unified Kill Chain (UKC)

Published by **Paul Pols in 2017**, the UKC is designed to **complement**
(not replace) other kill chain frameworks like Lockheed Martin's and
MITRE ATT&CK. Its key advantage: it's far more detailed, defining **18
phases** total (vs. the smaller handful in other frameworks), grouped here
into three overarching goals: **In, Through, Out.**

---

### Goal: In (Initial Foothold)

The attacker's aim here is simply **gaining access** to a system or
network, using techniques like reconnaissance to discover potential attack
vectors.

- **Reconnaissance (TA0043)** — gathering info about the target: running
  systems/services, employee contact lists (for social
  engineering/phishing), potential credentials, and network topology —
  all of which feeds into later phases
- **Weaponization (TA0001)** — setting up necessary attack infrastructure,
  e.g. a C2 server or a system to catch reverse shells and deliver payloads
- **Social Engineering (TA0001)** — manipulating employees into helping
  the attack, e.g. opening a malicious phishing attachment, entering
  credentials on a fake login page, or impersonating someone (a utility
  engineer, a user requesting a password reset) to gain physical or
  account access
- **Exploitation (TA0002)** — abusing a vulnerability to achieve code
  execution, e.g. uploading a reverse shell to a web app, interfering with
  an automated script, or exploiting a web app vulnerability directly
- **Persistence (TA0003)** — maintaining access to the initial foothold:
  creating a service for regain-access purposes, registering the system
  with a C2 server, or leaving conditional backdoors (e.g. triggering when
  an admin logs in)
- **Defence Evasion (TA0005)** — evading defensive measures like WAFs,
  network firewalls, antivirus, or IDS. This phase is especially valuable
  for defenders to study, since it directly informs how to improve future
  defences
- **Command & Control (TA0011)** — establishing the actual communication
  channel (building on Weaponization) to execute commands, steal data, or
  use the compromised system as a pivot point
- **Pivoting (TA0008)** — using an accessible system (e.g. a public-facing
  web server) as a stepping stone to reach otherwise-inaccessible internal
  systems, which often hold valuable data or weaker security

---

### Goal: Through (Network Propagation)

Once a foothold is established, if defences block the original objective,
the attacker pivots and expands access across the network:

- **Discovery (TA0007)** — mapping out the environment: active accounts,
  permissions, installed applications, browser activity, files/shares,
  and system configuration
- **Privilege Escalation (TA0004)** — using discovered info to escalate
  to a higher access level: SYSTEM/ROOT, Local Administrator, an
  admin-like account, or an account with specific valuable access
- **Execution (TA0002)** — deploying malicious code from the pivot system:
  remote trojans, C2 scripts, malicious links, or scheduled tasks, to
  maintain a recurring presence
- **Credential Access (TA0006)** — stealing account names/passwords via
  keylogging or credential dumping, working alongside Privilege
  Escalation — using legitimate credentials makes detection much harder
- **Lateral Movement (TA0008)** — using the escalated privileges and
  stolen credentials to move to other systems, ideally as stealthily as
  possible

---

### Goal: Out (Action on Objectives)

The final stage — the attacker now has access to critical assets and
pursues their actual goal, generally targeting the **CIA triad**:

- **Collection (TA0009)** — gathering valuable data of interest (drives,
  browsers, audio, video, email), compromising **confidentiality**
- **Exfiltration (TA0010)** — stealing the collected data, typically
  encrypted/compressed to avoid detection, often using the C2
  channel/tunnel set up earlier
- **Impact (TA0040)** — compromising **integrity and availability**:
  manipulating, interrupting, or destroying assets — removing account
  access, wiping disks, deploying ransomware, defacement, or DoS attacks
- **Objectives** — the attacker's ultimate strategic goal, e.g. financial
  gain via ransomware, or reputational damage via public data leaks

## 🛠️ Key Terms Introduced

- Threat modelling; STRIDE, DREAD, CVSS
- UKC goals: In, Through, Out
- MITRE Tactics: TA0043, TA0001, TA0002, TA0003, TA0005, TA0011, TA0008,
  TA0007, TA0004, TA0006, TA0009, TA0010, TA0040

## ❓ Questions I Had / Things to Revisit

- Want to compare the UKC's 18 phases side by side with the Cyber Kill
  Chain's 7 phases to see exactly where they overlap vs where UKC adds
  more granularity
- Curious how STRIDE or DREAD actually work in practice — want to look at
  one of them in more depth
- Want to practice mapping a real (or simulated) incident to UKC's In/
  Through/Out structure, to test how well I can classify each stage

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can
explain the three high-level goals, walk through each phase within them,
and connect several to their MITRE Tactic IDs.

---

*This complements the Cyber Kill Chain room nicely — where the Lockheed
Martin model gives 7 broad phases, the UKC breaks "Through" into much finer
detail (Discovery → Privilege Escalation → Execution → Credential Access →
Lateral Movement), which maps very directly onto what a SOC analyst
actually investigates once an attacker is already inside the network.*
