# 📖 Glossary — Cyber Security 101 Path

A one-stop revision and quick-reference file covering every major term
from the TryHackMe Cyber Security 101 path — both the 12 rooms with full
deep-dive writeups, and the remaining rooms completed but documented only
in the path summary. Organised by module, with plain-English definitions
and real-world scenario examples where useful.

> 💡 **How to use this file:** skim a section before an interview, before
> a related SOC Level 1 room, or whenever a term feels fuzzy — faster than
> re-reading a full writeup.

---

## Module 1 — Introduction

**Offensive vs Defensive Security** — see Pre Security glossary for full
definitions; this path built on both with much more hands-on practice.

**Search Skills** — effective use of search engines/documentation
(including advanced search operators) to research vulnerabilities, tools,
and techniques efficiently — a foundational but often overlooked skill.

---

## Module 2 — Linux Fundamentals

**Linux Fundamentals (Parts 1-3)** — progressively deeper coverage of the
Linux CLI beyond the Pre Security basics: file manipulation
(`cp`, `mv`, `rm`, `mkdir`), text processing (`grep`, `sed`, `awk`), package
management (`apt`), process management (`ps`, `kill`), and permissions
(`chmod`, `chown`).

*Scenario: `grep -r "password" /var/www/` recursively searches all files
under a web directory for the word "password" — a common first step when
hunting for hardcoded credentials during a security review.*

---

## Module 3 — Windows and AD Fundamentals

**Windows Fundamentals (1-3)** — core Windows OS concepts: Control Panel,
Task Manager, Registry, Services, Event Viewer, User Account Control (UAC).

**Active Directory (AD)** — Microsoft's directory service for managing
users, computers, and permissions across a Windows network domain.

**Domain Controller (DC)** — the server running Active Directory,
authenticating users and enforcing domain policies.

**Domain vs Workgroup** — a domain is centrally managed (via AD); a
workgroup is a small, decentralised peer-to-peer network with no central
authority.

*Scenario: In a company using AD, logging into any domain-joined computer
with the same corporate credentials works because authentication is
centrally handled by the Domain Controller — not stored locally on each
machine.*

---

## Module 4 — Command Line

**Windows Command Line (cmd)** — `dir`, `cd`, `ipconfig`, `tasklist`,
`netstat`, `whoami`.

**Windows PowerShell** — a more powerful, scripting-capable shell than
cmd; commands are called **cmdlets** (verb-noun format, e.g.
`Get-Process`). Heavily used by both defenders (automation) and attackers
(fileless malware, living-off-the-land techniques).

**Linux Shells** — different shell environments (`bash`, `sh`, `zsh`) that
interpret commands; `bash` is the most common default on major distros.

*Scenario: PowerShell's `Get-Process | Where-Object {$_.CPU -gt 50}` lists
all processes using more than 50% CPU — useful for a defender investigating
a possibly malicious resource-heavy process.*

---

## Module 5 — Networking

**Networking Concepts / Essentials** — reinforcement of OSI layers, IP
addressing, subnetting basics.

**Core Protocols** — see full writeup: `networking-core-protocols.md`
(DNS, HTTP/HTTPS, FTP, SMTP, POP3, IMAP with ports and commands).

**Secure Protocols** — the encrypted counterparts of common protocols:
**HTTPS** (vs HTTP), **SFTP/FTPS** (vs FTP), **SSH** (vs Telnet), **SMTPS/
IMAPS** (vs SMTP/IMAP) — all adding TLS/SSL encryption to protect data in
transit.

**Wireshark** — see full writeup: `wireshark-the-basics.md` (packet
capture/analysis GUI tool).

**Tcpdump** — a command-line packet capture tool (Wireshark's CLI
equivalent), useful on servers without a GUI.
*Example: `tcpdump -i eth0 port 80` captures only HTTP traffic on
interface eth0.*

**Nmap** — the industry-standard network scanning tool, used to discover
live hosts, open ports, and running services.
*Example: `nmap -sV 192.168.1.0/24` scans an entire subnet and attempts to
identify service versions on any open ports found.*

