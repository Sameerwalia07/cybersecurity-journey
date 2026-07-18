# TryHackMe — Firewall Fundamentals

**Path:** Cyber Security 101
**Date completed:** [17/06/2026]
**Room link:** https://tryhackme.com/room/firewallfundamentals

---

## 🎯 What I Learned

- What a firewall is and its core purpose
- The four main types of firewalls and their characteristics
- The basic components that make up a firewall rule
- Rule directionality (inbound, outbound, forward)
- How Windows Defender Firewall works and how to create custom rules
- Common Linux firewall tools

## 🧠 In My Own Words

A **firewall** is designed to monitor the **incoming and outgoing traffic**
of a network or device, with the core goal of preventing any unauthorized
visitor from entering a system or network. You control a firewall's
behaviour by giving it **rules** to check all traffic against — anything
entering or leaving a device/network faces the firewall first, and the
firewall then **allows or denies** that traffic based on its rules. Modern
firewalls go well beyond simple rule-based filtering, offering extra
protective functionality against outside threats.

**Types of firewalls:**

| Type | Key Characteristics |
|---|---|
| **Stateless** | Basic filtering; no memory of previous connections; efficient for high-speed networks |
| **Stateful (Stateful Inspection)** | Recognises traffic by patterns; supports complex rules; actively monitors network connections |
| **Proxy** | Inspects data *inside* packets; offers content filtering and application control; decrypts and inspects SSL/TLS traffic |
| **Next-Generation (NGFW)** | Provides advanced threat protection; includes an intrusion prevention system; detects anomalies via heuristic analysis; also decrypts/inspects SSL/TLS traffic |

**Basic components of a firewall rule:**
- **Source address** — where the traffic is coming from
- **Destination address** — where the traffic is going
- **Port** — the specific port involved
- **Protocol** — the protocol in use (TCP, UDP, etc.)
- **Action** — what the firewall does with matching traffic
- **Direction** — which way the traffic is flowing

**Types of actions:**
- **Allow** — permit the traffic through
- **Deny** — block the traffic
- **Forward** — pass the traffic on to another destination/network segment

**Rule directionality:**
- **Inbound rules** — govern traffic coming *into* the network/device
- **Outbound rules** — govern traffic leaving the network/device
- **Forward rules** — govern traffic passing *through* a device to another
  destination

**Windows Defender Firewall** is Microsoft's built-in firewall, offering
core functionality to allow/deny specific programs or build fully
customised rules. The room walked through the **step-by-step process** of
creating a custom rule directly in Windows Defender Firewall's interface.

**Linux firewall tools:**
- **Netfilter** — the underlying Linux kernel framework firewalls are built on
- **iptables** — a traditional, widely-used command-line firewall tool
- **nftables** — the modern successor to iptables
- **firewalld** — a dynamic firewall management tool, often used on
  Red Hat-based distros
- **UFW (Uncomplicated Firewall)** — a simplified, user-friendly frontend for
  managing firewall rules, common on Ubuntu/Debian systems

## 🛠️ Key Terms Introduced

- Stateless vs Stateful vs Proxy vs Next-Generation firewalls
- Firewall rule components: source, destination, port, protocol, action, direction
- Inbound / Outbound / Forward rules
- Windows Defender Firewall
- iptables, nftables, firewalld, UFW

## ❓ Questions I Had / Things to Revisit

- Want hands-on practice actually writing `iptables` or `ufw` rules in a
  Linux VM, not just knowing the tool names
- Want to understand SSL/TLS inspection a bit deeper — how does a proxy or
  NGFW decrypt encrypted traffic without breaking the connection?
- Curious how firewall logs specifically feed into a SIEM — this seems like
  a natural link back to the Introduction to SIEM room

## ✅ Self-Check

Could I explain this to someone else without notes? **Yes** — I can explain
the four firewall types, rule components, and directionality confidently.
Actual command-line rule-writing is what I'd want more practice with.

---

*Firewalls are one of the "Technology" pillar tools mentioned back in SOC
Fundamentals — seeing the actual rule structure here makes that piece much
more concrete. Want to eventually set up UFW or iptables rules in my home
lab and generate logs to feed into Splunk/ELK.*
