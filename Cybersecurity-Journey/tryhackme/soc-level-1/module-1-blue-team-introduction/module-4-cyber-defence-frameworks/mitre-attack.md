# TryHackMe — MITRE ATT&CK

**Path:** SOC Level 1 — Module 4: Cyber Defence Frameworks
**Date completed:** [21/07/2026]
**Room link:** [https://tryhackme.com/room/mitre]

---

## 🎯 What I Learned

- What MITRE is and its broader mission beyond cybersecurity
- The MITRE ATT&CK framework: Tactics, Techniques, Procedures (TTPs)
- How the ATT&CK Matrix and Navigator visualise this data
- Why ATT&CK matters for standardising communication and bridging threat
  intel with actual detection
- The Cyber Analytics Repository (CAR) — ready-made detections built on
  ATT&CK
- The MITRE D3FEND framework — the defensive counterpart to ATT&CK

## 🧠 In My Own Words

**MITRE** is a not-for-profit organisation conducting research across
cybersecurity, AI, healthcare, and space systems, all in service of its
mission "to solve problems for a safer world." Within cybersecurity, MITRE
produces several frameworks that have become foundational for both red and
blue teams: **ATT&CK, CAR, D3FEND, and Engage.**

### The ATT&CK Framework

**MITRE ATT&CK®** is a globally accessible knowledge base of adversary
tactics and techniques, based on **real-world observations**. Created in
2013 to document and categorise the standard TTPs used by APT groups, it
breaks attacker behaviour into three parts:

- **Tactic** — the adversary's goal ("why") — e.g. Reconnaissance
- **Technique** — how they achieve that goal — e.g. Active Scanning
- **Procedure** — the specific implementation of the technique in practice

### The ATT&CK Matrix

The **ATT&CK Matrix** visually represents all tactics and techniques —
tactics run across the top, with techniques (and expandable
sub-techniques) nested underneath. The **ATT&CK Navigator** is a tool for
annotating and exploring the matrix interactively.

**Worked example of the Tactic → Technique → Sub-technique hierarchy:**
1. **Tactic:** Reconnaissance (the attacker's goal)
2. **Technique:** Active Scanning (how they pursue that goal)
3. **Sub-techniques:** Active Scanning breaks down further into Scanning
   IP Blocks, Vulnerability Scanning, or Wordlist Scanning

### Why ATT&CK Matters

ATT&CK provides a **standard, consistent language** for describing
adversary behaviour — solving the common problem where the same technique
gets referred to by different names across reports and tools. Standard
terminology and unique IDs make it far easier to compare data across
incidents and communicate clearly across the security community.

It also **bridges threat intelligence and defensive operations**: a raw
threat report might describe *what* an attacker did without explaining how
to turn that into a usable detection. Mapping activity to ATT&CK TTPs lets
defenders translate intelligence directly into detection logic, SIEM
queries, and playbooks.

### Guide: Using ATT&CK in Practice

Here's a walkthrough of how an analyst might actually use ATT&CK during an
investigation:

1. **Start with an observed behaviour** — e.g. a SIEM alert shows a user's
   PowerShell process making an outbound HTTPS connection to an unfamiliar
   IP shortly after opening an email attachment
2. **Identify the likely Tactic** — this behaviour suggests **Execution**
   (TA0002), since code just ran on the host
3. **Narrow to the Technique** — searching the ATT&CK Matrix for
   "PowerShell" surfaces **T1059.001 (Command and Scripting Interpreter:
   PowerShell)**
4. **Check the technique page** — ATT&CK's page for T1059.001 lists real
   procedure examples (which known APT groups have used PowerShell this
   way), detection guidance, and related mitigations
5. **Use the ID to search for detections** — with the technique ID
   (T1059.001) in hand, the analyst can search MITRE **CAR** or their
   organisation's own detection rule library for a matching analytic
6. **Document the finding using the ID** — instead of writing "suspicious
   PowerShell activity" in a report, the analyst writes "activity
   consistent with T1059.001," which any other analyst or team
   (internally or externally) can immediately understand precisely

**Threat Intelligence Example:**
A threat intel report states that a specific ransomware group "gains
initial access via phishing emails with malicious macros, then uses
PowerShell to download a second-stage payload, followed by credential
dumping via LSASS memory access before spreading via SMB." A defender can
translate this narrative directly into ATT&CK IDs:
- Initial Access → **T1566 (Phishing)**
- Execution → **T1059.001 (PowerShell)**
- Credential Access → **T1003.001 (LSASS Memory)**
- Lateral Movement → **T1021.002 (SMB/Windows Admin Shares)**

With this mapping, the defender can now go build (or search CAR for) four
specific detection rules — one per technique — rather than trying to guess
what "detect ransomware" should actually look like technically.

### Cyber Analytics Repository (CAR)

**CAR** is MITRE's knowledge base of **ready-made detection analytics**
built directly on the ATT&CK model. Each analytic explains how to detect a
specific adversary behaviour, including the **operating theory and
rationale** behind it — not just a rule, but the reasoning for why it
works. CAR analytics often include:
- **Pseudocode** — a plain, human-readable description of the detection
  logic
- **Tool-specific implementations** — e.g. an actual Splunk query or
  LogPoint search
- **Unit Tests** (for some analytics) — letting an analyst validate that
  the detection actually works as intended

This effectively closes the gap between "here's the ATT&CK technique" and
"here's the actual SIEM query to detect it."

### MITRE D3FEND Framework

**D3FEND (Detection, Denial, and Disruption Framework Empowering Network
Defense)** is the defensive counterpart to ATT&CK — mapping out defensive
techniques with a shared vocabulary for describing how security controls
actually work. Its matrix is organised into **7 tactics**:
1. Model
2. Harden
3. Detect
4. Isolate
5. Deceive
6. Evict
7. Restore

**Worked example — Credential Rotation (D3-CRO):**
This D3FEND technique falls under the "Harden" tactic and recommends
**regularly rotating passwords** to prevent attackers from reusing stolen
credentials. D3FEND's page for this technique explains:
- **How the defence works** — regularly invalidating old credentials
  reduces the window in which a stolen password remains useful
- **Implementation considerations** — e.g. rotation frequency, exemptions
  for service accounts, user experience trade-offs
- **Related ATT&CK techniques** — this defence directly counters
  **T1078 (Valid Accounts)** and reduces the value of **T1003 (OS
  Credential Dumping)**, since dumped credentials become useless sooner

This is what makes D3FEND powerful paired with ATT&CK: for a given attacker
technique, you can look up the specific defensive countermeasure(s) that
directly address it, seeing both the **offensive move and the defensive
response** side by side.

## 🛠️ Key Terms Introduced

- MITRE ATT&CK, Tactic/Technique/Procedure (TTP)
- ATT&CK Matrix, ATT&CK Navigator
- CAR (Cyber Analytics Repository)
- D3FEND (7 tactics: Model, Harden, Detect, Isolate, Deceive, Evict, Restore)
- MITRE Engage (mentioned, adversary engagement framework)

## ❓ Questions I Had / Things to Revisit

- Want to explore the ATT&CK Navigator hands-on, building a simple
  annotated matrix for a specific threat actor
- Want to look up a few more CAR analytics and actually run one of the
  example Splunk queries against sample data
- Curious how MITRE Engage (deception/adversary engagement) fits alongside
  ATT&CK and D3FEND — want to explore this framework next

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can walk
through the Tactic/Technique/Sub-technique hierarchy, explain how ATT&CK
bridges threat intel and detection, and connect a D3FEND defence back to
the ATT&CK technique it counters.

---

*This ties together everything from this module — the Pyramid of Pain
argued TTPs are the most valuable thing to detect, the Kill Chain and UKC
showed the attacker's actual path, and ATT&CK/D3FEND now give the precise,
standardised vocabulary and ready-made detections to act on all of that in
a real SOC. Strong finish to Module 4.*