---

## Module 6 — Cryptography

**Cryptography Basics** — encryption fundamentals (see Pre Security
glossary for symmetric vs asymmetric).

**Public Key Cryptography** — asymmetric encryption in practice: a
**public key** (shareable, used to encrypt or verify) and a **private
key** (secret, used to decrypt or sign). Powers HTTPS, SSH keys, and
digital signatures.

**Hashing** — see full writeup: `hashing-basics.md` (MD5, SHA-1, SHA-256,
collisions, rainbow tables, HMAC).

**John the Ripper** — a widely used password-cracking tool, supporting
dictionary attacks, brute force, and rule-based mutations against hashed
passwords.
*Example: `john --wordlist=rockyou.txt hashes.txt` attempts to crack
password hashes using a common leaked-password wordlist.*

---

## Module 7 — Exploitation Basics

**CVE (Common Vulnerabilities and Exposures)** — a unique ID assigned to a
publicly disclosed vulnerability (e.g. `CVE-2024-21413`, the "Moniker
Link" Outlook vulnerability covered in this module).

**Metasploit Framework** — a widely used penetration testing framework for
developing, testing, and executing exploit code against target systems.
Key components: **modules** (exploits, payloads, auxiliary), **msfconsole**
(the CLI interface).

**Meterpreter** — an advanced Metasploit payload providing an interactive,
in-memory shell on a compromised system, letting an attacker/pentester
run commands, escalate privileges, or pivot further into a network.

**"Blue" (room)** — a beginner-friendly guided exploitation of the
EternalBlue vulnerability (MS17-010, used in the WannaCry ransomware
outbreak) via Metasploit — a good practical demonstration of how a single
unpatched vulnerability enabled a global-scale attack.

*Scenario: EternalBlue exploited a flaw in Windows SMBv1 — a textbook case
of why patch management (covered in Vulnerability Scanner Overview) is
critical: this single unpatched vulnerability caused billions in damages
worldwide via WannaCry.*

---

## Module 8 — Web Hacking

**Web Application Basics** — how web apps are structured (frontend/
backend, client-server requests, sessions).

**JavaScript Essentials** — client-side scripting; relevant to security via
**XSS (Cross-Site Scripting)**, where malicious JS is injected and executed
in a victim's browser.

**SQL Fundamentals** — see Pre Security glossary for SQL Injection basics;
this module goes deeper into actual query manipulation.

**Burp Suite** — the industry-standard web application testing tool,
acting as an intercepting proxy between browser and server, letting
testers view/modify requests in transit.

*Scenario: Using Burp Suite's "Repeater" tool, a tester can intercept a
login request, modify the username parameter to include an SQL injection
payload, and resend it to see if the application is vulnerable.*

---

## Module 9 — Offensive Security Tooling

**Hydra** — a fast, flexible online password-cracking tool, supporting
brute-force/dictionary attacks against many protocols (SSH, FTP, HTTP
login forms, etc.).

**Gobuster** — a tool for brute-forcing directories/files on web servers,
or subdomains, to discover hidden content not linked publicly.
*Example: `gobuster dir -u http://target.com -w wordlist.txt` finds hidden
directories like `/admin` or `/backup`.*

**Shells Overview** — the difference between a **bind shell** (victim
listens, attacker connects) and a **reverse shell** (victim connects back
out to the attacker) — reverse shells are more common since they more
easily bypass inbound firewall restrictions.

**SQLMap** — an automated SQL injection detection and exploitation tool,
capable of identifying and exploiting SQLi vulnerabilities across many
database types.

---

## Module 10 — Defensive Security

Covered in full writeups: `soc-fundamentals.md`,
`digital-forensics-fundamentals.md`, `incident-response-fundamentals.md`,
`logs-fundamentals.md`.

**Quick recall:**
- **SOC** = People (L1/L2/Engineer/Manager) + Process (triage, 5 Ws) +
  Technology (SIEM/EDR/Firewall)
- **Forensics methodology** = Collection → Examination → Analysis →
  Reporting
- **IR frameworks** = SANS PICERL (6 phases) vs NIST (4 phases)
- **Logs** = System, Audit, Security, Network, Access, Application

---

## Module 11 — Security Solutions

Covered in full writeups: `introduction-to-siem.md`,
`firewall-fundamentals.md`, `ids-fundamentals.md`,
`vulnerability-scanner-overview.md`.

**Quick recall:**
- **SIEM** = centralises + normalises + correlates + alerts + dashboards
- **Firewall types** = Stateless, Stateful, Proxy, Next-Gen (NGFW)
- **IDS** = HIDS/NIDS deployment, Signature/Anomaly/Hybrid detection (Snort
  example)
- **CVE** = what the vulnerability is; **CVSS** = how severe it is (0-10)

---

## Module 12 — Defensive Security Tooling

**CyberChef** — see full writeup: `cyberchef-the-basics.md` (the "Swiss
Army knife" for decoding/encoding data).

**CAPA** — a tool that automatically identifies capabilities in executable
files (e.g. "this binary can create files," "this binary can access the
registry") to speed up malware triage without full reverse engineering.

**REMnux** — a Linux toolkit distribution specifically built for malware
analysis, bundling many reverse engineering and analysis tools together.

**FlareVM** — a Windows-based toolkit distribution (from Mandiant/
FireEye) similarly bundling malware analysis and reverse engineering
tools, as the Windows counterpart to REMnux.

**Google Dorking** — using advanced Google search operators (`site:`,
`filetype:`, `intitle:`, `inurl:`) to find exposed sensitive information
indexed by search engines.
*Example: `site:example.com filetype:pdf confidential` searches for
potentially exposed confidential PDF documents on a specific domain.*

---

## Module 13 — Build Your Cyber Security Career

**Security Principles** — foundational ideas like least privilege, defense
in depth, and separation of duties that underpin most security decisions.

**Careers in Cyber** — the breadth of roles available (SOC, GRC, pentest,
forensics, AppSec) and how they interconnect (see SOC Role in Blue Team
writeup from SOC Level 1 for a deeper breakdown).

**Training Impact on Teams** — the case for continuous security training
and awareness programs reducing organisational risk over time.

---

## Module 14 — OWASP Top 10 (2025)

**OWASP (Open Web Application Security Project)** — a nonprofit producing
widely referenced web application security resources, most famously the
**OWASP Top 10** — the ten most critical web application security risks.

**IAAA Failures** — issues in **Identification, Authentication,
Authorization, Accountability** — e.g. broken login systems, missing
access controls.

**Application Design Flaws** — architectural/design-level weaknesses baked
into an application from the start, harder to fix than a simple code bug.

**Insecure Data Handling** — improper storage, transmission, or exposure
of sensitive data (e.g. unencrypted data at rest, exposing data in error
messages).

*Scenario: An e-commerce site storing credit card numbers in plaintext in
its database, then accidentally exposing a debug endpoint that dumps raw
database records, combines an Insecure Data Handling flaw with an
Application Design Flaw — exactly the kind of layered risk OWASP's Top 10
is designed to help teams catch before launch.*

---

## 🧠 Quick Self-Test

- [ ] What's the difference between a bind shell and a reverse shell?
- [ ] What does CVE-2024-21413 (Moniker Link) affect, and why does it
      matter?
- [ ] What's the difference between Nmap and Wireshark's use cases?
- [ ] What are the SANS PICERL phases, in order?
- [ ] What's the difference between REMnux and FlareVM?
- [ ] What are the 4 SIEM features covered in Introduction to SIEM?
- [ ] Give one real Google Dork example and what it searches for.
- [ ] What's the difference between IDS and a firewall?

---

*Companion file to `glossary-presecurity.md`. Next up: `glossary-soclevel1.md`,
to be built the same way once that path is complete.*
