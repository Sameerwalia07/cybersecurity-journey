# TryHackMe — Pyramid of Pain

**Path:** SOC Level 1 — Module 4: Cyber Defence Frameworks
**Date completed:** [18/07/2026]
**Room link:** [https://tryhackme.com/room/pyramidofpainax]

---

## 🎯 What I Learned

- What the Pyramid of Pain is and why it matters for CTI, threat hunting,
  and incident response
- The six levels of the pyramid, from trivial to tough for an attacker to
  change
- What kind of indicator sits at each level, with real examples
- Why detecting higher levels (especially TTPs) causes attackers the most
  disruption

## 🧠 In My Own Words

The **Pyramid of Pain** is a well-known concept applied across the
industry (Cisco Security, SentinelOne, SOCRadar) to improve **CTI (Cyber
Threat Intelligence)**, threat hunting, and incident response. It's built
around one core idea: **not all indicators of compromise are equally
valuable** — some are trivial for an attacker to change, while others force
them to rebuild their entire operation from scratch. The higher up the
pyramid you can detect and disrupt, the more "pain" you inflict on the
attacker.

### 1. Hash Values — *Trivial*

A **hash value** is a fixed-length numeric value that uniquely identifies
data, produced by a hashing algorithm. Common algorithms:
- **MD5** — 128-bit hash, designed in 1992; no longer cryptographically
  secure (collision attacks documented in RFC 6151)
- **SHA-1** — 160-bit hash; deprecated by NIST in 2011, banned for digital
  signatures by 2013 due to brute-force vulnerability
- **SHA-2 (e.g. SHA-256)** — 256-bit hash, designed by NIST/NSA to replace
  SHA-1, currently the recommended standard

Security professionals use hashes to uniquely reference a specific
malicious file. **Example:** flagging a known ransomware sample by its
SHA-256 hash. The problem: an attacker only needs to change **a single bit**
of the file to produce a completely different hash — making file-hash-based
detection trivially easy to evade at scale.

### 2. IP Addresses — *Easy*

IP addresses identify devices on a network (represented by **green** in
the pyramid). Blocking a known malicious IP at the firewall is a common
defence, but it's not bulletproof — an experienced attacker can simply
switch to a new public IP.

**Example technique — Fast Flux:** a DNS technique used by botnets to hide
phishing, malware delivery, or C2 communication behind constantly rotating
compromised host IPs tied to a single domain, making IP blocking largely
ineffective against it.

### 3. Domain Names — *Simple*

Domains (teal in the pyramid) map to IP addresses via a text string (e.g.
`evilcorp.com`, or a subdomain like `tryhackme.evilcorp.com`). Changing a
domain is more of a hassle for attackers than switching an IP — they need
to purchase, register, and configure DNS records — but loose registrar
standards and easy APIs still make this fairly quick to do.

**Example:** blocking a known malicious domain used for C2 communication.
**Punycode** is a related technique — converting non-ASCII characters into
ASCII-compatible encoding, sometimes abused to create deceptive
look-alike domains.

### 4. Host & Network Artifacts — *Annoying*

Both sit in the **yellow zone** — detecting these forces an attacker to
actually go back and change tools/methods, costing real time and
resources.

- **Host artifacts** — traces left on a system: registry values,
  suspicious process execution, dropped files, or other IOCs.
  *Example:* a malicious registry run-key added for persistence.
- **Network artifacts** — patterns in network traffic: unusual
  **User-Agent strings**, C2 beacon patterns, or suspicious URI patterns in
  HTTP POST requests. *Example:* spotting an unfamiliar User-Agent string in
  Wireshark/TShark packet captures, or via Snort IDS alerts.

### 5. Tools — *Challenging*

At this level, detecting and blocking the attacker's actual **tools**
(maldoc builders, backdoors, custom EXEs/DLLs, password crackers) often
means the attacker gives up or has to build/acquire an entirely new tool —
a real investment of money, time, or training.

**Detection resources:**
- **MalwareBazaar** and **Malshare** — malware sample/feed repositories
- **SOC Prime Threat Detection Marketplace** — shared detection rules,
  including for newly exploited CVEs
- **Fuzzy hashing (e.g. SSDeep)** — matches files with only minor
  differences via similarity analysis, defeating attempts to evade
  detection through small file tweaks

**Example:** using a YARA rule to detect a specific malicious macro-loader
pattern regardless of the exact file hash.

### 6. TTPs (Tactics, Techniques, Procedures) — *Tough*

The **apex** of the pyramid. TTPs cover the entire **MITRE ATT&CK Matrix**
— the full range of steps an adversary takes from initial phishing through
persistence and data exfiltration. Detecting and responding to TTPs quickly
leaves attackers almost no room to adapt.

**Example:** detecting a **Pass-the-Hash** attack via Windows Event Log
monitoring lets defenders identify the compromised host and stop lateral
movement almost immediately. At this point the attacker has only two
options:
1. Retreat, retrain, and rebuild their entire toolkit/approach
2. Give up and move on to an easier target

Option 2 is by far the more likely outcome — which is exactly why TTP-level
detection is the most valuable (and hardest to achieve) goal for a SOC.

## 🛠️ Key Terms Introduced

- Pyramid of Pain (6 levels: Hash Values, IP Addresses, Domain Names, Host
  Artifacts, Network Artifacts, Tools, TTPs)
- Fast Flux, Punycode
- YARA rules, Fuzzy hashing (SSDeep)
- MITRE ATT&CK, Pass-the-Hash

## ❓ Questions I Had / Things to Revisit

- Want to actually try writing a simple YARA rule myself against a sample
  file
- Curious how a real SOC decides where to invest detection effort — is it
  realistic to aim for TTP-level detection on everything, or is a layered
  approach (catching some threats at IP/domain level too) more practical?
- Want to look at a real MITRE ATT&CK technique page end to end to see how
  TTP-level detail is documented

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can walk
through all six levels with examples and explain why TTP-level detection
causes attackers the most disruption.

---

*This is a genuinely foundational mental model for prioritising detection
work — I want to keep this pyramid in mind going forward, especially when
building or evaluating detection rules, since chasing hash-level IOCs alone
is clearly a losing game long-term.*
