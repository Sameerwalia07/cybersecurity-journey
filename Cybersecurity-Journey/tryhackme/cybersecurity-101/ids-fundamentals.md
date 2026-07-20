# TryHackMe — IDS Fundamentals

**Path:** Cyber Security 101
**Date completed:** [18/06/2026]
**Room link:** https://tryhackme.com/room/idsfundamentals

---

## 🎯 What I Learned

- Why an IDS is needed even when a firewall is in place
- Deployment modes: HIDS vs NIDS
- Detection modes: signature-based, anomaly-based, hybrid
- Snort as a real-world IDS example, and its three operating modes
- The structure of a Snort rule
- Basics of rule creation, testing, and running Snort against pcap files

## 🧠 In My Own Words

Even if an attacker manages to bypass a firewall — for example, by using a
connection that looks legitimate on the surface — they can still end up
performing malicious activity **inside** the network. This is exactly the
gap an **Intrusion Detection System (IDS)** fills: it's a security solution
placed inside the network specifically to detect that kind of activity in a
timely manner, catching what the firewall alone might miss.

**Deployment modes:**
- **HIDS (Host Intrusion Detection System)** — deployed on an individual
  host/system, monitoring activity on that specific device
- **NIDS (Network Intrusion Detection System)** — deployed at the network
  level, monitoring traffic across the network as a whole

**Detection modes:**
- **Signature-based IDS** — detects threats by matching traffic against
  known attack patterns (signatures)
- **Anomaly-based IDS** — detects threats by identifying behaviour that
  deviates from an established baseline of "normal"
- **Hybrid IDS** — combines both approaches for broader coverage

**Snort** is one of the most widely used open-source IDS solutions,
originally developed in 1998. It uses both signature-based and
anomaly-based detection to identify known threats, with detection logic
defined in **rule files**.

**Snort's three modes:**
1. **Packet Sniffer mode** — reads and displays network packets without
   performing any detection/analysis. Not really an IDS function on its
   own, but useful for troubleshooting network issues (e.g. diagnosing
   performance problems by observing raw traffic flow)
2. **Packet Logging mode** — logs network traffic to a **PCAP** file for
   later analysis, including any detections. Useful for forensic
   investigators doing root cause analysis after an attack
3. **NIDS mode** — Snort's primary mode; monitors traffic in real time and
   applies rule files to match known attack patterns, generating an alert
   whenever a match occurs. This is the core IDS functionality.

## 🛠️ Snort Rule Format

A Snort rule is built from these components:

| Component | Purpose |
|---|---|
| **Action** | What Snort does on a match (e.g. `alert`, `log`, `pass`) |
| **Protocol** | The protocol to inspect (e.g. `tcp`, `udp`, `icmp`) |
| **Source IP** | The traffic's source address to match |
| **Source Port** | The traffic's source port to match |
| **Destination IP** | The traffic's destination address to match |
| **Destination Port** | The traffic's destination port to match |
| **Rule metadata** | Additional rule information/options |
| **Message** | A human-readable description shown when the rule triggers |
| **Signature ID (SID)** | A unique ID identifying this specific rule |
| **Rule Revision** | The version number of the rule, incremented on updates |

**Example rule I built to map against this format:**

```
alert tcp any any -> 192.168.1.10 22 (msg:"Possible SSH brute force attempt"; sid:1000001; rev:1;)
```

Breaking this down against the format above:
- **Action:** `alert` — generate an alert if this rule matches
- **Protocol:** `tcp` — inspecting TCP traffic
- **Source IP / Port:** `any any` — from any source address, any source port
- **Destination IP / Port:** `192.168.1.10 22` — targeting this specific
  host on port 22 (SSH)
- **Message:** `"Possible SSH brute force attempt"` — the description shown
  when this rule fires
- **Signature ID:** `sid:1000001` — a unique identifier for this custom rule
- **Rule Revision:** `rev:1` — first version of this rule

The room finished with practical **rule creation and testing**, and running
Snort against **pcap files** to detect matches within previously captured
traffic rather than only live traffic.

## ❓ Questions I Had / Things to Revisit

- Want more practice writing rules for different attack types beyond just
  SSH brute force (e.g. detecting a specific malware signature)
- Curious how a real production environment tunes anomaly-based detection
  to avoid excessive false positives
- Want to understand how IDS alerts specifically get forwarded into a SIEM
  for centralised correlation

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
IDS deployment/detection modes, Snort's three modes, and break down a rule's
components confidently, including writing a basic rule myself.

---

*This is a natural next step after Firewall Fundamentals — firewalls block
based on rules at the edge, while an IDS like Snort watches for what gets
through or happens internally. Want to actually install Snort in my home
lab and test it against sample malicious traffic next.*
