# TryHackMe — Introduction to SOAR

**Path:** SOC Level 1 — Module 3: Core SOC Solutions
**Date completed:** [17/07/2026]
**Room link:** [https://tryhackme.com/room/soar]

---

## 🎯 What I Learned

- The key capabilities of a traditional SOC.
- The core challenges traditional SOCs face.
- What SOAR is and how it solves those challenges.
- SOAR's three core capabilities: Orchestration, Automation, Response.
- Why SOAR doesn't replace SOC analysts.
- What playbooks look like in practice, using Phishing and CVE Patching
  examples.

## 🧠 In My Own Words

A SOC relies on multiple tools (SIEM, EDR, firewalls, threat intelligence)
and constant communication with IT/management. As threats grow more
complex, SOC teams increasingly struggle with **alert fatigue, manual
processes, disconnected tools, and cross-team communication** — this is
exactly the gap **SOAR** is designed to close.

### Key SOC Capabilities

- **Monitoring and Detection** — continuously scanning for suspicious
  activity, mainly via SIEM (e.g. flagging repeated failed logins or a
  login from an unfamiliar location)
- **Recovery and Remediation** — acting as first responders once a threat
  is identified: isolating endpoints, removing malware, stopping malicious
  processes, often using EDR, firewalls, or IAM tools
- **Threat Intelligence** — maintaining a continuous flow of up-to-date
  threat data (IPs, hashes, domains) to inform detection and blocking
- **Communication** — coordinating with IT and management to ensure
  incidents are properly addressed (e.g. opening a ticket for IT to verify
  a recent patch)

### Challenges SOC Teams Face

- **Alert Fatigue** — too many alerts, many false positives or low-value,
  overwhelming analysts
- **Too Many Disconnected Tools** — tools deployed without integration,
  forcing analysts to manually navigate between separate systems
- **Manual Processes** — undocumented investigation procedures relying on
  "tribal knowledge" from experienced analysts, slowing response times
- **Talent Shortage** — difficulty recruiting/scaling skilled analysts fast
  enough to match a growing, increasingly sophisticated threat landscape

### What is SOAR?

**Security Orchestration, Automation, and Response (SOAR)** is a tool that
**unifies** all the security tools a SOC uses — instead of switching
between SIEM, EDR, firewall, and other tools separately, analysts operate
everything from a single SOAR interface. It also adds ticketing and case
management, so incidents can be documented, tracked, and resolved in a
structured way.

### SOAR's Three Core Capabilities

**1. Orchestration** — traditionally, investigating something like a VPN
brute force means manually switching between:
1. SIEM — check if the user's IP is typical for them
2. Threat Intelligence — verify the IP's reputation
3. IAM — disable the user if a successful login attempt occurred
4. Ticketing system — open and track the incident

Orchestration solves this by connecting all these tools inside one unified
SOAR interface, using **Playbooks** — predefined workflows that define how
to investigate a specific type of alert.

**2. Automation** — the playbook logic from Orchestration can be
**automated entirely**, meaning SOAR executes the steps itself without
requiring manual clicks from an analyst.

**3. Response** — SOAR can take real actions across multiple tools from one
place, and (combined with Automation) can fully execute a response — e.g.
for a VPN brute force playbook: block the IP on the firewall, disable the
user in IAM, and open a ticket with full details, all without manual
intervention.

### Do We Still Need SOC Analysts?

Yes — SOAR automates repetitive tasks, but it **doesn't replace analysts**.
Complex investigations still require human judgement, especially at
critical decision points SOAR can't make a call on. Analysts also
understand the broader **business context** behind a threat, and they're
the ones who actually **design the playbooks** SOAR follows in the first
place. SOAR eases the burden and organises the work — it doesn't eliminate
the need for skilled analysts.

### Playbooks in Practice

**Phishing Playbook** — phishing remains the most common attack vector, but
investigating it (analysing attachments/URLs, checking threat intel) is
time-consuming and manual. A playbook automates this in the background.
The logical flow looks roughly like:
- Alert: "Suspicious email received" → create a ticket
- Does it contain a URL or attachment?
  - **No** → notify the user, close out
  - **Yes** → branch further based on whether it's a URL or an attachment,
    running the appropriate analysis/remediation steps for each

This is essentially a structured chain of **"if this happens, do this;
else, do that"** logic — which is what makes a playbook buildable and
repeatable rather than relying on an analyst's memory each time.

**CVE Patching Playbook** — CVEs are disclosed constantly, and manually
tracking, verifying, and patching each one can quickly overwhelm a SOC
team, leading to a growing backlog and unpatched systems. A CVE Patching
playbook automates this by: analysing the CVE's details, assessing its risk
threshold, creating a patching ticket, and testing the patch before it goes
to production.

## 🛠️ Key Terms Introduced

- SOAR (Security Orchestration, Automation, and Response)
- Orchestration, Automation, Response (SOAR's three capabilities)
- Playbook
- Alert fatigue

## ❓ Questions I Had / Things to Revisit

- Want to actually build a simple playbook flowchart myself (like the
  phishing example) for a different scenario, e.g. unusual login location
- Curious how much playbook-building is realistically part of an L1 role
  vs something reserved for L2/engineers
- Want to look at a real SOAR tool's interface (Splunk SOAR or Cortex XSOAR)
  to see what building/running a playbook actually looks like hands-on

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
SOAR's three core capabilities, why analysts are still needed, and walk
through both the phishing and CVE patching playbook examples confidently.

---

*This wraps up Module 3 nicely — EDR, SIEM/Elastic, and SOAR together form
the core toolchain of a modern SOC: EDR and SIEM detect and provide
visibility, while SOAR ties everything together and automates the
repetitive parts of the response. Good full picture of "Core SOC
Solutions."*
